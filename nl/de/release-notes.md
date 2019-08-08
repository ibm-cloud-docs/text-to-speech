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

# Releaseinformationen
{: #release-notes}

In den folgenden Abschnitten sind die neuen Funktionen und die Änderungen dokumentiert, die bei jedem Release und jeder Aktualisierung des {{site.data.keyword.texttospeechfull}}-Service aufgenommen wurden. Die Informationen enthalten alle bekannten Einschränkungen. Sofern nicht anders angegeben, sind alle Änderungen mit früheren Releases kompatibel sowie automatisch und transparent für alle neuen und vorhandenen Anwendungen verfügbar.
{: shortdesc}

## Bekannte Einschränkungen
{: #limitations}

Zu diesem Zeitpunkt sind keine bekannten Einschränkungen bekannt.

## 30. Juli 2019
{: #July2019}

Der Service bietet nun eine neuronale Stimme in Japanisch: `ja-JP_EmiV3Voice`. Es stehen nun sowohl Standard- als auch neuronale Versionen aller verfügbaren Stimmen in allen unterstützten Sprachen zur Verfügung. Weitere Informationen finden Sie unter [Sprachen und Stimmen](/docs/services/text-to-speech?topic=text-to-speech-voices).

## 24. Juni 2019
{: #June2019}

-   Der Service bietet nun zwei Versionen der meisten seiner verfügbaren Stimmen an:
    -   [Standardstimmen](/docs/services/text-to-speech?topic=text-to-speech-voices#standardVoices), die eine konkatenative Synthese verwenden, um Segmente der aufgezeichneten Sprache zusammenzusetzen, um die aufgezeichnete Audioausgabe zu generieren. Standardstimmen enthalten keine Versionszeichenfolge in ihrem Namen (z. B. `en-US_AllisonVoice`).
    -   [Neuronale Stimmen](/docs/services/text-to-speech?topic=text-to-speech-voices#neuralVoices), die Deep Neural Networks (DNNs) verwenden, um die akustischen (spektralen) Merkmale der Sprache vorherzusagen. Neuronale Stimmen enthalten eine Versionszeichenfolge (`V3`) in ihrem Namen (z. B. `en-US_AllisonV3Voice`).

    Erweiterte neuronale Versionen sind für alle Standardstimmen verfügbar, mit Ausnahme der Stimme `ja-JP_EmiVoice`, die bald verfügbar sein wird. Die SSML-Elemente `<express-as>` und `<voice-transformation>` können nicht mit den neuronalen Stimmen verwendet werden. Und Sie können das Attribut `volume` des Elements `<prosody>` nicht mit den neuronalen Stimmen verwenden.

    Weitere Informationen zu den verfügbaren Stimmen finden Sie unter [Sprachen und Stimmen](/docs/services/text-to-speech?topic=text-to-speech-voices).
-   Der Service enthält nicht mehr die zuvor verfügbaren `V2`-DNN-Stimmen. Wenn Sie eine `V2`-Stimme in Ihrer Anwendung verwenden, verwendet der Service stattdessen automatisch die entsprechende `V3`-Stimme.

## 24. März 2019
{: #March2019c}

-   Der Service bietet jetzt `V2`DNN-Versionen (DNN; Deep Neural Network) für die deutschen Stimmen:
    -   `de-DE_BirgitV2Voice`
    -   `de-DE_DieterV2Voice`

    Weitere Informationen zu DNN-basierten Stimmen finden Sie unter [Sprachen und Stimmen](/docs/services/text-to-speech?topic=text-to-speech-voices).-   Alle DNN-basierten Stimmen des Service unterstützen künftig die Attribute `pitch` und `rate` des SSML-Elements `<prosody>`. Das Attribut `volume` des Elements `<prosody>` wird von den DNN-basierten Stimmen nicht unterstützt. Weitere Informationen enthält der Abschnitt [Element 'prosody'](/docs/services/text-to-speech?topic=text-to-speech-elements#prosody_element).

## Ältere Releases
{: #older}

-   [21. März 2019](#March2019b)
-   [4. März 2019](#March2019a)
-   [28. Januar 2019](#January2019)
-   [13. Dezember 2018](#December2018)
-   [7. November 2018](#November2018)
-   [30. Oktober 2018](#October2018)
-   [12. Juni 2018](#June2018)
-   [15. Mai 2018](#May2018)
-   [2. Oktober 2017](#October2017)
-   [14. Juli 2017](#July2017)
-   [10. April 2017](#April2017)
-   [1. Dezember 2016](#December2016)
-   [22. September 2016](#September2016)
-   [23. Juni 2016](#June2016)
-   [10. März 2016](#March2016)
-   [22. Februar 2016](#February2016)
-   [17. Dezember 2015](#December2015)
-   [21. September 2015](#September2015)
-   [1. Juli 2015](#July2015)

### 21. März 2019
{: #March2019b}

Benutzer können nun ausschließlich Informationen zu Serviceberechtigungsnachweisen für die Rolle anzeigen, die ihrem {{site.data.keyword.cloud_notm}}-Konto zugeordnet ist. Falls Ihnen beispielsweise die Rolle `Leseberechtigter` zugeordnet ist, sind Serviceberechtigungsnachweise der Ebene `Schreibberechtigter` oder einer höheren Ebene für Sie nicht mehr sichtbar.

Diese Änderung betrifft nicht den API-Zugriff für Benutzer oder Anwendungen mit bestehenden Serviceberechtigungsnachweisen. Sie wirkt sich lediglich auf das Anzeigen von Berechtigungsnachweisen in {{site.data.keyword.cloud_notm}} aus.

Weitere Informationen zu Serviceschlüsseln und Benutzerrollen enthält der Abschnitt [Service-API-Schlüssel von IAM](/docs/services/watson?topic=watson-api-key-bp#api-key-bp).

### 4. März 2019
{: #March2019a}

Der Service bietet nun vier neue `V2`-Stimmen, die Audioausgabe mithilfe einer Deep-Learning-Synthese generieren:

-   `it-IT_FrancescaV2Voice`
-   `en-US_AllisonV2Voice`
-   `en-US_LisaV2Voice`
-   `en-US_MichaelV2Voice`

Diese neuen Stimmen verwenden maschinelles Lernen und DNN, um synthetisch Sprache aus Text zu erstellen. Die auch als 'DNN-basiert' (Deep Neural Network ) bezeichnete Deep-Learning-Synthese erzeugt Audioausgabe mit einem natürlicheren Satzrhythmus und einer konsistenteren Gesamtqualität.

Die neuen Stimmen erzeugen auch Audioausgabe mit unterschiedlicher Signalqualität, weshalb sie möglicherweise nicht für alle Anwendungen geeignet sind. Außerdem werden die SSML-Elemente `<prosody>`, `<express-as>` und `<voice-transformation>` von den neuen Stimmen nicht unterstützt.

Weitere Informationen zu diesen DNN-basierten Stimmen und ihren Unterschieden zu den vorhandenen Stimmen finden Sie unter [Sprachen und Stimmen](/docs/services/text-to-speech?topic=text-to-speech-voices).

### 28. Januar 2019
{: #January2019}

Die WebSocket-Schnittstelle unterstützt jetzt die tokenbasierte Authentifizierung von Identity and Access Management (IAM) für browserbasierten JavaScript-Code. Die anderslautende Einschränkung besteht nicht mehr. So können Sie eine authentifizierte Verbindung mit der WebSocket-Methode `/v1/synthesize` herstellen:

-   Beziehen Sie bei Verwendung der Authentifizierung mit IAM den Abfrageparameter `access_token` ein.
-   Beziehen Sie bei Verwendung von Cloud Foundry-Serviceberechtigungsnachweisen den Abfrageparameter `watson-token` ein.

Weitere Informationen hierzu finden Sie unter [Verbindung öffnen](/docs/services/text-to-speech?topic=text-to-speech-usingWebSocket#WSopen).

### 13. Dezember 2018
{: #December2018}

Der {{site.data.keyword.texttospeechshort}}-Service ist jetzt am {{site.data.keyword.cloud}}-Standort London verfügbar (**eu-gb**). Wie alle Standorte verwendet auch der Standort London die tokenbasierte Authentifizierung von Identity and Access Management (IAM). Alle neuen Serviceinstanzen, die Sie an diesem Standort erstellen, verwenden die IAM-Authentifizierung.

### 7. November 2018
{: #November2018}

Der {{site.data.keyword.texttospeechshort}}-Service ist jetzt am {{site.data.keyword.cloud}}-Standort Tokio verfügbar (**jp-tok**). Wie alle Standorte verwendet auch der Standort Tokio die tokenbasierte Authentifizierung von Identity and Access Management (IAM). Alle neuen Serviceinstanzen, die Sie an diesem Standort erstellen, verwenden die IAM-Authentifizierung.

### 30. Oktober 2018
{: #October2018}

Der {{site.data.keyword.texttospeechshort}}-Service wurde für alle Standorte auf die tokenbasierte Authentifizierung von Identity and Access Management (IAM) migriert. Alle {{site.data.keyword.cloud_notm}}-Services verwenden jetzt die IAM-Authentifizierung. Der {{site.data.keyword.texttospeechshort}}-Service wurde an allen Standorten jeweils am nachfolgend angegebenen Datum migriert:

-   Dallas (**us-south**): 30. Oktober 2018
-   Frankfurt (**eu-de**): 30. Oktober 2018
-   Washington, DC (**us-east**): 12. Juni 2018
-   Sydney (**au-syd**): 15. Mai 2018

Die Migration auf die IAM-Authentifizierung wirkt sich bei neuen und vorhandenen Serviceinstanzen unterschiedlich aus:

-   *Alle neuen Serviceinstanzen, die Sie an einem beliebigen Standort erstellen,* verwenden jetzt die IAM-Authentifizierung für den Zugriff auf den Service. Sie können entweder ein Trägertoken oder einen API-Schlüssel übergeben: Tokens unterstützen authentifizierte Anforderungen, ohne dass in jeden Aufruf Serviceberechtigungsnachweise integriert werden müssen; API-Schlüssel verwenden die HTTP-Basisauthentifizierung. Wenn Sie eines der {{site.data.keyword.ibmwatson}}-SDKs verwenden, können Sie den API-Schlüssel übergeben und das SDK den Lebenszyklus der Tokens verwalten lassen.
-   *Bestehende Serviceinstanzen, die Sie vor dem Migrationsdatum an einem Standort erstellt haben,* verwenden zur Authentifizierung weiterhin die Werte für `{username}` (Benutzername) und `{password}` (Kennwort) aus ihren vorherigen Cloud Foundry-Serviceberechtigungsnachweisen, bis Sie sie auf die Verwendung der IAM-Authentifizierung migrieren. Weitere Informationen zur Migration auf die IAM-Authentifizierung finden Sie unter [Cloud Foundry-Serviceinstanzen auf eine Ressourcengruppe migrieren](https://{DomainName}/docs/resources?topic=resources-migrate).

Zusätzliche Angaben können Sie der folgenden Dokumentation entnehmen:

-   Um das von Ihrer Serviceinstanz verwendete Authentifizierungsverfahren zu ermitteln, klicken Sie im [{{site.data.keyword.cloud_notm}}-Dashboard](https://{DomainName}/dashboard/apps){: external} auf die Instanz.
-   Weitere Informationen zur Verwendung von IAM-Tokens bei {{site.data.keyword.watson}}-Services enthält der Abschnitt [Authentifizierung mit IAM-Tokens durchführen](/docs/services/watson?topic=watson-iam).
-   Zusätzliche Angaben über die Verwendung von IAM-API-Schlüsseln bei {{site.data.keyword.watson}}-Services enthält der Abschnitt [Service-API-Schlüssel von IAM](/docs/services/watson?topic=watson-api-key-bp).
-   Beispiele mit Verwendung der IAM-Authentifizierung sind in der [API-Referenz](https://{DomainName}/apidocs/text-to-speech){: external}.

### 12. Juni 2018
{: #June2018}

Die folgenden Funktionen wurden für Anwendungen aktiviert, die am Standort Washington, DC (**us-east**) gehostet werden:

-   Der Service unterstützt jetzt einen neuen API-Authentifizierungsprozess. Weitere Informationen können Sie dem Abschnitt über die Serviceaktualisierung vom [30. Oktober 2018](#October2018) entnehmen.
-   Der Service unterstützt jetzt den Header `X-Watson-Metadata` und die Methode `DELETE /v1/user_data`. Weitere Informationen finden Sie unter [Informationssicherheit](/docs/services/text-to-speech?topic=text-to-speech-information-security).

### 15. Mai 2018
{: #May2018}

Die folgenden Funktionen wurden für Anwendungen aktiviert, die am Standort Sydney (**au-syd**) gehostet werden:

-   Der Service unterstützt jetzt einen neuen API-Authentifizierungsprozess. Weitere Informationen können Sie dem Abschnitt über die Serviceaktualisierung vom [30. Oktober 2018](#October2018) entnehmen.
-   Der Service unterstützt jetzt den Header `X-Watson-Metadata` und die Methode `DELETE /v1/user_data`. Weitere Informationen finden Sie unter [Informationssicherheit](/docs/services/text-to-speech?topic=text-to-speech-information-security).

### 2. Oktober 2017
{: #October2017}

Beim Format `audio/l16` können Sie künftig optional einen Endianess-Wert für die zurückgegebene Audioausgabe angeben. (Die Abtastfrequenz mussten Sie bereits angeben.) Beispiele sind `audio/l16;rate=22050;endianness=big-endian` und `audio/l16;rate=22050;endianness=little-endian`; Standardeinstellung ist Big Endian. Weitere Informationen finden Sie unter [Audioformate](/docs/services/text-to-speech?topic=text-to-speech-audioFormats).

### 14. Juli 2017
{: #July2017}

Der Service unterstützt jetzt das Audio-Format 'MP3' oder 'Motion Picture Experts Group' (MPEG). Weitere Informationen zu unterstützten Audioformaten finden Sie unter [Audioformate](/docs/services/text-to-speech?topic=text-to-speech-audioFormats).

### 10. April 2017
{: #April2017}

-   Der Service unterstützt nun das Audioformat 'Web Media' (WebM) mit dem Opus- oder Vorbis-Codec. Außerdem unterstützt er das Audioformat 'Ogg' nun zusätzlich zum Opus-Codec mit dem Vorbis-Codec. Weitere Informationen zu unterstützten Audioformaten finden Sie unter [Audioformate](/docs/services/text-to-speech?topic=text-to-speech-audioFormats).
-   Der Service unterstützt jetzt Cross-Origin Resource Sharing (CORS), damit browserbasierte Clients den Service direkt aufrufen können. Weitere Informationen enthält der Abschnitt [CORS-Unterstützung](/docs/services/text-to-speech?topic=text-to-speech-overview#cors).
-   Die HTTP-Antwortcodes für den erfolgreichen Abschluss einiger Methoden der Anpassungsschnittstelle wurden geändert:
    -   Die Methode `POST /v1/customizations` gibt jetzt 201 (anstelle von 200) zurück.
    -   Die Methode `POST /v1/customizations/{customization_id}` gibt jetzt 200 (anstelle von 201) zurück.
    -   Die Methode `POST /v1/customizations/{customization_id}/words` gibt jetzt 200 (anstelle von 201) zurück.
    -   Die Methode `PUT /v1/customizations/{customization_id}/words/{word}` gibt jetzt 200 (anstelle von 201) zurück.
-   Die Methoden `POST /v1/customizations/{custom_id}/words` und `PUT /v1/customizations/{customization_id}/words/{word}` geben jetzt den HTTP-Antwortcode 400 mit der Fehlernachricht `Part of speech is supported for ja-JP language only` zurück, falls Sie versuchen, bei einer anderen Sprache als Japanisch eine Wortart (Attribut `part_of_speech`) anzugeben.
-   Die Methode `POST /v1/customizations/{custom_id}/words` gibt jetzt einen leeren Antworthauptteil (`{}`) zurück.

### 1. Dezember 2016
{: #December2016}

-   Der Service enthält eine neue Stimme namens `es-LA_SofiaVoice`. Sie ist das lateinamerikanische Äquivalent zur Stimme `es-US_SofiaVoice`. Der größte Unterschied zwischen den beiden Stimmen besteht in ihrer Interpretation eines Dollarzeichens (`$`): Die lateinamerikanische Version verwendet den Begriff *pesos*, während die nordamerikanische Version den Begriff *dolares* verwendet. Darüber hinaus kann es einige geringere Unterschiede zwischen den beiden Stimmen geben.
-   Neben `en-US_AllisonVoice` können nun zwei weitere Stimmen mit der SSML-Stimmenumwandlung verändert werden: `en-US_LisaVoice` und `en-US_MichaelVoice`. Weitere Informationen zur Stimmenumwandlung enthält der Abschnitt [SSML für Stimmenumwandlung](/docs/services/text-to-speech?topic=text-to-speech-transformation).
-   Bei Verwendung der Anpassungsschnittstelle in Verbindung mit Japanisch verwendet der Service jetzt als Übereinstimmung das längste Wort aus den Paaren für Wort und Umsetzung, die für ein angepasstes Sprechmodell definiert sind. Dies soll an den beiden folgenden Beispieleinträgen für eine angepasste Stimme erläutert werden:

    <pre><code data-copy="false" class="language-javascript">  {
      "words": [
        {"word":"&#65326;&#65337;", "translation":"&#12491;&#12517;&#12540;&#12520;&#12540;&#12463;", "part_of_speech":"Mesi"},
        {"word":"&#65326;&#65337;&#65315;", "translation":"&#12491;&#12517;&#12540;&#12520;&#12540;&#12463;&#12471;&#12486;&#12451;", "part_of_speech":"Mesi"}
      ]
    }</code></pre>

    Falls der Service im Eingabetext die Zeichenfolge <code>&#65326;&#65337;&#65315;</code> findet, verwendet er dieses Wort als Übereinstimmung, weil es eine längere Übereinstimmung als <code>&#65326;&#65337;</code> ist. Zuvor hätte der Service die Zeichenfolge <code>&#65326;&#65337;</code> als Übereinstimmung verwendet. Weitere Informationen zur Arbeit mit Einträgen für ein angepasstes Sprechmodell in Japanisch enthält der Abschnitt [Mit Einträgen in Japanisch arbeiten](/docs/services/text-to-speech?topic=text-to-speech-rules#jaNotes).

### 22. September 2016
{: #September2016}

-   Die Anpassungsschnittstelle, die die Methoden 'customization' und `GET /v1/pronunciation` umfasst, ist nun für alle vom Service unterstützten Sprachen verfügbar. Die Schnittstelle liegt weiterhin als Betaversion vor. Weitere Informationen enthält der Abschnitt [Wissenswertes über die Anpassung](/docs/services/text-to-speech?topic=text-to-speech-customIntro).
-   Der Service unterstützt jetzt SSML (Speech Synthesis Markup Language) für Japanisch. Allgemeine Informationen zur SSML-Unterstützung finden Sie unter [SSML verwenden](/docs/services/text-to-speech?topic=text-to-speech-ssml). Angaben über SPR- und IPA-Symbole für Japanisch enthält der Abschnitt [Symbole für Japanisch](/docs/services/text-to-speech?topic=text-to-speech-jaSymbols). Für die Erstellung von Einträgen für Wörter in einem angepassten Sprechmodell für Japanisch gibt es zusätzliche Hinweise und ein Feld `part_of_speech`. Näheres hierzu ist im Abschnitt [Mit Einträgen in Japanisch arbeiten](/docs/services/text-to-speech?topic=text-to-speech-rules#jaNotes) zu finden.
-   Der Service bietet jetzt durch das neue Element `<voice-transformation>` die Möglichkeit zur SSML-Stimmenumwandlung. Sie können die Palette der möglichen Stimmen vergrößern, indem Sie angepasste Stimmenumwandlungen erstellen, die die Tonhöhe, den Tonumfang, den Glottisdruck, die Aspiration, das Tempo und das Timbre einer Stimme ändern. Der Service bietet außerdem zwei integrierte virtuelle Stimmen namens *Young* und *Soft*. Gegenwärtig wird die Stimmenumwandlung vom Service nur bei der Stimme 'Allison' für amerikanisches Englisch unterstützt. Weitere Informationen enthält der Abschnitt [SSML für Stimmenumwandlung](/docs/services/text-to-speech?topic=text-to-speech-transformation).
-   Der Service kann jetzt für alle Zeichenfolgen des Eingabetextes, den Sie an die WebSocket-Schnittstelle übergeben, Worttaktinformationen zurückgeben. Um die Start- und die Endzeit jeder Zeichenfolge in der Eingabe zu erhalten, geben Sie ein Array an, das die Zeichenfolge `words` für den optionalen Parameter `timings` des JSON-Objekts enthält, das Sie an den Service übergeben. Für Eingabetext in Japanisch ist die Funktion gegenwärtig nicht verfügbar. Weitere Informationen finden Sie unter [Worttakt abrufen](/docs/services/text-to-speech?topic=text-to-speech-timing).
-   Der Service validiert jetzt alle SSML-Elemente, die Sie in einem beliebigen Inhalt übergeben. Falls er einen ungültigen Tag findet, meldet der Service einen HTTP-Antwortcode 400 mit einer beschreibenden Nachricht und die Methode schlägt fehl. In früheren Releases hat der Service Fehler nicht auf konsistente Weise abgewickelt; beispielsweise konnte die Angabe einer ungültigen Aussprache für ein Wort zu einem unvorhersehbaren oder inkonsistenten Verhalten führen. Weitere Informationen finden Sie unter [SSML-Validierung](/docs/services/text-to-speech?topic=text-to-speech-ssml#errors).
-   Die Verwendung des Arguments `spr` für die Option `format` der Methode `GET /v1/pronunciation` und beim Attribut `alphabet` eines SSML-Elements `<phoneme>` wird künftig nicht weiter unterstützt. Verwenden Sie zur Verwendung der Schreibweise gemäß {{site.data.keyword.IBM_notm}} Symbolic Phonetic Representation (SPR) in allen Fällen das Argument `ibm` anstelle von `spr`.
-   Die Liste der unterstützten Audioformate umfasst jetzt auch `audio/mulaw;rate=8000`. Wie bei `audio/basic` handelt es sich hierbei um ein Einzelkanalaudioformat, das mithilfe von 8-Bit-U-Law-Daten (oder Mu-Law-Daten) mit einer Abtastfrequenz von 8 kHz codiert wird. Weitere Informationen finden Sie unter [Audioformate](/docs/services/text-to-speech?topic=text-to-speech-audioFormats).
-   Die Methoden `GET /v1/voices` und `GET /v1/voices/{voice}` geben jetzt als Teil der Ausgabe für jede Stimme ein Objekt `supported_features` zurück. Das Objekt beschreibt, ob die Stimme eine Anpassung und das SSML-Element `<voice_transformation>` unterstützt. Weitere Informationen finden Sie unter [Sprachen und Stimmen](/docs/services/text-to-speech?topic=text-to-speech-voices).

### 23. Juni 2016
{: #June2016}

-   Der Service bietet jetzt für die synthetische Erstellung von Sprache aus Text eine WebSocket-Schnittstelle. Die Schnittstelle bietet dieselben Funktionen wie die Methode `/v1/synthesize` der HTTP-Schnittstelle. Sie akzeptiert einfachen Text oder Text mit der XML-basierten Markup-Sprache 'Speech Synthesis Markup Language' (SSML). Außerdem unterstützt sie die Verwendung des SSML-Elements `<mark>`, mit dem der Zeitpunkt in der Audioausgabe ermittelt werden kann, an dem die synthetische Erstellung von Sprache aus dem gesamten Text endet, der der Markierung vorausgeht. Weitere Informationen finden Sie im Abschnitt [WebSocket-Schnittstelle](/docs/services/text-to-speech?topic=text-to-speech-usingWebSocket).
-   Der Service unterstützt jetzt mit SSML annotierten Text bei kastilischem und nordamerikanischem Spanisch, Italienisch und brasilianischem Portugiesisch. Die Verwendung von SSML wurde vom Service zuvor bereits für amerikanisches und britisches Englisch, Französisch sowie Deutsch unterstützt. Ab dieser Aktualisierung unterstützt der Service SSML bei allen Sprachen außer Japanisch. Darüber hinaus können Sie sowohl {{site.data.keyword.IBM_notm}} SPR als auch IPA als Schreibweise zum Definieren von Wortaussprachevarianten mit dem SSML-Element `<phoneme>` verwenden. Weitere Informationen enthalten die Abschnitte [SSML verwenden](/docs/services/text-to-speech?topic=text-to-speech-ssml) und [IBM SPR verwenden](/docs/services/text-to-speech?topic=text-to-speech-sprs).

    Bei amerikanischem Englisch können Sie mit dem SSML-Element `<phoneme>`
    außerdem Worteinträge in einem angepassten Sprechmodell erstellen; die
    Anpassung wird nur für amerikanisches Englisch unterstützt. Weitere Informationen enthält der
    Abschnitt [Wissenswertes
    über die Anpassung](/docs/services/text-to-speech?topic=text-to-speech-customIntro).
-   Der Service bietet für die am häufigsten verwendeten Stimmen eine verbesserte Expressivität und Natürlichkeit. Grundlage der Verbesserungen ist die auf Recursive Neural Network (RNN) basierende Prosodievorhersage aus dem Eingabetext. Diese Verbesserungen werden als neue Service-Engine und Sprechmodellaktualisierungen für die folgenden Sprachen verfügbar gemacht:

    -   `en-US_AllisonVoice`
    -   `en-US_LisaVoice`
    -   `en-US_MichaelVoice`
    -   `es-ES_EnriqueVoice`
    -   `fr-FR_ReneeVoice`
-   Die Methode `GET /v1/pronunciation` akzeptiert jetzt den optionalen Abfrageparameter `customization_id`. Der Parameter ruft eine Wortumsetzung aus einem angegebenen angepassten Sprechmodell ab. Falls das Wort im Sprechmodell nicht enthalten ist, gibt die Methode die Standardaussprache für das Wort zurück. Weitere Informationen finden Sie in der [API-Referenz](https://{DomainName}/apidocs/text-to-speech){: external}.

    Bei Verwendung der Methode `GET /v1/pronunciation` ohne Anpassungs-ID und für eine andere Sprache als amerikanisches Englisch können Sie die Aussprache eines Wortes nur in der Schreibweise nach {{site.data.keyword.IBM_notm}} SPR anfordern. Für eine andere Sprache als amerikanisches Englisch müssen Sie `spr` mit der Option `format` der Methode angeben.
    {: note}
-   Die Liste der unterstützten Audioformate umfasst jetzt auch `audio/basic`. Dieses Format stellt eine Einkanalaudioausgabe mit in 8-Bit-U-Law (oder Mu-Law) codierten Daten und einer Abtastfrequenz von 8 kHz bereit. Weitere Informationen finden Sie unter [Audioformate](/docs/services/text-to-speech?topic=text-to-speech-audioFormats).
-   Die HTTP- und WebSocket-Methoden `/v1/synthesize` können eine Antwort des Typs `warnings` zurückgeben, die Nachrichten über ungültige Abfrageparameter oder JSON-Felder in einer Anforderung enthält. Das Format der Warnungen wurde geändert. Das folgende Beispiel zeigt das vorherige Format:

    `"warnings": "Unknown arguments: [u'{ungültiges_argument_1}', u'{ungültiges_argument_2}']."`

    Dieselbe Warnung hat jetzt das folgende Format:

    `"warnings": "Unknown arguments: {ungültiges_argument_1}, {ungültiges_argument_2}."`

### 10. März 2016
{: #March2016}

-   Die Methoden `GET` und `POST /v1/synthesize` können jetzt einen Antwortheader namens `Warnings` zurückgeben, der eine Liste mit Warnungen über ungültige Abfrageparameter oder JSON-Felder in der Anforderung enthält. Jedes Element der Liste beinhaltet eine Zeichenfolge, die die Art der Warnung beschreibt und auf die ein Array der ungültigen Argumentzeichenfolgen folgt; z. B. `Unknown arguments: [u'{ungültiges_argument_1}', u'{ungültiges_argument_2}'].` Weitere Informationen finden Sie in der [API-Referenz](https://{DomainName}/apidocs/text-to-speech){: external}.
-   Die Betaversion von *{{site.data.keyword.watson}} Speech Software Development Kit (SDK) for the Apple&reg; iOS operating system* wird nicht mehr unterstützt und wurde durch *{{site.data.keyword.watson}} Swift SDK* ersetzt. Das neue SDK ist im [Repository 'swift-sdk'](https://github.com/watson-developer-cloud/swift-sdk){: external} im Namensbereich `watson-developer-cloud` bei GitHub verfügbar.

### 22. Februar 2016
{: #February2016}

Der Service wurde mit einer neuen SSML-Funktion für die Expressivität aktualisiert. Er erweitert SSML (Speech Synthesis Markup Language) durch ein Element `<express-as>`, mit dem Sie für die Expressivität einen der drei Sprechstile `GoodNews` (= Gute Neuigkeiten), `Apology` (= Entschuldigung) oder `Uncertainty` (= Unsicherheit) angeben können. Das Element kann auf den gesamten Text, einen Satz, einen Ausdruck oder ein Wort angewendet werden. Die Expressivität wird vom Service gegenwärtig nur bei der Stimme 'Allison' für amerikanisches Englisch unterstützt (`en-US_AllisonVoice`). Weitere Informationen finden Sie unter [SSML für Expressivität](/docs/services/text-to-speech?topic=text-to-speech-expressive).

### 17. Dezember 2015
{: #December2015}

-   Der Service bietet eine neue Anpassungsschnittstelle, mit der Sie angeben können, wie er ungewöhnliche Wörter aussprechen soll, die in der Eingabe enthalten sind. Die Schnittstelle umfasst eine Reihe von neuen Methoden, mit denen Sie angepasste Sprechmodelle sowie die darin enthaltenen Paare aus Wort und Umsetzung erstellen und verwalten können. Anschließend können Sie Ihre angepassten Modelle bei der synthetischen Erstellung von Audioausgabe aus Text verwenden.

    Der Service unterstützt gleich klingende und phonetische Umsetzungen. Phonetische Umsetzungen können entweder die Darstellung in IPA (International Phonetic Alphabet) oder das {{site.data.keyword.IBM_notm}} Format SPR (Symbolic Phonetic Representation) verwenden. Zur Angabe von phonetischen Umsetzungen verwenden Sie SSML (Speech Synthesis Markup Language).

    Die Anpassungsschnittstelle enthält eine Reihe von neuen HTTP-Methoden namens `POST /v1/customizations`, `POST /v1/customizations/{customization_id}`, `POST /v1/customizations/{customization_id}/words` und `PUT /v1/customizations/{customization_id}/words/{word}`. Außerdem bietet der Service eine neue Methode `GET /v1/pronunciation`, mit der die Aussprache für ein beliebiges Wort zurückgegeben wird, sowie die neue Methode `GET /v1/voices/{voice}`, die detaillierte Informationen zu einer bestimmten Stimme zurückgibt. Darüber hinaus akzeptieren die bereits vorhandenen Methoden der Serviceschnittstelle jetzt bei Bedarf Parameter für angepasste Sprechmodelle.

    Weitere Informationen zur Anpassung und der dafür verwendeten Schnittstelle enthalten der Abschnitt [Wissenswertes über die Anpassung](/docs/services/text-to-speech?topic=text-to-speech-customIntro) und die [API-Referenz](https://{DomainName}/apidocs/text-to-speech){: external}.

    Die Anpassungsschnittstelle liegt als Betaversion vor, die gegenwärtig nur amerikanisches Englisch unterstützt. Alle Anpassungsmethoden und die Methode `GET /v1/pronunciation` können derzeit nur zur Erstellung und Bearbeitung von angepassten Sprechmodellen und Wortumsetzungen für amerikanisches Englisch verwendet werden.
    {: note}
-   Der Service unterstützt eine neue Stimme namens `pt-BR_IsabelaVoice` für die synthetische Erstellung von Audioausgabe in brasilianischem Portugiesisch mit einer Frauenstimme. Weitere Informationen finden Sie unter [Sprachen und Stimmen](/docs/services/text-to-speech?topic=text-to-speech-voices).

### 21. September 2015
{: #September2015}

-   Für die Sprachservices sind zwei neue Software Development Kits (SDKs) für mobile Geräte verfügbar. Die SDKs ermöglichen mobilen Anwendungen eine Interaktion mit dem {{site.data.keyword.texttospeechshort}}-Service und dem {{site.data.keyword.speechtotextshort}}-Service. Mithilfe der SDKs können Sie Text an den {{site.data.keyword.texttospeechshort}}-Service senden und eine Sprachausgabe empfangen.
    -   Das *{{site.data.keyword.watson}} Swift SDK* ist im [Repository 'swift-sdk'](https://github.com/watson-developer-cloud/swift-sdk){: external} im Namensbereich `watson-developer-cloud` bei GitHub verfügbar.
    -   Das *{{site.data.keyword.watson}} Speech Android SDK* ist im [Repository 'speech-android-sdk'](https://github.com/watson-developer-cloud/speech-android-sdk){: external} im Namensbereich `watson-developer-cloud` bei GitHub verfügbar.

    Beide SDKs unterstützen die Authentifizierung bei den Sprachservices entweder mit Ihren {{site.data.keyword.cloud_notm}}-Serviceberechtigungsnachweisen oder mit einem Authentifizierungstoken.

    Da die SDKs als Betaversionen vorliegen, bleiben künftige Änderungen vorbehalten.
    {: note}
-   Der Service unterstützt jetzt mit Japanisch eine weitere Sprache. Die Stimme `ja-JP_EmiVoice` ist eine Frauenstimme für Japanisch.

### 1. Juli 2015
{: #July2015}

Der Service wurde am 1. Juli von einer Betaversion in eine Version mit allgemeiner Verfügbarkeit geändert. Zwischen der Betaversion und der allgemein verfügbaren Version der {{site.data.keyword.texttospeechshort}}-API bestehen die folgenden Unterschiede. Das allgemein verfügbare Release macht für die Benutzer ein Upgrade auf die neue Version des Service erforderlich.

-   Ein neues Programmiermodell unterstützt die direkte Interaktion zwischen einem Client und dem Service. Mithilfe dieses Modells kann ein Client ein Authentifizierungstoken zur direkten Kommunikation mit dem Service anfordern. Bei Verwendung des Tokens ist der Client nicht mehr gezwungen, eine serverseitige Proxy-Anwendung in {{site.data.keyword.cloud_notm}} zu nutzen, die den Service in seinem Namen aufruft. Tokens sind das bevorzugte Verfahren für die Interaktion von Clients mit dem Service.

    Der Service unterstützt weiterhin das alte Programmiermodell, das auf einem serverseitigen Proxy zur Weitergabe der Kommunikation und der Daten zwischen dem Client und dem Service verwendet wird. Das neue Modell ist jedoch effizienter und bietet einen höheren Durchsatz.
-   Sie können jetzt SSML (Speech Synthesis Markup Language) an die HTTP-Versionen `GET` und `POST` der Methode `/v1/synthesize` übergeben. SSML ist eine XML-basierte Markup-Sprache, die für die Bereitstellung von Annotationen von Text für Sprachsyntheseanwendungen wie den {{site.data.keyword.texttospeechshort}}-Service konzipiert wurde. Zusätzliche Informationen zur Übergabe von SSML-Eingabe an den Service finden Sie unter [Eingabetext angeben](/docs/services/text-to-speech?topic=text-to-speech-usingHTTP#input).

    Der Service unterstützt die Verwendung von SSML zunächst nur für britisches sowie amerikanisches Englisch, Französisch und Deutsch. Die Verwendung von SSML bei Italienisch und Spanisch wird durch den Service nicht unterstützt. Achten Sie bei Verwendung von SSML darauf, dass Sie für die Sprachausgabe keine Stimme in einer der nicht unterstützten Sprache auswählen. Die Ergebnisse in diesem Fall sind nicht sinnvoll.
-   Die Stimmen, die für synthetisch erstellte Sprache unterstützt werden, wurden geändert und erweitert. Der Service unterstützt bei der Methode `/v1/synthesize` jetzt eine Reihe zusätzlicher Stimmen, Sprachen und Dialekte. Zusätzliche Angaben über unterstützte Stimmen enthält der Abschnitt [Sprachen und Stimmen](/docs/services/text-to-speech?topic=text-to-speech-voices).

    In der allgemein verfügbaren Version wurden die in der Betaversion verfügbaren Stimmen umbenannt:
    -   `VoiceEnUsMichael` heißt jetzt `en-US_MichaelVoice`.
    -   `VoiceEnUsLisa` heißt jetzt `en-US_LisaVoice`.
    -   `VoiceEsEsEnrique` heißt jetzt `es-ES_EnriqueVoice`.

    Die vorherigen Namen der Stimmen können bei der Betaversion des Service (über die API-Endpunkte `-beta`) weiterhin verwendet werden, solange diese Version verfügbar bleibt. Bei der allgemein verfügbaren Version des Service müssen Sie jedoch die neuen Namen verwenden.
-   Sie können künftig anfordern, dass der Service Sprachausgabe im Format 'Free Lossless Audio Codec' (FLAC) zurückgibt. Der Service kann Sprachausgabe weiterhin im Format 'Ogg' mit dem Opus-Codec (Standardeinstellung) und im Format 'Waveform Audio File Format' (WAV) zurückgeben. Weitere Informationen zur Verwendung von Audioformaten bei den Methoden `/v1/synthesize` finden Sie unter [Audioformate](/docs/services/text-to-speech?topic=text-to-speech-audioFormats).
-   Der Text, den Sie an die Methode `/v1/synthesize` in der URL einer HTTP-Anforderung `GET` oder im Hauptteil einer HTTP-Anforderung `POST` senden, ist jetzt auf eine Größe vom maximal 5 KB begrenzt. Bei der Betaversion galt für den Text eine maximale Größe von 4 MB.
-   Bei der Methode `/v1/synthesize` können Sie jetzt durch eine Einbeziehung des Headers `X-WDC-PL-OPT-OUT` steuern, ob der Service Text und Audioergebnisse aus einer Operation nutzt, um künftige Ergebnisse zu verbessern. Geben Sie für den Header den Wert `1` an, um zu verhindern, dass der Service Text und Audioergebnisse nutzt. Der Parameter gilt nur für die aktuelle Anforderung. Der neue Header ersetzt den Header `X-logging` aus den Methoden der Betaversion. Weitere Informationen enthält der Abschnitt [Anforderungsprotokollierung für {{site.data.keyword.watson}}-Services steuern](/docs/services/watson?topic=watson-gs-logging-overview).
-   Die folgende Fehlercodes für die Methoden `/v1/synthesize` wurden geändert:
    -   Der Fehlercode 406 ("Not acceptable. Unsupported MIME type.") wurde entfernt.
    -   Der Fehlercode 415 ("Unsupported Media Type") wurde hinzugefügt.
    -   Der Fehlercode 503 ("Service Unavailable") wurde hinzugefügt.
-   Die folgenden Fehlercodes für die Methode `GET /v1/voices` wurden geändert:
    -   Der Fehlercode 406 ("Not acceptable. Unsupported MIME type.") wurde entfernt.
    -   Der Fehlercode 415 ("Unsupported Media Type") wurde hinzugefügt.
