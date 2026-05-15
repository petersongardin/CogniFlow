# SPEC-CONSOLIDADA — CogniFlow

Versão: `v0.2.0-consolidacao-produto`

## 1. Definição do produto

CogniFlow é uma ferramenta externa de compensação executiva para pessoas com TDAH e instabilidade de energia/humor.

O sistema organiza tarefas, prioriza o que protege a vida real do usuário, fragmenta projetos em Minitafs, acompanha execução com follow-up ativo, detecta fuga para dopamina barata e ajuda o usuário a transformar intenção em conclusão.

## 2. Formulação central

```text
CogniFlow ajuda a pessoa a ser conduzida pela sua capacidade cognitiva, não limitada pela sua deficiência executiva.
```

## 3. Unidade operacional: Minitaf

```text
Minitaf = 25 minutos de foco + 5 minutos de pausa + follow-up ativo.
```

Uma Minitaf válida deve:

- começar com verbo de ação;
- ter objeto claro;
- ter critério de término;
- caber idealmente em 25 minutos;
- permitir resposta: `acabei`, `não acabei` ou `travei`.

## 4. Problemas que o sistema compensa

- desconto do futuro;
- dificuldade de iniciação;
- cegueira temporal;
- memória de trabalho fraca;
- busca por novidade;
- fuga para dopamina barata;
- dificuldade de persistência e conclusão;
- regulação emocional e de energia;
- desorganização financeira;
- perda de contexto em tarefas longas.

## 5. Priorização vital

O CogniFlow não prioriza apenas o que o usuário quer fazer agora. Ele prioriza o que protege a vida real.

Áreas vitais:

- trabalho;
- desenvolvimento profissional;
- saúde;
- sono;
- alimentação;
- relacionamentos;
- finanças;
- obrigações com prazo;
- futuro.

Regra:

```text
Interesse não define prioridade. Impacto vital define prioridade.
```

## 6. Entradas aceitas

O sistema deve aceitar:

- texto;
- áudio;
- imagem;
- imagem com legenda;
- PDF/documento;
- comandos curtos.

Comandos mínimos:

```text
iniciar
acabei
não acabei
travei
adiar
dividir
sono
sem energia
quanto gastei
como está meu mês
```

## 7. Fluxo central de execução

```text
Entrada do usuário
↓
Normalização
↓
Classificação de intenção
↓
Priorização vital
↓
Fragmentação em Minitafs
↓
Execução
↓
Follow-up ativo
↓
Resposta do usuário
↓
Concluir, dividir, reagendar ou reduzir
```

## 8. Importação de projetos inteiros

O CogniFlow deve aceitar um projeto inteiro, como PDF ou texto longo, e criar:

```text
Nível 1 = Projeto
Nível 2 = Etapa
Nível 3 = Entrega
Nível 4 = Minitaf
```

Somente nível 4 pode ser executável.

Após importar um projeto, o sistema deve mostrar a árvore resumida e indicar apenas a primeira Minitaf, sem sobrecarregar o usuário.

## 9. Follow-up ativo

O follow-up é requisito central, não acessório.

Ele deve:

- lembrar a tarefa ativa;
- cobrar retorno;
- detectar silêncio;
- reintervir;
- mostrar consequência ruim da não execução;
- mostrar recompensa boa da execução;
- reduzir tarefa em caso de travamento;
- proteger sono quando necessário.

## 10. Sintomas de iniciação

O sistema deve permitir registrar sintomas de resistência antes de iniciar tarefas.

Exemplos:

- coceira;
- dor de cabeça;
- irritação;
- sonolência;
- vontade de fugir;
- bloqueio mental;
- urgência falsa de fazer outra coisa.

Esses sintomas devem ser tratados como sinais de resistência de iniciação, não como falha moral.

## 11. Filtro antidopamina

O sistema deve detectar quando o usuário troca tarefa vital por tarefa estimulante de baixa prioridade.

Exemplos de dopamina barata:

