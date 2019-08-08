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

# SSML-Elemente
{: #elements}

Beim {{site.data.keyword.texttospeechfull}}-Service können Sie die meisten Elemente von SSML (Speech Synthesis Markup Language) verwenden, um die Sprachsynthese für Ihren Text zu steuern. Die Elemente sind für alle unterstützten Sprachen verfügbar. Die folgende Tabelle vermittelt Ihnen einen Überblick über die Unterstützung des Service für SSML-Elemente und -Attribute.

-   *Vollständig* bedeutet, dass der Service das Element oder Attribut bei seiner HTTP- und WebSocket-Schnittstelle vollumfänglich unterstützt.
-   *Teilweise* bedeutet, dass der Service nicht alle Aspekte des Elements oder Attributs unterstützt. Dies kann auch bedeuten, dass der Service das Element bzw. Attribut nur bei einer seiner Schnittstellen unterstützt oder dass das Element bzw. Attribut nicht bei allen Stimmen unterstützt wird.
-   *Keine* bedeutet, dass der Service das Element oder Attribut nicht unterstützt.

Weitere Informationen zu einem Element oder Attribut finden Sie in der zugehörigen Beschreibung. Bei einigen Attributen und Werten unterscheidet sich die Unterstützung etwas von der SSML-Spezifikation; solche Fälle sind entsprechend gekennzeichnet. Zusätzliche Angaben sind auf der Seite [W3C Speech Synthesis Markup Language (SSML) Version 1.0](http://www.w3.org/TR/speech-synthesis/){: external}.

<table>
  <caption>Tabelle 1. SSML-Elemente</caption>
  <tr>
    <th style="text-align:left; width:30%">Element oder Attribut</th>
    <th style="text-align:center; width:12%">Unterstützung</th>
    <th style="text-align:left; width:46%; padding-left:75px">Element oder Attribut</th>
    <th style="text-align:center; width:12%">Unterstützung</th>
  </tr>
  <tr>
    <td>[audio](#audio_element)</td>
    <td style="text-align:center">Keine</td>
    <td style="padding-left:75px">[say-as](#say-as_element)</td>
    <td style="text-align:center">Teilweise</td>
  </tr>
  <tr>
    <td>[break](#break_element)</td>
    <td style="text-align:center">Vollständig</td>
    <td style="padding-left:100px">[cardinal](#sayAsCardinal)</td>
    <td style="text-align:center">Teilweise</td>
  </tr>
  <tr>
    <td>[desc](#desc_element)</td>
    <td style="text-align:center">Keine</td>
    <td style="padding-left:100px">[date](#sayAsDate)</td>
    <td style="text-align:center">Teilweise</td>
  </tr>
  <tr>
    <td>[emphasis](#emphasis_element)</td>
    <td style="text-align:center">Keine</td>
    <td style="padding-left:100px">[digits](#sayAsDigits)</td>
    <td style="text-align:center">Teilweise</td>
  </tr>
  <tr>
    <td>[lexicon](#lexicon_element)</td>
    <td style="text-align:center">Keine</td>
    <td style="padding-left:100px">[letters](#sayAsLetters)</td>
    <td style="text-align:center">Teilweise</td>
  </tr>
  <tr>
    <td>[mark](#mark_element)</td>
    <td style="text-align:center">Teilweise</td>
    <td style="padding-left:100px">[number](#sayAsNumber)</td>
    <td style="text-align:center">Teilweise</td>
  </tr>
  <tr>
    <td>[meta](#mm_element)</td>
    <td style="text-align:center">Keine</td>
    <td style="padding-left:125px">cardinal</td>
    <td style="text-align:center">Teilweise</td>
  </tr>
  <tr>
    <td>[metadata](#mm_element)</td>
    <td style="text-align:center">Keine</td>
    <td style="padding-left:125px">ordinal</td>
    <td style="text-align:center">Teilweise</td>
  </tr>
  <tr>
    <td>[paragraph](#ps_element)</td>
    <td style="text-align:center">Vollständig</td>
    <td style="padding-left:125px">telephone</td>
    <td style="text-align:center">Teilweise</td>
  </tr>
  <tr>
    <td>[phoneme](#phoneme_element)</td>
    <td style="text-align:center">Vollständig</td>
    <td style="padding-left:150px">punctuation</td>
    <td style="text-align:center">Teilweise</td>
  </tr>
  <tr>
    <td style="padding-left:25px">IBM SPR</td>
    <td style="text-align:center">Vollständig</td>
    <td style="padding-left:100px">[ordinal](#sayAsOrdinal)</td>
    <td style="text-align:center">Teilweise</td>
  </tr>
  <tr>
    <td style="padding-left:25px">IPA</td>
    <td style="text-align:center">Vollständig</td>
    <td style="padding-left:100px">[vxml:boolean](#vxml-boolean)</td>
    <td style="text-align:center">Teilweise</td>
  </tr>
  <tr>
    <td>[prosody](#prosody_element)</td>
    <td style="text-align:center">Teilweise</td>
    <td style="padding-left:100px">[vxml:currency](#vxml-currency)</td>
    <td style="text-align:center">Teilweise</td>
  </tr>
  <tr>
    <td style="padding-left:25px">contour</td>
    <td style="text-align:center">Keine</td>
    <td style="padding-left:100px">[vxml:date](#vxml-date)</td>
    <td style="text-align:center">Teilweise</td>
  </tr>
  <tr>
    <td style="padding-left:25px">duration</td>
    <td style="text-align:center">Keine</td>
    <td style="padding-left:100px">[vxml:digits](#vxml-digits)</td>
    <td style="text-align:center">Teilweise</td>
  </tr>
  <tr>
    <td style="padding-left:25px">[pitch](#prosody-pitch)</td>
    <td style="text-align:center">Vollständig</td>
    <td style="padding-left:100px">[vxml:phone](#vxml-phone)</td>
    <td style="text-align:center">Teilweise</td>
  </tr>
  <tr>
    <td style="padding-left:25px">range</td>
    <td style="text-align:center">Keine</td>
    <td style="padding-left:75px">[sentence](#ps_element)</td>
    <td style="text-align:center">Vollständig</td>
  </tr>
  <tr>
    <td style="padding-left:25px">[rate](#prosody-rate)</td>
    <td style="text-align:center">Vollständig</td>
    <td style="padding-left:75px">[speak](#speak_element)</td>
    <td style="text-align:center">Vollständig</td>
  </tr>
  <tr>
    <td style="padding-left:25px">[volume](#prosody-volume)</td>
    <td style="text-align:center">Teilweise</td>
    <td style="padding-left:75px">[sub](#sub_element)</td>
    <td style="text-align:center">Vollständig</td>
  </tr>
  <tr>
    <td></td>
    <td></td>
    <td style="padding-left:75px">[voice](#voice_element)</td>
    <td style="text-align:center">Keine</td>
  </tr>
</table>

## Element 'audio'
{: #audio_element}

Dieses Element `<audio>` fügt aufgezeichnete Elemente in die vom Service generierte Audioausgabe ein. Es wird nicht unterstützt.

## Element 'break'
{: #break_element}

Das Element `<break>` fügt eine Pause in den gesprochenen Text ein. Es besitzt die folgenden optionalen Attribute:

-   Das Attribut `strength` gibt die Länge der Pause in Form von unterschiedlichen Werten an:
    -   `none` unterdrückt eine Pause, die ansonsten möglicherweise während der Verarbeitung entsteht.
    -   `x-weak`, `weak`, `medium`, `strong` oder `x-strong` fügen in der hier angegebenen Reihenfolge immer längere Pausen ein.
-   Das Attribut `time` gibt die Länge der Pause in Form von Sekunden oder Millisekunden an. Gültige Werteformate sind `{ganzzahl}s` für Sekunden oder `{ganzzahl}ms` für Millisekunden.

```xml
<speak version="1.0">
  Größenunterschied <break strength="none">keine Pause</break>
  Größenunterschied <break strength="x-weak">kürzeste Pause</break>
  Größenunterschied <break strength="weak">kurze Pause</break>
  Größenunterschied <break strength="medium">mittlere Pause</break>
  Größenunterschied <break strength="strong">lange Pause</break>
  Größenunterschied <break strength="x-strong">längste Pause</break>
  Größenunterschied <break time="1s">einsekündige Pause</break>
  Größenunterschied <break time="1500ms">1500-millisekündige Pause</break>
</speak>
```
{: codeblock}

## Element 'desc'
{: #desc_element}

Das Element `<desc>` kann nur innerhalb eines Elements `<audio>` verwendet werden. Da das Element `<audio>` nicht unterstützt wird, wird auch das Element `<desc>` nicht unterstützt.

## Element 'emphasis'
{: #emphasis_element}

Das Element `<emphasis>` fordert an, dass der eingeschlossene Text beim Sprechen besonders betont wird. Es wird nicht unterstützt.

## Element 'lexicon'
{: #lexicon_element}

Dieses Element `<lexicon>` führt Wortausspracheverzeichnisse für das angegebene SSML-Dokument ein. Es wird nicht unterstützt.

In der Anpassungsschnittstelle des Service können Sie ein Wörterverzeichnis mit angepassten Einträgen (Paare aus Wort und Umsetzung) definieren, das während der Sprachsynthese verwendet werden soll. Weitere Informationen enthält der Abschnitt [Wissenswertes über die Anpassung](/docs/services/text-to-speech?topic=text-to-speech-customIntro).

## Element 'mark'
{: #mark_element}

Das Element `<mark>` wird nur durch die WebSocket-Schnittstelle des Service unterstützt. Von der HTTP-Schnittstelle wird das Element nicht unterstützt und ignoriert. Weitere Informationen finden Sie unter [SSML-Markup eingeben](/docs/services/text-to-speech?topic=text-to-speech-timing#mark).
{: note}

Das Element `<mark>` ist ein leeres Element, das eine Markierung in dem Text setzt, aus dem synthetisch Sprache erstellt werden soll. Der Client wird benachrichtigt, sobald aus dem gesamten Text, der dem Element `<mark>` vorangeht, synthetisch Sprache erstellt worden ist. Das Element akzeptiert ein einziges Attribut `name`, in dem eine Zeichenfolge angegeben ist, die die Markierung eindeutig kennzeichnet; der Name muss mit einem alphanumerischen Zeichen beginnen. Der Name wird zusammen mit dem Zeitpunkt zurückgegeben, an dem die Markierung in der synthetisch erstellten Audioausgabe vorkommt.

```xml
<speak version="1.0">
  Hello <mark name="here"/> world.
</speak>
```
{: codeblock}

## Elemente 'meta' und 'metadata'
{: #mm_element}

Die Elemente `<meta>` und `<metadata>` sind Container, in denen Sie Informationen zum Dokument angeben können. Sie werden nicht unterstützt.

## Elemente 'paragraph' und 'sentence'
{: #ps_element}

Die Elemente `<paragraph>` (bzw. `<p>`) und `<sentence>` (bzw. `s`) sind optionale Elemente, mit denen Hinweise zur Textstruktur gegeben werden können. Falls der in einem Element `<paragraph>` oder `<sentence>` eingeschlossene Text nicht mit einem Interpunktionszeichen für das Ende eines Satzes (z. B. einem Punkt) aufhört, fügt der Service der synthetisch erstellten Audioausgabe eine längere Pause als gewöhnlich hinzu.

Das einzige gültige Attribut für beide Elemente ist `xml:lang`; es ermöglicht einen Wechsel der Sprache. Das Attribut wird nicht unterstützt.

```xml
<speak version="1.0">
  <paragraph>
    <sentence>Text in einem Element 'sentence'.</sentence>
    <s>Weiterer Text in einem anderen Element 'sentence'.</s>
  </paragraph>
</speak>
```
{: codeblock}

## Element 'phoneme'
{: #phoneme_element}

Das Element `<phoneme>` stellt eine phonetische Aussprache für den eingeschlossenen Text bereit. Die phonetische Schreibweise stellt dar, aus welchen Lauten ein Wort besteht, wie die Laute in Silben unterteilt sind und welche Silben betont werden. Das Element besitzt zwei Attribute:

-   Das optionale Attribut `alphabet` gibt an, welche Phonetik verwendet werden soll. Die folgenden Alphabete werden unterstützt:
    -   Standard 'IPA' (International Phonetic Alphabet): `alphabet="ipa"`
    -   {{site.data.keyword.IBM_notm}} SPR (Symbolic Phonetic Representation): `alphabet="ibm"`

    Wenn kein Alphabet angegeben ist, verwendet der Service standardmäßig IBM SPR.
-   Das erforderliche Attribut `ph` stellt die Aussprache im angegebenen Alphabet bereit. Die folgenden Beispiele zeigen die Aussprache für das Wort *tomato* in beiden Formaten:

    -   IPA-Format:

        <pre><code>&lt;speak version="1.0"&gt;
          &lt;phoneme alphabet="ipa" ph="t&#601;&#712;me&#618;.&#638;o&#650;"&gt;tomato&lt;/phoneme&gt;
        &lt;/speak&gt;</code></pre>

    -   IPA-Format mit Unicode-Symbolen:

        <pre><code>&lt;speak version="1.0"&gt;
          &lt;phoneme alphabet="ipa" ph="t&amp;&#35;x259;mei&amp;&#35;x027E;o&amp;&#035;x028A;"&gt;tomato&lt;/phoneme&gt;
        &lt;/speak&gt;</code></pre>

    -   IBM SPR-Format:

        <pre><code>&lt;speak version="1.0"&gt;
          &lt;phoneme alphabet="ibm" ph=".0tx.1me.0Fo"&gt;tomato&lt;/phoneme&gt;
        &lt;/speak&gt;</code></pre>

Näheres über die Verwendung der SPR- und IPA-Schreibweise beim Element `<phoneme>` finden Sie unter [IBM SPR verwenden](/docs/services/text-to-speech?topic=text-to-speech-sprs).

## Element 'prosody'
{: #prosody_element}

Das Element `<prosody>` steuert die Tonhöhe, das Sprechtempo und die Lautstärke des Textes. Alle Attribute sind optional, aber falls kein Attribut angegeben ist, tritt ein Fehler auf. Die SSML-Spezifikation lässt drei Attribute zu, die vom Service nicht unterstützt werden: `contour`, `range` und `duration`. Der Service unterstützt die Attribute `pitch`, `rate` und `volume`.

### Attribut 'pitch'
{: #prosody-pitch}

Das Attribut `pitch` ändert die Grundtonhöhe für den Text innerhalb des Elements. Gültige Werte:

-   Zahl gefolgt von der Bezeichnung `Hz` (Hertz): Hierbei wird die Grundtonhöhe um den angegebenen Wert transponiert (aufwärts oder abwärts).
-   Relativer Änderungswert (in Halbtönen): Eine Zahl, die eine absolute Verschiebung vom aktuellen Grundniveau bewirkt. Der Zahl geht das Zeichen `+` (Erhöhung) oder `-` (Absenkung) voran; auf sie folgt die Angabe `st` (für 'semitones' = Halbtöne). Beispiel: `+5st`.
-   Relativer Änderungswert in Prozent: Eine Zahl, die eine relative Verschiebung vom aktuellen Grundniveau bewirkt. Der Zahl geht das Zeichen `+` (Erhöhung) oder `-` (Absenkung) voran; auf sie folgt `%` (Prozentzeichen). Beispiel: `-10%`.
-   1 der folgenden sechs Schlüsselwörter, die die Tonhöhe in die entsprechenden vordefinierten Werte ändern:
    -   `default` verwendet die Standardgrundtonhöhe des Service.
    -   `x-low` verschiebt die Grundtonhöhe um 12 Halbtöne nach unten.
    -   `low` verschiebt die Grundtonhöhe um sechs Halbtöne nach unten.
    -   `medium` erzeugt dasselbe Verhalten wie `default`.
    -   `high` verschiebt die Grundtonhöhe um sechs Halbtöne nach oben.
    -   `x-high` verschiebt die Grundtonhöhe um zwölf Halbtöne nach oben.

    ```xml
    <speak version="1.0">
      <prosody pitch="150Hz">Tonhöhe auf 150 Hz transponieren</prosody>
      <prosody pitch="-20Hz">Tonhöhe von Grundniveau um 20 Hz absenken</prosody>
      <prosody pitch="+20Hz">Tonhöhe von Grundniveau um 20 Hz anheben</prosody>
      <prosody pitch="-12st">Tonhöhe um 12 Halbtöne von Grundniveau absenken</prosody>
      <prosody pitch="+12st">Tonhöhe um 12 Halbtöne von Grundniveau anheben</prosody>
      <prosody pitch="x-low">Tonhöhe um 12 Halbtöne von Grundniveau absenken</prosody> </speak>
    ```
    {: codeblock}

### Attribut 'rate'
{: #prosody-rate}

Das Attribut `rate` ändert das Sprechtempo für den Text innerhalb des Elements. Der Wert für das Tempo wird in Wörtern pro Minute ausgedrückt; falls das Sprechtempo 50 Wörter pro Minute beträgt, hat das Attribut `rate` den Wert `50`. Wenn für das Attribut `rate` eine positive Zahl angegeben ist, hält die Implementierung die aktuelle W3C-Spezifikation für das Attribut 'rate' des Elements 'prosody'  nicht ein. Außerdem unterstützt der Service relative prozentuale Änderungen (z. B. `+15%`), jedoch keine relativen Wertänderungen (z. B. `+15`). Gültige Werte:

-   Relativer Prozentsatz für Erhöhung oder Verringerung: `+10%`.
-   Anzahl von Wörtern pro Minute als positive Zahl: `75`.
-   `default` verwendet das Standardtempo des Service.
-   `x-slow` verringert das Tempo um 50 Prozent.
-   `slow` verringert das Tempo um 25 Prozent.
-   `medium` erzeugt dasselbe Verhalten wie `default`.
-   `fast` erhöht das Tempo um 25 Prozent.
-   `x-fast` erhöht das Tempo um 50 Prozent.

```xml
<speak version="1.0">
  <prosody rate="slow">Sprechtempo um 25% verringern</prosody>
  <prosody rate="50">Sprechtempo mit 50 Wörtern pro Minute festlegen</prosody>
  <prosody rate="+5%">Sprechtempo um 5 Prozent erhöhen</prosody>
</speak>
```
{: codeblock}

### Attribut 'volume'
{: #prosody-volume}

Der Service unterstützt nicht das Attribut `volume` des Elements `<prosody>` mit seinen neuronalen Stimmen (z. B. `en-US_AllisonV3Voice`). Weitere Informationen finden Sie unter [Neuronale Stimmen](/docs/services/text-to-speech?topic=text-to-speech-voices#neuralVoices).
{: note}

Das Attribut `volume` ändert die Lautstärke für den Text innerhalb des Elements. Sie können eine ganze Zahl oder einen Dezimalwert im Bereich von 1,0 bis 100,0 (maximale Lautstärke) angeben. Sie können auch einen der folgenden Zeichenfolgewerte verwenden, die vordefinierten Einstellungen im Bereich von 0 bis 100 entsprechen. (Der Wert `silent` wird nicht unterstützt.)

-   `x-soft` hat den Wert 30.
-   `soft` hat den Wert 50.
-   `medium` hat den Wert 80.
-   `loud` hat den Wert 90.
-   `default` hat den Wert 92.
-   `x-loud` hat den Wert 100.

```xml
<speak version="1.0">
  <prosody volume="75">Geänderte Lautstärke ist 75</prosody>
  <prosody volume="88.9">Geänderte Lautstärke ist 88,9</prosody>
  <prosody volume="loud">Geänderte Lautstärke ist 90</prosody> </speak>
```
{: codeblock}

## Element 'say-as'
{: #say-as_element}

Das Element `<say-as>` wird bei den meisten Sprachen nur teilweise unterstützt. Bei anderen Sprachen als amerikanischem Englisch unterstützt der Service normalerweise nur die Attribute `digits` und `letters` des Elements.
{: note}

Das Element `<say-as>` stellt Informationen zu dem Texttyp bereit, der im Element enthalten ist, und gibt den Detaillierungsgrad für die Wiedergabe des Textes an. Das Element besitzt ein erforderliches Attribut namens `interpret-as`, mit dem angegeben wird, wie der eingeschlossene Text zu interpretieren ist. Es besitzt zwei optionale Attribute namens `format` und `detail`, die wie in den folgenden Beispielen gezeigt nur für bestimmte Werte innerhalb des Attributs `interpret-as` verwendet werden.

Nachfolgend sind die gültigen Werte für das Attribut `interpret-as` mit zugehörigen Beispielen aufgeführt.

### Wert 'cardinal'
{: #sayAsCardinal}

Der Wert `cardinal` bewirkt das Sprechen der Kardinalzahl für die Ziffer im Element. Beim folgenden Beispiel wird *Super Bowl forty-nine* gesprochen. Die erste Angabe ist überflüssig, weil das Standardverhalten des Service nicht geändert wird.

```xml
<speak version="1.0">
  Super Bowl <say-as interpret-as="cardinal">49</say-as>
  Super Bowl <say-as interpret-as="cardinal">XLIX</say-as>
</speak>
```
{: codeblock}

### Wert 'date'
{: #sayAsDate}

Der Wert `date` führt dazu, dass das Datum im Element gemäß dem Format gesprochen wird, das im zugehörigen Attribut `format` angegeben ist. Das Attribut `format` ist für den Wert `date` erforderlich. Falls kein Attribut `format` vorhanden ist, versucht der Service trotzdem, das Datum zu sprechen. Bei den folgenden Beispielen werden die angegebenen Datumsangaben in den angegebenen Formaten gesprochen; hierbei stehen `d`, `m` und `y` für den Tag, den Monat und das Jahr.

```xml
<speak version="1.0">
  <say-as interpret-as="date" format="mdy">12/17/2005</say-as>
  <say-as interpret-as="date" format="ymd">2005/12/17</say-as>
  <say-as interpret-as="date" format="dmy">17/12/2005</say-as>
  <say-as interpret-as="date" format="ydm">2005/17/12</say-as>
  <say-as interpret-as="date" format="my">12/2005</say-as>
  <say-as interpret-as="date" format="md">12/17</say-as>
  <say-as interpret-as="date" format="ym">2005/12</say-as>
</speak>
```
{: codeblock}

### Wert 'digits'
{: #sayAsDigits}

Der Wert `digits` bewirkt, dass die Ziffern in der Zahl gesprochen werden, die im Element enthalten ist. Beim folgenden Beispiel werden die einzelnen Ziffern *123456* gesprochen.

```xml
<speak version="1.0">
  <say-as interpret-as="digits">123456</say-as>
</speak>
```
{: codeblock}

### Wert 'letters'
{: #sayAsLetters}

Der Wert `letters` bewirkt, dass das im Element enthaltene Wort buchstabiert wird. Beim folgenden Beispiel wird das Wort *Hello* buchstabiert.

```xml
<speak version="1.0">
  <say-as interpret-as="letters">Hello</say-as>
</speak>
```
{: codeblock}

### Wert 'number'
{: #sayAsNumber}

Der Wert `number` bietet eine Alternative zu den Werten `cardinal` und `ordinal`. Mit dem optionalen Attribut `format` können Sie angeben, wie eine Reihe von Zahlen interpretiert werden soll. Beim ersten Beispiel ist das Attribut `format` nicht angegeben, damit die Zahl als Kardinalzahl gesprochen wird. Im zweiten Beispiel ist explizit angegeben, dass die Zahl als Kardinalzahl auszusprechen ist (durch den Wert `cardinal`). Das dritte Beispiel gibt an, dass die Zahl als Ordinalzahl zu sprechen ist (Wert `ordinal`).

```xml
<speak version="1.0">
  <say-as interpret-as="number">123456</say-as>
  <say-as interpret-as="number" format="cardinal">123456</say-as>
  <say-as interpret-as="number" format="ordinal">123456</say-as>
</speak>
```
{: codeblock}

Für das Attribut `format` können Sie auch den Wert `telephone` angeben. Die folgenden Beispiele zeigen verschiedene Möglichkeiten zum Sprechen einer Reihe von Zahlen als Telefonnummern. Damit die Zahlen inklusive der Interpunktion gesprochen werden, geben Sie den Wert `punctuation` für das optionale Attribut `detail` an.

```xml
<speak version="1.0">
  <say-as interpret-as="number" format="telephone">555-555-5555</say-as>
  <say-as interpret-as="number" format="telephone" detail="punctuation">555-555-5555</say-as>
</speak>
```
{: codeblock}

### Wert 'ordinal'
{: #sayAsOrdinal}

Der Wert `ordinal` bewirkt, dass die Ziffer innerhalb des Elements als Ordinalzahl gesprochen wird. Im folgenden Beispiel wird *second first* gesprochen.

```xml
<speak version="1.0">
  <say-as interpret-as="ordinal">2</say-as>
  <say-as interpret-as="ordinal">1</say-as>
</speak>
```
{: codeblock}

### Wert 'vxml:boolean'
{: #vxml-boolean}

Der Wert `vxml:boolean` bewirkt, dass entweder *yes* oder *no* gesprochen wird (abhängig vom Wert `true` bzw. `false` im Element).

```xml
<speak version="1.0">
  <say-as interpret-as="vxml:boolean">true</say-as>
  <say-as interpret-as="vxml:boolean">false</say-as>
</speak>
```
{: codeblock}

### Wert 'vxml:currency'
{: #vxml-currency}

Mit dem Wert `vxml:currency` wird die Sprachsynthese von Währungswerten gesteuert. Die Zeichenfolge muss im Format `UUUmm.nn` geschrieben sein, wobei `UUU` der dreistellige Währungsindikator gemäß dem ISO-Standard 4217 und `mm.nn` der Betrag ist. Im folgenden Beispiel wird *forty-five dollars and thirty cents* gesprochen.

```xml
<speak version="1.0">
  <say-as interpret-as="vxml:currency">USD45.30</say-as>
</speak>
```
{: codeblock}

Wenn die angegebene Zahl mehr als zwei Dezimalstellen umfasst, wird der Betrag synthetisch als Dezimalzahl gefolgt vom Währungsindikator erstellt. Falls der dreistellige Währungsindikator nicht vorhanden ist, wird der Betrag nur als Dezimalzahl synthetisch erstellt und der Währungstyp wird nicht gesprochen. Beim folgenden Beispiel wird *forty-five point three two nine US dollars* gesprochen.

```xml
<speak version="1.0">
  <say-as interpret-as="vxml:currency">USD45.329</say-as>
</speak>
```
{: codeblock}

### Wert 'vxml:date'
{: #vxml-date}

Der Wert `vxml:date` hat dieselbe Funktionsweise wie der Wert `date`, das Format ist allerdings mit `JJJJMMTT` vordefiniert. Falls ein Wert für den Tag, den Monat oder das Jahr unbekannt ist oder nicht gesprochen werden soll, ersetzen Sie den Wert durch `?` (Fragezeichen). Im zweiten und dritten Beispiel werden Fragezeichen verwendet.

```xml
<speak version="1.0">
  <say-as interpret-as="vxml:date">20050720</say-as>
  <say-as interpret-as="vxml:date">????0720</say-as>
  <say-as interpret-as="vxml:date">200507??</say-as>
</speak>
```
{: codeblock}

### Wert 'vxml:digits'
{: #vxml-digits}

Der Wert `vxml:digits` bietet dieselbe Funktionsweise wie der Wert `digits`.

### Wert 'vxml:phone'
{: #vxml-phone}

Der Wert `vxml:phone` bewirkt, dass eine Telefonnummer sowohl mit Ziffern als auch mit Interpunktion gesprochen wird. Dies entspricht funktional der Verwendung des Wertes `number` unter Angabe von `telephone` für das Attribut `format` und `punctuation` für das Attribut `detail`.

```xml
<speak version="1.0">
  <say-as interpret-as="vxml:phone">555-555-5555</say-as>
</speak>
```
{: codeblock}

## Element 'speak'
{: #speak_element}

Das Element `<speak>` ist das Stammelement für SSML-Dokumente. Gültige Attribute:

-   Das erforderliche Attribut `version` gibt die SSML-Spezifikation an. Der gültige Wert ist `1.0`.
-   Das Attribut `xml:lang` wird vom Service nicht benötigt. Lassen Sie das Attribut bei Verwendung dieses Elements weg.
-   Das Attribut `xml:base` ist wirkungslos.

```xml
<speak version="1.0">
  Der zu sprechende Text.
</speak>
```
{: codeblock}

## Element 'sub'
{: #sub_element}

Das Element `sub` gibt an, dass der im Attribut `alias` angegebene Text bei der synthetischen Spracherstellung als Ersatz für den Text verwendet werden soll, der im Element eingeschlossen ist. Das Attribut `alias` ist das einzige Attribut des Elements und ist erforderlich.

```xml
<speak version="1.0">
  <sub alias="International Business Machines">IBM</sub>
</speak>
```
{: codeblock}

## Element 'voice'
{: #voice_element}

Dieses Element `<voice>` fordert eine Änderung der Stimme an. Es wird nicht unterstützt.
