# 15 — Priorização Vital, Recompensa Diária e Consequência da Não Execução

## 1. Correção de enquadramento

O CogniFlow é sim um organizador de tarefas, mas não é uma lista neutra de tarefas.

Ele deve organizar tarefas com base no impacto real na vida da pessoa, especialmente:

- trabalho;
- desenvolvimento profissional;
- saúde;
- sono;
- relações;
- finanças pessoais;
- obrigações com prazo;
- tarefas que reduzem sofrimento futuro;
- tarefas que destravam projetos importantes.

O sistema não deve tratar todas as tarefas como equivalentes.

## 2. Problema central

O usuário com TDAH pode saber exatamente o que precisa fazer, mas trocar a tarefa prioritária por uma tarefa de dopamina barata.

Exemplos de dopamina barata:

- conversar sobre outra ideia;
- pesquisar ferramenta nova;
- reorganizar sistema em vez de executar;
- abrir projeto novo;
- responder mensagens menos importantes;
- consumir conteúdo;
- fazer tarefa fácil para sentir progresso;
- resolver algo pequeno enquanto evita a tarefa crítica.

O resultado é alívio imediato, mas prejuízo acumulado.

## 3. Consequência da não execução

A não execução da tarefa prioritária pode gerar:

- atraso profissional;
- perda de confiança de outras pessoas;
- piora da reputação;
- irritação;
- culpa;
- ansiedade;
- prejuízo em relacionamentos;
- conflito familiar ou profissional;
- sobrecarga futura;
- sensação de estar abaixo da própria capacidade cognitiva.

O CogniFlow deve ajudar o usuário a enxergar a consequência real, sem culpa genérica e sem moralismo.

## 4. Formulação do problema pessoal

O usuário não quer viver limitado pela capacidade executiva quando possui capacidade cognitiva maior.

Formulação central:

```text
Quero ser um profissional à altura da minha capacidade cognitiva, não limitado pela minha deficiência executiva.
```

O CogniFlow existe para reduzir essa distância.

## 5. Papel da ferramenta externa

Como há deficiência executiva, o sistema deve funcionar como apoio externo para:

- escolher a tarefa mais importante;
- iniciar a tarefa prioritária;
- impedir fuga para dopamina barata;
- lembrar o custo de não executar;
- mostrar a recompensa diária de executar;
- manter follow-up ativo;
- trazer o usuário de volta quando dispersar;
- conduzir conclusão em Minitafs.

## 6. Priorização por impacto vital

O CogniFlow deve classificar tarefas por impacto.

Dimensões mínimas:

```text
trabalho
prazo
saúde
sono
desenvolvimento profissional
relações
finanças
risco futuro
energia disponível
bloqueio de outras tarefas
```

## 7. Score de prioridade sugerido

Cada tarefa pode receber uma pontuação operacional.

Campos sugeridos:

```json
{
  "importance_score": 1,
  "urgency_score": 1,
  "life_impact_area": "work|health|sleep|relationships|finance|professional_development|home|other",
  "future_damage_if_ignored": "string",
  "daily_reward_if_done": "string",
  "dopamine_trap_risk": "low|medium|high",
  "execution_priority": "low|medium|high|critical"
}
```

## 8. Tarefas prioritárias

Uma tarefa deve ser priorizada quando:

- tem prazo próximo;
- afeta trabalho;
- afeta desenvolvimento profissional;
- afeta saúde;
- afeta sono;
- está atrasada;
- gera prejuízo se não for feita;
- destrava outras tarefas;
- reduz sofrimento acumulado;
- evita conflito ou perda de confiança.

## 9. Sono como prioridade terapêutica operacional

O CogniFlow deve tratar sono como eixo central de execução.

Para TDAH, sono regular é um dos fatores mais importantes para melhorar controle executivo, regulação emocional e capacidade de iniciar tarefas.

Regra de produto:

```text
O sistema não deve sacrificar sono de forma recorrente para compensar atraso.
```

O sistema pode sugerir:

