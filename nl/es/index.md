---

copyright:
  years: 2015, 2019
lastupdated: "2019-07-30"

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

# Acerca de
{: #about}

> ** Actualización del servicio:** *El servicio {{site.data.keyword.texttospeechshort}} se ha actualizado el 30 de julio de 2019. El servicio da soporte ahora a una voz neuronal en japonés: `ja-JP_EmiV3Voice`. Para obtener más información, consulte la [Actualización del servicio de 30 de julio de 2019](/docs/services/text-to-speech?topic=text-to-speech-release-notes#July2019) en las Notas del release*.

El servicio {{site.data.keyword.texttospeechfull}} proporciona una API (interfaz de programación de aplicaciones) que utiliza las funciones de síntesis de voz de {{site.data.keyword.IBM_notm}} para convertir texto escrito en una voz que suene natural. El servicio transmite los resultados de vuelta al cliente con un retardo mínimo. El servicio ofrece interfaces [HTTP](/docs/services/text-to-speech?topic=text-to-speech-usingHTTP) y [WebSocket](/docs/services/text-to-speech?topic=text-to-speech-usingWebSocket).

## Características y funciones

El servicio {{site.data.keyword.texttospeechshort}} ofrece las características y funciones siguientes:

-   **Formatos de audio** - Produce audio en Ogg o WebM con el códec Opus o Vorbis, en formato WAV, FLAC, MP3 (MPEG), l16 (PCM), mulaw o el formato básico. Para obtener más información, consulte [Formatos de audio](/docs/services/text-to-speech?topic=text-to-speech-audioFormats).
-   **Voces** - Sintetiza texto a audio varios idiomas, voces y dialectos. El servicio ofrece las versiones estándar (concatenativa) y neuronal de la mayoría de voces. Para obtener más información, consulte [Idiomas y voces](/docs/services/text-to-speech?topic=text-to-speech-voices).
-   **SSML** - Acepta texto sin formato o texto anotado con el lenguaje SSML (Speech Synthesis Markup Language) basado en XML. Para obtener más información, consulte [Utilización de SSML](/docs/services/text-to-speech?topic=text-to-speech-ssml).
-   **Expresividad** - Se amplía SSML con un elemento de expresión que puede utilizar para indicar un estilo de habla: *GoodNews*, *Apology* o *Uncertainty*. Disponible únicamente para la voz estándar de Allison en inglés de EE.UU. Para obtener más información, consulte [SSML expresivo](/docs/services/text-to-speech?topic=text-to-speech-expressive).
-   **Transformación de voz** - Se amplía SSML añadiendo un elemento de transformación de voz. Puede utilizar el elemento para ampliar el rango de voces posibles controlando aspectos tales como el tono, la velocidad y el timbre. También se ofrecen dos voces virtuales integradas, *Young* y *Soft*. Disponible únicamente para las voces estándar en inglés de EE.UU. Para obtener más información, consulte [SSML de transformación de voz](/docs/services/text-to-speech?topic=text-to-speech-transformation).
-   **Temporizaciones de palabras** - Con la interfaz WebSocket, se admite el elemento SSML `<mark>` e información opcional de temporización de palabras para todas las series de caracteres del texto de entrada. La información de temporización sincroniza el texto de entrada y el audio resultante. Para obtener más información, consulte [Obtener temporizaciones de palabras](/docs/services/text-to-speech?topic=text-to-speech-timing).
-   **Personalización** - Se proporciona una interfaz de personalización que se puede utilizar para especificar cómo debe pronunciar el servicio las palabras inusuales que aparecen en la entrada. Puede definir la pronunciación con IPA (International Phonetic Alphabet) o con {{site.data.keyword.IBM_notm}} SPR (Symbolic Phonetic Representation). Para obtener más información, consulte [Comprender la personalización](/docs/services/text-to-speech?topic=text-to-speech-customIntro).

Para obtener más información sobre los planes de precios del servicio, consulte el servicio {{site.data.keyword.texttospeechshort}} en el [Catálogo de {{site.data.keyword.cloud_notm}}](https://{DomainName}/catalog/services/text-to-speech){: external}.

## Soporte de idiomas
{: #languages-index}

El servicio da soporte a voces en los idiomas siguientes: portugués de Brasil, inglés (en sus dialectos del Reino Unido y de Estados Unidos), francés, alemán, italiano, japonés y español (en sus dialectos de España, latinoamericano y norteamericano).

El servicio ofrece al menos una voz femenina para cada idioma. Para algunos idiomas, el servicio ofrece varias voces, tanto masculinas como femeninas. Cada voz utiliza la cadencia y la entonación adecuadas según su dialecto. El servicio ofrece las versiones estándar y neuronal de la mayoría de voces.

Para obtener más información sobre las voces que hay disponibles para cada idioma, consulte [Idiomas y voces](/docs/services/text-to-speech?topic=text-to-speech-voices).

## Casos prácticos
{: #usecases}

El servicio es apropiado para aplicaciones dirigidas por voz y sin pantalla, donde el audio es el método preferido de salida:

-   Las interfaces para las personas con discapacidad, como por ejemplo las herramientas de asistencia para personas con discapacidad visual
-   Lectura de mensajes de texto y correo electrónico en voz alta a los conductores
-   Narración de guiones de vídeo y voz en off en vídeos
-   Herramientas educativas basadas en la lectura
-   Soluciones de automatización doméstica

## Probar el servicio

Para ver ejemplos del servicio en acción, consulte

-   Una [demostración rápida](https://text-to-speech-demo.ng.bluemix.net/){: external} del servicio {{site.data.keyword.texttospeechshort}} que acepta texto y genera habla con distintas voces. Ofrece expresividad y transformación allí donde están soportadas.
-   Aplicaciones en [Kits de inicio de {{site.data.keyword.ibmwatson}}](http://www.ibm.com/watson/developercloud/starter-kits.html){: external} que muestran el servicio {{site.data.keyword.texttospeechshort}}.
