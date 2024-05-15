---

copyright:
  years: 2022, 2023
lastupdated: "2024-05-10"

subcollection: text-to-speech

---

{{site.data.keyword.attribute-definition-list}}

# English expressive voices
{: #expressive-english}

## Speaking styles
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

## Emphasizing interjections
{: #syntheses-expressive-interjections-en}

For English, we currently support the following interjections - `aha`, `hmm`, `huh`, `oh`, `uh`, `uh-huh` and `um`.

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
{: #syntheses-expressive-interjections-ssml-en}
For English, it is possible to enable/disable the following interjections using SSML - `aha` and `oh`.

### Usage notes for interjections
{: #syntheses-expressive-interjections-notes-en}

Keep the following in mind when using interjections:

-   The `<say-as>` element with the `interpret-as="interjection"` attribute has no effect if the word to be modified is not one of the interjections `aha` or `oh`.
-   Including punctuation with the text that is to be modified can affect whether the interjection is enabled or disabled. Do not include any punctuation characters with the word inside of the `<say-as>` tag.
-   The word `oh`, when used colloquially to indicate the number zero, is never treated as an interjection. For example, the word is not emphasized as an interjection in the following sentence: `The number is one oh three.`
-   The neutral style does not emphasize interjections to the extent of the default expressive voice or the other styles.