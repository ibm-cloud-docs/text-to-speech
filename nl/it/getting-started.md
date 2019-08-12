---

copyright:
  years: 2019
lastupdated: "2019-07-30"

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
{:go: .ph data-hd-programlang='go'}
{:python: .ph data-hd-programlang='python'}
{:swift: .ph data-hd-programlang='swift'}
{:download: .download}
{:url: data-credential-placeholder='url'}
{:hide-dashboard: .hide-dashboard}

# Esercitazione introduttiva
{: #gettingStarted}

{{site.data.keyword.texttospeechdatafull}} for {{site.data.keyword.icp4dfull}} converte il testo scritto in audio con suono naturale per fornire funzionalità di sintesi vocale per le applicazioni. Questa esercitazione basata su curl può aiutarti a iniziare a utilizzare subito il servizio . Gli esempi ti mostrano come chiamare i metodi `POST` e `GET /v1/synthesize` del servizio per richiedere un flusso audio.
{: shortdesc}

## Prima di cominciare
{: #before-you-begin}

Per utilizzare {{site.data.keyword.texttospeechshort}} for {{site.data.keyword.icp4dfull_notm}}, devi prima completare la seguente procedura:

1.  Esegui il provisioning di un'istanza di {{site.data.keyword.texttospeechshort}} for {{site.data.keyword.icp4dfull_notm}}. Per ulteriori informazioni sul provisioning, vedi [Installazione del servizio](/docs/services/text-to-speech-data?topic=text-to-speech-data-install).
1.  Dal menu del client web {{site.data.keyword.icp4dfull_notm}}, scegli **My Instances**.
1.  Fai clic sull'istanza di {{site.data.keyword.texttospeechshort}} per aprire la pagina della panoramica. Copia i valori delle credenziali `{token}` e `{URL}`.

### Utilizzo degli esempi curl
{: #getting-started-curl}

Questa esercitazione utilizza il comando `curl` per richiamare i metodi dell'interfaccia HTTP del servizio. Assicurati che il comando `curl` sia installato sul tuo sistema.

1.  Per verificare se `curl` è installato, immetti il seguente comando sulla riga di comando. Se l'output elenca la versione `curl` che supporta SSL (Secure Sockets Layer), hai le impostazioni necessarie per l'esercitazione.

    ```bash
    curl -V
    ```
    {: pre}

1.  Se necessario, installa la versione di `curl` con SSL abilitato per il tuo sistema operativo da [curl.haxx.se](https://curl.haxx.se/){: external}.

Ometti le parentesi graffe dagli esempi. Indicano dei valori di variabile.
{: tip}

## Passo 1: sintetizza il testo in inglese americano
{: #synthesizeEnglish}

I seguenti comandi utilizzano il metodo `POST /v1/synthesize` per sintetizzare l'input in inglese americano in file audio in due formati diversi. Entrambe le richieste utilizzano la voce in inglese americano predefinita, `en-US_MichaelVoice`.

1.  Immetti il seguente comando per sintetizzare la stringa "hello world" e produrre un file WAV denominato `hello_world.wav`.
    -   Sostituisci `{token}` con il token di accesso della tua istanza del servizio.
    -   Sostituisci `{url}` con l'URL della tua istanza del servizio.

    *Gli utenti Windows,* devono sostituire la barra rovesciata (``\`) alla fine di ogni riga con un accento circonflesso (``^`). Assicurati che non ci siano spazi finali.
    {: tip}

    ```bash
    curl -X POST \
    --header "Authorization: Bearer {token}" \
    --header "Content-Type: application/json" \
    --header "Accept: audio/wav" \
    --data "{\"text\":\"hello world\"}" \
    --output hello_world.wav \
    "{url}/v1/synthesize"
    ```
    {: pre}

1.  Immetti il seguente comando per sintetizzare lo stesso testo ma produrre un file Ogg (il formato predefinito) denominato `hello_world.ogg`.
    -   Sostituisci `{token}` con il token di accesso della tua istanza del servizio.
    -   Sostituisci `{url}` con l'URL della tua istanza del servizio.

    ```bash
    curl -X POST \
    --header "Authorization: Bearer {token}" \
    --header "Content-Type: application/json" \
    --data "{\"text\":\"hello world\"}" \
    --output hello_world.ogg \
    "{url}/v1/synthesize"
    ```
    {: pre}

Puoi utilizzare un browser o altri strumenti per riprodurre i file audio prodotti dagli esempi. Per ulteriori informazioni, vedi [Riproduzione di un file audio](/docs/services/text-to-speech-data?topic=text-to-speech-data-audioFormats#formatsPlay).
{: note}

## Passo 2: sintetizza il testo in spagnolo
{: #synthesizeSpanish}

Il seguente comando utilizza il metodo `GET /v1/synthesize` per sintetizzare l'input in spagnolo in un file audio.

1.  Immetti il seguente comando per sintetizzare la stringa "hola mundo" e produrre un file WAV denominato `hola_mundo.wav`. Il testo di input è codificato in URL. Il metodo include i parametri di query `accept` per specificare il formato audio e `voice` per specificare una voce in spagnolo, `es-ES_EnriqueV3Voice`.
    -   Sostituisci `{token}` con il token di accesso della tua istanza del servizio.
    -   Sostituisci `{url}` con l'URL della tua istanza del servizio.

    ```bash
    curl -X POST \
    --header "Authorization: Bearer {token}" \
    --output hola_mundo.wav \
    "{url}/v1/synthesize?accept=audio%2Fwav&text=hola%20mundo&voice=es-ES_EnriqueV3Voice"
    ```
    {: pre}

## Passi successivi

-   Ottieni ulteriori informazioni sull'interfaccia HTTP del servizio in [L'interfaccia HTTP](/docs/services/text-to-speech-data?topic=text-to-speech-data-usingHTTP).
-   Ottieni ulteriori informazioni sull'interfaccia WebSocket del servizio in [L'interfaccia WebSocket](/docs/services/text-to-speech-data?topic=text-to-speech-data-usingWebSocket).
-   Trova le informazioni dettagliate su tutti i metodi delle interfacce del servizio nel [Riferimento API](https://{DomainName}/apidocs/text-to-speech-data){: external}.
