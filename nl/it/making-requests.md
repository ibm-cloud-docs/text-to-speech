---

copyright:
  years: 2018, 2019
lastupdated: "2019-06-27"

subcollection: text-to-speech-data

---

{:shortdesc: .shortdesc}
{:external: target="_blank" .external}
{:tip: .tip}
{:note: .note}
{:deprecated: .deprecated}
{:important: .important}
{:pre: .pre}
{:codeblock: .codeblock}
{:screen: .screen}
{:javascript: .ph data-hd-programlang='javascript'}
{:java: .ph data-hd-programlang='java'}
{:python: .ph data-hd-programlang='python'}
{:swift: .ph data-hd-programlang='swift'}

# Effettuare le richieste al servizio
{: #making-requests}

Per effettuare richieste autenticate a {{site.data.keyword.texttospeechdatafull}} for {{site.data.keyword.icp4dfull}}, esegui il provisioning di un'istanza del servizio e ottieni le credenziali. Utilizza un URL diverso per le interfacce HTTP e WebSocket del servizio. Se utilizzi un certificato autofirmato, devi disabilitare la verifica SSL per le richieste al servizio.
{: shortdesc}

## Provisioning di un'istanza e ottenimento delle credenziali
{: #making-requests-provisioning}

Prima di utilizzare il servizio {{site.data.keyword.texttospeechshort}}, devi eseguire il provisioning di un'istanza del servizio e ottenere le tue credenziali. Per ulteriori informazioni, vedi [Prima di cominciare](/docs/services/text-to-speech-data?topic=text-to-speech-data-gettingStarted#before-you-begin). Nell'ultimo passo della procedura, copia `{token}` e `{URL}` per la tua istanza del servizio:

-   `{token}` fornisce il tuo token di accesso per l'autenticazione al servizio. Puoi utilizzare il token di accesso visualizzato nel client web {{site.data.keyword.icp4dfull_notm}}. Tuttavia, in un ambiente di produzione, utilizza un token che generi in modo programmatico per la tua istanza del servizio. Per ulteriori informazioni e per degli esempi, vedi *Autenticazione* nel [Riferimento API](https://{DomainName}/apidocs/text-to-speech-data#authentication){: external}.

    Esegui l'autenticazione con il servizio {{site.data.keyword.texttospeechshort}} passando il tuo token di accesso con ogni richiesta. {{site.data.keyword.texttospeechshort}} for {{site.data.keyword.icp4dfull_notm}} è una soluzione cloud a più tenant. Le tue credenziali forniscono l'accesso solo ai tuoi dati ed essi sono isolati dagli altri utenti.
-   `{URL}` fornisce l'endpoint di base che utilizzi per richiamare i metodi del servizio.

L'URL contiene i seguenti componenti:

```
https://{icp4d_cluster_host}{:port}/text-to-speech/{release}/instances/{instance_id}/api
```
{: codeblock}

I valori di variabile in `{}` (parentesi graffe) forniscono le seguenti informazioni:

-   `{icp4d_cluster_host}` è il nome o l'indirizzo IP dell'host su cui viene distribuito il tuo cluster {{site.data.keyword.icp4dfull_notm}}.
-   `{:port}` è il numero di porta in cui il servizio è in ascolto per le richieste sull'host specificato. Devi anteporre al numero di porta un simbolo `:` (due punti).
-   `{release}` è il nome della release che è stato specificato quando è stato installato il grafico Helm.
-   `{instance_id}` è l'identificativo della tua istanza del servizio.

Le parentesi graffe indicano delle stringhe di variabile che devi sostituire con valori letterali. Non includere le parentesi graffe nelle chiamate reali al servizio.
{: note}

## Effettuare una richiesta HTTP autenticata
{: #httpRequest}

Il servizio {{site.data.keyword.texttospeechshort}} offre un'[interfaccia HTTP](/docs/services/text-to-speech-data?topic=text-to-speech-data-usingHTTP) che fornisce l'accesso a tutte le funzionalità del servizio, incluse le interfacce di personalizzazione. L'interfaccia HTTP accetta le richieste sul protocollo sicuro HTTP, che a sua volta si basa sul protocollo SSL (Secure Sockets Layer) (o TLS (Transport Layer Security)). Tutti gli URL per le richieste all'interfaccia HTTP iniziano con la specifica del protocollo `https`.

Gli esempi in questa documentazione utilizzano il comando `curl` per richiamare l'interfaccia HTTP del servizio. Per ulteriori informazioni, vedi [Utilizzo degli esempi curl](/docs/services/text-to-speech-data?topic=text-to-speech-data-gettingStarted#getting-started-curl). Il formato di base di una richiesta HTTP con `curl` include i seguenti componenti:

```bash
curl -X {http_method}
--header "Authorization: Bearer {token}"
"https://{icp4d_cluster_host}{:port}/text-to-speech/{release}/instances/{instance_id}/api/v1/{method}"
```
{: pre}

I valori di variabile nelle parentesi graffe forniscono le seguenti informazioni:

-   `{http_method}` specifica il metodo di richiesta HTTP ad esempio: `POST`, `PUT`, `GET` o `DELETE`. Il metodo di richiesta è obbligatorio con `curl` per tutti i tipi diversi da `GET`.
-   `{token}` fornisce il token di accesso della tua istanza del servizio. Devi utilizzare il token di accesso per effettuare una richiesta sicura al servizio.
-   `{method}` è il metodo del servizio che stai richiamando. Ad esempio, utilizza il metodo `synthesize` per effettuare una richiesta HTTP al servizio.

I valori di variabile rimanenti forniscono le informazioni che sono state descritte in precedenza. Molti metodi hanno nomi più lunghi e includono dei parametri di percorso che devi specificare come parte della richiesta. La maggior parte degli esempi includono anche intestazioni di richiesta, parametri di query e altri valori.

Gli esempi mostrano l'URL per le chiamate all'interfaccia HTTP come `{url}/v1/{method}`. Sostituisci `{url}` con i valori appena descritti.
{: note}

## Effettuare una richiesta WebSocket autenticata
{: #websocketRequest}

Il servizio {{site.data.keyword.texttospeechshort}} offre un'[interfaccia WebSocket](/docs/services/text-to-speech-data?topic=text-to-speech-data-usingWebSocket) che fornisce solo sintesi vocali. Il servizio accetta richieste sul protocollo sicuro WebSocket, che a sua volta si basa sul protocollo SSL (Secure Sockets Layer) (o TLS (Transport Layer Security)). Tutti gli URL per le richieste all'interfaccia WebSocket iniziano con la specifica del protocollo `wss`.

Puoi richiamare l'interfaccia WebSocket solo dal codice dell'applicazione. Non puoi richiamare l'interfaccia WebSocket dalla riga di comando. Stabilisci una connessione WebSocket al servizio al seguente endpoint.

```
wss://{icp4d_cluster_host}{:port}/text-to-speech/{release}/instances/{instance_id}/api/v1/synthesize
```
{: codeblock}

I valori di variabile forniscono le informazioni che sono state descritte in precedenza. Passa il tuo token di accesso tramite il parametro di query `access_token` del metodo.

Gli esempi mostrano l'URL per le chiamate all'interfaccia WebSocket come `{ws_url}/v1/synthesize`. Sostituisci `{ws_url}` con i valori appena descritti.
{: note}

## Disabilitazione della verifica SSL
{: #SSLverification}

Tutti i servizi Watson utilizzano SSL (o TLS) per le connessioni e le comunicazioni sicure tra il client e il server. La connessione è verificata tramite l'archivio di certificati locale per garantire l'autenticazione, l'integrità e la riservatezza.

{{site.data.keyword.icp4dfull_notm}} installa un certificato autofirmato. Questo certificato non può essere verificato correttamente per impostazione predefinita. Puoi effettuare una delle seguenti azioni per eseguire la connessione correttamente a un'istanza del servizio:

-   Aggiungi il certificato autofirmato al truststore per il tuo agent utente.

    Ad esempio, per effettuare richieste sicure con `curl`, aggiungi il certificato al truststore per `curl`. Per effettuare richieste dal tuo browser, aggiungi il certificato al truststore per il browser.
-   Disabilita la verifica SSL.

    La disabilitazione della verifica SSL compromette la sicurezza della connessione e dei dati. È fortemente sconsigliato. Disabilita SSL solo se assolutamente necessario e riabilita SSL il prima possibile.
    {: important}

    -   Per disabilitare la verifica SSL per una richiesta `curl`, utilizza l'opzione `--insecure` (`-k`) con la richiesta. Questa opzione indirizza il comando ignorando la verifica dei certificati SSL dello strumento.
    -   Per disabilitare la verifica SSL per una richiesta WebSocket, utilizza l'approccio appropriato per la tua libreria client o utilizza uno degli SDK {{site.data.keyword.ibmwatson}} {{site.data.keyword.texttospeechshort}}.

Per ulteriori informazioni sulla disabilitazione della verifica SSL per le chiamate al servizio, vedi *Disabilitazione della verifica SSL* nel [Riferimento API](https://{DomainName}/apidocs/text-to-speech-data#disabling-ssl){: external}. Le informazioni includono degli esempi per `curl` e per tutti gli SDK.
