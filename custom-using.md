---

copyright:
  years: 2015, 2020
lastupdated: "2020-06-22"

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

# Using a custom voice model
{: #customUsing}

Once you create a custom model and populate it with custom entries, you use it by passing its customization ID (GUID) with the `customization_id` query parameter of the HTTP `GET` or `POST /v1/synthesize` method or the WebSocket `/v1/synthesize` method. When you include a customization ID, you must call a `synthesize` method with credentials for the instance of the service that owns the specified custom model.
{: shortdesc}

The first two examples generate a custom pronunciation for `IEEE` that is based on entries from the indicated custom model. The custom pronunciation is used instead of the default pronunciation from the service's regular pronunciation rules.

-   The HTTP `GET /v1/synthesize` method:

    ```bash
    curl -X GET -u "apikey:{apikey}" \
    --header "Accept: audio/flac" \
    --output ieee.flac \
    "{url}/v1/synthesize?text=IEEE&customization_id={customization_id}"
    ```
    {: pre}

-   The HTTP `POST /v1/synthesize` method:

    ```bash
    curl -X POST -u "apikey:{apikey}" \
    --header "Content-Type: application/json" \
    --header "Accept: audio/flac" \
    --data "{\"text\":\"IEEE\"}" \
    --output ieee.flac \
    "{url}/v1/synthesize?customization_id={customization_id}"
    ```
    {: pre}

The third example establishes a WebSocket connection with the `/v1/synthesize` method that uses the indicated custom model to synthesize text passed over the connection:

```javascript
var token = {authentication-token};
var wsURI = '{ws_url}/v1/synthesize'
  + '?access_token=' + IAM_access_token
  + '&customization_id={customization_id}';
var websocket = new WebSocket(wsURI);
```
{: codeblock}
