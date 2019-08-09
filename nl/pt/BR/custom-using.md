---

copyright:
  years: 2015, 2019
lastupdated: "2019-06-24"

subcollection: text-to-speech

---

{:shortdesc: .shortdesc}
{:external: target="_blank" .external}
{:tip: .tip}
{:important: .important}
{:note: .note}
{:deprecated: .deprecated}
{:pre: .pre}
{:codeblock: .codeblock}
{:screen: .screen}
{:javascript: .ph data-hd-programlang='javascript'}
{:java: .ph data-hd-programlang='java'}
{:python: .ph data-hd-programlang='python'}
{:swift: .ph data-hd-programlang='swift'}

# Usando um modelo de voz customizado
{: #customUsing}

Depois de criar um modelo customizado e preenchê-lo com as entradas customizadas, use-o transmitindo seu ID de customização (GUID) com o parâmetro de consulta `customization_id` do método HTTP `GET` ou `POST /v1/synthesize` ou do método WebSocket `/v1/synthesize`. Ao incluir um ID de customização, um método `synthesize` deve ser chamado com credenciais para a instância
do serviço que possui o modelo customizado especificado.
{: shortdesc}

Os primeiros dois exemplos geram uma pronúncia customizada para `IEEE`, que se baseia em entradas do modelo customizado indicado. A pronúncia customizada é usada em vez da pronúncia padrão das regras de pronúncia regular do serviço.

-   O método HTTP `GET /v1/synthesize`:

    ```bash
    curl -X GET -u "apikey: { apikey }"
    -- header "Accept: audio / flac"
    -- output ieee.flac
    "https: //stream.watsonplatform.net/text-to-speech/api/v1/synthesize?text=IEEE & customization_id = { customization_id }"
    ```
    {: pre}

-   O método HTTP `POST /v1/synthesize`:

    ```bash
    curl -X POST -u "apikey:{apikey}"
    --header "Content-Type: application/json"
    --header "Accept: audio/flac"
    --data "{\"text\":\"IEEE\"}"
    -- output ieee.flac
    "https: //stream.watsonplatform.net/text-to-speech/api/v1/synthesize?customization_id = { customization_id }"
    ```
    {: pre}

O terceiro exemplo estabelece uma conexão do WebSocket com o método `/v1/synthesize` que usa o modelo customizado indicado para sintetizar o texto transmitido pela conexão:

```javascript
var token = {authentication-token};
var wsURI = 'wss://stream.watsonplatform.net/text-to-speech/api/v1/synthesize'
  + '?access_token=' + IAM_access_token
  + '&customization_id={customization_id}';
var websocket = new WebSocket(wsURI);
```
{: codeblock}
