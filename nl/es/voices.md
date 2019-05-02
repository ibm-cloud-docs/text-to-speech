---

copyright:
  years: 2015, 2019
lastupdated: "2019-03-28"

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

# Idiomas y voces
{: #voices}

El servicio {{site.data.keyword.texttospeechfull}} da soporte a una variedad de idiomas, voces y dialectos. El servicio ofrece al menos una voz masculina o femenina, a veces ambas, por cada idioma. Cada voz utiliza la cadencia y la entonación adecuadas según su dialecto.
{: shortdesc}

## Idiomas y voces soportados
{: #languageVoices}

En la tabla 1 se listan las voces disponibles para cada idioma y dialecto, indicando también el género. Si se omite el parámetro opcional `voice` en una solicitud, el servicio utiliza de forma predeterminada la voz `en-US_MichaelVoice`. Para saber por qué el servicio ofrece dos versiones de algunas voces, consulte [Tecnologías de síntesis de voz](#technologiesVoices).

Un problema con el despliegue de las voces `V2` actualmente causa ruido de fondo en el habla sintetizada. Para obtener más información, consulte [Limitaciones conocidas](/docs/services/text-to-speech/release-notes.html#limitations).
{: note}

<table style="width:90%">
  <caption>Tabla 1. Idiomas y voces soportados</caption>
  <tr>
    <th style="text-align:left">Idioma</th>
    <th style="text-align:center">Voz</th>
    <th style="text-align:center">Género</th>
  </tr>
  <tr>
    <td style="text-align:left">Portugués de Brasil</td>
    <td style="text-align:center"><code>pt-BR_IsabelaVoice</code></td>
    <td style="text-align:center">Femenino</td>
  </tr>
  <tr>
    <td style="text-align:left">Español de España</td>
    <td style="text-align:center"><code>es-ES_EnriqueVoice</code></td>
    <td style="text-align:center">Masculino</td>
  </tr>
  <tr>
    <td></td>
    <td style="text-align:center"><code>es-ES_LauraVoice</code></td>
    <td style="text-align:center">Femenino</td>
  </tr>
  <tr>
    <td style="text-align:left">Francés</td>
    <td style="text-align:center"><code>fr-FR_ReneeVoice</code></td>
    <td style="text-align:center">Femenino</td>
  </tr>
  <tr>
    <td style="text-align:left">Alemán</td>
    <td style="text-align:center"><code>de-DE_BirgitVoice</code><br/>
      <code>de-DE_BirgitV2Voice</code></td>
    <td style="text-align:center">Femenino</td>
  </tr>
  <tr>
    <td></td>
    <td style="text-align:center"><code>de-DE_DieterVoice</code><br/>
      <code>de-DE_DieterV2Voice</code></td>
    <td style="text-align:center">Masculino</td>
  </tr>
  <tr>
    <td style="text-align:left">Italiano</td>
    <td style="text-align:center"><code>it-IT_FrancescaVoice</code><br/>
      <code>it-IT_FrancescaV2Voice</code></td>
    <td style="text-align:center">Femenino</td>
  </tr>
  <tr>
    <td style="text-align:left">Japonés</td>
    <td style="text-align:center"><code>ja-JP_EmiVoice</code></td>
    <td style="text-align:center">Femenino</td>
  </tr>
  <tr>
    <td style="text-align:left">Español de América Latina</td>
    <td style="text-align:center"><code>es-LA_SofiaVoice</code></td>
    <td style="text-align:center">Femenino</td>
  </tr>
  <tr>
    <td style="text-align:left">Español de América del Norte</td>
    <td style="text-align:center"><code>es-US_SofiaVoice</code></td>
    <td style="text-align:center">Femenino</td>
  </tr>
  <tr>
    <td style="text-align:left">Inglés del Reino Unido</td>
    <td style="text-align:center"><code>en-GB_KateVoice</code></td>
    <td style="text-align:center">Femenino</td>
  </tr>
  <tr>
    <td style="text-align:left">Inglés de EE.UU.</td>
    <td style="text-align:center"><code>en-US_AllisonVoice</code><br/>
      <code>en-US_AllisonV2Voice</code></td>
    <td style="text-align:center">Femenino</td>
  </tr>
  <tr>
    <td></td>
    <td style="text-align:center"><code>en-US_LisaVoice</code><br/>
      <code>en-US_LisaV2Voice</code></td>
    <td style="text-align:center">Femenino</td>
  </tr>
  <tr>
    <td></td>
    <td style="text-align:center"><code>en-US_MichaelVoice</code><br/>
      <code>en-US_MichaelV2Voice</code></td>
    <td style="text-align:center">Masculino</td>
  </tr>
</table>

Las voces `es-LA_SofiaVoice` y `es-US_SofiaVoice` son esencialmente la misma voz. La diferencia más significativa se refiere a cómo las dos voces interpretan el signo de dólar ($). La versión latinoamericana utiliza el término *pesos*, mientras que la versión norteamericana utiliza el término *d&oacute;lares*. También puede haber otras diferencias menores entre las dos voces.
{: note}

### Tecnologías de síntesis de voz
{: #technologiesVoices}

El servicio ofrece dos versiones de algunas voces, por ejemplo, `en-US_AllisonVoice` y `en-US_AllisonV2Voice`. La diferencia principal entre las dos versiones refleja la tecnología que el servicio utiliza para sintetizar el habla:

-   La *Síntesis concatenativa* ensambla segmentos (o unidades) de voz grabada para generar el audio solicitado. Genera audio que puede ser considerado como un sonido más crítico, pero los puntos de concatenación de los segmentos grabados a veces resultan en distorsiones del habla.

    Las voces que no incluyen la serie `V2` en el nombre (por ejemplo, `en-US_AllisonVoice`) están basados en síntesis concatenativa.
-   La *Síntesis de aprendizaje profundo* utiliza una red neuronal profunda (DNN - Deep Neural Network) para sintetizar el habla correspondiente al texto especificado. En lugar de concatenar segmentos grabados de audio, este método utiliza aprendizaje automático para entrenar una DNN con datos de habla grabados. La síntesis de aprendizaje profundo o basada en DNN genera audio con una prosodia más natural y una calidad general más coherente.

    Las voces que incluyen la serie `V2` en el nombre (por ejemplo, `en-US_AllisonV2Voice`) son voces más nuevas que utilizan síntesis basada en DNN.

Tiene que experimentar con las nuevas voces antes de adoptarlas para su aplicación. Las dos tecnologías producen audio con diferentes calidades de señal, así que podría ser que las nuevas voces no fueran mejores para todas las aplicaciones. Además, las voces basadas en DNN no admiten los siguientes elementos o atributos SSML:

-   El atributo `volume` del elemento `<prosody>`
-   El elemento `<express-as>`
-   El elemento `<voice-transformation>`

Si su aplicación utiliza estos elementos, siga utilizando las voces basadas en síntesis concatenativa.

### Personalización de voces
{: #customizeVoice}

Al sintetizar texto, el servicio aplica reglas de pronunciación dependientes del idioma para convertir la ortografía ordinaria de cada palabra en una ortografía fonética. Las reglas de pronunciación del servicio funcionan bien para las palabras comunes, pero pueden producir resultados imperfectos para palabras inusuales, tales como vocablos extranjeros, nombres personales y abreviaturas o acrónimos.

Si el léxico de la aplicación incluye palabras de este tipo, puede utilizar la interfaz de personalización para especificar cómo los pronuncia el servicio. Para obtener más información, consulte [Comprender la personalización](/docs/services/text-to-speech/custom-intro.html).

## Especificar una voz
{: #specifyVoice}

Tanto los métodos HTTP `GET` y `POST /v1/synthesize`, como el método WebSocket `/v1/synthesize`, aceptan un parámetro de consulta opcional `voice` para especificar la voz del audio sintetizado. Para obtener más información, consulte [La interfaz HTTP](/docs/services/text-to-speech/http.html) y [La interfaz WebSocket](/docs/services/text-to-speech/websockets.html).

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
      Identifica la voz para la que se debe devolver información. Para especificar una voz
      se utiliza su nombre (por ejemplo, <code>en-US_LisaVoice</code>).
    </td>
  </tr>
  <tr>
    <td><code>customization_id</code><br/><em>Opcional</em></td>
    <td style="text-align:center">Consulta</td>
    <td style="text-align:center">Serie</td>
    <td>
      Proporciona el identificador exclusivo global (GUID) de un modelo de
      voz personalizado que se ha definido para la voz especificada. Si incluye
      un ID de personalización, debe llamar al método con las credenciales
      de servicio del propietario del modelo personalizado.
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

Los atributos del campo adicional `customization` proporcionan información como, por ejemplo, el GUID, el nombre, el idioma y la descripción del modelo de voz personalizado. También muestran las credenciales de servicio del propietario del modelo, la fecha y la hora en la que se ha creado el modelo y la fecha y la hora de su última modificación.
