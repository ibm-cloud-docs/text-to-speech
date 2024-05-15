---

copyright:
  years: 2022, 2023
lastupdated: "2024-05-10"

subcollection: text-to-speech

---

{{site.data.keyword.attribute-definition-list}}

# How to modify speech synthesis
{: #synthesis-expressive}

The expressive neural voices that are available with the {{site.data.keyword.texttospeechfull}} service offer some additional features that are not available with other types of voices: *using speaking styles*, *emphasizing interjections*, and *emphasizing words*.  These features are available for both the HTTP and WebSocket interfaces.
{: shortdesc}

The features involve the use of elements of the Speech Synthesis Markup Language (SSML). The descriptions of the features provide information about how they interact with related SSML elements and attributes.

### Using speaking styles
{: #syntheses-expressive-styles}

The expressive neural voices determine the sentiment of the text from the context of its words and phrases. The speech that they produce, in addition to having a very conversational style, reflects the mood of the text. The expressive voices naturally express gratitude, thankfulness, happiness, empathy, confusion, and other sentiments by default, with no explicit additional tagging.

However, you can embellish the voices' natural tendencies by using the `<express-as>` element with the required `style` attribute to indicate that all or some of the text is to emphasize specific characteristics. These characteristics are referred to as speaking styles:

-   `cheerful` - Expresses happiness and good news. The style is upbeat, welcoming, and conveys a positive message. 
-   `empathetic` - Expresses empathy and compassion. The style has sympathetic undertones, but it is not excessively sorrowful.
-   `neutral` - Expresses objectivity and evenness. The style strives for less emotion, and instead conveys a more even and instructional tone.
-   `uncertain` - Expresses uncertainty and confusion. The style conveys the feeling of being unsure or in doubt.

In many cases, the effect of the styles is very subtle. In such cases, the differences might not be readily discernible from the default expressive tone. But there are instances where the style can audibly enhance the voices' inherent ability to detect and express emotion. The differences are often detectable only on certain words and phrases.

### Expressing speaking styles with SSML
{: #syntheses-expressive-styles-ssml}

The following HTTP request uses the `<express-as>` element with a `style` of `cheerful` to modify the speaking style of the entire input text. The example uses the `en-US_EmmaExpressive` voice.

[IBM Cloud]{: tag-ibm-cloud}

```sh
curl -X POST -u "apikey:{apikey}" \
--header "Content-Type: application/json" \
--header "Accept: audio/wav" \
--output full-cheerful-style.wav \
--data "{\"text\":\"<express-as style='cheerful'>Oh, that&apos;s good news! I am very happy for you!</express-as>\"}" \
"{url}/v1/synthesize?voice=en-US_EmmaExpressive"
```
{: pre}

[IBM Cloud Pak for Data]{: tag-cp4d}

```sh
curl -X POST \
--header "Authorization: Bearer {token}" \
--header "Content-Type: application/json" \
--header "Accept: audio/wav" \
--output full-cheerful-style.wav \
--data "{\"text\":\"<express-as style='cheerful'>Oh, that&apos;s good news! I am very happy for you!</express-as>\"}" \
"{url}/v1/synthesize?voice=en-US_EmmaExpressive"
```
{: pre}

The following example HTTP request uses the `cheerful` style for the first sentence of the request only. The second sentence is spoken with the default voice. The example again uses the `en-US_EmmaExpressive` voice.

[IBM Cloud]{: tag-ibm-cloud}

```sh
curl -X POST -u "apikey:{apikey}" \
--header "Content-Type: application/json" \
--header "Accept: audio/wav" \
--output partial-cheerful-style.wav \
--data "{\"text\":\"<express-as style='cheerful'>Oh, that&apos;s good news!</express-as> Do you need any further help?\"}" \
"{url}/v1/synthesize?voice=en-US_EmmaExpressive"
```
{: pre}

[IBM Cloud Pak for Data]{: tag-cp4d}

```sh
curl -X POST \
--header "Authorization: Bearer {token}" \
--header "Content-Type: application/json" \
--header "Accept: audio/wav" \
--output partial-cheerful-style.wav \
--data "{\"text\":\"<express-as style='cheerful'>Oh, that&apos;s good news!</express-as> Do you need any further help?\"}" \
"{url}/v1/synthesize?voice=en-US_EmmaExpressive"
```
{: pre}

### Emphasizing interjections
{: #syntheses-expressive-interjections}

When you use expressive neural voices, the service automatically detects a number of common interjections based on context. In the resulting audio, it gives them the natural emphasis that a human would use in normal conversation. Expressive voices support a different set of interjections based on language. Please refer to the language specific pages for more details on which interjections are supported.

### Enabling or disabling interjections with SSML
{: #syntheses-expressive-interjections-ssml}

The service always interprets and pronounces most of the interjections as expected. However, there are some interjections that could be used in a different context. In such cases, the default behaviour of the service is to disable such interjections by default. You can use SSML to enable or disable such interjections. The `interpret-as` attribute of the SSML `<say-as>` element accepts an additional value, `interjection`. When you use the `interpret-as` attribute with the `interjection` value, you include the additional `enabled` attribute with a value of `true` or `false` to indicate whether the word is to be pronounced as an interjection. Every language has a different subset of interjections that can be enabled/disabled through SSML. Please refer to the language specific pages for more details on which interjections can be enabled/disabled using SSML.

The following example HTTP request directs the service not to pronounce `oh` and `aha` as interjections. The example uses the `en-US_AllisonExpressive` voice.

[IBM Cloud]{: tag-ibm-cloud}

```bash
curl -X POST -u "apikey:{apikey}" \
--header "Content-Type: application/json" \
--header "Accept: audio/wav" \
--output disabled-interjections.wav \
--data "{\"text\":\"<say-as interpret-as='interjection' enabled='false'>Oh</say-as>, in addition, the <say-as interpret-as='interjection' enabled='false'>aha</say-as> wasp is endemic to Australia.\"}" \
"{url}/v1/synthesize?voice=en-US_AllisonExpesssive"
```
{: pre}

[IBM Cloud Pak for Data]{: tag-cp4d}

```sh
curl -X POST \
--header "Authorization: Bearer {token}" \
--header "Content-Type: application/json" \
--header "Accept: audio/wav" \
--output disabled-interjections.wav \
--data "{\"text\":\"<say-as interpret-as='interjection' enabled='false'>Oh</say-as>, in addition, the <say-as interpret-as='interjection' enabled='false'>aha</say-as> wasp is endemic to Australia.\"}" \
"{url}/v1/synthesize?voice=en-US_AllisonExpesssive"
```
{: pre}

## Emphasizing words
{: #syntheses-expressive-word-emphasis}

All the expressive voices use a conversational style that naturally applies the correct intonation from context. But you can use the SSML `<emphasis>` element to indicate that one or more words are to be given more or less emphasis in the synthesized audio. The change in stress can be indicated by an increase or decrease in pitch, timing, volume, or other acoustic attributes.

The `<emphasis>` element supports an optional `level` attribute that accepts one of the following values:

-   `none` - Prevents the service from emphasizing text that might otherwise be emphasized.
-   `moderate` - Provides a noticeable amount of emphasis to the text. This value is the default if you omit the `level` attribute.
-   `strong` - Provides a more significant amount of emphasis to the text than the `moderate` level provides.
-   `reduced` - De-emphasizes the text by tending to reduce its significance in the audio. This level is the opposite of stressing the text.

Table 3 provides examples of each available `level` for the `emphasis` element. The samples use the `en-US_MichaelExpressive` voice. A request that uses the `emphasis` element fails if a specified level is not one of the supported values.

| Level of emphasis | Example sentence | Audio sample |
|-------------------|------------------|:------------:|
| No emphasis | `"I am going to give her the book."` | ![No emphasis](https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples-emphasis/michael-emphasis-plain.wav){: audio controls} |
| `none` | `"I am going to give her the <emphasis level='none'>book</emphasis>."` | ![Emphasis: none](https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples-emphasis/michael-emphasis-none.wav){: audio controls} |
| `moderate` | `"I am going to <emphasis level='moderate'>give</emphasis> her the book."` | ![Emphasis: moderate](https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples-emphasis/michael-emphasis-moderate.wav){: audio controls} |
| `strong` | `"I am going to <emphasis level='strong'>give</emphasis> her the book."` | ![Emphasis: strong](https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples-emphasis/michael-emphasis-strong.wav){: audio controls} |
| `reduced` | `"I <emphasis level='reduced'>am going to give</emphasis> her the book."` | ![Emphasis: reduced](https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples-emphasis/michael-emphasis-reduced.wav){: audio controls} |
{: caption="Table 3. Emphasizing words"}

### Emphasizing a word with SSML
{: #syntheses-expressive-word-emphasis-example}

The following example HTTP request uses the `<emphasis>` element with a `level` of `moderate` (the default) to emphasize the word `give` in the sentence. The example uses the `en-US_MichaelExpressive` voice.

[IBM Cloud]{: tag-ibm-cloud}

```bash
curl -X POST -u "apikey:{apikey}" \
--header "Content-Type: application/json" \
--header "Accept: audio/wav" \
--output strong-emphasis.wav \
--data "{\"text\":\"I am going to <emphasis level='moderate'>give</emphasis> her the book.\"}" \
"{url}/v1/synthesize?voice=en-US_MichaelExpesssive"
```
{: pre}

[IBM Cloud Pak for Data]{: tag-cp4d}

```sh
curl -X POST \
--header "Authorization: Bearer {token}" \
--header "Content-Type: application/json" \
--header "Accept: audio/wav" \
--output strong-emphasis.wav \
--data "{\"text\":\"I am going to <emphasis level='moderate'>give</emphasis> her the book.\"}" \
"{url}/v1/synthesize?voice=en-US_MichaelExpesssive"
```
{: pre}
