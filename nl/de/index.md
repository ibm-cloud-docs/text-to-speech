---

copyright:
  years: 2015, 2019
lastupdated: "2019-07-30"

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

# Produktinformation
{: #about}

> ** Serviceaktualisierung:** *Der {{site.data.keyword.texttospeechshort}}-Service wurde am 30. Juli 2019 aktualisiert. Der Service unterstützt nun eine neuronale Stimme in Japanisch: `ja-JP_EmiV3Voice`. Weitere Angaben finden Sie unter [Serviceaktualisierung vom 30. Juli 2019](/docs/services/text-to-speech?topic=text-to-speech-release-notes#July2019) in den Releaseinformationen*.

Der {{site.data.keyword.texttospeechfull}}-Service bietet eine API, die geschriebenen Text mithilfe der Sprachsynthesefunktionen von {{site.data.keyword.IBM_notm}} in gut verständliche Sprache umwandelt. Der Service überträgt die Ergebnisse mit minimaler Verzögerung zurück an den Client. Er bietet Schnittstellen sowohl für [HTTP](/docs/services/text-to-speech?topic=text-to-speech-usingHTTP) als auch für [WebSocket](/docs/services/text-to-speech?topic=text-to-speech-usingWebSocket).

## Features und Funktionen

Der {{site.data.keyword.texttospeechshort}}-Service bietet die folgenden Features und Funktionen:

-   **Audioformate** - Erzeugt Sprachausgabe im Ogg- oder WebM-Format mit Opus- oder Vorbis-Codec, im WAV-Format, FLAC-Format, MP3-Format (MPEG), l16-Format (PCM), Mu-Law-Format oder im Basisformat. Weitere Informationen finden Sie unter [Audioformate](/docs/services/text-to-speech?topic=text-to-speech-audioFormats).
-   **Stimmen** - Erstellt aus Text synthetisch Sprachausgabe in verschiedenen Sprachen, Stimmen und Dialekten. Es bietet sowohl Standardversionen (konkatenativ) als auch neuronale Versionen der meisten Stimmen an. Weitere Informationen finden Sie unter [Sprachen und Stimmen](/docs/services/text-to-speech?topic=text-to-speech-voices).
-   **SSML** - Akzeptiert einfachen Text oder Text mit der XML-basierten Markup-Sprache 'Speech Synthesis Markup Language' (SSML). Weitere Informationen finden Sie im Abschnitt [SSML verwenden](/docs/services/text-to-speech?topic=text-to-speech-ssml).
-   **Expressivität** - Erweitert SSML durch ein expressives Element, mit dem Sie den Sprechstil *GoodNews* (= Gute Neuigkeiten), *Apology* (= Entschuldigung) oder *Uncertainty* (= Unsicherheit) angeben können. Verfügbar nur für die Stimme 'Allison' für amerikanisches Standard-Englisch. Weitere Informationen finden Sie unter [SSML für Expressivität](/docs/services/text-to-speech?topic=text-to-speech-expressive).
-   **Stimmenumwandlung** - Erweitert SSML durch ein Element für die Stimmenumwandlung. Mithilfe des Elements können Sie die Palette der möglichen Stimmen erweitern, indem Sie Aspekte wie Tonhöhe, Geschwindigkeit und Timbre steuern. Diese Funktion bietet außerdem zwei integrierte virtuelle Stimmen namens *Young* und *Soft*. Nur für Stimmen für amerikanisches Standard-Englisch verfügbar. Weitere Informationen enthält der Abschnitt [SSML für Stimmenumwandlung](/docs/services/text-to-speech?topic=text-to-speech-transformation).
-   **Worttakt** - Unterstützt bei der WebSocket-Schnittstelle das SSML-Element `<mark>` und optionale Worttaktinformationen für alle Zeichenfolgen des Eingabetextes. Die Taktinformationen synchronisieren den Eingabetext und die resultierende Sprachausgabe. Weitere Informationen finden Sie unter [Worttakt abrufen](/docs/services/text-to-speech?topic=text-to-speech-timing).
-   **Anpassung** - Bietet eine Anpassungsschnittstelle, mit der Sie angeben können, wie der Service ungewöhnliche Wörter aussprechen soll, die in der Eingabe enthalten sind. Zum Definieren der Aussprachevarianten können Sie IPA (International Phonetic Alphabet, internationales phonetisches Alphabet) oder {{site.data.keyword.IBM_notm}} Symbolic Phonetic Representation (SPR) verwenden. Weitere Informationen enthält der Abschnitt [Wissenswertes über die Anpassung](/docs/services/text-to-speech?topic=text-to-speech-customIntro).

Zusätzliche Angaben über die Preistarife für den Service erhalten Sie nach Aufruf des Eintrags für den {{site.data.keyword.texttospeechshort}}-Service im [{{site.data.keyword.cloud_notm}}-Katalog](https://{DomainName}/catalog/services/text-to-speech){: external}.

## Sprachunterstützung
{: #languages-index}

Der Service unterstützt Stimmen in den folgenden Sprachen: brasilianisches Portugiesisch, Englisch (britischer und amerikanischer Dialekt), Französisch, Deutsch, Italienisch, Japanisch und Spanisch (kastilischer, lateinamerikanischer und nordamerikanischer Dialekt).

Der Service bietet für jede Sprache mindestens eine Frauenstimme an. Für einige Sprachen bietet der Service mehrere Stimmen an, darunter sowohl Männer- als auch Frauenstimmen. Jede Stimme verwendet den geeigneten Tonfall und die passende Satzmelodie für ihren Dialekt. Der Service bietet sowohl Standard- als auch neuronale Versionen der meisten Stimmen an.

Weitere Informationen zu den Stimmen, die für jede Sprache verfügbar sind, finden Sie unter [Sprachen und Stimmen](/docs/services/text-to-speech?topic=text-to-speech-voices).

## Anwendungsfälle
{: #usecases}

Der Service ist für sprachgesteuerte und anzeigenlose Anwendungen geeignet, bei denen vorzugsweise Audioausgabe verwendet wird:

-   Schnittstellen für Personen mit körperlichen Beeinträchtigungen wie beispielsweise Assistenztools für Sehbehinderte
-   Funktionen zum Vorlesen von Text und E-Mail-Nachrichten für Autofahrer
-   Drehbuchkommentare und Off-Kommentare für Videos
-   Lesebasierte Lernmittel
-   Lösungen für die Haushaltsautomation

## Service ausprobieren

Beispiele für den ausgeführten Service können Sie über die folgenden Links aufrufen:

-   Eine [Kurzdemo](https://text-to-speech-demo.ng.bluemix.net/){: external} des {{site.data.keyword.texttospeechshort}}-Service, der Text als Eingabe verwendet und Sprachausgabe in verschiedenen Stimmen generiert. Bei entsprechender Unterstützung bietet der Service Expressivität und Stimmenumwandlung.
-   Anwendungen in {{site.data.keyword.ibmwatson}}[Starter Kits](http://www.ibm.com/watson/developercloud/starter-kits.html){: external}, die den {{site.data.keyword.texttospeechshort}}-Service vorführen.
