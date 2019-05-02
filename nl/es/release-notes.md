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

# Notas del release
{: #release-notes}

En las secciones siguientes se documentan las nuevas características y los cambios que se han incluido para cada release y actualización del servicio {{site.data.keyword.texttospeechfull}}. En esta información se incluyen las limitaciones conocidas. A menos que se indique lo contrario, todos los cambios son compatibles con releases anteriores y se encuentran disponibles de forma automática y transparente para todas las aplicaciones nuevas y existentes.
{: shortdesc}

## Limitaciones conocidas
{: #limitations}

Un problema con el despliegue de las voces DNN (Deep Neural Network) `V2` causa ruido de fondo en el habla sintetizada. {{site.data.keyword.IBM_notm}} está trabajando para solucionar el problema.

## 24 de marzo de 2019
{: #March2019c}

-   El servicio ahora ofrece versiones DNN (Deep Neural Network) de las voces en alemán:
    -   `de-DE_BirgitV2Voice`
    -   `de-DE_DieterV2Voice`

    Para obtener más información sobre las voces basadas en DNN, consulte [Tecnologías de síntesis de voz](/docs/services/text-to-speech/voices.html#technologiesVoices).
-   Todas las voces basadas en DNN del servicio ahora admiten los atributos `pitch` y `rate` del elemento SSML `<prosody>`. Las voces basadas en DNN del servicio no admiten el atributo `volume` del elemento `<prosody>`. Para obtener más información, consulte [Elemento prosody](/docs/services/text-to-speech/SSML-elements.html#prosody_element).

## 21 de marzo de 2019
{: #March2019b}

Ahora los usuarios sólo pueden ver la información de credenciales de servicio que está asociada al rol que se ha asignado a su cuenta de {{site.data.keyword.cloud_notm}}. Por ejemplo, si se le asigna un rol de `lector`, las credenciales de servicio de `escritor` o de otros niveles superiores ya no son visibles.

Este cambio no afecta al acceso de API para usuarios o aplicaciones con credenciales de servicio existentes. El cambio sólo afecta a la visualización de credenciales dentro de {{site.data.keyword.cloud_notm}}.

Para obtener más información sobre claves de servicio y roles de usuario, consulte [Claves de API de servicio de IAM](/docs/services/watson?topic=watson-api-key-bp#api-key-bp).

## 4 de marzo de 2019
{: #March2019a}

El servicio ahora ofrece cuatro nuevas voces que utilizan la síntesis de aprendizaje profundo para generar audio:

-   `it-IT_FrancescaV2Voice`
-   `en-US_AllisonV2Voice`
-   `en-US_LisaV2Voice`
-   `en-US_MichaelV2Voice`

Estas nuevas voces utilizan el aprendizaje automático y un DNN para sintetizar texto a voz. La síntesis de aprendizaje profundo o basada en DNN genera audio con una prosodia más natural y una calidad general más coherente.

Pero las nuevas voces también producen audio con diferentes calidades de señal a partir de las voces existentes, por lo que podrían no ser apropiadas para todas las aplicaciones. Además, las nuevas voces no admiten los elementos SSML `<prosody>`, `<express-as>` y `<voice-transformation>`.

Para obtener más información sobre estas voces basadas en DNN y sobre cómo difieren de las voces existentes, consulte [Tecnologías de síntesis de voz](/docs/services/text-to-speech/voices.html#technologiesVoices).

## Releases anteriores
{: #older}

-   [28 de enero de 2019](#January2019)
-   [13 de diciembre de 2018](#December2018)
-   [7 de noviembre de 2018](#November2018)
-   [30 de octubre de 2018](#October2018)
-   [12 de junio de 2018](#June2018)
-   [15 de mayo de 2018](#May2018)
-   [2 de octubre de 2017](#October2017)
-   [14 de julio de 2017](#July2017)
-   [10 de abril de 2017](#April2017)
-   [1 de diciembre de 2016](#December2016)
-   [22 de septiembre de 2016](/docs/services/text-to-speech/release-notes.html#September2016)
-   [23 de junio de 2016](/docs/services/text-to-speech/release-notes.html#June2016)
-   [10 de marzo de 2016](/docs/services/text-to-speech/release-notes.html#March2016)
-   [22 de febrero de 2016](/docs/services/text-to-speech/release-notes.html#February2016)
-   [17 de diciembre de 2015](/docs/services/text-to-speech/release-notes.html#December2015)
-   [21 de septiembre de 2015](/docs/services/text-to-speech/release-notes.html#September2015)
-   [1 de julio de 2015](/docs/services/text-to-speech/release-notes.html#July2015)

### 28 de enero de 2019
{: #January2019}

La interfaz WebSocket ahora admite la autenticación de IAM (Identity and Access Management) basada en señales (IAM) a partir de código JavaScript basado en navegador. Se ha eliminado la limitación de lo contrario. Para establecer una conexión autenticada con el método WebSocket `/v1/synthesize`:

-   Si utiliza la autenticación de IAM, incluya el parámetro de consulta `access_token`.
-   Si utiliza las credenciales de servicio de Cloud Foundry, incluya el parámetro de consulta `watson-token`.

Para obtener más información, consulte [Abrir una conexión](/docs/services/text-to-speech/websockets.html#WSopen).

### 13 de diciembre de 2018
{: #December2018}

El servicio {{site.data.keyword.texttospeechshort}} está ahora disponible en la ubicación de Londres (**eu-gb**) de {{site.data.keyword.cloud}}. Al igual que todas las ubicaciones, Londres utiliza la autenticación de IAM (Identity and Access Management) basada en señales. Todas las nuevas instancias de servicios que se crean en esta ubicación utilizan la autenticación de IAM.

### 7 de noviembre de 2018
{: #November2018}

El servicio {{site.data.keyword.texttospeechshort}} está ahora disponible en la ubicación de Tokio (**jp-tok**) de {{site.data.keyword.cloud}}. Al igual que todas las ubicaciones, Tokio utiliza la autenticación de IAM (Identity and Access Management) basada en señales. Todas las nuevas instancias de servicios que se crean en esta ubicación utilizan la autenticación de IAM.

### 30 de octubre de 2018
{: #October2018}

El servicio {{site.data.keyword.texttospeechshort}} se ha migrado a la autenticación de IAM (Identity and Access Management) basada en señales para todas las ubicaciones. Ahora, todos los servicios de {{site.data.keyword.cloud_notm}} utilizan la autenticación de IAM. El servicio {{site.data.keyword.texttospeechshort}} se ha migrado en cada ubicación en las fechas siguientes:

-   Dallas (**us-south**): 30 de octubre de 2018
-   Frankfurt (**eu-de**): 30 de octubre de 2018
-   Washington, DC (**us-east**): 12 de junio de 2018
-   Sídney (**au-syd**): 15 de mayo de 2018

La migración a la autenticación de IAM afecta de forma distinta a las instancias de servicio nuevas y existentes:

-   *Todas las instancias de servicio nuevas que se crean en cualquier ubicación* ahora utilizan la autenticación de IAM para acceder al servicio. Puede pasar una señal portadora o una clave de API: las señales admiten solicitudes autenticadas sin incluir credenciales de servicio en cada llamada; las claves de API utilizan la autenticación básica HTTP. Cuando se utiliza cualquier SDK de {{site.data.keyword.ibmwatson}}, se puede pasar la clave de API y dejar que SDK gestione el ciclo de vida de las señales.
-   *Las instancias de servicio existentes que ha creado en una ubicación antes de la fecha de migración indicada* siguen utilizando el `{username}` y la `{password}` de sus credenciales de servicio de Cloud Foundry para la autenticación hasta que las migre para que utilicen la autenticación de IAM. Para obtener más información sobre la migración a la autenticación de IAM, consulte [Migración de instancias de servicio de Cloud Foundry a un grupo de recursos](https://{DomainName}/docs/resources/instance_migration.html).

Para obtener más información, consulte la documentación siguiente:

-   Para saber qué mecanismo de autenticación utiliza la instancia de servicio, consulte las credenciales de servicio pulsando la instancia en el [panel de control de {{site.data.keyword.cloud_notm}} ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://{DomainName}/dashboard/apps){: new_window}.
-   Para obtener más información sobre el uso de las señales IAM con los servicios de {{site.data.keyword.watson}}, consulte [Autenticación con señales IAM](/docs/services/watson/getting-started-iam.html).
-   Para obtener más información sobre el uso de las claves de API de IAM con los servicios de {{site.data.keyword.watson}}, consulte [Claves de API de servicio de IAM](/docs/services/watson/apikey-bp.html).
-   Para obtener ejemplos que utilicen la autenticación de IAM, consulte la publicación [Referencia de la API ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://{DomainName}/apidocs/text-to-speech){: new_window}.

### 12 de junio de 2018
{: #June2018}

Hay las siguientes características habilitadas para las aplicaciones alojadas en Washington, DC (**us-east**):

-   El servicio ahora admite un nuevo proceso de autenticación de API. Para obtener más información, consulte la [actualización de servicio del 30 de octubre de 2018](#October2018).
-   El servicio ahora admite la cabecera `X-Watson-Metadata` y el método `DELETE /v1/user_data`. Para obtener más información, consulte [Seguridad de la información](/docs/services/text-to-speech/information-security.html).

### 15 de mayo de 2018
{: #May2018}

Hay las siguientes características habilitadas para las aplicaciones alojadas en Sídney (**au-syd**):

-   El servicio ahora admite un nuevo proceso de autenticación de API. Para obtener más información, consulte la [actualización de servicio del 30 de octubre de 2018](#October2018).
-   El servicio ahora admite la cabecera `X-Watson-Metadata` y el método `DELETE /v1/user_data`. Para obtener más información, consulte [Seguridad de la información](/docs/services/text-to-speech/information-security.html).

### 2 de octubre de 2017
{: #October2017}

Para el formato `audio/l16`, ahora tiene la opción de especificar la endianness del audio que se devuelve. (Debe especificar a la frecuencia de muestreo). Por ejemplo: `audio/l16;rate=22050;endianness=big-endian` y `audio/l16;rate=22050;endianness=little-endian`; el valor predeterminado es big endian. Para obtener más información, consulte [Formatos de audio](/docs/services/text-to-speech/audio-formats.html).

### 14 de julio de 2017
{: #July2017}

El servicio ahora admite el formato de audio MP3 o MPEG (Motion Picture Experts Group). Para obtener más información sobre los formatos de audio soportados, consulte [Formatos de audio](/docs/services/text-to-speech/audio-formats.html).

### 10 de abril de 2017
{: #April2017}

-   El servicio ahora admite el formato de audio WebM (Web Media) con el códec Opus o Vorbis. El servicio ahora también admite el formato de audio Ogg con el códec Vorbis además del códec Opus. Para obtener más información sobre los formatos de audio soportados, consulte [Formatos de audio](/docs/services/text-to-speech/audio-formats.html).
-   El servicio ahora admite CORS (Cross-Origin Resource Sharing) para permitir que los clientes basados en navegador llamen al servicio directamente. Para obtener más información, consulte [Soporte de CORS](/docs/services/text-to-speech/developer-overview.html#cors).
-   Los códigos de respuesta HTTP para la finalización satisfactoria de algunos métodos de la interfaz de personalización han cambiado:
    -   El método `POST /v1/customizations` ahora devuelve 201 (en lugar de 200).
    -   El método `POST /v1/customizations/{customization_id}` ahora devuelve 200 (en lugar de 201).
    -   El método `POST /v1/customizations/{customization_id}/words` ahora devuelve 200 (en lugar de 201).
    -   El método `PUT /v1/customizations/{customization_id}/words/{word}` ahora devuelve 200 (en lugar de 201).
-   Los métodos `POST /v1/customizations/{custom_id}/words` y `PUT /v1/customizations/{customization_id}/words/{word}` ahora devuelven el código de respuesta HTTP 400 con el mensaje de error `Part of speech is supported for ja-JP language only` si se intenta especificar `part_of_speech` para un idioma distinto del japonés.
-   El método `POST /v1/customizations/{custom_id}/words` ahora devuelve un cuerpo de respuesta vacío (`{}`).

### 1 de diciembre de 2016
{: #December2016}

-   El servicio incluye una nueva voz, `es-LA_SofiaVoice`, que es el equivalente latinoamericano de la voz de `es-US_SofiaVoice`. La diferencia más significativa entre las dos voces es la forma en que interpretan un `$` (signo de dólar): la versión latinoamericana utiliza el término *pesos*, mientras que la versión norteamericana utiliza el término *dólares*. También puede haber otras diferencias menores entre las dos voces.
-   Además de la voz `en-US_AllisonVoice`, ahora hay dos voces más transformables con el SSML de transformación de voz: `en-US_LisaVoice` y `en-US_MichaelVoice`. Para obtener más información sobre la transformación de voz, consulte [SSML de transformación de voz](/docs/services/text-to-speech/SSML-transformation.html).
-   Cuando se utiliza la interfaz de personalización con japonés, el servicio ahora elige la palabra más larga de los pares palabra/conversión definidos para un modelo de voz personalizado. Por ejemplo, imaginemos que hay las dos entradas siguientes para una voz personalizada:

    <pre><code data-copy="false" class="language-javascript">  {
      "words": [
        {"word":"&#65326;&#65337;", "translation":"&#12491;&#12517;&#12540;&#12520;&#12540;&#12463;", "part_of_speech":"Mesi"},
        {"word":"&#65326;&#65337;&#65315;", "translation":"&#12491;&#12517;&#12540;&#12520;&#12540;&#12463;&#12471;&#12486;&#12451;", "part_of_speech":"Mesi"}
      ]
    }</code></pre>

    Si el servicio encuentra la serie <code>&#65326;&#65337;&#65315;</code> en el texto de entrada, elige esa palabra porque es una coincidencia más larga que <code>&#65326;&#65337;</code>. Anteriormente, el servicio habría elegido la serie <code>&#65326;&#65337;</code>. Para obtener más información sobre cómo trabajar con entradas en japonés para un modelo de voz personalizado, consulte [Trabajar con entradas en japonés](/docs/services/text-to-speech/custom-rules.html#jaNotes).

### 22 de septiembre de 2016
{: #September2016}

-   La interfaz de personalización, que incluye los métodos de personalización y `GET /v1/pronunciation`, está ahora disponible para todos los idiomas que admite el servicio. La interfaz sigue siendo un release beta. Para obtener más información, consulte [Comprender la personalización](/docs/services/text-to-speech/custom-intro.html).
-   El servicio ahora admite SSML (Speech Synthesis Markup Language) para japonés. Para obtener información general sobre el soporte de SSML, consulte [Utilización de SSML](/docs/services/text-to-speech/SSML.html). Para obtener información sobre los símbolos SPR e IPA japoneses, consulte [Símbolos para el japonés](/docs/services/text-to-speech/ja-JP-SPRs.html). Se aplican consideraciones adicionales y también un campo de más `part_of_speech` al crear entradas de palabras en un modelo de voz personalizado en japonés. Para obtener más información, consulte [Trabajar con entradas en japonés](/docs/services/text-to-speech/custom-rules.html#jaNotes).
-   El servicio ahora ofrece transformación de voz SSML a través del nuevo elemento `<voice-transformation>`. Puede ampliar la gama de voces posibles creando transformaciones de voz personalizadas que modifican el tono, el rango de tono, la tensión glotal, la respiración, la velocidad y el timbre de una voz. El servicio también ofrece dos voces virtuales integradas, *Young* y *Soft*. El servicio actualmente da soporte a la transformación de voz sólo para la voz de Allison en inglés de Estados Unidos. Para obtener más información, consulte [SSML de transformación de voz](/docs/services/text-to-speech/SSML-transformation.html).
-   Ahora el servicio puede devolver información de temporización de palabras para todas las series del texto de entrada que pase a la interfaz WebSocket. Para recibir la hora de inicio y finalización de cada serie de caracteres de la entrada, especifique una matriz que incluya la serie `words` para el parámetro opcional `timings` del objeto JSON que pase al servicio. Esta característica no está disponible actualmente para texto de entrada en japonés. Para obtener más información, consulte [Obtener temporizaciones de palabras](/docs/services/text-to-speech/word-timing.html).
-   El servicio ahora valida todos los elementos SSML que se envían en cualquier contexto. Si encuentra una etiqueta no válida, el servicio notifica un código de respuesta HTTP 400 con un mensaje descriptivo, y el método falla. En releases anteriores, el servicio manejaba errores de forma incoherente; especificar una pronunciación de palabra no válida, por ejemplo, podía provocar un comportamiento imprevisible o incoherente. Para obtener más información, consulte [Validación de SSML](/docs/services/text-to-speech/SSML.html#errors).
-   El uso de `spr` queda en desuso como argumento de la opción `format` del método `GET /v1/pronunciation` así como para su uso con el atributo `alphabet` de un elemento SSML `<phoneme>`. Para utilizar la notación {{site.data.keyword.IBM_notm}} SPR (Symbolic Phonetic Representation), utilice el argumento `ibm` en lugar `spr` en todos los casos.
-   En la lista de formatos de audio admitidos ahora se incluye `audio/mulaw;rate=8000`. Al igual que `audio/basic`, este formato proporciona audio de un solo canal que se codifica utilizando datos u-law (o mu-law) de 8 bits que se muestrean a 8 kHz. Para obtener más información, consulte [Formatos de audio](/docs/services/text-to-speech/audio-formats.html).
-   Los métodos `GET /v1/voices` y `GET /v1/voices/{voice}` ahora devuelven un objeto `supported_features` como parte de su salida para cada voz. El objeto describe si la voz admite personalización y el elemento SSML `<voice_transformation>`. Para obtener más información, consulte [Idiomas y voces](/docs/services/text-to-speech/voices.html).

### 23 de junio de 2016
{: #June2016}

-   El servicio ahora ofrece una interfaz WebSocket para sintetizar texto a voz. La interfaz ofrece las mismas características que el método `/v1/synthesize` de la interfaz HTTP. Acepta texto sin formato o texto con marcaje SSML. Además, también admite el uso del elemento SSML `<mark>` para identificar la hora en que termina de sintetizar todo el texto que precede a la marca. Para obtener más información, consulte [La interfaz WebSocket](/docs/services/text-to-speech/websockets.html).
-   El servicio ahora ofrece soporte para texto anotado con SSML para los idiomas español de España y de América del Norte, italiano y portugués de Brasil. El servicio ya admitía el uso de SSML para inglés británico y de EE.UU., francés y alemán. A partir de esta actualización, el servicio admite SSML para todos los idiomas excepto el japonés. Además, puede utilizar tanto la notación SPR como la notación IPA de {{site.data.keyword.IBM_notm}} para definir pronunciaciones de palabras con el elemento SSML `<phoneme>`. Para obtener más información, consulte [Utilización de SSML](/docs/services/text-to-speech/SSML.html) y [Utilización de IBM SPR](/docs/services/text-to-speech/SPRs.html).

    Para inglés de Estados Unidos, también puede utilizar el elemento SSML `<phoneme>` para crear entradas de palabras en un modelo de voz personalizado; solo se admite la personalización para el inglés de Estados Unidos. Para obtener más información, consulte [Comprender la personalización](/docs/services/text-to-speech/custom-intro.html).
-   El servicio ha mejorado la expresividad y la naturalidad de las voces más utilizadas. Estas mejoras se basan en la predicción de prosodia basada en RNN (Recursive Neural Network) a partir del texto de entrada. Están disponibles como un nuevo motor de servicio y actualizaciones de modelos de voz para los idiomas siguientes:

    -   `en-US_AllisonVoice`
    -   `en-US_LisaVoice`
    -   `en-US_MichaelVoice`
    -   `es-ES_EnriqueVoice`
    -   `fr-FR_ReneeVoice`
-   El método `GET /v1/pronunciation` ahora acepta un parámetro de consulta opcional `customization_id`. Este parámetro obtiene una conversión de palabras a partir de un modelo de voz personalizado especificado. Si el modelo de voz no contiene la palabra, el método devuelve la pronunciación predeterminada de la palabra. Para obtener más información, consulte la [Referencia de API ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://{DomainName}/apidocs/text-to-speech){: new_window}.

    Al utilizar el método `GET /v1/pronunciation` sin un ID de personalización y para un idioma distinto del inglés de EE.UU., puede solicitar la pronunciación de una palabra sólo en la notación {{site.data.keyword.IBM_notm}} SPR. Para un idioma distinto del inglés de EE.UU., debe especificar `spr` con la opción `format` del método.
    {: note}
-   La lista de formatos de audio admitidos incluye ahora `audio/basic`, que proporciona un audio de un solo canal que se codifica utilizando datos u-law (o mu-law) de 8 bits que se muestrean a 8 kHz. Para obtener más información, consulte [Formatos de audio](/docs/services/text-to-speech/audio-formats.html).
-   Los métodos HTTP y WebSocket `/v1/synthesize` pueden devolver una respuesta de `warnings` que incluye mensajes sobre parámetros de consulta no válidos o campos JSON que se incluyen en una solicitud. El formato de los avisos ha cambiado. En el ejemplo siguiente se muestra el formato anterior:

    `"warnings": "Unknown arguments: [u'{invalid_arg_1}', u'{invalid_arg_2}']."`

    Ahora, el mismo aviso tiene el formato siguiente:

    `"warnings": "Unknown arguments: {invalid_arg_1}, {invalid_arg_2}."`

### 10 de marzo de 2016
{: #March2016}

-   Los métodos `GET` y `POST /v1/synthesize` ahora pueden devolver una cabecera de respuesta `Warnings` que incluye una lista de mensajes de aviso acerca de parámetros de consulta no válidos o campos JSON que se incluyen en la solicitud. Cada elemento de la lista incluye una serie de caracteres que describe la naturaleza del aviso seguido de una matriz de series de argumentos no válidos; por ejemplo, `Unknown arguments: [u'{invalid_arg_1}', u'{invalid_arg_2}'].` Para obtener más información, consulte la [Referencia de API ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://{DomainName}/apidocs/text-to-speech){: new_window}.
-   La versión beta de *{{site.data.keyword.watson}} Speech Software Development Kit (SDK) para el sistema operativo Apple&reg; iOS* ha quedado en desuso y se ha sustituido por *{{site.data.keyword.watson}} Swift SDK*. El nuevo SDK está disponible en el [repositorio swift-sdk ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://github.com/watson-developer-cloud/swift-sdk){: new_window} del espacio de nombres `watson-developer-cloud` en GitHub.

### 22 de febrero de 2016
{: #February2016}

El servicio se ha actualizado con una nueva característica de expresión de SSML. El servicio amplía el lenguaje SSML (Speech Synthesis Markup Language) con un elemento `<express-as>` que se puede utilizar para indicar la expresividad en tres estilos de habla: `GoodNews`, `Apology` o `Uncertainty`. Puede aplicar el elemento a todo el cuerpo del texto, a una frase o a una palabra. Actualmente, el servicio da soporte a la expresividad sólo para la voz de Allison en inglés de EE.UU. (`en-US_AllisonVoice`). Para obtener más información, consulte [SSML expresivo](/docs/services/text-to-speech/SSML-expressive.html).

### 17 de diciembre de 2015
{: #December2015}

-   El servicio ofrece una nueva interfaz de personalización que se puede utilizar para especificar cómo se pronuncian las palabras inusuales que aparecen en la entrada. La interfaz incluye diversos nuevos métodos que se pueden utilizar para crear y gestionar modelos de voz personalizados y los pares de palabras/conversión que contienen. Puede utilizar los modelos personalizados al sintetizar texto a audio.

    El servicio admite conversiones de tipo 'suena como' y transcripciones fonéticas. Las transcripciones fonéticas pueden utilizar la representación estándar IPA (International Phonetic Alphabet) o la representación SPR (Symbolic Phonetic Representation), propiedad de {{site.data.keyword.IBM_notm}}. Se debe utilizar SSML (Speech Synthesis Markup Language) para especificar las transcripciones fonéticas.

    La interfaz de personalización incluye una colección de nuevos métodos HTTP denominados `POST /v1/customizations`, `POST /v1/customizations/{customization_id}`, `POST /v1/customizations/{customization_id}/words` y `PUT /v1/customizations/{customization_id}/words/{word}`. El servicio también proporciona el nuevo método `GET /v1/pronunciation` que devuelve la pronunciación de cualquier palabra y el nuevo método `GET /v1/voices/{voice}` que devuelve información detallada acerca de una voz específica. Además, los métodos existentes de la interfaz del servicio aceptan ahora los parámetros de modelo de voz personalizados según sea necesario.

    Para obtener más información sobre la personalización y su interfaz, consulte [Comprender la personalización](/docs/services/text-to-speech/custom-intro.html) y la [Referencia de API ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://{DomainName}/apidocs/text-to-speech){: new_window}.

    La interfaz de personalización es un release beta que actualmente sólo da soporte al inglés de Estados Unidos. Todos los métodos de personalización y el método `GET /v1/pronunciation` sólo se pueden utilizar actualmente para crear y manipular modelos de voz personalizados y traducciones de palabras en inglés de Estados Unidos.
    {: note}
-   El servicio admite una nueva voz, `pt-BR_IsabelaVoice`, para sintetizar audio en portugués de Brasil con una voz femenina. Para obtener más información, consulte [Idiomas y voces](/docs/services/text-to-speech/voices.html).

### 21 de septiembre de 2015
{: #September2015}

-   Hay dos nuevos SDK (Software Development Kits) beta para móviles disponibles para los servicios de voz. Estos SDK permiten a las aplicaciones móviles interaccionar con los servicios {{site.data.keyword.texttospeechshort}} y {{site.data.keyword.speechtotextshort}}. Puede utilizar los SDK para enviar texto al servicio {{site.data.keyword.texttospeechshort}} y recibir una respuesta de audio.
    -   *{{site.data.keyword.watson}} Swift SDK* está disponible en el [repositorio swift-sdk ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://github.com/watson-developer-cloud/swift-sdk){: new_window} en el espacio de nombres `watson-developer-cloud` en GitHub.
    -   *{{site.data.keyword.watson}} Speech Android SDK* está disponible en el [repositorio speech-android-sdk ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://github.com/watson-developer-cloud/speech-android-sdk){: new_window} en el espacio de nombres `watson-developer-cloud` en GitHub.

    Los dos SDK admiten la autenticación con servicios de voz utilizando las credenciales de servicio de {{site.data.keyword.cloud_notm}} o bien una señal de autenticación.

    Debido a que los SDK son funcionalidades beta, están sujetos a cambios en el futuro.
    {: note}
-   El servicio admite un nuevo idioma, el japonés. La voz `ja-JP_EmiVoice` es una voz japonesa femenina.

### 1 de julio de 2015
{: #July2015}

El servicio ha pasado de beta a disponibilidad general (GA - General Availability) el 1 de julio de 2015. Existen las siguientes diferencias entre las versiones beta y GA de la API de {{site.data.keyword.texttospeechshort}}. El release de GA requiere que los usuarios se actualicen a la nueva versión del servicio.

-   Un nuevo modelo de programación da soporte a la interacción directa entre un cliente y el servicio. Utilizando este modelo, un cliente puede obtener una señal de autenticación para comunicarse directamente con el servicio. Utilizando la señal, el cliente puede eludir la necesidad de una aplicación proxy del lado del servidor en {{site.data.keyword.cloud_notm}} para llamar al servicio en su nombre. Las señales son el medio preferido para que los clientes interactúen con el servicio.

    El servicio continúa admitiendo el modelo de programación antiguo que utilizaba un proxy del lado del servidor para retransmitir comunicaciones y datos entre el cliente y el servicio. Pero el nuevo modelo es más eficiente y proporciona un mayor rendimiento. Para obtener más información sobre el nuevo modelo de programación, consulte [Modelos de programación para los servicios de {{site.data.keyword.watson}}](/docs/services/watson/getting-started-develop.html).
-   Ahora, se puede pasar SSML (Speech Synthesis Markup Language) a las versiones HTTP `GET` y `POST` del método `/v1/synthesize`. SSML es un lenguaje de códigos basado en XML, diseñado para proporcionar anotaciones de texto para aplicaciones de síntesis de voz, como por ejemplo el servicio {{site.data.keyword.texttospeechshort}}. Para obtener más información sobre cómo pasar la entrada SSML al servicio, consulte [Especificar el texto de entrada](/docs/services/text-to-speech/http.html#input).

    Inicialmente, el servicio admite el uso de SSML sólo para los idiomas inglés británico y de EE.UU., francés y alemán. El servicio no admite SSML para italiano o español. Al utilizar SSML, asegúrese de que no seleccionar una voz para el audio en uno de los idiomas no soportados. Los resultados en tal caso no serían significativos.
-   Se ha cambiado y ampliado el número de voces soportadas para el habla sintetizada. El servicio ahora admite varias voces más, así como nuevos idiomas y dialectos, con los métodos `/v1/synthesize`. Para obtener más información sobre las voces soportadas, consulte [Idiomas y voces](/docs/services/text-to-speech/voices.html).

    Las tres voces que había disponibles en beta se han renombrado para GA:
    -   `VoiceEnUsMichael` es ahora `en-US_MichaelVoice`
    -   `VoiceEnUsLisa` es ahora `en-US_LisaVoice`
    -   `VoiceEsEsEnrique` es ahora `es-ES_EnriqueVoice`

    Los nombres anteriores de las voces seguirán funcionando con la versión beta del servicio (a través de los puntos finales de la API `-beta`) mientras esa versión siga disponible. Sin embargo, debe utilizar los nuevos nombres con la versión GA del servicio.
-   Ahora puede solicitar al servicio que devuelva el audio en formato FLAC (Free Lossless Audio). El servicio todavía puede devolver el audio en formato Ogg con el códec Opus (el predeterminado) y en formato WAV (Waveform Audio File Format). Para obtener más información sobre el uso de los formatos de audio con los métodos `/v1/synthesize`, consulte [Formatos de audio](/docs/services/text-to-speech/audio-formats.html).
-   El texto que se envía al método `/v1/synthesize` en el URL de una solicitud HTTP `GET` o en el cuerpo de una solicitud HTTP `POST` está ahora limitado a un máximo de 5 KB. En la versión beta, el texto tenía un tamaño máximo de 4 MB.
-   Los métodos `/v1/synthesize` ahora incluyen la cabecera `X-WDC-PL-OPT-OUT` para controlar si el servicio utiliza los resultados de texto y audio de una operación para mejorar los resultados futuros. Especifique el valor `1` para impedir que el servicio utilice los resultados de texto y de audio. El parámetro se aplica sólo a la solicitud actual. La nueva cabecera sustituye a la cabecera `X-logging` de los métodos beta. Para obtener más información, consulte [Control del registro de solicitud para servicios de {{site.data.keyword.watson}}](/docs/services/watson/getting-started-logging.html).
-   Para los métodos `/v1/synthesize`, se han modificado los siguientes códigos de error:
    -   Se ha eliminado el código de error 406 ("No aceptable. Tipo MIME no soportado.") .
    -   Se ha añadido el código de error 415 ("Tipo de soporte no soportado").
    -   Se ha añadido el código de error 503 ("Servicio no disponible").
-   Para el método `GET /v1/voices`, se han modificado los códigos de error siguientes:
    -   Se ha eliminado el código de error 406 ("No aceptable. Tipo MIME no soportado.") .
    -   Se ha añadido el código de error 415 ("Tipo de soporte no soportado").
