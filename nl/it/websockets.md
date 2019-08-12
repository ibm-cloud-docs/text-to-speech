---

copyright:
  years: 2019
lastupdated: "2019-06-24"

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

# L'interfaccia WebSocket
{: #usingWebSocket}

Per sintetizzare il testo in voce utilizzando l'interfaccia WebSocket di {{site.data.keyword.texttospeechdatafull}} for {{site.data.keyword.icp4dfull}}, stabilisci innanzitutto una connessione con il servizio richiamandone il metodo `/v1/synthesize`. Poi invia il testo da sintetizzare al servizio come un messaggio di testo JSON tramite la connessione. Il servizio chiude automaticamente la connessione WebSocket quando termina l'elaborazione della richiesta.
{: shortdesc}

Il ciclo di richiesta e risposta della sintesi include i seguenti passi:

1.  [Apri una connessione](#WSopen).
1.  [Invia il testo di input](#WSsend).
1.  [Ricevi una risposta](#WSreceive).

L'interfaccia WebSocket accetta input identico e produce risultati identici come i metodi `GET` e `POST /v1/synthesize` dell'interfaccia HTTP. Tuttavia, l'interfaccia WebSocket supporta l'uso dell'elemento `<mark>` SSML per identificare la posizione dei contrassegni specificati dall'utente nell'audio. Può anche restituire le informazioni di temporizzazione per tutte le stringhe del testo di input. Per ulteriori informazioni, vedi [Come ottenere le temporizzazioni delle parole](/docs/services/text-to-speech-data?topic=text-to-speech-data-timing).

I frammenti di codice di esempio che seguono sono scritti in JavaScript e sono basati sull'API WebSocket HTML5. Per ulteriori informazioni sul protocollo WebSocket, vedi l'IETF (Internet Engineering Task Force) [Request for Comment (RFC) 6455](http://tools.ietf.org/html/rfc6455){: external}.
{: note}

## Apri una connessione
{: #WSopen}

{{site.data.keyword.texttospeechshort}} utilizza il protocollo WSS (WebSocket Secure) per rendere il metodo `/v1/synthesize` disponibile al seguente endpoint. Per ulteriori informazioni sui componenti dell'URL, vedi [Effettuare le richieste al servizio](/docs/services/text-to-speech-data?topic=text-to-speech-data-making-requests).

```
wss://{icp4d_cluster_host}{:port}/text-to-speech/{release}/instances/{instance_id}/api/v1/synthesize
```
{: codeblock}

Gli esempi nella documentazione fanno riferimento a questo endpoint come `{ws_url}`.
{: note}

Un client WebSocket richiama questo metodo con i seguenti parametri di query per stabilire una connessione autenticata con il servizio.

<table>
  <caption>Tabella 1. Parametri del metodo
    <code>/v1/synthesize</code></caption>
  <tr>
    <th style="text-align:left; width:23%">Parametro</th>
    <th style="text-align:center; width:12%">Tipo di dati</th>
    <th style="text-align:left">Descrizione</th>
  </tr>
  <tr>
    <td style="text-align:left"><code>access_token</code>
      <br/><em>Obbligatorio</em></td>
    <td style="text-align:center">Stringa</td>
    <td style="text-align:left">
      Passa un token di accesso valido per l'autenticazione con il servizio. Devi
      utilizzare il token di accesso prima che scada.
    </td>
  </tr>
  <tr>
    <td><code>voice</code><br/><em>Facoltativo</em></td>
    <td style="text-align:center">Stringa</td>
    <td>
      Specifica la voce con cui deve essere pronunciato il testo nell'audio.
      Ometti il parametro per utilizzare la voce predefinita, `en-US_MichaelV3Voice`.
      Per ulteriori informazioni, vedi
      [Lingue e voci](/docs/services/text-to-speech-data?topic=text-to-speech-data-voices).
    </td>
  </tr>
  <tr>
    <td><code>customization_id</code><br/><em>Facoltativo</em></td>
    <td style="text-align:center">Stringa</td>
    <td>
      Specifica il GUID (globally unique identifier) per un modello vocale
      personalizzato da utilizzare per la sintesi. Il funzionamento di un
      modello vocale personalizzato è garantito solo se corrisponde alla lingua
      della voce utilizzata per la sintesi. Se includi un ID
      di personalizzazione, devi effettuare la richiesta con le credenziali per l'istanza del servizio
      che gestisce il modello personalizzato. Ometti il parametro per utilizzare la voce specificata senza personalizzazioni. Per ulteriori informazioni, vedi
      [Informazioni sulla personalizzazione](/docs/services/text-to-speech-data?topic=text-to-speech-data-customIntro).
    </td>
  </tr>
  <tr>
    <td style="text-align:left"><code>x-watson-metadata</code>
      <br/><em>Facoltativo</em></td>
    <td style="text-align:center">Stringa</td>
    <td style="text-align:left">
      Associa un ID cliente ai dati che vengono passati tramite
      la connessione. Il parametro accetta l'argomento
      <code>customer_id={id}</code>, dove <code>id</code> è una stringa
      casuale o generica che deve essere associata ai dati. Devi
      codificare in URL l'argomento nel parametro, ad esempio,
      `customer_id%3dmy_ID`. Per impostazione predefinita,
      nessun ID cliente viene associato ai dati. Per ulteriori informazioni, vedi [Sicurezza delle informazioni](/docs/services/text-to-speech-data?topic=text-to-speech-data-information-security).
    </td>
  </tr>
</table>

Il seguente frammento di codice JavaScript apre una connessione con il servizio. La chiamata al metodo `/v1/synthesize` passa i parametri di query `access_token` e `voice`, questi ultimi per indirizzare il servizio a utilizzare la voce in inglese americano Allison. Una volta stabilita la connessione, i listener di eventi (`onOpen`, `onClose` e così via) vengono definiti per rispondere agli eventi dal servizio.

```javascript
var my_access_token = '{token}';
var wsURI = '{ws_url}/v1/synthesize'
  + '?access_token=' + my_access_token
  + '&voice=en-US_AllisonV3Voice';
var websocket = new WebSocket(wsURI);

websocket.onopen = function(evt) { onOpen(evt) };
websocket.onclose = function(evt) { onClose(evt) };
websocket.onmessage = function(evt) { onMessage(evt) };
websocket.onerror = function(evt) { onError(evt) };
```
{: codeblock}

## Invia il testo di input
{: #WSsend}

Per sintetizzare il testo, il client passa un messaggio di testo JSON semplice al servizio con i seguenti parametri.

<table>
  <caption>Tabella 2. Parametri del messaggio di testo JSON</caption>
  <tr>
    <th style="text-align:left; width:23%">Parametro</th>
    <th style="text-align:center; width:12%">Tipo di dati</th>
    <th style="text-align:left">Descrizione</th>
  </tr>
  <tr>
    <td><code>text</code><br/><em>Obbligatorio</em></td>
    <td style="text-align:center">Stringa</td>
    <td>
      Fornisce il testo da sintetizzare. Il client può passare il testo
      semplice o il testo annotato con SSML (Speech Synthesis
      Markup Language). Il client può passare massimo 5 KB di testo
      di input con la richiesta. Il limite include qualsiasi SSML
      tu specifichi. Per ulteriori informazioni, vedi
      [Specifica del testo di input](/docs/services/text-to-speech-data?topic=text-to-speech-data-usingHTTP#input)
      e le sezioni che seguono.<br/><br/>
      L'input SSML può includere anche l'elemento <code>&lt;mark&gt;</code>.
      Per ulteriori informazioni, vedi [Specifica di un contrassegno SSML](/docs/services/text-to-speech-data?topic=text-to-speech-data-timing#mark).
    </td>
  </tr>
  <tr>
    <td><code>accept</code><br/><em>Obbligatorio</em></td>
    <td style="text-align:center">Stringa</td>
    <td>
      Specifica il formato richiesto (tipo MIME) dell'audio. Utilizza
      `*/*` per richiedere il formato audio predefinito,
      <code>audio/ogg;codecs=opus</code>. Per ulteriori informazioni, vedi [Formati audio](/docs/services/text-to-speech-data?topic=text-to-speech-data-audioFormats).
    </td>
  </tr>
  <tr>
    <td><code>timings</code><br/><em>Facoltativo</em></td>
    <td style="text-align:center">String[ ]</td>
    <td>
      Specifica che il servizio deve restituire le informazioni di temporizzazione delle
      parole per tutte le stringhe del testo di input. Il servizio restituisce il tempo di
      inizio e di fine di ogni token nell'input. Specifica <code>words</code> come unico
      elemento dell'array per richiedere la temporizzazione delle parole. Specifica un array
      vuoto oppure ometti il parametro per non ricevere alcuna temporizzazione delle parole.
      Per ulteriori informazioni, vedi [Come ottenere le temporizzazioni delle parole](/docs/services/text-to-speech-data?topic=text-to-speech-data-timing#timing). <em>Non supportato per il testo di input in giapponese.</em>
    </td>
  </tr>
</table>

Il seguente frammento di codice JavaScript passa un semplice messaggio "Hello world" come testo di input e richiede il formato predefinito per l'audio. Le chiamate sono incluse nella funzione `onOpen` definita per il client per assicurare che vengano inviate solo una volta stabilita la connessione.

```javascript
function onOpen(evt) {
  var message = {
    text: 'Hello world',
    accept: '*/*'
  };
  websocket.send(JSON.stringify(message));
}
```
{: codeblock}

Il servizio risponde a questo messaggio inviando un messaggio di testo che conferma il formato della risposta audio. La seguente risposta conferma il formato audio predefinito.

```javascript
{
  'binary_streams': [
    {
      content_type: 'audio/ogg;codecs=opus'
    }
  ]
}
```
{: codeblock}

## Ricevi una risposta
{: #WSreceive}

Una volta confermato il formato audio, il servizio invia l'audio sintetizzato come un flusso binario di dati nel formato indicato. Il servizio invia le informazioni di temporizzazione come uno o più messaggi di testo se

-   Il testo di input include uno o più elementi `<mark>` SSML.
-   Specifichi il parametro `timings` con la richiesta.

Il servizio invia anche i messaggi di testo con avvertenze o errori. Quando termina di sintetizzare il testo di input, il servizio chiude automaticamente la connessione WebSocket.

Il client deve accodare le risposte binarie provenienti dal servizio ai risultati audio ricevuti tramite la connessione. Può gestire i messaggi di testo rispondendo ad essi, visualizzandoli o acquisendoli per essere utilizzati dall'applicazione (ad esempio, se contengono posizioni di contrassegno). L'esempio semplice di una funzione `onMessage` riportato di seguito, accoda il testo e i messaggi binari ricevuti dal servizio alla variabile appropriata in base al loro tipo. Quando la funzione `onClose()` viene eseguita, è stato ricevuto l'intero flusso audio.

```javascript
var messages;
var audioStream;

function onMessage(evt) {
  if (typeof evt.data === string) {
    messages += evt.data;
  } else {
    console.log('Received ' + evt.data.size() + ' binary bytes');
    audioStream += evt.data;
  }
}

function onClose(evt) {
  // The audio stream is complete.
}
```
{: codeblock}

## Codici di ritorno WebSocket
{: #returnCodes}

Il servizio può inviare i seguenti codici di ritorno al client tramite la connessione WebSocket:

-   `1000` indica la normale chiusura della connessione, il che significa che lo scopo per il quale la connessione è stata stabilita è stato soddisfatto.
-   `1002` indica che il servizio sta chiudendo la connessione a causa di un errore di protocollo.
-   `1006` indica che la connessione è stata chiusa in modo anomalo.
-   `1009` indica che la dimensione del frame ha superato il limite di 4 MB.
-   `1011` indica che il servizio sta terminando la connessione perché ha riscontrato una condizione imprevista che impedisce di soddisfare la richiesta, ad esempio un argomento non valido. Il codice di ritorno indica anche che il testo di input è troppo lungo.

Se il socket si chiude con un errore, il servizio invia al client un messaggio informativo del tipo `{"error": "Specific error message"}` prima di chiudersi. Il servizio invia anche messaggi di avvertenza non irreversibile per parametri sconosciuti.

## Messaggi di errore e di avvertenza di esempio
{: #returnErrors}

I seguenti esempi mostrano le risposte di errore. Includono un messaggio di testo JSON e un messaggio formattato dal metodo di callback `onClose` del client. I messaggi formattati iniziano con un `true` booleano perché la connessione è chiusa. Includono anche il codice di errore WebSocket che ha causato la chiusura.

-   Questo esempio mostra i messaggi di errore per un argomento non valido per il parametro `accept`:

    ```javascript
    {
      "error": "Unsupported mimetype. Supported mimetypes are: ['application/json', 'audio/flac', ...]"
    }
    (True, 1011, u'see the previous message for the error details.')
    ```
    {: codeblock}

-   Questo esempio mostra i messaggi di errore per un parametro `text` mancante:

    ```javascript
    {
      "error": "Required parameter \"text\" is missing."
    }
    (True, 1011, u'see the previous message for the error details.')
    ```
    {: codeblock}

Il seguente esempio mostra una risposta di avvertenza, in questo caso per un parametro sconosciuto denominato `invalid-parameter`. Non include il secondo messaggio perché la connessione non viene chiusa dall'avvertenza.

```javascript
{
  "warnings": "Unknown arguments: invalid-parameter."
}
```
{: codeblock}

Per ulteriori informazioni sui codici di ritorno WebSocket, vedi l'IETF (Internet Engineering Task Force) [Request for Comments (RFC) 6455](http://tools.ietf.org/html/rfc6455){: external}.
