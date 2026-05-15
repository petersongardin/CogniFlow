# 07 — Iniciação, Sintomas de Resistência e Feedback Sensorial

## 1. Princípio central

No TDAH, o problema muitas vezes não é entender a tarefa nem saber executá-la tecnicamente. O gargalo crítico está na iniciação.

O usuário pode compreender perfeitamente o que precisa fazer, mas sentir resistência intensa ao começar, especialmente quando a tarefa é obrigatória, atrasada, emocionalmente carregada ou grande demais.

## 2. Hipótese operacional do CogniFlow

O CogniFlow deve tratar a dificuldade de iniciar como um evento observável, registrável e manejável.

A resistência de iniciação pode aparecer como:

- fuga para conversas paralelas;
- busca por novas ideias;
- troca de assunto;
- organização excessiva antes de executar;
- abertura de novas frentes;
- sensação corporal desagradável;
- irritação;
- sonolência;
- dor de cabeça;
- coceira;
- inquietação;
- vontade de levantar;
- vontade de fazer algo mais fácil;
- sensação de bloqueio mental;
- urgência falsa de resolver outra coisa.

Esses sinais devem ser registrados como parte do estado de execução, não como falha moral do usuário.

## 3. Sintomas corporais de boicote de iniciação

O sistema deve permitir que o usuário registre sintomas sentidos ao pensar em iniciar uma tarefa.

Exemplos:

```text
Sinto coceiras quando penso em iniciar a tarefa obrigatória.
Sinto dor de cabeça antes de começar.
Sinto pressão no corpo.
Sinto irritação.
Sinto vontade de fugir para outra coisa.
```

O objetivo não é diagnosticar clinicamente o sintoma, mas ajudar o usuário a reconhecer padrões de resistência.

## 4. Registro dos sintomas

Cada execução pode ter um registro de sintomas antes, durante ou depois da Minitaf.

Campos sugeridos:

```sql
CREATE TABLE initiation_symptoms (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  user_id TEXT NOT NULL,
  task_id UUID REFERENCES tasks(id),
  execution_session_id UUID REFERENCES execution_sessions(id),
  symptom_type TEXT NOT NULL,
  symptom_description TEXT,
  intensity INT CHECK (intensity BETWEEN 1 AND 5),
  moment TEXT CHECK (moment IN ('before_start', 'during_execution', 'after_execution')),
  created_at TIMESTAMPTZ DEFAULT NOW()
);
```

## 5. Uso prático dos sintomas

Quando o usuário registrar um sintoma, o sistema deve responder de forma curta e operacional.

Exemplo:

```text
PASSO ATUAL
Reconheça isso como resistência de iniciação, não como ordem para parar. Abra o arquivo e faça apenas a primeira Minitaf.

OBJETIVO
Mostrar ao cérebro que a tarefa começou sem precisar enfrentar o projeto inteiro.

PRÓXIMO PASSO
Depois de 25 minutos, responda: acabei, não acabei ou travei.
```

## 6. Lembrança ativa do custo da não execução

O CogniFlow deve lembrar o usuário, de forma direta e não punitiva, do problema concreto que será criado caso a tarefa não seja executada.

Essa lembrança deve ser factual, curta e relacionada ao prazo.

Exemplo:

```text
Essa tarefa vence em 31/05. Se você não iniciar agora, o relatório continuará atrasado e a pressão aumentará hoje à noite.
```

O sistema não deve usar culpa genérica. Deve usar consequência concreta.

## 7. Regra para tarefas atrasadas

Quando uma tarefa estiver atrasada ou próxima do prazo, o sistema deve aumentar a frequência e a objetividade do follow-up.

Critérios:

- prazo em até 7 dias;
- tarefa essencial ainda não iniciada;
- relatório ou entrega obrigatória;
- usuário dispersando em conversa paralela;
- histórico recente de adiamento.

Comportamento esperado:

```text
Você está conversando sobre o sistema, mas a tarefa crítica é o relatório. A próxima Minitaf é pequena: abrir o arquivo e escrever o sumário provisório.
```

## 8. Minitaf como unidade cognitiva visual, sonora e pequena

O TDAH tende a responder melhor a comandos pequenos, visuais, sonoros e imediatamente executáveis.

Portanto, uma Minitaf deve ser:

- pequena o suficiente para não ameaçar o cérebro;
- visualmente clara;
- se possível, lida em voz alta ou enviada em áudio;
- limitada a uma ação operacional;
- associada a um critério de término visível.

Exemplo ruim:

```text
Fazer o relatório final do projeto.
```

Exemplo correto:

```text
Abrir o documento do relatório e escrever os títulos: Resumo, Objetivo, Metodologia, Resultados, Conclusão.
```

## 9. Regra anti-abstração

O sistema deve evitar comandos abstratos como:

- organizar o projeto;
- resolver o relatório;
- avançar na escrita;
- trabalhar na análise;
- revisar os dados.

Esses comandos devem ser convertidos em Minitafs concretas.

Exemplo:

```text
Comando abstrato: revisar os dados.
Minitaf: abrir a planilha de produtividade e marcar em amarelo as colunas que serão usadas no relatório.
```

## 10. Regra de retorno ao foco

Se o usuário estiver em uma conversa sobre o próprio sistema enquanto há uma tarefa crítica atrasada, o CogniFlow deve registrar a dispersão e redirecionar para a Minitaf atual.

Formato:

```text
PASSO ATUAL
Execute a Minitaf X agora.

OBJETIVO
Reduzir o atraso da entrega Y.

PRÓXIMO PASSO
Volte aqui em 25 minutos e responda: acabei, não acabei ou travei.
```

## 11. Critério de sucesso

Essa funcionalidade é bem-sucedida quando o usuário aprende a reconhecer que sintomas corporais e fuga cognitiva podem ser sinais de resistência de iniciação, e não motivos automáticos para abandonar a tarefa.

O sistema deve ajudar o usuário a transformar esse reconhecimento em ação pequena, imediata e concluível.
