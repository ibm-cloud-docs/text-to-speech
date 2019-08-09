---

copyright:
  years: 2015, 2019
lastupdated: "2019-07-25"

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

# Idiomas y voces
{: #voices}

El servicio {{site.data.keyword.texttospeechfull}} da soporte a una variedad de idiomas, voces y dialectos. El servicio ofrece al menos una voz femenina para cada idioma. Para algunos idiomas, el servicio ofrece varias voces, tanto masculinas como femeninas. Cada voz utiliza la cadencia y la entonación adecuadas según su dialecto.
{: shortdesc}

Se ha dejado de prestar servicio de mantenimiento a las voces de `V2` que estaban disponibles anteriormente con el servicio. Si utiliza una voz de `V2` en su aplicación, el servicio automáticamente utiliza la voz equivalente de `V3`.
{: note}

## Idiomas y voces soportados
{: #languageVoices}

En la tabla 1 se listan las voces disponibles para cada idioma y dialecto, indicando también el tipo y el género. Todas las voces están disponibles como [Voces estándar](#standardVoices) y como [Voces neuronales](#neuralVoices). Si se omite el parámetro opcional `voice` en una solicitud, el servicio utilizará la voz estándar `en-US_MichaelVoice` de forma predeterminada.

<table style="width:100%">
  <caption>Tabla 1. Idiomas y voces soportados</caption>
  <tr>
    <th style="text-align:left">Idioma</th>
    <th style="text-align:center">Tipo</th>
    <th style="text-align:center">Voz</th>
    <th style="text-align:center">Género</th>
  </tr>
  <tr>
    <td style="text-align:left">Portugués de Brasil</td>
    <td style="text-align:center">Estándar</td>
    <td style="text-align:center"><code>pt-BR_IsabelaVoice</code></td>
    <td style="text-align:center">Femenino</td>
  </tr>
  <tr>
    <td style="text-align:left"></td>
    <td style="text-align:center">Neuronal</td>
    <td style="text-align:center"><code>pt-BR_IsabelaV3Voice</code></td>
    <td style="text-align:center">Femenino</td>
  </tr>
  <tr>
    <td style="text-align:left">Español de España</td>
    <td style="text-align:center">Estándar</td>
    <td style="text-align:center"><code>es-ES_EnriqueVoice</code></td>
    <td style="text-align:center">Masculino</td>
  </tr>
  <tr>
    <td style="text-align:left"></td>
    <td style="text-align:center">Neuronal</td>
    <td style="text-align:center"><code>es-ES_EnriqueV3Voice</code></td>
    <td style="text-align:center">Masculino</td>
  </tr>
  <tr>
    <td></td>
    <td style="text-align:center">Estándar</td>
    <td style="text-align:center"><code>es-ES_LauraVoice</code></td>
    <td style="text-align:center">Femenino</td>
  </tr>
  <tr>
    <td></td>
    <td style="text-align:center">Neuronal</td>
    <td style="text-align:center"><code>es-ES_LauraV3Voice</code></td>
    <td style="text-align:center">Femenino</td>
  </tr>
  <tr>
    <td style="text-align:left">Francés</td>
    <td style="text-align:center">Estándar</td>
    <td style="text-align:center"><code>fr-FR_ReneeVoice</code></td>
    <td style="text-align:center">Femenino</td>
  </tr>
  <tr>
    <td style="text-align:left"></td>
    <td style="text-align:center">Neuronal</td>
    <td style="text-align:center"><code>fr-FR_ReneeV3Voice</code></td>
    <td style="text-align:center">Femenino</td>
  </tr>
  <tr>
    <td style="text-align:left">Alemán</td>
    <td style="text-align:center">Estándar</td>
    <td style="text-align:center"><code>de-DE_BirgitVoice</code></td>
    <td style="text-align:center">Femenino</td>
  </tr>
  <tr>
    <td style="text-align:left"></td>
    <td style="text-align:center">Neuronal</td>
    <td style="text-align:center"><code>de-DE_BirgitV3Voice</code></td>
    <td style="text-align:center">Femenino</td>
  </tr>
  <tr>
    <td></td>
    <td style="text-align:center">Estándar</td>
    <td style="text-align:center"><code>de-DE_DieterVoice</code></td>
    <td style="text-align:center">Masculino</td>
  </tr>
  <tr>
    <td></td>
    <td style="text-align:center">Neuronal</td>
    <td style="text-align:center"><code>de-DE_DieterV3Voice</code></td>
    <td style="text-align:center">Masculino</td>
  </tr>
  <tr>
    <td style="text-align:left">Italiano</td>
    <td style="text-align:center">Estándar</td>
    <td style="text-align:center"><code>it-IT_FrancescaVoice</code></td>
    <td style="text-align:center">Femenino</td>
  </tr>
  <tr>
    <td style="text-align:left"></td>
    <td style="text-align:center">Neuronal</td>
    <td style="text-align:center"><code>it-IT_FrancescaV3Voice</code></td>
    <td style="text-align:center">Femenino</td>
  </tr>
  <tr>
    <td style="text-align:left">Japonés</td>
    <td style="text-align:center">Estándar</td>
    <td style="text-align:center"><code>ja-JP_EmiVoice</code></td>
    <td style="text-align:center">Femenino</td>
  </tr>
  <tr>
    <td style="text-align:left"></td>
    <td style="text-align:center">Neuronal</td>
    <td style="text-align:center"><code>ja-JP_EmiV3Voice</code></td>
    <td style="text-align:center">Femenino</td>
  </tr>
  <tr>
    <td style="text-align:left">Español de América Latina</td>
    <td style="text-align:center">Estándar</td>
    <td style="text-align:center"><code>es-LA_SofiaVoice</code></td>
    <td style="text-align:center">Femenino</td>
  </tr>
  <tr>
    <td style="text-align:left"></td>
    <td style="text-align:center">Neuronal</td>
    <td style="text-align:center"><code>es-LA_SofiaV3Voice</code></td>
    <td style="text-align:center">Femenino</td>
  </tr>
  <tr>
    <td style="text-align:left">Español de América del Norte</td>
    <td style="text-align:center">Estándar</td>
    <td style="text-align:center"><code>es-US_SofiaVoice</code></td>
    <td style="text-align:center">Femenino</td>
  </tr>
  <tr>
    <td style="text-align:left"></td>
    <td style="text-align:center">Neuronal</td>
    <td style="text-align:center"><code>es-US_SofiaV3Voice</code></td>
    <td style="text-align:center">Femenino</td>
  </tr>
  <tr>
    <td style="text-align:left">Inglés del Reino Unido</td>
    <td style="text-align:center">Estándar</td>
    <td style="text-align:center"><code>en-GB_KateVoice</code></td>
    <td style="text-align:center">Femenino</td>
  </tr>
  <tr>
    <td style="text-align:left"></td>
    <td style="text-align:center">Neuronal</td>
    <td style="text-align:center"><code>en-GB_KateV3Voice</code></td>
    <td style="text-align:center">Femenino</td>
  </tr>
  <tr>
    <td style="text-align:left">Inglés de EE.UU.</td>
    <td style="text-align:center">Estándar</td>
    <td style="text-align:center"><code>en-US_AllisonVoice</code></td>
    <td style="text-align:center">Femenino</td>
  </tr>
  <tr>
    <td style="text-align:left"></td>
    <td style="text-align:center">Neuronal</td>
    <td style="text-align:center"><code>en-US_AllisonV3Voice</code></td>
    <td style="text-align:center">Femenino</td>
  </tr>
  <tr>
    <td></td>
    <td style="text-align:center">Estándar</td>
    <td style="text-align:center"><code>en-US_LisaVoice</code></td>
    <td style="text-align:center">Femenino</td>
  </tr>
  <tr>
    <td></td>
    <td style="text-align:center">Neuronal</td>
    <td style="text-align:center"><code>en-US_LisaV3Voice</code></td>
    <td style="text-align:center">Femenino</td>
  </tr>
  <tr>
    <td></td>
    <td style="text-align:center">Estándar</td>
    <td style="text-align:center"><code>en-US_MichaelVoice</code></td>
    <td style="text-align:center">Masculino</td>
  </tr>
  <tr>
    <td></td>
    <td style="text-align:center">Neuronal</td>
    <td style="text-align:center"><code>en-US_MichaelV3Voice</code></td>
    <td style="text-align:center">Masculino</td>
  </tr>
</table>

Las voces `es-LA_SofiaVoice` y `es-US_SofiaVoice` son esencialmente la misma voz. La diferencia más significativa se refiere a cómo las dos voces interpretan el signo de dólar ($). La versión latinoamericana utiliza el término *pesos*, mientras que la versión norteamericana utiliza el término *d&oacute;lares*. También puede haber otras diferencias menores entre las dos voces.
{: note}

### Voces estándar
{: #standardVoices}

Las voces estándar no incluyen una cadena de la versión (`V3`) en sus nombres (por ejemplo, `pt-BR_IsabelaVoice` y `en-US_AllisonVoice`). Las voces estándar utilizan la síntesis concatenativa para ensamblar segmentos (o unidades) de voz grabada para generar el audio solicitado. Los puntos de concatenación de los segmentos grabados a veces generan discontinuidades de habla que pueden degradar la calidad y la naturalidad del discurso resultante.

### Voces neuronales
{: #neuralVoices}

Las voces neuronales incluyen una cadena de la versión (`V3`) en sus nombres (por ejemplo, `pt-BR_IsabelaV3Voice` y `en-US_AllisonV3Voice`). En su lugar de basarse en la selección y la concatenación de segmentos, la tecnología de voz neuronal utiliza varias redes neuronales profundas (DNN - Deep Neural Networks) para predecir las características acústicas (espectrales) del habla. Las DNN se basan en el habla humana natural y generan el audio resultante a partir de las características acústicas pronosticadas.

Durante la síntesis, las DNN predicen el tono y la duración del fonema (prosodia), la estructural espectral y la forma de onda del habla. Las voces neuronales generan habla que es nítida y clara, con una calidad de sonido muy natural y suave. Por ello, las voces neuronales tienen mayor coherencia en la calidad en general que las voces estándar.

Para obtener más información sobre la tecnología de voz neuronal del servicio, consulte

-   La publicación de blog [IBM Watson Text to Speech: Neural Voices Generally Available](https://medium.com/ibm-watson/ibm-watson-text-to-speech-neural-voices-added-to-service-e562106ff9c7){: external}
-   El documento de investigación [High quality, lightweight and adaptable Text to Speech using LPCNet](https://arxiv.org/abs/1905.00590){: external}

Las voces neuronales no admiten los elementos SSML o atributos siguientes:

-   El atributo `volume` del elemento `<prosody>`
-   El elemento `<express-as>`
-   El elemento `<voice-transformation>`

Sin embargo, es posible que encuentre que estas características SSML ya no son necesarias cuando se utilicen las voces neuronales. Además, puede realizar modificaciones de tono y velocidad a voces neuronales utilizando el elemento `<prosody>` en lugar del elemento `<voice-transformation>`. Para obtener más información, consulte [Elemento prosody](/docs/services/text-to-speech?topic=text-to-speech-elements#prosody_element).

### Personalización de voces
{: #customizeVoice}

Al sintetizar texto, el servicio aplica reglas de pronunciación dependientes del idioma para convertir la ortografía ordinaria de cada palabra en una ortografía fonética. Las reglas de pronunciación del servicio funcionan bien para las palabras comunes, pero pueden producir resultados imperfectos para palabras inusuales, tales como vocablos extranjeros, nombres personales y abreviaturas o acrónimos.

Si el léxico de la aplicación incluye palabras de este tipo, puede utilizar la interfaz de personalización para especificar cómo los pronuncia el servicio. Para obtener más información, consulte [Comprender la personalización](/docs/services/text-to-speech?topic=text-to-speech-customIntro).

Se crea un modelo de voz personalizado para un idioma específico, no para una voz específica. Por ello, se puede utilizar un modelo personalizado con cualquier voz, estándar o neuronal, para su idioma especificado.

## Especificar una voz
{: #specifyVoice}

Tanto los métodos HTTP `GET` y `POST /v1/synthesize`, como el método WebSocket `/v1/synthesize`, aceptan un parámetro de consulta opcional `voice` para especificar la voz del audio sintetizado. Para obtener más información, consulte [La interfaz HTTP](/docs/services/text-to-speech?topic=text-to-speech-usingHTTP) y [La interfaz WebSocket](/docs/services/text-to-speech?topic=text-to-speech-usingWebSocket).

El servicio basa su comprensión del idioma del texto de entrada en la voz especificada. Asegúrese de especificar una voz que coincida con el idioma del texto de entrada. Por ejemplo, si especifica la voz en francés (`fr-FR_ReneeVoice`), el servicio presupone que el texto de entrada está escrito en francés. Si pasa texto que no está escrito en el mismo idioma que la voz (por ejemplo, texto en inglés para una voz en francés), puede ser que el servicio no produzca resultados comprensibles.

## Listado de todas las voces disponibles
{: #listVoices}

El método `GET /v1/voices` muestra información sobre todas las voces disponibles. No toma argumentos y devuelve una matriz JSON denominada `voices`. La matriz incluye un objeto distinto para cada voz.

```javascript
{
  "voices": [
    {
      "name": "en-US_LisaVoice",
      "language": "en-US",
      "gender": "female",
      "url": "https://stream.watsonplatform.net/text-to-speech/api/v1/voices/en-US_LisaVoice",
      "description": "Lisa: American English female voice.",
      "customizable": true,
      "supported_features": {
        "voice_transformation": true,
        "custom_pronunciation": true
      }
    },
    . . .
  ]
}
```
{: codeblock}

Los campos de los objetos de voz proporcionan la información siguiente:

-   `name` es un identificador para la voz (por ejemplo, `en-US_LisaVoice`). Especifique este valor para el parámetro `voice` del método `/v1/synthesize`.
-   `language` especifica el idioma y la región de la voz (por ejemplo, `en-US`).
-   `gender` identifica la voz como `male` (masculina) o `female` (femenina).
-   `url` identifica el URL de la voz.
-   `description` proporciona una breve descripción de la voz.
-   `customizable` es un valor booleano que indica si la voz se puede personalizar con la interfaz de personalización del servicio. (Este campo, que proporciona la misma información que el campo `custom_pronunciation`, se mantiene para la compatibilidad con versiones anteriores).
-   `supported_features` describe las características de servicio adicionales que admite la voz:
    -   `voice_transformation` es un valor booleano que indica si la voz se puede transformar mediante el uso del elemento SSML `<voice-transformation>`.
    -   `custom_pronunciation` es un valor booleano que indica si la voz se puede personalizar con la interfaz de personalización del servicio.

## Listar una voz específica
{: #listVoice}

El método `GET /v1/voices/{voice}` muestra información sobre una voz específica. Acepta dos parámetros.

<table>
  <caption>Tabla 2. Parámetros del método <code>voices</code></caption>
  <tr>
    <th style="text-align:left; width:18%">Parámetro</th>
    <th style="text-align:center; width:12%">Tipo</th>
    <th style="text-align:center; width:12%">Tipo de datos</th>
    <th style="text-align:left">Descripción</th>
  </tr>
  <tr>
    <td><code>voice</code><br/><em>Obligatorio</em></td>
    <td style="text-align:center">Vía de acceso</td>
    <td style="text-align:center">Serie</td>
    <td>
      Identifica la voz para la que se debe devolver información. Para especificar una voz se utiliza su nombre (por ejemplo, <code>en-US_LisaVoice</code>).
    </td>
  </tr>
  <tr>
    <td><code>customization_id</code><br/><em>Opcional</em></td>
    <td style="text-align:center">Consulta</td>
    <td style="text-align:center">Serie</td>
    <td>
      Proporciona el identificador exclusivo global (GUID) de un modelo de voz personalizado que se ha definido para el idioma de la voz especificada. Si incluye un ID de personalización, debe realizar la solicitud con las credenciales para la instancia del servicio que posee el modelo personalizado.
    </td>
  </tr>
</table>

Si omite el parámetro `customization_id`, el método devuelve la salida JSON de la voz especificada que es idéntica a la información devuelta para una voz por el método `GET /v1/voices`. Si especifica un `customization_id`, la salida incluye un campo `customization` que proporciona información acerca del modelo de voz personalizado especificado.

```javascript
{
  "name": "en-US_LisaVoice",
  "language": "en-US",
  "gender": "female",
  "url": "https://stream.watsonplatform.net/text-to-speech/api/v1/voices/en-US_LisaVoice",
  "description": "Lisa: American English female voice.",
  "customizable": true,
  "supported_features": {
    "voice_transformation": true,
    "custom_pronunciation": true
  },
  "customization": {
    "customization_id": "64f4807f-a5f1-5867-924f-7bba1a84fe97",
    "owner": "297cfd08-330a-22ba-93ce-1a73f454dd98",
    "created": "2017-09-16T17:12:31.743Z",
    "name": "curl Test",
    "language": "en-US",
    "description": "Customization test via curl",
    "last_modified": "2017-09-16T17:12:31.743Z"
  }
}
```
{: codeblock}

Los atributos del campo adicional `customization` proporcionan información como, por ejemplo, el GUID, el nombre, el idioma y la descripción del modelo de voz personalizado. También muestran las credenciales del propietario del modelo, la fecha y la hora en la que se ha creado el modelo y la fecha y la hora de su última modificación.
