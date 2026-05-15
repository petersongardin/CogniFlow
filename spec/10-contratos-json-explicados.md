# 10 — Contratos JSON explicados

## 1. O que é um contrato JSON

Um contrato JSON é um combinado fixo sobre como uma informação deve ser escrita para que o sistema entenda sem ambiguidade.

Em linguagem simples:

```text
Contrato JSON = formulário padrão que a IA deve preencher.
```

Ele serve para impedir que a IA responda cada vez de um jeito diferente.

## 2. Por que o CogniFlow precisa disso

O CogniFlow não pode depender de respostas soltas como:

```text
Legal, vou dividir sua tarefa em partes menores.
```

O sistema precisa de respostas estruturadas, como:

```json
{
  "type": "minitaf",
  "title": "Abrir o relatório e criar os títulos principais",
  "duration_minutes": 25,
  "break_minutes": 5,
  "status": "pending"
}
```

Assim o banco, o follow-up e a interface sabem exatamente o que fazer.

## 3. Analogia simples

Imagine que o CogniFlow tem gavetas.

Cada gaveta aceita apenas um tipo de informação:

- gaveta de projeto;
- gaveta de etapa;
- gaveta de entrega;
- gaveta de Minitaf;
- gaveta de sintoma;
- gaveta de follow-up;
- gaveta de resposta do usuário.

O contrato JSON define o formato correto de cada gaveta.

## 4. Exemplo: contrato de Projeto

Quando o usuário envia um projeto inteiro, a IA deve preencher algo assim:

```json
{
  "type": "project",
  "user_id": "joao",
  "title": "VitisOnFarm",
  "description": "Avaliação da sustentabilidade na viticultura com uso de biológicos on farm",
  "deadline": "2026-05-31",
  "status": "active",
  "source": "pdf"
}
```

## 5. Exemplo: contrato de Etapa

```json
{
  "type": "stage",
  "user_id": "joao",
  "parent_project": "VitisOnFarm",
  "title": "Etapa 1 — Estudo comparativo entre manejo biológico e manejo convencional",
  "status": "pending"
}
```

## 6. Exemplo: contrato de Entrega

```json
{
  "type": "deliverable",
  "user_id": "joao",
  "parent_stage": "Etapa 1",
  "title": "Tabela com avaliações de campo realizadas no projeto",
  "acceptance_criteria": "Tabela criada com avaliação, frequência, local, responsável e status",
  "status": "pending"
}
```

## 7. Exemplo: contrato de Minitaf

```json
{
  "type": "minitaf",
  "user_id": "joao",
  "parent_deliverable": "Tabela com avaliações de campo realizadas no projeto",
  "title": "Listar as avaliações da Etapa 1 em uma tabela simples",
  "action_verb": "Listar",
  "duration_minutes": 25,
  "break_minutes": 5,
  "acceptance_criteria": "Tabela com pelo menos 5 avaliações criada no documento",
  "status": "pending",
  "is_executable": true
}
```

## 8. Exemplo: contrato de Sintoma de Iniciação

```json
{
  "type": "initiation_symptom",
  "user_id": "joao",
  "task_context": "Relatório final VitisOnFarm",
  "symptom": "coceira ao pensar em iniciar",
  "intensity": 4,
  "moment": "before_start"
}
```

## 9. Exemplo: contrato de Follow-up

```json
{
  "type": "followup",
  "user_id": "joao",
  "minitaf_title": "Listar as avaliações da Etapa 1 em uma tabela simples",
  "scheduled_for": "2026-05-15T10:30:00-03:00",
  "followup_stage": 1,
  "message": "Você concluiu a Minitaf? Responda: acabei, não acabei ou travei.",
  "status": "scheduled"
}
```

## 10. Exemplo: contrato de Resposta do Usuário

```json
{
  "type": "user_execution_response",
  "user_id": "joao",
  "response": "travei",
  "interpreted_status": "blocked",
  "next_action": "reduce_minitaf"
}
```

## 11. Regra prática

O usuário não precisa escrever JSON.

O usuário escreve ou fala normalmente:

```text
Estou travado, não consigo começar o relatório.
```

O CogniFlow transforma isso internamente em JSON:

```json
{
  "type": "user_execution_response",
  "response": "travei",
  "interpreted_status": "blocked",
  "next_action": "reduce_minitaf"
}
```

## 12. Por que isso importa

Sem contrato JSON:

- a IA pode responder bonito, mas o sistema não sabe o que salvar;
- o banco recebe dados bagunçados;
- o follow-up falha;
- o usuário perde estado;
- o sistema não escala para multiusuário.

Com contrato JSON:

- cada tarefa tem dono;
- cada Minitaf tem status;
- cada follow-up tem horário;
- cada resposta gera uma próxima ação;
- o sistema consegue continuar de onde parou.

## 13. Regra para o desenvolvimento

Durante a conversa com o usuário, o CogniFlow responde em linguagem simples.

Internamente, o agente sempre deve produzir ou atualizar estruturas padronizadas.

Formulação:

```text
Para o usuário: mensagem simples.
Para o sistema: JSON estruturado.
```

## 14. Próximo passo técnico

Depois desta explicação, a próxima especificação deve definir os contratos oficiais em formato rígido para implementação.

Arquivo futuro:

```text
spec/11-contratos-json-oficiais.md
```
