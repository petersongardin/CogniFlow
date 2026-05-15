# 02 — Requisitos Funcionais

## RF-001 — Receber entrada por texto

O sistema deve receber mensagens de texto enviadas pelo usuário via WhatsApp, app ou interface de teste.

## RF-002 — Receber entrada por áudio

O sistema deve receber áudios enviados pelo usuário e transcrevê-los antes do processamento pela IA.

## RF-003 — Normalizar entrada

O sistema deve converter diferentes tipos de entrada em um formato comum:

```json
{
  "user_id": "string",
  "input_type": "text|audio",
  "user_message": "string",
  "source": "whatsapp|app|test"
}
```

## RF-004 — Classificar intenção

O sistema deve identificar se a mensagem do usuário representa:

- criação de projeto/tarefa ampla;
- resposta a decomposição;
- início de execução;
- conclusão (`acabei`);
- não conclusão (`não acabei`);
- travamento (`travei`);
- reagendamento;
- pedido de agenda;
- tentativa de abrir nova frente.

## RF-005 — Criar projeto/tarefa ampla

Quando o usuário criar uma tarefa ampla, o sistema deve criar um registro de nível 1:

- `nivel = 1`;
- `is_executable = false`;
- `status = pending`.

O sistema não deve iniciar follow-up para tarefas de nível 1.

## RF-006 — Fragmentar tarefa automaticamente

O sistema deve propor decomposição sem exigir que o usuário escreva manualmente todas as subtarefas.

## RF-007 — Hierarquia de tarefas

O sistema deve organizar tarefas em quatro níveis:

```text
Nível 1 = Projeto ou tarefa ampla
Nível 2 = Subtarefa
Nível 3 = Entrega
Nível 4 = Execução concreta
```

Somente nível 4 pode ter `is_executable = true`.

## RF-008 — Gerar execução válida

Uma execução válida deve:

- começar com verbo;
- ter objeto claro;
- ter critério de término;
- caber idealmente em 25 minutos;
- poder ser iniciada imediatamente.

## RF-009 — Iniciar bloco TDAH

Ao iniciar uma execução, o sistema deve:

- marcar a execução como ativa;
- registrar horário de início;
- calcular horário previsto de término;
- agendar follow-up para o fim do bloco.

## RF-010 — Follow-up ativo

Ao final do bloco, o sistema deve perguntar se o usuário concluiu a execução.

Respostas mínimas aceitas:

- `acabei`;
- `não acabei`;
- `travei`.

## RF-011 — Concluir execução

Se o usuário responder `acabei`, o sistema deve:

- marcar execução como concluída;
- registrar `completed_at`;
- buscar próxima execução recomendada;
- orientar pausa ou próximo passo.

## RF-012 — Tratar não conclusão

Se o usuário responder `não acabei`, o sistema deve:

- perguntar se precisa de mais um bloco ou divisão;
- evitar julgamento;
- reagendar ou reduzir a tarefa.

## RF-013 — Tratar travamento

Se o usuário responder `travei`, o sistema deve reduzir a tarefa para um micro-passo.

Exemplo:

```text
Abrir o documento e escrever apenas uma frase ruim sobre o tema.
```

## RF-014 — Evitar dispersão

Se o usuário tentar abrir nova tarefa enquanto existe execução ativa, o sistema deve confirmar se deve pausar/reagendar a execução atual antes de aceitar a nova frente.

## RF-015 — Agenda do dia

O sistema deve permitir consulta das execuções programadas para o dia.

## RF-016 — Registro de histórico

O sistema deve registrar eventos importantes:

- tarefa criada;
- execução iniciada;
- follow-up enviado;
- usuário respondeu;
- execução concluída;
- execução travada;
- execução reagendada.

## RF-017 — Resposta estruturada ao usuário

Durante execução, o sistema deve responder preferencialmente no formato:

```text
PASSO ATUAL
...

OBJETIVO
...

PRÓXIMO PASSO
...
```
