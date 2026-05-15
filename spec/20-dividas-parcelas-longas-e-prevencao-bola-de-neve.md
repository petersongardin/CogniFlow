# 20 — Dívidas, Parcelas Longas, Renda Variável e Prevenção de Bola de Neve

## 1. Princípio

O módulo financeiro do CogniFlow deve ajudar o usuário a enxergar o impacto futuro de dívidas, financiamentos, empréstimos e compras parceladas longas.

Para pessoas com TDAH, o problema não é apenas registrar o gasto. O problema é manter na memória de trabalho que uma parcela continuará comprometendo a renda por muitos meses ou anos.

O sistema deve transformar compromissos financeiros futuros em alertas mensais visíveis.

## 2. Problema central

O TDAH perde facilmente contas de médio e longo prazo.

Exemplo:

```text
Comprei uma caminhonete em 60 parcelas de R$ 1.778,84.
```

Esse compromisso não é apenas uma compra. É uma redução mensal de renda disponível por 60 meses.

## 3. Comando natural do usuário

O usuário deve poder falar ou escrever:

```text
Comprei uma caminhonete em 60 parcelas de 1778,84. Coloque isso na minha renda mensal durante 60 meses.
```

Interpretação esperada:

```json
{
  "type": "long_term_financial_commitment",
  "description": "Caminhonete",
  "commitment_type": "vehicle_financing",
  "installment_amount": 1778.84,
  "installment_total": 60,
  "currency": "BRL",
  "affects_monthly_income": true,
  "status": "active"
}
```

## 4. Resposta esperada

```text
Registrado: caminhonete em 60 parcelas de R$ 1.778,84.
Isso compromete sua renda mensal pelos próximos 60 meses.

Vou considerar esse valor na previsão de todos os meses até o fim do financiamento.
```

## 5. Renda mensal prevista e renda mensal real

O sistema deve diferenciar:

```text
renda prevista
renda recebida
renda líquida disponível
renda comprometida
saldo previsto do mês
```

Exemplo:

```text
Este mês você esperava receber R$ 20.000,00.
Mas a renda real prevista caiu para R$ 15.600,00 por descontos.
```

O sistema deve recalcular o mês sempre que a renda mudar.

## 6. Descontos e variações de salário

O usuário deve poder registrar:

```text
mês que vem vou receber 15600 por causa do desconto do plano de saúde
este mês recebo 20000
entrou 3000 extra
esse mês não recebo tal parcela
```

O sistema deve atualizar a previsão mensal.

## 7. Previsão mensal obrigatória

Todo mês, o sistema deve calcular:

```text
renda prevista
renda recebida
contas fixas
parcelas de cartão
parcelas longas
empréstimos
financiamentos
assinaturas
investimentos planejados
reserva técnica planejada
gastos variáveis já realizados
saldo projetado
risco de déficit
```

## 8. Alerta de gasto maior que renda

Quando a previsão mensal indicar déficit, o sistema deve avisar claramente.

Exemplo:

```text
ALERTA FINANCEIRO
Este mês sua previsão indica que você vai gastar mais do que ganha.

Renda prevista: R$ 15.600,00
Compromissos previstos: R$ 17.200,00
Diferença: -R$ 1.600,00

Pergunta de controle:
Existe alguma renda extra ainda não registrada ou isso é descontrole financeiro?
```

## 9. Pergunta de controle

Quando houver gasto acima da renda, o sistema deve perguntar:

```text
Tem algum ganho extra este mês que justifique esse gasto?
```

Se sim:

```text
Registrar renda extra e recalcular.
```

Se não:

```text
Classificar como risco financeiro e sugerir uma Minitaf de contenção.
```

## 10. Prevenção de bola de neve

O sistema deve alertar quando dívidas, cartão, empréstimos ou parcelas futuras começarem a comprometer renda de forma perigosa.

Sinais de risco:

- gasto previsto maior que renda;
- uso recorrente de empréstimo para fechar o mês;
- fatura do cartão crescendo;
- múltiplas parcelas longas simultâneas;
- ausência de reserva técnica;
- investimentos planejados não realizados;
- gastos impulsivos em meses deficitários;
- comprometimento fixo alto da renda.

