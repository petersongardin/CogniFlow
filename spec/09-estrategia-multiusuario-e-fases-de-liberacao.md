# 09 — Estratégia Multiusuário e Fases de Liberação

## 1. Princípio

O CogniFlow deve nascer com arquitetura robusta e multiusuário, mesmo que o primeiro ciclo de testes seja realizado por apenas um usuário.

A lógica de produto não deve ser construída como um script pessoal rígido. Ela deve ser desenhada desde o início para suportar múltiplos usuários, isolamento de dados, perfis individuais, histórico separado, preferências pessoais e escalabilidade progressiva.

## 2. Estratégia de liberação

A evolução do produto seguirá três fases:

```text
Fase 1 — Uso individual controlado
Fase 2 — Grupo pequeno de usuários com TDAH
Fase 3 — Uso geral
```

## 3. Fase 1 — Uso individual controlado

### Objetivo

Validar o ciclo essencial de execução com um único usuário real.

### Escopo

- entrada por texto e/ou áudio;
- criação de projetos;
- decomposição em Minitafs;
- follow-up ativo;
- registro de sintomas de iniciação;
- resposta a `acabei`, `não acabei` e `travei`;
- retomada de contexto;
- lembrete do custo da não execução.

### Critério de sucesso

O sistema é aprovado para a próxima fase quando conseguir, de forma confiável:

```text
receber tarefa/projeto → fragmentar → iniciar Minitaf → cobrar → interpretar resposta → concluir/replanejar
```

## 4. Fase 2 — Grupo pequeno de usuários TDAH

### Objetivo

Testar variações reais de comportamento, linguagem, resistência de iniciação, sintomas, rotinas e padrões de follow-up.

### Escopo

- múltiplos usuários reais;
- perfis individuais;
- preferências de horário;
- canais de entrada separados;
- isolamento completo de dados;
- coleta de feedback qualitativo;
- ajustes em linguagem, frequência de cobrança e tamanho das Minitafs.

### Critério de sucesso

A fase é bem-sucedida quando o sistema mostra utilidade para diferentes perfis sem depender de ajustes manuais para cada pessoa.

## 5. Fase 3 — Uso geral

### Objetivo

Disponibilizar o CogniFlow para uso amplo, com infraestrutura, segurança e suporte adequados.

### Requisitos antes da abertura geral

- autenticação estável;
- isolamento multiusuário;
- logs de erro;
- monitoramento de filas;
- controle de custos por usuário;
- política de privacidade;
- termos de uso;
- backup de dados;
- painel administrativo mínimo;
- limites de uso;
- rotina de suporte.

## 6. Requisitos multiusuário desde o MVP

Mesmo no uso individual, o banco e a arquitetura devem conter `user_id` como campo obrigatório nas entidades principais.

Entidades que devem ser isoladas por usuário:

```text
tasks
execution_sessions
followup_jobs
execution_logs
behavior_logs
initiation_symptoms
user_preferences
source_documents
```

Regra obrigatória:

```text
Nenhuma consulta operacional pode buscar tarefas, logs, sintomas ou sessões sem filtrar por user_id.
```

## 7. Preferências individuais

Cada usuário deve poder ter preferências próprias.

Campos sugeridos:

```sql
CREATE TABLE user_preferences (
  user_id TEXT PRIMARY KEY,
  timezone TEXT DEFAULT 'America/Sao_Paulo',
  default_focus_minutes INT DEFAULT 25,
  default_break_minutes INT DEFAULT 5,
  preferred_channel TEXT DEFAULT 'whatsapp',
  followup_intensity TEXT DEFAULT 'normal',
  morning_start TIME,
  evening_end TIME,
  language TEXT DEFAULT 'pt-BR',
  created_at TIMESTAMPTZ DEFAULT NOW(),
  updated_at TIMESTAMPTZ DEFAULT NOW()
);
```

## 8. Segurança e privacidade

Como o sistema lidará com tarefas pessoais, profissionais, sintomas, dificuldades executivas e possíveis dados sensíveis, a arquitetura deve considerar privacidade desde o início.

Regras:

- dados de usuários devem ser isolados;
- logs não devem expor informações sensíveis desnecessariamente;
- documentos enviados devem ter vínculo com `user_id`;
- usuários beta devem aceitar termos claros de uso;
- o sistema não deve se apresentar como substituto de atendimento médico ou psicológico.

## 9. Escalabilidade progressiva

O sistema não precisa nascer grande, mas precisa nascer corretamente estruturado.

Estratégia:

```text
começar simples na interface
manter robustez no banco
usar filas para follow-up
separar usuário desde o início
registrar logs operacionais
monitorar erros
expandir agentes apenas depois do ciclo essencial funcionar
```

## 10. Decisão arquitetural

O CogniFlow deve evitar atalhos que funcionam apenas para um usuário, como:

- `user_id` fixo no código;
- tabelas sem dono;
- follow-up sem fila persistente;
- memória compartilhada entre usuários;
- prompts com dados pessoais fixos;
- ausência de logs por usuário;
- ausência de controle de canal.

## 11. Regra de produto

A experiência pode começar pessoal e manual, mas a fundação técnica deve ser multiusuário.

Formulação:

```text
Testar como usuário único. Construir como produto multiusuário.
```

## 12. Critério de avanço entre fases

### Para sair da Fase 1

- pelo menos 30 dias de uso real individual;
- mínimo de 100 Minitafs criadas;
- mínimo de 50 Minitafs concluídas ou replanejadas;
- follow-up ativo funcionando com confiabilidade;
- logs suficientes para revisar padrões de falha.

### Para sair da Fase 2

- grupo pequeno usando por período definido;
- feedback qualitativo coletado;
- erros críticos corrigidos;
- custos por usuário estimados;
- política de privacidade e termos preparados.

### Para abrir uso geral

- autenticação, privacidade, suporte e monitoramento implementados;
- sistema capaz de lidar com falhas sem perder estado de execução;
- documentação mínima de onboarding disponível.
