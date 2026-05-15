# PRD — Product Requirements Document — CogniFlow

Versão: `v0.1.0-prd-inicial`

## 1. Objetivo do PRD

Este documento define o produto CogniFlow de forma profissional para orientar desenvolvimento, arquitetura, priorização, custos, credenciais, riscos, fases e critérios de entrega.

A Spec Consolidada define o comportamento do sistema. O PRD define o produto, o plano e as condições de desenvolvimento.

## 2. Visão do produto

CogniFlow é uma ferramenta externa de compensação executiva para pessoas com TDAH e instabilidade de energia/humor.

O produto ajuda o usuário a priorizar tarefas vitais, quebrar obrigações em Minitafs, iniciar ações difíceis, manter contexto, receber follow-up ativo, evitar fuga para dopamina barata e reduzir desorganização financeira.

## 3. Público-alvo

### Usuário inicial

Adulto com TDAH, alta capacidade cognitiva e dificuldade prática de execução, iniciação, persistência, organização financeira e conclusão.

### Beta fechado

Pequeno grupo de pessoas com TDAH, com diferentes perfis de trabalho, rotina, energia e dificuldades executivas.

### Uso geral futuro

Usuários adultos que desejam apoio externo para execução, rotina, finanças e priorização vital.

## 4. Problema

O usuário sabe o que precisa fazer, mas não consegue iniciar ou concluir tarefas prioritárias com consistência.

Isso gera:

- atraso profissional;
- irritação;
- prejuízo em relacionamentos;
- perda de confiança;
- desorganização financeira;
- piora do sono;
- sensação de viver abaixo da própria capacidade cognitiva.

## 5. Proposta de valor

```text
CogniFlow transforma tarefas grandes em passos pequenos, acompanha a execução e protege o usuário da fuga para dopamina barata.
```

## 6. Funcionalidades do MVP

### Obrigatórias

1. Entrada por texto.
2. Entrada por áudio com transcrição.
3. Criação de projeto/tarefa.
4. Fragmentação em Minitafs.
5. Follow-up ativo.
6. Respostas `acabei`, `não acabei`, `travei`.
7. Banco multiusuário com `user_id`.
8. Registro simples de sintomas de iniciação.
9. Priorização vital.
10. Filtro antidopamina básico.
11. Registro financeiro simples por linguagem natural.
12. Controle básico de créditos de IA por usuário.

### Pós-MVP

1. Entrada por imagem.
2. Importação de PDF grande.
3. RAG psicoeducativa.
4. Dashboard financeiro.
5. Simulação de compras.
6. Análise comportamental avançada.
7. App mobile completo.
8. Assinatura e recarga de créditos.

## 7. Stack tecnológica recomendada

### MVP rápido

- Backend/orquestração: n8n ou FastAPI.
- IA: OpenAI API.
- Transcrição: OpenAI Audio Transcription.
- Banco: PostgreSQL/Supabase.
- Fila/follow-up: BullMQ + Redis.
- Canal inicial: WhatsApp ou interface web simples.
- Hospedagem: VPS ou cloud gerenciada.

### Evolução robusta

- Backend principal: Python FastAPI.
- Agente: LangGraph.
- Banco: PostgreSQL.
- Vetores/RAG: pgvector.
- Jobs: BullMQ + Redis ou Celery/RQ.
- Frontend: Next.js ou app mobile posterior.
- Observabilidade: logs estruturados + monitoramento.

## 8. Credenciais necessárias

### Desenvolvimento

- GitHub.
- OpenAI API key.
- Banco PostgreSQL/Supabase.
- Redis.
- VPS/cloud.
- Domínio opcional.

### Integrações futuras

- WhatsApp Cloud API ou Evolution API.
- Gateway de pagamento.
- Serviço de e-mail transacional.
- Armazenamento de arquivos: S3, MinIO ou Supabase Storage.

## 9. Custos a estimar

### Custos fixos

- VPS ou cloud.
- Banco de dados.
- Redis.
- Domínio.
- Backup.
- Observabilidade.

### Custos variáveis

- tokens de IA;
- transcrição de áudio;
- análise de imagem;
- processamento de PDF;
- embeddings/RAG;
- mensagens WhatsApp;
- armazenamento de arquivos;
- gateway de pagamento.

## 10. Modelo de créditos

O usuário deve ver créditos simples.

Internamente o sistema mede:

- tokens;
- modelo usado;
- recurso acionado;
- custo estimado;
- créditos debitados;
- saldo por usuário.

## 11. Privacidade e compliance

Antes do beta, o produto precisa de:

- política de privacidade;
- termo de uso;
- aviso de não substituição clínica;
- consentimento para dados sensíveis;
- exportação e exclusão de dados;
- isolamento por usuário;
- minimização de logs sensíveis.

## 12. Riscos principais

### Produto

- virar app de tarefas genérico;
- excesso de funcionalidades antes do núcleo funcionar;
- respostas longas demais;
- follow-up fraco;
- sistema reforçar culpa em vez de execução.

### Técnico

- custo alto de IA;
- falha no follow-up;
- perda de estado;
- vazamento de dados sensíveis;
- arquitetura mono usuário difícil de escalar.

### Clínico/ético

- parecer terapia ou diagnóstico;
- lidar mal com relatos graves;
- incentivar hiperprodutividade;
- ignorar sono e saúde.

## 13. Métricas de sucesso

### MVP individual

- Minitafs criadas;
- Minitafs iniciadas;
- Minitafs concluídas;
- taxa de resposta ao follow-up;
- tarefas prioritárias retomadas;
- vezes em que o sistema detectou fuga dopaminérgica;
- registros financeiros realizados;
- saldo de créditos consumido por recurso.

### Beta

- retenção semanal;
- redução de tarefas esquecidas;
- taxa de conclusão por usuário;
- feedback qualitativo;
- custo médio por usuário;
- incidentes de privacidade;
- falhas de follow-up.

## 14. Fases de desenvolvimento

### Fase 1 — Prova individual

Objetivo: fazer o ciclo essencial funcionar para um usuário.

Escopo:

```text
texto/áudio → Minitaf → follow-up → resposta → conclusão/replanejamento
```

### Fase 2 — Beta fechado

Objetivo: testar com grupo pequeno.

Adicionar:

- onboarding;
- preferências por usuário;
- privacidade beta;
- controle de créditos;
- logs e monitoramento.

### Fase 3 — Produto público

Objetivo: abrir para uso geral.

Adicionar:

- pagamento;
- dashboard;
- suporte;
- termos formais;
- escalabilidade;
- RAG mais robusta;
- app ou interface web mais completa.

## 15. Decisão técnica inicial

O primeiro desenvolvimento deve focar no núcleo:

```text
Minitafs + follow-up ativo + estado persistente + user_id + controle de créditos.
```

O módulo financeiro pode entrar como módulo adicional, mas com arquitetura prevista desde o início.

## 16. Próximos documentos necessários

- `docs/ARCHITECTURE.md`
- `docs/DATABASE_SCHEMA.md`
- `docs/API_CONTRACTS.md`
- `docs/PRIVACY_POLICY_DRAFT.md`
- `docs/COST_MODEL.md`
- `docs/DEVELOPMENT_ROADMAP.md`
