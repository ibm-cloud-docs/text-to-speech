---

copyright:
  years: 2025
lastupdated: "2025-02-17"

subcollection: text-to-speech

---

{{site.data.keyword.attribute-definition-list}}

# Portuguese expressive voices
{: #expressive-portuguese}

## Speaking styles
{: #speaking-styles-portuguese}

Table 1 provides examples of each available `style` for the `<express-as>` element for Portuguese. To demonstrate the effect of the styles, the table provides two samples for each example. The first sample speaks the text with the default `pt-BR_LucasExpressive` voice. The second sample speaks the same text with the same voice but with the indicated style. A request that uses the `<express-as>` element fails if the `style` is not one of the supported values or is omitted from the element.

| Style | Example input text | Audio sample |
|-------|--------------------|:------------:|
| `cheerful` | `"Claro! Que ótima notícia!"` | ![Speaking style: default cheerful](https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples-styles/pt-br-lucas-cheerful_untagged.wav){: audio controls} |
| | `"<express-as style="cheerful"> Claro! Que ótima notícia! </express-as>"` | ![Speaking style: cheerful](https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples-styles/pt-br-lucas-cheerful_tagged.wav){: audio controls} |
| `empathetic` | `"Infelizmente, não vou conseguir te ajudar nisso."` | ![Speaking style: default empathetic](https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples-styles/pt-br-lucas-empathetic_untagged.wav){: audio controls} |
|  | `"<express-as style="empathetic"> Infelizmente, não vou conseguir te ajudar nisso. </express-as>"` | ![Speaking style: empathetic](https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples-styles/pt-br-lucas-empathetic_tagged.wav){: audio controls} |
| `neutral` | `"O clima é muito seco no outono."` | ![Speaking style: default neutral](https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples-styles/pt-br-lucas-neutral_untagged.wav){: audio controls} |
|  | `"<express-as style="neutral"> O clima é muito seco no outono. </express-as>"` | ![Speaking style: neutral](https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples-styles/pt-br-lucas-neutral_tagged.wav){: audio controls} |
| `uncertain` | `"Desculpe, poderia repetir seu número novamente?"` | ![Speaking style: default uncertain](https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples-styles/pt-br-lucas-uncertain_untagged.wav){: audio controls} |
|  | `"<express-as style="uncertain"> Desculpe, poderia repetir seu número novamente? </express-as>"` | ![Speaking style: uncertain](https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples-styles/pt-br-lucas-uncertain_tagged.wav){: audio controls} |
{: caption="Speaking styles"}

## Emphasizing interjections
{: #syntheses-expressive-interjections-pt}

For Portuguese, we currently support the following interjections - `ah`, `aham`, `ahn`, `eh`, `hum` and `uhum`.

Table 2 lists the interjections that the service recognizes and provides examples of how they are pronounced in synthesized speech. The samples use the `pt-BR_LucasExpressive` voice. The table shows the primary spelling of each interjection. The service recognizes alternative spellings for some of the interjections. For example, `eh` and `ehh` produce the same sound, as do `hum` and `humm`. However, the service produces slightly different pronunciations for other alternative spellings, such as `aah` and `eeh`.

| Interjection | Example sentence | Audio sample |
|--------------|------------------|:------------:|
| `ah` | `"Ah, não tem problema algum!"` | ![Interjection: Ah](https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples-interjections/pt-br-lucas-interjection-ah.wav){: audio controls} |
| `aham` | `"Aham, já encaminharemos para você imediatamente."` | ![Interjection: Aham](https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples-interjections/pt-br-lucas-interjection-aham.wav){: audio controls} |
| `ahn` | `"Ahn, poderia aguardar na linha por favor?"` | ![Interjection: Ahn](https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples-interjections/pt-br-lucas-interjection-ahn.wav){: audio controls} |
| `eh` | `"Eh, só um segundinho que vou checar com meu gerente."` | ![Interjection: Eh](https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples-interjections/pt-br-lucas-interjection-eh.wav){: audio controls} |
| `hum` | `"Hum, não tenho muita certeza disso."` | ![Interjection: Hum](https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples-interjections/pt-br-lucas-interjection-hum.wav){: audio controls} |
| `uhum` | `"Uhum, seu pacote será entregue até o final do dia!"` | ![Interjection: Uhum](https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples-interjections/pt-br-lucas-interjection-uhum.wav){: audio controls} |
{: caption="Interjections that are emphasized"}

### Enabling or disabling interjections with SSML
{: #syntheses-expressive-interjections-ssml-pt}

For Spanish, all interjections are enabled by default, and it is not possible to enable/disable these interjections.

### Usage notes for interjections
{: #syntheses-expressive-interjections-notes-pt}

Keep the following in mind when using interjections:

-   The neutral style does not emphasize interjections to the extent of the default expressive voice or the other styles.
