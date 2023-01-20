---

copyright:
  years: 2022, 2023
lastupdated: "2023-01-14"

subcollection: text-to-speech

---

{{site.data.keyword.attribute-definition-list}}

# Modifying speech synthesis with expressive neural voices
{: #synthesis-expressive}

The expressive neural voices that are available with the {{site.data.keyword.texttospeechfull}} service offer some additional features that are not available with other types of voices: *using speaking styles*, *emphasizing interjections*, and *emphasizing words*.  These features are available for both the HTTP and WebSocket interfaces. Like the expressive voices themselves, they are available only for US English.
{: shortdesc}

The features involve the use of elements of the Speech Synthesis Markup Language (SSML). The descriptions of the features provide information about how they interact with related SSML elements and attributes.

## Using speaking styles
{: #syntheses-expressive-styles}

[IBM Cloud]{: tag-ibm-cloud}

The expressive neural voices determine the sentiment of the text from the context of its words and phrases. The speech that they produce, in addition to having a very conversational style, reflects the mood of the text. The expressive voices naturally express gratitude, thankfulness, happiness, empathy, confusion, and other sentiments by default, with no explicit additional tagging.

However, you can embellish the voices' natural tendencies by using the `<express-as>` element with the required `style` attribute to indicate that all or some of the text is to emphasize specific characteristics. These characteristics are referred to as speaking styles:

-   `cheerful` - Expresses happiness and good news. The style is upbeat, welcoming, and conveys a positive message.
-   `empathetic` - Expresses empathy and compassion. The style has sympathetic undertones, but it is not excessively sorrowful.
-   `neutral` - Expresses objectivity and evenness. The style strives for less emotion, and instead conveys a more even and instructional tone.
-   `uncertain` - Expresses uncertainty and confusion. The style conveys the feeling of being unsure or in doubt.

In many cases, the effect of the styles is very subtle. In such cases, the differences might not be readily discernible from the default expressive tone. But there are instances where the style can audibly enhance the voices' inherent ability to detect and express emotion. The differences are often detectable only on certain words and phrases.

Table 1 provides examples of each available `style` for the `<express-as>` element. To demonstrate the effect of the styles, the table provides two samples for each example. The first sample speaks the text with the default `en-US_EmmaExpressive` voice. The second sample speaks the same text with the same voice but with the indicated style. A request that uses the `<express-as>` element fails if the `style` is not one of the supported values or is omitted from the element.

| Style | Example input text | Audio sample |
|-------|--------------------|:------------:|
| `cheerful` | `"Oh, that&apos;s good news. I am very happy for you!"` | ![Speaking style: default cheerful](https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples-styles/emma-cheerful-default.wav){: audio controls} |
| | `"<express-as style='cheerful'>Oh, that&apos;s good news. I am very happy for you!</express-as>"` | ![Speaking style: cheerful](https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples-styles/emma-cheerful.wav){: audio controls} |
| `empathetic` | `"Oh, I&apos;m sorry to hear that. I know how difficult that can be."` | ![Speaking style: default empathetic](https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples-styles/emma-empathetic-default.wav){: audio controls} |
|  | `"<express-as style='empathetic'>Oh, I&apos;m sorry to hear that. I know how difficult that can be.</express-as>"` | ![Speaking style: empathetic](https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples-styles/emma-empathetic.wav){: audio controls} |
| `neutral` | `"A five-alarm fire early this morning claimed the lives of more than a dozen residents."` | ![Speaking style: default neutral](https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples-styles/emma-neutral-default.wav){: audio controls} |
|  | `"<express-as style='neutral'>A five-alarm fire early this morning claimed the lives of more than a dozen residents.</express-as>"` | ![Speaking style: neutral](https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples-styles/emma-neutral.wav){: audio controls} |
| `uncertain` | `"That&apos;s strange. Hmm, I don&apos;t know if I&apos;ve seen this before."` | ![Speaking style: default uncertain](https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples-styles/emma-uncertain-default.wav){: audio controls} |
|  | `"<express-as style='uncertain'>That&apos;s strange. Hmm, I don&apos;t know if I&apos;ve seen this before.</express-as>"` | ![Speaking style: uncertain](https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples-styles/emma-uncertain.wav){: audio controls} |
{: caption="Table 1. Speaking styles"}

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

<!--
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
-->

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

<!--
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
-->

## Emphasizing interjections
{: #syntheses-expressive-interjections}

[IBM Cloud]{: tag-ibm-cloud}

When you use expressive neural voices, the service automatically detects a number of common interjections based on context. In the resulting audio, it gives them the natural emphasis that a human would use in normal conversation.

Table 2 lists the interjections that the service recognizes and provides examples of how they are pronounced in synthesized speech. The samples use the `en-US_AllisonExpressive` voice. The table shows the primary spelling of each interjection. The service recognizes alternative spellings for some of the interjections. For example, `oh` and `ohh` produce the same sound, as do `hmm` and `hmmm`. However, the service produces slightly different pronunciations for other alternative spellings, such as `ooh` and `uhm`,

| Interjection | Example sentence | Audio sample |
|--------------|------------------|:------------:|
| `aha` | `"Aha. So that&apos;s the secret."` | ![Interjection: Aha](https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples-interjections/allison-interjection-aha.wav){: audio controls} |
| `hmm` | `"Hmm. I&apos;m not sure I understand."` | ![Interjection: Hmm](https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples-interjections/allison-interjection-hmm.wav){: audio controls} |
| `huh` | `"Huh, I hadn&apos;t noticed that."` | ![Interjection: Huh](https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples-interjections/allison-interjection-huh.wav){: audio controls} |
| `oh` | `"Oh, let me get that for you."` | ![Interjection: Oh](https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples-interjections/allison-interjection-oh.wav){: audio controls} |
| `uh` | `"Uh, let me check."` | ![Interjection: Uh](https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples-interjections/allison-interjection-uh.wav){: audio controls} |
| `uh-huh` | `"Uh-huh, that&apos;s right."` | ![Interjection: Uh-huh](https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples-interjections/allison-interjection-uh-huh.wav){: audio controls} |
| `um` | `"That&apos;s, um, not quite right."` | ![Interjection: Um](https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples-interjections/allison-interjection-um.wav){: audio controls} |
{: caption="Table 2. Interjections that are emphasized"}

### Enabling or disabling interjections with SSML
{: #syntheses-expressive-interjections-ssml}

The service always interprets and pronounces most of the interjections as described in the previous section. However, you can use SSML to enable or disable the interjections `aha` and `oh`. The `interpret-as` attribute of the SSML `<say-as>` element accepts an additional value, `interjection`. When you use the `interpret-as` attribute with the `interjection` value, you include the additional `enabled` attribute with a value of `true` or `false` to indicate whether the word is to be pronounced as an interjection.

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

<!--
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
-->

### Usage notes for interjections
{: #syntheses-expressive-interjections-notes}

Keep the following in mind when using interjections:

-   The `<say-as>` element with the `interpret-as="interjection"` attribute has no effect if the word to be modified is not one of the interjections `aha` or `oh`.
-   Including punctuation with the text that is to be modified can affect whether the interjection is enabled or disabled. Do not include any punctuation characters with the word inside of the `<say-as>` tag.
-   The word `oh`, when used colloquially to indicate the number zero, is never treated as an interjection. For example, the word is not emphasized as an interjection in the following sentence: `The number is one oh three.`
-   The neutral style does not emphasize interjections to the extent of the default expressive voice or the other styles.

## Emphasizing words
{: #syntheses-expressive-word-emphasis}

[IBM Cloud]{: tag-ibm-cloud}

The expressive voices use a conversational style that naturally applies the correct intonation from context. But you can use the SSML `<emphasis>` element to indicate that one or more words are to be given more or less emphasis in the synthesized audio. The change in stress can be indicated by an increase or decrease in pitch, timing, volume, or other acoustic attributes.

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

<!--
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
-->
