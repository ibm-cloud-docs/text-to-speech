---

copyright:
  years: 2015, 2019
lastupdated: "2019-03-14"

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

Zur Authentifizierung verwendet das
Lernprogramm API-Schlüssel von {{site.data.keyword.cloud}}
Identity and Access
Management (IAM). Ältere Serviceinstanzen verwenden für die
Authentifizierung unter Umständen weiterhin die Werte für
`{username}` (Benutzername) und
`{password}` (Kennwort) aus ihren bestehenden Cloud
Foundry-Serviceberechtigungsnachweisen. Verwenden Sie für die Authentifizierung
die Methode, die für Ihre Serviceinstanz geeignet ist. Weitere Angaben über die
Verwendung der IAM-Authentifizierung durch den Service finden Sie unter
[Serviceaktualisierung
vom 30. Oktober 2018](/docs/services/text-to-speech/release-notes.html#October2018) in den Releaseinformationen.
{: important}

## Vorbereitende Schritte
{: #before-you-begin}

- {: hide-dashboard}  Erstellen Sie eine Instanz des Service:
    1.  {: hide-dashboard} Rufen Sie die Seite [{{site.data.keyword.texttospeechshort}} ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://{DomainName}/catalog/services/text-to-speech){: new_window} im {{site.data.keyword.cloud_notm}}-Katalog auf.
    1.  {: hide-dashboard} Registrieren Sie sich für ein kostenloses {{site.data.keyword.cloud_notm}}-Konto oder melden Sie sich an.
    1.  {: hide-dashboard} Klicken Sie auf **Erstellen**.
-   Kopieren Sie die Berechtigungsnachweise zur Authentifizierung bei Ihrer Serviceinstanz:
    1.  {: hide-dashboard} Klicken Sie im [{{site.data.keyword.cloud_notm}}-Dashboard ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://{DomainName}/dashboard/apps){: new_window} auf Ihre {{site.data.keyword.texttospeechshort}}-Serviceinstanz, um auf die Dashboardseite für den {{site.data.keyword.texttospeechshort}}-Service zu wechseln.
    1.  Klicken Sie auf der Seite **Verwalten** auf **Anzeigen**, um Ihre Berechtigungsnachweise anzuzeigen.
    1.  Kopieren Sie die Werte für den `API-Schlüssel` und die `URL`.
-   Vergewissern Sie sich, dass der Befehl `curl` verfügbar ist.
    -   Die Beispiele verwenden den Befehl `curl`, um Methoden der HTTP-Schnittstelle aufzurufen. Installieren Sie ausgehend von der Seite [curl.haxx.se ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://curl.haxx.se/){: new_window} die Version für Ihr Betriebssystem. Installieren Sie die Version, die das Protokoll 'Secure Sockets Layer' (SSL) unterstützt. Nehmen Sie unbedingt die installierte Binärdatei in Ihre Umgebungsvariable `PATH` auf.

Ersetzen Sie bei der Eingabe eines Befehls die Platzhalter `{api-schlüssel}` und `{url}` durch Ihre tatsächlichen Werte für den API-Schlüssel und die URL. Lassen Sie die geschweiften Klammern, die einen Variablenwert kenntlich machen, dabei weg. Ein tatsächlicher Wert sieht etwa wie im folgenden Beispiel aus: {: hide-dashboard}

```bash
curl -X POST -u "apikey:L_HALhLVIksh1b73l97LSs6R_3gLo4xkujAaxm7i-b9x"
. . .
"https://stream.watsonplatform.net/text-to-speech/api/v1/synthesize"
```
{:pre}
{: hide-dashboard}

Zur Wiedergabe der Audiodateien, die durch die Beispiele in diesem Lernprogramm erzeugt werden, können Sie einen Browser oder andere Tools verwenden. Weitere Informationen finden Sie im Abschnitt [Audiodatei wiedergeben](/docs/services/text-to-speech/audio-formats.html#formatsPlay).
{: note}

## Schritt 1: Synthetische Sprachausgabe aus Text in amerikanischem Englisch erstellen
{: #synthesizeEnglish}

Die folgenden Befehle verwenden die Methode `POST /v1/synthesize`, um aus Eingabe in amerikanischem Englisch synthetisch Audiodateien in zwei unterschiedlichen Formaten zu erstellen. Beide Anforderungen verwenden die Standardstimme für amerikanisches Englisch `en-US_MichaelVoice`.

1.  Geben Sie den folgenden Befehl aus, um für die Zeichenfolge 'hello world' synthetisch Sprachausgabe zu erstellen und eine WAV-Datei namens `hello_world.wav` zu erzeugen.
    -   {: hide-dashboard}Ersetzen Sie hierbei `{api-schlüssel}` und `{url}` durch Ihren API-Schlüssel und Ihre URL.

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
    -   {: hide-dashboard}Ersetzen Sie hierbei `{api-schlüssel}` und `{url}` durch Ihren API-Schlüssel und Ihre URL.

    ```bash
    curl -X POST -u "apikey:{api-schlüssel}"{: apikey} \
    --header "Content-Type: application/json" \
    --data "{\"text\":\"hello world\"}" \
    --output hello_world.ogg \
    "{url}/v1/synthesize"{: url}
    ```
    {: pre}

## Schritt 2: Sprachausgabe synthetisch aus Text in Spanisch erstellen
{: #synthesizeSpanish}

Der folgende Befehl verwendet die Methode `GET /v1/synthesize`, um aus Eingabe in Spanisch synthetisch eine Audiodatei zu erstellen.

1.  Geben Sie den folgenden Befehl aus, um synthetisch eine Sprachausgabe für die Zeichenfolge 'hola mundo' zu erstellen und eine WAV-Datei namens `hola_mundo.wav` zu erzeugen. Der Eingabetext ist URL-codiert. Die Methode beinhaltet die Abfrageparameter `accept` zur Angabe des Audioformats und `voice` zur Angabe der Stimme für Spanisch namens `es-ES_EnriqueVoice`.
    -   {: hide-dashboard}Ersetzen Sie hierbei `{api-schlüssel}` und `{url}` durch Ihren API-Schlüssel und Ihre URL.

    ```bash
    curl -X GET -u "apikey:{api-schlüssel}"{: apikey} \
    --output hola_mundo.wav \
    "{url}/v1/synthesize?accept=audio%2Fwav&text=hola%20mundo&voice=es-ES_EnriqueVoice"{: url}
    ```
    {: pre}

## Nächste Schritte

-   Informieren Sie sich im Abschnitt [HTTP-Schnittstelle](/docs/services/text-to-speech/http.html) über die HTTP-Schnittstelle des Service.
-   Informieren Sie sich im Abschnitt [WebSocket-Schnittstelle](/docs/services/text-to-speech/websockets.html) über die WebSocket-Schnittstelle des Service.
-   Lesen Sie die ausführlichen Informationen zu den Methoden der Serviceschnittstelle in der [API-Referenz. ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://{DomainName}/apidocs/text-to-speech){: new_window}