## 11. Reserva técnica

A reserva técnica deve ser tratada como proteção contra imprevistos, não como sobra opcional.

Exemplo de alerta:

```text
Este mês você ainda não separou reserva técnica.
Como há parcelas longas ativas, isso aumenta risco de entrar em empréstimo se surgir imprevisto.
```

## 12. Investimentos planejados

O sistema deve lembrar compromissos de investimento ou recomposição de reserva.

Exemplo:

```text
Você planejou investir R$ 500,00 este mês, mas ainda não registrou nenhum depósito.
Quer revisar o orçamento antes de novos gastos não essenciais?
```

## 13. Dívida total e consciência financeira

O sistema deve permitir registrar dívida total estimada.

Exemplo:

```text
Tenho 300 mil reais em empréstimos.
```

O sistema deve registrar isso como dado financeiro sensível e, se o usuário quiser, ajudar a decompor em contratos, parcelas, juros, vencimentos e prioridades.

Resposta adequada:

```text
Entendi. Vou tratar isso como dado financeiro sensível.
Para te ajudar, precisamos transformar essa dívida total em lista de compromissos: banco, saldo, parcela, juros, vencimento e prazo.
```

## 14. Minitaf de organização de dívidas

Quando o usuário informar dívida alta ou descontrole, o sistema não deve gerar uma análise gigante. Deve criar uma Minitaf.

Exemplo:

```text
MINITAF FINANCEIRA
Listar apenas os empréstimos ativos em uma tabela com: banco, valor da parcela, vencimento e saldo aproximado.

Critério de término:
Pelo menos 3 empréstimos listados ou todos os que lembrar em 25 minutos.
```

## 15. Modelos de dados sugeridos

### financial_income_monthly

```text
id
user_id
month
expected_income
received_income
income_notes
status
created_at
updated_at
```

### financial_commitments

```text
id
user_id
commitment_type
description
monthly_amount
total_installments
remaining_installments
first_month
last_month
lender_or_merchant
payment_method
category
status
created_at
updated_at
```

### financial_monthly_forecast

```text
id
user_id
month
expected_income
fixed_commitments_total
variable_expenses_total
installments_total
debt_payments_total
planned_investments
planned_reserve
forecast_balance
risk_level
created_at
updated_at
```

## 16. Resposta mensal padrão

O usuário deve poder perguntar:

```text
como está meu mês?
```

Resposta esperada:

```text
RESUMO DO MÊS
Renda prevista: R$ 15.600,00
Compromissos fixos e parcelas: R$ 12.400,00
Gastos variáveis até agora: R$ 2.100,00
Reserva/investimento planejado: R$ 500,00
Saldo projetado: R$ 600,00

ALERTA
A margem está baixa. Evite novos gastos não essenciais até revisar o cartão.
```

## 17. Privacidade

Dívidas, renda, empréstimos, financiamentos e investimentos são dados altamente sensíveis.

Regras:

```text
tudo deve ter user_id
não enviar dados financeiros para RAG geral
não expor valores em logs desnecessários
permitir exclusão e exportação
usar consentimento claro para dados financeiros
```

## 18. Limite de orientação financeira

O CogniFlow pode ajudar a organizar, lembrar, projetar e alertar.

O CogniFlow não deve se apresentar como consultor financeiro regulado, nem prometer resolver dívidas.

Quando houver endividamento alto, o sistema pode sugerir procurar orientação financeira profissional ou renegociação formal com instituições, mas sem fazer recomendações financeiras complexas sem contexto suficiente.

## 19. Critério de sucesso

A funcionalidade é bem-sucedida quando o usuário consegue:

1. registrar parcelas longas por linguagem natural;
2. ver o impacto mensal futuro;
3. comparar renda prevista com compromissos;
4. receber alerta antes de gastar mais do que ganha;
5. lembrar reserva técnica e investimentos;
6. transformar dívida grande em uma lista organizada;
7. evitar crescimento silencioso da bola de neve financeira.
