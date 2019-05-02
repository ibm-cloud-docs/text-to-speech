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

# Utilisation d'un modèle vocal personnalisé 
{: #customUsing}

Une fois que vous avez créé un modèle personnalisé et que vous l'avez rempli avec des entrées personnalisées, vous l'utilisez en transmettant son ID de personnalisation (GUID) avec le paramètre de requête `customization_id` de la méthode HTTP `GET` ou `POST /v1/synthesize` ou de la méthode WebSocket `/v1/synthesize`. Les données d'identification de service du propriétaire d'un modèle doivent être utilisées pour appeler une méthode `synthesize` qui utilise le modèle personnalisé.
{: shortdesc}

Les deux premiers exemples génèrent une prononciation personnalisée pour `IEEE` basée sur les entrées du modèle personnalisé indiqué. La prononciation personnalisée est utilisée à la place de la prononciation par défaut des règles de prononciation habituelles du service. 

-   Méthode HTTP `GET /v1/synthesize` :

    ```bash
    curl -X GET -u "apikey:{apikey}"
    --header "Accept: audio/flac"
    --output ieee.flac
    "https://stream.watsonplatform.net/text-to-speech/api/v1/synthesize?text=IEEE&customization_id={customization_id}"
    ```
    {: pre}

-   Méthode HTTP `POST /v1/synthesize` :

    ```bash
    curl -X POST -u "apikey:{apikey}"
    --header "Content-Type: application/json"
    --header "Accept: audio/flac"
    --data "{\"text\":\"IEEE\"}"
    --output ieee.flac
    "https://stream.watsonplatform.net/text-to-speech/api/v1/synthesize?customization_id={customization_id}"
    ```
    {: pre}

Le troisième exemple établit une connexion WebSocket avec la méthode `/v1/synthesize` qui utilise le modèle personnalisé indiqué pour synthétiser le texte transmis via la connexion :

```javascript
var token = {authentication-token};
var wsURI = 'wss://stream.watsonplatform.net/text-to-speech/api/v1/synthesize'
  + '?access_token=' + IAM_access_token
  + '&customization_id={customization_id}';
var websocket = new WebSocket(wsURI);
```
{: codeblock}
