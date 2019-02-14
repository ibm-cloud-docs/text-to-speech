---

copyright:
  years: 2015, 2019
lastupdated: "2019-02-14"

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

# Languages and voices
{: #voices}

The {{site.data.keyword.texttospeechfull}} service supports a variety of languages, voices, and dialects. The service offers at least one male or female voice, sometimes both, for each language. Each voice uses appropriate cadence and intonation for its dialect.
{: shortdesc}

## Supported languages and voices
{: #languageVoices}

Table 1 lists the voices that are available for each language and dialect, including their gender. If you omit the optional `voice` parameter from a request, the service uses the `en-US_MichaelVoice` voice by default.

<table style="width:90%">
  <caption>Table 1. Supported languages and voices</caption>
  <tr>
    <th style="text-align:left">Languages</th>
    <th style="text-align:center">Voice</th>
    <th style="text-align:center">Gender</th>
  </tr>
  <tr>
    <td style="text-align:left">Brazilian Portuguese</td>
    <td style="text-align:center"><code>pt-BR_IsabelaVoice</code></td>
    <td style="text-align:center">Female</td>
  </tr>
  <tr>
    <td style="text-align:left">Castilian Spanish</td>
    <td style="text-align:center"><code>es-ES_EnriqueVoice</code></td>
    <td style="text-align:center">Male</td>
  </tr>
  <tr>
    <td></td>
    <td style="text-align:center"><code>es-ES_LauraVoice</code></td>
    <td style="text-align:center">Female</td>
  </tr>
  <tr>
    <td style="text-align:left">French</td>
    <td style="text-align:center"><code>fr-FR_ReneeVoice</code></td>
    <td style="text-align:center">Female</td>
  </tr>
  <tr>
    <td style="text-align:left">German</td>
    <td style="text-align:center"><code>de-DE_BirgitVoice</code></td>
    <td style="text-align:center">Female</td>
  </tr>
  <tr>
    <td></td>
    <td style="text-align:center"><code>de-DE_DieterVoice</code></td>
    <td style="text-align:center">Male</td>
  </tr>
  <tr>
    <td style="text-align:left">Italian</td>
    <td style="text-align:center"><code>it-IT_FrancescaVoice</code></td>
    <td style="text-align:center">Female</td>
  </tr>
  <tr>
    <td style="text-align:left">Japanese</td>
    <td style="text-align:center"><code>ja-JP_EmiVoice</code></td>
    <td style="text-align:center">Female</td>
  </tr>
  <tr>
    <td style="text-align:left">Latin American Spanish</td>
    <td style="text-align:center"><code>es-LA_SofiaVoice</code></td>
    <td style="text-align:center">Female</td>
  </tr>
  <tr>
    <td style="text-align:left">North American Spanish</td>
    <td style="text-align:center"><code>es-US_SofiaVoice</code></td>
    <td style="text-align:center">Female</td>
  </tr>
  <tr>
    <td style="text-align:left">UK English</td>
    <td style="text-align:center"><code>en-GB_KateVoice</code></td>
    <td style="text-align:center">Female</td>
  </tr>
  <tr>
    <td style="text-align:left">US English</td>
    <td style="text-align:center"><code>en-US_AllisonVoice</code></td>
    <td style="text-align:center">Female</td>
  </tr>
  <tr>
    <td></td>
    <td style="text-align:center"><code>en-US_LisaVoice</code></td>
    <td style="text-align:center">Female</td>
  </tr>
  <tr>
    <td></td>
    <td style="text-align:center"><code>en-US_MichaelVoice</code></td>
    <td style="text-align:center">Male</td>
  </tr>
</table>

The voices `es-LA_SofiaVoice` and `es-US_SofiaVoice` are essentially the same voice. The most significant difference concerns how the two voices interpret a `$` (dollar sign). The Latin American version uses the term *pesos*, while the North American version uses the term *dolares*. Other minor differences might exist between the two voices.
{: note}

### Voice customization
{: #customizeVoice}

When you synthesize text, the service applies language-dependent pronunciation rules to convert the ordinary spelling of each word to a phonetic spelling. The service's pronunciation rules work well for common words, but they can yield imperfect results for unusual words, such as terms with foreign origins, personal names, and abbreviations or acronyms.

If your application's lexicon includes such words, you can use the customization interface to specify how the service pronounces them. For more information, see [Understanding customization](/docs/services/text-to-speech/custom-intro.html).

## Specifying a voice
{: #specifyVoice}

Both the HTTP `GET` and `POST /v1/synthesize` methods, as well as the WebSocket `/v1/synthesize` method, accept an optional `voice` query parameter to specify the voice for the synthesized audio. For more information, see [The HTTP interface](/docs/services/text-to-speech/http.html) and [The WebSocket interface](/docs/services/text-to-speech/websockets.html).

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
      model that is defined for the specified voice. If you include a
      customization ID, you must call the method with the service
      credentials of the custom model's owner.
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

The attributes of the additional `customization` field provide information such as the GUID, name, language, and description of the custom voice model. They also show the service credentials of the model's owner, the date and time at which the model was created, and the date and time of its last modification.
