---

copyright:
  years: 2015, 2019
lastupdated: "2019-06-06"

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

# Utilización de IBM SPR
{: #sprs}

El servicio {{site.data.keyword.texttospeechfull}} admite tanto la notación estándar IPA (International Phonetic Alphabet) como la notación SPR (Symbolic Phonetic Representation) de {{site.data.keyword.IBM}} para representar los sonidos de las palabras. SPR es una codificación fonética que representa la pronunciación de una palabra, los sonidos que componen la palabra, cómo se dividen los sonidos en sílabas y qué sílabas están acentuadas. SPR es una representación alternativa a IPA.
{: shortdesc}

En las secciones siguientes se introduce la notación {{site.data.keyword.IBM_notm}} SPR. Dado que IPA es una notación estándar, en esta documentación no se proporciona información de uso básica de IPA. Para obtener unas breves instrucciones de uso, consulte [Trabajar con IPA](#ipa).

## Introducción a IBM SPR
{: #introduction-SPRs}

Una pronunciación SPR se define con el [Elemento phoneme](/docs/services/text-to-speech?topic=text-to-speech-elements#phoneme_element) de SSML (Speech Synthesis Markup Language). Consiste en una secuencia de símbolos permitidos para un idioma dado entre comillas dobles. Los símbolos definen cómo se debe pronunciar la palabra contenida en el elemento `<phoneme>`. El atributo `alphabet` del elemento tiene el valor `ibm` para indicar que la pronunciación está definida en SPR, y el atributo `ph` define la pronunciación. A continuación se muestran unos ejemplos de notación SPR válida para las palabras *through* y *shocking* en inglés de Estados Unidos:

```xml
<phoneme alphabet="ibm" ph=".1Tru">through</phoneme>
<phoneme alphabet="ibm" ph=".1Sa.0kIG">shocking</phoneme>
```
{: codeblock}

En las definiciones, se marca con un `.` (punto) el principio de una nueva sílaba, los dígitos `1` y `0` indican el nivel de acentuación de las sílabas y las letras representan sonidos específicos del habla en inglés de Estados Unidos. Una entrada SPR que no se ajuste a la especificación requerida no es válida.

## Límites silábicos

Puede utilizar un `.` (punto) para marcar el principio de cada sílaba. No obstante, para preservar la fonética válida de un idioma, el servicio puede elegir no hacer caso de los puntos en algunos casos (por ejemplo, si se pone un límite de sílaba en una posición no permitida o no natural para un idioma). En general, en los casos donde el usuario puede indicar una preferencia válida por un límite de sílaba u otro aspecto de la pronunciación de una palabra, el servicio cumple dichas solicitudes.

## Acento silábico

Puede utilizar los símbolos de la tabla siguiente para marcar el acento silábico en una pronunciación. {{site.data.keyword.IBM_notm}} recomienda indicar el estrés primario para la pronunciación, sea en SPR o en IPA. No obstante, indicar el acento silábico es opcional para ambos formatos; el servicio determina dónde va el acento si no se indica.

<table style="width:80%">
  <caption>Tabla 1. Acento silábico</caption>
  <tr>
    <th style="width:22%; text-align:center; vertical-align:bottom">
      Símbolo en IBM SPR
    </th>
    <th style="width:22%; text-align:center; vertical-align:bottom">
      Símbolo IPA
    </th>
    <th style="width:22%; text-align:center; vertical-align:bottom">
      IPA Unicode
    </th>
    <th style="text-align:left; vertical-align:bottom">
      Significado
    </th>
  </tr>
  <tr>
    <td style="text-align:center">
      1
    </td>
    <td style="text-align:center">
      <code>&#712;</code>
    </td>
    <td style="text-align:center">
      02C8
    </td>
    <td>
      Acento principal
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      2
    </td>
    <td style="text-align:center">
      <code>&#716;</code>
    </td>
    <td style="text-align:center">
      02CC
    </td>
    <td>
      Acento secundario
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      0
    </td>
    <td style="text-align:center">Ningún símbolo</td>
    <td style="text-align:center">Ningún valor</td>
    <td>
      Sin acento
    </td>
  </tr>
</table>

**Notas:**

-   En IPA, para el francés, los símbolos de acentuación silábica se ignoran. En SPR, para francés, el acento silábico no se ignora, si se especifica, debe ir inmediatamente antes de la vocal de la sílaba. En SPR, el acento silábico para el francés es mucho más estricto que para otros idiomas; si el símbolo de acentuación está en una posición no válida, se produce un error.
-   En SPR para español e italiano, sólo puede especificar `1` (acento primario). Si se especifica un acento secundario o no se especifica ningún acento, se produce un error.
-   En SPR, para el japonés, solo se admite `1` (acento primario) y `0` (sin acento). Si se especifica un acento secundario, se produce un error.

Debe colocar un marcador de acento silábico dentro de un límite de sílaba, pero siempre a la izquierda de la vocal de la sílaba. Puede colocar un marcador en cualquier lugar siempre que sea a la izquierda de la vocal acentuada. Por ejemplo, todos los ejemplos de SPR siguientes colocan el acento primario en la vocal correcta de la palabra *construction*:

```xml
<phoneme alphabet="ibm" ph="kXn1strHkSXn">construction</phoneme>
<phoneme alphabet="ibm" ph="kXns1trHkSXn">construction</phoneme>
<phoneme alphabet="ibm" ph="kXnst1rHkSXn">construction</phoneme>
<phoneme alphabet="ibm" ph="kXnstr1HkSXn">construction</phoneme>
```
{: codeblock}

## Símbolos de sonidos del habla

Cada idioma utiliza su propio inventario de símbolos SPR para representar los sonidos del habla en ese idioma. Se aplican las reglas siguientes para la especificación de un símbolo SPR:

-   Las letras son sensibles a mayúsculas y minúsculas, por tanto `e` y `E`, por ejemplo, representan dos sonidos distintos.
-   Los símbolos de dos y tres caracteres deben ir entre comillas simple, por ejemplo, el símbolo `aj` dentro de la palabra en alemán *heim*: `"h'aj'm"`.
-   El servicio considera no válida cualquier definición de SPR que contenga símbolos de sonido que no estén permitidos en un idioma.

Tenga en cuenta también lo siguiente al definir la pronunciación de una palabra en formato SPR:

-   Los sonidos de cada idioma tienen patrones de distribución específicos dentro de ese idioma. Por ejemplo, en todos los dialectos del inglés, el sonido `G` en *sing* (`".1sIG"`) no aparece nunca a principio de palabra. Otros sonidos en inglés de Estados Unidos que tienen una distribución particularmente limitada son la oclusiva glotal (`?`), la vibrante alveolar simple (`F`), y la nasal silábica (`N`). Si especifica un símbolo de sonido en un contexto en el que normalmente no se produce, el discurso resultante puede quedar no natural.
-   El servicio {{site.data.keyword.texttospeechshort}} aplica un sofisticado conjunto de reglas lingüísticas a la entrada para reflejar los procesos por los que los sonidos cambian en contextos específicos en el lenguaje natural. Por ejemplo, en inglés de Estados Unidos, el sonido `t` de la palabra *write* (`".1r1Yt"`) se pronuncia como una vibrante alveolar simple (`F`) en *writer* (`".1rY.0FR"`). La entrada de SPR sufre estas modificaciones igual que el texto de entrada ordinario. En este ejemplo, si especifica `".1rY.0tR"` o `".1rY.0FR"` no afecta al habla que se genera.

## Trabajar con IPA
{: #ipa}

La información siguiente se aplica para trabajar con pronunciaciones en la notación IPA:

-   Utilice únicamente los símbolos IPA documentados. Cuando se listan varios símbolos IPA (o combinaciones de símbolos) para un símbolo SPR, todos son equivalentes al símbolo SPR individual. En este caso, el servicio trata todos estos símbolos IPA de la misma forma y no advierte las diferencias sutiles o regionales que el sistema IPA sí describe.
-   También puede especificar pronunciaciones IPA como valores de IPA Unicode. En las tablas específicas de cada idioma de la sección siguiente se documentan los símbolos IPA y sus valores IPA Unicode equivalentes. Para obtener un ejemplo de pronunciación que utilice valores IPA Unicode, consulte [Elemento phoneme](/docs/services/text-to-speech?topic=text-to-speech-elements#phoneme_element).

Para obtener más información, consulte lo siguiente:

-   Para obtener más información sobre IPA, consulte [Alfabeto fonético internacional (IPA - International Phonetic Alphabet)](https://wikipedia.org/wiki/International_Phonetic_Alphabet){: external}.
-   Para obtener más información sobre los símbolos fonéticos en Unicode, consulte [Símbolos fonéticos en Unicode](https://wikipedia.org/wiki/Phonetic_symbols_in_Unicode){: external}.

## Idiomas soportados
{: #supportedLanguages}

En las páginas siguientes se documentan los símbolos SPR, los símbolos IPA y los valores IPA Unicode equivalentes para cada idioma. Se muestran ejemplos de cada símbolo en palabras del idioma. Debido a las diferencias dialectales, es posible que los ejemplos no siempre coincidan con su pronunciación.

-   [Símbolos para el portugués de Brasil](/docs/services/text-to-speech?topic=text-to-speech-ptSymbols)
-   [Símbolos para el inglés británico](/docs/services/text-to-speech?topic=text-to-speech-gbSymbols)
-   [Símbolos para el francés](/docs/services/text-to-speech?topic=text-to-speech-frSymbols)
-   [Símbolos para el alemán](/docs/services/text-to-speech?topic=text-to-speech-deSymbols)
-   [Símbolos para el italiano](/docs/services/text-to-speech?topic=text-to-speech-itSymbols)
-   [Símbolos para el japonés](/docs/services/text-to-speech?topic=text-to-speech-jaSymbols)
-   [Símbolos para el español](/docs/services/text-to-speech?topic=text-to-speech-esSymbols)
-   [Símbolos para el inglés de EE.UU.](/docs/services/text-to-speech?topic=text-to-speech-usSymbols)
