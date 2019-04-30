---

copyright:
  years: 2015, 2019
lastupdated: "2019-03-28"

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

# Note sulla release
{: #release-notes}

Le seguenti sezioni documentano le nuove funzioni e le modifiche incluse per ogni release e aggiornamento del servizio {{site.data.keyword.texttospeechfull}}. Le informazioni includono le limitazioni note. Salvo diversa indicazione, tutte le modifiche sono compatibili con le release precedenti e sono automaticamente e trasparentemente disponibili per tutte le applicazioni nuove ed esistenti.
{: shortdesc}

## Limitazioni note
{: #limitations}

Un problema con la distribuzione delle voci DDN (Deep Neural Network) `V2` causa un rumore di fondo nel discorso sintetizzato. {{site.data.keyword.IBM_notm}} sta lavorando per risolvere il problema. 

## 24 marzo 2019
{: #March2019c}

-   Il servizio ora offre versioni DNN (Deep Neural Network) delle sue voci in tedesco:
    -   `de-DE_BirgitV2Voice`
    -   `de-DE_DieterV2Voice`

    Per ulteriori informazioni sulle voci basate su DNN, vedi [Tecnologie di sintesi vocale](/docs/services/text-to-speech/voices.html#technologiesVoices).
-   Tutte le voci basate su DNN del servizio ora supportano gli attributi `pitch` e `rate` dell'elemento `<prosody>` SSML. Le voci basate su DNN non supportano l'attributo `volume` dell'elemento `<prosody>`. Per ulteriori informazioni, vedi [L'elemento prosody](/docs/services/text-to-speech/SSML-elements.html#prosody_element). 

## 21 marzo 2019
{: #March2019b}

Ora gli utenti possono vedere solo le informazioni sulla credenziale del servizio associate al ruolo che è stato assegnato al loro account {{site.data.keyword.cloud_notm}}. Ad esempio, se ti viene assegnato un ruolo `reader`, qualsiasi livello `writer` o superiore delle credenziali del servizio non sarà più visibile.

Questa modifica non influisce sull'accesso API per gli utenti o le applicazioni con credenziali del servizio esistenti. La modifica influisce solo sulla visualizzazione delle credenziali all'interno di {{site.data.keyword.cloud_notm}}.

Per ulteriori informazioni sulle chiavi del servizio e sui ruoli utente, vedi [Chiavi API del servizio IAM](/docs/services/watson?topic=watson-api-key-bp#api-key-bp).

## 4 marzo 2019
{: #March2019a}

Ora il servizio offre quattro nuove voci che utilizzano la sintesi di apprendimento approfondito per generare l'audio:

-   `it-IT_FrancescaV2Voice`
-   `en-US_AllisonV2Voice`
-   `en-US_LisaV2Voice`
-   `en-US_MichaelV2Voice`

Queste nuove voci utilizzano il machine learning e una DNN per sintetizzare il testo in voce. La sintesi di apprendimento approfondito o basata su DNN produce un audio con una prosodia più naturale e una qualità complessiva più coerente. 

Tuttavia le nuove voci producono anche un audio con qualità di segnale diverse dalle voci esistenti, quindi potrebbero non essere appropriate per tutte le applicazioni. Inoltre, le nuove voci non supportano gli elementi `<prosody>`, `<express-as>` e `<voice-transformation>` SSML.

Per ulteriori informazioni su queste voci basate su DNN e su come differiscono dalle voci esistenti, vedi [Tecnologie di sintesi vocale](/docs/services/text-to-speech/voices.html#technologiesVoices).

## Release precedenti
{: #older}

-   [28 gennaio 2019](#January2019)
-   [13 dicembre 2018](#December2018)
-   [7 novembre 2018](#November2018)
-   [30 ottobre 2018](#October2018)
-   [12 giugno 2018](#June2018)
-   [15 maggio 2018](#May2018)
-   [2 ottobre 2017](#October2017)
-   [14 luglio 2017](#July2017)
-   [10 aprile 2017](#April2017)
-   [1 dicembre 2016](#December2016)
-   [22 settembre 2016](/docs/services/text-to-speech/release-notes.html#September2016)
-   [23 giugno 2016](/docs/services/text-to-speech/release-notes.html#June2016)
-   [10 marzo 2016](/docs/services/text-to-speech/release-notes.html#March2016)
-   [22 febbraio 2016](/docs/services/text-to-speech/release-notes.html#February2016)
-   [17 dicembre 2015](/docs/services/text-to-speech/release-notes.html#December2015)
-   [21 settembre 2015](/docs/services/text-to-speech/release-notes.html#September2015)
-   [1 luglio 2015](/docs/services/text-to-speech/release-notes.html#July2015)

### 28 gennaio 2019
{: #January2019}

Ora l'interfaccia WebSocket supporta l'autenticazione IAM (Identity and Access Management) basata sul token dal codice JavaScript basato sul browser. La limitazione al contrario è stata rimossa. Per stabilire una connessione autenticata con il metodo WebSocket `/v1/synthesize`:

-   Se utilizzi l'autenticazione IAM, includi il parametro di query `access_token`. 
-   Se utilizzi le credenziali del servizio Cloud Foundry, includi il parametro di query `watson-token`.

Per ulteriori informazioni, vedi [Apri una connessione](/docs/services/text-to-speech/websockets.html#WSopen).

### 13 dicembre 2018
{: #December2018}

Il servizio {{site.data.keyword.texttospeechshort}} è ora disponibile nell'ubicazione Londra di {{site.data.keyword.cloud}} (**eu-gb**). Come tutte le ubicazioni, Londra utilizza l'autenticazione IAM (Identity and Access Management) basata sul token. Tutte le nuove istanze del servizio che crei in questa ubicazione utilizzano l'autenticazione IAM. 

### 7 novembre 2018
{: #November2018}

Il servizio {{site.data.keyword.texttospeechshort}} è ora disponibile nell'ubicazione Tokyo di {{site.data.keyword.cloud}} (**jp-tok**). Come tutte le ubicazioni, Tokyo utilizza l'autenticazione IAM (Identity and Access Management) basata sul token. Tutte le nuove istanze del servizio che crei in questa ubicazione utilizzano l'autenticazione IAM. 

### 30 ottobre 2018
{: #October2018}

Il servizio {{site.data.keyword.texttospeechshort}} è stato migrato all'autenticazione IAM (Identity and Access Management) basata sul token per tutte le ubicazioni. Ora tutti i servizi {{site.data.keyword.cloud_notm}} utilizzano l'autenticazione IAM. Il servizio {{site.data.keyword.texttospeechshort}} ha eseguito la migrazione in ciascuna ubicazione nelle seguenti date:

-   Dallas (**us-south**): 30 ottobre 2018
-   Francoforte (**eu-de**): 30 ottobre 2018
-   Washington, DC (**us-east**): 12 giugno 2018
-   Sydney (**au-syd**): 15 maggio 2018

La migrazione all'autenticazione IAM influisce sulle nuove istanze del servizio e su quelle esistenti in modo diverso: 

-   *Tutte le nuove istanze del servizio che crei in qualsiasi ubicazione* ora utilizzano l'autenticazione IAM per accedere al servizio. Puoi passare un token di connessione o una chiave API: i token supportano le richieste autenticate senza integrare le credenziali di servizio in ogni chiamata; le chiavi API utilizzano l'autenticazione di base HTTP. Quando utilizzi uno qualsiasi degli SDK {{site.data.keyword.ibmwatson}}, puoi passare la chiave API e lasciare che SDK gestisca il ciclo di vita dei token.
-   *Le istanze del servizio esistenti che hai creato in un'ubicazione prima della data di migrazione indicata* continuano a utilizzare `{username}` e `{password}` delle loro precedenti credenziali del servizio Cloud Foundry per l'autenticazione fino a quando non le aggiornerai per utilizzare l'autenticazione IAM. Per ulteriori informazioni sulla migrazione all'autenticazione IAM, vedi [Migrazione di istanze del servizio Cloud Foundry a un gruppo di risorse](https://{DomainName}/docs/resources/instance_migration.html).

Per ulteriori informazioni, consulta la seguente documentazione:

-   Per sapere quale meccanismo di autenticazione viene utilizzato dalla tua istanza del servizio, visualizza le tue credenziali del servizio facendo clic sull'istanza nel [dashboard {{site.data.keyword.cloud_notm}}  ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://{DomainName}/dashboard/apps){: new_window}.
-   Per ulteriori informazioni sull'utilizzo dei token IAM con i servizi {{site.data.keyword.watson}}, vedi [Autenticazione con i token IAM](/docs/services/watson/getting-started-iam.html).
-   Per ulteriori informazioni sull'utilizzo delle chiavi API IAM con i servizi {{site.data.keyword.watson}}, vedi [Chiavi API del servizio IAM](/docs/services/watson/apikey-bp.html).
-   Per esempi che utilizzano l'autenticazione IAM, vedi il [Riferimento API ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://{DomainName}/apidocs/text-to-speech){: new_window}.

### 12 giugno 2018
{: #June2018}

Le seguenti funzioni sono abilitate per le applicazioni ospitate a Washington, DC (**us-east**):

-   Ora il servizio supporta un nuovo processo di autenticazione API. Per ulteriori informazioni, vedi l'[aggiornamento del servizio del 30 ottobre 2018](#October2018).
-   Ora il servizio supporta l'intestazione `X-Watson-Metadata` e il metodo `DELETE /v1/user_data`. Per ulteriori informazioni, vedi [Sicurezza delle informazioni](/docs/services/text-to-speech/information-security.html).

### 15 maggio 2018
{: #May2018}

Le seguenti funzioni sono abilitate per le applicazioni ospitate a Sydney (**au-syd**):

-   Ora il servizio supporta un nuovo processo di autenticazione API. Per ulteriori informazioni, vedi l'[aggiornamento del servizio del 30 ottobre 2018](#October2018).
-   Ora il servizio supporta l'intestazione `X-Watson-Metadata` e il metodo `DELETE /v1/user_data`. Per ulteriori informazioni, vedi [Sicurezza delle informazioni](/docs/services/text-to-speech/information-security.html).

### 2 ottobre 2017
{: #October2017}

Per il formato `audio/l16`, ora puoi specificare facoltativamente l'endianness dell'audio restituito. (Devi aver già specificato la velocità di campionamento.) Gli esempi sono `audio/l16;rate=22050;endianness=big-endian` e `audio/l16;rate=22050;endianness=little-endian`; il valore predefinito è big endian. Per ulteriori informazioni, vedi [Formati audio](/docs/services/text-to-speech/audio-formats.html).

### 14 luglio 2017
{: #July2017}

Ora il servizio supporta il formato audio MP3 o MPEG (Motion Picture Experts Group). Per ulteriori informazioni sui formati audio supportati, vedi [Formati audio](/docs/services/text-to-speech/audio-formats.html).

### 10 aprile 2017
{: #April2017}

-   Ora il servizio supporta il formato audio Web Media (WebM) con il codec Opus o Vorbis. Al momento in servizio supporta anche il formato audio Ogg con il codec Vorbis in aggiunta al codec Opus. Per ulteriori informazioni sui formati audio supportati, vedi [Formati audio](/docs/services/text-to-speech/audio-formats.html).
-   Ora il servizio supporta CORS (Cross-Origin Resource Sharing) per consentire ai client basati sul browser di richiamare direttamente il servizio. Per ulteriori informazioni, vedi [Supporto CORS](/docs/services/text-to-speech/developer-overview.html#cors).
-   I codici di risposta HTTP per il completamento riuscito di alcuni metodi dell'interfaccia di personalizzazione sono cambiati: 
    -   Il metodo `POST /v1/customizations` ora restituisce 201 (invece di 200).
    -   Il metodo `POST /v1/customizations/{customization_id}` ora restituisce 200 (invece di 201).
    -   Il metodo `POST /v1/customizations/{customization_id}/words` ora restituisce 200 (invece di 201).
    -   Il metodo `PUT /v1/customizations/{customization_id}/words/{word}` ora restituisce 200 (invece di 201).
-   I metodi `POST /v1/customizations/{custom_id}/words` e `PUT /v1/customizations/{customization_id}/words/{word}` ora restituiscono il codice risposta HTTP 400 con il messaggio di errore `Part of speech is supported for ja-JP language only` se tenti di specificare `part_of_speech` per una lingua diversa dal giapponese. 
-   Il metodo `POST /v1/customizations/{custom_id}/words` ora restituisce un corpo della risposta vuoto (`{}`).

### 1 dicembre 2016
{: #December2016}

-   Il servizio include una nuova voce, `es-LA_SofiaVoice`, che è l'equivalente latino americano della voce `es-US_SofiaVoice`. La differenza più significativa tra le due voci riguarda il modo in cui interpretano un `$` (segno del dollaro): la versione latino americana utilizza il termine *pesos*, mentre la versione nord americana utilizza il termine *dolares*. Tra le due voci potrebbero esistere anche altre piccole differenze. 
-   In aggiunta a `en-US_AllisonVoice`, ora altre due voci sono trasformabili con la trasformazione della voce SSML: `en-US_LisaVoice` e `en-US_MichaelVoice`. Per ulteriori informazioni sulla trasformazione della voce, vedi [SSML per la trasformazione della voce](/docs/services/text-to-speech/SSML-transformation.html).
-   Quando utilizzi l'interfaccia personalizzata con il giapponese, il servizio mette ora in corrispondenza la parola più lunga proveniente dalle coppie di parole/traduzioni definite per un modello vocale personalizzato. Ad esempio, considera le due voci riportate di seguito per una voce personalizzata: 

    <pre><code data-copy="false" class="language-javascript">  {
      "words": [
        {"word":"&#65326;&#65337;", "translation":"&#12491;&#12517;&#12540;&#12520;&#12540;&#12463;", "part_of_speech":"Mesi"},
        {"word":"&#65326;&#65337;&#65315;", "translation":"&#12491;&#12517;&#12540;&#12520;&#12540;&#12463;&#12471;&#12486;&#12451;", "part_of_speech":"Mesi"}
      ]
    }</code></pre>

    Se il servizio trova la stringa <code>&#65326;&#65337;&#65315;</code> nel testo di input, mette in corrispondenza tale parola perché è una corrispondenza più lunga di <code>&#65326;&#65337;</code>. In precedenza, il servizio avrebbe messo in corrispondenza la stringa <code>&#65326;&#65337;</code>. Per ulteriori informazioni su come utilizzare le voci in giapponese per un modello vocale personalizzato, vedi [Utilizzo di voci in giapponese](/docs/services/text-to-speech/custom-rules.html#jaNotes).

### 22 settembre 2016
{: #September2016}

-   L'interfaccia di personalizzazione, che include la personalizzazione e i metodi `GET /v1/pronunciation`, è ora disponibile per tutte le lingue supportate dal servizio. L'interfaccia rimane a una release beta. Per ulteriori informazioni, vedi [Informazioni sulla personalizzazione](/docs/services/text-to-speech/custom-intro.html). 
-   Ora il servizio supporta SSML (Speech Synthesis Markup Language) per il giapponese. Per informazioni generali sul supporto SSML, vedi [Utilizzo di SSML](/docs/services/text-to-speech/SSML.html). Per informazioni sui simboli SPR e IPA in giapponese, vedi [Simboli per il giapponese](/docs/services/text-to-speech/ja-JP-SPRs.html). Quando crei le voci per le parole in un modello vocale personalizzato in giapponese, vengono applicate considerazioni supplementari e un campo `part_of_speech`. Per ulteriori informazioni, vedi [Utilizzo di voci in giapponese](/docs/services/text-to-speech/custom-rules.html#jaNotes).
-   Ora il servizio offre una trasformazione della voce SSML tramite il nuovo elemento `<voice-transformation>`. Puoi espandere la gamma di possibili voci creando delle trasformazioni della voce personalizzate che modificano il tono, la gamma dei toni, la tensione glottidale, la respirazione, la velocità e il timbro di una voce. Il servizio offre anche due voci virtuali integrate, *Young* e *Soft*. Al momento il servizio supporta la trasformazione della voce solo per la voce in inglese americano Allison. Per ulteriori informazioni, vedi [SSML per la trasformazione della voce](/docs/services/text-to-speech/SSML-transformation.html).
-   Ora il servizio può restituire le informazioni di temporizzazione per tutte le stringhe del testo di input che passi all'interfaccia WebSocket. Per ricevere il tempo di inizio e di fine di ogni stringa nell'input, specifica un array che include la stringa `words` per il parametro facoltativo `timings` dell'oggetto JSON che passi al servizio. La funzione non è al momento disponibile per il testo di input in giapponese. Per ulteriori informazioni, vedi [Come ottenere le temporizzazioni delle parole](/docs/services/text-to-speech/word-timing.html).
-   Ora il servizio convalida tutti gli elementi SSML che inoltri in qualsiasi contesto. Se trova una tag non valida, il servizio riporta un codice di risposta HTTP 400 con un messaggio descrittivo e il metodo ha esito negativo. Nelle release precedenti, il servizio gestiva gli errori in modo incoerente; se si specificava la pronuncia non valida di una parola, ad esempio, poteva verificarsi un comportamento imprevedibile o incoerente. Per ulteriori informazioni, vedi [Convalida SSML](/docs/services/text-to-speech/SSML.html#errors).
-   L'uso di `spr` è obsoleto come argomento per l'opzione `format` del metodo `GET /v1/pronunciation` e per l'uso con l'attributo `alphabet` di un elemento `<phoneme>` SSML. Per utilizzare la notazione {{site.data.keyword.IBM_notm}} SPR (Symbolic Phonetic Representation), utilizza l'argomento `ibm` invece di `spr` in tutti i casi.
-   Ora l'elenco dei formati audio supportati include `audio/mulaw;rate=8000`. Come `audio/basic`, questo formato fornisce un audio a canale singolo che viene codificato utilizzando dati u-law (o mu-law) a 8 bit campionati a 8 kHz. Per ulteriori informazioni, vedi [Formati audio](/docs/services/text-to-speech/audio-formats.html).
-   Ora i metodi `GET /v1/voices` e `GET /v1/voices/{voice}` restituiscono un oggetto `supported_features` come parte del loro output per ciascuna voce. L'oggetto descrive se la voce supporta la personalizzazione e l'elemento `<voice_transformation>` SSML. Per ulteriori informazioni, vedi
      [Lingue e voci](/docs/services/text-to-speech/voices.html).
    

### 23 giugno 2016
{: #June2016}

-   Ora il servizio offre un'interfaccia WebSocket per sintetizzare il testo in voce. L'interfaccia offre le stesse funzioni del metodo `/v1/synthesize` dell'interfaccia HTTP. Accetta il testo semplice o il testo contrassegnato con SSML. Inoltre, supporta l'uso dell'elemento `<mark>` SSML per identificare nell'audio il momento in cui termina la sintetizzazione di tutto il testo che precede il contrassegno. Per ulteriori informazioni, vedi [L'interfaccia WebSocket](/docs/services/text-to-speech/websockets.html).
-   Ora il servizio offre il supporto per il testo annotato con SSML per le lingue spagnolo castigliano e spagnolo nord americano, italiano e portoghese brasiliano. Il servizio supportata già l'uso di SSML per inglese americano e britannico, francese e tedesco. A partire da questo aggiornamento, il servizio supporta SSML per tutte le lingue ad eccezione del giapponese. Inoltre, puoi utilizzare entrambe le notazioni {{site.data.keyword.IBM_notm}} SPR e IPA per definire la pronuncia delle parole con l'elemento `<phoneme>` SSML. Per ulteriori informazioni, vedi [Utilizzo di SSML](/docs/services/text-to-speech/SSML.html) e [Utilizzo di IBM SPR](/docs/services/text-to-speech/SPRs.html).

    Per l'inglese americano, puoi anche utilizzare l'elemento `<phoneme>` SSML per creare immissioni di parole in un modello vocale personalizzato; la personalizzazione è supportata solo per l'inglese americano. Per ulteriori informazioni, vedi [Informazioni sulla personalizzazione](/docs/services/text-to-speech/custom-intro.html).
-   Il servizio offre una migliore espressività e naturalezza per le voci utilizzate più di frequente. I miglioramenti si basano sulla predizione della prosodia basata su RNN (Recursive Neural Network) derivante dal testo di input. Sono resi disponibili come nuovi aggiornamenti al motore di servizio e al modello vocale per le seguenti lingue: 

    -   `en-US_AllisonVoice`
    -   `en-US_LisaVoice`
    -   `en-US_MichaelVoice`
    -   `es-ES_EnriqueVoice`
    -   `fr-FR_ReneeVoice`
-   Ora il metodo `GET /v1/pronunciation` accetta un parametro di query `customization_id` facoltativo. Il parametro ottiene la traduzione di una parola da un modello vocale personalizzato specificato. Se il modello vocale non contiene la parola, il metodo restituisce la pronuncia predefinita della parola. Per ulteriori informazioni, vedi il [Riferimento API ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://{DomainName}/apidocs/text-to-speech){: new_window}.

    Quando utilizzi il metodo `GET /v1/pronunciation` senza un ID di personalizzazione e per una lingua diversa dall'inglese americano, puoi richiedere la pronuncia di una parola solo nella notazione {{site.data.keyword.IBM_notm}} SPR. Per le lingue diverse dall'inglese americano, devi specificare `spr` con l'opzione `format` del metodo.
    {: note}
-   Ora l'elenco dei formati audio supportati include `audio/basic`, che fornisce un audio a canale singolo che viene codificato utilizzando dati u-law (o mu-law) a 8 bit campionati a 8 kHz. Per ulteriori informazioni, vedi [Formati audio](/docs/services/text-to-speech/audio-formats.html).
-   I metodi `/v1/synthesize` HTTP e WebSocket possono restituire una risposta `warnings` che include messaggi relativi a parametri di query o campi JSON non validi che vengono inclusi in una richiesta. Il formato delle avvertenze è cambiato. Il seguente esempio mostra il formato precedente: 

    `"warnings": "Unknown arguments: [u'{invalid_arg_1}', u'{invalid_arg_2}']."`

    Ora la stessa avvertenza ha il seguente formato: 

    `"warnings": "Unknown arguments: {invalid_arg_1}, {invalid_arg_2}."`

### 10 marzo 2016
{: #March2016}

-   Ora i metodi `GET` e `POST /v1/synthesize` possono restituire un'intestazione di risposta `Warnings` che include un elenco di messaggi di avvertenza relativi a parametri di query o campi JSON non validi che vengono inclusi nella richiesta. Ogni elemento dell'elenco include una stringa che descrive la natura dell'avvertenza seguita da un array di stringhe di argomenti non valide; ad esempio, `Unknown arguments: [u'{invalid_arg_1}', u'{invalid_arg_2}'].` Per ulteriori informazioni, vedi il [Riferimento API ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://{DomainName}/apidocs/text-to-speech){: new_window}.
-   La versione beta di *{{site.data.keyword.watson}} Speech Software Development Kit (SDK) per il sistema operativo iOS di Apple&reg;* è obsoleta ed è stata sostituita da *{{site.data.keyword.watson}} SDK Swift*. Il nuovo SDK è disponibile nel [repository swift-sdk ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://github.com/watson-developer-cloud/swift-sdk){: new_window} nello spazio dei nomi `watson-developer-cloud` su GitHub.

### 22 febbraio 2016
{: #February2016}

Il servizio è stato aggiornato con una nuova funzione SSML di espressività. Il servizio estende SSML (Speech Synthesis Markup Language) con un elemento `<express-as>` che puoi utilizzare per indicare l'espressività in uno dei tre stili di pronuncia: `GoodNews`, `Apology` o `Uncertainty`. Puoi applicare l'elemento all'intero corpo del testo, a un periodo, a una frase o a una parola. Al momento il servizio supporta l'espressività solo per la voce in inglese americano Allison (`en-US_AllisonVoice`). Per ulteriori informazioni, vedi [SSML di espressività](/docs/services/text-to-speech/SSML-expressive.html).

### 17 dicembre 2015
{: #December2015}

-   Il servizio offre una nuova interfaccia di personalizzazione che puoi utilizzare per specificare la pronuncia di parole insolite nel tuo input. L'interfaccia include un numero di nuovi metodi che puoi utilizzare per creare e gestire i modelli vocali personalizzati e le coppie di parole/traduzioni che essi contengono. Puoi quindi utilizzare i tuoi modelli personalizzati per sintetizzare il testo in audio. 

    Il servizio supporta le traduzioni di suoni simili e le traduzioni fonetiche. Le traduzioni fonetiche possono utilizzare la rappresentazione IPA o {{site.data.keyword.IBM_notm}} SPR proprietaria. Puoi utilizzare SSML (Speech Synthesis Markup Language) per specificare traduzioni fonetiche. 

    L'interfaccia di personalizzazione include una raccolta di nuovi metodi HTTP denominati `POST /v1/customizations`, `POST /v1/customizations/{customization_id}`, `POST /v1/customizations/{customization_id}/words` e `PUT /v1/customizations/{customization_id}/words/{word}`. Il servizio fornisce anche un nuovo metodo `GET /v1/pronunciation` che restituisce la pronuncia di qualsiasi parola e un nuovo metodo `GET /v1/voices/{voice}` che restituisce le informazioni dettagliate su una specifica voce. Inoltre, ora i metodi esistenti dell'interfaccia del servizio accettano i parametri del modello vocale personalizzato a seconda delle necessità. 

    Per ulteriori informazioni sulla personalizzazione e sulla sua interfaccia, vedi [Informazioni sulla personalizzazione](/docs/services/text-to-speech/custom-intro.html) e il [Riferimento API ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://{DomainName}/apidocs/text-to-speech){: new_window}.

    L'interfaccia di personalizzazione è una release beta che al momento supporta solo l'inglese americano. Tutti i metodi di personalizzazione e il metodo `GET /v1/pronunciation` possono essere attualmente utilizzati per creare e manipolare modelli vocali personalizzati e traduzioni delle parole solo in inglese americano.
    {: note}
-   Il servizio supporta una nuova voce, `pt-BR_IsabelaVoice`, per sintetizzare l'audio in portoghese brasiliano con una voce femminile. Per ulteriori informazioni, vedi [Lingue e voci](/docs/services/text-to-speech/voices.html). 

### 21 settembre 2015
{: #September2015}

-   Sono disponibili due nuovi SDK (Software Development Kit) mobili versione beta per i servizi vocali. Gli SDK consentono alle applicazioni mobili di interagire con i servizi {{site.data.keyword.texttospeechshort}} e {{site.data.keyword.speechtotextshort}}. Puoi utilizzare gli SDK per inviare testo al servizio {{site.data.keyword.texttospeechshort}} e ricevere una risposta audio. 
    -   *{{site.data.keyword.watson}} SDK Swift* è disponibile nel [repository swift-sdk ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://github.com/watson-developer-cloud/swift-sdk){: new_window} nello spazio dei nomi `watson-developer-cloud` su GitHub.
    -   L'*{{site.data.keyword.watson}} SDK Speech Android* è disponibile nel [repository speech-android-sdk ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://github.com/watson-developer-cloud/speech-android-sdk){: new_window} nello spazio dei nomi `watson-developer-cloud` su GitHub.

    Entrambi gli SDK supportano l'autenticazione con i servizi vocali utilizzando le tue credenziali del servizio {{site.data.keyword.cloud_notm}} o un token di autenticazione. 

    Poiché gli SDK sono funzionalità di versione beta, sono soggetti a cambiamenti in futuro.
    {: note}
-   Il servizio supporta una nuova lingua, il giapponese. La voce `ja-JP_EmiVoice` è una voce femminile in giapponese. 

### 1 luglio 2015
{: #July2015}

Il servizio è passato da beta a GA (general availability) il 1° luglio 2015. Tra le versioni beta e GA dell'API {{site.data.keyword.texttospeechshort}} erano presenti le seguenti differenze. La release GA ha richiesto che gli utenti eseguissero l'upgrade alla nuova versione del servizio. 

-   Un nuovo modello di programmazione supporta l'interazione diretta tra un client e il servizio. Utilizzando questo modello, un client può ottenere un token di autenticazione per comunicare direttamente con il servizio. Utilizzando il token, il client può eludere la necessità di un'applicazione proxy lato server in {{site.data.keyword.cloud_notm}} che richiami il servizio per suo conto. I token sono i mezzi preferiti per i client per interagire con il servizio. 

    Il servizio continua a supportare il vecchio modello di programmazione basato su un proxy lato server per trasmettere le comunicazioni e i dati tra il client e il servizio. Tuttavia, il nuovo modello è più efficiente e offre una velocità effettiva più elevata. Per ulteriori informazioni sul nuovo modello di programmazione, vedi [Modelli di programmazione per i servizi {{site.data.keyword.watson}}](/docs/services/watson/getting-started-develop.html).
-   Ora puoi passare SSML (Speech Synthesis Markup Language) alle versioni `GET` e `POST` HTTP del metodo `/v1/synthesize`. SSML è un linguaggio di markup basato su XML progettato per fornire annotazioni di testo per le applicazioni di sintesi vocale come il servizio {{site.data.keyword.texttospeechshort}}. Per ulteriori informazioni sul passaggio dell'input SSML al servizio, vedi [Specifica del testo di input](/docs/services/text-to-speech/http.html#input).

    Il servizio supporta inizialmente l'uso di SSML solo per le lingue inglese americano e inglese britannico, il francese e il tedesco. Il servizio non supporta SSML con l'italiano e lo spagnolo. Quando utilizzi SSML, assicurati di non selezionare una delle lingue non supportate per una voce per l'audio. I risultati in questo caso non sono significativi.
-   Le voci supportate per il discorso sintetizzato sono cambiate e sono state ampliate. Ora il servizio supporta voci, lingue e dialetti aggiuntivi con i metodi `/v1/synthesize`. Per ulteriori informazioni sulle voci supportate, vedi [Lingue e voci](/docs/services/text-to-speech/voices.html).

    Tre voci che erano disponibili nella versione beta sono state ridenominate per la GA:
    -   `VoiceEnUsMichael` è ora `en-US_MichaelVoice`
    -   `VoiceEnUsLisa` è ora `en-US_LisaVoice`
    -   `VoiceEsEsEnrique` è ora `es-ES_EnriqueVoice`

    I nomi precedenti delle voci continuano a funzionare con la versione beta del servizio (tramite gli endpoint API `-beta`) mentre tale versione rimane disponibile. Tuttavia, devi utilizzare i nuovi nomi con la versione GA del servizio.
-   Ora puoi richiedere al servizio di restituire l'audio nel formato FLAC (Free Lossless Audio Codec). Il servizio può ancora restituire l'audio nel formato Ogg con il codec Opus (l'impostazione predefinita) e nel formato WAV (Waveform Audio File Format). Per ulteriori informazioni sull'utilizzo dei formati audio con i metodi `/v1/synthesize`, vedi [Formati audio](/docs/services/text-to-speech/audio-formats.html).
-   Il testo che invii al metodo `/v1/synthesize` nell'URL di una richiesta `GET` HTTP o nel corpo di una richiesta `POST` HTTP è ora limitato a un massimo di 5 KB. Il testo aveva una dimensione massima di 4 MB per la versione beta.
-   Ora i metodi `/v1/synthesize` includono l'intestazione `X-WDC-PL-OPT-OUT` per controllare se il servizio utilizza il testo e i risultati audio provenienti da un'operazione per migliorare i risultati futuri. Specifica un valore `1` affinché l'intestazione impedisca al servizio di utilizzare il testo e i risultati audio. Il parametro si applica solo alla richiesta corrente. La nuova intestazione sostituisce l'intestazione `X-logging` proveniente dai metodi beta. Per ulteriori informazioni, vedi [Controllo della registrazione delle richieste per i servizi {{site.data.keyword.watson}}](/docs/services/watson/getting-started-logging.html).
-   Per i metodi `/v1/synthesize`, sono cambiati i seguenti codici di errore: 
    -   Il codice di errore 406 ("Not acceptable. Unsupported MIME type.") è stato rimosso.
    -   Il codice di errore 415 ("Unsupported Media Type") è stato aggiunto.
    -   Il codice di errore 503 ("Service Unavailable") è stato aggiunto.
-   Per il metodo `GET /v1/voices`, sono cambiati i seguenti codici di errore:
    -   Il codice di errore 406 ("Not acceptable. Unsupported MIME type.") è stato rimosso.
    -   Il codice di errore 415 ("Unsupported Media Type") è stato aggiunto.
