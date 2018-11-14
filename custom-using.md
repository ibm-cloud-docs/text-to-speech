---

copyright:
  years: 2015, 2017
lastupdated: "2018-10-28"

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

# Using a custom voice model
{: #customUsing}

Once you create a custom model and populate it with custom entries, you use it by passing its customization ID (GUID) with the `customization_id` query parameter of the HTTP `GET` or `POST /v1/synthesize` method or the WebSocket `/v1/synthesize` method. The service credentials of a model's owner must be used to call a `synthesize` method that uses the custom model.
{: shortdesc}

The first two examples generate a custom pronunciation for `IEEE` that is based on entries from the indicated custom model. The custom pronunciation is used instead of the default pronunciation from the service's regular pronunciation rules.

-   The HTTP `GET /v1/synthesize` method:

    ```bash
    curl -X GET -u "apikey:{apikey}"
    --header "Accept: audio/flac"
    --output ieee.flac
    "https://stream.watsonplatform.net/text-to-speech/api/v1/synthesize?text=IEEE&customization_id={customization_id}"
    ```
    {: pre}

-   The HTTP `POST /v1/synthesize` method:

    ```bash
    curl -X POST -u "apikey:{apikey}"
    --header "Content-Type: application/json"
    --header "Accept: audio/flac"
    --data "{\"text\":\"IEEE\"}"
    --output ieee.flac
    "https://stream.watsonplatform.net/text-to-speech/api/v1/synthesize?customization_id={customization_id}"
    ```
    {: pre}

The third example establishes a WebSocket connection with the `/v1/synthesize` method that uses the indicated custom model to synthesize text passed over the connection:

```javascript
var token = {authentication-token};
var wsURI = 'wss://stream.watsonplatform.net/text-to-speech/api/v1/synthesize'
  + '?watson-token=' + token
  + '&customization_id={customization_id}';
var websocket = new WebSocket(wsURI);
```
{: codeblock}
