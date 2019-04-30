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

# Esercitazione introduttiva
{: #gettingStarted}

Il servizio {{site.data.keyword.texttospeechfull}} converte il testo scritto in audio con suono naturale per fornire funzionalità di sintesi vocale per le applicazioni. Questa esercitazione basata su curl può aiutarti a iniziare a utilizzare subito il servizio . Gli esempi ti mostrano come chiamare i metodi `POST` e `GET /v1/synthesize` del servizio per richiedere un flusso audio.
{: shortdesc}

L'esercitazione utilizza le chiavi API di {{site.data.keyword.cloud}} IAM (Identity and Access Management) per l'autenticazione. Le istanze del servizio meno recenti potrebbero continuare a utilizzare `{username}` e `{password}` delle loro credenziali esistenti del servizio Cloud Foundry per eseguire l'autenticazione. Esegui l'autenticazione utilizzando l'approccio corretto per la tua istanza del servizio. Per ulteriori informazioni sull'utilizzo dell'autenticazione IAM da parte del servizio, vedi l'[aggiornamento del servizio del 30 ottobre 2018](/docs/services/text-to-speech/release-notes.html#October2018) nelle note sulla release.
{: important}

## Prima di cominciare
{: #before-you-begin}

- {: hide-dashboard}  Crea un'istanza del servizio
    1.  {: hide-dashboard}Vai alla pagina [{{site.data.keyword.texttospeechshort}} ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://{DomainName}/catalog/services/text-to-speech){: new_window} nel catalogo {{site.data.keyword.cloud_notm}}.
    1.  {: hide-dashboard} Registrati per un account {{site.data.keyword.cloud_notm}} gratuito o accedi.
    1.  {: hide-dashboard} Fai clic su **Crea**.
-   Copia le credenziali per eseguire l'autenticazione presso la tua istanza del servizio:
    1.  {: hide-dashboard} Dal [dashboard {{site.data.keyword.cloud_notm}} ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://{DomainName}/dashboard/apps){: new_window}, fai clic sulla tua istanza del servizio {{site.data.keyword.texttospeechshort}} per passare alla pagina del dashboard del servizio {{site.data.keyword.texttospeechshort}}.
    1.  Nella pagina **Gestisci**, fai clic su **Mostra** per visualizzare le tue credenziali.
    1.  Copia i valori `API Key` e `URL`.
-   Assicurati di avere il comando `curl`.
    -   Gli esempi utilizzano il comando `curl` per chiamare i metodi dell'interfaccia HTTP. Installa la versione per il tuo sistema operativo da [curl.haxx.se ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://curl.haxx.se/){: new_window}. Installa la versione che supporta il protocollo SSL (Secure Sockets Layer). Assicurati di includere il file binario installato nella tua variabile di ambiente `PATH`.

Quando immetti un comando, sostituisci `{apikey}` e `{url}` con la tua chiave API e il tuo URL effettivi. Ometti dal comando le parentesi graffe, che indicano un valore di variabile. Un valore effettivo è simile al seguente esempio:
{: hide-dashboard}

```bash
curl -X POST -u "apikey:L_HALhLVIksh1b73l97LSs6R_3gLo4xkujAaxm7i-b9x"
. . .
"https://stream.watsonplatform.net/text-to-speech/api/v1/synthesize"
```
{:pre}
{: hide-dashboard}

Puoi utilizzare un browser o altri strumenti per riprodurre i file audio prodotti dagli esempi in questa esercitazione. Per ulteriori informazioni, vedi [Riproduzione di un file audio](/docs/services/text-to-speech/audio-formats.html#formatsPlay).
{: note}

## Passo 1: sintetizza il testo in inglese americano
{: #synthesizeEnglish}

I seguenti comandi utilizzano il metodo `POST /v1/synthesize` per sintetizzare l'input in inglese americano in file audio in due formati diversi. Entrambe le richieste utilizzano la voce in inglese americano predefinita, `en-US_MichaelVoice`.

1.  Immetti il seguente comando per sintetizzare la stringa "hello world" e produrre un file WAV denominato `hello_world.wav`.
    -   {: hide-dashboard} Sostituisci `{apikey}` e `{url}` con la tua chiave API e il tuo URL.

    ```bash
    curl -X POST -u "apikey:{apikey}"{: apikey} \
    --header "Content-Type: application/json" \
    --header "Accept: audio/wav" \
    --data "{\"text\":\"hello world\"}" \
    --output hello_world.wav \
    "{url}/v1/synthesize"{: url}
    ```
    {: pre}

1.  Immetti il seguente comando per sintetizzare lo stesso testo ma produrre un file Ogg (il formato predefinito) denominato `hello_world.ogg`.
    -   {: hide-dashboard} Sostituisci `{apikey}` e `{url}` con la tua chiave API e il tuo URL.

    ```bash
    curl -X POST -u "apikey:{apikey}"{: apikey} \
    --header "Content-Type: application/json" \
    --data "{\"text\":\"hello world\"}" \
    --output hello_world.ogg \
    "{url}/v1/synthesize"{: url}
    ```
    {: pre}

## Passo 2: sintetizza il testo in spagnolo
{: #synthesizeSpanish}

Il seguente comando utilizza il metodo `GET /v1/synthesize` per sintetizzare l'input in spagnolo in un file audio.

1.  Immetti il seguente comando per sintetizzare la stringa "hola mundo" e produrre un file WAV denominato `hola_mundo.wav`. Il testo di input è codificato in URL. Il metodo include i parametri di query `accept` per specificare il formato audio e `voice` per specificare una voce in spagnolo, `es-ES_EnriqueVoice`.
    -   {: hide-dashboard} Sostituisci `{apikey}` e `{url}` con la tua chiave API e il tuo URL.

    ```bash
    curl -X GET -u "apikey:{apikey}"{: apikey} \
    --output hola_mundo.wav \
    "{url}/v1/synthesize?accept=audio%2Fwav&text=hola%20mundo&voice=es-ES_EnriqueVoice"{: url}
    ```
    {: pre}

## Passi successivi

-   Ottieni ulteriori informazioni sull'interfaccia HTTP del servizio in [L'interfaccia HTTP](/docs/services/text-to-speech/http.html).
-   Ottieni ulteriori informazioni sull'interfaccia WebSocket del servizio in [L'interfaccia WebSocket](/docs/services/text-to-speech/websockets.html).
-   Ottieni informazioni dettagliate sui metodi dell'interfaccia del servizio nel [Riferimento API ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://{DomainName}/apidocs/text-to-speech){: new_window}.
