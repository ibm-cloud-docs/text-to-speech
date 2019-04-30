---

copyright:
  years: 2015, 2019
lastupdated: "2019-03-07"

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

# Creazione e gestione di voci personalizzate
{: #customWords}

Una volta che esiste un modello personalizzato, il passo successivo è aggiungere le voci personalizzate sotto forma di coppie di parole/traduzioni per definire il modo in cui le parole specificate devono essere pronunciate durante la sintesi. Le definizioni sovrascrivono le regole di pronuncia regolare predefinite del servizio. Puoi aggiungere ed eseguire query di traduzioni per una o più parole alla volta e puoi eliminare singole parole che non ti servono più. Una volta acquisita familiarità con l'interfaccia di personalizzazione, la manipolazione di più parole alla volta può essere più pratica rispetto alla gestione parola per parola. Devi utilizzare le credenziali del servizio per l'istanza del servizio che possiede un modello personalizzato per utilizzare qualsiasi metodo che richieda il suo ID di personalizzazione.
{: shortdesc}

## Aggiunta di una singola parola a un modello personalizzato
{: #cuWordAdd}

Per aggiungere una singola coppia di parola/traduzione a un modello personalizzato, utilizza il metodo `PUT /v1/customizations/{customization_id}/words/{word}`. Specifica la parola da aggiungere nell'URL del metodo. Fornisci la traduzione della parola come oggetto JSON con un singolo attributo `translation`. L'aggiunta di una nuova traduzione per una parola che già esiste in un modello sovrascrive la traduzione esistente della parola.

Puoi fornire una traduzione utilizzando il metodo di suoni simili o il metodo fonetico (o una combinazione dei due). Per le traduzioni fonetiche, puoi utilizzare il formato IPA (International Phonetic Alphabet) o il formato {{site.data.keyword.IBM_notm}} SPR (Symbolic Phonetic Representation). I seguenti esempi utilizzano approcci diversi per aggiungere traduzioni equivalenti per la parola `IEEE` a un modello personalizzato.

-   **Suoni simili:** per questo esempio, il metodo di suoni simili è l'approccio più semplice:

    ```bash
    curl -X PUT -u "apikey:{apikey}"
    --header "Content-Type: application/json"
    --data "{\"translation\":\"I triple E\"}"
    "https://stream.watsonplatform.net/text-to-speech/api/v1/customizations/{customization_id}/words/IEEE"
    ```
    {: pre}

-   **Fonetica IPA:** IPA richiede l'utilizzo dell'elemento `<phoneme>` con l'attributo `alphabet` impostato su `ipa` e l'attributo `ph` definito nel formato IPA:

    <pre><code class="language-bash">  curl -X PUT -u "apikey:{apikey}"
    --header "Content-Type: application/json"
    --data "{\"translation\":\"&lt;phoneme alphabet=\\\"ipa\\\" ph=\\\"&#712;a&#618;.t&#633;&#712;&#616;p&#601;l.&#712;i\\\"&gt;&lt;/phoneme&gt;\"}"
    "https://stream.watsonplatform.net/text-to-speech/api/v1/customizations/{customization_id}/words/IEEE"</code></pre>

-   **Fonetica {{site.data.keyword.IBM_notm}} SPR:** SPR utilizza l'elemento `<phoneme>` con l'attributo `alphabet` impostato su `ibm` e l'attributo `ph` definito nel formato SPR:

    ```bash
    curl -X PUT -u "apikey:{apikey}"
    --header "Content-Type: application/json"
    --data "{\"translation\":\"<phoneme alphabet=\\\"ibm\\\" ph=\\\"1Y.tr1Ipxl.1i\\\"></phoneme>\"}"
    "https://stream.watsonplatform.net/text-to-speech/api/v1/customizations/{customization_id}/words/IEEE"
    ```
    {: pre}

## Aggiunta di più parole a un modello personalizzato
{: #cuWordsAdd}

Per aggiungere una o più parole alla volta a un modello personalizzato, utilizza il metodo `POST /v1/customizations/{customization_id}/words`. Specifica le voci da aggiungere al modello personalizzato come un'array JSON di coppie di parole/traduzioni. Il seguente esempio aggiunge traduzioni di suoni simili comuni per le parole `NCAA` e `iPhone` a un modello personalizzato:

```bash
curl -X POST -u "apikey:{apikey}"
--header "Content-Type: application/json"
--data "{\"words\": [{\"word\":\"NCAA\", \"translation\":\"N C double A\"}, {\"word\":\"iPhone\", \"translation\":\"I phone\"}]}"
"https://stream.watsonplatform.net/text-to-speech/api/v1/customizations/{customization_id}/words"
```
{: pre}

Il contenuto JSON inviato nel corpo della richiesta equivale a quanto segue:

```javascript
{
  "words": [
    {"word":"NCAA", "translation":"N C double A"},
    {"word":"iPhone", "translation":"I phone"}
  ]
}
```
{: codeblock}

Come accennato in [Aggiornamento di un modello personalizzato](/docs/services/text-to-speech/custom-models.html#cuModelsUpdate), puoi anche utilizzare il metodo `POST /v1/customizations/{customization_id}` per aggiungere parole a un modello personalizzato. Nel seguente esempio viene utilizzato questo metodo per aggiungere le stesse due parole dell'esempio precedente; non vengono apportate modifiche ai metadati del modello. Ad eccezione dell'URL, i due metodi sono identici.

```bash
curl -X POST -u "apikey:{apikey}"
--header "Content-Type: application/json"
--data "{\"words\": [{\"word\":\"NCAA\", \"translation\":\"N C double A\"}, {\"word\":\"iPhone\", \"translation\":\"I phone\"}]}"
"https://stream.watsonplatform.net/text-to-speech/api/v1/customizations/{customization_id}"
```
{: pre}

## Aggiunta di parole a un modello personalizzato in giapponese
{: #cuJapaneseAdd}

Quando crei le voci per le parole in un modello vocale personalizzato in giapponese, vengono applicate ulteriori considerazioni e un campo `part_of_speech` aggiuntivo; per ulteriori informazioni, vedi [Utilizzo di voci in giapponese](/docs/services/text-to-speech/custom-rules.html#jaNotes). Specifica una parte del discorso per una voce personalizzata in giapponese nel seguente modo:

-   Per il metodo `PUT /v1/customizations/{customization_id}/words/{word}`, passa un oggetto JSON del seguente formato:

    ```javascript
    {
      "translation": "value",
      "part_of_speech": "value"
    }
    ```
    {: codeblock}

-   Per i metodi `POST /v1/customizations/{customization_id}/words` e `POST customizations/{customization_id}`, passa un oggetto JSON come il seguente esempio:

    ```javascript
    {
      "words": [
        {
          "word": "value",
          "translation": "value",
          "part_of_speech": "value"
        }
        . . .
      ]
    }
    ```
    {: codeblock}

I seguenti esempi del metodo `PUT /v1/customizations/{customization_id}/words/{word}` traducono la stringa a doppio byte con codifica URL per `NY` nel nome (`Mesi`) <code>&#12491;&#12517;&#12540;&#12520;&#12540;&#12463;</code> (`New York` in inglese). Se questa traduzione personalizzata non è definita, la stringa viene letta come `enu wai`.

-   **Suoni simili:**

    <pre><code>curl -X PUT -u "apikey:{apikey}"
    --header "Content-Type: application/json"
    --data "{\"translation\":\"&#12491;&#12517;&#12540;&#12520;&#12540;&#12463;\", \"part_of_speech\":\"Mesi\"}"
    "https://stream.watsonplatform.net/text-to-speech/api/v1/customizations/{customization_id}/words/%EF%BC%AE%EF%BC%B9"</code></pre>

-   **Fonetica IPA:**

    <pre><code>curl -X PUT -u "apikey:{apikey}"
    --header "Content-Type: application/json"
    --data "{\"translation\":\"&lt;phoneme alphabet=\\\"ipa\\\" ph=\\\"&#626;&#623;&#720;&#106;&#111;&#720;&#107;&#623;\\\"&gt;&lt;/phoneme&gt;\", \"part_of_speech\":\"Mesi\"}"
    "https://stream.watsonplatform.net/text-to-speech/api/v1/customizations/{customization_id}/words/%EF%BC%AE%EF%BC%B9"</code></pre>

-   **Fonetica {{site.data.keyword.IBM_notm}} SPR:**

    <pre><code>curl -X PUT -u "apikey:{apikey}"
    --header "Content-Type: application/json"
    --data "{\"translation\":\"&lt;phoneme alphabet=\\\"ibm\\\" ph=\\\"nyu:yo:ku\\\"&gt;&lt;/phoneme&gt;\", \"part_of_speech\":\"Mesi\"}"
    "https://stream.watsonplatform.net/text-to-speech/api/v1/customizations/{customization_id}/words/%EF%BC%AE%EF%BC%B9"</code></pre>

## Esecuzione di query di una singola parola da un modello personalizzato
{: #cuWordQueryModel}

Per eseguire la query della traduzione di una singola parola da un modello personalizzato, utilizza il metodo `GET /v1/customizations/{customization_id}/words/{word}`. Specifica la parola nell'URL del metodo. La traduzione viene restituita come è definita nel modello personalizzato (parola simile o fonetica).

Il seguente esempio esegue una query su un modello personalizzato per interrogare la traduzione della parola `IEEE`:

```bash
curl -X GET -u "apikey:{apikey}"
"https://stream.watsonplatform.net/text-to-speech/api/v1/customizations/{customization_id}/words/IEEE"
```
{: pre}

Se la parola ha la traduzione di suoni simili nel modello, l'esempio restituisce il seguente output JSON:

```javascript
{
  "translation": "I triple E"
}
```
{: codeblock}

## Esecuzione di query di tutte le parole da un modello personalizzato
{: #cuWordsQueryModel}

Per vedere le traduzioni di tutte le parole definite in un modello personalizzato, utilizza il metodo `GET /v1/customizations/{customization_id}/words`. Il seguente esempio utilizza il metodo per elencare le voci da un modello personalizzato che contiene le traduzioni di suoni simili per tre parole:

```bash
curl -X GET -u "apikey:{apikey}"
"https://stream.watsonplatform.net/text-to-speech/api/v1/customizations/{customization_id}/words"
```
{: pre}

Il metodo restituisce un array JSON con i seguenti dati. Per i modelli personalizzati in giapponese, l'output include la parte del discorso per le singole parole.

```javascript
{
  "words": [
    {
      "word": "IEEE",
      "translation": "I triple E"
    },
    {
      "word": "NCAA",
      "translation": "N C double A"
    },
    {
      "word": "iPhone",
      "translation": "I phone"
    }
  ]
}
```
{: codeblock}

Come descritto in [Esecuzione di query di un modello personalizzato](/docs/services/text-to-speech/custom-models.html#cuModelsQuery), puoi anche utilizzare il metodo `GET /v1/customizations/{customization_id}` per visualizzare sia i metadati che le parole per un modello personalizzato:

```bash
curl -X GET -u "apikey:{apikey}"
"https://stream.watsonplatform.net/text-to-speech/api/v1/customizations/{customization_id}"
```
{: pre}

Il metodo restituisce l'output JSON del seguente formato. Poiché questo esempio e quello precedente specificano lo stesso modello personalizzato, l'array di parole nel loro output è identico.

```javascript
{
  "customization_id": "64f4807f-a5f1-5867-924f-7bba1a84fe97",
  "owner": "297cfd08-330a-22ba-93ce-1a73f454dd98",
  "created": "2016-07-15T19:15:17.926Z",
  "name": "curl Test",
  "language": "en-US",
  "description": "Customization test via curl",
  "last_modified": "2016-07-15T19:46:01.387Z",
  "words": [
    {
      "word": "IEEE",
      "translation": "I triple E"
    },
    {
      "word": "NCAA",
      "translation": "N C double A"
    },
    {
      "word": "iPhone",
      "translation": "I phone"
    }
  ]
}
```
{: codeblock}

## Esecuzione di query di una parola da una lingua
{: #cuWordsQueryLanguage}

Per eseguire una query della pronuncia di una parola, utilizza il metodo `GET /v1/pronunciation`. Specifica una voce per ottenere la pronuncia nella lingua di quella voce. Per impostazione predefinita, il metodo restituisce la pronuncia in base alle regole di pronuncia regolare del servizio, ma puoi anche richiedere la pronuncia per un modello vocale personalizzato specificato. Il metodo include quattro parametri di query che ti consentono di specificare le informazioni che devono essere restituite:

-   Il parametro obbligatorio `text` specifica la parola di cui deve essere restituita la pronuncia.
-   Il parametro facoltativo `voice` ti consente di specificare la lingua della pronuncia. Specifica uno dei modelli vocali (ad esempio, `en-US_LisaVoice`) per indicare la lingua desiderata; tutte le voci per la stessa lingua (ad esempio, `en-US`) restituiscono la stessa pronuncia. Per impostazione predefinita, la pronuncia viene restituita per l'inglese americano.
-   Il parametro facoltativo `format` ti consente di specificare il formato fonetico della pronuncia, `ipa` o `ibm`. Per impostazione predefinita, la pronuncia viene restituita in formato IPA.
-   Il parametro facoltativo `customization_id` ti consente di specificare un modello vocale personalizzato per il quale deve essere restituita la pronuncia. Se la parola non è definita nel modello vocale specificato, il servizio restituisce la pronuncia predefinita per la lingua del modello. Ometti il parametro per vedere la traduzione per la voce specificata senza alcuna personalizzazione. Non specificare sia una voce che un modello vocale personalizzato.

Questo metodo è utile perché ti consente di eseguire la query di una parola da qualsiasi lingua e, poiché non richiede un ID di personalizzazione, non pone restrizioni sulle parole che puoi visualizzare. Può rivelarsi particolarmente utile quando si compone una traduzione fonetica per una nuova parola; puoi usarlo per ottenere la pronuncia per una parola esistente che puoi quindi utilizzare come base per la tua nuova traduzione, che è molto più comodo rispetto a creare una traduzione da zero.

Il seguente esempio ottiene la pronuncia per la parola `IEEE` nel formato IPA predefinito.

```bash
curl -X GET -u "apikey:{apikey}"
"https://stream.watsonplatform.net/text-to-speech/api/v1/pronunciation?text=IEEE"
```
{: pre}

<pre><code data-copy="false" class="language-javascript">{
  "pronunciation": ".&#712;a&#618; .&#712;i .&#712;i .&#712;i"
}</code></pre>

Il seguente esempio immette una traduzione di suoni simili per la parola `IEEE` e ottiene l'equivalente fonetico in formato {{site.data.keyword.IBM_notm}} SPR. Ottenere la pronuncia fonetica per una traduzione di suoni simili è un approccio particolarmente interessante alla composizione di una traduzione fonetica. Nell'esempio, gli spazi della parola sono codificati in URL.

```bash
curl -X GET -u "apikey:{apikey}"
"https://stream.watsonplatform.net/text-to-speech/api/v1/pronunciation?text=i%20triple%20e&format=ibm"
```
{: pre}

```javascript
{
  "pronunciation": "1Y.tr1Ipxl.1i"
}
```
{: codeblock}

## Eliminazione di una parola da un modello personalizzato
{: #cuWordDelete}

Per eliminare una parola da un modello personalizzato, utilizza il metodo `DELETE /v1/customizations/{customization_id}/words/{word}`. Specifica la parola da eliminare nell'URL del metodo. Puoi eliminare solo parole singole; non puoi eliminare più parole con un singolo metodo.

Il seguente esempio elimina la parola `IEEE` dal modello personalizzato specificato:

```bash
curl -X DELETE -u "apikey:{apikey}"
"https://stream.watsonplatform.net/text-to-speech/api/v1/customizations/{customization_id}/words/IEEE"
```
{: pre}
