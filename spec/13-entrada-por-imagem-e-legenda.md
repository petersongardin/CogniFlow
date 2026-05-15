# 13 — Entrada por Imagem, Print e Legenda

## 1. Princípio

O CogniFlow deve suportar entrada por imagem porque pessoas com TDAH nem sempre conseguem transformar rapidamente uma situação visual em texto organizado.

O sistema deve permitir que o usuário envie:

- print de tela;
- foto de anotação em papel;
- foto de quadro branco;
- imagem de uma lista de tarefas;
- imagem de um documento;
- imagem com legenda escrita ou falada;
- foto de ambiente de trabalho bagunçado;
- foto de planilha, calendário, agenda ou lembrete.

## 2. Correção técnica da premissa de custo

Ler imagem pode ser viável e relativamente barato em muitos casos, mas não deve ser tratado como custo irrelevante.

O custo depende de:

- resolução da imagem;
- quantidade de imagens por usuário;
- frequência de uso;
- modelo de visão utilizado;
- necessidade de OCR;
- necessidade de interpretação visual complexa;
- armazenamento do arquivo original;
- tempo de processamento;
- política de retenção e privacidade.

Regra:

```text
Imagem deve ser suportada, mas com compressão, limites de tamanho, controle de custo e política de privacidade.
```

## 3. Papel da imagem no CogniFlow

A imagem deve servir como entrada de baixa fricção.

Em vez de exigir que o usuário explique tudo, ele pode enviar uma imagem e dizer:

```text
Transforme isso em Minitafs.
```

Ou:

```text
O que eu faço primeiro aqui?
```

Ou:

```text
Organize isso para mim.
```

## 4. Imagem com legenda

A forma ideal de entrada multimodal é imagem + legenda.

Exemplo:

```text
Imagem: foto de uma folha com várias tarefas.
Legenda: preciso executar isso hoje, mas estou travado.
```

O sistema deve combinar:

- conteúdo visual da imagem;
- texto da legenda;
- contexto do usuário;
- prazo;
- tarefa ativa;
- estado emocional ou sintoma informado.

## 5. Fluxo de processamento

```text
Usuário envia imagem
   ↓
Sistema identifica tipo de imagem
   ↓
Se houver legenda, combina imagem + legenda
   ↓
Extrai texto ou elementos visuais relevantes
   ↓
Classifica intenção
   ↓
Cria projeto, tarefa, entrega ou Minitaf
   ↓
Sugere a primeira Minitaf
   ↓
Agenda follow-up se o usuário iniciar
```

## 6. Tipos de imagem e resposta esperada

### 6.1 Print de tela

Uso:

- extrair tarefas de app, e-mail, WhatsApp, calendário, sistema web ou To Do.

Resposta esperada:

```text
Identifiquei 6 itens. A primeira Minitaf é resolver apenas o item mais urgente.
```

### 6.2 Foto de papel ou caderno

Uso:

- transformar anotações soltas em lista executável.

Resposta esperada:

```text
Vou separar isso em projeto, tarefas e Minitafs. Primeiro: transcrever os títulos principais.
```

### 6.3 Foto de quadro branco

Uso:

- capturar ideias, fluxos ou planejamento visual.

Resposta esperada:

```text
Transformei o quadro em 3 frentes. Recomendo iniciar pela frente com prazo mais próximo.
```

### 6.4 Foto de ambiente bagunçado

Uso:

- ajudar o usuário a iniciar organização doméstica ou física.

Resposta esperada:

```text
Primeira Minitaf: retirar apenas os objetos do chão e colocar em uma caixa temporária.
```

### 6.5 Documento fotografado

Uso:

- extrair obrigação, prazo ou ação necessária.

Resposta esperada:

```text
Identifiquei um documento com prazo. A primeira Minitaf é localizar a seção de exigências e listar o que precisa ser entregue.
```

## 7. Regra anti-sobrecarga

O sistema não deve devolver uma análise longa da imagem quando o usuário precisa agir.

Deve responder com:

```text
1. o que foi identificado;
2. a primeira Minitaf;
3. o critério de término;
4. a pergunta para iniciar.
```

## 8. Contrato interno sugerido

```json
{
  "type": "image_input",
  "user_id": "string",
  "source": "whatsapp|app|upload",
  "image_type": "screenshot|paper_note|whiteboard|document|environment|other",
  "caption": "string|null",
  "extracted_text": "string|null",
  "visual_summary": "string",
  "detected_intent": "create_project|create_task|extract_minitafs|clarify|unknown",
  "privacy_sensitivity": "low|medium|high",
  "next_action": "string"
}
```

## 9. Privacidade de imagens

Imagens podem conter dados sensíveis não percebidos pelo usuário, como:

- nomes;
- e-mails;
- telefones;
- documentos;
- dados financeiros;
- informações médicas;
- telas de sistemas;
- dados de terceiros;
- imagens de pessoas;
- localização ou ambiente privado.

Regra:

```text
Toda imagem deve ser tratada como potencialmente sensível até classificação contrária.
```

## 10. Retenção de imagens

Para reduzir risco e custo, o sistema deve separar:

```text
arquivo original da imagem
texto extraído
resumo visual
Minitafs geradas
```

Estratégia recomendada:

- armazenar o mínimo necessário;
- permitir apagar a imagem original após extração;
- manter apenas resumo e tarefas quando possível;
- vincular tudo ao `user_id`;
- registrar consentimento para retenção de imagens.

## 11. Controle de custo

Regras recomendadas:

- comprimir imagens antes do envio ao modelo;
- limitar tamanho máximo;
- limitar quantidade por dia no plano gratuito/beta;
- usar OCR simples quando só houver texto claro;
- usar modelo multimodal apenas quando for necessário interpretar layout ou contexto visual;
- salvar resultado estruturado para não reler a mesma imagem várias vezes.

## 12. Quando usar visão multimodal

Usar visão multimodal quando:

- houver layout visual importante;
- a imagem tiver mistura de texto, setas, quadros ou organização espacial;
- o usuário pedir interpretação da cena;
- a imagem for foto de ambiente, quadro ou anotação desorganizada.

Usar OCR/text extraction simples quando:

- a imagem for apenas documento textual claro;
- print com texto linear;
- tabela simples;
- lista de tarefas escrita de forma legível.

## 13. Relação com TDAH

A entrada por imagem reduz a barreira de iniciação.

Em vez de o usuário precisar explicar tudo, ele pode mostrar o problema.

Formulação:

```text
Para TDAH, mostrar pode ser mais fácil do que organizar verbalmente.
```

## 14. Resposta padrão ao receber imagem

```text
IMAGEM ENTENDIDA
Resumo curto do que foi identificado.

PRIMEIRA MINITAF
Ação concreta de 25 minutos.

CRITÉRIO DE TÉRMINO
Como saber que terminou.

CONFIRMAÇÃO
Quer iniciar agora?
```

## 15. Critério de sucesso

A funcionalidade é bem-sucedida quando o usuário consegue enviar uma imagem confusa e receber uma primeira ação pequena, concreta e executável, sem precisar organizar tudo manualmente.
