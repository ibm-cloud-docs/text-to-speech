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

# SSML verwenden
{: #ssml}

SSML (Speech Synthesis Markup Language) ist eine XML-basierte Markup-Sprache, die Annotationen von Text für Sprachsyntheseanwendungen bereitstellt. Es handelt sich hierbei um eine Empfehlung der W3C Voice-Browser Working Group, die durch die Spezifikation 'VoiceXML 2.0' als Standard-Markup-Sprache für die Sprachsynthese übernommen wurde. SSML bietet Entwicklern von Sprachanwendungen ein Standardverfahren, mit dem durch die Angabe von Aussprache, Lautstärke, Tonhöhe, Geschwindigkeit und anderen Attribute über die Markup-Sprache Aspekte des Syntheseprozesses gesteuert werden können.
{: shortdesc}

Beim {{site.data.keyword.texttospeechfull}}-Service können Sie mit SSML die Synthese Ihres Textes für alle unterstützten Sprachen steuern. Hierzu gehört auch das SSML-Element `<phoneme>`, mit dem die Aussprache eines Wortes entweder gemäß IPA (International Phonetic Alphabet) oder {{site.data.keyword.IBM_notm}} SPR (Symbolic Phonetic Representation) definiert wird. Der Service verwendet darüber hinaus das SSML-Element `<phoneme>`, um die phonetische Umsetzung für ein Wort mit der Anpassungsschnittstelle zu definieren; weitere Informationen hierzu enthält der Abschnitt [Wissenswertes über die Anpassungsschnittstelle](/docs/services/text-to-speech?topic=text-to-speech-customIntro).

## Einführung in SSML
{: #introduction-SSML}

Die Funktionsweise von SSML ergibt sich daraus, dass einfacher Text, der an eine Sprachsynthesefunktion übergeben wird, durch eine vordefinierte Gruppe von Elementen (auch 'Tags' genannt) erweitert wird. Der einfache Eingabetext wird zunächst durch einen XML-Parser von den Markup-Spezifikationen getrennt. Anschließend werden die Spezifikationen verarbeitet und zur Erzeugung der gewünschten Effekte als Gruppe von Anweisungen in einem Format gesendet, dass für die Sprachsynthesefunktion verständlich ist. Damit der XML-Parser diese Aufgabe erfüllen kann, müssen die Markup-Formatierungen korrekt formatiert sein; beispielsweise müssen Elemente abgeschlossen und mehrere Elemente ordnungsgemäß verschachtelt sein. Eine Einführung in die grundlegenden XML-Konzepte finden Sie unter der Adresse [w3schools.com/xml/xml_whatis.asp](http://www.w3schools.com/xml/xml_whatis.asp){: external}.

Als SSLM-Element gelten alle Daten, die in einem Starttag und seinem zugehörigen Endtag enthalten sind; auch die Tags gehören zum Element. Wie aus dem folgenden Beispiel hervorgeht, kann ein Element eine Kombination aus Tags und anderen Elementen enthalten (Tags können verschachtelt werden). Elemente können zudem Attribute erfordern oder optional akzeptieren, um bestimmte Werte festzulegen.

```xml
<tag1>
  <tag2 attributename="attributewert">
    ... some text ...
  </tag2>
</tag1>
```
{: codeblock}

Ein vollständig gültiges SSML-Dokument besteht aus einem XML-Prolog, der Informationen wie die Codierung und das Schema für die Validierung des SSML-Dokuments enthält und auf den das Stammelement `<speak>` folgt. (Weitere Inforationen zur Struktur des Prologs finden Sie unter der Adresse [tizag.com/xmlTutorial/xmlprolog.php](http://www.tizag.com/xmlTutorial/xmlprolog.php){: external}.) Innerhalb des Elements `<speak>` geben Sie den Text an, aus dem synthetisch Sprache erstellt werden soll und der durch zusätzliche Elemente erweitert wird.

```xml
<!-- XML-Prolog -->
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE speak PUBLIC "-//W3C//DTD SYNTHESIS 1.0//EN"
  "http://www.w3.org/TR/speech-synthesis/synthesis.dtd">

<!-- Stammelement -->
<speak version="1.0" xmlns="www.w3.org/2001/10/synthesis"
  ... Hauptteil mit Tex für die Sprachsynthese sowie Markup-Formatierung ...</speak>
```
{: codeblock}

Der Service unterstützt SSML-Fragmente; dies sind SSML-Elemente, die nicht den vollständigen XML-Header enthalten.

## SSML-Unterstützung
{: #ssmlSupport}

Die Unterstützung des {{site.data.keyword.texttospeechshort}}-Service basiert auf der SSML-Version 1.0, die am 7. September 2004 von W3C empfohlen wurde. Weitere Informationen zur W3C-Empfehlung für SSML sind auf der Seite [W3C Speech Synthesis Markup Language (SSML) Version 1.0](http://www.w3.org/TR/speech-synthesis/){: external}.

Zusätzliche Angaben über die Verwendung von SSML beim Service bieten die folgenden Quellen:

-   Vollständige Informationen zu den Service-Levels der Unterstützung, die der Service für alle SSML-Elemente bietet, finden Sie unter [SSML-Elemente](/docs/services/text-to-speech?topic=text-to-speech-elements). Der Service implementiert den Großteil der W3C-Spezifikation sowie SSML-Fragmente mit nur wenigen Ausnahmen.
-   Der Service erweitert SSML durch ein Element `<express-as>`, mit dem angegeben wird, mit welcher Expressivität ein Text beim Sprechen versehen werden soll (gute Neuigkeit, Entschuldigung oder Unsicherheit). Die Expressivität wird vom Service nur bei der Stimme 'Allison' für amerikanisches Englisch unterstützt. Weitere Informationen finden Sie unter [SSML für Expressivität](/docs/services/text-to-speech?topic=text-to-speech-expressive).
-   Der Service erweitert SSML durch ein Element `<voice-transformation>`, mit dem Sie die Palette der möglichen Stimmen durch eine Steuerung der Tonhöhe, des Tonumfangs, des Glottisdrucks, der Aspiration, des Tempos und des Timbres von gesprochenem Text vergrößern können. Der Service bietet außerdem zwei integrierte virtuelle Stimmen namens *Young* und *Soft*. Die Stimmenumwandlung wird vom Service nur bei den Stimmen für amerikanisches Englisch unterstützt. Weitere Informationen enthält der Abschnitt [SSML für Stimmenumwandlung](/docs/services/text-to-speech?topic=text-to-speech-transformation).
-   Die Anpassungsschnittstelle des Service unterstützt die Verwendung des SSML-Elements `<phoneme>`, mit dem die phonetische Schreibweise angegeben wird, die für die Aussprache eines Wortes zu verwenden ist. Die phonetische Schreibweise stellt dar, aus welchen Lauten ein Wort besteht, wie diese Laute in Silben unterteilt werden und welche Silben betont werden.
    -   Informationen zur Anpassungsschnittstelle enthält der Abschnitt [Wissenswertes über die Anpassung](/docs/services/text-to-speech?topic=text-to-speech-customIntro).
    -   Angaben über die gültigen Symbole, die Sie in einer {{site.data.keyword.IBM_notm}} SPR- oder IPA-Spezifikation für jede unterstützte Sprache verwenden können, finden Sie unter [IBM SPR verwenden](/docs/services/text-to-speech?topic=text-to-speech-sprs).

## SSML-Validierung
{: #errors}

Der Service validiert alle SSML-Elemente, die Sie in einem beliebigen Inhalt übergeben, also entweder als Eingabetext für die Synthese oder als Definition der Umsetzung eines Worts für die Anpassung. Der Service kann nicht vorab feststellen, ob der zur Synthese übergebene Text SSML-Elemente enthält. Er führt daher für jeden Eingabetext dieselbe Validierung unabhängig davon durch, ob der Text SSML enthält oder nicht.

-   *Die gesamte SSML-Eingabe muss korrekt und einwandfrei formatiert sein.* Nicht unterstützte SSML-Elemente werden vom Service ohne Ausgabe einer entsprechenden Nachricht ignoriert. Aus dem Text, der in einem nicht unterstützten Element oder in einem Element, das nicht unterstützte Funktionen verwendet, enthalten ist, wird durch den Service synthetisch Sprache erstellt; lediglich das Element wird ignoriert.
-   *Für ungültige Elemente meldet der Service den HTTP-Fehlercode 400.* Die Fehlerantwort enthält eine beschreibende Nachricht und die Anforderung schlägt fehl.

Der Service gibt insbesondere in den folgenden Fällen einen Fehler zurück:

-   *Ungültiges Element:* Sie geben beispielsweise einen Tag falsch an, lassen ein erforderliches Attribut weg oder beziehen einen Starttag, jedoch ohne zugehörigen Endtag ein.
-   *Ungültiges Symbol:* Das Attribut `ph` eines Elements `<phoneme>` enthält ein nicht unterstütztes IPA- oder SPR-Symbol für die angegebene Sprache.
-   *Keine Vokale:* Das Attribut `ph` eines Elements `<phoneme>` gibt eine Wortaussprache an, die keine Vokale umfasst.
-   *Bindung in Französisch an ungültiger Position:* Im Attribut `ph` eines Elements `<phoneme>` folgt das Bindungszeichen nicht auf einen Konsonanten oder ist in der Mitte der Wortaussprache angegeben.
-   *Japanisches Symbol `:` steht nicht vor einem Vokal:* Im Attribut `ph` eines Elements `<phoneme>` steht ein Zeichen `:` nicht vor einem Vokal (möglicherweise mit anderen Symbolen wie Silbengrenzen dazwischen).
-   *Ungültige Silbenbetonung:* Das Attribut `ph` eines Elements `<phoneme>` für {{site.data.keyword.IBM_notm}} SPR enthält eine ungültige Silbenbetonung. Bei Französisch steht ein Symbol für die Silbenbetonung nicht unmittelbar vor einem Vokal. Bei Spanisch oder Italienisch wird ein Symbol für die Nebenbetonung (`2`) oder für keine Betonung (`0`) verwendet. Bei Japanisch wird ein Symbol für die Nebenbetonung (`2`) verwendet.
-   *Ungültige Verwendung des SSML-Elements `<express-as>` oder `<voice-transformation>`:* Diese SSML-Erweiterungen können Sie nur bei den angegebenen Stimmen für amerikanisches Standard-Englisch verwenden.
-   *Ungültige Verwendung des SSML-Elements `<prosody>`:* Sie können die Attribute `contour`, `duration` und `range` des Elements `<prosody>` nicht mit einer beliebigen Stimme verwenden. Darüber hinaus können Sie das Attribut `volume` des Elements `<prosody>` nicht mit neuronalen Stimmen (z. B. `en-US_AllisonV3Voice`) verwenden. 
-   *XML-Steuerzeichen ohne Escapezeichen:* Der Eingabetext selbst enthält ein Zeichen <code>&quot;</code>, <code>&apos;</code>, `&`, `<` oder `>` anstelle der äquivalenten Escapezeichenfolge oder Zeichencodierung. Weitere Informationen finden Sie im Abschnitt [XML-Steuerzeichen mit Escapezeichen versehen](/docs/services/text-to-speech?topic=text-to-speech-usingHTTP#escape).
