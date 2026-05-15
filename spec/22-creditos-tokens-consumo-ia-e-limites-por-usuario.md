# 22 — Créditos, Tokens, Consumo de IA e Limites por Usuário

## 1. Princípio

O CogniFlow deve controlar o consumo de IA por usuário desde o início.

Como o sistema usará IA para texto, áudio, imagem, RAG, importação de projetos, follow-up, simulações financeiras e análise comportamental, cada interação pode gerar custo.

Esse custo precisa ser mensurado, limitado e vinculado ao usuário.

## 2. Correção de conceito

O usuário pode chamar de `créditos de token`, mas o produto deve mostrar uma unidade mais simples.

Sugestão:

```text
Créditos CogniFlow
```

O usuário não precisa entender tokens, custo por modelo, embeddings ou transcrição. Ele precisa entender:

```text
saldo disponível
quanto foi usado
quando precisa recarregar
quais recursos gastam mais
```

Internamente, o sistema registra tokens e custo real.

## 3. Regra central

```text
Para o usuário: créditos simples.
Para o sistema: tokens, chamadas, modelo usado e custo estimado.
```

## 4. Por que isso é necessário

Sem controle de créditos:

- o custo de IA fica invisível;
- um usuário pode consumir demais;
- áudio, imagem e PDF podem gerar gasto alto;
- o produto fica difícil de escalar;
- não há previsibilidade de custo por usuário;
- não há como criar planos pagos, beta ou gratuitos.

## 5. Tipos de consumo que devem ser medidos

```text
chat_text
voice_transcription
image_analysis
rag_query
project_import_pdf
minitaf_generation
followup_message
financial_simulation
behavior_analysis
weekly_summary
dashboard_generation
```

## 6. Saldo de créditos por usuário

Tabela sugerida:

```sql
CREATE TABLE user_credit_balances (
  user_id TEXT PRIMARY KEY,
  credit_balance NUMERIC(12,2) DEFAULT 0,
  total_credits_purchased NUMERIC(12,2) DEFAULT 0,
  total_credits_used NUMERIC(12,2) DEFAULT 0,
  plan_type TEXT DEFAULT 'prepaid',
  status TEXT DEFAULT 'active',
  created_at TIMESTAMPTZ DEFAULT NOW(),
  updated_at TIMESTAMPTZ DEFAULT NOW()
);
```

## 7. Livro-caixa de créditos

Toda entrada e saída de créditos deve ser registrada.

```sql
CREATE TABLE credit_ledger (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  user_id TEXT NOT NULL,
  transaction_type TEXT NOT NULL CHECK (transaction_type IN ('purchase', 'usage', 'refund', 'bonus', 'adjustment')),
  credits_amount NUMERIC(12,2) NOT NULL,
  balance_after NUMERIC(12,2),
  usage_type TEXT,
  reference_id UUID,
  description TEXT,
  created_at TIMESTAMPTZ DEFAULT NOW()
);
```

## 8. Log técnico de uso de IA

Além do saldo comercial, o sistema deve registrar uso técnico.

```sql
CREATE TABLE ai_usage_logs (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  user_id TEXT NOT NULL,
  request_id UUID,
  feature TEXT NOT NULL,
  provider TEXT,
  model TEXT,
  input_tokens INT,
  output_tokens INT,
  total_tokens INT,
  audio_seconds INT,
  image_count INT,
  document_pages INT,
  estimated_cost_usd NUMERIC(12,6),
  credits_charged NUMERIC(12,2),
  created_at TIMESTAMPTZ DEFAULT NOW()
);
```

## 9. Regras de cobrança interna

Cada recurso pode consumir créditos de forma diferente.

Exemplo conceitual:

```text
mensagem simples de texto = baixo consumo
áudio curto = médio
imagem = médio/alto
PDF grande = alto
RAG = médio
simulação financeira = baixo/médio
resumo semanal = médio/alto
```

A tabela exata de conversão deve ser definida depois, com base no custo real dos provedores de IA.

## 10. Planos possíveis

O CogniFlow deve suportar:

```text
plano pré-pago
assinatura com créditos mensais
beta gratuito limitado
plano híbrido: assinatura + compra de créditos adicionais
```

## 11. Recarga de créditos

O usuário deve poder adicionar créditos.

Exemplos:

```text
Adicionar 500 créditos
Comprar mais créditos
Recarregar saldo
Adicionar créditos ao meu usuário
```

O sistema deve registrar:

```text
usuário
valor pago
créditos comprados
meio de pagamento
saldo após recarga
data
```

## 12. Alerta de saldo baixo

O sistema deve avisar quando o saldo estiver baixo.

Exemplo:

```text
Seu saldo está baixo: 18 créditos.
Você ainda consegue usar mensagens simples, mas importação de PDF, áudio longo e imagem podem exigir recarga.
```

## 13. Bloqueio ou limitação por saldo

Quando o usuário não tiver saldo suficiente, o sistema deve:

1. permitir ações críticas de baixo custo, se definido pela política do produto;
2. bloquear ações caras;
3. oferecer recarga;
4. explicar qual recurso consome mais.

Exemplo:

```text
Você não tem créditos suficientes para importar este PDF agora.
Você ainda pode criar Minitafs por texto curto ou recarregar créditos.
```

## 14. Controle de custo por recurso

Para evitar gasto excessivo, o sistema deve ter limites:

```text
limite diário de mensagens
limite diário de imagens
limite de páginas por PDF
limite de áudios longos
limite de consultas RAG por dia
limite de follow-ups automáticos por usuário
```

## 15. Otimização de custo

O sistema deve reduzir consumo quando possível:

- não consultar RAG sem necessidade;
- não reler PDF já processado;
- salvar resumo estruturado de documentos;
- usar modelos mais baratos para tarefas simples;
- usar modelos melhores apenas em decisões complexas;
- comprimir imagens;
- transcrever áudio uma vez e salvar texto;
- reutilizar resultados já calculados.

## 16. Transparência para o usuário

O usuário deve poder perguntar:

```text
quantos créditos tenho?
quanto gastei hoje?
o que consumiu mais créditos este mês?
quanto custa importar um PDF?
```

Resposta esperada:

```text
Você tem 420 créditos.
Hoje usou 18 créditos:
- 10 em áudio
- 5 em chat
- 3 em follow-ups
```

## 17. Multiusuário

Créditos são sempre por usuário.

Regra obrigatória:

```text
Nenhuma chamada paga de IA deve ocorrer sem user_id e sem registro de consumo.
```

## 18. Beta fechado

Durante o beta, o sistema pode conceder créditos gratuitos limitados.

Exemplo:

```text
Usuário beta recebe 1000 créditos/mês.
Uso acima disso exige liberação manual ou recarga.
```

## 19. Critério de sucesso

Essa funcionalidade é bem-sucedida quando o CogniFlow consegue:

1. medir consumo de IA por usuário;
2. converter consumo técnico em créditos simples;
3. limitar uso caro;
4. permitir recarga;
5. evitar prejuízo operacional;
6. mostrar saldo e consumo de forma compreensível.
