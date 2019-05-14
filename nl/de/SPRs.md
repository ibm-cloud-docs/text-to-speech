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

# IBM SPR verwenden
{: #sprs}

Der {{site.data.keyword.texttospeechfull}}-Service unterstützt für die schriftliche Abbildung der Laute von Wörtern als Schreibweise sowohl den Standard 'IPA' (International Phonetic Alphabet) als auch {{site.data.keyword.IBM}} Symbolic Phonetic Representation (SPR). SPR ist eine phonetische Codierung und stellt dar, wie ein Wort ausgesprochen wird, aus welchen Lauten ein Wort besteht, wie die Laute in Silben unterteilt werden und welche Silben betont sind. SPR ist eine Darstellungsalternative zu IPA.
{: shortdesc}

In den folgenden Abschnitten wird die Schreibweise gemäß {{site.data.keyword.IBM_notm}} SPR vorgestellt. Da es sich bei IPA um eine Standardschreibweise handelt, werden in der Dokumentation keine grundlegenden Nutzungsinformationen zu IPA bereitgestellt. Kurze Verwendungshinweise sind jedoch im Abschnitt [Mit IPA arbeiten](#ipa) zu finden.

## Einführung in IBM SPR
{: #introduction-SPRs}

Eine SPR-Aussprache wird mit dem Element `<phoneme>` von SSML (Speech Synthesis Markup Language) definiert; entsprechende Informationen finden Sie unter [Element 'phoneme'](/docs/services/text-to-speech/SSML-elements.html#phoneme_element). Sie besteht aus einer Abfolge mit zulässigen Symbolen für eine bestimmte Sprache, die in doppelte Anführungszeichen eingeschlossen ist. Die Symbole definieren, wie das im Element `<phoneme>` eingeschlossene Wort auszusprechen ist. Das Attribut `alphabet` des Elements macht durch den Wert `ibm` kenntlich, dass die Aussprache in SPR definiert ist, und das Attribut `ph` definiert die Aussprache. Die folgenden Beispiele zeigen gültige SPR-Schreibweisen für die Wörter *through* und *shocking* in amerikanischem Englisch:

```xml
<phoneme alphabet="ibm" ph=".1Tru">through</phoneme>
<phoneme alphabet="ibm" ph=".1Sa.0kIG">shocking</phoneme>
```
{: codeblock}

In den Definitionen signalisiert ein Punkt (`.`) den Beginn einer neuen Silbe. Die Ziffern `1` und `0` geben den Betonungsgrad der Silben an und die Buchstaben stellen bestimmte Laute der Sprache im amerikanischen Englisch dar. Ein SPR-Eintrag, der nicht der erforderlichen Spezifikation entspricht, ist ungültig.

## Silbengrenzen

Mit einem Punkt (`.`) können Sie den Anfang jeder Silbe kennzeichnen. Damit die gültige Phonetik einer Sprache erhalten bleibt, kann der Service jedoch in manchen Fällen eine Nichtbeachtung von Punkten vornehmen (wenn beispielsweise eine Silbengrenze an einer unzulässigen oder unnatürlichen Position für eine Sprache festgelegt ist). In Fällen, in denen der Benutzer eine gültige Vorgabe für eine Silbengrenze oder für einen anderen Aspekt der Aussprache eines Wortes festlegen kann, akzeptiert der Service im Allgemeinen solche Anforderungen.

## Silbenbetonung

Mit den Symbolen in der folgenden Tabelle können Sie die Silbenbetonung für eine Aussprache kennzeichnen. {{site.data.keyword.IBM_notm}} empfiehlt, die Hauptbetonung in SPR oder IPA anzugeben. Bei beiden Formaten ist die Angabe der Silbenbetonung jedoch optional; falls Sie keine Betonung angeben, legt der Service fest, wo die Betonung stattfindet.

<table style="width:80%">
  <caption>Tabelle 1. Silbenbetonung</caption>
  <tr>
    <th style="width:22%; text-align:center; vertical-align:bottom">
      Symbol in IBM SPR
    </th>
    <th style="width:22%; text-align:center; vertical-align:bottom">
      Symbol in IPA
    </th>
    <th style="width:22%; text-align:center; vertical-align:bottom">
      Unicode in IPA
    </th>
    <th style="text-align:left; vertical-align:bottom">
      Bedeutung
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
      Hauptbetonung
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
      Nebenbetonung
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      0
    </td>
    <td style="text-align:center">Kein Symbol</td>
    <td style="text-align:center">Kein Wert</td>
    <td>
      Keine Betonung
    </td>
  </tr>
</table>

**Hinweise:**

-   In IPA für Französisch werden Silbenbetonungssymbole ignoriert. In SPR für Französisch wird die Silbenbetonung nicht ignoriert; falls sie angegeben ist, muss die Silbenbetonung unmittelbar vor dem Vokal der Silbe stehen. In SPR wird die Silbenbetonung für Französisch viel strenger behandelt als bei anderen Sprachen. Falls sich das Betonungssymbol an einer ungültigen Position befindet, tritt ein Fehler auf.
-   In SPR für Spanisch und Italienisch können Sie lediglich das Symbol `1` (Hauptbetonung) angeben. Falls Sie eine Nebenbetonung oder gar keine Betonung angeben, tritt ein Fehler auf.
-   In SPR für Japanisch werden nur die Symbole `1` (Hauptbetonung) und `0` (keine Betonung) unterstützt. Falls Sie eine Nebenbetonung angeben, tritt ein Fehler auf.

Die Markierung für eine Silbenbetonung muss innerhalb der Silbengrenze angegeben werden, jedoch immer links vom Vokal der Silbe. Die Position links neben dem Vokal der betonten Silbe können Sie frei wählen. Beispielsweise ist bei jedem der folgenden Beispiele die Hauptbetonung ordnungsgemäß auf dem korrekten Vokal des Wortes *construction* platziert:

```xml
<phoneme alphabet="ibm" ph="kXn1strHkSXn">construction</phoneme>
<phoneme alphabet="ibm" ph="kXns1trHkSXn">construction</phoneme>
<phoneme alphabet="ibm" ph="kXnst1rHkSXn">construction</phoneme>
<phoneme alphabet="ibm" ph="kXnstr1HkSXn">construction</phoneme>
```
{: codeblock}

## Symbole für Sprachlaute

Jede Sprache verwendet ihr eigenes Inventar von SPR-Symbolen, um die Sprachlaute dieser Sprache darzustellen. Für die Angabe eines SPR-Symbols gelten die folgenden Regeln:

-   Bei Buchstaben wird die Groß-/Kleinschreibung beachtet, weshalb beispielsweise `e` und `E` zwei unterschiedliche Laute repräsentieren.
-   Zwei- und dreistellige Symbole müssen in Hochkommas eingeschlossen werden. Ein Beispiel hierfür ist das Symbol `aj` im deutschen Wort *heim*: `"h'aj'm"`.
-   Der Service betrachtet eine SPR-Definition mit Lautsymbolen, die in einer Sprache nicht zulässig sind, als ungültig.

Beachten Sie außerdem Folgendes, wenn Sie die Aussprache eines Wortes im SPR-Format definieren:

-   Für die Laute jeder Sprache gibt es bestimmte Verteilungsmuster innerhalb dieser Sprache. Beispielsweise tritt bei allen englischen Dialekten der Laut `G` in *sing* (`".1sIG"`) nicht am Anfang eines Wortes auf. Weitere Laute im amerikanischen Englisch, für die es eine besonders eingeschränkte Verteilung gibt, sind der Glottisschlag (`?`), der geschlagene Laut (`F`) und der syllabische Nasal (`N`). Falls Sie ein Lautsymbol in einem Kontext eingeben, in dem es normalerweise nicht auftritt, klingt die resultierende Sprache möglicherweise unnatürlich.
-   Durch die Anwendung einer hoch entwickelten Gruppe von linguistischen Regeln auf die Eingabe bildet der {{site.data.keyword.texttospeechshort}}-Service die Prozesse ab, durch die Laute in bestimmten Kontexten einer natürlichen Sprache geändert werden. Im amerikanischen Englisch wird beispielsweise der Laut `t` des Wortes *write* (`".1r1Yt"`) im Wort *writer* (`".1rY.0FR"`) als geschlagener Laut (`F`) ausgesprochen. SPR-Eingabe unterliegt diesen Änderungen wie jeder herkömmliche Eingabetext. In diesem Beispiel hat es keinen Einfluss auf die generierte Sprache, ob Sie `".1rY.0tR"` oder `".1rY.0FR"` eingeben.

## Mit IPA arbeiten
{: #ipa}

Für die Arbeit mit Aussprache in IPA-Schreibweise gelten die folgenden Informationen:

-   Verwenden Sie ausschließlich die dokumentierten IPA-Symbole. Wenn für ein SPR-Symbol mehrere IPA-Symbole (oder Symbolkombinationen) aufgeführt sind, sind alle zum einzelnen SPR-Symbol äquivalent. In diesem Fall behandelt der Service alle diese IPA-Symbole gleich und erkennt die subtilen oder regionalen Unterschiede, die das IPA-System beschreiben soll, nicht.
-   IPA-Aussprachen können auch in Form von IPA-Unicode-Werten angegeben werden. Die im folgenden Abschnitt genannten sprachspezifischen Tabellen dokumentieren sowohl die IPA-Symbole als auch deren äquivalente IPA-Unicode-Werte. Eine Beispielaussprache, die IPA-Unicode-Werte verwendet, finden Sie im Abschnitt [Element 'phoneme'](/docs/services/text-to-speech/SSML-elements.html#phoneme_element).

Weitere Informationen bieten die folgenden Quellen:

-   Unter der Adresse [en.wikipedia.org/wiki/International_Phonetic_Alphabet ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://en.wikipedia.org/wiki/International_Phonetic_Alphabet){: new_window} finden Sie weitere Informationen zu IPA.
-   Unter der Adresse [en.wikipedia.org/wiki/Phonetic_symbols_in_Unicode ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://en.wikipedia.org/wiki/Phonetic_symbols_in_Unicode){: new_window} sind zusätzliche Angaben über phonetische Symbole für Unicode verfügbar.

## Unterstützte Sprachen
{: #supportedLanguages}

In den folgenden Abschnitten sind die SPR-Symbole, IPA-Symbole und äquivalenten IPA-Unicode-Werte für die einzelnen Sprachen dokumentiert. Für jedes Symbol sind dabei Beispiele in Wörtern aus dieser Sprache angegeben. Aufgrund von dialektalen Unterschieden stimmen die Beispiele möglicherweise nicht immer mit Ihrer Aussprache überein.

-   [Symbole für Portugiesisch (Brasilien)](/docs/services/text-to-speech/pt-BR-SPRs.html)
-   [Symbole für britisches Englisch](/docs/services/text-to-speech/en-GB-SPRs.html)
-   [Symbole für Französisch](/docs/services/text-to-speech/fr-FR-SPRs.html)
-   [Symbole für Deutsch](/docs/services/text-to-speech/de-DE-SPRs.html)
-   [Symbole für Italienisch](/docs/services/text-to-speech/it-IT-SPRs.html)
-   [Symbole für Japanisch](/docs/services/text-to-speech/ja-JP-SPRs.html)
-   [Symbole für Spanisch](/docs/services/text-to-speech/es-ES-SPRs.html)
-   [Symbole für amerikanisches Englisch](/docs/services/text-to-speech/en-US-SPRs.html)
