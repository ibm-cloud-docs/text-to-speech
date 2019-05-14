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

# Angepasstes Sprechmodell verwenden
{: #customUsing}

Nachdem Sie ein angepasstes Modell erstellt und mit angepassten Einträgen gefüllt haben, verwenden Sie es, indem Sie seine Anpassungs-ID (GUID) mit dem Abfrageparameter `customization_id` der HTTP-Methode `GET` bzw. `POST /v1/synthetisize` oder der WebSocket-Methode `/v1/synthesize` übergeben. Zum Aufrufen einer Methode `synthesize`, die ein angepasstes Modell verwendet, müssen die Serviceberechtigungsnachweise für den Eigner des Modells verwendet werden.
{: shortdesc}

In den ersten beiden Beispielen wird eine angepasste Aussprache für das Wort `IEEE` generiert, die auf Einträgen aus dem angepassten Modell basiert. Die angepasste Aussprache wird anstelle der Standardaussprache aus den normalen Ausspracheregeln des Service verwendet.

-   HTTP-Methode `GET /v1/synthesize`:

    ```bash
    curl -X GET -u "apikey:{apikey}"
    --header "Accept: audio/flac"
    --output ieee.flac
    "https://stream.watsonplatform.net/text-to-speech/api/v1/synthesize?text=IEEE&customization_id={customization_id}"
    ```
    {: pre}

-   HTTP-Methode `POST /v1/synthesize`:

    ```bash
    curl -X POST -u "apikey:{apikey}"
    --header "Content-Type: application/json"
    --header "Accept: audio/flac"
    --data "{\"text\":\"IEEE\"}"
    --output ieee.flac
    "https://stream.watsonplatform.net/text-to-speech/api/v1/synthesize?customization_id={customization_id}"
    ```
    {: pre}

Im dritten Beispiel wird mit der Methode `/v1/synthesize` eine WebSocket-Verbindung aufgebaut, die das angegebene angepasste Modell zur synthetischen Erstellung von Sprache aus dem Text verwendet, der über die Verbindung übergeben wird:

```javascript
var token = {authentication-token};
var wsURI = 'wss://stream.watsonplatform.net/text-to-speech/api/v1/synthesize'
  + '?access_token=' + IAM_access_token
  + '&customization_id={customization_id}';
var websocket = new WebSocket(wsURI);
```
{: codeblock}
