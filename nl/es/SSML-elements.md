---

copyright:
  years: 2015, 2019
lastupdated: "2019-06-21"

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

# Elementos SSML
{: #elements}

Con el servicio {{site.data.keyword.texttospeechfull}}, puede utilizar la mayoría de los elementos SSML (Synthesis Markup Language) para controlar la síntesis del texto. Los elementos están disponibles para todos los idiomas soportados. En la tabla siguiente se ofrece un resumen del soporte del servicio de elementos y atributos SSML.

-   *Completo* significa que el servicio da soporte completo al elemento o atributo con sus interfaces HTTP y WebSocket.
-   *Parcial* significa que el servicio no da soporte a todos los aspectos del elemento o atributo. También puede significar que el servicio da soporte al elemento o atributo con sólo una de sus interfaces, o que el elemento o atributo no está soportado con todas las voces.
-   *Ninguno* significa que el servicio no da soporte al elemento o atributo.

Para obtener más información sobre un elemento o atributo, consulte su descripción. Allí donde se indique, el soporte para algunos atributos y valores difiere ligeramente de la especificación SSML. Para obtener más información, consulte la [Versión 1.0 de W3C Speech Synthesis Markup Language (SSML)](http://www.w3.org/TR/speech-synthesis/){: external}.

<table>
  <caption>Tabla 1. Elementos SSML</caption>
  <tr>
    <th style="text-align:left; width:30%">Elemento o atributo</th>
    <th style="text-align:center; width:12%">Soporte</th>
    <th style="text-align:left; width:46%; padding-left:75px">Elemento o atributo</th>
    <th style="text-align:center; width:12%">Soporte</th>
  </tr>
  <tr>
    <td>[Audio](#audio_element)</td>
    <td style="text-align:center">Ninguno</td>
    <td style="padding-left:75px">[Say-as](#say-as_element)</td>
    <td style="text-align:center">Parcial</td>
  </tr>
  <tr>
    <td>[Break](#break_element)</td>
    <td style="text-align:center">Completo</td>
    <td style="padding-left:100px">[cardinal](#sayAsCardinal)</td>
    <td style="text-align:center">Parcial</td>
  </tr>
  <tr>
    <td>[Desc](#desc_element)</td>
    <td style="text-align:center">Ninguno</td>
    <td style="padding-left:100px">[date](#sayAsDate)</td>
    <td style="text-align:center">Parcial</td>
  </tr>
  <tr>
    <td>[Emphasis](#emphasis_element)</td>
    <td style="text-align:center">Ninguno</td>
    <td style="padding-left:100px">[digits](#sayAsDigits)</td>
    <td style="text-align:center">Parcial</td>
  </tr>
  <tr>
    <td>[Lexicon](#lexicon_element)</td>
    <td style="text-align:center">Ninguno</td>
    <td style="padding-left:100px">[letters](#sayAsLetters)</td>
    <td style="text-align:center">Parcial</td>
  </tr>
  <tr>
    <td>[Mark](#mark_element)</td>
    <td style="text-align:center">Parcial</td>
    <td style="padding-left:100px">[number](#sayAsNumber)</td>
    <td style="text-align:center">Parcial</td>
  </tr>
  <tr>
    <td>[Meta](#mm_element)</td>
    <td style="text-align:center">Ninguno</td>
    <td style="padding-left:125px">cardinal</td>
    <td style="text-align:center">Parcial</td>
  </tr>
  <tr>
    <td>[Metadata](#mm_element)</td>
    <td style="text-align:center">Ninguno</td>
    <td style="padding-left:125px">ordinal</td>
    <td style="text-align:center">Parcial</td>
  </tr>
  <tr>
    <td>[Paragraph](#ps_element)</td>
    <td style="text-align:center">Completo</td>
    <td style="padding-left:125px">telephone</td>
    <td style="text-align:center">Parcial</td>
  </tr>
  <tr>
    <td>[Phoneme](#phoneme_element)</td>
    <td style="text-align:center">Completo</td>
    <td style="padding-left:150px">punctuation</td>
    <td style="text-align:center">Parcial</td>
  </tr>
  <tr>
    <td style="padding-left:25px">IBM SPR</td>
    <td style="text-align:center">Completo</td>
    <td style="padding-left:100px">[ordinal](#sayAsOrdinal)</td>
    <td style="text-align:center">Parcial</td>
  </tr>
  <tr>
    <td style="padding-left:25px">IPA</td>
    <td style="text-align:center">Completo</td>
    <td style="padding-left:100px">[vxml:boolean](#vxml-boolean)</td>
    <td style="text-align:center">Parcial</td>
  </tr>
  <tr>
    <td>[Prosody](#prosody_element)</td>
    <td style="text-align:center">Parcial</td>
    <td style="padding-left:100px">[vxml:currency](#vxml-currency)</td>
    <td style="text-align:center">Parcial</td>
  </tr>
  <tr>
    <td style="padding-left:25px">contour</td>
    <td style="text-align:center">Ninguno</td>
    <td style="padding-left:100px">[vxml:date](#vxml-date)</td>
    <td style="text-align:center">Parcial</td>
  </tr>
  <tr>
    <td style="padding-left:25px">duration</td>
    <td style="text-align:center">Ninguno</td>
    <td style="padding-left:100px">[vxml:digits](#vxml-digits)</td>
    <td style="text-align:center">Parcial</td>
  </tr>
  <tr>
    <td style="padding-left:25px">[pitch](#prosody-pitch)</td>
    <td style="text-align:center">Completo</td>
    <td style="padding-left:100px">[vxml:phone](#vxml-phone)</td>
    <td style="text-align:center">Parcial</td>
  </tr>
  <tr>
    <td style="padding-left:25px">range</td>
    <td style="text-align:center">Ninguno</td>
    <td style="padding-left:75px">[Sentence](#ps_element)</td>
    <td style="text-align:center">Completo</td>
  </tr>
  <tr>
    <td style="padding-left:25px">[rate](#prosody-rate)</td>
    <td style="text-align:center">Completo</td>
    <td style="padding-left:75px">[Speak](#speak_element)</td>
    <td style="text-align:center">Completo</td>
  </tr>
  <tr>
    <td style="padding-left:25px">[volume](#prosody-volume)</td>
    <td style="text-align:center">Parcial</td>
    <td style="padding-left:75px">[Sub](#sub_element)</td>
    <td style="text-align:center">Completo</td>
  </tr>
  <tr>
    <td></td>
    <td></td>
    <td style="padding-left:75px">[Voice](#voice_element)</td>
    <td style="text-align:center">Ninguno</td>
  </tr>
</table>

## Elemento audio
{: #audio_element}

El elemento `<audio>` inserta elementos grabados en el audio generado por el servicio. No está soportado.

## Elemento break
{: #break_element}

El elemento `<break>` inserta una pausa en el texto hablado. Tiene los atributos opcionales siguientes:

-   `strength` especifica la longitud de la pausa en términos de valores de intensidad variables:
    -   `none` suprime una pausa que si no se produciría durante el proceso.
    -   `x-weak`, `weak`, `medium`, `strong` o `x-strong` insertan pausas cada vez más largas.
-   `time` especifica la longitud de la pausa en términos de segundos o milisegundos. Los valores válidos son `{integer}s` para segundos o `{integer}ms` para milisegundos.

```xml
<speak version="1.0">
  Different sized <break strength="none">no pause</break>
  Different sized <break strength="x-weak">x-weak pause</break>
  Different sized <break strength="weak">weak pause</break>
  Different sized <break strength="medium">medium pause</break>
  Different sized <break strength="strong">strong pause</break>
  Different sized <break strength="x-strong">x-strong pause</break>
  Different sized <break time="1s">one-second pause</break>
  Different sized <break time="1500ms">1500-millisecond pause</break>
</speak>
```
{: codeblock}

## Elemento desc
{: #desc_element}

El elemento `<desc>` solo puede aparecer dentro de un elemento `<audio>`. Dado que el elemento `<audio>`n o está soportado, el elemento `<desc>` tampoco lo está.

## Elemento emphasis
{: #emphasis_element}

El elemento `<emphasis>` solicita que el texto indicado se diga con énfasis. No está soportado.

## Elemento lexicon
{: #lexicon_element}

El elemento `<lexicon>` introduce diccionarios de pronunciación para el documento SSML indicado. No está soportado.

Puede utilizar la interfaz de personalización del servicio para definir un diccionario de entradas personalizadas (pares de palabra/conversión) para su uso durante la síntesis de voz. Para obtener más información, consulte [Comprender la personalización](/docs/services/text-to-speech?topic=text-to-speech-customIntro).

## Elemento mark
{: #mark_element}

El elemento `<mark>` solo está soportado en la interfaz WebSocket del servicio, no en la interfaz HTTP, que lo ignora. Para obtener más información, consulte [Especificar un elemento SSML mark](/docs/services/text-to-speech?topic=text-to-speech-timing#mark).
{: note}

El elemento `<mark>` es un elemento vacío que coloca una marca en el texto que se va a sintetizar. Se notifica al cliente cuando todo el texto que precede al elemento `<mark>` se ha sintetizado. El elemento acepta solo un atributo `name` que especifica una serie que identifica de forma exclusiva la marca; el nombre debe empezar por un carácter alfanumérico. El nombre se devuelve junto con el tiempo en que aparece la marca en el audio sintetizado.

```xml
<speak version="1.0">
  Hello <mark name="here"/> world.
</speak>
```
{: codeblock}

## Elementos meta y metadata
{: #mm_element}

Los elementos `<meta>` y `<metadata>` son contenedores en los que puede poner información sobre el documento. No están soportados.

## Elementos paragraph y sentence
{: #ps_element}

Los elementos `<paragraph>` (o `<p>`) y `<sentence>` (o `<s>`) son elementos opcionales que se pueden utilizar para dar indicaciones sobre la estructura del texto. Si el texto que se incluye dentro de un elemento `<paragraph>` o un elemento `<sentence>` no termina con un carácter de puntuación de fin de oración (como un punto), el servicio añade una pausa más larga de lo normal al audio sintetizado.

El único atributo válido para cualquiera de estos dos elementos es `xml:lang`, que permite cambiar de idioma. Este atributo no está soportado.

```xml
<speak version="1.0">
  <paragraph>
    <sentence>Text within a sentence element.</sentence>
    <s>More text in another sentence.</s>
  </paragraph>
</speak>
```
{: codeblock}

## Elemento phoneme
{: #phoneme_element}

El elemento `<phoneme>` proporciona una pronunciación fonética para el texto que contiene. La escritura fonética representa los sonidos de una palabra, cómo los sonidos se dividen en sílabas y qué sílabas reciben acento. El elemento tiene dos atributos:

-   `alphabet` es un atributo opcional que especifica la fonología a utilizar. Los alfabetos soportados son
    -   El alfabeto fonético internacional estándar (IPA - International Phonetic Alphabet): `alphabet="ipa"`
    -   El alfabeto {{site.data.keyword.IBM_notm}} SPR (Symbolic Phonetic Representation): `alphabet="ibm"`

    Si no se especifica ningún alfabeto, el servicio utiliza el SPR de IBM de forma predeterminada.
-   `ph` es un atributo obligatorio que proporcionar la pronunciación en el alfabeto indicado. En los ejemplos siguientes se muestra la pronunciación de la palabra *tomato* en los dos formatos:

    -   Formato IPA:

        <pre><code>&lt;speak version="1.0"&gt;
          &lt;phoneme alphabet="ipa" ph="t&#601;&#712;me&#618;.&#638;o&#650;"&gt;tomato&lt;/phoneme&gt;
        &lt;/speak&gt;</code></pre>

    -   Formato IPA con símbolos Unicode:

        <pre><code>&lt;speak version="1.0"&gt;
          &lt;phoneme alphabet="ipa" ph="t&amp;&#35;x259;mei&amp;&#35;x027E;o&amp;&#035;x028A;"&gt;tomato&lt;/phoneme&gt;
        &lt;/speak&gt;</code></pre>

    -   Formato IBM SPR:

        <pre><code>&lt;speak version="1.0"&gt;
          &lt;phoneme alphabet="ibm" ph=".0tx.1me.0Fo"&gt;tomato&lt;/phoneme&gt;
        &lt;/speak&gt;</code></pre>

Para obtener más información sobre cómo utilizar las notaciones SPR e IPA con el elemento `<phoneme>`, consulte [Utilización de IBM SPR](/docs/services/text-to-speech?topic=text-to-speech-sprs).

## Elemento prosody
{: #prosody_element}

El elemento `<prosody>` controla el tono, la velocidad del habla y el volumen del texto. Todos los atributos son opcionales, pero se produce un error si no se especifica ninguno. La especificación SSML permite tres atributos que el servicio no admite: `contour`, `range` y `duration`. El servicio admite los atributos `pitch`, `rate` y `volume`.

### Atributo pitch
{: #prosody-pitch}

El atributo `pitch` modifica el tono base del texto que hay dentro del elemento. Los valores aceptados son

-   Un número seguido de la designación `Hz` (Hertz): El tono base se transpone (hacia arriba o hacia abajo) al valor especificado.
-   Un valor de cambio relativo (en semitonos): Un número que causa un cambio absoluto de la línea base actual. El número va precedido de un signo `+` (aumento) o `-` (reducción) y seguido de `st` (semitonos), por ejemplo, `+5st`.
-   Un cambio relativo en porcentaje: un número que causa un cambio relativo de la línea base actual. El número va precedido de un signo `+` (aumento) o `-` (reducción) y seguido de `%` (signo de porcentaje), por ejemplo, `-10%`.
-   Una de las siguientes palabras, que modifica el tono a los valores predefinidos correspondientes:
    -   `default` utiliza el tono base predeterminado del servicio.
    -   `x-low` baja la línea base del tono en 12 semitonos.
    -   `low` baja la línea base del tono en seis semitonos.
    -   `medium` produce el mismo comportamiento que `default`.
    -   `high` sube la línea base del tono en seis semitonos.
    -   `x-high` sube la línea base del tono en 12 semitonos.

    ```xml
    <speak version="1.0">
      <prosody pitch="150Hz">Transpose pitch to 150 Hz</prosody>
      <prosody pitch="-20Hz">Lower pitch by 20 Hz from baseline</prosody>
      <prosody pitch="+20Hz">Increase pitch by 20 Hz from baseline</prosody>
      <prosody pitch="-12st">Lower pitch by 12 semitones from baseline</prosody>
      <prosody pitch="+12st">Increase pitch by 12 semitones from baseline</prosody>
      <prosody pitch="x-low">Lower pitch by 12 semitones from baseline</prosody>
    </speak>
    ```
    {: codeblock}

### Atributo rate
{: #prosody-rate}

El atributo `rate` indica un cambio en la velocidad de habla para el texto de dentro del elemento. La velocidad rate se especifica en palabras por minuto; si la velocidad de habla es de 50 palabras por minuto, `rate` es igual a `50`. Cuando se establece `rate` en un número positivo, la implementación no cumple con la especificación de atributo de velocidad de prosodia W3C actual. Además, el servicio admite cambios porcentuales relativos (por ejemplo, `+15%`) pero no cambios de valor relativos (por ejemplo, `+15`). Los valores aceptados son

-   Un aumento o una reducción porcentual relativa: `+10%`.
-   Un número de palabras por minuto en forma de número positivo: `75`.
-   `default` utiliza la velocidad predeterminada del servicio.
-   `x-slow` disminuye la velocidad en un 50 por ciento.
-   `slow` disminuye la velocidad en un 25 por ciento.
-   `medium` produce el mismo comportamiento que `default`.
-   `fast` aumenta la velocidad en un 25 por ciento.
-   `x-fast` aumenta la velocidad en un 50 por ciento.

```xml
<speak version="1.0">
  <prosody rate="slow">Decrease speaking rate by 25%</prosody>
  <prosody rate="50">Set speaking rate at 50 words per minute</prosody>
  <prosody rate="+5%">Increase speaking rate by 5 percent</prosody>
</speak>
```
{: codeblock}

### Atributo volume
{: #prosody-volume}

El servicio no admite el atributo `volume` del elemento `<prosody>` en sus voces neuronales (por ejemplo, `en-US_AllisonV3Voice`). Para obtener más información, consulte [Voces neuronales](/docs/services/text-to-speech?topic=text-to-speech-voices#neuralVoices).
{: note}

El atributo `volume` modifica el volumen del texto que hay dentro del elemento. Puede especificar un valor entero o decimal dentro del rango de 1,0 a 100,0 (volumen máximo). También puede utilizar uno de los valores de serie siguientes, que corresponden a valores predefinidos dentro del rango de 0 a 100. (El valor `silent` no está soportado).

-   `x-soft` tiene el valor 30.
-   `soft` tiene el valor 50.
-   `medium` tiene el valor 80.
-   `loud` tiene el valor 90.
-   `default` tiene el valor 92.
-   `x-loud` tiene el valor 100.

```xml
<speak version="1.0">
  <prosody volume="75">Modified volume is 75</prosody>
  <prosody volume="88.9">Modified volume is 88.9</prosody>
  <prosody volume="loud">Modified volume is 90</prosody>
</speak>
```
{: codeblock}

## Elemento say-as
{: #say-as_element}

El elemento `<say-as>` sólo está soportado parcialmente para la mayoría de idiomas. Para idiomas distintos del inglés de Estados Unidos, el servicio generalmente solo admite los atributos `digits` y `letters` del elemento.
{: note}

El elemento `<say-as>` proporciona información sobre el tipo de texto que contiene el elemento y especifica el nivel de detalle para expresar el texto. El elemento tiene un atributo obligatorio, `interpret-as`, que indica cómo se debe interpretar el texto. Tiene dos atributos opcionales, `format` y `detail`, que se utilizan sólo con valores particulares dentro del atributo `interpret-as`, como se ilustra en los ejemplos siguientes.

A continuación se muestran los valores aceptables del atributo `interpret-as` y ejemplos de cada uno.

### cardinal
{: #sayAsCardinal}

El valor `cardinal` indica que hay que expresar el número cardinal del numeral que contiene el elemento. Los ejemplos siguientes se leen *Super Bowl forty-nine*. El primero es superfluo, puesto que no modifica el comportamiento predeterminado del servicio.

```xml
<speak version="1.0">
  Super Bowl <say-as interpret-as="cardinal">49</say-as>
  Super Bowl <say-as interpret-as="cardinal">XLIX</say-as>
</speak>
```
{: codeblock}

### date
{: #sayAsDate}

El valor `date` lee la fecha del elemento de acuerdo con el formato indicado en el atributo `format` asociado. El atributo `format` es obligatorio para el valor `date`. Si `format` no está, el servicio igualmente intenta pronunciar la fecha. En los siguientes ejemplos se leen las fechas indicadas en los formatos especificados, donde `d`, `m` e `y` representan día, mes y año.

```xml
<speak version="1.0">
  <say-as interpret-as="date" format="mdy">12/17/2005</say-as>
  <say-as interpret-as="date" format="ymd">2005/12/17</say-as>
  <say-as interpret-as="date" format="dmy">17/12/2005</say-as>
  <say-as interpret-as="date" format="ydm">2005/17/12</say-as>
  <say-as interpret-as="date" format="my">12/2005</say-as>
  <say-as interpret-as="date" format="md">12/17</say-as>
  <say-as interpret-as="date" format="ym">2005/12</say-as>
</speak>
```
{: codeblock}

### digits
{: #sayAsDigits}

El valor `digits` lee los dígitos del número que hay en el elemento. En el ejemplo siguiente se pronuncian los dígitos individuales *123456*.

```xml
<speak version="1.0">
  <say-as interpret-as="digits">123456</say-as>
</speak>
```
{: codeblock}

### letters
{: #sayAsLetters}

El valor `letters` deletrea los caracteres de la palabra dentro del elemento. En el ejemplo siguiente se deletrean las letras de la palabra *hello*.

```xml
<speak version="1.0">
  <say-as interpret-as="letters">Hello</say-as>
</speak>
```
{: codeblock}

### number
{: #sayAsNumber}

El valor `number` ofrece una alternativa a los valores `cardinal` y `ordinal`. Puede utilizar el atributo opcional `format` para indicar cómo se debe interpretar una serie de números. En el primer ejemplo se omite el atributo `format` para pronunciar el número como un valor cardinal. En el segundo ejemplo se especifica explícitamente que el número se tiene que pronunciar como un valor `cardinal`. En el tercer ejemplo se especifica que el número se debe pronunciar como un valor `ordinal`.

```xml
<speak version="1.0">
  <say-as interpret-as="number">123456</say-as>
  <say-as interpret-as="number" format="cardinal">123456</say-as>
  <say-as interpret-as="number" format="ordinal">123456</say-as>
</speak>
```
{: codeblock}

También puede especificar el valor `telephone` para el atributo `format`. Los ejemplos siguientes muestran dos maneras distintas de pronunciar una serie de números como un número de teléfono. Para pronunciar los números incluyendo la puntuación, especifique el valor `punctuation` en el atributo opcional `detail`.

```xml
<speak version="1.0">
  <say-as interpret-as="number" format="telephone">555-555-5555</say-as>
  <say-as interpret-as="number" format="telephone" detail="punctuation">555-555-5555</say-as>
</speak>
```
{: codeblock}

### ordinal
{: #sayAsOrdinal}

El valor `ordinal` lee el valor ordinal del dígito de dentro del elemento. En el ejemplo siguiente se pronuncia *second first*.

```xml
<speak version="1.0">
  <say-as interpret-as="ordinal">2</say-as>
  <say-as interpret-as="ordinal">1</say-as>
</speak>
```
{: codeblock}

### vxml:boolean
{: #vxml-boolean}

El valor `vxml:boolean` lee *yes* o *no* si el valor es `true` o `false` en el elemento.

```xml
<speak version="1.0">
  <say-as interpret-as="vxml:boolean">true</say-as>
  <say-as interpret-as="vxml:boolean">false</say-as>
</speak>
```
{: codeblock}

### vxml:currency
{: #vxml-currency}

El valor `vxml:currency` se utiliza para controlar la síntesis de los valores monetarios. La serie debe estar escrita en el formato `UUUmm.nn`, donde `UUU` es el indicador de moneda de tres caracteres que se especifica en el estándar ISO 4217 y `mm.nn` es la cantidad. En el ejemplo siguiente se lee *forty-five dollars and thirty cents*.

```xml
<speak version="1.0">
  <say-as interpret-as="vxml:currency">USD45.30</say-as>
</speak>
```
{: codeblock}

Si el número especificado incluye más de dos decimales, la cantidad se sintetiza como un número decimal seguido del indicador de moneda. Si el indicador de moneda de tres caracteres no está, la cantidad se sintetiza simplemente como un número decimal y no se pronuncia el tipo de moneda. En el ejemplo siguiente se lee *forty-five point three two nine US dollars*.

```xml
<speak version="1.0">
  <say-as interpret-as="vxml:currency">USD45.329</say-as>
</speak>
```
{: codeblock}

### vxml:date
{: #vxml-date}

El valor `vxml:date` funciona como el valor `date`, pero el formato está predefinido como `YYYYMMDD`. Si no se conoce un valor de día, mes o año, o si no desea que se diga, sustituya el valor por un `?` (signo de interrogación). En el segundo y tercer ejemplo aparecen signos de interrogación.

```xml
<speak version="1.0">
  <say-as interpret-as="vxml:date">20050720</say-as>
  <say-as interpret-as="vxml:date">????0720</say-as>
  <say-as interpret-as="vxml:date">200507??</say-as>
</speak>
```
{: codeblock}

### vxml:digits
{: #vxml-digits}

El valor `vxml:digits` proporciona la misma función que el valor `digits`.

### vxml:phone
{: #vxml-phone}

El valor `vxml:phone` lee un número de teléfono que contiene dígitos y signos de puntuación. Es equivalente a utilizar el valor `number` y especificar `telephone` en el atributo `format` y `punctuation` en el atributo `detail`.

```xml
<speak version="1.0">
  <say-as interpret-as="vxml:phone">555-555-5555</say-as>
</speak>
```
{: codeblock}

## Elemento speak
{: #speak_element}

El elemento `<speak>` es el elemento raíz de los documentos SSML. Los atributos válidos son

-   `version` es un atributo obligatorio que indica la especificación SSML. El valor aceptado es `1.0`.
-   `xml:lang` no es obligatorio para el servicio. Omita este atributo cuando utilice este elemento.
-   `xml:base` no tiene ningún efecto.

```xml
<speak version="1.0">
  The text to be spoken.
</speak>
```
{: codeblock}

## Elemento sub
{: #sub_element}

El elemento `<sub>` indica que el texto que se especifica en el atributo `alias` debe sustituir al texto de dentro del elemento al sintetizar el habla. El atributo `alias` es el único atributo de este elemento y es obligatorio.

```xml
<speak version="1.0">
  <sub alias="International Business Machines">IBM</sub>
</speak>
```
{: codeblock}

## Elemento voice
{: #voice_element}

El elemento `<voice>` solicita un cambio de voz. No está soportado.
