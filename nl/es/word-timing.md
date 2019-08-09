---

copyright:
  years: 2015, 2019
lastupdated: "2019-06-04"

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

# Obtener temporizaciones de palabras
{: #timing}

La interfaz WebSocket proporciona la misma funcionalidad que los métodos HTTP `GET` y `POST /v1/synthesize`. También puede utilizar la interfaz WebSocket para obtener información de temporización para ubicaciones específicas o para todas las palabras de la entrada:
{: shortdesc}

-   Incluya el elemento SSML `<mark>` en el texto de entrada para identificar el tiempo en que aparece el marcador en el audio.
-   Especifique el parámetro `timings` de un mensaje de texto JSON para obtener información de temporización de todas las series del texto de entrada.

La información de temporización es útil para sincronizar el audio y el texto de entrada. Por ejemplo, puede coordinar los gestos de un robot con el contenido del discurso sintetizado.

El parámetro `timings` no está soportado para texto de entrada en japonés.
{: note}

## Cómo devuelve las temporizaciones de palabras el servicio
{: #timingHow}

Para devolver información de temporización de marcas o palabras, el servicio multiplexa secuencias binarias y de texto independientes para generar la respuesta:

-   Para cada elemento `<mark`>, el servicio devuelve un mensaje de texto JSON. Cada mensaje indica el tiempo exacto desde el principio del audio sintetizado en que se produce la marca.
-   Para temporizaciones de palabra de todas las series, el servicio devuelve uno o más mensajes de texto JSON. Cada mensaje contiene una matriz de palabras y sus tiempos de inicio y de finalización desde el principio del audio sintetizado.

Las secuencias binarias y de texto que envía el servicio son independientes. Por lo tanto, el servicio tiene poco control sobre el número de fragmentos de audio que entrega y de cuándo el usuario recibe los mensajes de texto y de audio. Por ejemplo, si el audio se sintetiza más rápidamente de lo que se comprime, es posible que todos los mensajes de texto lleguen antes que los de audio.

En términos prácticos, el servicio puede enviar un número arbitrario de fragmentos de audio, incluyendo múltiples fragmentos de audio antes y después de cada mensaje de texto. También es posible que un solo fragmento binario contenga datos de audio antes y después de la información de temporización de una marca o una palabra.

Sin embargo, el mensaje de texto que contiene la información de temporización siempre llega antes que el fragmento binario que contiene el audio correspondiente. Ademas, los mensajes de audio siempre llegan en orden, de forma que puede generar una síntesis de audio precisa del texto a partir de los resultados binarios.

## Especificar una marca SSML
{: #mark}

El elemento SSML opcional `<mark>` es una etiqueta vacía que coloca una marca en el texto que se va a sintetizar. Se notifica al cliente cuando todo el texto que precede al elemento `<mark>` se ha sintetizado.

El elemento acepta solo un atributo `name` que especifica una serie que identifica de forma exclusiva la marca. El nombre debe empezar por un carácter alfanumérico. El servicio devuelve el nombre junto con el tiempo en que se produce la marca desde el principio del audio sintetizado. Puede incluir cualquier número de marcas en el texto de entrada.

El siguiente fragmento de código JavaScript incluye una instancia del elemento `<mark>` con el nombre `here`:

```javascript
function onOpen(evt) {
  var message = {
    text: 'Hello <mark name="here"/> world',
    accept: '*/*'
  };
  websocket.send(JSON.stringify(message));
}
```
{: codeblock}

Cuando termina de sintetizar el texto que precede a la marca, el servicio envía un mensaje de texto que identifica el nombre de la marca y el tiempo en segundos en que aparece la marca en el audio:

```javascript
{
  "marks": [
    ["here", 0.5019387755102041]
  ]
}
```
{: codeblock}

El mensaje de texto que contiene la información de temporización siempre llega antes que el fragmento de audio que contiene la marca.

## Solicitar temporizaciones de palabras para todas las palabras
{: #timingRequest}

El parámetro opcional `timings` del objeto JSON que pasa al servicio en una solicitud devuelve información de temporización de todas las series del texto de entrada. Esta funcionalidad elimina la necesidad de especificar el elemento SSML `<mark>` para cada palabra de la entrada. Pase una matriz que incluya la serie `words` para solicitar temporizaciones de palabras. Pase una matriz vacía u omita el parámetro si no desea recibir información de temporización.

El servicio devuelve timings de palabras a través de la conexión de WebSocket de la misma forma que devuelve información de temporización de los elementos `<mark>` individuales. Devuelve uno o más mensajes de texto JSON. Cada mensaje contiene una matriz de palabras y sus tiempos de inicio y de finalización en segundos desde el principio del audio sintetizado. Por ejemplo, en el ejemplo siguiente se solicita información de temporización de las palabras:

```javascript
function onOpen(evt) {
  var message = {
    text: 'I have a pet bird.',
    accept: '*/*',
    timings: ['words']
  };
  websocket.send(JSON.stringify(message));
}
```
{: codeblock}

Como respuesta, el servicio puede devolver los mensajes de texto siguientes:

```javascript
{
  "words": [
    ["I", [0.0690258394023930, 0.1655782733012873]]
    ["have", [0.1655789302434486, 0.3722901056092351]]
    ["a", [0.3722906798320199, 0.4012192331086645]]
  ]
}
{
  "words": [
    ["pet", [0.4012195492838347, 0.5798213856109801]]
    ["bird.", [0.5798218710823425, 0.7440360383928273]]
  ]
}
```
{: codeblock}

Esta respuesta es sólo un ejemplo. El servicio puede devolver uno o más mensajes de texto con la información de temporización de la entrada. Además, los mensajes pueden ir intercalados con respuestas que contengan fragmentos binarios de audio. Pero el mensaje de texto que contiene la información de temporización de una palabra siempre llega antes que el fragmento de audio que contiene esa palabra.

### Temporizaciones para texto sin formato
{: #timingText}

El proceso de síntesis del servicio incluye un paso de normalización de texto que deletrea números, fechas, horas, importes monetarios, acrónimos y abreviaturas. Los resultados corresponden a la forma en que se dicen dichas series. Por ejemplo, la serie *$200* se lee con tres palabras *two*, *hundred* y *dollars*. Debido a que se utiliza la información de sincronización de palabras para sincronizar el audio con el texto de entrada, el servicio devuelve la información de sincronización que corresponde a la ortografía no normalizada de la entrada.

Por ejemplo, imaginemos el texto de entrada siguiente:

```
The coldest recorded temperature is -89.2 degrees Celsius in Antarctica on July 21, 1983!
```
{: codeblock}

El servicio devuelve temporizaciones de audio para las series siguientes:

"*The*", "*coldest*", "*recorded*", "*temperature*", "*is*", "*-89.2*", "*degrees*", "*Celsius*", "*in*", "*Antarctica*", "*on*", "*July*", "*21,*", "*1983!*"

Aunque "*-89.2*" se dice en el audio con cinco palabras distintas (*minus*, *eighty*, *nine*, *point*, *two*), el mensaje de texto proporciona información de temporización de la serie como si fuera una sola unidad, con el momento de inicio de *minus* y el momento de finalización de *two*.

Como en el ejemplo anterior, las series no normalizadas también pueden contener signos de puntuación. El servicio incluye la puntuación que precede o sigue a una palabra en el mensaje de texto que devuelve con las temporizaciones. Por ejemplo, las series "*21,*" y "*1983!*" incluyen puntuación que el servicio devuelve en el mensaje de texto. Aunque la puntuación se traduce en silencio, la temporización de audio de la palabra *no* incluye el silencio.

Por ejemplo, imaginemos un texto de entrada que contiene la siguiente oración condicional:

```
If it is sunny, I will go to the beach.
```
{: codeblock}

El servicio devuelve información de temporización para todas las series de la entrada, incluyendo "*sunny,*" y "*beach.*", ambas terminan en la puntuación que produce un silencio. Pero la información de temporización de "*sunny,*" no incluye el silencio producido por la coma, y la información de temporización de "*beach.*" no incluye el silencio del punto. La información refleja únicamente la temporización de las series habladas.

### Temporizaciones para texto SSML
{: #timingSSML}

Cuando el servicio sintetiza texto sin formato, devuelve todos los caracteres de entrada excepto los espacios en blanco como parte de las series en su respuesta de temporización de palabras. No ocurre lo mismo con SSML, puesto que algunos elementos SSML no generan audio. En la lista siguiente se resumen los elementos SSML que pueden afectar a la información de temporización de palabras:

-   `<say-as>` indica cómo se debe manejar en el paso de normalización el texto que aparece entre las etiquetas de apertura y cierre de `<say-as>`. Los atributos especifican cómo se debe leer el texto que se incluye. En el ejemplo siguiente se indica cómo se va a pronunciar la fecha:

    ```xml
    The baby was born on <say-as interpret-as="date" format="mdy">3/4/2016</say-as>.
    ```
    {: codeblock}

    El servicio devuelve información de temporización para las series siguientes: "*The*", "*baby*", "*was*", "*born*", "*on*", "*3/4/2016.*" El servicio normaliza la serie "*3/4/2016*" como "*march fourth two thousand sixteen*". La información de temporización de palabras para la serie refleja el momento de inicio de "*march*" y el momento de finalización de "*sixteen*".

    En el ejemplo siguiente se indica que la palabra `Hello` se tiene que deletrear:

    ```xml
    <say-as interpret-as="letters">Hello</say-as>.
    ```
    {: codeblock}

    El servicio devuelve información de temporización para la serie "*Hello.*". El servicio deletrea la palabra letra por letra durante el paso de normalización. La información de temporización de palabras de la respuesta indica el momento de inicio de la letra "*h*" y el momento de finalización de la letra "*o*".
-   `<phoneme>` proporciona una pronunciación del texto que hay entre las etiquetas de apertura y cierne de `<phoneme>`. Pero tanto el texto como la etiqueta de cierre son opcionales. En el ejemplo siguiente hay texto y etiqueta de cierre para este atributo:

    ```xml
    The <phoneme alphabet="ibm" ph=".0tx.1me.0fo">tomato</phoneme> was ripe.
    ```
    {: codeblock}

    El servicio devuelve información de temporización para las series siguientes: "*The*", "*tomato*", "*was*", "*ripe.*"

    En cambio, el ejemplo siguiente proporciona un elemento `<phoneme>` unario sin texto ni etiqueta de cierre:

    ```xml
    The <phoneme alphabet="ibm" ph=".0tx.1me.0fo"/> was ripe.
    ```
    {: codeblock}

    En este caso, el servicio devuelve información de temporización para las series siguientes: "*The*", "*&lt;phoneme&gt;*", "*was*", "*ripe.*"
-   `<sub>` sustituye el texto que se incluye en el atributo `alias` del elemento por el texto que aparece entre las etiquetas `<sub>` de apertura y cierre en el audio hablado. Por ejemplo, la entrada siguiente incluye una sola etiqueta `<sub>`:

    ```xml
    I work at <sub alias="International Business Machines">IBM</sub>.
    ```
    {: codeblock}

    El servicio genera información de temporización para las series siguientes: "*I*", "*work*", "*at*", "*{{site.data.keyword.IBM_notm}}.*". El servicio normaliza la serie "*{{site.data.keyword.IBM_notm}}*" como "*International Business Machines*". La información de temporización de la serie refleja el momento de inicio de "*International*" y el momento de finalización de "*Machines*".
-   `<break>` inserta una pausa en el texto hablado. El servicio refleja el silencio resultante en las temporizaciones de palabras como un espacio entre el momento de finalización de la palabra que precede al elemento `<break>` y el momento de inicio de la palabra que sigue a este elemento.
- `<paragraph>` (o `<p>`) puede añadir silencio en el audio. El servicio no devuelve información de temporización para el silencio.
- `<sentence>` (o `<s>`) puede añadir silencio en el audio. El servicio no devuelve información de temporización para el silencio.

Los elementos SSML que no se mencionan en la lista no afectan a la información de temporización de palabras. Para obtener más información sobre el soporte del servicio para SSML, consulte [Utilización de SSML](/docs/services/text-to-speech?topic=text-to-speech-ssml).

## Ejemplos con elementos mark
{: #timingExample}

En los ejemplos siguientes se muestra una sesión de WebSocket simple entre un cliente y el servicio. Los ejemplos se centran en el intercambio de datos, no en la apertura de la conexión. El cliente envía un mensaje de texto que incluye dos elementos `<mark>`, denominados `SIMPLE` y `EXAMPLE`, y solicita que el audio se devuelva en formato WAV:

```javascript
{
  "text": "This is a <mark name=\"SIMPLE\"/>simple <mark name=\"EXAMPLE\"/> example.",
  "accept": "audio/wav"
}
```
{: codeblock}

El servicio primero envía un mensaje para confirmar el formato de audio. Después envía varios mensajes con los resultados. El servicio no puede garantizar el número de fragmentos de audio que envía al cliente ni el orden en el que se entregan los mensajes de texto y de audio.

Las dos respuestas siguientes son posibles. En cada caso, el servicio envía dos mensajes de texto que identifican las ubicaciones de las marcas en la secuencia binaria. Pero envía un número arbitrario de mensajes binarios que contienen el audio. La información de temporización de una marca siempre llega antes que el bloque de audio que contiene la ubicación de la marca.

### Primer ejemplo de respuesta

En el primer ejemplo de respuesta, los mensajes de texto se intercalan con ´múltiples mensajes de audio.

```javascript
{
  "binary_streams": [
    {
      "content_type": "audio/wav"
    }
  ]
}
... uno o más fragmentos de audio binario
    todo el audio va antes de la marca SIMPLE ...
{
  "marks": [
    [
      "SIMPLE",
      0.7848991042702103
    ]
  ]
}
... uno o más fragmentos de audio binario
    el audio puede ir antes o después de la marca SIMPLE
    todo el audio va antes de la marca EXAMPLE ...
{
  "marks": [
    [
      "EXAMPLE", 1.0034702987337102
    ]
  ]
}
... uno o más fragmentos de audio binario
    el audio puede ir antes o después de la marca EXAMPLE ...
```
{: codeblock}

### Segundo ejemplo de respuesta

En el segundo ejemplo de respuesta, los mensajes de texto llegan antes que ninguno de los mensajes de audio.

```javascript
{
  "binary_streams": [
    "content_type": "audio/wav"}
  ]
}
{
  "marks": [
    [
      "SIMPLE", 0.7848991042702103
    ]
  ]
}
{
  "marks": [
    [
      "EXAMPLE", 1.0034702987337102
    ]
  ]
}
... uno o más fragmentos de audio binario ...
```
{: codeblock}
