# CogniFlow

**CogniFlow** é uma ferramenta externa de compensação executiva para pessoas com TDAH e instabilidade de energia/humor.

O objetivo é transformar tarefas grandes, aversivas ou confusas em **Minitafs** pequenas, visuais, sonoras quando útil, executáveis e acompanhadas por **follow-up ativo**.

## Formulação central

```text
CogniFlow ajuda a pessoa a ser conduzida pela sua capacidade cognitiva, não limitada pela sua deficiência executiva.
```

## O que o CogniFlow é

- organizador vital de tarefas;
- prótese cognitiva externa;
- assistente de execução;
- fragmentador de projetos grandes;
- sistema de apoio à iniciação;
- memória externa de execução;
- filtro contra dopamina barata;
- sistema de follow-up ativo não punitivo.

## O que o CogniFlow não é

- CRM;
- app empresarial;
- gestor corporativo de projetos;
- app genérico de produtividade;
- terapeuta virtual;
- substituto de médico, psicólogo ou psiquiatra;
- sistema de cobrança moral ou culpa.

## Problema que resolve

Pessoas com TDAH podem entender o que precisa ser feito, mas ter dificuldade em iniciar tarefas prioritárias, manter contexto, estimar tempo, resistir à dopamina barata e concluir ciclos.

O CogniFlow prioriza o que protege a vida real do usuário: trabalho, desenvolvimento profissional, saúde, sono, alimentação, relações, finanças e futuro.

## Unidade central: Minitaf

```text
Minitaf = 25 minutos de foco + 5 minutos de pausa + follow-up ativo.
```

Uma Minitaf válida precisa ter verbo de ação, objeto claro, critério de término, duração aproximada de 25 minutos e resposta possível: `acabei`, `não acabei` ou `travei`.

## Núcleo do produto

1. Receber entrada por texto, áudio, imagem ou documento.
2. Identificar tarefa, projeto, sintoma, gasto ou decisão.
3. Priorizar o que protege a vida real do usuário.
4. Quebrar projetos e obrigações em Minitafs.
5. Fazer follow-up ativo até conclusão, replanejamento ou redução.
6. Detectar fuga para dopamina barata.
7. Mostrar consequência ruim da não execução e recompensa boa da execução.
8. Aprender padrões comportamentais do usuário com privacidade.

## Módulos previstos

### Execução e TDAH

- Minitafs;
- follow-up ativo;
- sintomas de iniciação;
- filtro antidopamina;
- priorização vital;
- RAG psicoeducativa;
- memória comportamental.

### Finanças de baixa fricção

- registro rápido de gastos;
- métodos de pagamento;
- renda mensal;
- orçamento;
- parcelas longas;
- dívidas;
- reserva técnica;
- simulação de compras;
- alertas de déficit e bola de neve.

### Produto e escala

- multiusuário;
- créditos de IA por usuário;
- privacidade e LGPD;
- beta fechado;
- uso geral futuro.

## Documentos principais

A partir de agora, o desenvolvimento deve seguir estes documentos centrais:

```text
SPEC-CONSOLIDADA.md
PRD.md
```

As specs numeradas em `spec/` permanecem como anexos e registro de decisões.

## Estrutura recomendada

```text
CogniFlow/
├── README.md
├── SPEC-CONSOLIDADA.md
├── PRD.md
├── spec/
├── docs/
├── workflows/
└── src/
```

## Status

```text
Spec-Driven Development em construção.
Versão atual: v0.2.0-consolidacao-produto
```

## Regra de desenvolvimento

```text
As specs modulares podem evoluir, mas qualquer implementação deve ser validada contra a SPEC-CONSOLIDADA.md e o PRD.md.
```
