# 06 — Importação de Projetos Inteiros e Minitafs

## 1. Conceito

O CogniFlow deve permitir que o usuário envie um projeto inteiro, em texto, áudio transcrito, PDF ou documento estruturado, e o sistema deve transformar esse projeto em uma árvore executável de trabalho.

A menor unidade executável do sistema passa a se chamar **Minitaf**.

## 2. Definição de Minitaf

Uma **Minitaf** é um bloco de execução desenhado para TDAH.

Estrutura padrão:

```text
25 minutos de foco
+ 5 minutos de pausa
+ follow-up ativo
```

## 3. Regras de uma Minitaf válida

Uma Minitaf válida deve:

- começar com verbo de ação;
- ter objeto claro;
- ter critério de término;
- caber idealmente em 25 minutos;
- produzir avanço visível;
- ser pequena o suficiente para reduzir resistência de início;
- ser registrável como `acabei`, `não acabei` ou `travei`.

Exemplo inválido:

```text
Executar o projeto VitisOnFarm.
```

Exemplo válido:

```text
Ler a seção Metodologia e listar as três etapas principais do projeto em tópicos.
```

## 4. Entrada por projeto inteiro

O sistema deve aceitar documentos grandes como entrada e executar uma decomposição em camadas.

Exemplos de entrada:

- PDF de projeto de pesquisa;
- proposta técnica;
- edital;
- plano de negócio;
- documento de projeto empresarial;
- áudio longo descrevendo um projeto;
- texto livre com muitas tarefas misturadas.

## 5. Hierarquia após importação

Ao importar um projeto inteiro, o CogniFlow deve gerar a seguinte estrutura:

```text
Nível 1 = Projeto
Nível 2 = Etapa ou eixo principal
Nível 3 = Entrega objetiva
Nível 4 = Minitaf executável
```

Somente o nível 4 pode ser executável.

## 6. Processo de decomposição

O sistema deve seguir esta ordem:

1. identificar nome do projeto;
2. extrair objetivo geral;
3. identificar etapas principais;
4. identificar entregas exigidas;
5. identificar atividades técnicas;
6. converter atividades em Minitafs;
7. priorizar o que está atrasado, pendente ou bloqueado;
8. sugerir a primeira Minitaf a executar.

## 7. Exemplo de projeto importado

Projeto: `VitisOnFarm`

Estrutura identificada:

```text
Nível 1 — VitisOnFarm

Nível 2 — Etapa 1: Estudo comparativo entre manejo biológico e manejo convencional
Nível 2 — Etapa 2: Viabilidade de multiplicados biológicos e compatibilidade com fungicidas
Nível 2 — Etapa 3: Seleção e caracterização de bactérias promotoras de crescimento e biocontrole
```

Exemplos de Minitafs derivadas:

```text
Minitaf 1
Ler o resumo do projeto e escrever em 5 linhas o objetivo operacional do VitisOnFarm.

Minitaf 2
Listar as avaliações previstas na Etapa 1 em uma tabela com: avaliação, frequência, local e responsável.

Minitaf 3
Separar as atividades de campo da Etapa 1 das atividades de laboratório.

Minitaf 4
Criar uma lista dos dados que ainda precisam ser coletados para produtividade, doenças, solo e planta.

Minitaf 5
Transformar a Etapa 2 em uma sequência de bancada: preparo, diluição, incubação, leitura e registro.

Minitaf 6
Listar os testes da Etapa 3: antagonismo, solubilização de fosfato, sideróforos, AIA, fixação de nitrogênio e identificação molecular.
```

## 8. Regra de resposta após importação

Depois de receber um projeto inteiro, o sistema não deve devolver todas as Minitafs de uma vez como lista gigante.

O comportamento correto é:

1. confirmar que o projeto foi importado;
2. mostrar a árvore resumida;
3. indicar a primeira Minitaf;
4. perguntar se o usuário quer iniciar agora.

Formato:

```text
PROJETO IMPORTADO
Nome do projeto.

ESTRUTURA DETECTADA
Etapas principais.

PRIMEIRA MINITAF
Ação concreta de 25 minutos.

CONFIRMAÇÃO
Quer iniciar essa Minitaf agora?
```

## 9. Regra contra sobrecarga

O sistema pode armazenar dezenas ou centenas de Minitafs, mas a interface com o usuário deve mostrar apenas:

- a Minitaf atual;
- o objetivo;
- o próximo passo;
- o progresso resumido;
- os bloqueios relevantes.

O usuário não deve ser obrigado a visualizar todo o projeto para iniciar.

## 10. Campos sugeridos no banco

Adicionar ou considerar os seguintes campos na tabela `tasks`:

```sql
source_document_id UUID;
source_page_start INT;
source_page_end INT;
minitaf_number INT;
acceptance_criteria TEXT;
energy_level_required INT;
context_summary TEXT;
```

## 11. Critério de sucesso

A funcionalidade é bem-sucedida quando o usuário consegue enviar um documento grande e receber uma primeira ação simples, sem precisar organizar manualmente o projeto.
