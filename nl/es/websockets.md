---

copyright:
  years: 2015, 2019
lastupdated: "2019-04-09"

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

# La interfaz WebSocket
{: #usingWebSocket}

Para sintetizar texto a voz con la interfaz WebSocket del servicio {{site.data.keyword.texttospeechfull}}, primero debe establecer una conexión con el servicio llamando a su método `/v1/synthesize`. A continuación, debe enviar el texto a sintetizar al servicio en forma de mensaje de texto JSON a través de la conexión. El servicio cierra automáticamente la conexión WebSocket cuando termina de procesar la solicitud.
{: shortdesc}

La solicitud de síntesis y el ciclo de respuesta incluye los siguientes pasos:

1.  [Abrir una conexión](#WSopen).
1.  [Enviar el texto de entrada](#WSsend).
1.  [Recibir una respuesta](#WSreceive).

La interfaz WebSocket acepta la misma entrada y produce resultados idénticos que los métodos `GET` y `POST /v1/synthesize` de la interfaz HTTP. Sin embargo, la interfaz WebSocket admite el uso del elemento SSML `<mark>` para identificar la ubicación de marcadores especificados por el usuario en el audio. También puede devolver información de temporización para todas las series del texto de entrada. Para obtener más información, consulte [Obtener temporizaciones de palabras](/docs/services/text-to-speech/word-timing.html).

Los fragmentos de código de ejemplo que se muestran a continuación están escritos en JavaScript y se basan en la API de WebSocket HTML5. Para obtener más información sobre el protocolo WebSocket, consulte Internet Engineering Task Force (IETF) [Request for Comment (RFC) 6455 ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](http://tools.ietf.org/html/rfc6455){: new_window}.
{: note}

## Abrir una conexión
{: #WSopen}

Para abrir una conexión con el servicio se debe hacer una llamada al método `/v1/synthesize` a través del protocolo WebSocket Secure (WSS). El método está disponible en el punto final siguiente:

```
wss://{host_name}/text-to-speech/api/v1/synthesize
```
{: codeblock}

donde `{host_name}` es la ubicación donde está alojada su aplicación:

-   `stream.watsonplatform.net` para Dallas (en los ejemplos siguientes se utiliza este nombre de host)
-   `stream-fra.watsonplatform.net` para Frankfurt
-   `gateway-syd.watsonplatform.net` para Sídney
-   `gateway-wdc.watsonplatform.net` para Washington, DC
-   `gateway-tok.watsonplatform.net` para Tokio
-   `gateway-lon.watsonplatform.net` para Londres

Un cliente WebSocket llama a este método con los siguientes parámetros de consulta para establecer una conexión autenticada con el servicio. Si utiliza la autenticación de IAM (Identity and Access Management), utilice el parámetro de consulta `access_token`. Si utiliza las credenciales de servicio de Cloud Foundry, utilice el parámetro de consulta `watson-token`.

<table>
  <caption>Tabla 1. Parámetros del método <code>/v1/synthesize</code></caption>
  <tr>
    <th style="text-align:left; width:23%">Parámetro</th>
    <th style="text-align:center; width:12%">Tipo de datos</th>
    <th style="text-align:left">Descripción</th>
  </tr>
  <tr>
    <td style="text-align:left"><code>access_token</code>
      <br/><em>Opcional</em></td>
    <td style="text-align:center">Serie</td>
    <td style="text-align:left">
      <em>Si utiliza la autenticación de IAM,</em> pase una señal de acceso de IAM
      válida para autenticarse con el servicio. Se pasa una señal de acceso de IAM
      en lugar de pasar una clave de API con la llamada. Debe utilizar la
      señal de acceso antes de que caduque. Para obtener información sobre
      cómo obtener una señal de acceso, consulte
      [Autenticación con señales IAM](/docs/services/watson/getting-started-iam.html).
    </td>
  </tr>
  <tr>
    <td style="text-align:left"><code>watson-token</code>
      <br/><em>Opcional</em></td>
    <td style="text-align:center">Serie</td>
    <td style="text-align:left">
      <em>Si utiliza las credenciales de servicio de Cloud Foundry,</em> pase una
      señal de autenticación de {{site.data.keyword.watson}} válida para autenticarse
      con el servicio. Se pasa una señal de {{site.data.keyword.watson}} en lugar
      de pasar las credenciales de servicio con la llamada.
      Las señales de {{site.data.keyword.watson}} están basadas en las credenciales
      de servicio de Cloud Foundry, que utilizan un `username` y una `password`
      para la autenticación HTTP básica. Para obtener información sobre cómo
      obtener una señal de {{site.data.keyword.watson}}, consulte
      [Señales de {{site.data.keyword.watson}}](/docs/services/watson/getting-started-tokens.html).
    </td>
  </tr>
  <tr>
    <td><code>voice</code><br/><em>Opcional</em></td>
    <td style="text-align:center">Serie</td>
    <td>
      Especifica la voz en que se debe leer el texto en el audio.
      Omita el parámetro para utilizar la voz predeterminada, `en-US_MichaelVoice`.
      Para obtener más información, consulte
      [Idiomas y voces](/docs/services/text-to-speech/voices.html).
    </td>
  </tr>
  <tr>
    <td><code>customization_id</code><br/><em>Opcional</em></td>
    <td style="text-align:center">Serie</td>
    <td>
      Especifica el identificador exclusivo global (GUID) de un modelo de voz
      personalizado a utilizar para la síntesis. Sólo se garantiza que un modelo
      de voz personalizado funcionará si coincide con el idioma de la voz que
      se utiliza para la síntesis. Si incluye un ID de personalización, debe
      llamar al método con las credenciales de servicio del propietario del modelo personalizado.
      Omita el parámetro para utilizar la voz especificada sin personalización.
      Para obtener más información, consulte
      [Comprender la personalización](/docs/services/text-to-speech/custom-intro.html).
    </td>
  </tr>
  <tr>
    <td><code>x-watson-learning-opt-out</code><br/><em>Opcional</em></td>
    <td style="text-align:center">Booleano</td>
    <td>
      Indica si el servicio registra las solicitudes y los resultados que se envían
      a través de la conexión. Para evitar que IBM acceda a sus datos para mejoras de servicio
      generales, especifique <code>true</code> en el parámetro. Para
      obtener más información, consulte
      [Control del registro de solicitudes para los servicios de Watson](/docs/services/watson/getting-started-logging.html).
    </td>
  </tr>
  <tr>
    <td style="text-align:left"><code>x-watson-metadata</code>
      <br/><em>Opcional</em></td>
    <td style="text-align:center">Serie</td>
    <td style="text-align:left">
      Asocia un ID de cliente con los datos que se pasan a través
      de la conexión. El parámetro acepta el argumento
      <code>customer_id={id}</code>, donde <code>id</code> es una serie
      aleatoria o genérica para asociar a los datos. Debe codificar
      como URL del argumento en el parámetro, por ejemplo,
      `customer_id%3dmy_ID`. De forma predeterminada, no hay ningún ID
      de cliente asociado a los datos. Para obtener más información, consulte
      [Seguridad de la información](/docs/services/text-to-speech/information-security.html).
    </td>
  </tr>
</table>

El siguiente fragmento de código JavaScript abre una conexión con el servicio. La llamada al método `/v1/synthesize` pasa los parámetros de consulta `voice` y `access_token`, el primero para indicar al servicio que debe utilizar la voz de Allison en inglés de Estados Unidos. Una vez establecida la conexión, se definen los escuchas de sucesos (`onOpen`, `onClose`, etc.) para responder a los sucesos del servicio.

```javascript
var IAM_access_token = '{access_token}';
var wsURI = 'wss://stream.watsonplatform.net/text-to-speech/api/v1/synthesize'
  + '?access_token=' + IAM_access_token
  + '&voice=en-US_AllisonVoice';

var websocket = new WebSocket(wsURI);
websocket.onopen = function(evt) { onOpen(evt) };
websocket.onclose = function(evt) { onClose(evt) };
websocket.onmessage = function(evt) { onMessage(evt) };
websocket.onerror = function(evt) { onError(evt) };
```
{: codeblock}

## Enviar texto de entrada
{: #WSsend}

Para sintetizar texto, el cliente pasa un mensaje de texto JSON simple al servicio con los parámetros siguientes.

<table>
  <caption>Tabla 2. Parámetros del mensaje de texto JSON</caption>
  <tr>
    <th style="text-align:left; width:23%">Parámetro</th>
    <th style="text-align:center; width:12%">Tipo de datos</th>
    <th style="text-align:left">Descripción</th>
  </tr>
  <tr>
    <td><code>text</code><br/><em>Obligatorio</em></td>
    <td style="text-align:center">Serie</td>
    <td>
      Proporciona el texto a sintetizar. El cliente puede pasar
      texto sin formato o texto anotado con SSML (Speech Synthesis
      Markup Language). El cliente puede pasar un máximo de 5 KB de
      texto de entrada con la solicitud. Este límite incluye cualquier
      SSML especificado. Para obtener más información, consulte
      [Especificar texto de entrada](/docs/services/text-to-speech/http.html#input)
      y las secciones siguientes.<br/><br/>
      La entrada SSML también puede incluir el elemento <code>&lt;mark&gt;</code>.
      Para obtener más información, consulte
      [Especificar una marca SSML](/docs/services/text-to-speech/word-timing.html#mark).
    </td>
  </tr>
  <tr>
    <td><code>accept</code><br/><em>Obligatorio</em></td>
    <td style="text-align:center">Serie</td>
    <td>
      Especifica el formato solicitado (tipo MIME) del audio. Utilice
      `*/*` para solicitar el formato de audio predeterminado,
      <code>audio/ogg;codecs=opus</code>. Para obtener más información,
      consulte [Formatos de audio](/docs/services/text-to-speech/audio-formats.html).
    </td>
  </tr>
  <tr>
    <td><code>timings</code><br/><em>Opcional</em></td>
    <td style="text-align:center">Serie[ ]</td>
    <td>
      Especifica que el servicio debe devolver información de temporización de palabras
      para todas las series del texto de entrada. El servicio devuelve el momento
      de inicio y finalización de cada señal de entrada. Especifique <code>words</code>
      como único elemento de la matriz para solicitar temporizaciones de palabras. Especifique
      una matriz vacía o bien omita el parámetro para no recibir temporizaciones de palabras.
      Para obtener más información, consulte
      [Obtener temporizaciones de palabras](/docs/services/text-to-speech/word-timing.html#timing). <em>No soportado para texto de entrada en japonés.</em>
    </td>
  </tr>
</table>

El siguiente fragmento de código JavaScript pasa un mensaje "Hello world" simple como texto de entrada y solicita el formato predeterminado para el audio. Las llamadas se incluyen en la función `onOpen` que se ha definido para el cliente para asegurarse de que se envían sólo después de que se haya establecido la conexión.

```javascript
function onOpen(evt) {
  var message = {
    text: 'Hello world',
    accept: '*/*'
  };
  websocket.send(JSON.stringify(message));
}
```
{: codeblock}

El servicio responde a este mensaje enviando un mensaje de texto que confirma el formato de la respuesta de audio. La siguiente respuesta confirma el formato de audio predeterminado.

```javascript
{
  'binary_streams': [
    {
      content_type: 'audio/ogg;codecs=opus'
    }
  ]
}
```
{: codeblock}

## Recibir una respuesta
{: #WSreceive}

Una vez que ha confirmado el formato de audio, el servicio envía el audio sintetizado como una corriente binaria de datos en el formato indicado. El servicio envía información de temporización en forma de uno o más mensajes de texto si

-   El texto de entrada incluye uno o más elementos SSML `<mark>`.
-   Se ha especificado el parámetro `timings` en la solicitud.

El servicio también puede enviar mensajes de texto con avisos o errores. Cuando termina de sintetizar el texto de entrada, el servicio cierra automáticamente la conexión de WebSocket.

El cliente tiene que añadir respuestas binarias del servicio a los resultados de audio recibidos a través de la conexión. Puede manejar mensajes de texto respondiendo a los mismos, visualizándolos o capturándolos para que los utilice la aplicación (por ejemplo, si contienen ubicaciones de marcas). En el siguiente ejemplo simple de una función `onMessage`, se añaden mensajes de texto y binarios que se reciben del servicio a la variable adecuada según tipo de los mismos. Cuando se ejecuta la función `onClose()`, ya se ha recibido la secuencia de audio completa.

```javascript
var messages;
var audioStream;

function onMessage(evt) {
  if (typeof evt.data === string) {
    messages += evt.data;
  } else {
    console.log('Received ' + evt.data.size() + ' binary bytes');
    audioStream += evt.data;
  }
}

function onClose(evt) {
  // The audio stream is complete.
}
```
{: codeblock}

## Códigos de retorno de WebSocket
{: #returnCodes}

El servicio puede enviar los siguientes códigos de retorno al cliente a través de la conexión de WebSocket:

-   `1000` indica el cierre normal de la conexión, lo que significa que la finalidad para la que se ha establecido la conexión se ha cumplido.
-   `1002` indica que el servicio cierra la conexión debido a un error de protocolo.
-   `1006` indica que la conexión se ha cerrado anormalmente.
-   `1009` indica que el tamaño de trama ha sobrepasado el límite de 4 MB.
-   `1011` indica que el servicio está terminando la conexión porque ha encontrado una condición inesperada que le impide cumplir la solicitud, como por ejemplo un argumento no válido. El código de retorno también puede indicar que el texto de entrada era demasiado grande.

Si el socket se cierra con un error, el servicio envía al cliente un mensaje informativo con el formato `{"error": "Specific error message"}` antes de cerrarse. El servicio también puede enviar mensajes de aviso no muy graves para parámetros desconocidos.

## Ejemplos de mensajes de error y de aviso
{: #returnErrors}

Los ejemplos siguientes muestran respuestas de error. Incluyen un mensaje de texto JSON y un mensaje formateado del método de devolución de llamada `onClose` del cliente. Los mensajes con formato empiezan por el booleano `true` porque la conexión está cerrada. También incluyen el código de error de WebSocket que ha provocado el cierre.

-   En este ejemplo se muestran los mensajes de error para un argumento no válido del parámetro `accept`:

    ```javascript
    {
      "error": "Unsupported mimetype. Supported mimetypes are: ['application/json', 'audio/flac', ...]"
    }
    (True, 1011, u'see the previous message for the error details.')
    ```
    {: codeblock}

-   En este ejemplo se muestran los mensajes de error para un parámetro `text` que falta:

    ```javascript
    {
      "error": "Required parameter \"text\" is missing."
    }
    (True, 1011, u'see the previous message for the error details.')
    ```
    {: codeblock}

En el ejemplo siguiente se muestra una respuesta de aviso, en este caso para un parámetro desconocido denominado `invalid-parameter`. No incluye el segundo mensaje porque la conexión no se cierra debido al aviso.

```javascript
{
  "warnings": "Unknown arguments: invalid-parameter."
}
```
{: codeblock}

Para obtener más información acerca de los códigos de retorno de WebSocket, consulte Internet Engineering Task Force (IETF) [Request for Comments (RFC) 6455 ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](http://tools.ietf.org/html/rfc6455){: new_window}.
