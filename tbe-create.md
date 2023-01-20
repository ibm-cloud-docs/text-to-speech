---

copyright:
  years: 2021, 2023
lastupdated: "2023-01-14"

subcollection: text-to-speech

---

{{site.data.keyword.attribute-definition-list}}

# Creating a custom prompt
{: #tbe-create}

The Tune by Example feature is beta functionality that is supported only for US English custom models and voices.
{: beta}

Follow these steps to create a custom prompt for use in speech synthesis with the {{site.data.keyword.texttospeechfull}} service:
{: shortdesc}

1.  [Create a custom model](#tbe-create-custom-model). You can create a new custom model for your prompt, or you can add your prompt to an existing custom model.
1.  [Create a speaker model](#tbe-create-speaker-model). A speaker model lets the service train itself on the voice of the user who speaks a prompt. Speaker models are optional but highly recommended.
1.  [Add a custom prompt](#tbe-create-add-prompt). You add a custom prompt to a custom model. A custom model can contain multiple prompts.
1.  [Evaluate the custom prompt](#tbe-create-evaluate-prompt). Once you add a custom prompt to a custom model, it is important to verify the quality of the prompt by using it in a synthesis request. For information about using a prompt with a speech synthesis request, see [Using a custom prompt for speech synthesis](/docs/text-to-speech?topic=text-to-speech-tbe-use).

You can add custom models, custom prompts, and speaker models as often as you need. You can add a maximum of 1000 custom prompts to a single custom model.

## Create a custom model
{: #tbe-create-custom-model}

You add a custom prompt to a custom model.  You can create a new custom model for your prompt, or you can add the prompt to an existing custom model.  The same custom model can contain multiple prompts, and the model's prompts can be associated with multiple speaker models. The same custom model can also contain custom words. To create a new custom model for your prompt, use the `POST /v1/customizations` method. For more information, see [Creating a custom model](/docs/text-to-speech?topic=text-to-speech-customModels#cuModelsCreate).

The following example creates a new custom model that is named `Prompt test`. Because custom prompts and speaker models are supported only for US English, the `language` of the model is `en-US`. The `Content-Type` header for the request must be `application/json`.

[IBM Cloud]{: tag-ibm-cloud}

```bash
curl -X POST -u "apikey:{apikey}" \
--header "Content-Type: application/json" \
--data "{\"name\":\"Prompt test\", \"language\":\"en-US\", \"description\":\"Custom model to test prompts\"}" \
"{url}/v1/customizations"
```
{: pre}

[IBM Cloud Pak for Data]{: tag-cp4d}

```bash
curl -X POST \
--header "Authorization: Bearer {token}" \
--header "Content-Type: application/json" \
--data "{\"name\":\"Prompt test\", \"language\":\"en-US\", \"description\":\"Custom model to test prompts\"}" \
"{url}/v1/customizations"
```
{: pre}

The method returns a globally unique identifier (GUID) as the customization ID for the new custom model. You use this GUID to identify the custom model in subsequent requests to the service.

```javascript
{
  "customization_id": "82f4809a-bf63-89a6-52ca-22731fe467ba"
}
```
{: codeblock}

## Create a speaker model
{: #tbe-create-speaker-model}

To create a speaker model for the speaker of your prompt, use the `POST /v1/speakers` method. You pass a unique name for the speaker with the `speaker_name` query parameter and the enrollment audio as the body of the request. The audio must be in WAV format and must have a sampling rate of no less that 16 kHz. For information about the rules and guidelines for the speaker name and audio, see [Rules for creating speaker models](/docs/text-to-speech?topic=text-to-speech-tbe-rules#tbe-rules-speakers).

The enrollment audio is distinct from the audio for any prompts. Enrollment audio lets the service extract information about a speaker’s voice. It then applies that knowledge to prompts that are associated with that speaker. Creation of a speaker model is optional. You can create prompts that are not associated with speakers. However, a speaker model can make a very positive difference in the quality of a prompt, so speaker models are highly recommended for all prompts.

The following example creates a speaker model named `speaker_one`. The request passes a 16 kHz WAV file as the enrollment audio in the body of the request. The `Content-Type` header of the request must be `audio/wav`.

[IBM Cloud]{: tag-ibm-cloud}

```bash
curl -X POST -u "apikey:{apikey}" \
--header "Content-Type: audio/wav" \
--data-binary "@speaker-one-audio.wav" \
"{url}/v1/speakers?speaker_name=speaker_one"
```
{: pre}

[IBM Cloud Pak for Data]{: tag-cp4d}

```bash
curl -X POST \
--header "Authorization: Bearer {token}" \
--header "Content-Type: audio/wav" \
--data-binary "@speaker-one-audio.wav" \
"{url}/v1/speakers?speaker_name=speaker_one"
```
{: pre}

The method returns a GUID as the speaker ID for the new speaker model. You use this GUID to identify the speaker model in subsequent requests to the service.

```javascript
{
  "speaker_id": "56367f89-546d-4b37-891e-4eb0c13cc833"
}
```
{: codeblock}

Speaker enrollment is a synchronous operation. Although it accepts more audio data than a custom prompt, the process of adding a speaker model is very fast. The service simply extracts information about the speaker’s voice from the audio. Unlike prompts, speaker models neither need nor accept a transcription of the audio, so the service does not need to align text and audio. When the call returns with a 201 response code to indicate success, the audio is fully processed and the speaker enrollment is complete.

## Add a custom prompt
{: #tbe-create-add-prompt}

To add a prompt to a custom model, use the `POST /v1/customizations/{customization_id}/prompts/{prompt_id}` method. You pass a unique identifier for the prompt as a path parameter. You then use that ID to specify the prompt in speech synthesis and other requests to the service.

You pass the required text of the prompt and the optional speaker ID with the `prompt_text` and `speaker_id` fields as a JSON object by using the multipart form parameter named `metadata`. You pass the audio for the prompt with a multipart form parameter named `file`. The audio must be in WAV format and must have a sampling rate of no less that 16 kHz. For more information about the rules and guidelines for the prompt ID, text, and audio, see [Rules for creating custom prompts](/docs/text-to-speech?topic=text-to-speech-tbe-rules#tbe-rules-prompts).

It is very important that the text and audio of the prompt match exactly. Discrepancies can reduce the quality of the synthesized prompt or even result in failure of the request.

The following example creates a custom prompt named `goodbye` that contains a simple farewell message. The request specifies the speaker ID for the speaker named `speaker_one` and the customization ID for the custom model that was created in the first step. The `Content-Type` header of the request must be `multipart/form-data`.

[IBM Cloud]{: tag-ibm-cloud}

```bash
curl -X POST -u apikey:{apikey} \
--header "Content-Type:multipart/form-data" \
--form metadata="{\"prompt_text\": \"Thank you and good-bye!\", \
   \"speaker_id\": \"56367f89-546d-4b37-891e-4eb0c13cc833\"}" \
--form file=@goodbye-prompt.wav \
"{url}/v1/customizations/82f4809a-bf63-89a6-52ca-22731fe467ba/prompts/goodbye"
```
{: pre}

[IBM Cloud Pak for Data]{: tag-cp4d}

```bash
curl -X POST \
--header "Authorization: Bearer {token}" \
--header "Content-Type:multipart/form-data" \
--form metadata="{\"prompt_text\": \"Thank you and good-bye!\", \
   \"speaker_id\": \"56367f89-546d-4b37-891e-4eb0c13cc833\"}" \
--form file=@goodbye-prompt.wav \
"{url}/v1/customizations/82f4809a-bf63-89a6-52ca-22731fe467ba/prompts/goodbye"
```
{: pre}

The service returns the following response with information about the prompt, including its initial status:

```javascript
{
   "prompt": "Thank you and good-bye!",
   "prompt_id": "goodbye",
   "status": "processing",
   "speaker_id": "823068b2-ed4e-11ea-b6e0-7b6456aa95cc"
}
```
{: codeblock}

Adding a prompt is an asynchronous operation. For more information about checking the status of a new prompt, see [Monitoring the add prompt request](#tbe-create-add-prompt-monitor).

### Monitoring the add prompt request
{: #tbe-create-add-prompt-monitor}

The service returns a 201 response code if it successfully initiates the request to add the prompt. Although adding a prompt accepts less audio than speaker enrollment, the service must align the audio with the provided text. The time that it takes to process a prompt depends on the length of the audio for the prompt. The processing time generally matches the length of the audio (for example, it takes 20 seconds to process a 20-second prompt).

For shorter prompts, you can wait for a reasonable amount of time and then check the status of the prompt with the `GET /v1/customizations/{customization_id}/prompts/{prompt_id}` method. For longer prompts, consider using that method to poll the service every few seconds to determine when the prompt is ready. The following example checks the status of the `goodbye` prompt:

[IBM Cloud]{: tag-ibm-cloud}

```bash
curl -X GET -u "apikey:{apikey}" \
"{url}/v1/customizations/82f4809a-bf63-89a6-52ca-22731fe467ba/prompts/goodbye"
```
{: pre}

[IBM Cloud Pak for Data]{: tag-cp4d}

```bash
curl -X GET \
--header "Authorization: Bearer {token}" \
"{url}/v1/customizations/82f4809a-bf63-89a6-52ca-22731fe467ba/prompts/goodbye"
```
{: pre}

While the service is evaluating the prompt, the status is `processing`. When the status becomes `available`, as shown in the following response, the prompt is ready to be used in a synthesis request. If the status is `failed`, a problem prevented creation of the prompt; the service includes an error message to describe the reason for the failure.

```javascript
{
   "prompt": "Thank you and good-bye!",
   "prompt_id": "goodbye",
   "status": "available",
   "speaker_id": "823068b2-ed4e-11ea-b6e0-7b6456aa95cc"
}
```
{: codeblock}

Only prompts that are in the `available` state can be used for speech synthesis. No prompt can be used for speech synthesis if it is in the `processing` or `failed` state. For more information about checking the status of a prompt, see [Listing custom prompts](/docs/text-to-speech?topic=text-to-speech-tbe-custom-prompts#tbe-custom-prompts-list).

## Evaluate the custom prompt
{: #tbe-create-evaluate-prompt}

When you create a prompt, the text of the prompt must reasonably match the spoken audio. The service does its best to align the specified text with the audio, and it can often compensate for mismatches between the two. If the differences between the text and the audio are too pronounced, however, the service cannot create the prompt. The longer the prompt, the greater the chance for misalignment between its text and audio. Multiple shorter prompts are therefore preferable to a single long prompt.

There is always the chance that the service might fail to detect a mismatch or might not produce a prompt that completely satisfies your needs. Therefore, you must listen to and evaluate all prompts before using them in production. Evaluating a prompt also allows you to detect unusual words that the service might not pronounce correctly. And it lets you be certain that the service’s voice speaks the prompt exactly as you intend.

Always listen to and evaluate a prompt to determine its quality before using it in production. To evaluate a prompt, include only the single prompt in a speech synthesis request by using the following SSML extension, in this case for a prompt whose ID is `goodbye`:

`<ibm:prompt id="goodbye"/>`

You call the same methods to evaluate a custom prompt and to use it in an application. For example, the following request uses the `POST /v1/synthesize` method to synthesize the prompt:

[IBM Cloud]{: tag-ibm-cloud}

```bash
curl -X POST -u "apikey:{apikey}" \
--header "Content-Type: application/json" \
--header "Accept: audio/wav" \
--data "{\"text\":\"<ibm:prompt id='goodbye'/>\"}" \
"{url}/v1/synthesize?customization_id=82f4809a-bf63-89a6-52ca-22731fe467ba&voice=en-US_AllisonV3Voice"
```
{: pre}

[IBM Cloud Pak for Data]{: tag-cp4d}

```bash
curl -X POST \
--header "Authorization: Bearer {token}" \
--header "Content-Type: application/json" \
--header "Accept: audio/wav" \
--data "{\"text\":\"<ibm:prompt id='goodbye'/>\"}" \
"{url}/v1/synthesize?customization_id=82f4809a-bf63-89a6-52ca-22731fe467ba&voice=en-US_AllisonV3Voice"
```
{: pre}

For more information about using prompts with speech synthesis, see [Using a custom prompt for speech synthesis](/docs/text-to-speech?topic=text-to-speech-tbe-use).

### Resolving evaluation problems for custom prompts
{: #tbe-create-evaluate-prompt-problems}

A custom prompt can suffer from different types of problems for different reasons. In some cases, you might need to rerecord and resubmit a prompt as many as a handful of times to address the following possible issues:

-   The service might fail to detect a mismatch between the prompt’s text and audio. This problem is more likely to occur with longer prompts. Multiple shorter prompts are preferable to a single long prompt.
-   The text of a prompt might include a word that the service does not recognize. In this case, you can add a custom word/translation pair to the prompt's custom model to tell the service how to pronounce the word. For more information, see [Adding a single word to a custom model](/docs/text-to-speech?topic=text-to-speech-customWords#cuWordAdd).
-   The quality of the input audio might be insufficient or the service’s processing of the audio might fail to detect or reflect the intended prosody. Submitting new audio for the prompt can correct these issues.

If a prompt that is created without a speaker ID does not adequately reflect the intended prosody, enrolling the speaker and providing a speaker ID for the prompt is one recommended means of potentially improving the quality of the prompt. This is especially important for shorter prompts such as "good-bye" or "thank you," where less audio data makes it more difficult for the service to match the prosody of the speaker.
