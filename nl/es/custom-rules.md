---

copyright:
  years: 2015, 2019
lastupdated: "2018-06-04"

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

# Reglas para crear entradas personalizadas
{: #rules}

Se aplican las siguientes reglas y directrices para cumplimentar un modelo personalizado con entradas personalizadas (pares de palabra/traducción).

## Número máximo de entradas personalizadas

Un modelo personalizado no puede incluir más de 20.000 entradas personalizadas.

## Codificación de caracteres

El servicio acepta la codificación de caracteres ASCII y UTF-8 para las entradas de *palabra* y *traducción*. En las traducciones, utilice la codificación ASCII para las notaciones SPR y la codificación UTF-8 para las notaciones IPA.

## Espacio en blanco

Una *palabra* no puede incluir un espacio en blanco. El servicio utiliza el espacio en blanco para delimitar las palabras en el texto de entrada.

## Sensibilidad a mayúsculas y minúsculas

Una *palabra* es sensible a mayúsculas y minúsculas. Por ejemplo, supongamos que un modelo personalizado contiene la entrada `{word='Sun', translation='Sunday'}`. El servicio aplica su pronunciación predeterminada a la palabra `sun` y la traducción personalizada a la palabra `Sun`, puesto que sólo esta última tiene una letra mayúscula inicial.


## Sensibilidad al contexto

Las pronunciaciones de algunas palabras son sensibles al contexto. Por ejemplo, imaginemos la siguiente frase de entrada:

```
St. Anthony lives on Henry St.
```
{: codeblock}

Las reglas de pronunciación predeterminadas del servicio sintetizan correctamente este texto como

```
Saint Anthony lives on Henry Street
```
{: codeblock}

No obstante, si sustituye las reglas de pronunciación predeterminadas de la serie `St.` para traducirlo como `saint`, el servicio ya no puede pronunciar la palabra en base al contexto. Si se aplicara un modelo de voz personalizado que incluyera esta traducción haría que el servicio pronunciara la oración de entrada anterior como

```
Saint Anthony lives on Henry saint
```
{: codeblock}

Tenga presentes estos casos al desarrollar pares de palabra/traducción.

## Puntos finales

El servicio aplica una palabra de un modelo personalizado sólo a las series del texto de entrada que coinciden exactamente con la palabra. Un punto final `.` (punto) en una entrada de palabra cambia la forma en que se sintetiza la palabra:

-   *Una palabra que no tenga un punto final* puede contener prácticamente cualquier carácter. Los caracteres incluyen letras, dígitos, signos de puntuación (distintos del punto final), símbolos sin letras (como por ejemplo %, &amp;, y @), comillas, paréntesis, corchetes, etc. Su *conversión* puede incluir cualquier entrada legal para el servicio, incluyendo el espacio en blanco y una representación fonética en formato SSML.
-   *Una palabra que tenga un punto final* sólo puede contener letras, puntos y apóstrofos internos (no como primer ni último carácter). La *conversión* de la palabra sólo puede contener palabras normales con la ortografía normal separadas por espacios en blanco o guiones. No puede contener una representación fonética.

Un ejemplo de una palabra con un punto final es "`div.`". Supongamos que un modelo personalizado incluye la entrada `{word='div.', translation='division'}`. El servicio no aplica la conversión a la serie"`div`" porque no incluye un punto final y, por tanto, no coincide con la entrada.

## Trabajar con entradas IBM SPR
{: #sprNotes}

SPR (Symbolic Phonetic Representation) es un formato propietario, dependiente del idioma, desarrollado por {{site.data.keyword.IBM_notm}} para especificar la pronunciación de las palabras. Para cada idioma soportado, SPR incluye un alfabeto de fonemas, símbolos para los límites silábicos y símbolos para los distintos niveles de acentuación léxica. Se aplican las reglas básicas siguientes para la creación de entradas SPR:

-   La pronunciación predeterminada que devuelve la interfaz de personalización para una palabra comienza con un <code>&#96;</code> (acento agudo) y va rodeada de `[]` (corchetes cuadrados). Por ejemplo, la interfaz devuelve la siguiente pronunciación para la palabra `tomato`:

    ```xml
    `[.0tx.1ma.0to]
    ```
    {: codeblock}

    Omita las comillas y corchetes cuando especifique la conversión de una palabra con los métodos de la interfaz de personalización.
-   Puede utilizar un punto para indicar el principio de una sílaba en una conversión, pero los puntos son opcionales y no influyen en la pronunciación de la palabra. Sólo aparecen en la pronunciación de una palabra si se incluyen en la conversión de la misma. No utilice espacios para indicar los límites silábicos.
-   {{site.data.keyword.IBM_notm}} recomienda marcar la vocal que tiene el acento primario con un símbolo `1` antes de la vocal, aunque no es estrictamente necesario. El servicio determina dónde va el acento si no se indica. También puede utilizar un símbolo `2` para indicar la posición del acento secundario, pero el uso del símbolo `2` también es opcional. Sólo aparecen en la pronunciación de una palabra si se incluyen en la conversión de la misma.

Para obtener más información sobre cómo trabajar con SPR, consulte [Utilización de IBM SPR](/docs/services/text-to-speech?topic=text-to-speech-sprs).

## Trabajar con entradas en japonés
{: #jaNotes}

Se aplican reglas adicionales, así como el campo adicional `part_of_speech` para la creación de palabras en un modelo de voz personalizado en japonés:

-   Una conversión 'suena como' sólo puede contener caracteres *Katakana*. Los caracteres *Kanji* e *Hiragana* no están permitidos.
-   Al crear una conversión ('suena como' o fonética) para una palabra, también puede especificar un campo `part_of_speech` opcional para identificar la categoría léxica de la palabra. El servicio utiliza la categoría léxica para producir la entonación correcta para esa palabra. Para obtener una lista completa, consulte [Categorías léxicas del japonés](#partsOfSpeech).
-   Solo se puede crear una entrada para cada palabra y solo se puede especificar una categoría léxica para cada palabra. No se pueden crear varias entradas con diferentes categorías léxicas (por ejemplo, nombre y verbo) para una misma palabra. Si se añade una conversión para una palabra que ya existe en un modelo, se sobrescribe la conversión existente de la palabra, incluyendo la categoría léxica.
-   El servicio aplica la palabra coincidente más larga de los pares de palabra/conversión que hay definidos para un modelo de voz personalizado. Por ejemplo, imaginemos que hay las tres entradas siguientes para un modelo personalizado.

    <pre><code>{
      "words": [
        {
          "word": "&#65326;&#65337;",
          "translation": "&#12491;&#12517;&#12540;&#12520;&#12540;&#12463;",
          "part_of_speech": "Mesi"
        },
        {
          "word": "&#65326;&#65337;&#65315;",
          "translation": "&#12491;&#12517;&#12540;&#12520;&#12540;&#12463;&#12471;&#12486;&#12451;",
          "part_of_speech": "Mesi"
        },
        {
          "word": "&#65337;&#65315;",
          "translation": "&#12520;&#12467;&#12495;&#12510;&#12481;&#12517;&#12540;&#12459;&#12460;&#12452;",
          "part_of_speech": "Mesi"
        }
      ]
    }</code></pre>

    Con estas entradas, imaginemos que el servicio recibe el siguiente texto de entrada: <code>&#19968;&#36913;&#38291;&#65326;&#65337;&#65315;&#12434;&#35370;&#21839;&#12375;&#12383;</code>. En este caso, el servicio coincide con la palabra <code>&#65326;&#65337;&#65315;</code> porque <code>&#65326;&#65337;&#65315;</code> es más largo que <code>&#65326;&#65337;</code> y porque <code>&#65326;&#65337;&#65315;</code> coincide antes que <code>&#65337;&#65315;</code>.

### Categorías léxicas del japonés
{: #partsOfSpeech}

En la tabla siguiente se listan las categorías léxicas que están soportadas para las entradas personalizadas en japonés. Para obtener más información sobre cómo especificar la categoría léxica de una entrada personalizada en japonés, consulte [Añadir palabras a un modelo personalizado en japonés](/docs/services/text-to-speech?topic=text-to-speech-customWords#cuJapaneseAdd).

<table style="width:75%">
  <caption>Tabla 1. Categorías léxicas del japonés</caption>
  <tr>
    <th style="text-align:center">argumento <code>part_of_speech</code></th>
    <th style="text-align:center; width:35%">Significado en japonés</th>
    <th style="text-align:center; width:35%">Significado en inglés</th>
  </tr>
  <tr>
    <td style="text-align:center"><code>Josi</code></td>
    <td style="text-align:center"><em>Joshi</em></td>
    <td style="text-align:center">Participio</td>
  </tr>
  <tr>
    <td style="text-align:center"><code>Mesi</code></td>
    <td style="text-align:center"><em>Meishi</em></td>
    <td style="text-align:center">Nombre</td>
  </tr>
  <tr>
    <td style="text-align:center"><code>Kigo</code></td>
    <td style="text-align:center"><em>Kigou</em></td>
    <td style="text-align:center">Símbolo</td>
  </tr>
  <tr>
    <td style="text-align:center"><code>Gobi</code></td>
    <td style="text-align:center"><em>Gobi</em></td>
    <td style="text-align:center">Inflexión</td>
  </tr>
  <tr>
    <td style="text-align:center"><code>Dosi</code></td>
    <td style="text-align:center"><em>Doushi</em></td>
    <td style="text-align:center">Verbo</td>
  </tr>
  <tr>
    <td style="text-align:center"><code>Jodo</code></td>
    <td style="text-align:center"><em>Jodoushi</em></td>
    <td style="text-align:center">Verbo auxiliar</td>
  </tr>
  <tr>
    <td style="text-align:center"><code>Koyu</code></td>
    <td style="text-align:center"><em>Koyuumeishi</em></td>
    <td style="text-align:center">Nombre propio</td>
  </tr>
  <tr>
    <td style="text-align:center"><code>Stbi</code></td>
    <td style="text-align:center"><em>Setsubiji</em></td>
    <td style="text-align:center">Sufijo</td>
  </tr>
  <tr>
    <td style="text-align:center"><code>Suji</code></td>
    <td style="text-align:center"><em>Suuji</em></td>
    <td style="text-align:center">Numeral</td>
  </tr>
  <tr>
    <td style="text-align:center"><code>Kedo</code></td>
    <td style="text-align:center"><em>Keiyodoushi</em></td>
    <td style="text-align:center">Verbo adjetival</td>
  </tr>
  <tr>
    <td style="text-align:center"><code>Fuku</code></td>
    <td style="text-align:center"><em>Fukishi</em></td>
    <td style="text-align:center">Adverbio</td>
  </tr>
  <tr>
    <td style="text-align:center"><code>Keyo</code></td>
    <td style="text-align:center"><em>Keiyoshi</em></td>
    <td style="text-align:center">Verbo adjetival</td>
  </tr>
  <tr>
    <td style="text-align:center"><code>Stto</code></td>
    <td style="text-align:center"><em>Settoji</em></td>
    <td style="text-align:center">Prefijo</td>
  </tr>
  <tr>
    <td style="text-align:center"><code>Reta</code></td>
    <td style="text-align:center"><em>Rentaishi</em></td>
    <td style="text-align:center">Determinante</td>
  </tr>
  <tr>
    <td style="text-align:center"><code>Stzo</code></td>
    <td style="text-align:center"><em>Setsuzokushi</em></td>
    <td style="text-align:center">Conjunción</td>
  </tr>
  <tr>
    <td style="text-align:center"><code>Kato</code></td>
    <td style="text-align:center"><em>Kantoushi</em></td>
    <td style="text-align:center">Interjección</td>
  </tr>
  <tr>
    <td style="text-align:center"><code>Hoka</code></td>
    <td style="text-align:center"><em>Hoka</em></td>
    <td style="text-align:center">Otro</td>
  </tr>
</table>
