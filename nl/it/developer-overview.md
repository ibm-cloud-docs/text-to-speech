---

copyright:
  years: 2019
lastupdated: "2019-07-06"

subcollection: text-to-speech-data

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

# Panoramica per gli sviluppatori
{: #overview}

Puoi accedere alle funzionalità di {{site.data.keyword.texttospeechdatafull}} for {{site.data.keyword.icp4dfull}} tramite un'API REST (Representational State Transfer ) HTTP o un'interfaccia WebSocket. Sono inoltre disponibili diversi SDK per semplificare lo sviluppo delle applicazioni in vari linguaggi di programmazione. Le seguenti sezioni forniscono una panoramica dello sviluppo delle applicazioni con il servizio.
{: shortdesc}

Esegui l'autenticazione con il servizio {{site.data.keyword.texttospeechshort}} passando un token di accesso con ogni richiesta. {{site.data.keyword.texttospeechshort}} for {{site.data.keyword.icp4dfull_notm}} è una soluzione cloud a più tenant. Le tue credenziali forniscono l'accesso solo ai tuoi dati ed essi sono isolati dagli altri utenti.

## Interfaccia HTTP
{: #overview-http}

Per sintetizzare il testo con l'API HTTP, chiama la versione `GET` o `POST` del metodo `/v1/synthesize` del servizio. Le due versioni del metodo offrono funzionalità generalmente equivalenti:

-   *Testo di input:* puoi passare il testo di input che deve essere sintetizzato in due modi diversi:
    -   Il metodo `GET /v1/synthesize` accetta il testo di input come parametro di query. La dimensione massima della richiesta è di 8 KB, che include il testo di input e l'URL e le intestazioni.
    -   Il metodo `POST /v1/synthesize` accetta il testo di input nel corpo della richiesta. La dimensione massima della richiesta è di 8 KB per l'URL e le intestazioni e di 5 KB per il testo di input inviato nel corpo della richiesta.

    Puoi passare al servizio il testo semplice o il testo annotato con il linguaggio SSML (Speech Synthesis Markup Language). SSML è un linguaggio di markup basato su XML che fornisce annotazioni di testo per le applicazioni di sintesi vocale, come il servizio {{site.data.keyword.texttospeechshort}}.

    Per ulteriori informazioni, vedi [Specifica del testo di input](/docs/services/text-to-speech-data?topic=text-to-speech-data-usingHTTP#input).
-   *Voci:* il servizio accetta il testo e produce l'audio in varie lingue, voci e dialetti. Il servizio offre almeno una voce femminile per ogni lingua. Per alcune lingue il servizio offre più voci, che possono includere voci maschili e femminili. Il servizio offre anche diversi dialetti come ad esempio inglese americano e britannico.

    Puoi utilizzare i metodi `GET /v1/voices` o `GET /v1/voices/{voice}` del servizio per saperne di più sulle voci supportate. Il servizio sintetizza il testo nella lingua della voce specificata. Assicurati di abbinare la voce al testo di input.

    Per ulteriori informazioni, vedi [Lingue e voci](/docs/services/text-to-speech-data?topic=text-to-speech-data-voices).
-   *Formati audio:* il servizio può produrre l'audio nei seguenti formati: formato Ogg o Web Media (WebM) con il codec Opus (predefinito) o Vorbis, formato MP3 (Motion Picture Experts Group o MPEG), WAV (Waveform Audio File Format), FLAC (Free Lossless Audio Codec), PCM (Pulse-Code Modulation) lineare a 16 bit, mu-law (u-law) a 8 bit o audio di base.

    Per ulteriori informazioni, vedi [Formati audio](/docs/services/text-to-speech-data?topic=text-to-speech-data-audioFormats).

## Interfaccia WebSocket
{: #overview-websocket}

Il servizio offre un'interfaccia WebSocket che puoi utilizzare per sintetizzare il testo. L'interfaccia fornisce una singola versione del metodo `/v1/synthesize` che accetta un massimo di 5 KB di testo di input. Specifica il testo da sintetizzare, la voce da utilizzare e il formato per l'audio. Puoi fornire il testo semplice o il testo annotato con il linguaggio SSML. Per ulteriori informazioni, vedi [L'interfaccia WebSocket](/docs/services/text-to-speech-data?topic=text-to-speech-data-usingWebSocket).

L'interfaccia WebSocket supporta l'uso dell'elemento SSML `<mark>` per identificare posizioni specifiche nell'audio. Puoi anche richiedere le informazioni di temporizzazione per tutte le parole del testo di input. Per ulteriori informazioni, vedi [Come ottenere le temporizzazioni delle parole](/docs/services/text-to-speech-data?topic=text-to-speech-data-timing).

## Interfaccia di personalizzazione
{: #overview-customization}

Il servizio include un'interfaccia di personalizzazione che puoi utilizzare per creare modelli vocali personalizzati da utilizzare durante la sintesi vocale. Un modello vocale personalizzato è un dizionario di parole e relative traduzioni per una lingua specifica. Ogni coppia di parola/traduzione in un modello indica al servizio come pronunciare la parola quando si presenta nel testo di input.

Puoi utilizzare i modelli vocali personalizzati per creare traduzioni specifiche dell'applicazione per le parole inusuali per le quali le regole di pronuncia regolare del servizio potrebbero fornire delle pronunce imperfette. Puoi definire la voce personalizzata per una coppia di parola/traduzione nella rappresentazione IPA (International Phonetic Alphabet) standard o nella rappresentazione {{site.data.keyword.IBM_notm}} SPR (Symbolic Phonetic Representation) proprietaria.

Ad esempio, la tua applicazione potrebbe incontrare regolarmente termini speciali con origini straniere, nomi personali o geografici o abbreviazioni e acronimi. Utilizzando la personalizzazione, puoi definire le traduzioni che indicano al servizio come vuoi che vengano pronunciati tali termini. Per ulteriori informazioni, vedi [Informazioni sulla personalizzazione](/docs/services/text-to-speech-data?topic=text-to-speech-data-customIntro).

L'interfaccia di personalizzazione è una release beta.
{: note}

## Supporto CORS
{: #cors}

Il servizio supporta CORS (Cross-Origin Resource Sharing). Utilizzando CORS, le pagine web possono richiedere le risorse direttamente da un dominio esterno. CORS aggira la politica di sicurezza della stessa origine, che altrimenti impedisce tali richieste. Poiché il servizio supporta CORS, una pagina web può comunicare direttamente con il servizio senza passare la richiesta attraverso il server web che ospita la pagina.

Ad esempio, una pagina web caricata da un server in {{site.data.keyword.cloud}} può chiamare direttamente l'API di personalizzazione, ignorando il server {{site.data.keyword.cloud_notm}}. Per ulteriori informazioni, vedi [enable-cors.org](https://enable-cors.org/){: external}.

## Utilizzo di SDK (Software Development Kit)
{: #sdks}

Gli SDK sono disponibili per il servizio {{site.data.keyword.texttospeechshort}} per semplificare lo sviluppo di applicazioni di riconoscimento vocale. Gli SDK {{site.data.keyword.ibmwatson}} sono disponibili per molti linguaggi di programmazione e piattaforme comuni.

-   Per un elenco completo di SDK e link agli SDK su GitHub, vedi [Utilizzo di SDK](/docs/services/watson?topic=watson-using-sdks).
-   Per informazioni dettagliate su tutti i metodi degli SDK Node, Java&trade;, Python, Ruby e Go per il servizio {{site.data.keyword.texttospeechshort}}, vedi il [Riferimento API](https://{DomainName}/apidocs/text-to-speech-data){: external}.
