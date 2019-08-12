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

# L'interfaccia HTTP
{: #usingHTTP}

Per sintetizzare il testo in voce utilizzando l'interfaccia REST HTTP del servizio {{site.data.keyword.texttospeechdatafull}} for {{site.data.keyword.icp4dfull}}, chiama il metodo `GET` o `POST /v1/synthesize`. Specifica il testo che deve essere sintetizzato e la voce e il formato per l'audio pronunciato. Puoi anche specificare un modello vocale personalizzato da utilizzare con la richiesta.
{: shortdesc}

Per ulteriori informazioni sull'interfaccia HTTP, vedi il [Riferimento API](https://{DomainName}/apidocs/text-to-speech-data){: external}.

## Sintetizzazione del testo in audio
{: #synthesize}

Per sintetizzare il testo in audio, chiama una delle due versioni del metodo `/v1/synthesize` del servizio:

-   Il metodo `GET /v1/synthesize` accetta il testo che deve essere sintetizzato come parametro di query `text` obbligatorio. La dimensione massima della richiesta è di 8 KB, che include il testo di input, qualsiasi SSML che specifichi e l'URL e le intestazioni.
-   Il metodo `POST /v1/synthesize` accetta il testo che deve essere sintetizzato come costrutto JSON nel corpo della richiesta. La dimensione massima della richiesta è di 8 KB per l'URL e le intestazioni e di 5 KB per il testo di input inviato nel corpo della richiesta. Il limite di 5 KB include qualsiasi SSML da te specificato.

Le due versioni del metodo `/v1/synthesize` hanno in comune i seguenti parametri:

<table>
  <caption>Tabella 1. Parametri dei metodi
    <code>/v1/synthesize</code></caption>
  <tr>
    <th style="text-align:left; width:18%">Parametro</th>
    <th style="text-align:center; width:12%">Tipo</th>
    <th style="text-align:center; width:12%">Tipo di dati</th>
    <th style="text-align:left">Descrizione</th>
  </tr>
  <tr>
    <td><code>accept</code><br/><em>Facoltativo</em></td>
    <td style="text-align:center">Query</td>
    <td style="text-align:center">Stringa</td>
    <td>
      Specifica il formato audio richiesto, o tipo MIME, in cui il
      servizio deve restituire l'audio. Puoi anche specificare questo valore con
      l'intestazione della richiesta HTTP <code>Accept</code>. Codifica in URL l'argomento
      nel parametro di query `accept`. Per ulteriori informazioni, vedi [Formati audio](/docs/services/text-to-speech-data?topic=text-to-speech-data-audioFormats).
    </td>
  </tr>
  <tr>
    <td><code>voice</code><br/><em>Facoltativo</em></td>
    <td style="text-align:center">Query</td>
    <td style="text-align:center">Stringa</td>
    <td>
      Specifica la voce in cui deve essere pronunciato il testo
      nell'audio. Utilizza il metodo <code>/v1/voices</code> per ottenere
      l'elenco corrente delle voci supportate. La voce predefinita è
      <code>en-US_MichaelV3Voice</code>. Per ulteriori informazioni, vedi [Lingue e voci](/docs/services/text-to-speech-data?topic=text-to-speech-data-voices).
    </td>
  </tr>
  <tr>
    <td><code>customization_id</code><br/><em>Facoltativo</em></td>
    <td style="text-align:center">Query</td>
    <td style="text-align:center">Stringa</td>
    <td>
      Specifica un GUID (globally unique identifier) per un modello vocale
      personalizzato che deve essere utilizzato per la sintesi. È garantito che un modello
      vocale personalizzato specificato funzioni solo se corrisponde alla lingua
      della voce utilizzata per la sintesi. Se includi un ID
      di personalizzazione, devi effettuare la richiesta con le credenziali per l'istanza del servizio
      che gestisce il modello personalizzato. Ometti il parametro per utilizzare la voce specificata
      senza alcuna personalizzazione. Per ulteriori informazioni, vedi
      [Informazioni sulla personalizzazione](/docs/services/text-to-speech-data?topic=text-to-speech-data-customIntro).
    </td>
  </tr>
</table>

Puoi anche utilizzare l'intestazione della richiesta `X-Watson-Metadata`, che associa un ID cliente ai dati che vengono passati con una richiesta. Per ulteriori informazioni, vedi [Sicurezza delle informazioni](/docs/services/text-to-speech-data?topic=text-to-speech-data-information-security).

Se specifichi un parametro di query o un campo JSON non valido come parte dell'input al metodo `/v1/synthesize`, il servizio restituisce un'intestazione di risposta `Warnings` che descrive ed elenca ogni argomento non valido. La richiesta riesce nonostante le avvertenze.
{: note}

## Specifica del testo di input
{: #input}

Entrambi i metodi `GET` e `POST /v1/synthesize` accettano il testo di input semplice o il testo annotato con SSML. Le due versioni differiscono principalmente nel modo in cui specifichi il testo che deve essere sintetizzato:

-   Il metodo `GET /v1/synthesize` accetta il testo di input specificato dal parametro di query `text`. Specifica l'input come testo semplice o come SSML, in entrambi i casi con codifica URL.
-   Il metodo `POST /v1/synthesize` accetta il testo di input nel corpo della richiesta. Specifica l'input con il seguente costrutto JSON semplice che incapsula il testo normale o SSML. Devi anche specificare un valore di `application/json` per l'intestazione `Content-Type`.

    ```javascript
    {
      "text": ""
    }
    ```
    {: codeblock}

Sebbene i metodi `GET` e `POST` offrano funzionalità equivalenti, è sempre più sicuro passare il testo di input al servizio con il metodo `POST`. Una richiesta `POST` passa l'input nel corpo della richiesta, mentre una richiesta `GET` espone i dati nell'URL.

## Specifica dell'input SSML
{: #ssml-http}

SSML (Speech Synthesis Markup Language) è un linguaggio di markup basato su XML progettato per fornire annotazioni di testo per le applicazioni di sintesi vocale come il servizio {{site.data.keyword.texttospeechshort}}. Puoi utilizzare gli elementi SSML e i loro attributi per ottenere un maggiore controllo sulla sintesi e sull'output audio risultante.

Per ulteriori informazioni sull'utilizzo di SSML per annotare il testo di input, vedi [Utilizzo di SSML](/docs/services/text-to-speech-data?topic=text-to-speech-data-ssml). La documentazione archivia gli elementi SSML e gli attributi supportati dal servizio.

## Escape dei caratteri di controllo XML
{: #escape}

Dal momento che puoi inoltrare il testo di input che include annotazioni SSML basate su XML, il servizio convalida tutto l'input per garantire che qualsiasi SSML sia corretto e ben formato. Pertanto, devi eseguire l'escape di tutti i caratteri di controllo XML presenti nel testo di input, a prescindere che l'input includa o meno SSML. Utilizza le stringhe di escape o le codifiche di caratteri equivalenti della Tabella 2 anziché i caratteri indicati.

<table style="width:80%">
  <caption>Tabella 2. Escape dei caratteri di controllo XML</caption>
  <tr>
    <th style="text-align:center; vertical-align:bottom; width:40%">Carattere</th>
    <th style="text-align:center; vertical-align:bottom; width:30%">Stringhe di escape</th>
    <th style="text-align:center; vertical-align:bottom; width:30%">Codifica dei caratteri</th>
  </tr>
  <tr>
    <td style="text-align:center"><code>&quot;</code><br/>(virgolette)</td>
    <td style="text-align:center"><code>&amp;quot;</code></td>
    <td style="text-align:center"><code>&amp;#34;</code></td>
  </tr>
  <tr>
    <td style="text-align:center"><code>'</code><br/>(apostrofo o virgoletta singola)</td>
    <td style="text-align:center"><code>&amp;apos;</code></td>
    <td style="text-align:center"><code>&amp;#39;</code></td>
  </tr>
  <tr>
    <td style="text-align:center"><code>&amp;</code><br/>(e commerciale)</td>
    <td style="text-align:center"><code>&amp;amp;</code></td>
    <td style="text-align:center"><code>&amp;#38;</code></td>
  </tr>
  <tr>
    <td style="text-align:center"><code>&lt;</code><br/>(parentesi angolare sinistra)</td>
    <td style="text-align:center"><code>&amp;lt;</code></td>
    <td style="text-align:center"><code>&amp;#60;</code></td>
  </tr>
  <tr>
    <td style="text-align:center"><code>&gt;</code><br/>(parentesi angolare destra)</td>
    <td style="text-align:center"><code>&amp;gt;</code></td>
    <td style="text-align:center"><code>&amp;#62;</code></td>
  </tr>
</table>

Per ulteriori informazioni su come il servizio convalida il testo di input, vedi [Convalida SSML](/docs/services/text-to-speech-data?topic=text-to-speech-data-ssml#errors).

## Esempi di testo di input
{: #httpExamples}

I seguenti esempi mostrano come specificare il testo di input con entrambi i metodi dell'interfaccia HTTP. Mostrano anche come eseguire l'escape dei caratteri di controllo XML. Gli esempi includono interruzioni di riga per la leggibilità. *Non* includere le interruzioni di riga nell'input effettivo.

### Input di esempio con una richiesta GET
{: #getExamples}

I seguenti esempi passano l'input codificato in URL con il parametro di query `text` del metodo `GET /v1/synthesize`:

-   Input di testo semplice:

    ```
    text=This&20is&20the&20first&20sentence&20of&20the&20paragraph.&20Here
    &20is&20another&20sentence.&20Finally,&20this&20is&20the&20last&20sentence.
    ```
    {: codeblock}

-   Input SSML:

    ```
    text=%22%3Cp%3E%3Cs%3EThis%20is%20the%20first%20sentence%20of%20the%20%3C
    break%20time=%225s%22/%3E%20paragraph.%3C/s%3E%3Cs%3EHere%20is%20another
    %20sentence.%3C/s%3E%3Cs%3EFinally,%20this%20is%20the%20last%20sentence.
    %3C/s%3E%3C/p%3E%22
    ```
    {: codeblock}

### Input di esempio con una richiesta POST
{: #postExamples}

I seguenti esempi passano l'input nel corpo del metodo `POST /v1/synthesize`:

-   Input di testo semplice:

    ```javascript
    {
      "text": "This is the first sentence of the paragraph. Here is another
        sentence. Finally, this is the last sentence."
    }
    ```
    {: codeblock}

-   Input SSML:

    ```javascript
    {
      "text": "<p><s>This is the first sentence of the <break time=\"5s\"/>
        paragraph.</s><s>Here is another sentence.</s><s>Finally, this is
        the last sentence.</s></p>"
    }
    ```
    {: codeblock}

### Input di esempio con i caratteri di controllo XML
{: #xmlExamples}

Il seguente esempio invia una frase al metodo `POST /v1/synthesize`. L'esempio esegue correttamente l'escape dei caratteri XML incorporati.

```
"What have I learned?" he asked. "Everything!"
```
{: codeblock}

```javascript
{
  "text": "&quot;What have I learned?&quot; he asked. &quot;Everything!&quot;"
    }
```
{: codeblock}
