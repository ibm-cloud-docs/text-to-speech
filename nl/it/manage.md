---

copyright:
  years: 2019
lastupdated: "2019-06-27"

subcollection: text-to-speech-data

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:external: target="_blank" .external}
{:deprecated: .deprecated}
{:important: .important}
{:note: .note}
{:tip: .tip}
{:pre: .pre}
{:codeblock: .codeblock}
{:screen: .screen}
{:javascript: .ph data-hd-programlang='javascript'}
{:java: .ph data-hd-programlang='java'}
{:python: .ph data-hd-programlang='python'}
{:swift: .ph data-hd-programlang='swift'}
{:download: .download}

# Gestione del cluster
{: #manage}

Dopo aver installato e configurato {{site.data.keyword.texttospeechdatafull}} on {{site.data.keyword.icp4dfull}}, puoi gestire l'istanza e il cluster.

## Preparazione della tua macchina locale
{: #manage-prep-local-machine}

Assicurati che i seguenti prerequisiti siano installati e funzionanti correttamente sulla tua macchina locale prima di eseguire una qualsiasi attività di gestione del cluster.

1. Installa e configura i seguenti strumenti della riga di comando:

  - {{site.data.keyword.icp4dfull_notm}} 2.1.0 o successiva, che include la CLI IBM Cloud Private: [`cloudctl`](https://www.ibm.com/support/knowledgecenter/SSBS6K_3.1.2/manage_cluster/install_cli.html){: external}
  - Kubernetes 1.12.4 o successiva: [`kubectl`](https://docs-icpdata.mybluemix.net/docs/content/SSQNUZ_current/com.ibm.icpdata.doc/zen/install/kubectl-access.html){: external}
  - Helm 2.9.1 o successiva: [`helm`](https://helm.sh){: external}

1.  Avvia `helm`:
  
    ```bash
    helm init --client-only
    ```
    {: pre}

1.  Verifica che gli strumenti siano installati correttamente immettendo i seguenti comandi di verifica.

    - Verifica la CLI IBM Cloud Private (`cloudctl`):

      ```bash
      cloudctl login -a https://{hostname}:8443 -u {admin_user_id} -p {admin_password}
      ```
      {: pre}
    
      Se stai utilizzando un programma di bilanciamento del carico, specifica il suo nome host invece di quello del nodo master.
      {: note}

    - Verifica Kubernetes (`kubectl`):

      ```bash
      kubectl get namespaces
      ```
      {: pre}

      Se non puoi eseguire il comando `kubectl`, vedi [Enabling access to the Kubernetes command-line interface](https://www.ibm.com/support/knowledgecenter/SSQNUZ_2.1.0/com.ibm.icpdata.doc/zen/install/kubectl-access.html){: external}.
      {: note}

    - Verifica Helm (`helm`):

      ```bash
      helm version --tls
      ```
      {: pre}

## Esecuzione delle attività di gestione 
{: perform-mgmt-tasks}

Le seguenti sono alcune attività che puoi eseguire per monitorare e conservare la tua istanza {{site.data.keyword.texttospeechshort}}.

  - Identifica i nodi cluster a cui viene distribuito il prodotto:
    ```bash
    kubectl get pods -o wide | grep -v Completed
    ```
    {: pre}

  - Elenca il numero di repliche di ogni microservizio in un determinato `{namespace}`:
    ```bash
    kubectl get deploy -n {namespace}
    ```
    {: pre}
    o
    ```bash
    kubectl get statefulset -n {namespace}
    ```
    {: pre}

  - Modifica (aumenta o diminuisci) il numero di repliche:
    ```bash
    kubectl scale deploy {pod_name} --replicas={number}
    ```
    {: pre}
    o
    ```bash
    kubectl scale statefulsets {set_name} --replicas={number}
    ```
    {: pre}

  - Visualizza i log

    Per impostazione predefinita, {{site.data.keyword.icp4dfull_notm}} registra automaticamente le informazioni da ogni servizio. Per ulteriori informazioni, vedi [Viewing logs](https://www.ibm.com/support/knowledgecenter/SSQNUZ_2.1.0/com.ibm.icpdata.doc/zen/admin/logs.html){: external}. 

## Gestione dell'accesso utente 
{: #manage-user-access}

Dopo aver eseguito il provisioning di un'istanza, puoi condividere l'URL del servizio con altri utenti. Tuttavia, tali utenti possono accedere al servizio solo se gli fornisci l'accesso. 

Se intendi utilizzare SAML per SSO (Single Sign-On), completa [Configuring single sign-on](https://www.ibm.com/support/knowledgecenter/SSQNUZ_2.1.0/com.ibm.icpdata.doc/zen/admin/saml-sso.html#saml-sso) prima di aggiungere degli utenti. Se aggiungi degli utenti prima di configurare SSO, devi riaggiungerli con il loro ID SAML per abilitarli ad utilizzare SSO. 

1.  Dal menu del client web, fai clic su **Administer > Manage user**. 

1.  Fai clic su **Add user**, quindi specifica il nome completo, il nome utente e l'indirizzo email dell'utente. Imposta le autorizzazioni dell'utente e poi fai clic su **Add**. 

1.  Dal menu del client web, seleziona **My Instances**. 

1.  Trova la tua istanza di {{site.data.keyword.texttospeechshort}}, fai clic sul menu More (**...**) e quindi scegli **Manage Access**. 

1.  Fai clic su **Add user**. 

1.  Fai clic sul campo del nome utente per visualizzare un elenco di persone che puoi aggiungere. 

    Gli utenti che hai aggiunto nei passi precedenti vengono elencati. Seleziona un nome, scegli **User** o **Admin** come loro ruolo di accesso e fai quindi clic su **Add**.  

    Se non sei connesso a un registro utenti esistente e non hai abilitato SSO (single sign-on), vengono create delle password temporanee per gli utenti che aggiungi. Le password temporanee vengono inviate agli utenti per mezzo degli indirizzi email che hai specificato. 
