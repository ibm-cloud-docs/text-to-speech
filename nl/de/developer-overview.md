---

copyright:
  years: 2015, 2019
lastupdated: "2019-07-06"

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

# Überblick für Entwickler
{: #overview}

Auf die Sprachsynthesefunktionen des {{site.data.keyword.texttospeechfull}}-Service können Sie über eine HTTP-REST-API oder eine WebSocket-Schnittstelle zugreifen. Es gibt außerdem mehrere Software-Development-Kits (SDKs), mit denen die Anwendungsentwicklung in unterschiedlichen Programmiersprachen vereinfacht wird. Die folgenden Abschnitte vermitteln Ihnen einen Überblick über die Anwendungsentwicklung mit dem Service.
{: shortdesc}

## HTTP-Schnittstelle
{: #overview-http}

Zum synthetischen Erstellen von Text mit der HTTP-API rufen Sie die Version `GET` oder `POST` für die Methode `/v1/synthesize` des Service auf. Die beiden Versionen der Methode bieten generell eine äquivalente Funktionalität:

-   *Eingabetext* - Sie übergeben den Eingabetext, für den synthetisch Sprachausgabe erstellt werden soll, auf zwei unterschiedlichen Wegen:
    -   Die Methode `GET /v1/synthesize` akzeptiert den Eingabetext als Abfrageparameter. Die maximale Größe der Anforderung beträgt 8 KB, was den Eingabetext sowie die URL und die Header beinhaltet.
    -   Die Methode `POST /v1/synthesize` akzeptiert den Eingabetext im Hauptteil der Anforderung. Die maximale Größe der Anforderung beträgt 8 KB für die URL und die Header und 5 KB für den Eingabetext, der im Hauptteil der Anforderung gesendet wird.

    An den Service können Sie einfachen Text oder auch Text übergeben, der mit SSML (Speech Synthesis Markup Language) annotiert ist. SSML ist eine XML-basierte Markup-Sprache, die Annotationen von Text für Sprachsyntheseanwendungen wie den {{site.data.keyword.texttospeechshort}}-Service bereitstellt. Der Service erweitert SSML durch servicespezifische Elemente für Expressivität und Stimmenumwandlung, die für einige Stimmen für amerikanisches Standard-Englisch zur Verfügung stehen.

    Weitere Informationen finden Sie unter [Eingabetext angeben](/docs/services/text-to-speech?topic=text-to-speech-usingHTTP#input).
-   *Stimmen* - Der Service verwendet Text als Eingabe und erzeugt Audioausgabe in unterschiedlichen Sprachen, Stimmen und Dialekten. Der Service bietet für jede Sprache mindestens eine Frauenstimme an. Für einige Sprachen bietet der Dienst mehrere Stimmen an, die sowohl Männer- als auch Frauenstimmen umfassen können. Der Service bietet auch verschiedene Varianten an, zum Beispiel amerikanisches oder britisches Englisch. Es bietet sowohl Standardversionen (konkatenativ) als auch erweiterte neuronale Versionen der meisten Stimmen an.

    Mithilfe den Methoden `GET /v1/voices` bzw. `GET /v1/voices/{voice}` des Service können Sie mehr über die unterstützen Sprachen erfahren. Der Service erstellt aus dem Text synthetisch Sprache in der angegebenen Stimme. Achten Sie darauf, dass die Stimme zum Eingabetext passt.

    Weitere Informationen finden Sie unter [Sprachen und Stimmen](/docs/services/text-to-speech?topic=text-to-speech-voices).
-   *Audioformate:* Der Service kann Audioausgabe in den folgenden Formaten erzeugen: Ogg oder Web Media (WebM) mit Opus-Codec (Standardeinstellung) oder Vorbis-Codec, MP3 (Motion Picture Experts Group; kurz 'MPEG'), WAV (Waveform Audio File), FLAC (Free Lossless Audio Codec), lineares 16-Bit-PCM (Pulse-Code Modulation), 8-Bit-Mu-Law (U-Law) oder Audiobasisformat.

    Weitere Informationen finden Sie unter [Audioformate](/docs/services/text-to-speech?topic=text-to-speech-audioFormats).

## WebSocket-Schnittstelle
{: #overview-websocket}

Der Service bietet eine WebSocket-Schnittstelle, mit der Sie synthetisch Sprache aus Text erstellen können. Die Schnittstelle stellt eine einzige Version der Methode `/v1/synthesize` bereit, die Eingabetext mit einer maximalen Größe von 5 KB akzeptiert. Sie geben den Text, für den synthetisch Sprache erstellt werden soll, sowie die zu verwendende Stimme und das Audioformat an. Sie können einfachen Text oder mit SSML annotierten Text bereitstellen. Weitere Informationen finden Sie im Abschnitt [WebSocket-Schnittstelle](/docs/services/text-to-speech?topic=text-to-speech-usingWebSocket).

Die WebSocket-Schnittstelle unterstützt die Verwendung des SSML-Elements `<mark>` zur Angabe bestimmter Positionen in der Audioausgabe. Außerdem können Sie für alle Wörter des Eingabetextes Worttaktinformationen anfordern. Weitere Informationen finden Sie unter [Worttakt abrufen](/docs/services/text-to-speech?topic=text-to-speech-timing).

## Anpassungsschnittstelle
{: #overview-customization}

Der Service beinhaltet eine Anpassungsschnittstelle, mit deren Hilfe Sie angepasste Sprechmodelle zur Verwendung bei der Sprachsynthese erstellen können. Ein angepasstes Sprechmodell ist ein Verzeichnis von Wörtern und ihrer Umsetzung für eine bestimmte Sprache. Jedes Paar aus Wort und Umsetzung in einem Modell weist den Service an, wie das Wort auszusprechen ist, wenn es im Eingabetext vorkommt.

Mithilfe von angepassten Sprechmodellen können Sie anwendungsspezifische Umsetzungen für ungewöhnliche Wörter erstellen, bei denen die normalen Ausspracheregeln des Service zu fehlerhaften Aussprachevarianten führen könnten. Den angepassten Eintrag für ein Paar aus Wort und Umsetzung können Sie in der Standarddarstellung IPA (International Phonetic Alphabet) oder in der {{site.data.keyword.IBM_notm}} eigenen Darstellung SPR (Symbolic Phonetic Representation) definieren.

Beispiel: Ihre Anwendung nutzt gewohnheitsmäßig Sonderbegriffe fremdsprachigen Ursprungs, Personennamen bzw. geografische Bezeichnungen oder Abkürzungen und Akronyme. Mithilfe der Anpassung können Sie Umsetzungen definieren, die den Service anweisen, wie solche Begriffe auszusprechen sind. Weitere Informationen enthält der Abschnitt [Wissenswertes über die Anpassung](/docs/services/text-to-speech?topic=text-to-speech-customIntro).

Die Anpassungsschnittstelle liegt als Betaversion vor. Sie benötigen außerdem den Standardpreisplan, um die Anpassung des Sprachmodells nutzen zu können. Benutzer des Lite-Plans können die Anpassungsschnittstelle nicht verwenden. Weitere Informationen enthält die [Preisstruktur-Seite](https://www.ibm.com/cloud/watson-text-to-speech/pricing){: external} für den {{site.data.keyword.texttospeechshort}}-Service.
{: note}

## CORS-Unterstützung
{: #cors}

Der Service unterstützt Cross-Origin Resource Sharing (CORS). Mithilfe von CORS können Webseiten Ressourcen direkt aus einer fremden Domäne anfordern. CORS umgeht die Sicherheitsrichtlinie für einen identischen Ursprung, die solche Anforderungen andernfalls verhindert. Da der Service CORS unterstützt, kann eine Webseite direkt mit dem Service kommunizieren, ohne die Anforderung über den Webserver zu übergeben, der die Seite hostet.

Beispielsweise kann eine Webseite, die aus einem Server in {{site.data.keyword.cloud}} geladen wird, die Anpassungs-API unter Umgehung des {{site.data.keyword.cloud_notm}}-Servers direkt aufrufen. Weitere Informationen finden Sie unter [enable-cors.org](https://enable-cors.org/){: external}.

## Software-Development-Kits verwenden
{: #sdks}

Für den {{site.data.keyword.texttospeechshort}}-Service sind SDKs verfügbar, die die Entwicklung von Sprachanwendungen vereinfachen. {{site.data.keyword.ibmwatson}} SDKs stehen für viele gängige Programmiersprachen und Plattformen zur Verfügung.

-   Eine vollständige Liste der SDKs und Links zu den SDKs bei GitHub finden Sie im Abschnitt [SDKs verwenden](/docs/services/watson?topic=watson-using-sdks).
-   Ausführliche Informationen zu allen Methoden der Node-, Java&trade;-, Python-, Ruby-, Swift- und Go-SDKs für den {{site.data.keyword.texttospeechshort}}-Service enthält die [API-Referenz](https://{DomainName}/apidocs/text-to-speech){: external}.

## Weitere Informationen zur Anwendungsentwicklung
{: #learn}

Zusätzliche Angaben über die Arbeit mit {{site.data.keyword.watson}}-Services und {{site.data.keyword.cloud_notm}} enthalten die folgenden Quellen:

-   Eine Einführung in die Arbeit mit {{site.data.keyword.watson}}-Services und {{site.data.keyword.cloud_notm}} bietet der Abschnitt [Einführung in {{site.data.keyword.watson}} und {{site.data.keyword.cloud_notm}}](/docs/services/watson?topic=watson-about).
-   Alle neuen Serviceinstanzen verwenden {{site.data.keyword.cloud_notm}} Identity and Access Management (IAM) zur Authentifizierung. Ältere Serviceinstanzen verwenden für die Authentifizierung unter Umständen weiterhin die Werte für `{username}` (Benutzername) und `{password}` (Kennwort) aus ihren bestehenden Cloud Foundry-Serviceberechtigungsnachweisen. Weitere Angaben über die Authentifizierung beim Service finden Sie unter [Serviceaktualisierung vom 30. Oktober 2018](/docs/services/text-to-speech?topic=text-to-speech-release-notes#October2018) in den Releaseinformationen.
-   Informationen zum Steuern der Standardprotokollierung für Anforderungen, die für alle {{site.data.keyword.watson}}-Services durchgeführt wird, enthält der Abschnitt [Anforderungsprotokollierung für {{site.data.keyword.watson}}-Services](/docs/services/watson?topic=watson-gs-logging-overview).
