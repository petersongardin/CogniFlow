# 01 — Problema e Usuário

## 1. Usuário principal

O usuário principal do CogniFlow é uma pessoa adulta com TDAH que precisa executar projetos pessoais, profissionais, domésticos, financeiros e empresariais, mas tem dificuldade em transformar intenção em ação contínua e conclusão.

Esse usuário pode ter alta capacidade cognitiva, criatividade, hiperfoco e compreensão sistêmica, mas sofre com falhas práticas de execução.

## 2. Dores principais

### 2.1 Iniciação

O usuário sabe o que precisa fazer, mas tem dificuldade para iniciar.

Exemplo:

```text
Preciso escrever o projeto.
```

Isso ainda é amplo demais. O sistema precisa transformar em algo como:

```text
Abrir o documento do projeto e escrever apenas o título e o objetivo geral.
```

### 2.2 Fragmentação

O usuário não deve precisar escrever tarefa por tarefa. O sistema deve fragmentar o projeto inteiro em partes menores.

Entrada ampla:

```text
Preciso organizar minha vida financeira.
```

Saída esperada:

```text
Primeiro bloco: listar todas as contas fixas do mês em uma tabela simples.
```

### 2.3 Percepção de tempo

O usuário pode subestimar ou superestimar a duração das tarefas. O sistema deve converter tarefas em blocos visíveis e temporizados.

### 2.4 Memória de trabalho

O usuário pode esquecer o que estava fazendo, especialmente após interrupções. O sistema deve preservar estado, contexto, execução atual e próximo passo.

### 2.5 Continuidade

O usuário pode iniciar muitos assuntos e não concluir. O sistema deve puxar o usuário de volta para a tarefa ativa antes de abrir novas frentes.

### 2.6 Conclusão

O sistema deve diferenciar movimento de entrega. A tarefa só deve ser marcada como concluída quando houver critério de término atendido.

## 3. Comportamentos que o sistema deve compensar

O CogniFlow deve compensar:

- dificuldade de iniciar;
- dificuldade de priorizar;
- dificuldade de quebrar tarefas;
- dificuldade de estimar tempo;
- dificuldade de retomar após interrupção;
- tendência a abrir novas frentes antes de concluir;
- esquecimento de tarefas ativas;
- baixa percepção de atraso;
- frustração após não concluir;
- travamento diante de tarefas amplas.

## 4. O que o sistema não deve fazer

O sistema não deve:

- devolver listas longas sem orientar a próxima ação;
- exigir que o usuário organize tudo manualmente;
- tratar projeto amplo como tarefa executável;
- perguntar muitas coisas de uma vez;
- abrir múltiplas frentes sem finalizar a atual;
- depender apenas de lembretes passivos;
- punir o usuário por falha de execução;
- gerar explicações longas durante o momento de ação.

## 5. Critério de sucesso do produto

O produto é bem-sucedido quando o usuário consegue:

1. enviar uma ideia confusa por áudio;
2. receber uma próxima ação clara;
3. iniciar sem precisar organizar tudo antes;
4. receber cobrança ativa;
5. concluir um bloco;
6. visualizar avanço;
7. retomar quando trava;
8. terminar mais tarefas do que terminaria sem o sistema.
