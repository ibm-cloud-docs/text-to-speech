---

copyright:
  years: 2015, 2019
lastupdated: "2019-03-21"

subcollection: text-to-speech

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

# La interfaz HTTP
{: #usingHTTP}

Para sintetizar texto a voz con la interfaz HTTP REST del servicio {{site.data.keyword.texttospeechfull}}, debe llamar al método `GET` o `POST /v1/synthesize`. Debe especificar el texto a sintetizar y la voz y el formato para el audio hablado. También puede especificar un modelo de voz personalizado a utilizar con la solicitud.
{: shortdesc}

Para obtener más información sobre la interfaz de HTTP, consulte la [Referencia de API ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://{DomainName}/apidocs/text-to-speech){: new_window}.

## Sintetizar texto a audio
{: #synthesize}

Para sintetizar texto a audio, debe efectuar una llamada a una de las dos versiones del método `/v1/synthesize` del servicio:

-   El método `GET /v1/synthesize` acepta el texto a sintetizar como un parámetro de consulta obligatorio `text`. El tamaño máximo de la solicitud es de 8 KB, incluyendo el texto de entrada, cualquier SSML que especifique y el URL y las cabeceras.
-   El método `POST /v1/synthesize` acepta el texto a sintetizar como un constructo JSON en el cuerpo obligatorio de la solicitud. El tamaño máximo de la solicitud es de 8 KB para el URL y las cabeceras y de 5 KB para el texto de entrada que se envía dentro del cuerpo de la solicitud. El límite de 5 KB incluye cualquier SSML que especifique.

Las dos versiones del método `/v1/synthesize` tienen los siguientes parámetros en común:

<table>
  <caption>Tabla 1. Parámetros de los métodos <code>/v1/synthesize</code></caption>
  <tr>
    <th style="text-align:left; width:18%">Parámetro</th>
    <th style="text-align:center; width:12%">Tipo</th>
    <th style="text-align:center; width:12%">Tipo de datos</th>
    <th style="text-align:left">Descripción</th>
  </tr>
  <tr>
    <td><code>accept</code><br/><em>Opcional</em></td>
    <td style="text-align:center">Consulta</td>
    <td style="text-align:center">Serie</td>
    <td>
      Especifica el formato de audio solicitado, o el tipo MIME, en el que.
      el servicio debe devolver el audio. También puede especificar este valor
      con la cabecera de solicitud HTTP <code>Accept</code>. Codifique como URL el argumento
      en el parámetro de consulta `accept`. Para obtener más información,
      consulte [Formatos de audio](/docs/services/text-to-speech/audio-formats.html).
    </td>
  </tr>
  <tr>
    <td><code>voice</code><br/><em>Opcional</em></td>
    <td style="text-align:center">Consulta</td>
    <td style="text-align:center">Serie</td>
    <td>
      Especifica la voz en que se debe leer el texto en el
      audio. Utilice el método <code>/v1/voices</code> para obtener
      la lista actual de voces soportadas. La voz predeterminada es
      <code>en-US_MichaelVoice</code>. Para obtener más información, consulte
      [Idiomas y voces](/docs/services/text-to-speech/voices.html).
    </td>
  </tr>
  <tr>
    <td><code>customization_id</code><br/><em>Opcional</em></td>
    <td style="text-align:center">Consulta</td>
    <td style="text-align:center">Serie</td>
    <td>
      Especifica un identificador exclusivo global (GUID) de un modelo de voz
      personalizado a utilizar para la síntesis. Sólo se garantiza que un modelo
      de voz personalizado especificado funcionará si coincide con el idioma de
      la voz que se utiliza para la síntesis. Si incluye un ID de personalización,
      debe llamar al método con las credenciales de servicio del propietario del
      modelo. Omita el parámetro para utilizar la voz especificada sin
      personalización. Para obtener más información, consulte
      [Comprender la personalización](/docs/services/text-to-speech/custom-intro.html).
    </td>
  </tr>
</table>

También puede utilizar las siguientes cabeceras de solicitud, que están disponibles para todos los servicios de {{site.data.keyword.watson}}, con una solicitud de síntesis:

-   `X-Watson-Learning-Opt-Out` indica si el servicio registra datos de solicitud y respuesta para mejorar el servicio para los usuarios futuros. Para evitar que IBM acceda a sus datos para mejoras de servicio generales, especifique <code>true</code> en el parámetro. Para obtener más información, consulte [Control del registro de solicitud para servicios de {{site.data.keyword.watson}}](/docs/services/watson/getting-started-logging.html).
-   `X-Watson-Metadata` asocia un ID de cliente a los datos que se pasan en una solicitud. Para obtener más información, consulte [Seguridad de la información](/docs/services/text-to-speech/information-security.html).

Si especifica un parámetro de consulta no válido o un campo JSON como parte de la entrada en el método `/v1/synthesize`, el servicio devuelve una cabecera de respuesta `Warnings` que describe y lista cada argumento no válido. La solicitud tiene éxito a pesar de las advertencias.
{: note}

## Especificar texto de entrada
{: #input}

Tanto el método `GET` como el método `POST /v1/synthesize` aceptan texto de entrada sin formato o bien texto anotado con SSML. Las dos versiones difieren principalmente en el modo en que se especifica el texto a sintetizar:

-   El método `GET /v1/synthesize` acepta el texto de entrada que se especifica mediante el parámetro de consulta `text`. La entrada se debe especificar como texto sin formato o como SSML, pero en ambos casos deben estar codificada como URL.
-   El método `POST /v1/synthesize` acepta texto de entrada en el cuerpo de la solicitud. La entrada se debe especificar con la siguiente construcción JSON simple que encapsula texto sin formato o texto SSML. También hay que especificar el valor `application/json` para la cabecera `Content-Type`.

    ```javascript
    {
      "text": ""
    }
    ```
    {: codeblock}

Aunque los métodos `GET` y `POST` ofrecen una funcionalidad equivalente, siempre es más seguro pasar texto de entrada al servicio con el método `POST`. Una solicitud `POST` pasa la entrada en el cuerpo de la solicitud, mientras que una solicitud `GET` expone los datos en el URL.

## Especificar entrada SSML
{: #ssml-http}

SSML (Speech Synthesis Markup Language) es un lenguaje de códigos basado en XML, diseñado para proporcionar anotaciones de texto para aplicaciones de síntesis de voz, como por ejemplo el servicio {{site.data.keyword.texttospeechshort}}. Puede utilizar los elementos SSML y sus atributos para obtener un mayor control sobre la síntesis y sobre la salida de audio resultante.

Para obtener más información sobre el uso de SSML para anotar el texto de entrada, consulte [Utilización de SSML](/docs/services/text-to-speech/SSML.html). En la documentación se inventarían los elementos y atributos SSML que admite el servicio. También se documentan las extensiones de expresión y de conversión de voz del servicio.

## Escapar los caracteres de control XML
{: #escape}

Puesto que puede enviar texto de entrada que incluye anotaciones SSML basadas en XML, el servicio valida toda la entrada para asegurarse de que el SSML es correcto y bien formado. Por lo tanto, debe escapar cualquier carácter de control XML que esté presente en el texto de entrada, independientemente de si la entrada incluye SSML. Utilice las series de escape o las codificaciones de caracteres equivalentes de la Tabla 2 en lugar de los caracteres indicados.

<table style="width:80%">
  <caption>Tabla 2. Escapar los caracteres de control XML</caption>
  <tr>
    <th style="text-align:center; vertical-align:bottom; width:40%">Carácter</th>
    <th style="text-align:center; vertical-align:bottom; width:30%">Series de escape</th>
    <th style="text-align:center; vertical-align:bottom; width:30%">Codificación de caracteres</th>
  </tr>
  <tr>
    <td style="text-align:center"><code>&quot;</code><br/>(comillas dobles)</td>
    <td style="text-align:center"><code>&amp;quot;</code></td>
    <td style="text-align:center"><code>&amp;#34;</code></td>
  </tr>
  <tr>
    <td style="text-align:center"><code>'</code><br/>(apóstrofo o comilla simple)</td>
    <td style="text-align:center"><code>&amp;apos;</code></td>
    <td style="text-align:center"><code>&amp;#39;</code></td>
  </tr>
  <tr>
    <td style="text-align:center"><code>&amp;</code><br/>(ampersand)</td>
    <td style="text-align:center"><code>&amp;amp;</code></td>
    <td style="text-align:center"><code>&amp;#38;</code></td>
  </tr>
  <tr>
    <td style="text-align:center"><code>&lt;</code><br/>(corchete angular izquierdo)</td>
    <td style="text-align:center"><code>&amp;lt;</code></td>
    <td style="text-align:center"><code>&amp;#60;</code></td>
  </tr>
  <tr>
    <td style="text-align:center"><code>&gt;</code><br/>(corchete angular derecho)</td>
    <td style="text-align:center"><code>&amp;gt;</code></td>
    <td style="text-align:center"><code>&amp;#62;</code></td>
  </tr>
</table>

Para obtener más información sobre cómo el servicio valida el texto de entrada, consulte [Validación de SSML](/docs/services/text-to-speech/SSML.html#errors).

## Ejemplos de texto de entrada
{: #httpExamples}

En los ejemplos siguientes se muestra cómo especificar texto de entrada con cualquiera de los métodos de la interfaz HTTP. También muestran cómo escapar los caracteres de control XML. En los ejemplos se incluyen saltos de línea para mejorar la legibilidad. *No* incluya los saltos de línea en la entrada real.

### Ejemplo de entrada con una solicitud GET
{: #getExamples}

En los ejemplos siguientes se pasa una entrada codificada en URL con el parámetro de consulta `text` del método `GET /v1/synthesize`:

-   Entrada en texto sin formato:

    ```
    text=This&20is&20the&20first&20sentence&20of&20the&20paragraph.&20Here
    &20is&20another&20sentence.&20Finally,&20this&20is&20the&20last&20sentence.
    ```
    {: codeblock}

-   Entrada en SSML:

    ```
    text=%22%3Cp%3E%3Cs%3EThis%20is%20the%20first%20sentence%20of%20the%20%3C
    break%20time=%225s%22/%3E%20paragraph.%3C/s%3E%3Cs%3EHere%20is%20another
    %20sentence.%3C/s%3E%3Cs%3EFinally,%20this%20is%20the%20last%20sentence.
    %3C/s%3E%3C/p%3E%22
    ```
    {: codeblock}

### Ejemplo de entrada con una solicitud POST
{: #postExamples}

En los ejemplos siguientes se pasa la entrada en el cuerpo del método `POST /v1/synthesize`:

-   Entrada en texto sin formato:

    ```javascript
    {
      "text": "This is the first sentence of the paragraph. Here is another
        sentence. Finally, this is the last sentence."
    }
    ```
    {: codeblock}

-   Entrada en SSML:

    ```javascript
    {
      "text": "<p><s>This is the first sentence of the <break time=\"5s\"/>
        paragraph.</s><s>Here is another sentence.</s><s>Finally, this is
        the last sentence.</s></p>"
    }
    ```
    {: codeblock}

### Ejemplo de entrada con caracteres de control XML
{: #xmlExamples}

En los ejemplos siguientes se envían dos frases al método `POST /v1/synthesize`. En los ejemplos se escapan adecuadamente los caracteres XML incluidos.

```
"What have I learned?" he asked. "Everything!"
```
{: codeblock}

-   Entrada en texto sin formato:

    ```javascript
    {
      "text": "&quot;What have I learned?&quot; he asked. &quot;Everything!&quot;"
    }
    ```
    {: codeblock}

-   Entrada en SSML:

    ```javascript
    {
      "text": "<s>&quot;What have I learned?&quot; he asked.
        &quot;<express-as type=\"GoodNews\">Everything!</express-as>&quot;</s>"
    }
    ```
    {: codeblock}
