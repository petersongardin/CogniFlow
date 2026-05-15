# 08 — Diagnóstico Executivo do TDAH aplicado ao CogniFlow

## 1. Objetivo deste documento

Registrar os padrões executivos que o CogniFlow deve compensar.

O sistema não deve ser tratado como um simples gerenciador de tarefas. Ele deve funcionar como uma prótese executiva externa para compensar dificuldades específicas de iniciação, tempo, memória de trabalho, persistência e regulação.

## 2. Diagnóstico objetivo

### 2.1 Desconto do futuro

O usuário tende a subestimar o valor de recompensas ou consequências futuras e priorizar alívios imediatos.

Consequência no sistema:

- tarefas importantes, mas distantes, são adiadas;
- o sistema deve tornar o custo futuro visível no presente;
- prazos devem ser convertidos em pressão operacional diária, não em lembrete genérico.

Regra de produto:

```text
Toda tarefa com prazo deve mostrar o custo concreto da não execução hoje.
```

Exemplo:

```text
Se você não iniciar esta Minitaf agora, o relatório continuará sem estrutura e o prazo de 31/05 ficará mais crítico.
```

### 2.2 Iniciação de tarefas

O usuário sabe o que fazer, mas não começa. A energia de ativação é alta.

Consequência no sistema:

- o primeiro passo precisa ser pequeno, concreto e imediato;
- o sistema deve reduzir a fricção inicial;
- a primeira Minitaf deve ser mais fácil do que a tarefa real parece.

Regra de produto:

```text
Quando houver resistência, reduzir a tarefa até um micro-passo de 2 a 5 minutos.
```

### 2.3 Persistência e conclusão

O usuário pode abrir muitos ciclos e não fechar entregas.

Consequência no sistema:

- o sistema deve detectar tarefas abertas;
- deve evitar abrir nova frente sem decisão explícita sobre a tarefa ativa;
- deve diferenciar movimento de entrega.

Regra de produto:

```text
Nenhuma nova frente crítica deve ser aberta enquanto houver uma Minitaf ativa sem conclusão, pausa ou reagendamento.
```

### 2.4 Regulação emocional e de energia

Sono, álcool, estresse, frustração e sobrecarga alteram diretamente a capacidade de execução.

Consequência no sistema:

- o sistema deve permitir registrar energia, sono, estresse e sintomas;
- a dificuldade de execução deve ser interpretada com contexto;
- em baixa energia, o sistema deve reduzir a Minitaf, não aumentar cobrança abstrata.

Regra de produto:

```text
Baixa energia muda o tamanho da Minitaf, não elimina a necessidade de avanço mínimo.
```

### 2.5 Gestão do tempo — time blindness

O usuário tem dificuldade em estimar duração, perceber atraso e sequenciar ações.

Consequência no sistema:

- o sistema deve transformar tempo abstrato em blocos visíveis;
- deve mostrar prazo, atraso e próxima ação;
- deve usar contagem de Minitafs em vez de duração ampla.

Exemplo:

```text
Relatório final estimado: 18 Minitafs.
Hoje precisamos concluir 4 Minitafs para reduzir o atraso.
```

Regra de produto:

```text
Todo projeto grande deve ser traduzido em número estimado de Minitafs.
```

### 2.6 Memória de trabalho fraca

O usuário perde contexto após interrupções.

Consequência no sistema:

- o sistema deve manter estado externo da tarefa;
- deve lembrar o que estava ativo;
- deve permitir retomada com contexto mínimo.

Formato de retomada:

```text
Você estava executando: [Minitaf atual].
Último estado: [acabei/não acabei/travei/sem resposta].
Próximo passo: [ação concreta].
```

Regra de produto:

```text
O usuário nunca deve depender da própria memória para saber onde parou.
```

### 2.7 Busca por novidade e dopamina

O usuário pode abandonar tarefas quando deixam de ser estimulantes e buscar conversas, ideias ou projetos novos.

Consequência no sistema:

- o sistema deve detectar dispersão;
- deve reconhecer a nova ideia sem abandonar a tarefa ativa;
- deve estacionar a ideia em backlog e retornar à execução atual.

Regra de produto:

```text
Novas ideias devem ser capturadas, mas não devem sequestrar a execução ativa.
```

Exemplo:

```text
Ideia registrada no backlog. Agora volte para a Minitaf ativa: escrever o sumário provisório do relatório.
```

## 3. Tabela de compensação do CogniFlow

| Dificuldade executiva | Compensação do CogniFlow |
|---|---|
| Desconto do futuro | Lembrança concreta do custo da não execução |
| Iniciação difícil | Minitaf pequena e micro-passo inicial |
| Falta de conclusão | Follow-up ativo e bloqueio de nova frente |
| Oscilação emocional/energia | Registro de estado e ajuste do tamanho da Minitaf |
| Time blindness | Blocos de 25+5, contagem de Minitafs e prazo visível |
| Memória de trabalho fraca | Estado persistente e retomada contextual |
| Busca por novidade | Captura em backlog e retorno à tarefa ativa |

## 4. Regra-mãe

O CogniFlow deve transformar:

```text
futuro abstrato → consequência presente
projeto grande → Minitafs pequenas
intenção → próxima ação
memória interna → estado externo
culpa → reentrada operacional
novidade dispersiva → backlog
movimento → entrega
```

## 5. Critério de sucesso

O sistema funciona quando reduz a distância entre saber o que deve ser feito e efetivamente iniciar, persistir e concluir.
