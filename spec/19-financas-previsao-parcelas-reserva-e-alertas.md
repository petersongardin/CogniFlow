# 19 — Finanças: previsão, parcelas, reserva e alertas de descontrole

## 1. Princípio

O módulo financeiro do CogniFlow deve ajudar o usuário a enxergar não apenas o que já gastou, mas também o que ainda vai comprometer sua renda futura.

Pessoas com TDAH podem registrar uma compra parcelada e esquecer que ela continuará consumindo salário nos meses seguintes. O sistema deve transformar parcelas futuras em impacto visível no orçamento mensal.

## 2. Consulta por categoria e método de pagamento

O usuário deve poder perguntar em linguagem natural:

```text
quanto gastei de mercado esse mês?
```

Resposta esperada:

```text
Você gastou R$ 600,00 em mercado este mês:
- R$ 300,00 no cartão de crédito
- R$ 200,00 no vale alimentação
- R$ 100,00 no Pix
```

## 3. Regra de agregação financeira

O sistema deve conseguir agrupar lançamentos por:

```text
categoria
método de pagamento
mês
semana
dia
cartão
conta
estabelecimento
recorrência
parcelamento
```

Exemplo:

```text
mercado + mês atual + agrupado por método de pagamento
```

## 4. Problema das parcelas no cartão

Parcelas futuras são um ponto crítico para TDAH porque o gasto parece pequeno no momento da compra, mas compromete renda futura por vários meses.

Exemplo:

```text
comprei 1200 em 6x no cartão
```

O sistema deve registrar:

```text
6 parcelas de R$ 200,00
impacto mensal por 6 meses
categoria da compra
cartão usado
mês de início
mês final
```

## 5. Registro de compra parcelada

Entrada:

```text
1200 em 6x cartão conserto do carro
```

Resposta:

```text
Registrado: R$ 1.200,00 em 6 parcelas de R$ 200,00 no cartão, categoria transporte/carro.
Isso compromete R$ 200,00 por mês durante 6 meses.
```

## 6. Modelo de parcelas

Tabela sugerida:

```text
financial_installments
- id
- user_id
- transaction_id
- card_id
- total_amount
- installment_amount
- installment_current
- installment_total
- first_due_month
- last_due_month
- category
- description
- status
- created_at
```

Cada parcela também pode gerar um lançamento previsto no mês correspondente.

## 7. Previsão mensal

O CogniFlow deve calcular uma previsão do mês somando:

```text
renda prevista
renda recebida
gastos já realizados
contas fixas
parcelas futuras do cartão
boletos a vencer
assinaturas
reserva técnica planejada
investimentos planejados
```

## 8. Alerta de gasto maior que renda

Quando a previsão indicar que o usuário vai gastar mais do que ganha, o sistema deve avisar de forma direta.

Exemplo:

```text
ALERTA FINANCEIRO
Este mês sua previsão de gastos está maior que sua renda prevista.

Renda prevista: R$ 10.000,00
Gastos previstos: R$ 11.200,00
Diferença: -R$ 1.200,00

Pergunta de controle:
Existe algum ganho extra este mês que justifique esse gasto, ou isso é descontrole?
```

## 9. Pergunta de controle: renda extra ou descontrole

Quando o sistema detectar gasto acima da renda, deve perguntar:

```text
Tem algum ganho extra este mês que ainda não foi registrado?
```

Se sim:

```text
Registrar renda extra.
Recalcular previsão.
```

Se não:

```text
Classificar como risco de descontrole.
Sugerir Minitaf financeira de contenção.
```

## 10. Reserva técnica de imprevistos

O sistema deve lembrar o usuário de reservar parte da renda para imprevistos.

Exemplo:

```text
RESERVA TÉCNICA
Este mês ainda não há valor reservado para imprevistos.
Sugestão: separar R$ 300,00 antes de novos gastos não essenciais.
```

A reserva técnica deve ser tratada como proteção da estabilidade, não como sobra opcional.

## 11. Investimentos e depósitos planejados

O sistema deve permitir registrar metas de investimento ou depósito mensal.

Exemplos de entrada:

```text
todo mês quero investir 500 no Tesouro
minha meta é depositar 1000 por mês na reserva
este mês investi 300 no CDB
```

Se o depósito planejado não ocorrer, o sistema deve avisar:

```text
Você ainda não depositou nada na reserva este mês.
Isso reduz sua proteção contra imprevistos.
Quer separar uma Minitaf financeira para revisar o orçamento?
```

## 12. Minitaf financeira de contenção

Quando houver risco de gastar mais do que ganha, o sistema deve criar uma Minitaf pequena.

Exemplo:

```text
MINITAF FINANCEIRA
Abrir os gastos do cartão deste mês e marcar 3 gastos que podem ser evitados até o fechamento da fatura.

Critério de término:
3 gastos não essenciais identificados.
```

## 13. Dashboard futuro

O dashboard financeiro futuro deve mostrar:

```text
renda do mês
gastos realizados
gastos previstos
parcelas futuras
cartão por vencimento
limites por categoria
reserva técnica planejada
reserva técnica realizada
investimentos planejados
investimentos realizados
saldo previsto no fim do mês
risco de descontrole
```

## 14. Respostas financeiras devem ser objetivas

O sistema não deve gerar sermão financeiro.

Deve responder com:

```text
valor total
quebra por método/categoria
alerta, se houver
pergunta de controle
Minitaf, se necessário
```

## 15. Privacidade

Dados financeiros, renda, investimentos e dívidas são sensíveis.

Regras:

```text
todo dado financeiro deve ter user_id
não indexar dados financeiros na RAG geral
não expor valores em logs desnecessários
permitir exportação
permitir exclusão
proteger prints e comprovantes
```

## 16. Critério de sucesso

A funcionalidade é bem-sucedida quando o usuário consegue:

1. registrar gastos rapidamente;
2. consultar gastos por categoria e método de pagamento;
3. enxergar parcelas futuras;
4. receber alerta antes de gastar mais do que ganha;
5. lembrar reserva técnica e investimento planejado;
6. diferenciar renda extra real de descontrole financeiro;
7. transformar risco financeiro em uma Minitaf prática.
