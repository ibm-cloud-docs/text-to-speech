---

copyright:
  years: 2015, 2019
lastupdated: "2019-06-23"

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

# Utilización de SSML
{: #ssml}

SSML (Speech Synthesis Markup Language) es un lenguaje de códigos basado en XML que proporciona anotaciones de texto para aplicaciones de síntesis de voz. Es una recomendación del W3C Voice-Browser Working Group y se ha adoptado como el lenguaje de marcación estándar para la síntesis de voz por la especificación de VoiceXML 2.0. SSML proporciona a los desarrolladores de aplicaciones de habla una forma estándar de controlar aspectos del proceso de síntesis, permitiéndoles especificar la pronunciación, el volumen, el tono, la velocidad y otros atributos a través de la marcación.
{: shortdesc}

Con el servicio {{site.data.keyword.texttospeechfull}}, puede utilizar SSML para controlar la síntesis de su texto en todos los idiomas soportados. Esto incluye el uso del elemento SSML `<phoneme>` para definir la pronunciación de una palabra en el Alfabeto fonético internacional (IPA -International Phonetic Alphabet) o en la Representación fonética simbólica (SPR -Symbolic Phonetic Representation) de {{site.data.keyword.IBM_notm}}. El servicio también utiliza el elemento SSML `<phoneme>` para definir la conversión fonética de una palabra con su interfaz de personalización; para obtener más información, consulte [Comprender la personalización](/docs/services/text-to-speech?topic=text-to-speech-customIntro).

## Introducción a SSML
{: #introduction-SSML}

SSML funciona aumentando el texto sin formato que se pasa a un sintetizador con un conjunto predefinido de elementos o etiquetas. Un analizador XML primero separa el texto de entrada sin formato de las especificaciones de marcado. A continuación, las especificaciones se procesan y se envían como un conjunto de instrucciones en una forma que el sintetizador pueda comprender para producir los efectos deseados. Para que el analizador XML pueda llevar a cabo esta tarea, la marcación tiene que tener un formato correcto; por ejemplo, los elementos se tienen que cerrar y si hay varios elementos, tienen que estar correctamente anidados. Para ver una introducción a los conceptos básicos de XML, consulte [w3schools.com/xml/xml_whatis.asp](http://www.w3schools.com/xml/xml_whatis.asp){: external}.

Un elemento SSML es cualquier cosa contenida entre una etiqueta de apertura y su etiqueta de cierre correspondiente y que incluye ambas etiquetas. Como se muestra en el ejemplo siguiente, un elemento puede contener una combinación de otros elementos (los códigos pueden anidarse) y texto. Además, los elementos pueden requerir o aceptar opcionalmente atributos definidos con valores particulares.

```xml
<tag1>
  <tag2 attributeName="attributeValue">
    ... some text ...
  </tag2>
</tag1>
```
{: codeblock}

Un documento SSML legal completo consta de un prólogo XML, que contiene información como la codificación y el esquema en el que se debe validar el documento SSML, seguido del elemento raíz, `<speak>`. (Para obtener más información sobre la estructura del prólogo, consulte [tizag.com/xmlTutorial/xmlprolog.php](http://www.tizag.com/xmlTutorial/xmlprolog.php){: external}.) Dentro del elemento `<speak>` se especifica el texto a sintetizar, aumentado con elementos adicionales.

```xml
<!-- The XML Prolog -->
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE speak PUBLIC "-//W3C//DTD SYNTHESIS 1.0//EN"
  "http://www.w3.org/TR/speech-synthesis/synthesis.dtd">

<!-- Root Element -->
<speak version="1.0" xmlns="www.w3.org/2001/10/synthesis"
  ... the body that contains text to be synthesized plus markup ...
</speak>
```
{: codeblock}

El servicio admite fragmentos SSML, que son elementos SSML que no incluyen la cabecera XML completa.

## Soporte de SSML
{: #ssmlSupport}

El servicio {{site.data.keyword.texttospeechshort}} basa su soporte en SSML Versión 1.0, que es la versión recomendada por W3C el 7 de septiembre de 2004. Para obtener más información sobre la recomendación W3C SSML, consulte la [Versión 1.0 de W3C Speech Synthesis Markup Language (SSML)](http://www.w3.org/TR/speech-synthesis/){: external}.

Para obtener más información sobre cómo utilizar SSML con el servicio, consulte lo siguiente:

-   Para obtener información completa sobre el nivel de soporte del servicio para todos los elementos SSML, consulte [Elementos SSML](/docs/services/text-to-speech?topic=text-to-speech-elements). Con algunas excepciones, el servicio implementa la mayoría de la especificación W3C, así como fragmentos de SSML.
-   El servicio amplía SSML con un elemento `<express-as>` que indica cómo se debe expresar el texto al convertirlo en habla (como una buena noticia, como una disculpa o con incertidumbre). El servicio da soporte a la expresividad sólo para la voz de Allison en inglés de EE.UU. Consulte [Utilización de SSML expresivo](/docs/services/text-to-speech?topic=text-to-speech-expressive).
-   El servicio amplía SSML con un elemento `<voice-transformation>` que amplía la gama de voces posibles permitiendo controlar el tono, el rango de tono, la tensión glotal, la respiración, la velocidad y el timbre del texto hablado. El servicio también ofrece dos voces virtuales integradas, *Young* y *Soft*. El servicio da soporte a la transformación de voz sólo para las voces en inglés de Estados Unidos. Consulte [Utilización de SSML de transformación de voz](/docs/services/text-to-speech?topic=text-to-speech-transformation).
-   La interfaz de personalización del servicio admite el uso del elemento SSML `<phoneme>` para especificar la escritura fonética que utiliza para pronunciar una palabra. La escritura fonética representa los sonidos de una palabra, cómo estos sonidos se dividen en sílabas y qué sílabas reciben acento.
    -   Para obtener información sobre la interfaz de personalización, consulte [Comprender la personalización](/docs/services/text-to-speech?topic=text-to-speech-customIntro).
    -   Para obtener información acerca de los símbolos válidos que puede utilizar en una especificación IPA o {{site.data.keyword.IBM_notm}} SPR para cualquier idioma soportado, consulte [Utilización de IBM SPR](/docs/services/text-to-speech?topic=text-to-speech-sprs).

## Validación de SSML
{: #errors}

El servicio valida todos los elementos SSML que se envían en cualquier contenido, ya sea como texto de entrada para la síntesis o como la definición de la conversión de una palabra para la personalización. El servicio no puede determinar antes de tiempo si el texto enviado para la síntesis contiene elementos SSML. Por lo tanto, realiza la misma validación para todo el texto de entrada, independientemente de si contiene SSML.

-   *Toda entrada SSML debe ser correcta y estar bien formada.* El servicio ignora silenciosamente los elementos SSML no soportados. El servicio sintetiza el texto contenido dentro de un elemento no soportado o un elemento que utilice características no soportadas; solo se ignora el elemento.
-   *El servicio notifica un código de error HTTP 400 cuando hay elementos no válidos.* La respuesta de error incluye un mensaje descriptivo, y la solicitud falla.

Específicamente, el servicio devuelve un error en los casos siguientes:

-   *Elemento no válido.* Por ejemplo, si se especifica una etiqueta de forma incorrecta, se omite un atributo obligatorio o se incluye un código de apertura, pero no el código de cierre correspondiente.
-   *Símbolo no válido.* El atributo `ph` de un elemento `<phoneme>` incluye un símbolo IPA o SPR no soportado para el idioma especificado.
-   *Sin vocales.* El atributo `ph` de un elemento `<phoneme>` especifica una pronunciación de palabra que no incluye vocales.
-   *Liaison francés en una ubicación no válida.* En el atributo `ph` de un elemento `<phoneme>`, el carácter de liaison no va seguido de una consonante ni aparece en medio de la pronunciación de una palabra.
-   *El símbolo de japonés `:` no precede a una vocal.* En el atributo `ph` de un elemento `<phoneme>`, un carácter `:` no aparece antes de una vocal (posiblemente con otros símbolos, como por ejemplo límite de sílaba en medio).
-   *Acento silábico no válido.* El atributo `ph` de un elemento `<phoneme>` de un {{site.data.keyword.IBM_notm}} SPR incluye un acento silábico no válido. En francés un símbolo de acento silábico no precede inmediatamente a una vocal. En español o italiano, se utiliza un símbolo de acento secundario (`2`) o de ningún acento (`0`). En japonés, se utiliza un símbolo de acento secundario (`2`).
-   *Uso no válido del elemento SSML `<express-as>` o `<voice-transformation>`.* Solo puede utilizar estas extensiones SSML con las voces en inglés estándar de Estados Unidos especificadas.
-   *Uso no válido del elemento SSML `<prosody>`.* No puede utilizar los atributos `contour`, `duration` y `range` del elemento `<prosody>` con cualquier voz. Además, no puede utilizar el atributo `volume` del elemento `<prosody>` con voces neuronales (por ejemplo, `en-US_AllisonV3Voice`).
-   *Caracteres de control XML no escapados.* El propio texto de entrada contiene un carácter <code>&quot;</code>, <code>&apos;</code>, `&`, `<` o `>` en lugar de su serie o codificación de caracteres de escape. Para obtener más información, consulte [Escapar los caracteres de control XML](/docs/services/text-to-speech?topic=text-to-speech-usingHTTP#escape).
