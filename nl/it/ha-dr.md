---

copyright:
  years: 2019
lastupdated: "2019-03-19"

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

# Alta disponibilità e ripristino di emergenza
{: #ha-dr}

Il servizio {{site.data.keyword.texttospeechfull}} è altamente disponibile all'interno di qualsiasi ubicazione {{site.data.keyword.cloud_notm}} (ad esempio, Dallas o Washington, DC). Tuttavia, il ripristino da potenziali perdite di dati che interessano un'intera ubicazione richiede pianificazione e preparazione.
{: shortdesc}

Sei responsabile della comprensione della configurazione, della personalizzazione e dell'utilizzo del servizio. Sei anche responsabile di essere pronto a ricreare un'istanza del servizio in una nuova ubicazione e ripristinare i tuoi dati in qualsiasi ubicazione.

## Alta disponibilità
{: #high-availability}

Il servizio {{site.data.keyword.texttospeechshort}} supporta l'alta disponibilità senza alcun singolo punto di guasto. Il servizio raggiunge l'alta disponibilità in modo automatico e trasparente mediante la funzione MZR (multi-zone region) fornita da {{site.data.keyword.cloud_notm}}.

{{site.data.keyword.cloud_notm}} abilita più zone che non condividono un singolo punto di guasto all'interno di una singola ubicazione. Fornisce anche il bilanciamento del carico automatico tra le zone all'interno di una regione.

## Ripristino di emergenza
{: #disaster-recovery}

Il ripristino di emergenza può diventare un problema se in un'ubicazione {{site.data.keyword.cloud_notm}} si verifica un guasto significativo che include la potenziale perdita di dati. Poiché MZR non è disponibile in tutte le ubicazioni, devi attendere che {{site.data.keyword.IBM_notm}} riporti online un'ubicazione se diventa non disponibile. Se i servizi di dati sottostanti sono compromessi dal guasto, devi anche attendere che {{site.data.keyword.IBM_notm}} ripristini tali servizi di dati.

In caso di un guasto irreversibile, {{site.data.keyword.IBM_notm}} potrebbe non essere in grado di ripristinare i dati dai backup del database. In questo caso, devi ripristinare i tuoi dati per riportare l'istanza del servizio al suo stato più recente. Puoi ripristinare i dati nella stessa ubicazione o in un'ubicazione diversa.

Per il servizio {{site.data.keyword.texttospeechshort}}, solo i dati per i modelli vocali personalizzati sono memorizzati su {{site.data.keyword.cloud_notm}}. Il tuo piano di ripristino di emergenza include la conoscenza, la conservazione e la preparazione per il ripristino dei tuoi modelli vocali personalizzati.

### Backup dei modelli vocali personalizzati
{: #disaster-recovery-backup}

Conserva le seguenti informazioni sui tuoi modelli vocali personalizzati e sulle relative voci personalizzate:

-   Un elenco di tutti i tuoi modelli vocali personalizzati e le relative definizioni. Per elencare le informazioni sui tuoi modelli personalizzati:
    -   Utilizza il metodo `GET /v1/customizations` per elencare le informazioni su tutti i modelli personalizzati. Per ulteriori informazioni, vedi [Esecuzione di query di tutti i modelli personalizzati](/docs/services/text-to-speech/custom-models.html#cuModelsQueryAll).
    -   Utilizza il metodo `GET /v1/customizations/{customization_id}` per elencare le informazioni su un modello personalizzato specificato. Per ulteriori informazioni, vedi [Esecuzione di query di un modello personalizzato](/docs/services/text-to-speech/custom-models.html#cuModelsQuery).
-   Informazioni su tutte le voci personalizzate (coppie di parole/traduzioni) nei tuoi modelli vocali personalizzati:
    -   Utilizza il metodo `GET /v1/customizations/{customization_id}/words` per elencare le informazioni su tutte le coppie di parole/traduzioni da un modello personalizzato. Per ulteriori informazioni, vedi [Esecuzione di query di tutte le parole da un modello personalizzato](/docs/services/text-to-speech/custom-entries.html#cuWordsQueryModel).
    -   Utilizza il metodo `GET /v1/customizations/{customization_id}/words/{word}` per elencare le informazioni su una coppia di parola/traduzione specificata da un modello personalizzato. Per ulteriori informazioni, vedi [Esecuzione di query di una singola parola da un modello personalizzato](/docs/services/text-to-speech/custom-entries.html#cuWordQueryModel).

È consigliabile conservare queste informazioni in un formato che puoi utilizzare per ricreare i tuoi modelli vocali personalizzati in caso di guasto. Conservare in modo attivo le informazioni sui tuoi modelli personalizzati e sulle tue voci personalizzate e preparare in anticipo le chiamate elencate nella seguente sezione, può permetterti di eseguire un ripristino il più rapidamente possibile.

### Ripristino dei modelli vocali personalizzati
{: #disaster-recovery-restore}

Se hai bisogno di eseguire un ripristino di emergenza, puoi utilizzare le informazioni di backup per ricreare i tuoi modelli vocali personalizzati e le relative voci personalizzate:

1.  Per ricreare i tuoi modelli vocali personalizzati, utilizza il metodo `POST /v1/customizations`. Per ulteriori informazioni, vedi [Creazione di un modello personalizzato](/docs/services/text-to-speech/custom-models.html#cuModelsCreate).
1.  Per aggiungere più coppie di parole/traduzioni ai tuoi modelli vocali personalizzati, utilizza il metodo `POST /v1/customizations/{customization_id}/words`. Per ulteriori informazioni, vedi [Aggiunta di più parole a un modello personalizzato](/docs/services/text-to-speech/custom-entries.html#cuWordsAdd).
1.  Per aggiungere una singola coppia di parola/traduzione ai tuoi modelli vocali personalizzati, utilizza il metodo `POST /v1/customizations/{customization_id}/words/{word}`. Per ulteriori informazioni, vedi [Aggiunta di una singola parola a un modello personalizzato](/docs/services/text-to-speech/custom-entries.html#cuWordAdd).

Puoi aggiungere tutte le tue voci personalizzate contemporaneamente, in gruppi o una alla volta.
