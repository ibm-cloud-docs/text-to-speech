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

# Informazioni
{: #about}

> ** Aggiornamento del servizio:** *il servizio {{site.data.keyword.texttospeechshort}} è stato aggiornato il 24 marzo 2019. Adesso, il servizio offre versioni DNN (Deep Neural Network) delle sue voci in tedesco e tutte le voci basate su DNN supportano gli attributi `pitch` e `rate` dell'elemento SSML `<prosody>`. Per ulteriori informazioni, vedi l'[aggiornamento del servizio del 24 marzo 2019](/docs/services/text-to-speech/release-notes.html#March2019c) nelle note sulla release*.

Il servizio {{site.data.keyword.texttospeechfull}} fornisce un'API (Application Programming Interface) che utilizza le funzionalità di sintesi vocale di {{site.data.keyword.IBM_notm}} per convertire il testo scritto in audio con suono naturale. Il servizio ritrasmette i risultati al client con un ritardo minimo. Il servizio offre sia l'interfaccia [HTTP](/docs/services/text-to-speech/http.html) che [WebSocket](/docs/services/text-to-speech/websockets.html).

## Caratteristiche e funzioni

Il servizio {{site.data.keyword.texttospeechshort}} offre le seguenti caratteristiche e funzioni:

-   **Formati audio** - Produce l'audio in formato Ogg o WebM con il codec Opus o Vorbis, WAV, FLAC, MP3 (MPEG), l16 (PCM), mulaw o formato di base. Per ulteriori informazioni, vedi [Formati audio](/docs/services/text-to-speech/audio-formats.html).
-   **Voci** - Sintetizza il testo in audio in varie lingue, voci e dialetti. Il servizio offre versioni basate su DNN di alcune voci. Per ulteriori informazioni, vedi [Lingue e voci](/docs/services/text-to-speech/voices.html).
-   **SSML** - Accetta il testo semplice o il testo contrassegnato con SSML (Speech Synthesis Markup Language) basato su XML. Per ulteriori informazioni, vedi [Utilizzo di SSML](/docs/services/text-to-speech/SSML.html).
-   **Espressività** - Estende SSML con un elemento di espressività che puoi utilizzare per indicare uno stile di pronuncia come *Buone notizie*, *Scuse* o *Incertezza*. Disponibile solo per la voce in inglese americano Allison che non è basata su DNN. Per ulteriori informazioni, vedi [SSML di espressività](/docs/services/text-to-speech/SSML-expressive.html).
-   **Trasformazione della voce** - Estende SSML aggiungendo un elemento di trasformazione della voce. Puoi utilizzare questo elemento per espandere la gamma di possibili voci controllando aspetti come tono, velocità e timbro. Offre anche due voci virtuali integrate, *Young* e *Soft*. Disponibile solo per le voci in inglese americano che non sono basate su DNN. Per ulteriori informazioni, vedi [SSML per la trasformazione della voce](/docs/services/text-to-speech/SSML-transformation.html).
-   **Temporizzazioni delle parole** - Con l'interfaccia WebSocket, supporta l'elemento SSML `<mark>` e le facoltative informazioni di temporizzazione delle parole per tutte le stringhe del testo di input. Le informazioni di temporizzazione sincronizzano il testo di input e l'audio risultante. Per ulteriori informazioni, vedi [Come ottenere le temporizzazioni delle parole](/docs/services/text-to-speech/word-timing.html).
-   **Personalizzazione** - Fornisce un'interfaccia di personalizzazione che puoi utilizzare per specificare il modo in cui il servizio pronuncia le parole inusuali presenti nel tuo input. Puoi definire le pronunce con il formato IPA (International Phonetic Alphabet) o {{site.data.keyword.IBM_notm}} SPR (Symbolic Phonetic Representation). Per ulteriori informazioni, vedi [Informazioni sulla personalizzazione](/docs/services/text-to-speech/custom-intro.html).

Per ulteriori informazioni sui piani dei prezzi per il servizio, vedi il servizio {{site.data.keyword.texttospeechshort}} nel [catalogo {{site.data.keyword.cloud_notm}} ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://{DomainName}/catalog/services/text-to-speech){: new_window}.

## Supporto linguistico
{: #languages-index}

Il servizio supporta voci nelle seguenti lingue: portoghese brasiliano, inglese (dialetto britannico e americano), francese, tedesco, italiano, giapponese e spagnolo (dialetto castigliano, latino americano e nord americano). Il servizio offre almeno una voce maschile o femminile, a volte entrambe, per ciascuna lingua. Ogni voce usa cadenza e intonazione appropriate per il suo dialetto. Per ulteriori informazioni sulle voci disponibili per ogni lingua, vedi [Lingue e voci](/docs/services/text-to-speech/voices.html).

## Casi di utilizzo
{: #usecases}

Il servizio è appropriato per applicazioni vocali e senza schermo, in cui l'audio è il metodo di output preferito:

-   Interfacce per disabili, come gli strumenti di assistenza per persone con disturbi della vista
-   Lettura ad alta voce dei messaggi di testo ed email per i conducenti
-   Narrazione di script video e voice over per video
-   Strumenti educativi basati sulla lettura
-   Soluzioni di domotica

## Prova il servizio

Per esempi del servizio in azione, vedi

-   Una [demo rapida ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://text-to-speech-demo.ng.bluemix.net/){: new_window} del servizio {{site.data.keyword.texttospeechshort}} che accetta il testo e genera sintesi vocali con voci diverse. Dove supportato, offre espressività e trasformazione.
-   Applicazioni nei [Kit starter ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](http://www.ibm.com/watson/developercloud/starter-kits.html){: new_window} {{site.data.keyword.ibmwatson}} che mostrano il servizio {{site.data.keyword.texttospeechshort}}.
