---

copyright:
  years: 2019
lastupdated: "2019-06-04"

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

# Come ottenere le temporizzazioni delle parole
{: #timing}

L'interfaccia WebSocket fornisce la stessa funzionalità dei metodi `GET` e `POST /v1/synthesize` HTTP. Puoi utilizzare anche l'interfaccia WebSocket per ottenere le informazioni di temporizzazione per posizioni specifiche o per tutte le parole dell'input:
{: shortdesc}

-   Includi l'elemento `<mark>` SSML nel testo di input per identificare il tempo in cui si presenta il contrassegno nell'audio.
-   Specifica il parametro `timings` di un messaggio di testo JSON per ottenere le informazioni di temporizzazione per tutte le stringhe del testo di input.

Le informazioni di temporizzazione sono utili per sincronizzare l'audio e il testo di input. Ad esempio, puoi coordinare i gesti di un robot con il contenuto del discorso sintetizzato.

Il parametro `timings` non è supportato per il testo di input in giapponese.
{: note}

## In che modo il servizio restituisce le temporizzazioni delle parole
{: #timingHow}

Per restituire le informazioni di temporizzazione delle parole o di un contrassegno, il servizio multiplexa flussi di testo e binari indipendenti per costruire la tua risposta:

-   Per ogni elemento `<mark`>, il servizio restituisce un messaggio di testo JSON. Ogni messaggio indica il tempo esatto, dall'inizio dell'audio sintetizzato, in cui viene utilizzato il contrassegno.
-   Per le temporizzazioni delle parole per tutte le stringhe, il servizio restituisce uno o più messaggi di testo JSON. Ogni messaggio contiene un array di parole e i tempi di inizio e di fine dall'inizio dell'audio sintetizzato.

I flussi di testo e binari che il servizio invia sono indipendenti. Quindi il servizio ha poco controllo sul numero di blocchi audio che consegna e su quando l'utente riceve i messaggi audio e di testo. Ad esempio, se l'audio viene sintetizzato più velocemente di quando viene compresso, tutti i messaggi di testo potrebbero arrivare prima di quelli audio.

In termini pratici, il servizio può inviare un numero arbitrario di blocchi audio, inclusi più blocchi audio prima e dopo ciascun messaggio di testo. È anche possibile che un singolo blocco binario contenga i dati audio che precedono e seguono le informazioni di temporizzazione per un contrassegno o una parola.

Tuttavia, il messaggio di testo che contiene le informazioni di temporizzazione arriva sempre prima del blocco binario che contiene l'audio corrispondente. Inoltre, i messaggi audio arrivano sempre in ordine, quindi puoi creare una sintesi audio accurata del testo proveniente dai risultati binari.

## Specifica di un contrassegno SSML
{: #mark}

L'elemento `<mark>` SSML facoltativo è una tag vuota che inserisce un contrassegno nel testo da sintetizzare. Il client viene informato quando tutto il testo che precede l'elemento `<mark>` è stato sintetizzato.

L'elemento accetta un singolo attributo `name` che specifica una stringa che identifica in modo univoco il contrassegno. Il nome deve iniziare con un carattere alfanumerico. Il servizio restituisce il nome insieme al tempo in cui si presenta il contrassegno dall'inizio dell'audio sintetizzato. Puoi includere qualsiasi numero di contrassegni nel testo di input.

Il seguente frammento di codice JavaScript include un'istanza dell'elemento `<mark>` con il nome `here`:

```javascript
function onOpen(evt) {
  var message = {
    text: 'Hello <mark name="here"/> world',
    accept: '*/*'
  };
  websocket.send(JSON.stringify(message));
}
```
{: codeblock}

Quando finisce di sintetizzare il testo che precede il contrassegno, il servizio invia un messaggio di testo che identifica il nome del contrassegno e il tempo, in secondi, in cui si presenta il contrassegno nell'audio:

```javascript
{
  "marks": [
    ["here", 0.5019387755102041]
  ]
}
```
{: codeblock}

Il messaggio di testo che contiene le informazioni di temporizzazione arriva sempre prima del blocco audio che contiene la posizione del contrassegno.

## Richiesta delle temporizzazioni delle parole per tutte le parole
{: #timingRequest}

Il parametro `timings` facoltativo dell'oggetto JSON che passi al servizio per una richiesta restituisce le informazioni di temporizzazione per tutte le stringhe del testo di input. Questa comodità elimina la necessità di specificare l'elemento `<mark>` SSML per ogni parola dell'input. Passa un array che include la stringa `words` per richiedere le temporizzazioni delle parole. Passa un array vuoto oppure ometti il parametro per non ricevere alcuna informazione di temporizzazione.

Il servizio restituisce le temporizzazioni delle parole tramite la connessione WebSocket nello stesso modo in cui restituisce le informazioni di temporizzazione per i singoli elementi `<mark>`. Restituisce uno o più messaggi di testo JSON. Ogni messaggio contiene un array di parole e i tempi di inizio e di fine, in secondi, dall'inizio dell'audio sintetizzato. Ad esempio, il seguente esempio richiede le informazioni di temporizzazione delle parole:

```javascript
function onOpen(evt) {
  var message = {
    text: 'I have a pet bird.',
    accept: '*/*',
    timings: ['words']
  };
  websocket.send(JSON.stringify(message));
}
```
{: codeblock}

In risposta, il servizio può restituire i seguenti messaggi di testo:

```javascript
{
  "words": [
    ["I", [0.0690258394023930, 0.1655782733012873]]
    ["have", [0.1655789302434486, 0.3722901056092351]]
    ["a", [0.3722906798320199, 0.4012192331086645]]
  ]
}
{
  "words": [
    ["pet", [0.4012195492838347, 0.5798213856109801]]
    ["bird.", [0.5798218710823425, 0.7440360383928273]]
  ]
}
```
{: codeblock}

La risposta è solo un esempio. Il servizio può restituire uno o più messaggi di testo con le informazioni di temporizzazione per l'input. Inoltre, i messaggi possono essere intervallati con risposte che contengono i blocchi binari di audio. Tuttavia, il testo del messaggio che contiene le informazioni di temporizzazione per una parola arriva sempre prima del blocco audio che contiene tale parola.

### Temporizzazioni per il testo semplice
{: #timingText}

Il processo di sintesi del servizio comporta una fase di normalizzazione del testo che specifica numeri, date, ore, importi monetari, acronimi e abbreviazioni. I risultati corrispondono a come vengono pronunciate tali stringhe. Ad esempio, la stringa *$200* viene pronunciata come composta da tre parole: *two*, *hundred* e *dollars*. Poiché le informazioni di temporizzazione delle parole vengono utilizzate per sincronizzare l'audio con il testo di input, il servizio restituisce le informazioni di temporizzazione che corrispondono all'ortografia denormalizzata dell'input.

Ad esempio, considera il seguente testo di input:

```
The coldest recorded temperature is -89.2 degrees Celsius in Antarctica on July 21, 1983!
```
{: codeblock}

Il servizio restituisce le temporizzazioni audio per le seguenti stringhe:

"*The*", "*coldest*", "*recorded*", "*temperature*", "*is*", "*-89.2*", "*degrees*", "*Celsius*", "*in*", "*Antarctica*", "*on*", "*July*", "*21,*", "*1983!*"

Sebbene "*-89.2*" venga pronunciato nell'audio come cinque parole separate (*minus*, *eighty*, *nine*, *point*, *two*), il messaggio di testo fornisce le informazioni di temporizzazione per la stringa come una singola unità con il tempo di inizio *minus* e il tempo di fine *two*.

Come nell'esempio precedente, le stringhe denormalizzate possono contenere anche la punteggiatura. Il servizio include la punteggiatura che precede o segue una parola nel messaggio di testo restituito con le temporizzazioni. Ad esempio, le stringhe "*21,*" e "*1983!*" includono la punteggiatura che il servizio restituisce nel suo messaggio di testo. Sebbene la punteggiatura generi un'assenza di suono, la temporizzazione dell'audio per la parola *non* include tale assenza.

Ad esempio, considera il testo di input che contiene la seguente frase condizionale:

```
If it is sunny, I will go to the beach.
```
{: codeblock}

Il servizio restituisce le informazioni di temporizzazione per tutte le stringhe dell'input, inclusi "*sunny,*" e "*beach.*", che terminano entrambi con una punteggiatura che genera un'assenza di suono. Ma le informazioni di temporizzazione per "*sunny,*" non includono l'assenza di suono generata da una virgola e le informazioni di temporizzazione per "*beach.*" non includono l'assenza di suono prevista per il punto. Le informazioni riflettono solo la temporizzazione delle stringhe pronunciate.

### Temporizzazioni per il testo SSML
{: #timingSSML}

Quando il servizio sintetizza il testo semplice, restituisce tutti i caratteri di input ad eccezione degli spazi vuoti come parte delle stringhe nella sua risposta di temporizzazione delle parole. Ciò non si verifica con SSML, in quanto alcuni elementi SSML non generano audio. L'elenco riportato di seguito riepiloga gli elementi SSML che possono influire sulle informazioni di temporizzazione delle parole:

-   `<say-as>` indica in che modo il testo racchiuso tra tag `<say-as>` di apertura e di chiusura deve essere gestito nella fase di normalizzazione. Gli attributi specificano in che modo deve essere pronunciato il testo integrato. Il seguente esempio indica in che modo deve essere pronunciata la data:

    ```xml
    The baby was born on <say-as interpret-as="date" format="mdy">3/4/2016</say-as>.
    ```
    {: codeblock}

    Il servizio restituisce le informazioni di temporizzazione per le seguenti stringhe: "*The*", "*baby*", "*was*", "*born*", "*on*", "*3/4/2016.*" Il servizio normalizza la stringa "*3/4/2016*" come "*march fourth two thousand sixteen*". Le informazioni di temporizzazione delle parole per la stringa riflettono il tempo di inizio "*march*" e il tempo di fine "*sixteen*".

    Il seguente esempio indica che deve essere specificata la parola `Hello`:

    ```xml
    <say-as interpret-as="letters">Hello</say-as>.
    ```
    {: codeblock}

    Il servizio restituisce le informazioni di temporizzazione per la stringa "*Hello.*". Il servizio specifica la parola lettera per lettera durante la fase di normalizzazione. Le informazioni di temporizzazione delle parole nella risposta riflettono il tempo di inizio della lettera "*h*" e il tempo di fine della lettera "*o*".
-   `<phoneme>` fornisce una pronuncia per il testo tra le tag `<phoneme>` di apertura e di chiusura. Tuttavia, sia il testo che la tag di chiusura sono facoltativi. Il seguente esempio include il testo integrato e una tag di chiusura:

    ```xml
    The <phoneme alphabet="ibm" ph=".0tx.1me.0fo">tomato</phoneme> was ripe.
    ```
    {: codeblock}

    Il servizio restituisce le informazioni di temporizzazione per le seguenti stringhe: "*The*", "*tomato*", "*was*", "*ripe.*"

    Al contrario, il seguente esempio fornisce un elemento `<phoneme>` unario senza testo integrato e senza tag di chiusura:

    ```xml
    The <phoneme alphabet="ibm" ph=".0tx.1me.0fo"/> was ripe.
    ```
    {: codeblock}

    In questo caso, il servizio restituisce le informazioni di temporizzazione per le seguenti stringhe: "*The*", "*&lt;phoneme&gt;*", "*was*", "*ripe.*"
-   `<sub>` sostituisce il testo incluso nell'attributo `alias` dell'elemento per il testo racchiuso tra le tag `<sub>` di apertura e di chiusura nell'audio pronunciato. Ad esempio, il seguente input include una singola tag `<sub>`:

    ```xml
    I work at <sub alias="International Business Machines">IBM</sub>.
    ```
    {: codeblock}

    Il servizio produce le informazioni di temporizzazione per le seguenti stringhe: "*I*", "*work*", "*at*", "*{{site.data.keyword.IBM_notm}}.*". Il servizio normalizza la stringa "*{{site.data.keyword.IBM_notm}}*" come "*International Business Machines*". Le informazioni di temporizzazione per la stringa riflettono il tempo di inizio "*International*" e il tempo di fine "*Machines*".
-   `<break>` inserisce una pausa nel testo pronunciato. Il servizio riflette l'assenza di suono risultante nelle temporizzazioni delle parole come un divario tra il tempo di fine di una parola che precede l'elemento `<break>` e il tempo di inizio della parola che segue l'elemento.
- `<paragraph>` (oppure `<p>`) può aggiungere un'assenza di suono all'audio. Il servizio non restituisce le informazioni di temporizzazione per l'assenza di suono.
- `<sentence>` (oppure `<s>`) può aggiungere un'assenza di suono all'audio. Il servizio non restituisce le informazioni di temporizzazione per l'assenza di suono.

Gli elementi SSML che non vengono menzionati nell'elenco non influiscono sulle informazioni di temporizzazione delle parole. Per ulteriori informazioni sul supporto del servizio per SSML, vedi [Utilizzo di SSML](/docs/services/text-to-speech-data?topic=text-to-speech-data-ssml).

## Esempi di elementi mark
{: #timingExample}

I seguenti esempi mostrano una sessione WebSocket semplice tra un client e il servizio. Gli esempi si concentrano sullo scambio di dati, non sull'apertura della connessione. Il client invia un messaggio di testo che include due elementi `<mark>`, denominati `SIMPLE` e `EXAMPLE` e richiede la restituzione dell'audio in formato WAV:

```javascript
{
  "text": "This is a <mark name=\"SIMPLE\"/>simple <mark name=\"EXAMPLE\"/> example.",
  "accept": "audio/wav"
}
```
{: codeblock}

Il servizio invia innanzitutto un messaggio per confermare il formato audio. Poi invia più messaggi con i risultati. Il servizio non può garantire il numero di blocchi audio che invia al client o l'ordine in cui vengono consegnati i messaggi audio e di testo.

Sono possibili entrambe le risposte riportate di seguito. In ogni caso, il servizio invia due messaggi di testo che identificano le posizioni dei contrassegni nel flusso binario. Tuttavia, invia un numero arbitrario di messaggi binari che contengono l'audio. Le informazioni di temporizzazione per un contrassegno arrivano sempre prima del blocco audio che contiene la posizione del contrassegno.

### Prima risposta di esempio

Nella prima risposta di esempio, i messaggi di testo vengono intervallati da più messaggi audio.

```javascript
{
  "binary_streams": [
    {
      "content_type": "audio/wav"
    }
  ]
}
... one or more chunks of binary audio
    all audio precedes the SIMPLE mark ...
{
  "marks": [
    [
      "SIMPLE",
      0.7848991042702103
    ]
  ]
}
... one or more chunks of binary audio
    audio can precede and follow the SIMPLE mark
    all audio precedes the EXAMPLE mark ...
{
  "marks": [
    [
      "EXAMPLE", 1.0034702987337102
    ]
  ]
}
... one or more chunks of binary audio
    audio can precede and follow the EXAMPLE mark ...
```
{: codeblock}

### Seconda risposta di esempio

Nella seconda risposta di esempio, i messaggi di testo arrivano prima dei messaggi audio.

```javascript
{
  "binary_streams": [
    "content_type": "audio/wav"}
  ]
}
{
  "marks": [
    [
      "SIMPLE", 0.7848991042702103
    ]
  ]
}
{
  "marks": [
    [
      "EXAMPLE", 1.0034702987337102
    ]
  ]
}
... one or more chunks of binary audio ...
```
{: codeblock}
