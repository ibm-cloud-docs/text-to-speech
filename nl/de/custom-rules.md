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

# Regeln für die Erstellung von angepassten Einträgen
{: #rules}

Für das Bestücken eines angepassten Modells durch angepasste Einträge (also Paare aus Wort und Umsetzung) gelten die folgenden Regeln und Richtlinien.

## Maximale Anzahl angepasster Einträge

Ein einzelnes angepasstes Modell kann höchstens 20.000 angepasste Einträge umfassen.

## Zeichencodierung

Der Service akzeptiert Einträge für *Wörter* und *Umsetzungen* in ASCII- und UTF-8-Zeichencodierung. Verwenden Sie bei Umsetzungen in SPR-Schreibweise die ASCII-Codierung und bei Umsetzungen in IPA-Schreibweise die UTF-8-Codierung.

## Leerzeichen

Ein *Wort* kann kein Leerzeichen enthalten. Der Service verwendet Leerzeichen, um einzelne Wörter im Eingabetext darzustellen.

## Beachtung der Groß-/Kleinschreibung

Bei einem *Wort* muss die Groß-/Kleinschreibung beachtet werden. Angenommen, ein angepasstes Modell enthält beispielsweise den Eintrag `{word='Sun', translation='Sunday'}`. Der Service wendet auf das Wort `sun` die Standardaussprache an, aber die angepasste Umsetzung auf das Wort `Sun`, da nur dieses Wort mit einem Großbuchstaben beginnt.


## Kontextabhängigkeit

Bei einigen Wörtern sind die Aussprachevarianten kontextabhängig. Dies wird an der folgenden Beispieleingabe erläutert:

```
St. Anthony lives on Henry St.
```
{: codeblock}

Die Standardausspracheregeln des Service erstellen aus diesem Text ordnungsgemäß die folgende synthetische Sprache:

```
Saint Anthony lives on Henry Street
```
{: codeblock}

Falls Sie jedoch die Standardausspracheregeln für die Zeichenfolge `St.` überschreiben und sie mit `saint` umsetzen, kann der Service das Wort nicht mehr anhand des Kontextes aussprechen. Durch die Anwendung eines angepassten Sprechmodells, das eine solche Umsetzung enthält, spricht der Service die obige Eingabe wie folgt aus:

```
Saint Anthony lives on Henry saint
```
{: codeblock}

Berücksichtigen Sie solche Fälle bei der Entwicklung von Paaren aus Wort und Umsetzung.

## Abschließende Punkte

Der Service wendet ein Wort aus einem angepassten Modell nur auf diejenigen Zeichenfolgen im Eingabetext an, die exakt mit dem Wort übereinstimmen. Ein abschließender Punkt (`.`) in einem Worteintrag ändert die synthetische Erstellung des Wortes:

-   Ein *Wort ohne abschließenden Punkt* kann praktisch jedes beliebige Zeichen enthalten. Zu Zeichen gehören in diesem Zusammenhang Buchstaben, Ziffern, Interpunktionszeichen (mit Ausnahme eines abschließenden Punktes), weitere Symbole (z. B. %, &amp; und @), Anführungszeichen, runde Klammern, eckige Klammern usw. Die *Umsetzung* eines solchen Wortes kann jede für den Service gültige Eingabe enthalten, auch Leerzeichen und eine phonetische Darstellung im SSML-Format.
-   Ein *Wort mit abschließendem Punkt* kann ausschließlich Buchstaben, Punkte und integrierte Hochkommas (jedoch nicht als erstes oder letztes Zeichen) enthalten. Die *Umsetzung* eines solchen Wortes kann nur normale Wörter in herkömmlicher Schreibweise enthalten, die durch Leerzeichen oder Bindestriche voneinander abgegrenzt sind. Sie kann keine phonetische Darstellung enthalten.

Ein Beispiel für ein Wort mit einem abschließenden Punkt ist "`div.`". Angenommen, ein angepasstes Modell enthält den Eintrag `{word='div.', translation='division'}`. Der Service wendet in diesem Fall die Umsetzung  nicht auf die Zeichenfolge "`div`" an, weil sie keinen abschließenden Punkt umfasst und daher nicht mit dem Eintrag übereinstimmt.

## IBM SPR-Einträge bearbeiten
{: #sprNotes}

SPR (Symbolic Phonetic Representation) ist ein von {{site.data.keyword.IBM_notm}} entwickeltes eigenes und sprachenabhängiges Format zur Angabe der Aussprache für ein Wort. Für jede unterstützte Sprache enthält SPR ein Phonemalphabet, Symbole für Silbengrenzen sowie Symbole für den Betonungsgrad. Für die Erstellung von SPR-Einträgen gelten die folgenden Grundregeln:

-   Die Standardaussprache, die von der Anpassungsschnittstelle zurückgegeben wird, beginnt mit <code>&#96;</code> (umgekehrte Anführungszeichen) und ist in `[]` (eckige Klammern) eingeschlossen. Für das Wort `tomato` gibt die Schnittstelle beispielsweise die folgende Aussprache zurück:

    ```xml
    `[.0tx.1ma.0to]
    ```
    {: codeblock}

    Lassen Sie die umgekehrten Anführungszeichen und die eckigen Klammern weg, wenn Sie die Umsetzung eines Wortes mit den Methoden der Anpassungsschnittstelle angeben.
-   Mit einem Punkt können Sie den Beginn einer Silbe in einer Umsetzung kenntlich machen. Punkte sind jedoch optional und haben keinen Einfluss auf die Aussprache des Wortes. Sie treten bei der Aussprache für ein Wort nur dann in Erscheinung, wenn Sie sie in die Umsetzung des Wortes einbeziehen. Verwenden Sie keine Leerzeichen, um Silbengrenzen anzugeben.
-   {{site.data.keyword.IBM_notm}} empfiehlt, dem Vokal mit der Hauptbetonung für ein Wort das Symbol `1` voranzustellen; dies ist jedoch nicht zwingend erforderlich. Der Service ermittelt, wo die Betonung zu setzen ist, falls Sie sie nicht angeben. Mit einem Symbol `2` können Sie außerdem die Position für eine Nebenbetonung angeben, aber auch die Verwendung des Symbols `2` ist optional. Diese Symbole treten bei der Aussprache für ein Wort nur dann in Erscheinung, wenn Sie sie in die Umsetzung des Wortes einbeziehen.

Weitere Informationen zum Arbeiten mit SPR finden Sie im Abschnitt [IBM SPR verwenden](/docs/services/text-to-speech?topic=text-to-speech-sprs).

## Mit Einträgen in Japanisch arbeiten
{: #jaNotes}

Für die Erstellung von Einträgen für Wörter in einem angepassten Sprechmodell für Japanisch gibt es zusätzliche Regeln und ein Feld `part_of_speech`:

-   Eine gleich klingende Umsetzung kann ausschließlich *Katakana*-Zeichen enthalten. *Kanji*- und *Hiragana*-Zeichen sind nicht zulässig.
-   Wenn Sie eine (gleich klingende oder phonetische) Umsetzung für ein Wort erstellen, können Sie auch ein optionales Feld `part_of_speech` angeben, um die Wortart des Wortes zu benennen. Der Service erzeugt anhand der Wortart den korrekten Tonfall für das Wort. Eine vollständige Liste enthält der Abschnitt [Japanische Wortarten](#partsOfSpeech).
-   Für jedes Wort können Sie nur einen einzigen Eintrag erstellen und nur eine einzige Wortart angeben. Die Erstellung von mehreren Einträgen für dasselbe Wort mit unterschiedlichen Wortarten (z. B. Nomen und Verb) ist nicht möglich. Durch das Hinzufügen einer Umsetzung für ein Wort, das in einem Modell vorhanden ist, wird die vorhandene Umsetzung des Wortes einschließlich der Wortart überschrieben.
-   Der Service wendet das längste übereinstimmende Wort aus den Paaren für Wort und Umsetzung an, die für ein angepasstes Sprechmodell definiert sind. Nehmen wir beispielsweise an, ein angepasstes Modell enthält die drei folgenden Einträge:

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

    Im Zusammenhang mit diesen Einträgen empfängt der Service den folgenden Eingabetext: <code>&#19968;&#36913;&#38291;&#65326;&#65337;&#65315;&#12434;&#35370;&#21839;&#12375;&#12383;</code>. In diesem Fall ermittelt der Service eine Übereinstimmung für das Wort <code>&#65326;&#65337;&#65315;</code>, weil <code>&#65326;&#65337;&#65315;</code> länger ist als <code>&#65326;&#65337;</code> und weil die Übereinstimmung mit <code>&#65326;&#65337;&#65315;</code> vor der Übereinstimmung mit <code>&#65337;&#65315;</code> festgestellt wird.

### Japanische Wortarten
{: #partsOfSpeech}

In der folgenden Tabelle sind die Wortarten aufgelistet, die für angepasste Einträge in Japanisch unterstützt werden. Weitere Informationen zum Angeben einer Wortart für einen angepassten Eintrag in Japanisch enthält der Abschnitt [Wörter zu einem angepassten Modell für Japanisch hinzufügen](/docs/services/text-to-speech?topic=text-to-speech-customWords#cuJapaneseAdd).

<table style="width:75%">
  <caption>Tabelle 1. Japanische Wortarten</caption>
  <tr>
    <th style="text-align:center">Argument <code>part_of_speech</code></th>
    <th style="text-align:center; width:35%">Japanische Bedeutung</th>
    <th style="text-align:center; width:35%">Deutsche Bedeutung</th>
  </tr>
  <tr>
    <td style="text-align:center"><code>Josi</code></td>
    <td style="text-align:center"><em>Joshi</em></td>
    <td style="text-align:center">Partizip</td>
  </tr>
  <tr>
    <td style="text-align:center"><code>Mesi</code></td>
    <td style="text-align:center"><em>Meishi</em></td>
    <td style="text-align:center">Substantiv</td>
  </tr>
  <tr>
    <td style="text-align:center"><code>Kigo</code></td>
    <td style="text-align:center"><em>Kigou</em></td>
    <td style="text-align:center">Symbol</td>
  </tr>
  <tr>
    <td style="text-align:center"><code>Gobi</code></td>
    <td style="text-align:center"><em>Gobi</em></td>
    <td style="text-align:center">Flexion</td>
  </tr>
  <tr>
    <td style="text-align:center"><code>Dosi</code></td>
    <td style="text-align:center"><em>Doushi</em></td>
    <td style="text-align:center">Verb</td>
  </tr>
  <tr>
    <td style="text-align:center"><code>Jodo</code></td>
    <td style="text-align:center"><em>Jodoushi</em></td>
    <td style="text-align:center">Hilfsverb</td>
  </tr>
  <tr>
    <td style="text-align:center"><code>Koyu</code></td>
    <td style="text-align:center"><em>Koyuumeishi</em></td>
    <td style="text-align:center">Eigenname</td>
  </tr>
  <tr>
    <td style="text-align:center"><code>Stbi</code></td>
    <td style="text-align:center"><em>Setsubiji</em></td>
    <td style="text-align:center">Suffix</td>
  </tr>
  <tr>
    <td style="text-align:center"><code>Suji</code></td>
    <td style="text-align:center"><em>Suuji</em></td>
    <td style="text-align:center">Numeral</td>
  </tr>
  <tr>
    <td style="text-align:center"><code>Kedo</code></td>
    <td style="text-align:center"><em>Keiyodoushi</em></td>
    <td style="text-align:center">Verbaladjektiv</td>
  </tr>
  <tr>
    <td style="text-align:center"><code>Fuku</code></td>
    <td style="text-align:center"><em>Fukishi</em></td>
    <td style="text-align:center">Adverb</td>
  </tr>
  <tr>
    <td style="text-align:center"><code>Keyo</code></td>
    <td style="text-align:center"><em>Keiyoshi</em></td>
    <td style="text-align:center">Verbaladjektiv</td>
  </tr>
  <tr>
    <td style="text-align:center"><code>Stto</code></td>
    <td style="text-align:center"><em>Settoji</em></td>
    <td style="text-align:center">Präfix</td>
  </tr>
  <tr>
    <td style="text-align:center"><code>Reta</code></td>
    <td style="text-align:center"><em>Rentaishi</em></td>
    <td style="text-align:center">Determinativ</td>
  </tr>
  <tr>
    <td style="text-align:center"><code>Stzo</code></td>
    <td style="text-align:center"><em>Setsuzokushi</em></td>
    <td style="text-align:center">Konjunktion</td>
  </tr>
  <tr>
    <td style="text-align:center"><code>Kato</code></td>
    <td style="text-align:center"><em>Kantoushi</em></td>
    <td style="text-align:center">Interjektion</td>
  </tr>
  <tr>
    <td style="text-align:center"><code>Hoka</code></td>
    <td style="text-align:center"><em>Hoka</em></td>
    <td style="text-align:center">Sonstige</td>
  </tr>
</table>
