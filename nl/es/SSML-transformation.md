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

# SSML de transformación de voz
{: #transformation}

El servicio {{site.data.keyword.texttospeechfull}}, como la mayoría de los sistemas de síntesis de voz, sólo puede hablar en un número limitado de voces. Además, en algunos idiomas solo se ofrecen una o dos voces. Para ampliar el rango de voces posibles, el servicio ahora amplía SSML con un elemento `<voice-transformation>`. Puede utilizar este elemento para crear distintas voces virtuales controlando aspectos de una voz predeterminada. Entre las aplicaciones de esta característica se incluyen:
{: shortdesc}

-   *Dar un carácter distinto a una voz.* Desea que una voz suene un poco distinta en general o para una aplicación específica.
-   *Voz de marca.* Desea utilizar una voz exclusiva para diferenciar sus aplicaciones.
-   *Aplicaciones con varios roles.* Necesita varias voces para representar personajes distintos.

Puede aplicar el elemento `<voice-transformation>` a todo el cuerpo del texto, a una frase o a una palabra o un fragmento. El elemento acepta un atributo obligatorio, `type`, que describe el tipo de transformación de voz que se debe aplicar al texto especificado. Puede aplicar una transformación integrada o crear una transformación personalizada basada en distintos aspectos de la voz.

## Soporte de idiomas
{: #languages-transformation}

El servicio sólo admite la transformación de voz para las siguientes voces en inglés de Estados Unidos:

-   `en-US_AllisonVoice`
-   `en-US_LisaVoice`
-   `en-US_MichaelVoice`

No se admite la transformación de voz con la `V2`, las versiones basadas en DNN de estas voces (por ejemplo, `en-US_AllisonV2Voice`). Si se utiliza el elemento con una voz no soportada, se devuelve un error.

## Transformaciones integradas

Las transformaciones integradas aplican cambios preconfigurados a los atributos de una voz. Considérelas voces virtuales que están disponibles en el servicio. El servicio ofrece dos transformaciones integradas. Para utilizarlas, especifique el nombre sensible a mayúsculas y minúsculas de la transformación integrada con el atributo `type`:

-   `Young` da a la voz un sonido más juvenil.
-   `Soft` hace que la voz suene más suave.

Puede aplicar el atributo opcional `strength` a cualquier voz integrada para controlar el grado en que el servicio aplica la transformación. Considere el valor un factor de mezcla que el servicio aplica a la voz original. El atributo acepta un valor del 0 al 100 por ciento. Si se especifica `0%` se deja la voz inalterada; si se especifica `100%` se alcanza el grado completo de la transformación. Si omite el atributo, la intensidad predeterminada es `100%`.

El servicio ignora los atributos de las transformaciones personalizadas si se utiliza una transformación integrada.
{: note}

## Ejemplos de transformación integradas

En los ejemplos siguientes se aplican las dos transformaciones integradas a la misma frase con distintas intensidades:

```xml
<voice-transformation type="Young" strength="80%">
  Could you provide us with new information?
</voice-transformation>

<voice-transformation type="Soft" strength="60%">
  Could you provide us with new information?
</voice-transformation>
```
{: codeblock}

## Transformaciones personalizadas

Las transformaciones personalizadas permiten un control más preciso de distintos aspectos de la transformación de voz. Para utilizar una transformación personalizada, debe especificar `Custom` en el atributo `type`. A continuación, puede utilizar uno o más de los siguientes atributos opcionales para controlar la transformación.

<table>
  <caption>Tabla 1. Atributos de transformación personalizada</caption>
  <tr>
    <th style="width:15%; text-align:left">Atributo</th>
    <th style="width:25%; text-align:center">Rango</th>
    <th style="text-align:left">Descripción</th>
  </tr>
  <tr>
    <td><code>pitch</code></td>
    <td style="text-align:center">[-100%, 100%],<br/>
      [<code>x-low</code>, <code>low</code>, <code>default</code>,
      <code>high</code>, <code>x-high</code>]</td>
    <td>
      Cambio relativo normalizado del nivel de contorno medio de tono (pitch)
      dentro de límites seguros. Este atributo controla el nivel de tonalidad
      medio percibido. Se toma prestado del atributo <code>pitch</code>
      del elemento SSML <code>&lt;prosody&gt;</code>. Contribuye
      a cambiar la percepción de la identidad del hablante.
    </td>
  </tr>
  <tr>
    <td><code>pitch_range</code></td>
    <td style="text-align:center">[-100%, 100%],<br/>
      [<code>x-narrow</code>, <code>narrow</code>, <code>default</code>,
      <code>wide</code>, <code>x-wide</code>]</td>
    <td>
      Cambio relativo normalizado del rango dinámico del contorno del tono (pitch)
      dentro de límites seguros. Al aumentar o disminuir el rango del tono
      hace que el estilo de voz sea más o menos expresivo. Este atributo
      se toma prestado del atributo <code>range</code> del elemento SSML
      <code>&lt;prosody&gt;</code>.</td>
  </tr>
  <tr>
    <td><code>glottal_tension</code></td>
    <td style="text-align:center">[-100%, 100%],<br/>
      [<code>x-low</code>, <code>low</code>, <code>default</code>,
      <code>high</code>, <code>x-high</code>]</td>
    <td>
      Cambio relativo normalizado de la tensión glotal dentro de límites
      seguros. Al aumentar o disminuir la tensión glotal se percibe una calidad
      de habla más tensa o más laxa. Un valor positivo puede producir
      zumbidos, que puede aliviar aumentando el valor del atributo
      <code>breathiness</code>. Un valor negativo se percibe como más
      susurrante y generalmente más agradable.
    </td>
  </tr>
  <tr>
    <td><code>breathiness</code></td>
    <td style="text-align:center">[-100%, 100%],<br/>
      [<code>x-low</code>, <code>low</code>, <code>default</code>,
      <code>high</code>, <code>x-high</code>]</td>
    <td>
      Cambio relativo normalizado del nivel percibido el ruido de aspiración
      dentro de límites seguros. Los valores extremos pueden producir un habla
      con ruidos (para un valor de breathiness positivo) o un sonido de zumbido
      (para un valor de breathiness negativo). Utilice este atributo para compensar los zumbidos o los
      ruidos producidos como efectos secundarios de otros atributos.
    </td>
  </tr>
  <tr>
    <td><code>rate</code></td>
    <td style="text-align:center">[-100%, 100%],<br/>
      [<code>x-slow</code>, <code>slow</code>, <code>default</code>,
      <code>fast</code>, <code>x-fast</code>]</td>
    <td>
      Cambio relativo normalizado de la velocidad de habla dentro de límites seguros.
      AL aumentar o disminuir la velocidad, el habla se produce más rápida o más lentamente.
      Una velocidad positiva (más rápida) hace que el rango de tono percibido sea más amplio,
      y una velocidad negativa (más lenta) estrecha perceptualmente el rango de tono.
      Este atributo se toma prestado del atributo <code>rate</code> del
      elemento SSML <code>&lt;prosody&gt;</code>.</td>
  </tr>
  <tr>
    <td><code>timbre</code></td>
    <td style="text-align:center">[<code>Sunrise</code>,
      <code>Breeze</code>]</td>
    <td>
      El nombre sensible a mayúsculas y minúsculas de una de las transformaciones integradas
      del tracto vocal: <code>Sunrise</code> o <code>Breeze</code>.
      Los nombres son simbólicos. Experimente con los timbres para ver su
      impacto sobre la transformación de la voz. Este atributo contribuye
      a cambiar la percepción de la identidad del hablante.
    </td>
  </tr>
  <tr>
    <td><code>timbre_extent</code></td>
    <td style="text-align:center">[0%, 100%]</td>
    <td>
      El alcance se la transformación del tracto vocal <code>timbre</code>:
      <code>0%</code> cancela la transformación; <code>100%</code>
      representa que la transformación se aplica completamente. Este atributo
      cuantifica la diferencia entre las voces transformadas y originales. Permite mezclar el timbre seleccionado con el timbre de la voz
      original. Incluso con valores moderados de timbre_extent, el
      atributo <code>timbre</code> contribuye a cambiar la percepción
      de la identidad del hablante.
    </td>
  </tr>
</table>

### Utilización de rangos
{: #ranges}

Los rangos numéricos de los distintos atributos indican el grado en que un atributo afecta a la voz. Por ejemplo, el atributo `rate` tiene un rango de -100% a 100%:

-   Un valor de `100%` no significa que la voz vaya a ser un 100% más rápida. Significa que el servicio aumenta la velocidad de la voz al máximo permitido para esa voz.
-   Un valor de `-100%` significa que el servicio utiliza la velocidad mínima permitida para la voz.
-   Un valor de `0%` representa el nivel inherente del atributo para la voz; la voz permanece inalterada.

### Utilización de valores literales
{: #literals}

Como facilidad, muchos de los atributos también definen valores literales que se pueden utilizar en lugar de porcentajes. El significado de estos valores son distintos de los valores que se utilizan con el elemento SSML `<prosody>`. El elemento `<voice-transformation>` utiliza una escala coherente en todos sus atributos.

-   `x-low`, `x-slow` y `x-narrow` equivalen a un valor del `-100%`.
-   `low`, `slow` y `narrow` equivalen a un valor del `-50%`.
-   `default` equivale a un valor del `0%`, el valor predeterminado de ese atributo y esa voz.
-   `high`, `fast` y `wide` equivalen a un valor del `+50%`.
-   `x-high`, `x-fast` y `x-wide` equivalen a un valor del `+100%`.

### Instrucciones de uso
{: #guidelines}

Utilice las siguientes directrices y la siguiente información admonitoria:

-   Para la voz de marca o para las aplicaciones con varios roles, utilice los atributos `timbre`, `pitch` y `glottal_tension` para cambiar la percepción de la identidad del hablante. Puede utilizar combinaciones de estos tres atributos para crear voces virtuales. Considere una voz virtual como un punto en el espacio multidimensional que se realiza mediante el timbre, el tono y la tensión glotal especificados. Diferentes combinaciones de los atributos dan lugar a diferentes voces virtuales.
-   Puede utilizar los atributos `pitch_range`, `breathiness` y `rate` para añadir carácter a una voz virtual. Otros usuarios pueden elegir los mismos valores de atributo o similares, por lo que el servicio no puede garantizar la exclusividad de la voz virtual creada.
-   Tenga presentes los siguientes efectos secundarios potenciales de aplicar los atributos:
    -   Si se utilizan unos valores elevados para glottal_tension y pitch y una velocidad baja puede hacer que se produzcan zumbidos. Para mitigar este efecto, puede aumentar el valor de breathiness.
    -   Un valor de glottal_tension demasiado bajo puede producir ruidos en el habla. Para reducir estos ruidos puede disminuir el valor de breathiness.
    -   Si se eleva o de reduce pitch_range y rate simultáneamente hasta sus grados extremos, puede que la voz no suene natural.
-   Tal como se ha indicado, algunos de los atributos se han tomado prestados del elemento SSML `<prosody>`. Para obtener más información, consulte [Elemento prosody](/docs/services/text-to-speech/SSML-elements.html#prosody_element). Para habilitar el control ajustado de prosody de una voz virtual, puede
    -   Anidar elementos de `<prosody>` dentro de elementos de `<voice-transformation>`.
    -   Anidar elementos de `<voice-transformation>` dentro de elementos de `<prosody>`.

    *No se pueden* anidar elementos de `<voice-transformation>`.

## Ejemplos de transformaciones personalizadas

En los siguientes ejemplos se aplican distintos atributos para mostrar posibles aplicaciones de las transformaciones personalizadas. En el primer ejemplo se reduce glottal_tension para suavizar la voz. También se aumenta de forma moderada pitch_range y rate para introducir un estilo de habla más dinámico.

```xml
<voice-transformation type="Custom" glottal_tension="-50%"
  pitch_range="30%" rate="10%">
  Do you have more information?
</voice-transformation>
```
{: codeblock}

En el segundo ejemplo se utiliza el valor máximo de glottal_tension el mínimo de pitch y rate. Estas combinaciones en general no son favorables y pueden producir zumbidos. En el ejemplo se mitiga este efecto aumentando el valor de breathiness.

```xml
<voice-transformation type="Custom" glottal_tension="100%" pitch="100%"
  rate="-100%" breathiness="60%">
  Do you have more information?
</voice-transformation>
```
{: codeblock}

En los dos ejemplos siguientes se cambia la percepción de la identidad del hablante aplicando timbre. La voz se altera controlando el grado de la mezcla y cambiando el nivel del atributo pitch. En el primer ejemplo se utiliza el grado predeterminado de timbre: 100%.

```xml
<voice-transformation type="Custom" timbre="Sunrise" pitch="40%">
  Do you have more information?
</voice-transformation>

<voice-transformation type="Custom" timbre="Breeze" timbre_extent="30%"
  pitch="-30%">
  Do you have more information?
</voice-transformation>
```
{: codeblock}

En el ejemplo final se utilizan varios atributos para transformar la voz. En el ejemplo se utiliza el grado predeterminado del atributo timbre y se omite breathiness.

```xml
<voice-transformation type="Custom" timbre="Sunrise" pitch="-30%"
  pitch_range="80%" rate="60%" glottal_tension="-80%">
  Do you have more information?
</voice-transformation>
```
{: codeblock}
