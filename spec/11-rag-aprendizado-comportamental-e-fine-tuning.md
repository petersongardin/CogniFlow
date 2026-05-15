# 11 — RAG, Aprendizado Comportamental e Fine-tuning

## 1. Princípio

O CogniFlow deve aprender o comportamento do usuário e também ensinar o usuário a reconhecer seus próprios padrões executivos.

Esse aprendizado deve ser dividido em camadas distintas:

```text
1. Base científica e psicoeducativa — RAG
2. Memória comportamental individual — banco estruturado
3. Regras de intervenção — prompts e políticas do agente
4. Personalização de linguagem — preferências do usuário
5. Fine-tuning — somente em fase posterior, se necessário
```

## 2. Correção técnica da ideia inicial

A ideia de alimentar uma RAG com artigos científicos, livros, resumos de livros, TCC, TDAH e saúde mental é adequada.

Mas a ordem correta de implementação é:

```text
Primeiro: RAG + memória estruturada + bons prompts
Depois: avaliação de qualidade
Só depois: considerar fine-tuning
```

Fine-tuning não deve ser usado como primeira solução, porque:

- não é ideal para armazenar conhecimento consultável;
- não atualiza facilmente quando novos artigos entram;
- não mostra a fonte da resposta;
- pode dificultar correção de comportamento;
- não substitui memória do usuário;
- não substitui RAG;
- não é necessário para o MVP.

## 3. Papel correto da RAG

A RAG deve ser usada para conhecimento externo e relativamente estável.

Exemplos:

- TDAH e funções executivas;
- iniciação de tarefas;
- desconto do futuro;
- cegueira temporal;
- regulação emocional;
- terapia cognitivo-comportamental;
- estratégias de organização;
- psicoeducação;
- manejo de procrastinação;
- evidências sobre hábitos, sono, estresse e execução.

A RAG deve responder perguntas como:

```text
O que a TCC recomenda quando o usuário está evitando uma tarefa?
Que estratégia é indicada para reduzir ativação inicial?
Como explicar desconto do futuro ao usuário de forma simples?
Que tipo de intervenção ajuda na cegueira temporal?
```

## 4. Papel correto da memória comportamental

A memória comportamental não deve ficar solta dentro da RAG.

Ela deve ser banco estruturado por usuário.

Exemplos de dados comportamentais:

- horários em que o usuário inicia melhor;
- horários em que trava mais;
- tipos de tarefa que geram fuga;
- sintomas de iniciação frequentes;
- taxa de conclusão de Minitafs;
- respostas mais comuns: `acabei`, `não acabei`, `travei`, silêncio;
- impacto de sono, energia, estresse e álcool;
- duração real média das Minitafs;
- tarefas que são abertas e não fechadas;
- temas que geram busca por novidade.

Regra:

```text
RAG ensina o sistema sobre TDAH.
Memória estruturada ensina o sistema sobre aquele usuário.
```

## 5. Papel correto dos arquivos `.md`

Arquivos `.md` são uma boa forma de alimentar a RAG, desde que sejam bem estruturados.

Cada arquivo deve ter:

```text
Título
Fonte original
Tipo de conteúdo
Resumo operacional
Conceitos principais
Aplicações no CogniFlow
Limitações
Tags
```

Exemplo:

```md
# Desconto do Futuro no TDAH

Fonte: resumo operacional baseado em livro/artigo X.
Tipo: psicoeducação

## Conceito
O usuário tende a subestimar consequências futuras e priorizar alívio imediato.

## Aplicação no CogniFlow
Quando houver prazo próximo, o sistema deve transformar consequência futura em custo presente concreto.

## Exemplo de intervenção
"Se você não iniciar agora, amanhã a tarefa estará maior e mais aversiva. A próxima Minitaf é abrir o arquivo e escrever apenas o título."

## Tags
TDAH, desconto-do-futuro, procrastinação, iniciação
```

## 6. Estrutura recomendada da base RAG

```text
knowledge_base/
├── tdah/
│   ├── desconto-do-futuro.md
│   ├── time-blindness.md
│   ├── iniciacao-de-tarefas.md
│   ├── memoria-de-trabalho.md
│   └── busca-por-novidade.md
├── tcc/
│   ├── ativacao-comportamental.md
│   ├── reestruturacao-cognitiva.md
│   ├── exposicao-a-tarefa-aversiva.md
│   └── prevencao-de-evitacao.md
├── produtividade/
│   ├── pomodoro.md
│   ├── implementacao-de-intencoes.md
│   └── planejamento-semanal.md
└── seguranca/
    ├── limites-nao-clinicos.md
    └── sinais-de-risco.md
```