- encerrar ciclo de trabalho;
- preparar sono;
- reduzir tarefa noturna para Minitaf mínima;
- reagendar execução para horário mais adequado;
- proteger rotina de dormir;
- registrar relação entre sono e execução.

## 10. Dopamina barata versus recompensa boa

O sistema deve diferenciar:

```text
Dopamina barata = alívio imediato que aumenta prejuízo futuro.
Recompensa boa = satisfação por executar o passo diário que protege a vida real.
```

Exemplo de resposta:

```text
Você está buscando alívio imediato falando de outra coisa. A recompensa boa de agora é concluir uma Minitaf pequena e reduzir o peso do relatório.
```

## 11. Recompensa diária

O CogniFlow deve mostrar a recompensa boa e concreta de executar a Minitaf do dia.

Exemplos:

- você reduz o atraso;
- você preserva sua reputação;
- você dorme com menos peso mental;
- você avança profissionalmente;
- você evita conflito futuro;
- você prova para si mesmo que consegue iniciar;
- você diminui a irritação acumulada;
- você protege seus relacionamentos.

## 12. Mensagem de consequência e recompensa

Para tarefas críticas, a resposta deve conter dois elementos:

```text
Consequência ruim se não fizer
Recompensa boa se fizer agora
```

Exemplo:

```text
CONSEQUÊNCIA SE NÃO EXECUTAR
O relatório continuará atrasado e isso aumenta a pressão profissional e a irritação no fim do dia.

RECOMPENSA SE EXECUTAR
Com uma Minitaf concluída, você reduz o atraso e termina o dia com avanço real.
```

## 13. Regra de redirecionamento quando houver fuga

Quando o usuário estiver conversando sobre assuntos paralelos enquanto existe uma tarefa prioritária ativa, o CogniFlow deve reconhecer a fuga e redirecionar.

Formato:

```text
Você está desviando para uma tarefa de dopamina barata.
A tarefa que protege sua vida real agora é: [Minitaf prioritária].
```

A linguagem deve ser firme, mas não humilhante.

## 14. Interação simples

Como o sistema existe para compensar deficiência executiva, a interação deve exigir pouco do usuário.

O usuário deve poder responder com comandos mínimos:

```text
iniciar
acabei
não acabei
travei
adiar
dividir
sono
sem energia
```

## 15. Follow-up ativo como regulação externa

O sistema deve avisar, cobrar e insistir de forma progressiva.

O follow-up deve:

- lembrar a tarefa prioritária;
- mostrar a consequência da não execução;
- mostrar a recompensa da execução;
- oferecer Minitaf pequena;
- detectar silêncio;
- reduzir tarefa se houver travamento;
- proteger sono quando necessário;
- evitar abertura de nova frente.

## 16. Exemplo de intervenção ideal

```text
PASSO ATUAL
Abra o relatório e escreva apenas os títulos principais.

CONSEQUÊNCIA SE NÃO EXECUTAR
Se você não iniciar agora, o relatório seguirá atrasado e a pressão vai aumentar hoje à noite.

RECOMPENSA SE EXECUTAR
Você termina o dia com avanço real e reduz o peso mental da entrega.

PRÓXIMO PASSO
Volte em 25 minutos e responda: acabei, não acabei ou travei.
```

## 17. Regra-mãe de priorização

O CogniFlow deve priorizar a tarefa que mais protege a vida real do usuário, não a tarefa que oferece mais alívio imediato.

Formulação:

```text
Priorizar o que protege trabalho, saúde, sono, relações e futuro — não o que dá dopamina barata agora.
```

## 18. Critério de sucesso

O CogniFlow é bem-sucedido quando ajuda o usuário a:

1. identificar a tarefa prioritária;
2. resistir à fuga para dopamina barata;
3. iniciar uma Minitaf pequena;
4. perceber a consequência real da não execução;
5. perceber a recompensa boa da execução;
6. concluir um passo diário;
7. proteger trabalho, saúde, sono e relacionamentos;
8. aproximar sua vida real da sua capacidade cognitiva.
