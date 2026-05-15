# 05 — Follow-up Ativo

## 1. Princípio

O follow-up ativo é o núcleo do CogniFlow.

Para o usuário com TDAH, não basta registrar uma tarefa. O sistema precisa acompanhar a execução, cobrar retorno, detectar silêncio, reduzir tarefa quando houver travamento e puxar o usuário de volta para a conclusão.

## 2. Ciclo básico

```text
Execução iniciada
   ↓
Agendar follow-up para T+25min
   ↓
Perguntar: você concluiu?
   ↓
Usuário responde
   ↓
Sistema decide: concluir, continuar, dividir ou reagendar
```

## 3. Estágios de follow-up

### Estágio 1 — Cobrança normal

Enviado ao final do bloco de 25 minutos.

```text
Você concluiu a execução atual?
Responda: acabei, não acabei ou travei.
```

### Estágio 2 — Retomada leve

Enviado se não houver resposta após período curto.

```text
Você ainda está nessa tarefa?
Responda só uma palavra: acabei, não acabei ou travei.
```

### Estágio 3 — Intervenção de redução

Enviado se houver silêncio prolongado ou resposta de travamento.

```text
Vamos reduzir. Faça apenas o primeiro micro-passo: abrir o arquivo e escrever uma frase inicial.
```

### Estágio 4 — Reagendamento

Se o usuário não responder ou não conseguir concluir, o sistema deve reagendar sem punição.

```text
Vou reagendar essa execução e manter a próxima ação pronta para retomada.
```

## 4. Respostas do usuário

### `acabei`

Ação:

- marcar execução como concluída;
- registrar horário;
- recomendar pausa de 5 minutos;
- buscar próxima execução.

### `não acabei`

Ação:

- perguntar se deseja mais um bloco ou divisão;
- manter contexto da tarefa;
- evitar gerar nova frente automaticamente.

### `travei`

Ação:

- reduzir a tarefa;
- gerar micro-passo de 2 a 5 minutos;
- remover exigência de perfeição;
- manter o usuário em movimento mínimo.

## 5. Estados mínimos

Toda execução ativa deve controlar:

```text
status
scheduled_start
scheduled_end
followup_stage
last_followup_at
next_followup_at
attempt_count
execution_session_id
```

## 6. Regras de tom

O follow-up deve ser:

- direto;
- curto;
- não punitivo;
- orientado à próxima ação;
- resistente ao silêncio;
- focado em conclusão.

O sistema não deve usar frases que aumentem vergonha ou culpa.

## 7. Regra de ouro

Antes de criar multiagentes sofisticados, RAG amplo ou análise comportamental avançada, o sistema precisa executar bem este ciclo:

```text
criar execução
iniciar execução
cobrar retorno
detectar silêncio
reintervir
concluir ou replanejar
puxar próxima execução
```

Se esse ciclo funcionar, o restante do sistema pode crescer em cima.
