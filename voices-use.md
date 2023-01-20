---

copyright:
  years: 2015, 2023
lastupdated: "2023-01-14"

subcollection: text-to-speech

---

{{site.data.keyword.attribute-definition-list}}

# Using a voice for speech synthesis
{: #voices-use}

Both the HTTP `POST` and `GET /v1/synthesize` methods, as well as the WebSocket `/v1/synthesize` method, accept an optional `voice` query parameter. You use the `voice` parameter to indicate the voice and language that are to be used for speech synthesis. The service bases its understanding of the language for the input text on the language of the specified voice.
{: shortdesc}

Be sure to specify a voice that matches the language of the input text. For example, if you specify the French voice `fr-FR_ReneeV3Voice`, the service expects to receive input text that is written in French. If you pass text that is not written in the language of the voice (for example, English text for the French voice), the service might not produce meaningful results.

## Specify a voice examples
{: #specify-voice}

The following example HTTP `POST` request uses the voice `en-US_AllisonV3Voice` for speech synthesis:

[IBM Cloud]{: tag-ibm-cloud}

```bash
curl -X POST -u "apikey:{apikey}" \
--header "Content-Type: application/json" \
--header "Accept: audio/wav" \
--data "{\"text\":\"hello world\"}" \
--output hello_world.wav \
"{url}/v1/synthesize?voice=en-US_AllisonV3Voice"
```
{: pre}

[IBM Cloud Pak for Data]{: tag-cp4d}

```bash
curl -X POST \
--header "Authorization: Bearer {token}" \
--header "Content-Type: application/json" \
--header "Accept: audio/wav" \
--data "{\"text\":\"hello world\"}" \
--output hello_world.wav \
"{url}/v1/synthesize?voice=en-US_AllisonV3Voice"
```
{: pre}

The following example shows an equivalent HTTP `GET` request for speech synthesis:

[IBM Cloud]{: tag-ibm-cloud}

```bash
curl -X GET -u "apikey:{apikey}" \
--output hello_world.wav \
"{url}/v1/synthesize?accept=audio%2Fwav&text=hello%20world&voice=en-US_AllisonV3Voice"
```
{: pre}

[IBM Cloud Pak for Data]{: tag-cp4d}

```bash
curl -X POST \
--header "Authorization: Bearer {token}" \
--output hello_world.wav \
"{url}/v1/synthesize?accept=audio%2Fwav&text=hello%20world&voice=en-US_AllisonV3Voice"
```
{: pre}

## Using the default voice
{: #specify-voice-default}

If you omit the `voice` parameter from a request, the service uses the US English `en-US_MichaelV3Voice` by default. This default applies to all speech synthesis requests and to the  `GET /v1/pronunciation` method.

[IBM Cloud Pak for Data]{: tag-cp4d} If you do not install the `en-US_MichaelV3Voice`, it cannot serve as the default voice. In this case, you must either

-   Use the `voice` parameter to pass the voice that is to be used with each request.
-   Specify a new default voice for your installation of {{site.data.keyword.texttospeechshort}} for {{site.data.keyword.icp4dfull_notm}} by using the `defaultTTSVoice` property in the Speech services custom resource. For more information, see  [Installing {{site.data.keyword.watson}} {{site.data.keyword.texttospeechshort}}](https://www.ibm.com/docs/en/cloud-paks/cp-data/4.0?topic=speech-installing-watson-text){: external}.

## Multilingual speech synthesis
{: #synthesis-multilingual}

The service does not support multilingual speech synthesis at this time. All synthesis is based on the language of the voice that is specified by the `voice` parameter. Depending on the language and the word in question, you might be able to use customization to approximate the pronunciation of a word in a language that is different from the voice of the request. For more information, see [Creating a custom model](/docs/text-to-speech?topic=text-to-speech-voices#customize-model).

If you decide to use customization to emulate pronunciation in a different language, use the HTTP `GET /v1/pronunciation` method to see the pronunciation of the word in the other language. The method returns the phonemes that the service uses to pronounce the word in that language. For more information, see [Phonetic translation](/docs/text-to-speech?topic=text-to-speech-customIntro#phonetic).

You can adjust the phonemes that the method returns to match as closely as possible the phonemes that are available in your language. You can then create a custom model that includes a custom word with that translation and use that model with your synthesis request. Becuase two different languages might not support the same phonemes, it might not be possible to match exactly the sounds and pronunciation of one language with the phonetic symbols of another language.

The Speech Synthesis Markup Language (SSML) `<speak>` element includes an `xml:lang` element, but that element applies to the entire request, and the service does not support its use as a way of specifying a different language for speech synthesis.
{: note}
