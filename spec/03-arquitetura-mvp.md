# 03 — Arquitetura MVP

## 1. Objetivo da arquitetura MVP

Construir o menor sistema funcional capaz de:

1. receber texto ou áudio;
2. transformar entrada em tarefa estruturada;
3. fragmentar tarefa ampla;
4. criar execução de 25 minutos;
5. realizar follow-up ativo;
6. registrar resposta do usuário;
7. concluir, reagendar ou reduzir a execução.

## 2. Componentes principais

```text
WhatsApp/App
   ↓
Webhook de entrada
   ↓
Normalizador de entrada
   ↓
Transcrição de áudio, se necessário
   ↓
Execution Agent
   ↓
Banco de dados
   ↓
Fila de follow-up
   ↓
Mensagem ativa ao usuário
```

## 3. Stack inicial recomendada

### Entrada

- WhatsApp via Evolution API, WhatsApp Cloud API ou interface de teste.
- App próprio em fase futura.

### Orquestração

- n8n no MVP inicial.
- LangGraph em fase posterior, quando a lógica de estado ficar mais complexa.

### IA

- Modelo LLM para interpretação, fragmentação e resposta estruturada.
- Transcrição de áudio por OpenAI ou equivalente.

### Banco de dados

- PostgreSQL/Supabase para tarefas, execuções, logs e memória estruturada.

### Follow-up

- BullMQ + Redis para jobs de cobrança ativa.
- Alternativa temporária: n8n Schedule/Wait nodes, apenas para protótipo.

## 4. Agente inicial

O MVP começa com um único agente principal:

```text
Execution_Agent
```

Responsabilidades:

- interpretar a mensagem do usuário;
- classificar a intenção;
- criar tarefa, subtarefa, entrega ou execução;
- impedir que tarefa ampla seja tratada como execução;
- responder com o próximo passo operacional;
- interpretar `acabei`, `não acabei` e `travei`.

## 5. Fluxo de áudio

```text
Usuário envia áudio
   ↓
Sistema baixa o arquivo
   ↓
Transcrição
   ↓
Texto transcrito vira user_message
   ↓
Execution_Agent processa normalmente
```

## 6. Fluxo de execução

```text
Usuário cria tarefa ampla
   ↓
Sistema cria nível 1
   ↓
Sistema fragmenta em nível 2 ou 3
   ↓
Sistema gera execução nível 4
   ↓
Usuário inicia bloco
   ↓
Sistema agenda cobrança em 25 minutos
   ↓
Usuário responde
   ↓
Sistema conclui, divide ou reagenda
```

## 7. Decisão arquitetural importante

O follow-up ativo não deve depender apenas da memória do chat nem de prompt. Ele deve ser controlado por estado persistente e fila de jobs.

Motivo: para TDAH, o valor central do produto é lembrar, cobrar, insistir e ajudar a retomar. Se o follow-up falhar, o sistema perde sua função principal.

## 8. Limites do MVP

O MVP deve evitar:

- multiagentes complexos;
- dashboards sofisticados;
- análise preditiva;
- integrações excessivas;
- planejamento semanal automático avançado.

Antes disso, o ciclo essencial precisa funcionar muito bem:

```text
criar → fragmentar → iniciar → cobrar → responder → concluir/replanejar
```
