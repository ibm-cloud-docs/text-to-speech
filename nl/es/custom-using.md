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

# Utilización de un modelo de voz personalizado
{: #customUsing}

Una vez que ha creado un modelo personalizado y lo ha cumplimentado con entradas personalizadas, lo puede utilizar pasando el ID de personalización (GUID) con el parámetro de consulta `customization_id` del método HTTP `GET` o `POST /v1/synthesize` o del método WebSocket `/v1/synthesize` method. Se deben utilizar las credenciales de servicio del propietario de un modelo para llamar a un método `synthesize` que utilice el modelo personalizado.
{: shortdesc}

En los dos primeros ejemplos se genera una pronunciación personalizada para `IEEE` basada en las entradas del modelo personalizado indicado. Se utiliza la pronunciación personalizada en lugar de la pronunciación predeterminada a partir de las reglas de pronunciación regular del servicio.

-   El método HTTP `GET /v1/synthesize`:

    ```bash
    curl -X GET -u "apikey:{apikey}"
    --header "Accept: audio/flac"
    --output ieee.flac
    "https://stream.watsonplatform.net/text-to-speech/api/v1/synthesize?text=IEEE&customization_id={customization_id}"
    ```
    {: pre}

-   El método HTTP `POST /v1/synthesize`:

    ```bash
    curl -X POST -u "apikey:{apikey}"
    --header "Content-Type: application/json"
    --header "Accept: audio/flac"
    --data "{\"text\":\"IEEE\"}"
    --output ieee.flac
    "https://stream.watsonplatform.net/text-to-speech/api/v1/synthesize?customization_id={customization_id}"
    ```
    {: pre}

En el tercer ejemplo se establece una conexión de WebSocket con el método `/v1/synthesize` que utiliza el modelo personalizado indicado para sintetizar el texto pasado a través de la conexión:

```javascript
var token = {authentication-token};
var wsURI = 'wss://stream.watsonplatform.net/text-to-speech/api/v1/synthesize'
  + '?access_token=' + IAM_access_token
  + '&customization_id={customization_id}';
var websocket = new WebSocket(wsURI);
```
{: codeblock}
