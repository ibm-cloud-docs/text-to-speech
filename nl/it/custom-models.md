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

# Creazione e gestione di modelli vocali personalizzati
{: #customModels}

Il primo passo per utilizzare un qualsiasi modello personalizzato è crearlo. Una volta creato, puoi gestire il modello eseguendo query o aggiornando i suoi metadati e le sue voci e, infine, eliminandolo quando non più necessario. Prima di iniziare, esamina le seguenti informazioni generali sull'utilizzo dei modelli personalizzati.
{: shortdesc}

## Note sull'utilizzo
{: #customGuidelines}

Considera le seguenti linee guida quando lavori con l'interfaccia di personalizzazione.

### Proprietà di modelli vocali personalizzati
{: #customOwner}

Un modello vocale personalizzato è di proprietà dell'istanza del servizio {{site.data.keyword.texttospeechshort}} di cui vengono utilizzate le credenziali per crearlo. Per lavorare con il modello personalizzato devi utilizzare le credenziali per tale istanza del servizio con i metodi dell'interfaccia di personalizzazione.

Tutte le credenziali ottenute per la stessa istanza del servizio {{site.data.keyword.texttospeechshort}} condividono l'accesso a tutti i modelli personalizzati creati per tale istanza. Per limitare l'accesso a un modello personalizzato, crea un'istanza del servizio separata e utilizza solo le credenziali di tale istanza per creare e utilizzare il modello. Le credenziali per altre istanze del servizio non possono influire sul modello personalizzato.

Un vantaggio della condivisione della proprietà tra le credenziali è che puoi annullare un insieme di credenziali, ad esempio, se vengono compromesse. Puoi quindi creare nuove credenziali per la stessa istanza del servizio e mantenere comunque la proprietà e l'accesso ai modelli personalizzati creati con le credenziali originali.

### Sicurezza delle informazioni
{: #customSecurity}

Il servizio ti consente di associare un ID cliente ai dati che vengono aggiunti o aggiornati per i modelli vocali personalizzati. Puoi associare un ID cliente a parole personalizzate passando l'intestazione `X-Watson-Metadata` con i seguenti metodi:

-   `POST /v1/customizations/{customization_id}`
-   `POST /v1/customizations/{customization_id}/words`
-   `PUT /v1/customizations/{customization_id}/words/{word}`

Se necessario, puoi quindi eliminare i dati associati all'ID cliente utilizzando il metodo `DELETE /v1/user_data`. Per ulteriori informazioni, vedi [Sicurezza delle informazioni](/docs/services/text-to-speech-data?topic=text-to-speech-data-information-security).

## Creazione di un modello personalizzato
{: #cuModelsCreate}

Per creare un nuovo modello personalizzato, utilizza il metodo `POST /v1/customizations`. Un nuovo modello è sempre vuoto quando lo crei per la prima volta. Devi utilizzare altri metodi per popolarlo con coppie di parole/traduzioni. Il nuovo modello personalizzato è di proprietà dell'istanza del servizio di cui vengono utilizzate le credenziali per crearlo. Per ulteriori informazioni, vedi [Proprietà di modelli vocali personalizzati](#customOwner).

Passa i seguenti attributi come oggetto JSON con il corpo della richiesta.

<table>
  <caption>Tabella 1. Parametri del metodo
    <code>POST /v1/customizations</code></caption>
  <tr>
    <th style="text-align:left; width:18%">Parametro</th>
    <th style="text-align:center; width:12%">Tipo di dati</th>
    <th style="text-align:left">Descrizione</th>
  </tr>
  <tr>
    <td><code>name</code><br/><em>Obbligatorio</em></td>
    <td style="text-align:center">Stringa</td>
    <td>
      Un nome definito dall'utente per il nuovo modello personalizzato. Il nome è utilizzato
      per etichettare il modello per una facile identificazione. Il nome deve essere univoco
      tra tutti i modelli personalizzati di tua proprietà.
    </td>
  </tr>
  <tr>
    <td><code>language</code><br/><em>Facoltativo</em></td>
    <td style="text-align:center">Stringa</td>
    <td>
      Un identificativo per la lingua del modello personalizzato. Il valore
      predefinito è <code>en-US</code> per l'inglese americano. Il modello personalizzato
      può essere utilizzato con qualsiasi voce disponibile nella lingua specificata.
    </td>
  </tr>
  <tr>
    <td><code>description</code><br/><em>Facoltativo</em></td>
    <td style="text-align:center">Stringa</td>
    <td>
      Una descrizione del nuovo modello. Sebbene sia facoltativa, è
      consigliabile fornire una descrizione.
    </td>
  </tr>
</table>

Il seguente comando `curl` di esempio crea un nuovo modello personalizzato denominato `curl Test`. L'intestazione `Content-Type` identifica il tipo di input come `application/json`.

```bash
curl -X POST
--header "Authorization: Bearer {token}"
--header "Content-Type: application/json"
--data "{\"name\":\"curl Test\", \"language\":\"en-US\", \"description\":\"Customization test via curl\"}"
"{url}/v1/customizations"
```
{: pre}

Il metodo restituisce un oggetto JSON che contiene un GUID (globally unique identifier) per il nuovo modello. Il GUID viene utilizzato come parametro `customization_id` nelle chiamate per accedere al modello, ad esempio per l'esecuzione di query, la modifica e l'utilizzo del modello e delle sue parole.

```javascript
{
  "customization_id": "64f4807f-a5f1-5867-924f-7bba1a84fe97"
}
```
{: codeblock}

## Esecuzione di query di un modello personalizzato
{: #cuModelsQuery}

Per eseguire la query sulle informazioni relative a un modello personalizzato esistente, utilizza il metodo `GET /v1/customizations/{customization_id}`. Questo è il modo più diretto per vedere tutte le informazioni su un modello, sia i suoi metadati che le coppie di parole/traduzioni che contiene.

```bash
curl -X GET
--header "Authorization: Bearer {token}"
"{url}/v1/customizations/{customization_id}"
```
{: pre}

Il metodo restituisce i suoi risultati come oggetto JSON del seguente formato:

```javascript
{
  "customization_id": "64f4807f-a5f1-5867-924f-7bba1a84fe97",
  "owner": "297cfd08-330a-22ba-93ce-1a73f454dd98",
  "created": "2016-07-15T18:12:31.743Z",
  "name": "curl Test",
  "language": "en-US",
  "description": "Customization test via curl",
  "last_modified": "2016-07-15T18:12:31.743Z",
  "words": []
}
```
{: codeblock}

Oltre alle informazioni immesse al momento della creazione del modello, l'output include le credenziali del proprietario del modello, la lingua e le ore di creazione e l'ultima modifica del modello. Poiché il modello non è stato modificato dalla sua creazione, le due ore nell'esempio sono uguali.

L'output include anche un array `words` che elenca le voci personalizzate del modello. Poiché il modello deve ancora essere aggiornato, l'array nell'esempio è vuoto.

## Esecuzione di query di tutti i modelli personalizzati
{: #cuModelsQueryAll}

Per visualizzare informazioni su tutti i modelli personalizzati di tua proprietà, utilizza il metodo `GET /v1/customizations`:

```bash
curl -X GET
--header "Authorization: Bearer {token}"
"{url}/v1/customizations"
```
{: pre}

Il metodo restituisce un array JSON che include un oggetto per ciascun modello personalizzato di proprietà del richiedente. Le credenziali del proprietario sono mostrate nel campo `owner`.

```javascript
{
  "customizations": [
    {
      "customization_id": "64f4807f-a5f1-5867-924f-7bba1a84fe97",
      "owner": "297cfd08-330a-22ba-93ce-1a73f454dd98",
      "created": "2016-07-15T19:15:17.926Z",
      "name": "curl Test",
      "language": "en-US",
      "description": "Customization test via curl",
      "last_modified": "2016-07-15T19:15:17.926Z"
    },
    {
      "customization_id": "63f5807f-a4f2-5766-914e-7abb1a84fe97",
      "owner": "297cfd08-330a-22ba-93ce-1a73f454dd98",
      "created": "2016-07-15T18:12:31.743Z",
      "name": "curl Test Two",
      "language": "en-US",
      "description": "Second customization test via curl",
      "last_modified": "2016-07-15T18:23:50.912Z"
    }
  ]
}
```
{: codeblock}

Le ore nei campi `created` e `last_modified` per il primo modello sono le stesse perché non è stato ancora aggiornato. Le ore per il secondo modello sono diverse, a indicare che è stato modificato dalla sua creazione iniziale. Le informazioni non includono le voci personalizzate definite per i modelli.

## Aggiornamento di un modello personalizzato
{: #cuModelsUpdate}

Per aggiornare le informazioni relative a un modello personalizzato, utilizza il metodo `POST /v1/customizations/{customization_id}`. Specifica gli aggiornamenti come oggetto JSON. Oltre a modificarne il nome e la descrizione, puoi utilizzare questo metodo anche per aggiungere o aggiornare coppie di parole/traduzioni nel modello. Non puoi modificare la lingua di un modello una volta creato.

Il seguente esempio aggiorna il nome e la descrizione di un modello personalizzato. Viene inviato un array JSON vuoto con il parametro `words` per indicare che le voci del modello devono rimanere invariate.

```bash
curl -X POST
--header "Authorization: Bearer {token}"
--header "Content-Type: application/json"
--data "{\"name\":\"curl Test Update\", \"description\":\"Customization test update via curl\", \"words\":[]}"
"{url}/v1/customizations/{customization_id}"
```
{: pre}

Per informazioni sull'aggiornamento delle parole in un modello, vedi [Aggiunta di più parole a un modello personalizzato](/docs/services/text-to-speech-data?topic=text-to-speech-data-customWords#cuWordsAdd).

## Eliminazione di un modello personalizzato
{: #cuModelsDelete}

Per eliminare un modello personalizzato che non ti serve più, utilizza il metodo `DELETE /v1/customizations/{customization_id}`. Utilizza questo metodo solo se sei certo di non aver più bisogno del modello, poiché l'eliminazione è permanente.

```bash
curl -X DELETE
--header "Authorization: Bearer {token}"
"{url}/v1/customizations/{customization_id}"
```
{: pre}
