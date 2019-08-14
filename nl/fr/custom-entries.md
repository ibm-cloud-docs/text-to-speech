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

# Création et gestion d'entrées personnalisées
{: #customWords}

Une fois qu'un modèle personnalisé existe, l'étape suivante consiste à ajouter des entrées personnalisées sous forme de paires mot/traduction afin de définir la manière dont les mots spécifiés doivent être prononcés lors de la synthèse. Les définitions remplacent les règles de prononciation standard par défaut du service. Vous pouvez ajouter et interroger des traductions d'un ou de plusieurs mots à la fois, et supprimer des mots individuels dont vous n'avez plus besoin. Une fois que vous êtes familiarisé avec l'interface de personnalisation, il peut être plus pratique de manipuler plusieurs mots à la fois que de travailler mot par mot. Vous devez utiliser les données d'identification pour l'instance du service qui possède un modèle personnalisé afin d'utiliser toute méthode nécessitant son ID de personnalisation.
{: shortdesc}

## Ajout d'un mot à un modèle personnalisé
{: #cuWordAdd}

Pour ajouter une paire unique mot/traduction à un modèle personnalisé, utilisez la méthode `PUT /v1/customizations/{customization_id}/words/{word}`. Vous spécifiez le mot à ajouter dans l'URL de la méthode. Vous fournissez la traduction du mot sous forme d'objet JSON avec un attribut `translation` unique. L'ajout d'une nouvelle traduction pour un mot qui existe déjà dans un modèle écrase la traduction existante du mot.

Vous pouvez fournir une traduction à l'aide de la méthode de similitude de sonorité ou de la méthode phonétique (ou d'une combinaison des deux). Pour les traductions phonétiques, vous pouvez utiliser le format Alphabétique phonétique international (IPA) ou le format de représentation phonétique symbolique (SPR) {{site.data.keyword.IBM_notm}}. Les exemples suivants utilisent différentes approches pour ajouter des traductions équivalentes pour le mot `IEEE` à un modèle personnalisé.

-   **Similitude de sonorité :** pour cet exemple, la méthode de similitude de sonorité est l'approche la plus simple :

    ```bash
    curl -X PUT -u "apikey:{apikey}"
    --header "Content-Type: application/json"
    --data "{\"translation\":\"I triple E\"}"
    "https://stream.watsonplatform.net/text-to-speech/api/v1/customizations/{customization_id}/words/IEEE"
    ```
    {: pre}

-   **IPA phonétique :** IPA requiert l'utilisation de l'élément `<phoneme>` avec l'attribut `alphabet` défini sur `ipa` et l'attribut `ph` défini au format IPA :

    <pre><code class="language-bash">  curl -X PUT -u "apikey:{apikey}"
    --header "Content-Type: application/json"
    --data "{\"translation\":\"&lt;phoneme alphabet=\\\"ipa\\\" ph=\\\"&#712;a&#618;.t&#633;&#712;&#616;p&#601;l.&#712;i\\\"&gt;&lt;/phoneme&gt;\"}"
    "https://stream.watsonplatform.net/text-to-speech/api/v1/customizations/{customization_id}/words/IEEE"</code></pre>

-   **{{site.data.keyword.IBM_notm}} SPR phonétique :** SPR utilise l'élément `<phoneme>` avec l'attribut `alphabet` défini sur `ibm` et l'attribut `ph` défini au format SPR :

    ```bash
    curl -X PUT -u "apikey:{apikey}"
    --header "Content-Type: application/json"
    --data "{\"translation\":\"<phoneme alphabet=\\\"ibm\\\" ph=\\\"1Y.tr1Ipxl.1i\\\"></phoneme>\"}"
    "https://stream.watsonplatform.net/text-to-speech/api/v1/customizations/{customization_id}/words/IEEE"
    ```
    {: pre}

## Ajout de plusieurs mots à un modèle personnalisé
{: #cuWordsAdd}

Pour ajouter un ou plusieurs mots à un modèle personnalisé à la fois, utilisez la méthode `POST /v1/customizations/{customization_id}/words`. Vous spécifiez les entrées à ajouter au modèle personnalisé sous la forme d'un tableau JSON de paires mot/traduction. L'exemple suivant ajoute des traductions courantes basées sur la sonorité pour les mots `NCAA` et `iPhone` à un modèle personnalisé :

```bash
curl -X POST -u "apikey:{apikey}"
--header "Content-Type: application/json"
--data "{\"words\": [{\"word\":\"NCAA\", \"translation\":\"N C double A\"}, {\"word\":\"iPhone\", \"translation\":\"I phone\"}]}"
"https://stream.watsonplatform.net/text-to-speech/api/v1/customizations/{customization_id}/words"
```
{: pre}

Le contenu JSON envoyé dans le corps de la demande correspond à ce qui suit :

```javascript
{
  "words": [
    {"word":"NCAA", "translation":"N C double A"},
    {"word":"iPhone", "translation":"I phone"}
  ]
}
```
{: codeblock}

Comme indiqué dans [Mise à jour d'un modèle personnalisé](/docs/services/text-to-speech?topic=text-to-speech-customModels#cuModelsUpdate), vous pouvez également utiliser la méthode `POST /v1/customizations/{customization_id}` pour ajouter des mots à un modèle personnalisé. L'exemple suivant utilise cette méthode pour ajouter les deux mêmes mots que l'exemple précédent ; il ne modifie pas les métadonnées du modèle. A l'exception de l'URL, les deux méthodes sont identiques.

```bash
curl -X POST -u "apikey:{apikey}"
--header "Content-Type: application/json"
--data "{\"words\": [{\"word\":\"NCAA\", \"translation\":\"N C double A\"}, {\"word\":\"iPhone\", \"translation\":\"I phone\"}]}"
"https://stream.watsonplatform.net/text-to-speech/api/v1/customizations/{customization_id}"
```
{: pre}

## Ajout de mots à un modèle personnalisé japonais
{: #cuJapaneseAdd}

Des considérations supplémentaires et une zone `part_of_speech` supplémentaire s'appliquent lors de la création d'entrées pour des mots dans un modèle personnalisé japonais ; pour plus d'informations, voir [Utilisation des entrées en japonais](/docs/services/text-to-speech?topic=text-to-speech-rules#jaNotes). Spécifiez une partie du discours pour une entrée personnalisée en japonais comme suit :

-   Pour la méthode `PUT /v1/customizations/{customization_id}/words/{word}`, transmettez un objet JSON au format suivant :

    ```javascript
    {
      "translation": "value",
      "part_of_speech": "value"
    }
    ```
    {: codeblock}

-   Pour les méthodes `POST /v1/customizations/{customization_id}/words` et `POST customizations/{customization_id}`, transmettez un objet JSON comme suit :

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

Les exemples suivants de la méthode `PUT /v1/customizations/{customization_id}/words/{word}` traduisent la chaîne codée sur deux octets dans l'URL pour `NY` par le nom (`Mesi`) <code>&#12491;&#12517;&#12540;&#12520;&#12540;&#12463;</code> (`New York` en anglais). Si cette traduction personnalisée n'est pas définie, la chaîne est lue `enu wai`.

-   **Basée sur la sonorité :**

    <pre><code>curl -X PUT -u "apikey:{apikey}"
    --header "Content-Type: application/json"
    --data "{\"translation\":\"&#12491;&#12517;&#12540;&#12520;&#12540;&#12463;\", \"part_of_speech\":\"Mesi\"}"
    "https://stream.watsonplatform.net/text-to-speech/api/v1/customizations/{customization_id}/words/%EF%BC%AE%EF%BC%B9"</code></pre>

-   **IPA phonétique :**

    <pre><code>curl -X PUT -u "apikey:{apikey}"
    --header "Content-Type: application/json"
    --data "{\"translation\":\"&lt;phoneme alphabet=\\\"ipa\\\" ph=\\\"&#626;&#623;&#720;&#106;&#111;&#720;&#107;&#623;\\\"&gt;&lt;/phoneme&gt;\", \"part_of_speech\":\"Mesi\"}"
    "https://stream.watsonplatform.net/text-to-speech/api/v1/customizations/{customization_id}/words/%EF%BC%AE%EF%BC%B9"</code></pre>

-   **{{site.data.keyword.IBM_notm}} SPR phonétique :**

    <pre><code>curl -X PUT -u "apikey:{apikey}"
    --header "Content-Type: application/json"
    --data "{\"translation\":\"&lt;phoneme alphabet=\\\"ibm\\\" ph=\\\"nyu:yo:ku\\\"&gt;&lt;/phoneme&gt;\", \"part_of_speech\":\"Mesi\"}"
    "https://stream.watsonplatform.net/text-to-speech/api/v1/customizations/{customization_id}/words/%EF%BC%AE%EF%BC%B9"</code></pre>

## Demande d'un mot à partir d'un modèle personnalisé
{: #cuWordQueryModel}

Pour demander la traduction d'un mot à partir d'un modèle personnalisé, utilisez la méthode `GET /v1/customizations/{customization_id}/words/{word}`. Vous spécifiez le mot dans l'URL de la méthode. La traduction est renvoyée telle qu'elle est définie dans le modèle personnalisé (sonorité ou phonétique).

L'exemple suivant interroge un modèle personnalisé pour la traduction du mot `IEEE` :

```bash
curl -X GET -u "apikey:{apikey}"
"https://stream.watsonplatform.net/text-to-speech/api/v1/customizations/{customization_id}/words/IEEE"
```
{: pre}

Si le mot contient la traduction basée sur la sonorité dans le modèle, l'exemple renvoie la sortie JSON suivante :

```javascript
{
  "translation": "I triple E"
}
```
{: codeblock}

## Demande de tous les mots d'un modèle personnalisé
{: #cuWordsQueryModel}

Pour voir les traductions de tous les mots définis dans un modèle personnalisé, utilisez la méthode `GET /v1/customizations/{customization_id}/words`. L'exemple suivant utilise la méthode pour répertorier les entrées d'un modèle personnalisé contenant des traductions basées sur la sonorité pour trois mots :

```bash
curl -X GET -u "apikey:{apikey}"
"https://stream.watsonplatform.net/text-to-speech/api/v1/customizations/{customization_id}/words"
```
{: pre}

La méthode renvoie un tableau JSON avec les données suivantes. Pour les modèles personnalisés japonais, la sortie inclut la partie du discours pour les mots individuels.

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

Comme décrit dans [Demande d'un modèle personnalisé](/docs/services/text-to-speech?topic=text-to-speech-customModels#cuModelsQuery), vous pouvez également utiliser la méthode `GET /v1/customizations/{customization_id}` pour afficher à la fois les métadonnées et les mots d'un modèle personnalisé :

```bash
curl -X GET -u "apikey:{apikey}"
"https://stream.watsonplatform.net/text-to-speech/api/v1/customizations/{customization_id}"
```
{: pre}

La méthode renvoie la sortie JSON du formulaire suivant. Dans la mesure où cet exemple et l'exemple précédent spécifient le même modèle personnalisé, le tableau de mots dans leur sortie est identique.

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

## Demande d'un mot à partir d'une langue
{: #cuWordsQueryLanguage}

Pour interroger la prononciation d'un mot, utilisez la méthode `GET /v1/pronunciation`. Spécifiez une voix pour obtenir la prononciation dans la langue de cette voix. Par défaut, la méthode renvoie la prononciation en fonction des règles de prononciation habituelles du service, mais vous pouvez également demander la prononciation d'un modèle vocal personnalisé spécifié. La méthode comprend quatre paramètres de requête qui vous permettent de spécifier les informations à renvoyer :

-   Le paramètre `text` obligatoire spécifie le mot dont la prononciation doit être renvoyée.
-   Le paramètre `voice` facultatif vous permet de spécifier la langue de la prononciation. Vous spécifiez l'un des modèles vocaux (par exemple, `en-US_LisaVoice`) pour indiquer la langue souhaitée ; toutes les voix de la même langue (par exemple, `en-US`) renvoient la même prononciation. Par défaut, la prononciation est renvoyée pour l'anglais américain.
-   Le paramètre `format` facultatif vous permet de spécifier le format phonétique de la prononciation, `ipa` ou `ibm`. Par défaut, la prononciation est renvoyée au format IPA.
-   Le paramètre `customization_id` facultatif vous permet de spécifier un modèle vocal personnalisé pour lequel la prononciation doit être renvoyée. Si le mot n'est pas défini dans le modèle vocal spécifié, le service renvoie la prononciation par défaut dans la langue du modèle. Omettez le paramètre pour voir la traduction dans la voix spécifiée sans personnalisation. Ne spécifiez pas à la fois une voix et un modèle vocal personnalisé.

Cette méthode est utile car elle vous permet de demander un mot dans n’importe quelle langue et, ne nécessitant pas d’ID de personnalisation, elle n’impose aucune restriction quant aux mots que vous pouvez voir. Cela peut s'avérer particulièrement utile lors de la composition de la traduction phonétique d'un nouveau mot ; vous pouvez l'utiliser pour obtenir la prononciation d'un mot existant, puis l'utiliser comme base de votre nouvelle traduction, ce qui est beaucoup plus pratique que de créer une toute nouvelle traduction.

L'exemple suivant obtient la prononciation du mot `IEEE` au format IPA par défaut.

```bash
curl -X GET -u "apikey:{apikey}"
"https://stream.watsonplatform.net/text-to-speech/api/v1/pronunciation?text=IEEE"
```
{: pre}

<pre><code data-copy="false" class="language-javascript">{
  "pronunciation": ".&#712;a&#618; .&#712;i .&#712;i .&#712;i"
}</code></pre>

L'exemple suivant entre une traduction basée sur la sonorité du mot `IEEE` et obtient l'équivalent phonétique au format {{site.data.keyword.IBM_notm}} SPR. L'obtention de la prononciation phonétique pour une traduction basée sur la sonorité est une approche particulièrement intéressante pour composer une traduction phonétique. Dans l'exemple suivant, les espaces du mot sont codés dans l'URL.

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

## Suppression d'un mot dans un modèle personnalisé
{: #cuWordDelete}

Pour supprimer un mot dans un modèle personnalisé, utilisez la méthode `DELETE /v1/customizations/{customization_id}/words/{word}`. Vous spécifiez le mot à supprimer dans l'URL de la méthode. Vous pouvez uniquement supprimer des mots individuels ; vous ne pouvez pas supprimer plusieurs mots avec une seule méthode.

L'exemple suivant supprime le mot `IEEE` dans le modèle personnalisé spécifié :

```bash
curl -X DELETE -u "apikey:{apikey}"
"https://stream.watsonplatform.net/text-to-speech/api/v1/customizations/{customization_id}/words/IEEE"
```
{: pre}
