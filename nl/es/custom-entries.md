---

copyright:
  years: 2015, 2019
lastupdated: "2019-06-24"

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

# Creación y gestión de entradas personalizadas
{: #customWords}

Una vez que existe un modelo personalizado, el siguiente paso es añadir entradas personalizadas en forma de pares palabra/conversión para definir cómo se deben pronunciar algunas palabras específicas durante la síntesis. Las definiciones sobrescriben las reglas de pronunciación regular predeterminadas del servicio. Se pueden añadir y consultar conversiones para una o más palabras de una vez, y se pueden suprimir palabras individuales que ya no se necesiten. Una vez que esté familiarizado con la interfaz de personalización, puede ser más conveniente manipular varias palabras a la vez que trabajar palabra por palabra. Debe utilizar las credenciales para la instancia del servicio que es propietaria de un modelo personalizado para utilizar cualquier método que requiera su ID de personalización.
{: shortdesc}

## Añadir una palabra a un modelo personalizado
{: #cuWordAdd}

Para añadir un par de palabra/conversión a un modelo personalizado, utilice el método `PUT /v1/customizations/{customization_id}/words/{word}`. La palabra a añadir se debe especificar en el URL del método. Para indicar la conversión para la palabra pasa un objeto JSON con un atributo `translation`. Si se añade una nueva conversión para una palabra que ya existe en un modelo, se sobrescribe la conversión existente de la palabra.

Para indicar una conversión, se puede utilizar el método 'suena como' o el método fonético (o una combinación de los dos). Para las transcripciones fonéticas se puede utilizar el formato IPA (International Phonetic Alphabet) o el formato {{site.data.keyword.IBM_notm}} SPR (Symbolic Phonetic Representation). En los ejemplos siguientes se utilizan distintos métodos para añadir conversiones equivalentes para la palabra `IEEE` en un modelo personalizado.

-   **Suena como:** Para este ejemplo, el método de tipo 'suena como' es el más simple:

    ```bash
    curl -X PUT -u "apikey:{apikey}"
    --header "Content-Type: application/json"
    --data "{\"translation\":\"I triple E\"}"
    "https://stream.watsonplatform.net/text-to-speech/api/v1/customizations/{customization_id}/words/IEEE"
    ```
    {: pre}

-   **IPA fonético:** IPA requiere el uso del elemento `<phoneme>` con el atributo `alphabet` establecido en `ipa` y el atributo `ph` definido en formato IPA:

    <pre><code class="language-bash">  curl -X PUT -u "apikey:{apikey}"
    --header "Content-Type: application/json"
    --data "{\"translation\":\"&lt;phoneme alphabet=\\\"ipa\\\" ph=\\\"&#712;a&#618;.t&#633;&#712;&#616;p&#601;l.&#712;i\\\"&gt;&lt;/phoneme&gt;\"}"
    "https://stream.watsonplatform.net/text-to-speech/api/v1/customizations/{customization_id}/words/IEEE"</code></pre>

-   **{{site.data.keyword.IBM_notm}} SPR fonético:** SPR utiliza el elemento `<phoneme>` con el atributo `alphabet` establecido en `ibm` y el atributo `ph` definido en formato SPR:

    ```bash
    curl -X PUT -u "apikey:{apikey}"
    --header "Content-Type: application/json"
    --data "{\"translation\":\"<phoneme alphabet=\\\"ibm\\\" ph=\\\"1Y.tr1Ipxl.1i\\\"></phoneme>\"}"
    "https://stream.watsonplatform.net/text-to-speech/api/v1/customizations/{customization_id}/words/IEEE"
    ```
    {: pre}

## Añadir varias palabras a un modelo personalizado
{: #cuWordsAdd}

Para añadir una o más palabras a un modelo personalizado de una vez, utilice el método `POST /v1/customizations/{customization_id}/words`. Debe especificar las entradas a añadir al modelo personalizado como una matriz de JSON de pares palabra/conversión. En el ejemplo siguiente se añaden conversiones comunes de tipo 'suena como' para las palabras `NCAA` e `iPhone` a un modelo personalizado:

```bash
curl -X POST -u "apikey:{apikey}"
--header "Content-Type: application/json"
--data "{\"words\": [{\"word\":\"NCAA\", \"translation\":\"N C double A\"}, {\"word\":\"iPhone\", \"translation\":\"I phone\"}]}"
"https://stream.watsonplatform.net/text-to-speech/api/v1/customizations/{customization_id}/words"
```
{: pre}

El contenido JSON enviado en el cuerpo de la solicitud equivale a lo siguiente:

```javascript
{
  "words": [
    {"word":"NCAA", "translation":"N C double A"},
    {"word":"iPhone", "translation":"I phone"}
  ]
}
```
{: codeblock}

Tal como se menciona en [Actualizar un modelo personalizado](/docs/services/text-to-speech?topic=text-to-speech-customModels#cuModelsUpdate), también se puede utilizar el método `POST /v1/customizations/{customization_id}` para añadir palabras a un modelo personalizado. En el ejemplo siguiente se utiliza este método para añadir las mismas dos palabras que en el ejemplo anterior; no se hacen cambios en los metadatos del modelo. Excepción en el URL, los dos métodos son idénticos.

```bash
curl -X POST -u "apikey:{apikey}"
--header "Content-Type: application/json"
--data "{\"words\": [{\"word\":\"NCAA\", \"translation\":\"N C double A\"}, {\"word\":\"iPhone\", \"translation\":\"I phone\"}]}"
"https://stream.watsonplatform.net/text-to-speech/api/v1/customizations/{customization_id}"
```
{: pre}

## Añadir palabras a un modelo personalizado en japonés
{: #cuJapaneseAdd}

Se aplican consideraciones adicionales y también un campo adicional, `part_of_speech` (categoría léxica), al crear entradas de palabras en un modelo personalizado en japonés; para obtener más información, consulte [Trabajar con entradas en japonés](/docs/services/text-to-speech?topic=text-to-speech-rules#jaNotes). Para especificar una categoría léxica para una entrada personalizada en japonés, haga lo siguiente:

-   Para el método `PUT /v1/customizations/{customization_id}/words/{word}`, pase un objeto JSON con el formato siguiente:

    ```javascript
    {
      "translation": "value",
      "part_of_speech": "value"
    }
    ```
    {: codeblock}

-   Para los métodos `POST /v1/customizations/{customization_id}/words` y `POST customizations/{customization_id}`, pase un objeto JSON como el siguiente:

    ```javascript
    {
      "words": [
        {
          "word": "value",
          "translation": "value",
          "part_of_speech": "value"
        }
        . . .
      ]
    }
    ```
    {: codeblock}

En los siguientes ejemplos del método `PUT /v1/customizations/{customization_id}/words/{word}` se convierte la serie de doble byte codificada como URL para `NY` al nombre (`Mesi`) <code>&#12491;&#12517;&#12540;&#12520;&#12540;&#12463;</code> (`New York` en inglés). Si no se define esta conversión, la serie de caracteres se lee como `enu wai`.

-   **Suena como:**

    <pre><code>curl -X PUT -u "apikey:{apikey}"
    --header "Content-Type: application/json"
    --data "{\"translation\":\"&#12491;&#12517;&#12540;&#12520;&#12540;&#12463;\", \"part_of_speech\":\"Mesi\"}"
    "https://stream.watsonplatform.net/text-to-speech/api/v1/customizations/{customization_id}/words/%EF%BC%AE%EF%BC%B9"</code></pre>

-   **IPA fonético:**

    <pre><code>curl -X PUT -u "apikey:{apikey}"
    --header "Content-Type: application/json"
    --data "{\"translation\":\"&lt;phoneme alphabet=\\\"ipa\\\" ph=\\\"&#626;&#623;&#720;&#106;&#111;&#720;&#107;&#623;\\\"&gt;&lt;/phoneme&gt;\", \"part_of_speech\":\"Mesi\"}"
    "https://stream.watsonplatform.net/text-to-speech/api/v1/customizations/{customization_id}/words/%EF%BC%AE%EF%BC%B9"</code></pre>

-   **{{site.data.keyword.IBM_notm}} SPR fonético:**

    <pre><code>curl -X PUT -u "apikey:{apikey}"
    --header "Content-Type: application/json"
    --data "{\"translation\":\"&lt;phoneme alphabet=\\\"ibm\\\" ph=\\\"nyu:yo:ku\\\"&gt;&lt;/phoneme&gt;\", \"part_of_speech\":\"Mesi\"}"
    "https://stream.watsonplatform.net/text-to-speech/api/v1/customizations/{customization_id}/words/%EF%BC%AE%EF%BC%B9"</code></pre>

## Consultar una palabra de un modelo personalizado
{: #cuWordQueryModel}

Para consultar la conversión de una palabra de un modelo personalizado, utilice el método `GET /v1/customizations/{customization_id}/words/{word}`. Especifique la palabra en el URL del método. La conversión se devuelve tal como está definida en el modelo personalizado ('suena como' o fonético).

En el ejemplo siguiente se consulta a un modelo personalizado la conversión de la palabra `IEEE`:

```bash
curl -X GET -u "apikey:{apikey}"
"https://stream.watsonplatform.net/text-to-speech/api/v1/customizations/{customization_id}/words/IEEE"
```
{: pre}

Si la palabra tiene una conversión 'suena como' en el modelo, el ejemplo devuelve la siguiente salida JSON:

```javascript
{
  "translation": "I triple E"
}
```
{: codeblock}

## Consultar todas las palabras de un modelo personalizado
{: #cuWordsQueryModel}

Para ver las conversiones de todas las palabras definidas en un modelo personalizado, utilice el método `GET /v1/customizations/{customization_id}/words`. En el ejemplo siguiente se utiliza este método para listar las entradas de un modelo personalizado que contiene conversiones 'suena como' para tres palabras:

```bash
curl -X GET -u "apikey:{apikey}"
"https://stream.watsonplatform.net/text-to-speech/api/v1/customizations/{customization_id}/words"
```
{: pre}

El método devuelve una matriz JSON con los datos siguientes. Para los modelos personalizados en japonés, la salida incluye la categoría léxica de las palabras.

```javascript
{
  "words": [
    {
      "word": "IEEE",
      "translation": "I triple E"
    },
    {
      "word": "NCAA",
      "translation": "N C double A"
    },
    {
      "word": "iPhone",
      "translation": "I phone"
    }
  ]
}
```
{: codeblock}

Tal como de describe en [Consulta de un modelo personalizado](/docs/services/text-to-speech?topic=text-to-speech-customModels#cuModelsQuery), también puede utilizar el método `GET /v1/customizations/{customization_id}` para ver los metadatos y las palabras de un modelo personalizado:

```bash
curl -X GET -u "apikey:{apikey}"
"https://stream.watsonplatform.net/text-to-speech/api/v1/customizations/{customization_id}"
```
{: pre}

El método devuelve una salida JSON con el formato siguiente. Dado que este ejemplo y el anterior especifican el mismo modelo personalizado, la matriz de palabras de su salida es idéntica.

```javascript
{
  "customization_id": "64f4807f-a5f1-5867-924f-7bba1a84fe97",
  "owner": "297cfd08-330a-22ba-93ce-1a73f454dd98",
  "created": "2016-07-15T19:15:17.926Z",
  "name": "curl Test",
  "language": "en-US",
  "description": "Customization test via curl",
  "last_modified": "2016-07-15T19:46:01.387Z",
  "words": [
    {
      "word": "IEEE",
      "translation": "I triple E"
    },
    {
      "word": "NCAA",
      "translation": "N C double A"
    },
    {
      "word": "iPhone",
      "translation": "I phone"
    }
  ]
}
```
{: codeblock}

## Consultar una palabra de un idioma
{: #cuWordsQueryLanguage}

Para consultar la pronunciación de una palabra, utilice el método `GET /v1/pronunciation`. Especifique una voz para obtener la pronunciación en el idioma de dicha voz. De forma predeterminada, el método devuelve la pronunciación en base a las reglas de pronunciación regular del servicio, pero también puede solicitar la pronunciación de un modelo de voz personalizado especificado. El método incluye cuatro parámetros de consulta que permiten especificar la información que se debe devolver:

-   El parámetro obligatorio `text` especifica la palabra cuya pronunciación ha de devolverse.
-   El parámetro opcional `voice` permite especificar el idioma de la pronunciación. Debe especificar uno de los modelos de voz (por ejemplo, `en-US_LisaVoice`) para indicar el idioma deseado, todas las voces del mismo idioma (por ejemplo, `en-US`) devuelven la misma pronunciación. De forma predeterminada, se devuelve la pronunciación en inglés de Estados Unidos.
-   El parámetro opcional `format` permite especificar el formato fonético de la pronunciación: `ipa` o `ibm`. De forma predeterminada, la pronunciación se devuelve en formato IPA.
-   El parámetro opcional `customization_id` permite especificar un modelo de voz personalizado del cual se debe devolver la pronunciación. Si la palabra no está definida en el modelo de voz especificado, el servicio devuelve la pronunciación predeterminada para el idioma del modelo. Si se omite este parámetro, se obtiene la conversión de la voz especificada sin personalización. No se puede especificar a la vez una voz y un modelo de voz personalizado.

Este método es útil porque permite consultar una palabra de cualquier idioma y, dado que no requiere un ID de personalización, no impone restricciones a las palabras que se pueden ver. Puede ser especialmente útil al componer una traducción fonética para una nueva palabra; se puede utilizar para obtener la pronunciación de una palabra existente y luego usarla como base de una nueva conversión, lo cual es mucho más conveniente que crear una conversión desde cero.

En el ejemplo siguiente se obtiene la pronunciación de la palabra `IEEE` en el formato predeterminado IPA.

```bash
curl -X GET -u "apikey:{apikey}"
"https://stream.watsonplatform.net/text-to-speech/api/v1/pronunciation?text=IEEE"
```
{: pre}

<pre><code data-copy="false" class="language-javascript">{
  "pronunciation": ".&#712;a&#618; .&#712;i .&#712;i .&#712;i"
}</code></pre>

En el ejemplo siguiente se especifica una conversión 'suena como' para la palabra `IEEE` y obtiene el equivalente fonético en el formato {{site.data.keyword.IBM_notm}} SPR. Obtener la pronunciación fonética de una conversión 'suena como' es un método especialmente interesante para componer una conversión fonética. Los espacios de la palabra están codificados en URL en el ejemplo.

```bash
curl -X GET -u "apikey:{apikey}"
"https://stream.watsonplatform.net/text-to-speech/api/v1/pronunciation?text=i%20triple%20e&format=ibm"
```
{: pre}

```javascript
{
  "pronunciation": "1Y.tr1Ipxl.1i"
}
```
{: codeblock}

## Suprimir una palabra de un modelo personalizado
{: #cuWordDelete}

Para suprimir una palabra de un modelo personalizado, utilice el método `DELETE /v1/customizations/{customization_id}/words/{word}`. Se debe especificar la palabra a suprimir en el URL del método. Sólo se pueden suprimir palabras individuales; no se pueden suprimir varias palabras con un solo método.

En el ejemplo siguiente se suprime la palabra `IEEE` del modelo personalizado especificado:

```bash
curl -X DELETE -u "apikey:{apikey}"
"https://stream.watsonplatform.net/text-to-speech/api/v1/customizations/{customization_id}/words/IEEE"
```
{: pre}
