---

copyright:
  years: 2015, 2019
lastupdated: "2019-07-03"

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
{:go: .ph data-hd-programlang='go'}
{:python: .ph data-hd-programlang='python'}
{:swift: .ph data-hd-programlang='swift'}
{:download: .download}
{:apikey: data-credential-placeholder='apikey'}
{:url: data-credential-placeholder='url'}
{:hide-dashboard: .hide-dashboard}

# Lernprogramm 'Einführung'
{: #gettingStarted}

Der {{site.data.keyword.texttospeechfull}}-Service konvertiert
geschriebenen Text in gut verständliche Sprache, damit Sprachsynthesefunktionen
für Anwendungen zur Verfügung stehen. Das vorliegende auf Curl basierende
Lernprogramm unterstützt Sie beim schnellen Einstieg in diesen Service. Die
Beispiele demonstrieren, wie Sie durch den Aufruf der vom Service
bereitgestellten Methoden `POST`
und `GET /v1/synthesize` einen Audiodatenstrom anfordern.
{: shortdesc}

## Vorbereitende Schritte
{: #before-you-begin}

- {: hide-dashboard}  Erstellen Sie eine Instanz des Service:
    1.  {: hide-dashboard}Rufen Sie die [{{site.data.keyword.texttospeechshort}}](https://{DomainName}/catalog/services/text-to-speech){: external}-Seite im {{site.data.keyword.cloud_notm}}-Katalog auf.
    1.  {: hide-dashboard}Registrieren Sie sich für ein kostenloses {{site.data.keyword.cloud_notm}}-Konto oder melden Sie sich an.
    1.  {: hide-dashboard} Klicken Sie auf **Erstellen**.
-   Kopieren Sie die Berechtigungsnachweise zur Authentifizierung bei Ihrer Serviceinstanz:
    1.  {: hide-dashboard}Klicken Sie in der [{{site.data.keyword.cloud_notm}}-Ressourcenliste](https://{DomainName}/resources){: external} auf Ihre {{site.data.keyword.texttospeechshort}}-Serviceinstanz, um zur Dashboardseite des {{site.data.keyword.texttospeechshort}}-Service zu wechseln.
    1.  Klicken Sie auf der Seite **Verwalten** auf **Anzeigen**, um Ihre Berechtigungsnachweise anzuzeigen.
    1.  Kopieren Sie die Werte für den `API-Schlüssel` und die `URL`.

### Die curl-Beispiele verwenden
{: #getting-started-curl}

In diesem Lernprogramm wird der Befehl `curl` verwendet, um Methoden der HTTP-Schnittstelle des Service aufzurufen. Stellen Sie sicher, dass der Befehl `curl` auf Ihrem System installiert ist.

1.  Um zu testen, ob `curl` installiert ist, führen Sie den folgenden Befehl in der Befehlszeile aus. Wenn die Ausgabe die `curl`-Version auflistet, die Secure Sockets Layer (SSL) unterstützt, sind Sie für das Lernprogramm bereit.

    ```bash
    curl -V
    ```
    {: pre}

1.  Installieren Sie falls erforderlich die Version von `curl` (SSL-fähig) für Ihr Betriebssystem von [curl.haxx.se](https://curl.haxx.se/){: external}.

Lassen Sie die geschweiften Klammern aus den Beispielen weg. Sie geben Variablenwerte an.
{: tip}

## Schritt 1: Synthetische Sprachausgabe aus Text in amerikanischem Englisch erstellen
{: #synthesizeEnglish}

Die folgenden Befehle verwenden die Methode `POST /v1/synthesize`, um aus Eingabe in amerikanischem Englisch synthetisch Audiodateien in zwei unterschiedlichen Formaten zu erstellen. Beide Anforderungen verwenden die Standardstimme für amerikanisches Englisch `en-US_MichaelVoice`.

1.  Geben Sie den folgenden Befehl aus, um für die Zeichenfolge 'hello world' synthetisch Sprachausgabe zu erstellen und eine WAV-Datei namens `hello_world.wav` zu erzeugen.
    -   {: hide-dashboard} Ersetzen Sie hierbei `{api-schlüssel}` und `{url}` durch Ihren API-Schlüssel und Ihre URL.

    *Windows-Benutzer* ersetzen den umgekehrten Schrägstrich (``\ `) am Ende jeder Zeile durch ein Winkelzeichen (``^ `). Stellen Sie sicher, dass keine nachgestellten Leerzeichen vorhanden sind.
    {: tip}

    ```bash
    curl -X POST -u "apikey:{api-schlüssel}"{: apikey} \
    --header "Content-Type: application/json" \
    --header "Accept: audio/wav" \
    --data "{\"text\":\"hello world\"}" \
    --output hello_world.wav \
    "{url}/v1/synthesize"{: url}
    ```
    {: pre}

1.  Geben Sie den folgenden Befehl aus, um synthetisch Sprachausgabe aus demselben Text zu erstellen, jedoch eine Datei im Standardformat 'Ogg' namens `hello_world.ogg` zu erzeugen.
    -   {: hide-dashboard} Ersetzen Sie hierbei `{api-schlüssel}` und `{url}` durch Ihren API-Schlüssel und Ihre URL.

    ```bash
    curl -X POST -u "apikey:{api-schlüssel}"{: apikey} \
    --header "Content-Type: application/json" \
    --data "{\"text\":\"hello world\"}" \
    --output hello_world.ogg \
    "{url}/v1/synthesize"{: url}
    ```
    {: pre}

Zur Wiedergabe der Audiodateien, die durch die Beispiele in diesem Lernprogramm erzeugt werden, können Sie einen Browser oder andere Tools verwenden. Weitere Informationen finden Sie im Abschnitt [Audiodatei wiedergeben](/docs/services/text-to-speech?topic=text-to-speech-audioFormats#formatsPlay).
{: note}

## Schritt 2: Sprachausgabe synthetisch aus Text in Spanisch erstellen
{: #synthesizeSpanish}

Der folgende Befehl verwendet die Methode `GET /v1/synthesize`, um aus Eingabe in Spanisch synthetisch eine Audiodatei zu erstellen.

1.  Geben Sie den folgenden Befehl aus, um synthetisch eine Sprachausgabe für die Zeichenfolge 'hola mundo' zu erstellen und eine WAV-Datei namens `hola_mundo.wav` zu erzeugen. Der Eingabetext ist URL-codiert. Die Methode beinhaltet die Abfrageparameter `accept` zur Angabe des Audioformats und `voice` zur Angabe der Stimme für Spanisch namens `es-ES_EnriqueVoice`.
    -   {: hide-dashboard} Ersetzen Sie hierbei `{api-schlüssel}` und `{url}` durch Ihren API-Schlüssel und Ihre URL.

    ```bash
    curl -X GET -u "apikey:{api-schlüssel}"{: apikey} \
    --output hola_mundo.wav \
    "{url}/v1/synthesize?accept=audio%2Fwav&text=hola%20mundo&voice=es-ES_EnriqueVoice"{: url}
    ```
    {: pre}

## Nächste Schritte

-   Informieren Sie sich im Abschnitt [HTTP-Schnittstelle](/docs/services/text-to-speech?topic=text-to-speech-usingHTTP) über die HTTP-Schnittstelle des Service.
-   Informieren Sie sich im Abschnitt [WebSocket-Schnittstelle](/docs/services/text-to-speech?topic=text-to-speech-usingWebSocket) über die WebSocket-Schnittstelle des Service.
-   Lesen Sie die ausführlichen Informationen zu den Methoden der Serviceschnittstelle in der [API-Referenz](https://{DomainName}/apidocs/text-to-speech){: external}.
