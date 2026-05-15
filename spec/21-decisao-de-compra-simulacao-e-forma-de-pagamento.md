# 21 — Decisão de Compra, Simulação e Melhor Forma de Pagamento

## 1. Princípio

O módulo financeiro do CogniFlow não deve apenas registrar gastos depois que eles acontecem. Ele também deve ajudar o usuário antes da compra.

Para pessoas com TDAH, a decisão de compra pode ser influenciada por impulso, pressão emocional, desejo imediato ou dificuldade de visualizar o impacto futuro no orçamento.

O sistema deve funcionar como uma camada externa de simulação, prudência e realidade financeira.

## 2. Caso de uso principal

O usuário pergunta em linguagem natural:

```text
Preciso comprar uma bicicleta para meu filho no valor de R$ 4.000,00. Qual é a melhor forma de pagar? À vista ou parcelado? Em quantas vezes cabe no meu orçamento?
```

O CogniFlow deve consultar:

- renda prevista do mês;
- renda dos próximos meses;
- gastos fixos;
- parcelas já existentes;
- cartão de crédito;
- reserva técnica;
- investimentos planejados;
- saldo projetado;
- risco de déficit.

## 3. Resposta esperada

A resposta deve ser curta, objetiva e baseada no orçamento.

Exemplo quando não cabe:

```text
ANÁLISE RÁPIDA
A compra de R$ 4.000,00 não cabe no seu orçamento deste mês.

Se pagar à vista, seu saldo projetado fica negativo.
Se parcelar em 10x de R$ 400,00, ainda cabe com margem baixa, mas reduz sua reserva nos próximos meses.

RECOMENDAÇÃO
Não comprar agora. Melhor esperar até liberar margem ou reduzir outro gasto.

PERGUNTA
Essa compra é urgente ou pode esperar 30 dias?
```

Exemplo quando cabe parcelado:

```text
ANÁLISE RÁPIDA
À vista não é recomendado porque reduz sua reserva técnica.
Parcelado em até 8x de R$ 500,00 cabe melhor no orçamento, sem deixar o mês negativo.

RECOMENDAÇÃO
Se comprar, prefira parcelar em até 8x e manter a reserva intacta.
```

## 4. Regra central

```text
Toda compra relevante deve ser simulada antes de virar compromisso financeiro.
```

Uma compra é relevante quando:

- tem valor alto em relação à renda;
- será parcelada;
- compromete cartão;
- reduz reserva técnica;
- afeta gastos essenciais;
- cria risco de déficit;
- pode ser impulsiva;
- não é vital no momento.

## 5. Comparação entre à vista e parcelado

O sistema deve comparar:

```text
pagamento à vista
parcelamento curto
parcelamento longo
adiamento da compra
compra de valor menor
compra usada ou alternativa
não comprar agora
```

A comparação deve considerar:

- impacto no mês atual;
- impacto nos meses futuros;
- risco de entrar no negativo;
- risco de comprometer reserva;
- custo psicológico de mais uma parcela;
- parcelas já ativas;
- necessidade real da compra.

## 6. Perguntas mínimas quando faltar dado

Se o sistema não tiver orçamento suficiente para responder, deve perguntar apenas o necessário.

Exemplos:

```text
Qual sua renda prevista deste mês?
Você já tem parcelas no cartão?
Essa compra é urgente?
Qual o máximo de parcela mensal que você tolera sem apertar o mês?
```

Regra:

```text
Perguntar uma coisa por vez para não sobrecarregar o usuário.
```

## 7. Contrato interno sugerido

```json
{
  "type": "purchase_decision_request",
  "user_id": "string",
  "item": "bicicleta para meu filho",
  "amount": 4000.00,
  "currency": "BRL",
  "urgency": "unknown|low|medium|high",
  "purchase_category": "family|child|transport|health|work|leisure|other",
  "payment_options_requested": ["cash", "installments"],
  "requires_budget_simulation": true
}
```

## 8. Resultado da simulação

```json
{
  "type": "purchase_decision_result",
  "user_id": "string",
  "item": "bicicleta para meu filho",
  "amount": 4000.00,
  "cash_option": {
    "fits_budget": false,
    "projected_balance_after_purchase": -500.00,
    "reserve_impact": "high"
  },
  "installment_options": [
    {
      "installments": 4,
      "monthly_amount": 1000.00,
      "fits_budget": false,
      "risk_level": "high"
    },
    {
      "installments": 8,
      "monthly_amount": 500.00,
      "fits_budget": true,
      "risk_level": "medium"
    },
    {
      "installments": 10,
      "monthly_amount": 400.00,
      "fits_budget": true,
      "risk_level": "medium"
    }
  ],
  "recommendation": "delay_or_installment_with_limit",
  "short_message": "À vista não cabe. Parcelado até 8 ou 10 vezes cabe, mas com margem baixa."
}
```

## 9. Risco de compra impulsiva

O sistema deve avaliar se a compra pode ser impulso dopaminérgico.

Sinais:

- compra não planejada;
- valor alto;
- usuário está estressado;
- compra ocorre à noite;
- orçamento já está apertado;
- existe dívida ativa;
- o usuário pergunta depois de já quase decidir;
- compra gera prazer imediato, mas aumenta parcelas futuras.

Intervenção:

```text
Essa compra pode esperar 24 horas? Como seu orçamento está apertado, recomendo não decidir agora.
```

## 10. Compra afetiva ou familiar

Algumas compras têm valor emocional, como comprar algo para filho ou família.

O sistema não deve tratar isso friamente como gasto supérfluo. Deve reconhecer o valor, mas ainda simular o impacto.

Exemplo:

```text
Entendo que a bicicleta para seu filho tem valor importante. Financeiramente, porém, à vista não cabe este mês. A opção mais segura é esperar ou parcelar dentro de uma parcela máxima que não deixe o mês negativo.
```

## 11. Regra de recomendação

O sistema deve recomendar uma das opções:

```text
comprar à vista
comprar parcelado até X vezes
adiar compra
reduzir valor da compra
buscar alternativa mais barata
não comprar agora
precisa de mais dados antes de decidir
```

## 12. Relação com prevenção de bola de neve

A decisão de compra deve consultar compromissos futuros.

Se o usuário já tiver financiamentos, empréstimos ou parcelas longas, o sistema deve avisar:

```text
Você já tem parcelas futuras relevantes. Adicionar mais R$ 400,00 por mês aumenta o risco de déficit nos próximos meses.
```

## 13. Minitaf financeira antes de compra

Se a compra for relevante e o orçamento estiver incerto, o sistema deve criar uma Minitaf de revisão.

```text
MINITAF FINANCEIRA
Listar renda prevista, fatura do cartão e contas fixas deste mês antes de decidir a compra.

Critério de término:
Renda, cartão e contas fixas anotados.
```

## 14. Privacidade e limite de orientação

Dados de compra, renda, cartão, dívidas e orçamento são sensíveis.

O CogniFlow pode organizar, simular e alertar. Ele não deve se apresentar como consultor financeiro regulado nem prometer resultado financeiro.

## 15. Critério de sucesso

A funcionalidade é bem-sucedida quando o usuário consegue perguntar antes de comprar e receber uma resposta curta que mostra:

1. se cabe no orçamento;
2. qual forma de pagamento é menos arriscada;
3. qual será o impacto nos próximos meses;
4. se a compra deve ser adiada;
5. qual Minitaf fazer se faltar informação.
