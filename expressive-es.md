---

copyright:
  years: 2022, 2023
lastupdated: "2024-05-10"

subcollection: text-to-speech

---

{{site.data.keyword.attribute-definition-list}}

# Spanish expressive voices
{: #expressive-spanish}

## Speaking styles
Table 1 provides examples of each available `style` for the `<express-as>` element for Spanish. To demonstrate the effect of the styles, the table provides two samples for each example. The first sample speaks the text with the default `es-LA_DanielaExpressive` voice. The second sample speaks the same text with the same voice but with the indicated style. A request that uses the `<express-as>` element fails if the `style` is not one of the supported values or is omitted from the element.

| Style | Example input text | Audio sample |
|-------|--------------------|:------------:|
| `cheerful` | `"¡Excelente! ¿Hay algo más en lo que pueda ayudarte?"` | ![Speaking style: default cheerful](https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples-styles/daniela-cheerful-default.wav){: audio controls} |
| | `"<express-as style="cheerful"> ¡Excelente! ¿Hay algo más en lo que pueda ayudarte? </express-as>"` | ![Speaking style: cheerful](https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples-styles/daniela-cheerful.wav){: audio controls} |
| `empathetic` | `"Lamento escuchar que este asunto aún no se ha resuelto, y le pido disculpas."` | ![Speaking style: default empathetic](https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples-styles/daniela-empathetic-default.wav){: audio controls} |
|  | `"<express-as style="empathetic"> Lamento escuchar que este asunto aún no se ha resuelto, y le pido disculpas. </express-as>"` | ![Speaking style: empathetic](https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples-styles/daniela-empathetic.wav){: audio controls} |
| `neutral` | `"Durante el otoño, el clima es ventoso."` | ![Speaking style: default neutral](https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples-styles/daniela-neutral-default.wav){: audio controls} |
|  | `"<express-as style="neutral"> Durante el otoño, el clima es ventoso. </express-as>"` | ![Speaking style: neutral](https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples-styles/daniela-neutral.wav){: audio controls} |
| `uncertain` | `"Disculpe, pero ¿le importaría repetir lo que me decía? No logré oirlo bien."` | ![Speaking style: default uncertain](https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples-styles/daniela-uncertain-default.wav){: audio controls} |
|  | `"<express-as style="uncertain"> Disculpe, pero ¿le importaría repetir lo que me decía? No logré oirlo bien. </express-as>"` | ![Speaking style: uncertain](https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples-styles/daniela-uncertain.wav){: audio controls} |
{: caption="Table 1. Speaking styles"}

## Emphasizing interjections
{: #syntheses-expressive-interjections-es}

For Spanish, we currently support the following interjections - `aah`, `ajá`, `eh`, `oh` and `uf`.

Table 2 lists the interjections that the service recognizes and provides examples of how they are pronounced in synthesized speech. The samples use the `es-LA_DanielaExpressive` voice. The table shows the primary spelling of each interjection. The service recognizes alternative spellings for some of the interjections. For example, `oh` and `ohh` produce the same sound, as do `uf` and `uff`. However, the service produces slightly different pronunciations for other alternative spellings, such as `ah` and `eeh`.

| Interjection | Example sentence | Audio sample |
|--------------|------------------|:------------:|
| `aah` | `"Aah, ese pago ya fue realizado la semana pasada, y su cuenta quedó saldada."` | ![Interjection: Aah](https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples-interjections/daniela-interjection-aah.wav){: audio controls} |
| `ajá` | `"¡Ajá, ya logré localizar su pedido! Está en camino y llegará dentro de 24 horas."` | ![Interjection: Ajá](https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples-interjections/daniela-interjection-aja.wav){: audio controls} |
| `eh` | `"Eh, no sé si podremos enviar un técnico a su residencia antes del miércoles."` | ![Interjection: Eh](https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples-interjections/daniela-interjection-eh.wav){: audio controls} |
| `oh` | `"Oh, claro que podemos guardar su equipaje en consigna hasta la hora de su salida. No hay problemas."` | ![Interjection: Oh](https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples-interjections/daniela-interjection-oh.wav){: audio controls} |
| `uf` | `"Uf, no creo que pueda concertarle una cita hasta que recibamos sus documentos."` | ![Interjection: Uf](https://watson-developer-cloud.github.io/doc-tutorial-downloads/text-to-speech/samples-interjections/daniela-interjection-uf.wav){: audio controls} |
{: caption="Table 2. Interjections that are emphasized"}

### Enabling or disabling interjections with SSML
{: #syntheses-expressive-interjections-ssml-es}
For Spanish, all interjections are enabled by default, and it is not possible to enable/disable these interjections.

### Usage notes for interjections
{: #syntheses-expressive-interjections-notes-es}

Keep the following in mind when using interjections:

-   The neutral style does not emphasize interjections to the extent of the default expressive voice or the other styles.