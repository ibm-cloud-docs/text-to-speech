---

copyright:
  years: 2021, 2023
lastupdated: "2023-01-14"

subcollection: text-to-speech

---

{{site.data.keyword.attribute-definition-list}}

# Managing custom prompts
{: #tbe-custom-prompts}

The Tune by Example feature is beta functionality that is supported only for US English custom models and voices.
{: beta}

Tune by Example includes methods for listing all custom prompts for a custom model, for getting information about an individual prompt, and for deleting a prompt. These methods are in addition to the `POST /v1/customizations/{customization_id}/prompts/{prompt_id}` method for adding a prompt to a custom model; for more information, see [Add a custom prompt](/docs/text-to-speech?topic=text-to-speech-tbe-create#tbe-create-add-prompt).
{: shortdesc}

## Listing custom prompts
{: #tbe-custom-prompts-list}

Tune be Example provides two methods for listing information about the custom prompts for a specified custom model:

-   The `GET /v1/customizations/{customization_id}/prompts` method lists information about all custom prompts that are defined for a custom model.
-   The `GET /v1/customizations/{customization_id}/prompts/{prompt_id}` method lists information about a specific custom prompt from a custom model. Use this method to poll the service about the status of a request to add a prompt to a custom model.

The first method returns a `prompts` array that lists all of the prompts for a custom model. For each prompt that is listed in the array, the service provides the same information as it does for an individual prompt:

-   `prompt` is the user-specified text of the prompt that was provided when the prompt was created.
-   `prompt_id` is the user-specified identifier of the prompt that was provided at the prompt's creation. The prompt ID is used to identify the prompt in requests to the service, including in the SSML of speech synthesis requests.
-   `status` is the current status of the prompt:
    -   `processing` indicates that the service received the request to add the prompt and is processing the prompt. This is the initial status of all prompts.
    -   `available` indicates that the service successfully validated the prompt. The prompt is now ready for use in a speech synthesis request.
    -   `failed` indicates that the service's validation of the prompt failed. The status of the prompt includes an `error` field that describes the reason for the failure.
-   `speaker_id` is the GUID of the speaker model that is associated with the prompt. The service omits the field if no speaker ID is associated with the prompt.

When listing all prompts for a custom model, the `prompts` array is empty if the model contains no prompts.

### List all custom prompts example
{: #tbe-custom-prompts-list-all-example}

The following example lists all custom prompts that are included in the custom model that has the specified customization ID:

[IBM Cloud]{: tag-ibm-cloud}

```bash
curl -X GET -u "apikey:{apikey}" \
"{url}/v1/customizations/{customization_id}/prompts"
```
{: pre}

[IBM Cloud Pak for Data]{: tag-cp4d}

```bash
curl -X GET \
--header "Authorization: Bearer {token}" \
"{url}/v1/customizations/{customization_id}/prompts"
```
{: pre}

The model contains three custom prompts. The first two prompts are associated with the same speaker; the first is `available` and ready to use, and the service is still `processing` the second. The third prompt, which is `available`, is associated with a different speaker.

```javascript
{
  "prompts": [
    {
      "prompt": "Hello and welcome!",
      "prompt_id": "greeting",
      "status": "available",
      "speaker_id": "56367f89-546d-4b37-891e-4eb0c13cc833"
    },
    {
      "prompt": "How can I help you today?",
      "prompt_id": "help",
      "status": "processing",
      "speaker_id": "56367f89-546d-4b37-891e-4eb0c13cc833"
    },
    {
      "prompt": "I am sorry to hear that.",
      "prompt_id": "sorry",
      "status": "available",
      "speaker_id": "323e4476-63de-9825-7cd7-8120e45f8331"
    }
  ]
}
```
{: codeblock}

### List a specific custom prompt example
{: #tbe-custom-prompts-list-specific-example}

The following example returns information about just the first custom prompt from the previous listing:

[IBM Cloud]{: tag-ibm-cloud}

```bash
curl -X GET -u "apikey:{apikey}" \
"{url}/v1/customizations/{customization_id}/prompts/greeting"
```
{: pre}

[IBM Cloud Pak for Data]{: tag-cp4d}

```bash
curl -X GET \
--header "Authorization: Bearer {token}" \
"{url}/v1/customizations/{customization_id}/prompts/greeting"
```
{: pre}

The response duplicates the information from the previous example:

```javascript
{
  "prompt": "Hello and welcome!",
  "prompt_id": "greeting",
  "status": "available",
  "speaker_id": "56367f89-546d-4b37-891e-4eb0c13cc833"
}
```
{: codeblock}

## Deleting a custom prompt
{: #tbe-custom-prompts-delete}

To delete a custom prompt from a custom model, use the `DELETE /v1/customizations/{customization_id}/prompts/{prompt_id}` method. Using a nonexistent or deleted custom prompt in a speech synthesis request causes the service to return a 400 response code. Make sure that you do not attempt to use a deleted prompt in production.

### Delete a custom prompt example
{: #tbe-custom-prompts-delete-example}

The following example deletes the specified custom prompt from the custom model that has specified customization ID:

[IBM Cloud]{: tag-ibm-cloud}

```bash
curl -X DELETE -u "apikey:{apikey}" \
"{url}/v1/customizations/{customization_id}/prompts/{prompt_id}"
```
{: pre}

[IBM Cloud Pak for Data]{: tag-cp4d}

```bash
curl -X DELETE \
--header "Authorization: Bearer {token}" \
"{url}/v1/customizations/{customization_id}/prompts/{prompt_id}"
```
{: pre}
