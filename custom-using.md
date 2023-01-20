---

copyright:
  years: 2015, 2023
lastupdated: "2023-01-14"

subcollection: text-to-speech

---

{{site.data.keyword.attribute-definition-list}}

# Using a custom model for speech synthesis
{: #custom-using}

Once you create a custom model and populate it with custom entries, you use it by passing its customization ID (GUID) with the `customization_id` query parameter of the HTTP `GET` or `POST /v1/synthesize` method or the WebSocket `/v1/synthesize` method. When you include a customization ID, you must call a `synthesize` method with credentials for the instance of the service that owns the specified custom model.
{: shortdesc}

## Examples of using a custom model
{: #custom-using-examples}

The first two examples generate a custom pronunciation for `IEEE` that is based on entries from the indicated custom model. The custom pronunciation is used instead of the default pronunciation from the service's regular pronunciation rules.

-   The HTTP `GET /v1/synthesize` method:

    [IBM Cloud]{: tag-ibm-cloud}

    ```bash
    curl -X GET -u "apikey:{apikey}" \
    --header "Accept: audio/flac" \
    --output ieee.flac \
    "{url}/v1/synthesize?text=IEEE&customization_id={customization_id}"
    ```
    {: pre}

    [IBM Cloud Pak for Data]{: tag-cp4d}

    ```bash
    curl -X GET \
    --header "Authorization: Bearer {token}" \
    --header "Accept: audio/flac" \
    --output ieee.flac \
    "{url}/v1/synthesize?text=IEEE&customization_id={customization_id}"
    ```
    {: pre}

-   The HTTP `POST /v1/synthesize` method:

    [IBM Cloud]{: tag-ibm-cloud}

    ```bash
    curl -X POST -u "apikey:{apikey}" \
    --header "Content-Type: application/json" \
    --header "Accept: audio/flac" \
    --data "{\"text\":\"IEEE\"}" \
    --output ieee.flac \
    "{url}/v1/synthesize?customization_id={customization_id}"
    ```
    {: pre}

    [IBM Cloud Pak for Data]{: tag-cp4d}

    ```bash
    curl -X POST \
    --header "Authorization: Bearer {token}" \
    --header "Content-Type: application/json" \
    --header "Accept: audio/flac" \
    --data "{\"text\":\"IEEE\"}" \
    --output ieee.flac \
    "{url}/v1/synthesize?customization_id={customization_id}"
    ```
    {: pre}

The third example establishes a WebSocket connection with the `/v1/synthesize` method. The request uses the indicated custom model to synthesize text that is passed over the connection.

```javascript
var access_token = '{access_token}';
var wsURI = '{ws_url}/v1/synthesize'
  + '?access_token=' + access_token
  + '&voice=en-US_AllisonV3Voice'
  + '&customization_id=={customization_id}';
var websocket = new WebSocket(wsURI);

```
{: codeblock}