- planejar demais;
- pesquisar ferramentas;
- abrir novos projetos;
- conversar sobre melhorias enquanto há entrega atrasada;
- fazer tarefa fácil para evitar tarefa crítica.

Regra:

```text
Ideias novas são registradas no backlog, mas não sequestram a execução ativa.
```

## 12. RAG e aprendizagem comportamental

O sistema deve ter duas camadas separadas:

```text
RAG = conhecimento geral sobre TDAH, TCC, bipolaridade, saúde mental, sono, hábitos e produtividade.
Memória estruturada = comportamento individual do usuário.
```

Fine-tuning não é prioridade inicial. Deve ser considerado apenas depois de RAG, memória estruturada e bons prompts.

## 13. Módulo financeiro

O CogniFlow deve ter módulo financeiro de baixa fricção para compensar dificuldade de registrar e prever gastos.

Funções:

- registrar gastos por texto, áudio ou imagem;
- separar categoria e método de pagamento;
- registrar renda mensal prevista e real;
- registrar parcelas longas;
- projetar impacto futuro;
- consultar gastos por categoria;
- alertar se o usuário vai gastar mais do que ganha;
- lembrar reserva técnica e investimentos planejados;
- simular compras antes da decisão.

Exemplo:

```text
Usuário: quanto gastei de mercado esse mês?
Sistema: Você gastou R$ 600,00 em mercado: R$ 300,00 no cartão, R$ 200,00 no vale alimentação e R$ 100,00 no Pix.
```

## 14. Decisão de compra

O sistema deve permitir perguntas antes do gasto:

```text
Quero comprar uma bicicleta de R$ 4.000,00. Cabe no meu orçamento? Melhor à vista ou parcelado?
```

A resposta deve mostrar:

- se cabe;
- impacto no mês;
- impacto nos próximos meses;
- melhor forma de pagamento;
- recomendação: comprar, parcelar, adiar, reduzir valor ou não comprar.

## 15. Privacidade e LGPD

Privacidade é requisito central.

Dados sensíveis:

- saúde mental;
- sintomas;
- finanças;
- documentos;
- rotina;
- sono;
- comportamento;
- dívidas;
- renda.

Regras:

- todo dado deve ter `user_id`;
- RAG geral não deve misturar dados pessoais;
- logs devem minimizar conteúdo sensível;
- o usuário deve poder exportar e excluir dados;
- política de privacidade é obrigatória antes do beta.

## 16. Multiusuário

O sistema será testado primeiro por um usuário, mas deve nascer multiusuário.

Regra:

```text
Testar como usuário único. Construir como produto multiusuário.
```

## 17. Créditos de IA

O CogniFlow deve controlar consumo de IA por usuário.

Para o usuário:

```text
Créditos CogniFlow
```

Para o sistema:

```text
tokens, modelo, custo, recurso usado, user_id e saldo.
```

Nenhuma chamada paga de IA deve ocorrer sem `user_id` e sem registro de consumo.

## 18. Limites clínicos

O CogniFlow pode oferecer apoio executivo e psicoeducação, mas não deve:

- diagnosticar;
- prescrever;
- alterar tratamento;
- substituir médico, psicólogo ou psiquiatra;
- prometer cura;
- tratar sofrimento grave como mera produtividade.

## 19. Critério de sucesso do MVP

O MVP é bem-sucedido quando consegue:

1. receber texto ou áudio;
2. criar tarefa ou projeto;
3. fragmentar em Minitafs;
4. iniciar uma Minitaf;
5. fazer follow-up ativo;
6. interpretar `acabei`, `não acabei` e `travei`;
7. registrar comportamento básico;
8. proteger o usuário da fuga para dopamina barata;
9. registrar gastos simples;
10. operar com dados isolados por usuário.

## 20. Fonte modular

Esta Spec consolida as decisões registradas nos arquivos numerados em `spec/`. As specs modulares continuam como documentação de detalhe e histórico de decisão.
