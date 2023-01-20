---

copyright:
  years: 2021, 2023
lastupdated: "2023-01-14"

subcollection: text-to-speech

---

{{site.data.keyword.attribute-definition-list}}

# Managing speaker models
{: #tbe-speaker-models}

The Tune by Example feature is beta functionality that is supported only for US English custom models and voices.
{: beta}

Tune by Example includes methods for listing speaker models, listing the prompts for a speaker model, and deleting a speaker model. It also includes the `POST /v1/speakers` method to create a speaker model; for more information, see [Create a speaker model](/docs/text-to-speech?topic=text-to-speech-tbe-create#tbe-create-speaker-model).
{: shortdesc}

## Listing all speaker models
{: #tbe-speaker-models-list}

To list all of the speaker models that are defined for a service instance, use the `GET /v1/speakers` method. The method returns a `speakers` array that provides the following information for each speaker model:

-   `speaker_id` indicates the speaker model's Globally Unique Identifier (GUID). The GUID is used to identify the speaker in calls to the service.
-   `name` is the user-specified name that was assigned to the speaker model when it was created.

The array is empty if no speaker models are defined for the service instance.

### List all speaker models example
{: #tbe-speaker-models-list-example}

The following example returns all of the available speaker models for the specified service credentials:

[IBM Cloud]{: tag-ibm-cloud}

```bash
curl -X GET -u "apikey:{apikey}" \
"{url}/v1/speakers"
```
{: pre}

[IBM Cloud Pak for Data]{: tag-cp4d}

```bash
curl -X GET \
--header "Authorization: Bearer {token}" \
"{url}/v1/speakers"
```
{: pre}

The credentials own two speaker models, `speaker_one` and `speaker_two`:

```javascript
{
  "speakers": [
    {
      "speaker_id": "56367f89-546d-4b37-891e-4eb0c13cc833",
      "name": "speaker_one"
    },
    {
      "speaker_id": "323e4476-63de-9825-7cd7-8120e45f8331",
      "name": "speaker_two"
    }
  ]
}
```
{: codeblock}

## Listing the custom prompts for a speaker model
{: #tbe-speaker-models-list-prompts}

To list all of the custom prompts that are associated with a speaker model, use the `GET /v1/speakers/{speaker_id}` method. Pass the GUID of the desired speaker model for the indicated path parameter.

The method returns a `customizations` array that lists all of the custom prompts for the speaker model organized by `customization_id`. For each customization ID, the method returns the following information:

-   `prompt` is the user-specified text of the prompt.
-   `prompt_id` is the user-specified identifier of the prompt. The ID is used to identify the prompt in calls to the service.
-   `status` is the current status of the prompt:
    -   `processing` indicates that the service received the request to add the prompt and is processing the prompt.
    -   `available` indicates that the service successfully validated the prompt, which is now ready for use in a speech synthesis request.
    -   `failed` indicates that the service's validation of the prompt failed. The status of the prompt includes an `error` field that describes the reason for the failure.

The `customizations` array is empty if the speaker model is not associated with any custom prompts.

### List the custom prompts for a speaker model example
{: #tbe-speaker-models-list-prompts-example}

The following example returns all of the custom prompts with which the specified `speaker_id` is associated:

[IBM Cloud]{: tag-ibm-cloud}

```bash
curl -X GET -u "apikey:{apikey}" \
"{url}/v1/speakers/{speaker_id}"
```
{: pre}

[IBM Cloud Pak for Data]{: tag-cp4d}

```bash
curl -X GET \
--header "Authorization: Bearer {token}" \
"{url}/v1/speakers/{speaker_id}"
```
{: pre}

The speaker model is associated with four prompts divided between two custom models:

```javascript
{
  "customizations": [
    {
      "customization_id": "9937efc0-5341-b436-77e1-9923f6e693a1",
      "prompts": [
        {
          "prompt": "Hello and welcome!",
          "prompt_id": "greeting",
          "status": "available"
        },
        {
          "prompt": "How can I help you today?",
          "prompt_id": "help",
          "status": "processing"
        }
      ]
    },
    {
      "customization_id": "82f4809a-bf63-89a6-52ca-22731fe467ba",
      "prompts": [
        {
          "prompt": "Thank you and good-bye!",
          "prompt_id": "goodbye",
          "status": "available"
        },
        {
          "prompt": "I do not understand that response.",
          "prompt_id": "do_not_understand",
          "status": "available"
        }
      ]
    }
  ]
}
```
{: codeblock}

## Deleting a speaker model
{: #tbe-speaker-models-delete}

To delete a speaker model, use the `DELETE /v1/speakers/{speaker_id}` method. Deleting a speaker model does not affect any prompts that are associated with the deleted speaker. The prosodic data that defines the quality of a prompt is established when the prompt is created. A prompt is static and remains unaffected by deletion of its associated speaker. However, the prompt cannot be resubmitted or updated with its original speaker once that speaker is deleted.

### Delete a speaker model example
{: #tbe-speaker-models-delete-example}

The following example deletes the speaker model that has the specified speaker ID:

[IBM Cloud]{: tag-ibm-cloud}

```bash
curl -X DELETE -u "apikey:{apikey}" \
"{url}/v1/speakers/{speaker_id}"
```
{: pre}

[IBM Cloud Pak for Data]{: tag-cp4d}

```bash
curl -X DELETE \
--header "Authorization: Bearer {token}" \
"{url}/v1/speakers/{speaker_id}"
```
{: pre}
