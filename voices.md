---

copyright:
  years: 2015, 2019
lastupdated: "2019-10-01"

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

# Languages and voices
{: #voices}

The {{site.data.keyword.texttospeechfull}} service supports a variety of languages, voices, and dialects. The service offers at least one female voice for each language. For some languages the service offers multiple voices, including both male and female voices. Each voice uses appropriate cadence and intonation for its dialect.
{: shortdesc}

The `V2` voices that were previously available with the service have been discontinued. If you use a `V2` voice in your application, the service automatically uses the equivalent `V3` voice instead.
{: note}

## Supported languages and voices
{: #languageVoices}

Table 1 lists the voices that are available for each language and dialect. All voices are available as both [Standard voices](#standardVoices) and [Neural voices](#neuralVoices). If you omit the optional `voice` parameter from a request, the service uses the standard `en-US_MichaelVoice` by default.

<table style="width:100%">
  <caption>Table 1. Supported languages and voices</caption>
  <tr>
    <th style="text-align:left">Language</th>
    <th style="text-align:center">Gender</th>
    <th style="text-align:center">Standard voice</th>
    <th style="text-align:center">Neural voice</th>
  </tr>
  <tr>
    <td style="text-align:left">Brazilian Portuguese</td>
    <td style="text-align:center">Female</td>
    <td style="text-align:center"><code>pt-BR_IsabelaVoice</code></td>
    <td style="text-align:center"><code>pt-BR_IsabelaV3Voice</code></td>
  </tr>
  <tr>
    <td style="text-align:left">English (United Kingdom)</td>
    <td style="text-align:center">Female</td>
    <td style="text-align:center"><code>en-GB_KateVoice</code></td>
    <td style="text-align:center"><code>en-GB_KateV3Voice</code></td>
  </tr>
  <tr>
    <td style="text-align:left">English (United States)</td>
    <td style="text-align:center">Female</td>
    <td style="text-align:center"><code>en-US_AllisonVoice</code></td>
    <td style="text-align:center"><code>en-US_AllisonV3Voice</code></td>
  </tr>
  <tr>
    <td style="text-align:left"></td>
    <td style="text-align:center">Female</td>
    <td style="text-align:center"><code>en-US_LisaVoice</code></td>
    <td style="text-align:center"><code>en-US_LisaV3Voice</code></td>
  </tr>
  <tr>
    <td style="text-align:left"></td>
    <td style="text-align:center">Male</td>
    <td style="text-align:center"><code>en-US_MichaelVoice</code></td>
    <td style="text-align:center"><code>en-US_MichaelV3Voice</code></td>
  </tr>
  <tr>
    <td style="text-align:left">French</td>
    <td style="text-align:center">Female</td>
    <td style="text-align:center"><code>fr-FR_ReneeVoice</code></td>
    <td style="text-align:center"><code>fr-FR_ReneeV3Voice</code></td>
  </tr>
  <tr>
    <td style="text-align:left">German</td>
    <td style="text-align:center">Female</td>
    <td style="text-align:center"><code>de-DE_BirgitVoice</code></td>
    <td style="text-align:center"><code>de-DE_BirgitV3Voice</code></td>
  </tr>
  <tr>
    <td style="text-align:left"></td>
    <td style="text-align:center">Male</td>
    <td style="text-align:center"><code>de-DE_DieterVoice</code></td>
    <td style="text-align:center"><code>de-DE_DieterV3Voice</code></td>
  </tr>
  <tr>
    <td style="text-align:left">Italian</td>
    <td style="text-align:center">Female</td>
    <td style="text-align:center"><code>it-IT_FrancescaVoice</code></td>
    <td style="text-align:center"><code>it-IT_FrancescaV3Voice</code></td>
  </tr>
  <tr>
    <td style="text-align:left">Japanese</td>
    <td style="text-align:center">Female</td>
    <td style="text-align:center"><code>ja-JP_EmiVoice</code></td>
    <td style="text-align:center"><code>ja-JP_EmiV3Voice</code></td>
  </tr>
  <tr>
    <td style="text-align:left">Spanish (Castilian)</td>
    <td style="text-align:center">Male</td>
    <td style="text-align:center"><code>es-ES_EnriqueVoice</code></td>
    <td style="text-align:center"><code>es-ES_EnriqueV3Voice</code></td>
  </tr>
  <tr>
    <td style="text-align:left"></td>
    <td style="text-align:center">Female</td>
    <td style="text-align:center"><code>es-ES_LauraVoice</code></td>
    <td style="text-align:center"><code>es-ES_LauraV3Voice</code></td>
  </tr>
  <tr>
    <td style="text-align:left">Spanish (Latin American)</td>
    <td style="text-align:center">Female</td>
    <td style="text-align:center"><code>es-LA_SofiaVoice</code></td>
    <td style="text-align:center"><code>es-LA_SofiaV3Voice</code></td>
  </tr>
  <tr>
    <td style="text-align:left">Spanish (North American)</td>
    <td style="text-align:center">Female</td>
    <td style="text-align:center"><code>es-US_SofiaVoice</code></td>
    <td style="text-align:center"><code>es-US_SofiaV3Voice</code></td>
  </tr>
</table>

The voices `es-LA_SofiaVoice` and `es-US_SofiaVoice` are essentially the same voice. The most significant difference concerns how the two voices interpret a $ (dollar sign). The Latin American version uses the term *pesos*, while the North American version uses the term *d&oacute;lares*. Other minor differences might also exist between the two voices.
{: note}

### Standard voices
{: #standardVoices}

Standard voices do not include a version string (`V3`) in their name (for example, `pt-BR_IsabelaVoice` and `en-US_AllisonVoice`). Standard voices use concatenative synthesis to assemble segments (or units) of recorded speech to generate the requested audio. The concatenation points of the recorded segments sometimes result in speech discontinuities that can degrade the quality and naturalness of the resulting speech.

### Neural voices
{: #neuralVoices}

Neural voices include a version string (`V3`) in their name (for example, `pt-BR_IsabelaV3Voice` and `en-US_AllisonV3Voice`). Instead of relying on segment selection and concatenation, neural voice technology uses multiple Deep Neural Networks (DNNs) to predict the acoustic (spectral) features of the speech. The DNNs are trained on natural human speech and generate the resulting audio from the predicted acoustic features.

During synthesis, the DNNs predict the pitch and phoneme duration (prosody), spectral structure, and waveform of the speech. Neural voices produce speech that is crisp and clear, with a very natural-sounding and smooth audio quality. Thus, neural voices have greater consistency in overall quality than standard voices.

For more information about the service's neural voice technology, see

-   The blog post [IBM Watson Text to Speech: Neural Voices Generally Available](https://medium.com/ibm-watson/ibm-watson-text-to-speech-neural-voices-added-to-service-e562106ff9c7){: external}
-   The research paper [High quality, lightweight and adaptable Text to Speech using LPCNet](https://arxiv.org/abs/1905.00590){: external}

The neural voices do not support the following SSML elements or attributes:

-   The `volume` attribute of the `<prosody>` element
-   The `<express-as>` element
-   The `<voice-transformation>` element

However, you might find that these SSML features are no longer needed when using the neural voices. Also, you can make pitch and rate modifications to neural voices by using the `<prosody>` element in place of the `<voice-transformation>` element. For more information, see [The prosody element](/docs/services/text-to-speech?topic=text-to-speech-elements#prosody_element).

### Voice customization
{: #customizeVoice}

When you synthesize text, the service applies language-dependent pronunciation rules to convert the ordinary spelling of each word to a phonetic spelling. The service's pronunciation rules work well for common words, but they can yield imperfect results for unusual words, such as terms with foreign origins, personal names, and abbreviations or acronyms.

If your application's lexicon includes such words, you can use the customization interface to specify how the service pronounces them. For more information, see [Understanding customization](/docs/services/text-to-speech?topic=text-to-speech-customIntro).

You create a custom voice model for a specific language, not for a specific voice. So a custom model can be used with any voice, standard or neural, for its specified language.

## Specifying a voice
{: #specifyVoice}

Both the HTTP `GET` and `POST /v1/synthesize` methods, as well as the WebSocket `/v1/synthesize` method, accept an optional `voice` query parameter to specify the voice for the synthesized audio. For more information, see [The HTTP interface](/docs/services/text-to-speech?topic=text-to-speech-usingHTTP) and [The WebSocket interface](/docs/services/text-to-speech?topic=text-to-speech-usingWebSocket).

The service bases its understanding of the language for the input text on the specified voice. Be sure to specify a voice that matches the language of the input text. For example, if you specify the French voice (`fr-FR_ReneeVoice`), the service assumes that the input text is written in French. If you pass text that is not written in the language of the voice (for example, English text for the French voice), the service might not produce meaningful results.

## Listing all available voices
{: #listVoices}

The `GET /v1/voices` method lists information about all available voices. It takes no arguments and returns a JSON array that is named `voices`. The array includes a separate object for each voice.

```javascript
{
  "voices": [
    {
      "name": "en-US_LisaVoice",
      "language": "en-US",
      "gender": "female",
      "url": "https://stream.watsonplatform.net/text-to-speech/api/v1/voices/en-US_LisaVoice",
      "description": "Lisa: American English female voice.",
      "customizable": true,
      "supported_features": {
        "voice_transformation": true,
        "custom_pronunciation": true
      }
    },
    . . .
  ]
}
```
{: codeblock}

The fields of the voice objects provide the following information:

-   `name` is an identifier for the voice (for example, `en-US_LisaVoice`). Specify this value for the `voice` parameter of the `/v1/synthesize` method.
-   `language` specifies the language and region of the voice (for example, `en-US`).
-   `gender` identifies the voice as `male` or `female`.
-   `url` identifies the URL for the voice.
-   `description` provides a brief description of the voice.
-   `customizable` is a boolean value that indicates whether the voice can be customized with the service's customization interface. (This field, which provides the same information as the `custom_pronunciation` field, is maintained for backward compatibility.)
-   `supported_features` describes the additional service features that are supported by the voice:
    -   `voice_transformation` is a boolean value that indicates whether the voice can be transformed by using the SSML `<voice-transformation>` element.
    -   `custom_pronunciation` is a boolean value that indicates whether the voice can be customized with the service's customization interface.

## Listing a specific voice
{: #listVoice}

The `GET /v1/voices/{voice}` method lists information about a specific voice. It accepts two parameters.

<table>
  <caption>Table 2. Parameters of the <code>voices</code> method</caption>
  <tr>
    <th style="text-align:left; width:18%">Parameter</th>
    <th style="text-align:center; width:12%">Type</th>
    <th style="text-align:center; width:12%">Data type</th>
    <th style="text-align:left">Description</th>
  </tr>
  <tr>
    <td><code>voice</code><br/><em>Required</em></td>
    <td style="text-align:center">Path</td>
    <td style="text-align:center">String</td>
    <td>
      Identifies the voice for which information is to be returned. You
      specify a voice by its name (for example, <code>en-US_LisaVoice</code>).
    </td>
  </tr>
  <tr>
    <td><code>customization_id</code><br/><em>Optional</em></td>
    <td style="text-align:center">Query</td>
    <td style="text-align:center">String</td>
    <td>
      Provides the globally unique identifier (GUID) of a custom voice
      model that is defined for the language of the specified voice. If
      you include a customization ID, you must make the request with
      credentials for the instance of the service that owns the custom
      model.
    </td>
  </tr>
</table>

If you omit the `customization_id` parameter, the method returns JSON output for the specified voice that is identical to the information returned for a voice by the `GET /v1/voices` method. If you specify a `customization_id`, the output includes a `customization` field that provides information about the specified custom voice model.

```javascript
{
  "name": "en-US_LisaVoice",
  "language": "en-US",
  "gender": "female",
  "url": "https://stream.watsonplatform.net/text-to-speech/api/v1/voices/en-US_LisaVoice",
  "description": "Lisa: American English female voice.",
  "customizable": true,
  "supported_features": {
    "voice_transformation": true,
    "custom_pronunciation": true
  },
  "customization": {
    "customization_id": "64f4807f-a5f1-5867-924f-7bba1a84fe97",
    "owner": "297cfd08-330a-22ba-93ce-1a73f454dd98",
    "created": "2017-09-16T17:12:31.743Z",
    "name": "curl Test",
    "language": "en-US",
    "description": "Customization test via curl",
    "last_modified": "2017-09-16T17:12:31.743Z"
  }
}
```
{: codeblock}

The attributes of the additional `customization` field provide information such as the GUID, name, language, and description of the custom voice model. They also show the credentials of the model's owner, the date and time at which the model was created, and the date and time of its last modification.
