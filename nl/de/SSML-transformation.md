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

# SSML für Stimmenumwandlung
{: #transformation}

Wie die meisten Systeme für die Sprachsynthese kann auch der {{site.data.keyword.texttospeechfull}}-Service für die Sprachausgabe nur eine begrenzte Anzahl von Stimmen verwenden. Einige Sprachen bieten darüber hinaus nur eine oder zwei Stimmen. Um die Palette der möglichen Stimmen zu vergrößern, erweitert der Service SSML durch ein Element `<voice-transformation>`. Mit diesem Element können Sie unterschiedliche virtuelle Stimmen erzielen, indem Sie die Aspekte einer Standardstimme steuern. Diese Funktion bietet unter anderem die hier aufgeführten Anwendungsmöglichkeiten.
{: shortdesc}

-   *Stimme mit einer anderen Variante versehen:* Sie können definieren, dass eine Stimme generell oder für eine bestimmte Anwendung etwas anders klingt.
-   *Kennzeichnung durch Stimme:* Durch die Verwendung einer eindeutigen Stimme können Sie Ihre Anwendungen voneinander unterscheiden.
-   *Anwendungen mit mehreren Rollen:* Sie benötigen mehrere Stimmen, um unterschiedliche Charaktere darzustellen.

Sie können das Element `<voice-transformation>` auf den gesamten Text, einen Satz oder ein Wort bzw. Fragment anwenden. Das Element akzeptiert nur ein einziges erforderliches Attribut namens `type`, das den Typ der Stimmenumwandlung beschreibt, die auf den angegebenen Text angewendet werden soll. Sie können eine integrierte Umwandlung anwenden oder eine angepasste Umwandlung erstellen, die auf unterschiedlichen Aspekten der Stimme beruht.

## Sprachunterstützung
{: #languages-transformation}

Die Stimmenumwandlung wird vom Service nur bei den folgenden Stimmen für amerikanisches Englisch unterstützt:

-   `en-US_AllisonVoice`
-   `en-US_LisaVoice`
-   `en-US_MichaelVoice`

Die Stimmenumwandlung wird mit den neuronalen Versionen dieser Stimmen (z. B. `en-US_AllisonV3Voice`) nicht unterstützt. Die Verwendung des Elements bei einer nicht unterstützten Stimme gibt einen Fehler zurück.

## Integrierte Umwandlungen
{: #ssml-built-in}

Die integrierten Umwandlungen wenden vorkonfigurierte Änderungen auf die Attribute einer Stimme an. Sie sind mit virtuellen Stimmen vergleichbar, die durch den Service zur Verfügung gestellt werden. Der Service bietet zwei integrierte Umwandlungen. Um sie zu verwenden, geben Sie den Namen der integrierten Umwandlung, bei dem die Groß- und Kleinschreibung beachtet werden muss, mit dem Attribut `type` an:

-   Die Umwandlung `Young` verleiht der Stimme einen jugendlicheren Klang.
-   Die Umwandlung `Soft` macht den Klang der Stimme weicher.

Auf jede integrierte Stimme können Sie das optionale Attribut `strength` anwenden, um den Umfang zu steuern, in dem der Service die Umwandlung anwendet. Dieser Wert ist mit einer Art Überblendungsfaktor vergleichbar, den der Service auf die ursprüngliche Stimme anwendet. Das Attribut akzeptiert einen Wert im Bereich von 0 bis 100 Prozent. Bei Angabe von `0%` wird die Stimme nicht geändert; durch Angabe von `100%` wird der volle Umfang der Umwandlung erreicht. Falls Sie das Attribut nicht angeben, wird `100%` als Standardwert für 'strength' verwendet.

Wenn Sie eine integrierte Umwandlung verwenden, ignoriert der Service Attribute für angepasste Umwandlungen.
{: note}

## Beispiele für integrierte Umwandlungen
{: #ssml-built-in-examples}

In den folgenden Beispielen werden die beiden integrierten Umwandlungen unterschiedlich stark auf denselben Satz angewendet:

```xml
<voice-transformation type="Young" strength="80%">
  Could you provide us with new information?
</voice-transformation>

<voice-transformation type="Soft" strength="60%">
  Could you provide us with new information?
</voice-transformation>
```
{: codeblock}

## Angepasste Umwandlungen
{: #ssml-custom-transforms}

Mit angepassten Umwandlungen können Sie verschiedene Aspekte der Stimmenumwandlung differenzierter steuern. Zur Verwendung einer angepassten Umwandlung geben Sie den Wert `Custom` für das Attribut `type` an. Anschließend können Sie mit einem oder mehreren der folgenden optionalen Attribute die Umwandlung steuern.

<table>
  <caption>Tabelle 1. Attribute für angepasste Umwandlung</caption>
  <tr>
    <th style="width:15%; text-align:left">Attribut</th>
    <th style="width:25%; text-align:center">Reichweite</th>
    <th style="text-align:left">Beschreibung</th>
  </tr>
  <tr>
    <td><code>pitch</code></td>
    <td style="text-align:center">[-100%, 100%],<br/>
      [<code>x-low</code>, <code>low</code>, <code>default</code>,
      <code>high</code>, <code>x-high</code>]</td>
    <td>
      Normalisiert relative Änderungen des durchschnittlichen Stimmhöhenumfangs
      im Rahmen von unproblematischen Grenzwerten. Das Attribut steuert die
      wahrgenommene durchschnittliche Tonhöhe. Es ist dem Attribut
      <code>pitch</code> des SSML-Elements <code>&lt;prosody&gt;</code> entlehnt. Mit
      seiner Hilfe kann die wahrgenommene Identität des Sprechers geändert werden.
    </td>
  </tr>
  <tr>
    <td><code>pitch_range</code></td>
    <td style="text-align:center">[-100%, 100%],<br/>
      [<code>x-narrow</code>, <code>narrow</code>, <code>default</code>,
      <code>wide</code>, <code>x-wide</code>]</td>
    <td>
      Normalisiert relative Änderungen des dynamischen Stimmhöhenumfangs
      im Rahmen von unproblematischen Grenzwerten. Das Herauf- oder Herabsetzen
      des Stimmhöhenumfangs macht den Sprechstil mehr oder weniger expressiv. Das Attribut ist dem Attribut <code>range</code> des SSML-Elements
      <code>&lt;prosody&gt;</code> entlehnt.</td>
  </tr>
  <tr>
    <td><code>glottal_tension</code></td>
    <td style="text-align:center">[-100%, 100%],<br/>
      [<code>x-low</code>, <code>low</code>, <code>default</code>,
      <code>high</code>, <code>x-high</code>]</td>
    <td>
      Normalisiert relative Änderungen des Glottisdrucks
      im Rahmen von unproblematischen Grenzwerten. Ein Herauf- oder Herabsetzen
      des Glottisdrucks wird als verstärkte Anspannung oder Entspannung
      wahrgenommen. Ein positiver Wert erzeugt unter Umständen einen
      schnarrenden Klang, den Sie abschwächen können, indem Sie den Wert des
      Attributs <code>breathiness</code> verringern. Ein negativer Wert wird
      als stärker aspiriert und generell angenehmer empfunden.
    </td>
  </tr>
  <tr>
    <td><code>breathiness</code></td>
    <td style="text-align:center">[-100%, 100%],<br/>
      [<code>x-low</code>, <code>low</code>, <code>default</code>,
      <code>high</code>, <code>x-high</code>]</td>
    <td>
      Normalisiert relative Änderungen am wahrgenommenen Grad der
      Aspirationsgeräusche im Rahmen von unproblematischen Grenzwerten. Extreme
      Werte erzeugen unter Umständen entweder eine laute Sprache (positive
      Aspiration) oder einen schnarrenden Klang (negative Aspiration). Mit
      diesem Attribut können Sie das Schnarren oder die zusätzliche Lautstärke
      kompensieren, das/die als Nebeneffekt anderer Attribute entsteht.
    </td>
  </tr>
  <tr>
    <td><code>rate</code></td>
    <td style="text-align:center">[-100%, 100%],<br/>
      [<code>x-slow</code>, <code>slow</code>, <code>default</code>,
      <code>fast</code>, <code>x-fast</code>]</td>
    <td>
      Normalisiert relative Änderungen des Sprechtempos
      im Rahmen von unproblematischen Grenzwerten.
      Durch ein Herauf- oder
      Herabsetzen des Tempos wird die Sprache schneller oder langsamer.
      Ein positives (schnelleres) Tempo vergrößert den wahrgenommenen
      Tonhöhenbereich; ein negatives (langsameres) Tempo schränkt den
      wahrgenommenen Tonhöhenbereich ein.
      Das Attribut ist dem Attribut
      <code>rate</code> des SSML-Elements <code>&lt;prosody&gt;</code> entlehnt.</td>
  </tr>
  <tr>
    <td><code>timbre</code></td>
    <td style="text-align:center">[<code>Sunrise</code>,
      <code>Breeze</code>]</td>
    <td>
      Der Name (mit Beachtung der Groß- und Kleinschreibung) für eine der
      integrierten Umwandlungen für den Stimmweg: <code>Sunrise</code> oder
      <code>Breeze</code>.
      Die Namen sind symbolisch. Experimentieren
      Sie mit den Timbres, um ihren Einfluss auf die Stimmenumwandlung
      kennenzulernen. Dieses Attribut trägt dazu bei, die wahrgenommene
      Identität des Sprechers zu ändern.
    </td>
  </tr>
  <tr>
    <td><code>timbre_extent</code></td>
    <td style="text-align:center">[0%, 100%]</td>
    <td>
      Der Grad für die Umwandlung der Stimmfarbe durch <code>timbre</code>:
      <code>0%</code> storniert die Umwandlung; bei <code>100%</code>
      wird die Umwandlung vollständig angewendet. Das Attribut
      quantifiziert den Unterschied zwischen der umgewandelten und der
      ursprünglichen Stimme. Es ermöglicht eine Überblendung des ausgewählten
      Timbres mit dem Timbre der Originalstimme. Selbst bei moderaten Werten
      für den Umfang des Timbres trägt das Attribut <code>timbre</code>
      dazu bei, die wahrgenommene Identität des Sprechers zu ändern.
    </td>
  </tr>
</table>

### Bereichswerte verwenden
{: #ranges}

Die numerischen Bereiche der unterschiedlichen Attribute geben an, in welchem Maß das Attribut die Stimme beeinflusst. Beispielsweise besitzt das Attribut `rate` einen Bereich von -100% bis 100%:

-   Der Wert `100%` bedeutet nicht, dass die Stimme 100% schneller wird. Er bedeutet vielmehr, dass der Service das Sprechtempo auf das zulässige Maximum für diese Stimme erhöht.
-   Der Wert `-100%` bedeutet, dass der Service das zulässige Mindesttempo für diese Stimme verwendet.
-   Der Wert `0%` stellt das Basisniveau des Attributs für die Stimme dar; bei seiner Verwendung wird die Stimme nicht geändert.

### Literalwerte verwenden
{: #literals}

Zur Steigerung des Benutzerkomforts sind für viele Attribute ebenfalls Literalwerte definiert, die anstelle von Prozentsätzen verwendet werden können. Die Bedeutungen dieser Werte weichen von denen der Werte ab, die beim SSML-Element `<prosody>` verwendet werden. Das Element `<voice-transformation>` verwendet eine Skala, die bei allen seinen Attributen konsistent ist.

-   `x-low`, `x-slow` und `x-narrow` entsprechen dem Wert `-100%`.
-   `low`, `slow` und `narrow` entsprechen dem Wert `-50%`.
-   `default` entspricht dem Wert `0%`, also dem Standardwert für dieses Attribut und diese Stimme.
-   `high`, `fast` und `wide` entsprechen dem Wert `+50%`.
-   `x-high`, `x-fast` und `x-wide` entsprechen dem Wert `+100%`.

### Verwendungsrichtlinien
{: #guidelines}

Beachten Sie die folgenden Richtlinien und Warnhinweise:

-   Verwenden Sie für die Kennzeichnung durch Sprache oder für Anwendungen mit mehreren Rollen die Attribute `timbre`, `pitch` und `glottal_tension`, um die wahrgenommene Identität des Sprechers zu ändern. Sie können diese drei Attribute kombinieren, um virtuelle Stimmen zu erzeugen. Eine virtuelle Stimme ist mit einem Punkt in dem mehrdimensionalen Bereich vergleichbar, der durch die Angaben für Timbre, Tonhöhe und Glottisdruck erzielt wird. Unterschiedliche Kombinationen der Attribute ergeben unterschiedliche virtuelle Stimmen.
-   Mit den Attributen `pitch_range`, `breathiness` und `rate` können Sie einer virtuellen Stimme eine bestimmte Ausstrahlung verleihen. Andere Benutzer können dieselben oder ähnliche Attributwerte auswählen, so dass der Service die Eindeutigkeit Ihrer virtuellen Stimme nicht garantieren kann.
-   Bedenken Sie bei der Anwendung der Attribute die folgenden möglichen Nebeneffekte:
    -   Hoher Glottisdruck, große Tonhöhe und geringes Tempo können das Auftreten von Schnarrgeräuschen verursachen. Setzen Sie den Wert für die Aspiration herauf, um den Effekt abzuschwächen.
    -   Ein extrem niedriger Glottisdruck kann zu undeutlicher Sprache führen. Setzen Sie die Aspiration herab, um diese Störung zu reduzieren.
    -   Die gleichzeitige Anhebung oder Verringerung des Tonhöhenbereichs und des Tempos auf extreme Werte kann dazu führen, dass die Stimme unnatürlich klingt.
-   Wie bereits angegeben, wurden einige Attribute dem SSML-Element `<prosody>` entlehnt. Weitere Informationen enthält der Abschnitt [Element 'prosody'](/docs/services/text-to-speech?topic=text-to-speech-elements#prosody_element). Mit den folgenden Maßnahmen können Sie eine differenzierte Steuerung der Prosodie für eine virtuelle Stimme erreichen:
    -   Verschachteln Sie Elemente `<prosody>` in Elementen `<voice-transformation>`.
    -   Verschachteln Sie Elemente `<voice-transformation>` in Elementen `<prosody>`.

    Elemente `<voice-transformation>` können *nicht* verschachtelt werden.

## Beispiele für angepasste Umwandlungen
{: #ssml-custom-transforms-examples}

In den folgenden Beispielen werden verschiedene Attribute angewendet, um die Anwendungsmöglichkeiten der angepassten Umwandlung zu veranschaulichen. Beim ersten Beispiel wird der Glottisdruck verringert, damit die Stimme weicher klingt. Außerdem werden der Tonhöhenbereich und das Tempo moderat erhöht, um einen dynamischeren Sprechstil zu erzielen.

```xml
<voice-transformation type="Custom" glottal_tension="-50%"
  pitch_range="30%" rate="10%">
  Do you have more information?
</voice-transformation>
```
{: codeblock}

Im zweiten Beispiel werden die maximalen Werte für Glottisdruck und Tonhöhe mit dem minimal möglichen Tempo kombiniert. Solche Kombinationen sind generell nicht vorteilhaft und können einen schnarrenden Ton verursachen. Beim Beispiel wird dieser Effekt durch die Erhöhung der Aspiration gemindert.

```xml
<voice-transformation type="Custom" glottal_tension="100%" pitch="100%"
  rate="-100%" breathiness="60%">
  Do you have more information?
</voice-transformation>
```
{: codeblock}

In den nächsten beiden Beispielen wird die wahrgenommene Identität des Sprechers durch eine Anwendung des Timbres geändert. Die Stimme wird durch die Steuerung des Überblendungsgrades und die Änderung des Tonhöhenniveaus geändert. Im ersten Beispiel wird der Standardumfang 100% für das Timbre verwendet.

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

Beim letzten Beispiel werden mehrere Attribute eingesetzt, um die Stimme umzuwandeln. Im Beispiel wird der Standardumfang für das Timbre verwendet und die Aspiration ist nicht angegeben.

```xml
<voice-transformation type="Custom" timbre="Sunrise" pitch="-30%"
  pitch_range="80%" rate="60%" glottal_tension="-80%">
  Do you have more information?
</voice-transformation>
```
{: codeblock}