## 7. Formato mínimo de metadados para cada chunk

Cada trecho indexado na RAG deve conter metadados.

```json
{
  "doc_id": "tdah-desconto-futuro-001",
  "title": "Desconto do Futuro no TDAH",
  "source_type": "book_summary",
  "domain": "tdah",
  "tags": ["desconto_do_futuro", "procrastinacao", "prazo"],
  "clinical_sensitivity": "low|medium|high",
  "use_case": "psicoeducacao|intervencao|explicacao|alerta",
  "language": "pt-BR"
}
```

## 8. Regras de segurança clínica

O CogniFlow pode oferecer psicoeducação e apoio executivo, mas não deve diagnosticar, prescrever tratamento ou substituir psicólogo, psiquiatra ou médico.

Regras:

- não diagnosticar doenças mentais;
- não recomendar medicação;
- não alterar tratamento;
- não prometer cura;
- não tratar RAG como verdade absoluta;
- sempre diferenciar psicoeducação de orientação clínica;
- sinalizar que sintomas graves exigem ajuda profissional.

## 9. Como o agente deve usar RAG

O agente não deve consultar a RAG em toda mensagem.

Deve consultar quando:

- o usuário pedir explicação;
- houver padrão repetido de travamento;
- for necessário escolher intervenção;
- houver sintoma de iniciação registrado;
- for gerar psicoeducação curta;
- for adaptar uma Minitaf ao estado emocional ou energético.

Não deve consultar RAG quando:

- o usuário precisa apenas executar a próxima Minitaf;
- a resposta precisa ser imediata;
- o conteúdo já está no estado da tarefa;
- a consulta atrasaria o follow-up.

## 10. Ensino ao usuário

O CogniFlow deve ensinar em microdoses.

Formato:

```text
1 conceito curto
1 relação com o comportamento do usuário
1 próxima ação concreta
```

Exemplo:

```text
Isso parece desconto do futuro: seu cérebro está tentando aliviar agora e empurrar o custo para depois.
A próxima Minitaf reduz esse custo: abrir o relatório e escrever só os títulos.
```

## 11. Aprendizado do comportamento do usuário

O sistema deve gerar insights a partir dos dados do próprio usuário.

Exemplos:

```text
Você trava mais em tarefas de escrita do que em tarefas técnicas.
Você conclui melhor Minitafs iniciadas antes das 10h.
Quando dorme pouco, sua taxa de conclusão cai.
Você costuma abrir novas ideias quando uma tarefa obrigatória fica aversiva.
```

Esses insights devem ser baseados em dados observados, não em suposição solta.

## 12. Fine-tuning

Fine-tuning pode ser considerado no futuro, mas não para armazenar conhecimento ou memória do usuário.

Uso adequado de fine-tuning, se necessário:

- padronizar tom do agente;
- reduzir respostas longas;
- melhorar classificação de intenção;
- melhorar transformação de tarefas amplas em Minitafs;
- manter formato de saída consistente;
- reproduzir estilo de coaching operacional do CogniFlow.

Uso inadequado de fine-tuning:

- guardar livros e artigos;
- memorizar histórico pessoal do usuário;
- substituir banco de dados;
- substituir RAG;
- substituir regras de segurança;
- corrigir arquitetura ruim.

Regra:

```text
Fine-tuning ajusta comportamento do modelo.
RAG fornece conhecimento.
Banco estruturado guarda comportamento do usuário.
Prompt define regras de intervenção.
```

## 13. Arquitetura recomendada

```text
Usuário
  ↓
Entrada texto/áudio
  ↓
Classificador de intenção
  ↓
Consulta estado do usuário
  ↓
Decide se precisa de RAG
  ↓
Gera intervenção ou Minitaf
  ↓
Salva evento comportamental
  ↓
Agenda follow-up
```

## 14. Critério de sucesso

A funcionalidade é bem-sucedida quando o CogniFlow consegue:

- ensinar o usuário a reconhecer padrões;
- adaptar o tamanho e o tom da Minitaf;
- explicar o comportamento sem gerar culpa;
- usar conhecimento científico sem virar consulta clínica;
- aprender padrões individuais por dados;
- melhorar execução ao longo do tempo.
