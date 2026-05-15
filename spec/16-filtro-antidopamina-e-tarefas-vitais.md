# 16 — Filtro Antidopamina e Tarefas Vitais

## 1. Princípio

O CogniFlow deve proteger o usuário de trocar tarefas vitais por tarefas de dopamina barata.

No TDAH, o foco pode ser muito intenso quando a tarefa é interessante, nova, criativa ou prazerosa. O problema é que esse foco pode ser desviado daquilo que é prioritário para a vida real do usuário.

O sistema deve ajudar o usuário a focar no que importa, não apenas no que estimula.

## 2. Definição de tarefa dopaminérgica

Uma tarefa dopaminérgica é uma atividade que oferece alívio imediato, novidade, prazer cognitivo ou sensação de progresso, mas desvia o usuário da tarefa vital que precisa ser feita.

Exemplos:

- pesquisar ferramenta nova;
- reorganizar o sistema de tarefas;
- conversar sobre ideias futuras;
- abrir novo projeto;
- melhorar a arquitetura antes de entregar o obrigatório;
- assistir conteúdo sobre produtividade;
- resolver tarefas pequenas e fáceis enquanto evita uma tarefa crítica;
- mexer em configurações;
- escrever especificações quando há entrega atrasada mais importante;
- planejar demais e executar de menos.

## 3. Definição de tarefa vital

Uma tarefa vital é aquela que protege a vida real do usuário.

Categorias principais:

```text
trabalho/emprego
entregas profissionais
desenvolvimento profissional
saúde
sono
boa alimentação
relacionamentos
finanças pessoais
obrigações legais ou institucionais
rotina mínima de estabilidade
```

O CogniFlow deve priorizar tarefas que preservam trabalho, evolução profissional, saúde e estabilidade da vida diária.

## 4. Regra central

```text
O sistema deve reduzir ou bloquear tarefas de dopamina barata quando houver tarefa vital pendente, atrasada ou crítica.
```

Isso não significa proibir criatividade. Significa estacionar a ideia e retornar ao que protege a vida real.

## 5. Diferença entre interesse e prioridade

O sistema deve diferenciar:

```text
O que o usuário quer fazer agora
vs.
O que o usuário precisa fazer agora para proteger seu futuro
```

No TDAH, o foco pode ir para o que gosta, enquanto a tarefa prioritária é evitada.

Regra de produto:

```text
Interesse não define prioridade. Impacto vital define prioridade.
```

## 6. Detecção de fuga dopaminérgica

O CogniFlow deve suspeitar de fuga dopaminérgica quando:

- o usuário muda de assunto enquanto há tarefa crítica ativa;
- o usuário começa a planejar outro sistema em vez de executar a entrega;
- o usuário abre nova ideia durante tarefa atrasada;
- o usuário escolhe tarefa fácil, mas a tarefa vital continua parada;
- o usuário conversa muito sobre execução sem executar;
- o usuário entra em pesquisa, ferramenta ou arquitetura enquanto existe entrega obrigatória próxima;
- a tarefa escolhida dá sensação de avanço, mas não reduz o risco real.

## 7. Resposta padrão à fuga dopaminérgica

A resposta deve ser firme, curta e não humilhante.

Formato:

```text
FOCO
Isso parece dopamina barata: interessante, mas não protege sua tarefa vital agora.

TAREFA VITAL
[Nome da tarefa prioritária]

MINITAF AGORA
[Ação pequena de 25 minutos]

RECOMPENSA
[Benefício concreto de executar]
```

Exemplo:

```text
FOCO
Essa conversa sobre melhorar o sistema é útil, mas agora parece dopamina barata porque o relatório está atrasado.

TAREFA VITAL
Relatório final do projeto.

MINITAF AGORA
Abrir o documento e escrever os títulos principais.

RECOMPENSA
Você reduz o atraso hoje e dorme com menos pressão mental.
```

## 8. Backlog de ideias dopaminérgicas

O CogniFlow não deve descartar ideias novas. Deve capturá-las em um backlog.

Regra:

```text
Ideias novas são registradas, não executadas imediatamente, quando houver tarefa vital ativa.
```

Contrato sugerido:

```json
{
  "type": "dopamine_backlog_item",
  "user_id": "string",
  "title": "string",
  "reason_captured": "new_idea_during_vital_task",
  "related_active_task": "string",
  "status": "parked",
  "review_after": "string"
}
```

## 9. Tarefas vitais de trabalho e profissão

O CogniFlow deve manter uma memória ativa das tarefas que afetam emprego, trabalho e evolução profissional.

Exemplos:

- relatórios;
- prazos institucionais;
- reuniões importantes;
- projetos atrasados;
- entregas combinadas;
- documentos profissionais;
- estudo essencial para carreira;
- escrita científica;
- preparação de apresentações;
- tarefas que melhoram reputação e confiança profissional.

Regra:

```text
Tarefas profissionais com prazo, impacto reputacional ou obrigação externa devem ter prioridade elevada.
```

## 10. Saúde, sono e alimentação como tarefas vitais

O CogniFlow deve lembrar que execução sustentável depende de base fisiológica.

Áreas vitais:

- sono regular;
- alimentação adequada;
- hidratação;
- medicação prescrita, quando o próprio usuário registrar como rotina, sem o sistema orientar alteração;
- movimento físico leve;
- pausa real;
- redução de álcool quando estiver associado a queda de execução;
- rotina de encerramento do dia.

Regra:

```text
Sono, alimentação e saúde não são tarefas secundárias. São infraestrutura da função executiva.
```

## 11. Sono como prioridade superior

O sistema deve evitar que o usuário use trabalho atrasado para destruir o sono de forma recorrente.

Exemplo de intervenção:

```text
Agora a tarefa vital é dormir. A falta de sono amanhã reduzirá sua execução e aumentará irritação. Vou deixar a primeira Minitaf pronta para amanhã cedo.
```

## 12. Foco no que interessa

O CogniFlow deve ajudar o usuário a responder continuamente:

```text
O que mais protege minha vida real hoje?
```

E não apenas:

```text
O que eu estou com vontade de fazer agora?
```

## 13. Priorização diária mínima

Todo dia, o CogniFlow deve identificar:

```text
1 tarefa vital de trabalho/profissão
1 tarefa vital de saúde/sono/alimentação
1 Minitaf mínima para reduzir atraso ou risco
```

Exemplo:

```text
Hoje, a tarefa vital profissional é avançar no relatório.
A tarefa vital de saúde é proteger o horário de dormir.
A Minitaf mínima é escrever o esqueleto do relatório.
```

## 14. Recompensa boa versus dopamina barata

O sistema deve ensinar o usuário a perceber a diferença.

Dopamina barata:

```text
alívio rápido + prejuízo futuro
```

Recompensa boa:

```text
avanço real + menor peso mental + proteção da vida real
```

## 15. Mensagem de reforço após execução

Quando o usuário concluir uma Minitaf vital, o sistema deve reforçar o valor real da ação.

Exemplo:

```text
Você não apenas fez uma tarefa. Você protegeu sua reputação profissional e reduziu o peso mental do prazo.
```

## 16. Critério de sucesso

Essa funcionalidade é bem-sucedida quando o CogniFlow consegue:

1. detectar fuga para dopamina barata;
2. capturar a ideia sem permitir que ela sequestra a execução;
3. lembrar a tarefa vital;
4. priorizar trabalho, profissão, saúde, sono e alimentação;
5. conduzir o usuário para uma Minitaf pequena;
6. mostrar recompensa boa da execução;
7. reduzir prejuízo profissional, irritação e impacto nos relacionamentos.
