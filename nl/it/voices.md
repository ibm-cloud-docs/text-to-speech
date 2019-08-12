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

# Lingue e voci
{: #voices}

{{site.data.keyword.texttospeechdatafull}} for {{site.data.keyword.icp4dfull}} supporta varie lingue, voci e dialetti. Il servizio offre almeno una voce femminile per ogni lingua. Per alcune lingue il servizio offre più voci, incluse sia voci maschili che femminili. Ogni voce usa cadenza e intonazione appropriate per il suo dialetto.
{: shortdesc}

## Lingue e voci supportate
{: #languageVoices}

La Tabella 1 elenca le voci disponibili per ogni lingua e dialetto, inclusi il loro tipo e sesso. Tutte le voci sono [voci neurali](#neuralVoices). (Una versione neurale del giapponese non è ancora disponibile). Se ometti il parametro `voice` facoltativo, il servizio utilizza la voce `en-US_MichaelV3Voice` per impostazione predefinita. 

<table style="width:100%">
  <caption>Tabella 1. Lingue e voci supportate</caption>
  <tr>
    <th style="text-align:left">Lingua</th>
    <th style="text-align:center">Voce</th>
    <th style="text-align:center">Sesso</th>
  </tr>
  <tr>
    <td style="text-align:left">Portoghese brasiliano</td>
    <td style="text-align:center"><code>pt-BR_IsabelaV3Voice</code></td>
    <td style="text-align:center">Femminile</td>
  </tr>
  <tr>
    <td style="text-align:left">Spagnolo castigliano</td>
    <td style="text-align:center"><code>es-ES_EnriqueV3Voice</code></td>
    <td style="text-align:center">Maschile</td>
  </tr>
  <tr>
    <td></td>
    <td style="text-align:center"><code>es-ES_LauraV3Voice</code></td>
    <td style="text-align:center">Femminile</td>
  </tr>
  <tr>
    <td style="text-align:left">Francese</td>
    <td style="text-align:center"><code>fr-FR_ReneeV3Voice</code></td>
    <td style="text-align:center">Femminile</td>
  </tr>
  <tr>
    <td style="text-align:left">Tedesco</td>
    <td style="text-align:center"><code>de-DE_BirgitV3Voice</code></td>
    <td style="text-align:center">Femminile</td>
  </tr>
  <tr>
    <td></td>
    <td style="text-align:center"><code>de-DE_DieterV3Voice</code></td>
    <td style="text-align:center">Maschile</td>
  </tr>
  <tr>
    <td style="text-align:left">Italiano</td>
    <td style="text-align:center"><code>it-IT_FrancescaV3Voice</code></td>
    <td style="text-align:center">Femminile</td>
  </tr>
  <tr>
    <td style="text-align:left">Spagnolo latino americano</td>
    <td style="text-align:center"><code>es-LA_SofiaV3Voice</code></td>
    <td style="text-align:center">Femminile</td>
  </tr>
  <tr>
    <td style="text-align:left">Spagnolo nord americano</td>
    <td style="text-align:center"><code>es-US_SofiaV3Voice</code></td>
    <td style="text-align:center">Femminile</td>
  </tr>
  <tr>
    <td style="text-align:left">Inglese britannico</td>
    <td style="text-align:center"><code>en-GB_KateV3Voice</code></td>
    <td style="text-align:center">Femminile</td>
  </tr>
  <tr>
    <td style="text-align:left">Inglese americano</td>
    <td style="text-align:center"><code>en-US_AllisonV3Voice</code></td>
    <td style="text-align:center">Femminile</td>
  </tr>
  <tr>
    <td></td>
    <td style="text-align:center"><code>en-US_LisaV3Voice</code></td>
    <td style="text-align:center">Femminile</td>
  </tr>
  <tr>
    <td></td>
    <td style="text-align:center"><code>en-US_MichaelV3Voice</code></td>
    <td style="text-align:center">Maschile</td>
  </tr>
</table>

Le voci `es-LA_SofiaV3Voice` e `es-US_SofiaV3Voice` sono essenzialmente la stessa voce. La differenza più significativa riguarda il modo in cui le due voci interpretano $ (segno del dollaro). La versione latino americana utilizza il termine *pesos*, mentre la versione nord americana utilizza il termine *d&oacute;lares*. Tra le due voci potrebbero esistere anche altre piccole differenze.
{: note}

### Voci neurali
{: #neuralVoices}

La tecnologia vocale neurale utilizza molteplici DNN (Deep Neural Network) per prevedere le caratteristiche acustiche (spettrali) del discorso. Le DNN sono addestrate sulla lingua naturale umana e generano l'audio risultante dalle caratteristiche acustiche previste. Durante la sintesi, le DNN prevedono la durata tonale e fonemica (prosodia), la struttura spettrale e la forma d'onda del discorso. Le voci neurali producono un discorso nitido e chiaro, con una qualità audio dal suono molto naturale e fluido.

Per ulteriori informazioni sulla tecnologia vocale neurale del servizio, vedi

-   Il post del blog [IBM Watson Text to Speech: Neural Voices Generally Available](https://medium.com/ibm-watson/ibm-watson-text-to-speech-neural-voices-added-to-service-e562106ff9c7){: external}
-   L'articolo di ricerca [High quality, lightweight and adaptable Text to Speech using LPCNet](https://arxiv.org/abs/1905.00590){: external}

### Personalizzazione della voce
{: #customizeVoice}

Quando sintetizzi il testo, il servizio applica le regole di pronuncia specifiche della lingua per convertire l'ortografia ordinaria di ciascuna parola in un'ortografia fonetica. Le regole di pronuncia del servizio funzionano bene per le parole comuni, ma possono fornire risultati imperfetti per le parole inusuali, ad esempio i termini con origini straniere, i nomi personali e le abbreviazioni o gli acronimi.

Se il dizionario della tua applicazione include parole di questo tipo, puoi utilizzare l'interfaccia personalizzata per specificare il modo in cui il servizio le pronuncia. Per ulteriori informazioni, vedi
      [Informazioni sulla personalizzazione](/docs/services/text-to-speech-data?topic=text-to-speech-data-customIntro).

Crei un modello vocale personalizzato per una specifica lingua, non per una specifica voce. Quindi un modello personalizzato può essere utilizzato con qualsiasi voce per la propria lingua specificata.

## Specifica di una voce
{: #specifyVoice}

Entrambi i metodi HTTP `GET` e `POST /v1/synthesize`, come pure il metodo WebSocket `/v1/synthesize`, accettano un parametro di query `voice` facoltativo per specificare la voce per l'audio sintetizzato. Per ulteriori informazioni, vedi [L'interfaccia HTTP](/docs/services/text-to-speech-data?topic=text-to-speech-data-usingHTTP) e [L'interfaccia WebSocket](/docs/services/text-to-speech-data?topic=text-to-speech-data-usingWebSocket).

Il servizio basa la sua comprensione della lingua per il testo di input sulla voce specificata. Assicurati di specificare una voce che corrisponda alla lingua del testo di input. Ad esempio, se specifichi la voce in francese (`fr-FR_ReneeV3Voice`), il servizio presuppone che il testo di input sia scritto in francese. Se passi del testo che non è scritto nella lingua della voce (ad esempio, testo in inglese per la voce in francese), il servizio potrebbe non produrre risultati significativi.

## Elenco di tutte le voci disponibili
{: #listVoices}

Il metodo `GET /v1/voices` elenca le informazioni su tutte le voci disponibili. Non accetta argomenti e restituisce un array JSON denominato `voices`. L'array include un oggetto separato per ogni voce.

```javascript
{
  "voices": [
    {
      "name": "en-US_LisaV3Voice",
      "language": "en-US",
      "gender": "female",
      "url": "{url}/v1/voices/en-US_LisaV3Voice",
      "description": "Lisa: American English female voice.",
      "customizable": true,
      "supported_features": {
        "voice_transformation": false,
        "custom_pronunciation": true
      }
    },
    . . .
  ]
}
```
{: codeblock}

I campi degli oggetti della voce forniscono le seguenti informazioni:

-   `name` è un identificativo per la voce (ad esempio, `en-US_LisaV3Voice`). Specifica questo valore per il parametro `voice` del metodo `/v1/synthesize`.
-   `language` specifica la lingua e la regione della voce (ad esempio, `en-US`).
-   `gender` identifica la voce come maschile (`male`) o femminile (`female`).
-   `url` identifica l'URL per la voce.
-   `description` fornisce una breve descrizione della voce.
-   `customizable` è un valore booleano che indica se la voce può essere personalizzata con l'interfaccia di personalizzazione del servizio. (Questo campo, che fornisce le stesse informazioni del campo `custom_pronunciation`, viene conservato per una compatibilità con le versioni precedenti.)
-   `supported_features` descrive le funzioni aggiuntive del servizio supportate dalla voce:
    -   `voice_transformation` è un valore booleano che indica se la voce può essere trasformata utilizzando l'elemento `<voice-transformation>` SSML. Poiché la trasformazione della voce non è supportata per le voci neurali, il campo è sempre `false`.
    -   `custom_pronunciation` è un valore booleano che indica se la voce può essere personalizzata con l'interfaccia di personalizzazione del servizio.

## Elenco di una voce specifica
{: #listVoice}

Il metodo `GET /v1/voices/{voice}` elenca le informazioni su una voce specifica. Accetta due parametri.

<table>
  <caption>Tabella 2. Parametri del metodo <code>voices</code></caption>
  <tr>
    <th style="text-align:left; width:18%">Parametro</th>
    <th style="text-align:center; width:12%">Tipo</th>
    <th style="text-align:center; width:12%">Tipo di dati</th>
    <th style="text-align:left">Descrizione</th>
  </tr>
  <tr>
    <td><code>voice</code><br/><em>Obbligatorio</em></td>
    <td style="text-align:center">Percorso</td>
    <td style="text-align:center">Stringa</td>
    <td>
      Identifica la voce per cui devono essere restituite le informazioni. Specifica
      una voce in base al suo nome (ad esempio, <code>en-US_LisaV3Voice</code>).
    </td>
  </tr>
  <tr>
    <td><code>customization_id</code><br/><em>Facoltativo</em></td>
    <td style="text-align:center">Query</td>
    <td style="text-align:center">Stringa</td>
    <td>
      Fornisce il GUID (globally unique identifier) di un modello vocale
      personalizzato definito per la lingua della voce specificata. Se includi un ID
      di personalizzazione, devi effettuare la richiesta con le credenziali per l'istanza del servizio
      che gestisce il modello personalizzato.
    </td>
  </tr>
</table>

Se ometti il parametro `customization_id`, il metodo restituisce un output JSON per la voce specificata che è identico alle informazioni restituite per una voce dal metodo `GET /v1/voices`. Se specifichi un `customization_id`, l'output include un campo `customization` che fornisce le informazioni sul modello vocale personalizzato.

```javascript
{
  "name": "en-US_LisaV3Voice",
  "language": "en-US",
  "gender": "female",
  "url": "{url}/v1/voices/en-US_LisaV3Voice",
  "description": "Lisa: American English female voice.",
      "customizable": true,
      "supported_features": {
    "voice_transformation": false,
    "custom_pronunciation": true
  },
  "customization": {
    "customization_id": "64f4807f-a5f1-5867-924f-7bba1a84fe97",
    "owner": "297cfd08-330a-22ba-93ce-1a73f454dd98",
    "created": "2017-09-16T17:12:31.743Z",
    "name": "curl Test",
    "language": "en-US",
    "description": "Customization test via curl",
    "last_modified": "2017-09-16T17:12:31.743Z"
  }
}
```
{: codeblock}

Gli attributi del campo aggiuntivo `customization` forniscono le informazioni come il GUID, il nome, la lingua e la descrizione del modello vocale personalizzato. Mostrano anche le credenziali del proprietario del modello, la data e l'ora in cui è stato creato il modello e la data e l'ora della sua ultima modifica. 
