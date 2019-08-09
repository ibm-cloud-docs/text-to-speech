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

# Comprender la personalización
{: #customIntro}

Al sintetizar texto con {{site.data.keyword.texttospeechfull}}, el servicio aplica reglas de pronunciación dependientes del idioma. El servicio aplica las reglas para convertir la escritura normal (ortográfica) de cada palabra a una escritura fonética. La escritura de una palabra utiliza símbolos que representan fonemas para definir cómo se pronuncia esa palabra. Estos símbolos son unidades distintas de sonido que distinguen las palabras de un idioma, los límites silábicos y las marcas de acentuación en las sílabas.
{: shortdesc}

Las reglas de pronunciación regular del servicio funcionan bien para las palabras comunes. Sin embargo, pueden producir resultados imperfectos para palabras inusuales. Estas palabras incluyen términos especiales de origen extranjero, nombres de persona o geográficos y abreviaturas o acrónimos. Si el léxico de la aplicación incluye palabras de este tipo, puede utilizar la interfaz de personalización para especificar cómo las pronuncia el servicio.

La interfaz de personalización es una funcionalidad beta que está disponible para todos los idiomas. Debe tener el Plan de precios estándar para utilizar la personalización del modelo de voz. Los usuarios del plan Lite no pueden utilizar la interfaz de personalización. Para obtener más información, consulte la [página de precios](https://www.ibm.com/cloud/watson-text-to-speech/pricing){: external} del servicio {{site.data.keyword.texttospeechshort}}.
{: note}

## Cómo funciona la personalización
{: #ciHow}

La interfaz de personalización del servicio {{site.data.keyword.texttospeechshort}} crea un diccionario de palabras y sus traducciones para un idioma específico. Este diccionario se conoce como *modelo de voz personalizado* o simplemente modelo personalizado. Cada entrada personalizada de un modelo de voz personalizado consta de un par de *palabra*/*conversión*. La conversión de una palabra indica al servicio cómo pronunciar la palabra cuando aparece en el texto de entrada.

La interfaz de personalización proporciona métodos para crear y gestionar los modelos de voz personalizados, que el servicio almacena permanentemente. Después de crear un modelo personalizado, puede utilizarlo durante la síntesis con cualquier versión del método `/v1/synthesize`. Cuando el servicio sintetiza texto de entrada, determina la pronunciación de las palabras que aparecen en el modelo personalizado aplicando sus conversiones directa o indirectamente. Puesto que crea un modelo de voz personalizado para un idioma específico, se puede utilizar un modelo personalizado con cualquier voz, estándar o neuronal, que esté disponible en ese idioma.

La conversión para una palabra en un modelo de voz personalizado se especifica como una *conversión 'suena como'* o como una *conversión fonética*. Puede utilizar los dos métodos para las entradas en el mismo modelo personalizado y puede mezclar los dos métodos dentro de la misma conversión. Se aplican varias reglas y directrices a las entradas personalizadas. Para obtener más información, consulte [Reglas para crear entradas personalizadas](/docs/services/text-to-speech?topic=text-to-speech-rules).

## Conversión 'suena como'
{: #soundsLike}

En una *conversión 'suena como'* se utilizan indirectamente las reglas de pronunciación regular de servicio para representar la pronunciación de una palabra de destino. Una conversión 'suena como' se forma a partir de las pronunciaciones normales de una o más palabras. El servicio primero sustituye la conversión especificada para cualquier aparición de la palabra que aparece en el texto de entrada. A continuación aplica las reglas de pronunciación regular a la conversión, convirtiendo la conversión a su representación fonética para obtener la pronunciación.

Por ejemplo, las reglas de pronunciación regular del servicio convierten adecuadamente muchas abreviaturas y acrónimos comunes. El servicio pronuncia la abreviatura *cm* como *centimeter*. Las abreviaturas menos comunes las pronuncia letra por letra. Por ejemplo, el servicio pronuncia la serie *Str* (la abreviatura de *street*) como *S T R*, pronunciando cada letra individualmente. Puede utilizar el método 'suena como' para especificar la conversión *street* para la serie *Str*.

Otro ejemplo de acrónimo es la palabra *IEEE*, que representa el nombre propio Institute of Electrical and Electronic Engineers. De forma predeterminada, el servicio pronuncia este acrónimo como *I E E E*. Pero el acrónimo se pronuncia comúnmente *I triple E*, que se puede definir fácilmente utilizando la conversión 'suena como' *I triple E*. Si la palabra *IEEE* aparece en el modelo personalizado con esta conversión, el servicio sustituye cada aparición de la palabra por la misma. A continuación aplica las reglas de pronunciación regular a las palabras individuales *I*, *triple* y *E* para producir la pronunciación común.

Usted puede aplicar el método 'suena como' a otras palabras aparte de las abreviaturas y acrónimos. Funciona igualmente bien para palabras complejas o inusuales. Por ejemplo, el siguiente par de conversiones 'suena como' producen pronunciaciones correctas para palabras inusuales que el servicio genera mal utilizando las reglas de pronunciación regular del servicio. Encontrar las conversiones adecuadas para estas palabras puede ser más difícil que para las abreviaturas. Las siguientes conversiones utilizan las reglas de pronunciación regular para alterar la ortografía de las palabras.

<table style="width:35%">
  <caption>Tabla 1. Conversiones 'suena como' de ejemplo</caption>
  <tr>
    <th style="text-align:left">Palabra</th>
    <th style="text-align:left">Conversión</th>
  </tr>
  <tr>
    <td>ayurvedic</td>
    <td>aayervedic</td>
  </tr>
  <tr>
    <td>gastroenteritis</td>
    <td>gastro enteritis</td>
  </tr>
</table>

Como muestran estos ejemplos, crear conversiones de tipo 'suena como' puede ser un proceso más bien de ensayo-error. Debe crear una conversión candidata en base a su intuición y su experiencia con el servicio. A continuación, sintetiza la palabra con la conversión candidata como texto de entrada y escucha el audio resultante. Si está satisfecho con la pronunciación, puede utilizar la conversión en el modelo personalizado; de lo contrario, puede modificar la traducción y volver a probarla.

## Conversión fonética
{: #phonetic}

El método 'suena como' es una forma relativamente simple y útil de lograr una pronunciación. Pero no siempre es posible desarrollar conversiones del tipo suena como'. La alternativa directa, el método fonético, puede parecer más largo y complicado, pero puede conseguir la pronunciación de cualquier palabra.

En una *conversión fonética* se especifica la pronunciación en términos de símbolos fonéticos, marcas de acentuación de sílabas y, opcionalmente, límites silábicos que sobrescriben las reglas de pronunciación regular del servicio. Una conversión fonética se especifica en uno de los formatos siguientes:

-   La representación estándar del Alfabeto fonético internacional (IPA -International Phonetic Alphabet)
-   La representación fonética simbólica (SPR -Symbolic Phonetic Representation) propiedad de {{site.data.keyword.IBM_notm}}

En cualquiera de los dos casos, debe especificar una conversión utilizando un formato de fonemas específico basado en SSML (Speech Synthesis Markup Language). SSML es un lenguaje de códigos basado en XML que proporciona anotaciones de texto para aplicaciones de síntesis de voz. Para especificar la conversión fonética de una palabra se utiliza el elemento SSML `<phoneme>`:

<pre><code>&lt;phoneme alphabet="{ipa | ibm}" ph="{translation}"&gt;&lt;/phoneme&gt;</code></pre>

El atributo `alphabet` especifica el tipo de representación fonética: `ipa` o `ibm`. El atributo `ph` especifica la serie de conversión fonética.

Por ejemplo, si tenemos la palabra `trinitroglycerin`. Las reglas de pronunciación regular del servicio producen una pronunciación que difiere de la comúnmente utilizada por los químicos y los médicos. La pronunciación correcta se puede lograr con una conversión fonética.

<table style="width:35%">
  <caption>Tabla 2. Conversiones fonéticas de ejemplo</caption>
  <tr>
    <th style="text-align:left">Alfabeto</th>
    <th style="text-align:left">Conversión</th>
  </tr>
  <tr>
    <td>IPA</td>
    <td>t&#633;a&#618;n&#712;a&#618;t&#633;&#601;gl&#618;s&#601;&#633;&#616;n</td>
  </tr>
  <tr>
    <td>SPR</td>
    <td>trYn1YtrxglIsxrXn</td>
  </tr>
</table>

En estos ejemplos, la serie de conversión fonética se compone de símbolos de fonemas y una única marca de acento primario. La marca de acento primario se representa con <code>&#712;</code> en IPA y con `1` en SPR. En ambos casos, se coloca justo antes del símbolo de la vocal acentuada. Aunque los ejemplos no lo muestran, en una conversión fonética también puede especificar límites de sílaba y posiciones de acento secundario. Estos elementos no son obligatorios y, por lo general, no son necesarios para lograr una pronunciación. Al igual que con las conversiones 'suena como', se puede componer una conversión fonética a partir de varias series delimitada por espacios.

También se puede especificar conversiones IPA con valores IPA Unicode. Para obtener más información, consulte [Utilización de IBM SPR](/docs/services/text-to-speech?topic=text-to-speech-sprs) y las tablas específicas del idioma en las páginas correspondientes de [Idiomas soportados](/docs/services/text-to-speech?topic=text-to-speech-sprs#supportedLanguages). Para ver una conversión de ejemplo que utilice valores de IPA Unicode, consulte [Elemento phoneme](/docs/services/text-to-speech?topic=text-to-speech-elements#phoneme_element).
{: note}

### Trabajar con una conversión fonética existente
{: #phoneticMethod}

A menos que sea un experto en fonología, la composición de conversiones fonéticas no es una tarea fácil. Siempre es más fácil editar una traducción fonética existente que componer una desde cero. Para ayudarle a crear conversiones fonéticas, la API del servicio incluye un método `GET /v1/pronunciation`. El método devuelve la representación IPA o SPR que se genera mediante las reglas de pronunciación regular del servicio para una palabra en un idioma especificado. También puede solicitar la pronunciación de una palabra para un modelo de voz personalizado para ver la conversión en el idioma de ese modelo.

Puede utilizar el método `/GET v/1/pronunciation` para obtener una conversión fonética inicial para una palabra. A continuación, puede modificar la conversión para conseguir la pronunciación deseada. Al igual que con el método 'suena como', se sigue un proceso de ensayo-error. Envía la conversión candidata al servicio, sintetiza la palabra introduciéndola como texto de entrada, escucha el audio resultante y vuelve a editar la conversión candidata. Puede repetir el proceso hasta que esté satisfecho con la pronunciación.

Para obtener más información, consulte [Consultar una palabra de un idioma](/docs/services/text-to-speech?topic=text-to-speech-customWords#cuWordsQueryLanguage).

### Más información sobre la conversión fonética
{: #phoneticInfo}

Los recursos siguientes proporcionan información sobre la conversión fonética:

-   Para obtener más información sobre el uso de SSML y el elemento `<phoneme>`, consulte [Utilización de SSML](/docs/services/text-to-speech?topic=text-to-speech-ssml).
-   Para obtener más información sobre la especificación de conversiones SPR y sus símbolos IPA equivalentes, consulte [Utilización de IBM SPR](/docs/services/text-to-speech?topic=text-to-speech-sprs).
-   Para obtener más información sobre el uso de símbolos IPA y para muestras de audio de los símbolos, consulte las fuentes en la web. Puede encontrar una descripción introductoria detallada en [Alfabeto fonético internacional](https://wikipedia.org/wiki/International_Phonetic_Alphabet){: external}.

## Mezcla de conversión 'suena como' y fonética

Puede mezclar los métodos 'suena como' y fonético en una misma conversión. Esta funcionalidad puede reducir el trabajo necesario para componer una conversión.

Por ejemplo, supongamos que ha utilizado el método 'suena como' para obtener la pronunciación correcta de parte de una palabra. Pero ahora necesita ajustar los demás elementos de la palabra. Puede utilizar el método fonético para especificar los aspectos más difíciles de la palabra. En el ejemplo siguiente se aplica una conversión mixta a la palabra `trinitroglycerin`:

<pre><code>try&lt;phoneme alphabet="ipa" ph="n&#712;a&#618;t&#633;&#601;gl&#618;s&#601;&#633;&#616;n"&gt;&lt;/phoneme&gt;</code></pre>
