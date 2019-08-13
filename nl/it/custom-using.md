---

copyright:
  years: 2015, 2019
lastupdated: "2019-03-07"

subcollection: text-to-speech

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
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

# Utilizzo di un modello vocale personalizzato
{: #customUsing}

Dopo aver creato un modello personalizzato e averlo popolato con voci personalizzate, lo utilizzi passando il suo ID di personalizzazione (GUID) con il parametro di query `customization_id` del metodo HTTP `GET` o `POST /v1/synthesize` o del metodo WebSocket `/v1/synthesize`. Le credenziali del servizio del proprietario di un modello devono essere utilizzate per chiamare un metodo `synthesize` che utilizza il modello personalizzato.
{: shortdesc}

I primi due esempi generano una pronuncia personalizzata per `IEEE` che si basa sulle voci dal modello personalizzato indicato. La pronuncia personalizzata viene utilizzata al posto della pronuncia predefinita dalle regole di pronuncia regolare del servizio.

-   Il metodo HTTP `GET /v1/synthesize`:

    ```bash
    curl -X GET -u "apikey:{apikey}"
    --header "Accept: audio/flac"
    --output ieee.flac
    "https://stream.watsonplatform.net/text-to-speech/api/v1/synthesize?text=IEEE&customization_id={customization_id}"
    ```
    {: pre}

-   Il metodo HTTP `POST /v1/synthesize`:

    ```bash
    curl -X POST -u "apikey:{apikey}"
    --header "Content-Type: application/json"
    --header "Accept: audio/flac"
    --data "{\"text\":\"IEEE\"}"
    --output ieee.flac
    "https://stream.watsonplatform.net/text-to-speech/api/v1/synthesize?customization_id={customization_id}"
    ```
    {: pre}

Il terzo esempio stabilisce una connessione WebSocket con il metodo `/v1/synthesize` che utilizza il modello personalizzato indicato per sintetizzare il testo passato tramite la connessione:

```javascript
var token = {authentication-token};
var wsURI = 'wss://stream.watsonplatform.net/text-to-speech/api/v1/synthesize'
  + '?access_token=' + IAM_access_token
  + '&customization_id={customization_id}';
var websocket = new WebSocket(wsURI);
```
{: codeblock}
