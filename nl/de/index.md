---

copyright:
  years: 2015, 2019
lastupdated: "2019-04-08"

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

# Produktinformation
{: #about}

> ** Serviceaktualisierung** *Der {{site.data.keyword.texttospeechshort}}-Service wurde am 24. März 2019 aktualisiert. Der Service bietet jetzt DNN-Versionen (DNN = Deep Neural Network) für seine deutschen Stimmen; alle auf DNN basierenden Stimmen unterstützen nun die Attribute `pitch` und `rate` des SSML-Elements `<prosody>`. Weitere Angaben finden Sie unter [Serviceaktualisierung vom 24. März 2019](/docs/services/text-to-speech/release-notes.html#March2019c) in den Releaseinformationen*.

Der {{site.data.keyword.texttospeechfull}}-Service bietet eine API, die geschriebenen Text mithilfe der Sprachsynthesefunktionen von {{site.data.keyword.IBM_notm}} in gut verständliche Sprache umwandelt. Der Service überträgt die Ergebnisse mit minimaler Verzögerung zurück an den Client. Er bietet Schnittstellen sowohl für [HTTP](/docs/services/text-to-speech/http.html) als auch für [WebSocket](/docs/services/text-to-speech/websockets.html). 

## Features und Funktionen

Der {{site.data.keyword.texttospeechshort}}-Service bietet die folgenden Features und Funktionen:

-   **Audioformate** - Erzeugt Sprachausgabe im Ogg- oder WebM-Format mit Opus- oder Vorbis-Codec, im WAV-Format, FLAC-Format, MP3-Format (MPEG), l16-Format (PCM), Mu-Law-Format oder im Basisformat. Weitere Informationen finden Sie unter [Audioformate](/docs/services/text-to-speech/audio-formats.html).
-   **Stimmen** - Erstellt aus Text synthetisch Sprachausgabe in verschiedenen Sprachen, Stimmen und Dialekten. Von einigen Stimmen bietet der Service jetzt DNN-basierte Versionen. Weitere Informationen finden Sie unter [Sprachen und Stimmen](/docs/services/text-to-speech/voices.html).
-   **SSML** - Akzeptiert einfachen Text oder Text mit der XML-basierten Markup-Sprache 'Speech Synthesis Markup Language' (SSML). Weitere Informationen finden Sie im Abschnitt [SSML verwenden](/docs/services/text-to-speech/SSML.html).
-   **Expressivität** - Erweitert SSML durch ein expressives Element, mit dem Sie den Sprechstil *GoodNews* (= Gute Neuigkeiten), *Apology* (= Entschuldigung) oder *Uncertainty* (= Unsicherheit) angeben können. Diese Funktionalität ist nur bei der nicht DNN-basierten Stimme 'Allison' für amerikanisches Englisch verfügbar. Weitere Informationen finden Sie unter [SSML für Expressivität](/docs/services/text-to-speech/SSML-expressive.html).
-   **Stimmenumwandlung** - Erweitert SSML durch ein Element für die Stimmenumwandlung. Mithilfe des Elements können Sie die Palette der möglichen Stimmen erweitern, indem Sie Aspekte wie Tonhöhe, Geschwindigkeit und Timbre steuern. Diese Funktion bietet außerdem zwei integrierte virtuelle Stimmen namens *Young* und *Soft*. Sie ist nur bei nicht DNN-basierten Stimmen für amerikanisches Englisch verfügbar. Weitere Informationen enthält der Abschnitt [SSML für Stimmenumwandlung](/docs/services/text-to-speech/SSML-transformation.html).
-   **Worttakt** - Unterstützt bei der WebSocket-Schnittstelle das SSML-Element `<mark>` und optionale Worttaktinformationen für alle Zeichenfolgen des Eingabetextes. Die Taktinformationen synchronisieren den Eingabetext und die resultierende Sprachausgabe. Weitere Informationen finden Sie unter [Worttakt abrufen](/docs/services/text-to-speech/word-timing.html).
-   **Anpassung** - Bietet eine Anpassungsschnittstelle, mit der Sie angeben können, wie der Service ungewöhnliche Wörter aussprechen soll, die in der Eingabe enthalten sind. Zum Definieren der Aussprachevarianten können Sie IPA (International Phonetic Alphabet, internationales phonetisches Alphabet) oder {{site.data.keyword.IBM_notm}} Symbolic Phonetic Representation (SPR) verwenden. Weitere Informationen enthält der Abschnitt [Wissenswertes über die Anpassung](/docs/services/text-to-speech/custom-intro.html).

Zusätzliche Angaben über die Preistarife für den Service erhalten Sie nach Aufruf des Eintrags für den {{site.data.keyword.texttospeechshort}}-Service im [{{site.data.keyword.cloud_notm}}-Katalog. ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://{DomainName}/catalog/services/text-to-speech){: new_window}

## Sprachunterstützung
{: #languages-index}

Der Service unterstützt Stimmen in den folgenden Sprachen: brasilianisches Portugiesisch, Englisch (britischer und amerikanischer Dialekt), Französisch, Deutsch, Italienisch, Japanisch und Spanisch (kastilischer, lateinamerikanischer und nordamerikanischer Dialekt). Für jede Sprache bietet der Service mindestens eine Männer- oder Frauenstimme, manchmal auch beides. Jede Stimme verwendet den geeigneten Tonfall und die passende Satzmelodie für ihren Dialekt. Weitere Informationen zu den Stimmen, die für jede Sprache verfügbar sind, finden Sie unter [Sprachen und Stimmen](/docs/services/text-to-speech/voices.html).

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

-   [Kurzdemo ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://text-to-speech-demo.ng.bluemix.net/){: new_window} des {{site.data.keyword.texttospeechshort}}-Service, der Text als Eingabe verwendet und Sprachausgabe in verschiedenen Stimmen generiert. Bei entsprechender Unterstützung bietet der Service Expressivität und Stimmenumwandlung.
-   Anwendungen in {{site.data.keyword.ibmwatson}} [Starter-Kits ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](http://www.ibm.com/watson/developercloud/starter-kits.html){: new_window}, die den {{site.data.keyword.texttospeechshort}}-Service vorführen.
