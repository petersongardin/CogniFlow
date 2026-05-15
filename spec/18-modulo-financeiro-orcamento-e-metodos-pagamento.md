# 18 — Módulo Financeiro: orçamento, métodos de pagamento e gasto dentro da renda

## 1. Princípio

O módulo financeiro do CogniFlow deve ajudar o usuário a registrar gastos com baixa fricção e, principalmente, gastar dentro do que ganha.

O objetivo não é criar um aplicativo financeiro complexo no início. O objetivo é compensar a dificuldade executiva de registrar, lembrar, somar, prever e limitar gastos.

## 2. Problema que o módulo resolve

Pessoas com TDAH podem ter dificuldade em:

- registrar gastos no momento em que acontecem;
- perceber pequenos gastos acumulados;
- lembrar compromissos financeiros;
- diferenciar saldo real de saldo aparente;
- controlar impulsos de compra;
- planejar gastos do mês;
- gastar de acordo com a renda disponível.

## 3. Regra central

```text
O usuário deve conseguir registrar o gasto em poucos segundos e o sistema deve comparar esse gasto com a renda, orçamento e limites do mês.
```

## 4. Exemplo de entrada simples

Entrada:

```text
300 cartão de crédito mercado
```

Resposta:

```text
Registrado: R$ 300,00 em mercado no cartão de crédito.
```

## 5. Exemplo com vários métodos de pagamento

Entrada:

```text
300 cartão de crédito mercado, 200 vale alimentação mercado, 100 pix mercado
```

Resposta:

```text
Registrado:
- R$ 300,00 mercado — cartão de crédito
- R$ 200,00 mercado — vale alimentação
- R$ 100,00 mercado — Pix
Total: R$ 600,00 em mercado.
```

## 6. Categoria versus método de pagamento

O sistema deve separar:

```text
Categoria = onde ou em que o dinheiro foi usado.
Método de pagamento = como foi pago.
```

Exemplo:

```text
mercado = categoria
cartão de crédito = método de pagamento
```

## 7. Métodos de pagamento iniciais

```text
dinheiro
Pix
cartão de débito
cartão de crédito
vale alimentação
vale refeição
boleto
transferência
cartão benefício
não identificado
```

## 8. Orçamento mensal

O sistema deve permitir registrar renda mensal e limites por categoria.

Exemplos:

```text
minha renda mensal é 12000
limite de mercado este mês é 2500
limite de alimentação fora é 800
limite do cartão é 4000
```

## 9. Tabelas sugeridas

### financial_transactions

```text
user_id
transaction_type
amount
currency
category
description
payment_method
transaction_date
source_text
batch_id
status
```

### financial_budgets

```text
user_id
month
income_expected
income_received
category
category_limit
spent_amount
remaining_amount
status
```

### financial_alerts

```text
user_id
alert_type
category
amount
message
status
created_at
```

## 10. Alertas de orçamento

O sistema deve avisar quando o usuário estiver se aproximando do limite.

Exemplo:

```text
Você já usou 82% do limite de mercado deste mês. Esse gasto ainda cabe, mas precisa reduzir compras extras até o fim do mês.
```

## 11. Regra de gasto dentro da renda

O sistema deve ajudar o usuário a responder:

```text
Esse gasto cabe no que eu ganho?
Esse gasto reduz minha segurança do mês?
Esse gasto é necessário ou é impulso?
```

## 12. Dopamina financeira

O sistema deve detectar possível gasto impulsivo quando houver padrão repetido, horário incomum ou categoria não vital.

Exemplo de intervenção:

```text
Esse gasto parece não essencial e você já está perto do limite do mês. Quer esperar 24 horas antes de comprar?
```

## 13. Dashboard futuro

Este módulo pode virar um módulo adicional do produto.

Dashboards futuros:

- gastos por categoria;
- gastos por método de pagamento;
- gasto versus renda;
- saldo previsto do mês;
- evolução semanal;
- gastos impulsivos;
- relação entre estresse, sono e gasto;
- contas a vencer;
- limite usado por cartão ou benefício.

## 14. Relação com o núcleo do CogniFlow

O módulo financeiro não substitui o núcleo do produto.

Núcleo:

```text
Minitafs, follow-up, priorização vital, antidopamina e execução.
```

Módulo financeiro:

```text
captura financeira rápida, orçamento, limites, alertas e dashboard futuro.
```

## 15. Critério de sucesso

A funcionalidade é bem-sucedida quando o usuário consegue registrar gastos em menos de 10 segundos e o sistema ajuda a manter o gasto dentro da renda mensal.
