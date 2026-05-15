# 04 — Modelo de Dados

## 1. Objetivo

Definir o modelo mínimo de dados necessário para representar projetos, tarefas, entregas, execuções, follow-ups e logs comportamentais.

## 2. Entidade principal: tasks

A tabela `tasks` representa todos os níveis da árvore de trabalho.

```sql
CREATE TABLE tasks (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  user_id TEXT NOT NULL,
  parent_id UUID REFERENCES tasks(id),
  title TEXT NOT NULL,
  description TEXT,
  nivel INT NOT NULL CHECK (nivel BETWEEN 1 AND 4),
  status TEXT NOT NULL DEFAULT 'pending',
  is_executable BOOLEAN NOT NULL DEFAULT false,
  prioridade INT DEFAULT 2 CHECK (prioridade BETWEEN 1 AND 3),
  duracao_min INT DEFAULT 25,
  scheduled_start TIMESTAMPTZ,
  scheduled_end TIMESTAMPTZ,
  started_at TIMESTAMPTZ,
  completed_at TIMESTAMPTZ,
  created_at TIMESTAMPTZ DEFAULT NOW(),
  updated_at TIMESTAMPTZ DEFAULT NOW()
);
```

## 3. Níveis de tarefa

```text
1 = Projeto ou tarefa ampla
2 = Subtarefa
3 = Entrega
4 = Execução concreta
```

Regra obrigatória:

```text
Somente nivel = 4 pode ter is_executable = true.
```

## 4. Status sugeridos

```text
pending      = criado, mas ainda não iniciado
active       = execução em andamento
done         = concluído
blocked      = travado
rescheduled  = reagendado
cancelled    = cancelado
```

## 5. Tabela execution_sessions

Representa cada ciclo real de execução.

```sql
CREATE TABLE execution_sessions (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  user_id TEXT NOT NULL,
  task_id UUID NOT NULL REFERENCES tasks(id),
  status TEXT NOT NULL DEFAULT 'active',
  started_at TIMESTAMPTZ DEFAULT NOW(),
  expected_end_at TIMESTAMPTZ,
  ended_at TIMESTAMPTZ,
  result TEXT,
  created_at TIMESTAMPTZ DEFAULT NOW()
);
```

## 6. Tabela followup_jobs

Representa cobranças agendadas e seus estágios.

```sql
CREATE TABLE followup_jobs (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  user_id TEXT NOT NULL,
  task_id UUID REFERENCES tasks(id),
  execution_session_id UUID REFERENCES execution_sessions(id),
  followup_stage INT NOT NULL DEFAULT 1,
  status TEXT NOT NULL DEFAULT 'scheduled',
  scheduled_for TIMESTAMPTZ NOT NULL,
  sent_at TIMESTAMPTZ,
  answered_at TIMESTAMPTZ,
  attempt_count INT DEFAULT 0,
  created_at TIMESTAMPTZ DEFAULT NOW()
);
```

## 7. Tabela execution_logs

Registra eventos importantes do sistema.

```sql
CREATE TABLE execution_logs (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  user_id TEXT NOT NULL,
  task_id UUID REFERENCES tasks(id),
  execution_session_id UUID REFERENCES execution_sessions(id),
  event_type TEXT NOT NULL,
  event_payload JSONB,
  created_at TIMESTAMPTZ DEFAULT NOW()
);
```

## 8. Tabela behavior_logs

Opcional no MVP, mas importante para evolução.

```sql
CREATE TABLE behavior_logs (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  user_id TEXT NOT NULL,
  log_date DATE DEFAULT CURRENT_DATE,
  sono_h FLOAT,
  energia INT CHECK (energia BETWEEN 1 AND 5),
  estresse INT CHECK (estresse BETWEEN 1 AND 5),
  alcool BOOLEAN,
  notas TEXT,
  created_at TIMESTAMPTZ DEFAULT NOW()
);
```

## 9. Índices mínimos

```sql
CREATE INDEX idx_tasks_user_status ON tasks(user_id, status);
CREATE INDEX idx_tasks_parent ON tasks(parent_id);
CREATE INDEX idx_tasks_scheduled_start ON tasks(scheduled_start);
CREATE INDEX idx_followup_jobs_scheduled ON followup_jobs(status, scheduled_for);
CREATE INDEX idx_execution_logs_task ON execution_logs(task_id);
```

## 10. Regra de integridade lógica

Toda execução ativa deve ter:

- `task_id` apontando para uma task de nível 4;
- `is_executable = true`;
- `status = active`;
- uma sessão em `execution_sessions`;
- ao menos um follow-up agendado.
