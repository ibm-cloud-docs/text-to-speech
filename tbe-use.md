---

copyright:
  years: 2021, 2023
lastupdated: "2023-01-14"

subcollection: text-to-speech

---

{{site.data.keyword.attribute-definition-list}}

# Using a custom prompt for speech synthesis
{: #tbe-use}

The Tune by Example feature is beta functionality that is supported only for US English custom models and voices.
{: beta}

To use a custom prompt in a speech synthesis request, you include the simple `<ibm:prompt>` element as the text of the request. This element is an {{site.data.keyword.IBM_notm}}-specific extension to SSML. The element has one attribute, `id`, which is a string that identifies a predefined prompt:
{: shortdesc}

`<ibm:prompt id="{prompt_id}"/>`

In addition to the [Rules for creating custom prompts](/docs/text-to-speech?topic=text-to-speech-tbe-rules#tbe-rules-prompts), the following restrictions apply to the use of a prompt in a speech synthesis request:

-   Only a single prompt can be used in a synthesis request. You cannot include two prompts in the same request.
-   A prompt must be the only thing that appears in a synthesis request. You cannot include additional text with the prompt.
-   A prompt can include only fixed text, not variable data that can change for different uses of the prompt. For example, "Your account balance is $500" contains variable data: "$500." The account balance is variable data that changes depending on a specific user's account. The prompt needs to speak "Your account balance is," and a second synthesis request needs to say the balance.

## Examples of using a custom prompt
{: #tbe-use-prompt-examples}

The following examples show speech synthesis requests for the `goodbye` prompt that was created in [Creating a custom prompt](/docs/text-to-speech?topic=text-to-speech-tbe-create). The examples use the `en-US_AllisonV3Voice` to speak the prompt and accept audio that is in the `audio/ogg;codecs=opus` audio format. You could use these same calls to evaluate the prompt before using it in a production application.

For the `customization_id`, substitute the GUID of the custom model that contains the prompt. Note that the speaker ID is specified only when you create a prompt, not when you include the prompt in a synthesis request.

The following examples use the [HTTP interface](/docs/text-to-speech?topic=text-to-speech-usingHTTP) to synthesize the prompt:

-   This example call the HTTP `POST /v1/synthesize` method to synthesize the prompt:

    [IBM Cloud]{: tag-ibm-cloud}

    ```bash
    curl -X POST -u "apikey:{apikey}" \
    --header "Content-Type: application/json" \
    --header "Accept: audio/ogg;codecs=opus" \
    --data "{\"text\":\"<ibm:prompt id='goodbye'/>\"}" \
    "{url}/v1/synthesize?customization_id={customization_id}&voice=en-US_AllisonV3Voice"
    ```
    {: pre}

    [IBM Cloud Pak for Data]{: tag-cp4d}

    ```bash
    curl -X POST \
    --header "Authorization: Bearer {token}" \
    --header "Content-Type: application/json" \
    --header "Accept: audio/ogg;codecs=opus" \
    --data "{\"text\":\"<ibm:prompt id='goodbye'/>\"}" \
    "{url}/v1/synthesize?customization_id={customization_id}&voice=en-US_AllisonV3Voice"
    ```
    {: pre}

-   This example calls the `GET /v1/synthesize` method to synthesize the prompt, which must be URL-encoded:

    [IBM Cloud]{: tag-ibm-cloud}

    ```bash
    curl -X GET -u apikey:{apikey } \
    --header "Accept: audio/ogg;codecs=opus" \
    "{url}/v1/synthesize?customization_id={customization_id}&voice=en-US_AllisonV3Voice&text=%3Cibm%3Aprompt%20id%3D%22goodbye%22%2F%3E"
    ```
    {: pre}

    [IBM Cloud Pak for Data]{: tag-cp4d}

    ```bash
    curl -X GET \
    --header "Authorization: Bearer {token}" \
    --header "Accept: audio/ogg;codecs=opus" \
    "{url}/v1/synthesize?customization_id={customization_id}&voice=en-US_AllisonV3Voice&text=%3Cibm%3Aprompt%20id%3D%22goodbye%22%2F%3E"
    ```
    {: pre}

The following snippet of JavaScript code uses the [WebSocket interface](/docs/text-to-speech?topic=text-to-speech-usingWebSocket) to synthesize the prompt:

```javascript
var access_token = '{access_token}';
var wsURI = '{ws_url}/v1/synthesize'
  + '?access_token=' + access_token
  + '&customization_id={customization_id}'
  + '&voice=en-US_AllisonV3Voice';
var websocket = new WebSocket(wsURI);

function onOpen(evt) {
  var message = {
    text: '<ibm:prompt id="goodbye"/>',
    accept: 'audio/ogg;codecs=opus'
  };
  websocket.send(JSON.stringify(message));
}

. . .
```
{: codeblock}
