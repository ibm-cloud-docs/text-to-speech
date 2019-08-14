---

copyright:
  years: 2015, 2019
lastupdated: "2019-06-24"

subcollection: text-to-speech

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

# L'interface WebSocket
{: #usingWebSocket}

Pour synthétiser du texte en parole avec l'interface WebSocket du service {{site.data.keyword.texttospeechfull}}, vous devez d'abord établir une connexion avec le service en appelant sa méthode `/v1/synthesize`. Vous envoyez ensuite le texte à synthétiser au service sous forme de message texte JSON via la connexion. Le service ferme automatiquement la connexion WebSocket une fois le traitement de la demande terminé.
{: shortdesc}

Le cycle de demande et de réponse de synthèse comprend les étapes suivantes :

1.  [Ouvrir une connexion](#WSopen).
1.  [Envoyer un texte de saisie](#WSsend).
1.  [Recevoir une réponse](#WSreceive).

L'interface WebSocket accepte une entrée identique et produit des résultats identiques à ceux des méthodes `GET` et `POST /v1/synthesize` de l'interface HTTP. Cependant, l'interface WebSocket prend en charge l'utilisation de l'élément `<mark>` SSML pour identifier l'emplacement des marqueurs spécifiés par l'utilisateur dans l'audio. Il peut également renvoyer des informations de minutage pour toutes les chaînes du texte en entrée. Pour plus d'informations, voir [Obtention du minutage des mots](/docs/services/text-to-speech?topic=text-to-speech-timing).

Les fragments d'exemples de code suivants sont écrits en JavaScript et sont basés sur l’API WebSocket HTML5. Pour plus d'informations sur le protocole WebSocket, voir [Request for Comments: 6455](http://tools.ietf.org/html/rfc6455){: external}, norme IETF (Internet Engineering Task Force).
{: note}

## Ouvrir une connexion
{: #WSopen}

Vous appelez la méthode `/v1/synthesize` via le protocole WebSocket Secure (WSS) pour ouvrir une connexion au service. La méthode est disponible sur le noeud final suivant :

```
wss://{host_name}/text-to-speech/api/v1/synthesize
```
{: codeblock}

où `{host_name}` est l'emplacement où votre application est hébergée :

-   `stream.watsonplatform.net` pour Dallas (les exemples suivants utilisent ce nom d'hôte)
-   `stream-fra.watsonplatform.net` pour Francfort
-   `gateway-syd.watsonplatform.net` pour Sydney
-   `gateway-wdc.watsonplatform.net` pour Washington, DC
-   `gateway-tok.watsonplatform.net` pour Tokyo
-   `gateway-lon.watsonplatform.net` pour Londres

Un client WebSocket appelle cette méthode avec les paramètres de requête suivants pour établir une connexion authentifiée avec le service. Si vous utilisez l'authentification IAM (Identity and Access Management), utilisez le paramètre de requête `access_token`. Si vous utilisez les données d'identification du service Cloud Foundry, incluez le paramètre de requête `watson-token`.

<table>
  <caption>Tableau 1. Paramètres de la méthode <code>/v1/synthesize</code></caption>
  <tr>
    <th style="text-align:left; width:23%">Paramètre</th>
    <th style="text-align:center; width:12%">Type de données</th>
    <th style="text-align:left">Description</th>
  </tr>
  <tr>
    <td style="text-align:left"><code>access_token</code>
      <br/><em>Facultatif</em></td>
    <td style="text-align:center">Chaîne</td>
    <td style="text-align:left">
      <em>Si vous utilisez l'authentification IAM,,</em> transmettez un jeton d'accès IAM valide pour vous authentifier auprès du service. Vous transmettez un jeton d'accès IAM au lieu de transmettre une clé d'API avec l'appel. Vous devez utiliser le jeton d'accès avant son expiration. Pour plus d'informations sur l'obtention d'un jeton d'accès, voir
      [Authentification avec des jetons IAM](/docs/services/watson?topic=watson-iam).
    </td>
  </tr>
  <tr>
    <td style="text-align:left"><code>watson-token</code>
      <br/><em>Facultatif</em></td>
    <td style="text-align:center">Chaîne</td>
    <td style="text-align:left">
      <em>Si vous utilisez les données d'identification du service Cloud Foundry,</em> transmettez un jeton d'authentification {{site.data.keyword.watson}} valide pour vous authentifier auprès du service. Vous transmettez un jeton {{site.data.keyword.watson}} au lieu de transmettre les données d'identification du service avec l'appel.
      Les jetons {{site.data.keyword.watson}} sont basés sur les données d'identification du service Cloud Foundry, qui utilisent un `username` et un `password` pour l'authentification de base HTTP. Pour plus d'informations sur l'obtention d'un jeton {{site.data.keyword.watson}}, voir
      [Jetons {{site.data.keyword.watson}}](/docs/services/watson?topic=watson-gs-tokens-watson-tokens).
    </td>
  </tr>
  <tr>
    <td><code>voice</code><br/><em>Facultatif</em></td>
    <td style="text-align:center">Chaîne</td>
    <td>
      Spécifie la voix dans laquelle le texte doit être prononcé en audio.
      Omettez le paramètre pour utiliser la voix par défaut, `en-US_MichaelVoice`.
      Pour plus d'informations, voir [Langues et voix](/docs/services/text-to-speech?topic=text-to-speech-voices).
    </td>
  </tr>
  <tr>
    <td><code>customization_id</code><br/><em>Facultatif</em></td>
    <td style="text-align:center">Chaîne</td>
    <td>
      Spécifie l'identificateur global unique (GUID) d'un modèle vocal personnalisé à utiliser pour la synthèse. Un modèle vocal personnalisé ne fonctionne que s'il correspond à la langue de la voix utilisée pour la synthèse. Si vous incluez un ID de personnalisation, vous devez effectuer la demande avec les données d'identification de l'instance du propriétaire du modèle personnalisé. Omettez le paramètre pour utiliser la voix spécifiée sans personnalisation. Pour plus d'informations, voir [Compréhension de la personnalisation](/docs/services/text-to-speech?topic=text-to-speech-customIntro).
    </td>
  </tr>
  <tr>
    <td><code>x-watson-learning-opt-out</code><br/><em>Facultatif</em></td>
    <td style="text-align:center">Valeur booléenne</td>
    <td>
      Indique si le service enregistre les demandes et les résultats envoyés via la connexion. Pour empêcher IBM d’accéder à vos données afin d’améliorer les services généraux, indiquez <code>true</code> pour le paramètre. Pour plus d'informations, voir
      [Contrôle de la journalisation des demandes pour les services Watson](/docs/services/watson?topic=watson-gs-logging-overview).
    </td>
  </tr>
  <tr>
    <td style="text-align:left"><code>x-watson-metadata</code>
      <br/><em>Facultatif</em></td>
    <td style="text-align:center">Chaîne</td>
    <td style="text-align:left">
      Associe un ID client aux données transmises via la connexion. Le paramètre accepte l'argument
      <code>customer_id={id}</code>, où <code>id</code> est une chaîne aléatoire ou générique devant être associée aux données. Vous devez coder dans l'URL l'argument associé au paramètre, par exemple,
      `customer_id%3dmy_ID`. Par défaut, aucun ID client n'est associé aux données. Pour plus d'informations, voir [Sécurité des informations](/docs/services/text-to-speech?topic=text-to-speech-information-security).
    </td>
  </tr>
</table>

Le fragment de code JavaScript suivant ouvre une connexion avec le service. L'appel à la méthode `/v1/synthesize` transmet les paramètres de requête `voice` et `access_token`, le premier permettant au service d'utiliser la voix en anglais américain Allison. Une fois la connexion établie, les écouteurs d'événements (`onOpen`, `onClose`, etc.) sont définis pour répondre aux événements émanant du service.

```javascript
var IAM_access_token = '{access_token}';
var wsURI = 'wss://stream.watsonplatform.net/text-to-speech/api/v1/synthesize'
  + '?access_token=' + IAM_access_token
  + '&voice=en-US_AllisonVoice';
var websocket = new WebSocket(wsURI);

websocket.onopen = function(evt) { onOpen(evt) };
websocket.onclose = function(evt) { onClose(evt) };
websocket.onmessage = function(evt) { onMessage(evt) };
websocket.onerror = function(evt) { onError(evt) };
```
{: codeblock}

## Envoyer un texte de saisie
{: #WSsend}

Pour synthétiser du texte, le client transmet un message texte JSON simple au service avec les paramètres suivants.

<table>
  <caption>Tableau 2. Paramètres du message texte JSON</caption>
  <tr>
    <th style="text-align:left; width:23%">Paramètre</th>
    <th style="text-align:center; width:12%">Type de données</th>
    <th style="text-align:left">Description</th>
  </tr>
  <tr>
    <td><code>text</code><br/><em>Obligatoire</em></td>
    <td style="text-align:center">Chaîne</td>
    <td>
      Fournit le texte à synthétiser. Le client peut transmettre du texte brut ou du texte annoté avec le langage SSML (Speech Synthesis Markup Language). Le client peut transmettre un maximum de 5 Ko de texte en entrée avec la demande. La limite inclut tout le texte SSML que vous spécifiez. Pour plus d'informations, voir
      [Spécification du texte d'entrée](/docs/services/text-to-speech?topic=text-to-speech-usingHTTP#input)
      et des sections qui suivent.<br/><br/>
      L'entrée SSML peut également inclure l'élément <code>&lt;mark&gt;</code>.
      Pour plus d'informations, voir [Spécification d'une marque SSML](/docs/services/text-to-speech?topic=text-to-speech-timing#mark).
    </td>
  </tr>
  <tr>
    <td><code>accept</code><br/><em>Obligatoire</em></td>
    <td style="text-align:center">Chaîne</td>
    <td>
      Spécifie le format demandé (type MIME) de l'audio. Utilisez
      `*/*` pour demander le format audio par défaut,
      <code>audio/ogg;codecs=opus</code>. Pour plus d'informations, voir [Formats audio](/docs/services/text-to-speech?topic=text-to-speech-audioFormats).
    </td>
  </tr>
  <tr>
    <td><code>timings</code><br/><em>Facultatif</em></td>
    <td style="text-align:center">Chaîne[ ]</td>
    <td>
      Spécifie que le service doit renvoyer des informations de minutage des mots pour toutes les chaînes du texte en entrée. Le service renvoie le temps de début et de fin de chaque jeton de l'entrée. Spécifiez <code>words</code> en tant qu'élément isolé du tableau pour demander le minutage des mots. Spécifiez un tableau vide ou omettez le paramètre pour ne recevoir aucun minutage de mot.
      Pour plus d'informations, voir [Obtention du minutage des mots](/docs/services/text-to-speech?topic=text-to-speech-timing#timing). <em>Non pris en charge pour le texte d'entrée en japonais.</em>
    </td>
  </tr>
</table>

Le fragment de code JavaScript suivant transmet un simple message "Hello world" en tant que texte d'entrée et demande le format audio par défaut. Les appels sont inclus dans la fonction `onOpen` définie pour le client afin de garantir qu'ils ne sont envoyés que lorsque la connexion est établie.

```javascript
function onOpen(evt) {
  var message = {
    text: 'Hello world',
    accept: '*/*'
  };
  websocket.send(JSON.stringify(message));
}
```
{: codeblock}

Le service répond à ce message en envoyant un message texte confirmant le format de la réponse audio. La réponse suivante confirme le format audio par défaut.

```javascript
{
  'binary_streams': [
    {
      content_type: 'audio/ogg;codecs=opus'
    }
  ]
}
```
{: codeblock}

## Recevoir une réponse
{: #WSreceive}

Après avoir confirmé le format audio, le service envoie le son synthétisé sous forme de flux binaire de données au format indiqué. Le service envoie des informations de minutage sous forme d'un ou plusieurs messages texte si

-   Le texte d'entrée comprend un ou plusieurs éléments `<mark>` SSML.
-   Vous spécifiez le paramètre `timings` avec la demande.

Le service peut également envoyer des messages texte avec des avertissements ou des erreurs. Une fois la synthèse du texte en entrée terminée, le service ferme automatiquement la connexion WebSocket.

Le client doit ajouter des réponses binaires émanant du service aux résultats audio reçus via la connexion. Il peut gérer les messages texte en y répondant, en les affichant ou en les capturant pour une utilisation par l'application (par exemple, s'ils contiennent des emplacements de marque). L'exemple simple suivant d'une fonction `onMessage` ajoute les messages texte et binaires reçus du service à la variable appropriée en fonction de leur type. Lorsque la fonction `onClose()` s'exécute, tout le flux audio a été reçu.

```javascript
var messages;
var audioStream;

function onMessage(evt) {
  if (typeof evt.data === string) {
    messages += evt.data;
  } else {
    console.log('Received ' + evt.data.size() + ' binary bytes');
    audioStream += evt.data;
  }
}

function onClose(evt) {
  // The audio stream is complete.
}
```
{: codeblock}

## Codes retour WebSocket
{: #returnCodes}

Le service peut envoyer les codes retour suivants au client via la connexion WebSocket :

-   `1000` indique la fermeture normale de la connexion, ce qui signifie que l'objectif pour lequel la connexion a été établie a été rempli.
-   `1002` indique que le service ferme la connexion en raison d'une erreur de protocole.
-   `1006` indique que la connexion s'est fermée anormalement.
-   `1009` indique que la taille de la trame a dépassé la limite de 4 Mo.
-   `1011` indique que le service met fin à la connexion car il a rencontré une condition inattendue l'empêchant de répondre à la demande, par exemple un argument non valide. Le code retour peut également indiquer que le texte en entrée était trop volumineux.

Si le socket se ferme avec une erreur, le service envoie au client un message informatif du type `{"error": "Specific error message"}` avant de se fermer. Le service peut également envoyer des messages d'avertissement non fatals pour des paramètres inconnus.

## Exemple de messages d'erreur et d'avertissement
{: #returnErrors}

Les exemples suivants montrent des réponses d'erreur. Ils incluent un message texte JSON et un message formaté à partir de la méthode de rappel `onClose` du client. Les messages formatés commencent par le booléen `true` car la connexion est fermée. Ils incluent également le code d'erreur WebSocket qui a provoqué la fermeture.

-   Cet exemple affiche des messages d'erreur relatifs à un argument non valide du paramètre `accept` :

    ```javascript
    {
      "error": "Unsupported mimetype. Supported mimetypes are: ['application/json', 'audio/flac', ...]"
    }
    (True, 1011, u'see the previous message for the error details.')
    ```
    {: codeblock}

-   Cet exemple affiche des messages d'erreur pour un paramètre `text` manquant :

    ```javascript
    {
      "error": "Required parameter \"text\" is missing."
    }
    (True, 1011, u'see the previous message for the error details.')
    ```
    {: codeblock}

L'exemple suivant montre une réponse d'avertissement, dans le cas présent pour un paramètre inconnu nommé `invalid-parameter`. Il n'inclut pas le deuxième message car la connexion n'est pas fermée par l'avertissement.

```javascript
{
  "warnings": "Unknown arguments: invalid-parameter."
}
```
{: codeblock}

Pour plus d'informations sur les codes retour WebSocket, voir [Request for Comments: 6455](http://tools.ietf.org/html/rfc6455){: external}, norme IETF (Internet Engineering Task Force).
