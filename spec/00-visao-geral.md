# 00 — Visão Geral do CogniFlow

## 1. Nome do sistema

**CogniFlow**

Sistema de execução pessoal com IA para pessoas com TDAH.

## 2. Problema central

Pessoas com TDAH podem compreender tarefas complexas, criar projetos sofisticados e visualizar soluções amplas, mas frequentemente têm dificuldade em:

- iniciar tarefas;
- transformar ideias em próximas ações;
- estimar tempo;
- manter sequência operacional;
- lembrar do que estava fazendo;
- concluir antes de abrir novas frentes;
- retomar tarefas após interrupções;
- perceber atraso antes que ele se torne crítico.

O problema principal não é ausência de inteligência, intenção ou capacidade técnica. O problema é a lacuna entre intenção, organização temporal, execução sustentada e conclusão.

## 3. Objetivo do sistema

Criar um assistente pessoal de execução que receba tarefas por texto ou áudio, fragmente automaticamente tarefas e projetos em blocos executáveis, agende sessões de execução e faça follow-up ativo até que cada bloco seja concluído, replanejado ou reduzido.

## 4. Entrada principal

O sistema deve aceitar, inicialmente:

- texto enviado por WhatsApp ou app;
- áudio enviado por WhatsApp ou app;
- comandos curtos como `acabei`, `não acabei`, `travei`, `adiar`, `continuar`, `próxima tarefa`.

## 5. Saída principal

O sistema deve devolver sempre uma orientação operacional curta, estruturada e executável.

Formato preferencial de resposta ao usuário:

```text
PASSO ATUAL
O que fazer agora.

OBJETIVO
Por que isso importa.

PRÓXIMO PASSO
O que vem depois.
```

## 6. Unidade mínima de execução

A unidade mínima inicial é o bloco TDAH:

- 25 minutos de foco;
- 5 minutos de pausa;
- follow-up ativo ao final do bloco;
- replanejamento se não houver resposta ou se o usuário travar.

## 7. Princípio central de produto

O sistema nunca deve tratar uma tarefa ampla como se fosse executável.

Uma execução válida deve:

- começar com verbo;
- ter objeto claro;
- ter critério de término;
- caber idealmente em 25 minutos;
- poder ser marcada como concluída, não concluída ou travada.

## 8. Resultado esperado

Ao usar o CogniFlow, o usuário deve saber:

- o que fazer agora;
- quando parar;
- como responder ao sistema;
- qual é o próximo passo;
- se está atrasado;
- se precisa dividir a tarefa;
- o que já foi concluído.

## 9. Escopo inicial do MVP

O MVP deve resolver apenas o ciclo essencial:

1. receber uma tarefa por texto ou áudio;
2. identificar se é projeto, tarefa, entrega ou execução;
3. fragmentar até gerar uma execução concreta;
4. iniciar um bloco de 25 minutos;
5. cobrar retorno ao final;
6. interpretar `acabei`, `não acabei` ou `travei`;
7. concluir, dividir, reagendar ou cobrar novamente.

## 10. Fora do escopo inicial

Não fazem parte do MVP inicial:

- dashboard complexo;
- gamificação avançada;
- múltiplos usuários;
- marketplace;
- integração completa com calendário;
- análise comportamental profunda;
- RAG clínico ou terapêutico;
- diagnósticos médicos.

Esses itens podem ser tratados em versões futuras.
