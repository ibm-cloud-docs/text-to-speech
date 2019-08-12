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

# Informazioni
{: #about}

{{site.data.keyword.texttospeechdatafull}} for {{site.data.keyword.icp4dfull}} fornisce funzionalità di sintesi vocale per le tue applicazioni per convertire il testo scritto in audio con suono naturale. Il servizio ritrasmette i risultati al client con un ritardo minimo. Il servizio offre sia l'interfaccia [HTTP](/docs/services/text-to-speech-data?topic=text-to-speech-data-usingHTTP) che [WebSocket](/docs/services/text-to-speech-data?topic=text-to-speech-data-usingWebSocket).

Per informazioni sull'installazione e la configurazione di {{site.data.keyword.texttospeechshort}} for {{site.data.keyword.icp4dfull_notm}}, vedi [Installazione del servizio](/docs/services/text-to-speech-data?topic=text-to-speech-data-install).

{{site.data.keyword.texttospeechdatafull}} for {{site.data.keyword.icp4dfull}} si basa sul servizio {{site.data.keyword.texttospeechfull}} su {{site.data.keyword.cloud_notm}} pubblico. Per ulteriori informazioni sul servizio pubblico, vedi [Informazioni su {{site.data.keyword.texttospeechshort}}](https://{DomainName}/docs/services/text-to-speech?topic=text-to-speech-about#about){: external}.
{: note}

## Caratteristiche e funzioni

Il servizio {{site.data.keyword.texttospeechshort}} offre le seguenti caratteristiche e funzioni:

-   **Formati audio** - Produce l'audio in formato Ogg o WebM con il codec Opus o Vorbis, WAV, FLAC, MP3 (MPEG), l16 (PCM), mulaw o formato di base. Per ulteriori informazioni, vedi [Formati audio](/docs/services/text-to-speech-data?topic=text-to-speech-data-audioFormats).
-   **Voci** - Sintetizza il testo in audio in varie lingue, voci e dialetti. Per ulteriori informazioni, vedi [Lingue e voci](/docs/services/text-to-speech-data?topic=text-to-speech-data-voices).
-   **SSML** - Accetta il testo semplice o il testo contrassegnato con SSML (Speech Synthesis Markup Language) basato su XML. Per ulteriori informazioni, vedi [Utilizzo di SSML](/docs/services/text-to-speech-data?topic=text-to-speech-data-ssml).
-   **Temporizzazioni delle parole** - Con l'interfaccia WebSocket, supporta l'elemento SSML `<mark>` e le facoltative informazioni di temporizzazione delle parole per tutte le stringhe del testo di input. Le informazioni di temporizzazione sincronizzano il testo di input e l'audio risultante. Per ulteriori informazioni, vedi [Come ottenere le temporizzazioni delle parole](/docs/services/text-to-speech-data?topic=text-to-speech-data-timing).
-   **Personalizzazione** - Fornisce un'interfaccia di personalizzazione che puoi utilizzare per specificare il modo in cui il servizio pronuncia le parole inusuali presenti nel tuo input. Puoi definire le pronunce con il formato IPA (International Phonetic Alphabet) o {{site.data.keyword.IBM_notm}} SPR (Symbolic Phonetic Representation). Per ulteriori informazioni, vedi
      [Informazioni sulla personalizzazione](/docs/services/text-to-speech-data?topic=text-to-speech-data-customIntro).

## Supporto linguistico
{: #languages-index}

Il servizio supporta voci nelle seguenti lingue: portoghese brasiliano, inglese (dialetto britannico e americano), francese, tedesco, italiano, giapponese e spagnolo (dialetto castigliano, latino americano e nord americano).

Il servizio offre almeno una voce femminile per ogni lingua. Per alcune lingue il servizio offre più voci, incluse sia voci maschili che femminili. Ogni voce usa cadenza e intonazione appropriate per il suo dialetto.

Per ulteriori informazioni sulle voci disponibili per ogni lingua, vedi [Lingue e voci](/docs/services/text-to-speech-data?topic=text-to-speech-data-voices).

Una voce in giapponese è in fase di sviluppo e sarà disponibile a breve.
{: note}

## Casi di utilizzo
{: #usecases}

Il servizio è appropriato per applicazioni vocali e senza schermo, in cui l'audio è il metodo di output preferito:

-   Interfacce per disabili, come gli strumenti di assistenza per persone con disturbi della vista
-   Lettura ad alta voce dei messaggi di testo ed email per i conducenti
-   Narrazione di script video e voice over per video
-   Strumenti educativi basati sulla lettura
-   Soluzioni di domotica

## Prova il servizio

Per esempi del servizio {{site.data.keyword.texttospeechshort}} in azione, vedi

-   Una [demo rapida](https://text-to-speech-demo.ng.bluemix.net/){: external} del servizio {{site.data.keyword.texttospeechshort}} che accetta il testo e genera sintesi vocali con voci diverse. Dove supportato, offre espressività e trasformazione.
-   Applicazioni nei [Kit starter](http://www.ibm.com/watson/developercloud/starter-kits.html){: external} {{site.data.keyword.ibmwatson}} che mostrano il servizio {{site.data.keyword.texttospeechshort}}.
