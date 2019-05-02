---

copyright:
  years: 2015, 2019
lastupdated: "2019-03-21"

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

# Interface HTTP 
{: #usingHTTP}

Pour synthétiser du texte en parole avec l'interface HTTP REST du service {{site.data.keyword.texttospeechfull}}, appelez la méthode `GET` ou `POST /v1/synthesize`. Spécifiez le texte à synthétiser, ainsi que la voix et le format de l'audio parlé. Vous pouvez également spécifier un modèle de voix personnalisé à utiliser avec la demande.
{: shortdesc}

Pour plus d'informations sur l'interface HTTP, voir la [référence d'API ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://{DomainName}/apidocs/text-to-speech){: new_window}.

## Synthèse de texte en audio 
{: #synthesize}

Pour synthétiser du texte en audio, appelez l’une des deux versions de la méthode `/v1/synthesize` du service :

-   La méthode `GET /v1/synthesize` accepte le texte à synthétiser en tant que paramètre de requête `text` obligatoire. La taille maximale de la demande est de 8 Ko, ce qui inclut le texte d'entrée, tout SSML spécifié, l'URL et les en-têtes.
-   La méthode `POST /v1/synthesize` accepte le texte à synthétiser en tant que construction JSON dans le corps requis de la demande. La taille maximale de la demande est de 8 Ko pour l'URL et les en-têtes et de 5 Ko pour le texte d'entrée envoyé dans le corps de la demande. La limite de 5 Ko inclut tout SSML que vous spécifiez. 

Les deux versions de la méthode `/v1/synthesize` ont les paramètres suivants en commun : 

<table>
  <caption>Tableau 1. Paramètres de la méthode <code>/v1/synthesize</code> </caption>
  <tr>
    <th style="text-align:left; width:18%">Paramètre</th>
    <th style="text-align:center; width:12%">Type</th>
    <th style="text-align:center; width:12%">Type de données</th>
    <th style="text-align:left">Description</th>
  </tr>
  <tr>
    <td><code>accept</code><br/><em>Facultatif</em></td>
    <td style="text-align:center">Requête</td>
    <td style="text-align:center">Chaîne </td>
    <td>
Spécifie le format audio demandé, ou le type MIME, dans lequel le service doit renvoyer l'audio. Vous pouvez également spécifier cette valeur avec l'en-tête de demande HTTP <code>Accept</code>. Codez dans l'URL l'argument vers le paramètre de requête `accept`. Pour plus d'informations, voir [Formats audio](/docs/services/text-to-speech/audio-formats.html).</td>
  </tr>
  <tr>
    <td><code>voice</code><br/><em>Facultatif</em></td>
    <td style="text-align:center">Requête</td>
    <td style="text-align:center">Chaîne </td>
    <td>
Spécifie la voix dans laquelle le texte doit être prononcé en audio. Utilisez la méthode <code>/v1/voices</code> pour obtenir la liste actuelle des voix prises en charge. La voix par défaut est <code>en-US_MichaelVoice</code>. Pour plus d'informations, voir [Langues et voix](/docs/services/text-to-speech/voices.html).
    </td>
  </tr>
  <tr>
    <td><code>customization_id</code><br/><em>Facultatif</em></td>
    <td style="text-align:center">Requête</td>
    <td style="text-align:center">Chaîne </td>
    <td>
Spécifie l'identificateur global unique (GUID) d'un modèle vocal personnalisé à utiliser pour la synthèse. Un modèle vocal personnalisé spécifié ne fonctionne que s'il correspond à la langue de la voix utilisée pour la synthèse. Si vous incluez un ID de personnalisation, vous devez appeler la méthode avec les données d'identification de service du propriétaire du modèle. Omettez le paramètre pour utiliser la voix spécifiée sans personnalisation. Pour plus d'informations, voir [Compréhension de la personnalisation](/docs/services/text-to-speech/custom-intro.html).</td>
  </tr>
</table>

Vous pouvez également utiliser les en-têtes de demande suivants, disponibles pour tous les services {{site.data.keyword.watson}}, avec une demande de synthèse : 

-   `X-Watson-Learning-Opt-Out` indique si le service enregistre les données de demande et de réponse afin d'améliorer le service pour les futurs utilisateurs. Pour empêcher IBM d’accéder à vos données afin d’améliorer les services généraux, indiquez <code>true</code> pour le paramètre. Pour plus d'informations, voir [Contrôle de la journalisation des demandes pour les services {{site.data.keyword.watson}}](/docs/services/watson/getting-started-logging.html).
-   `X-Watson-Metadata` associe un ID client aux données transmises avec une demande. Pour plus d'informations, voir [Sécurité des informations](/docs/services/text-to-speech/information-security.html).

Si vous spécifiez un paramètre de requête ou une zone JSON non valide dans le cadre de l'entrée de la méthode `/v1/synthesize`, le service renvoie un en-tête de réponse `Warnings` qui décrit et répertorie chaque argument non valide. La requête réussit malgré les avertissements.
{: note}

## Spécification de texte en entrée
{: #input}

Les méthodes `GET` et `POST /v1/synthesize` acceptent toutes deux le texte brut ou annoté avec SSML. Les deux versions diffèrent principalement par la manière dont vous spécifiez le texte à synthétiser : 

-   La méthode `GET /v1/synthesize` accepte le texte d'entrée spécifié par le paramètre de requête `text`. Vous spécifiez l'entrée en texte brut ou en texte SSML, qui doivent tous deux être codés dans l'URL. 
-   La méthode `POST /v1/synthesize` accepte le texte saisi dans le corps de la demande. Spécifiez l'entrée avec la construction JSON simple suivante qui encapsule du texte brut ou SSML. Vous devez également spécifier la valeur `application/json` pour l'en-tête `Content-Type`.

    ```javascript
    {
      "text": ""
    }
    ```
    {: codeblock}

Bien que les méthodes `GET` et `POST` offrent des fonctionnalités équivalentes, il est toujours plus sûr de transmettre du texte saisi au service via la méthode `POST`. La demande `POST` transmet une entrée dans le corps de la demande, tandis que la demande `GET` expose les données dans l'URL. 

## Spécification de l'entrée SSML 
{: #ssml-http}

SSML (Speech Synthesis Markup Language) est un langage de balisage basé sur XML conçu pour fournir des annotations de texte aux applications de synthèse vocale telles que le service {{site.data.keyword.texttospeechshort}}. Vous pouvez utiliser des éléments SSML et leurs attributs pour mieux contrôler la synthèse et la sortie audio obtenue. 

Pour plus d'informations sur l'utilisation de SSML pour annoter le texte en entrée, voir [Utilisation de SSML](/docs/services/text-to-speech/SSML.html). La documentation répertorie les éléments et attributs SSML pris en charge par le service. Elle couvre également les extensions d'expressivité et de transformation vocale du service. 

## Mise en échappement des caractères de contrôle XML 
{: #escape}

Dans la mesure où vous pouvez soumettre un texte en entrée comprenant des annotations SSML basées sur XML, le service valide toutes les entrées afin de garantir que tout le SSML est correct et bien formé. Par conséquent, vous devez mettre en échappement tous les caractères de contrôle XML présents dans le texte d'entrée, que l'entrée inclue le SSML ou non. Utilisez les chaînes d'échappement équivalentes ou les codages de caractères du Tableau 2 à la place des caractères indiqués. 

<table style="width:80%">
  <caption>Table 2. Mise en échappement des caractères de contrôle XML </caption>
  <tr>
    <th style="text-align:center; vertical-align:bottom; width:40%">Caractère</th>
    <th style="text-align:center; vertical-align:bottom; width:30%">Chaînes d'échappement</th>
    <th style="text-align:center; vertical-align:bottom; width:30%">Codage des caractères </th>
  </tr>
  <tr>
    <td style="text-align:center"><code>&quot;</code><br/>(guillemets doubles)</td>
    <td style="text-align:center"><code>&amp;quot;</code></td>
    <td style="text-align:center"><code>&amp;#34;</code></td>
  </tr>
  <tr>
    <td style="text-align:center"><code>'</code><br/>(apostrophe ou guillemet simple)</td>
    <td style="text-align:center"><code>&amp;apos;</code></td>
    <td style="text-align:center"><code>&amp;#39;</code></td>
  </tr>
  <tr>
    <td style="text-align:center"><code>&amp;</code><br/>(perluète)</td>
    <td style="text-align:center"><code>&amp;amp;</code></td>
    <td style="text-align:center"><code>&amp;#38;</code></td>
  </tr>
  <tr>
    <td style="text-align:center"><code>&lt;</code><br/>(crochet ouvrant)</td>
    <td style="text-align:center"><code>&amp;lt;</code></td>
    <td style="text-align:center"><code>&amp;#60;</code></td>
  </tr>
  <tr>
    <td style="text-align:center"><code>&gt;</code><br/>(crochet fermant)</td>
    <td style="text-align:center"><code>&amp;gt;</code></td>
    <td style="text-align:center"><code>&amp;#62;</code></td>
  </tr>
</table>

Pour plus d'informations sur la validation du texte saisi par le service, voir [Validation du SSML](/docs/services/text-to-speech/SSML.html#errors).

## Exemples de texte en entrée 
{: #httpExamples}

Les exemples suivants montrent comment spécifier un texte en entrée avec l'une ou l'autre des méthodes de l'interface HTTP. Ils montrent également comment mettre en échappement les caractères de contrôle XML. Les exemples incluent les sauts de ligne pour une meilleure lisibilité. *N'incluez pas* les sauts de ligne dans les entrées réelles. 

### Exemple d'entrée avec une requête GET 
{: #getExamples}

Les exemples suivants transmettent une entrée codée dans l'URL avec le paramètre de requête `text` de la méthode `GET /v1/synthesize` :

-   Entrée en texte brut : 

    ```
    text=This&20is&20the&20first&20sentence&20of&20the&20paragraph.&20Here
    &20is&20another&20sentence.&20Finally,&20this&20is&20the&20last&20sentence.
    ```
    {: codeblock}

-   Entrée SSML :

    ```
    text=%22%3Cp%3E%3Cs%3EThis%20is%20the%20first%20sentence%20of%20the%20%3C
    break%20time=%225s%22/%3E%20paragraph.%3C/s%3E%3Cs%3EHere%20is%20another
    %20sentence.%3C/s%3E%3Cs%3EFinally,%20this%20is%20the%20last%20sentence.
    %3C/s%3E%3C/p%3E%22
    ```
    {: codeblock}

### Exemple d'entrée avec une requête POST 
{: #postExamples}

Les exemples suivants transmettent des entrées dans le corps de la méthode `POST /v1/synthesize` :

-   Entrée en texte brut : 

    ```javascript
    {
      "text": "This is the first sentence of the paragraph. Here is another
        sentence. Finally, this is the last sentence."
    }
    ```
    {: codeblock}

-   Entrée SSML :

    ```javascript
    {
      "text": "<p><s>This is the first sentence of the <break time=\"5s\"/>
        paragraph.</s><s>Here is another sentence.</s><s>Finally, this is
        the last sentence.</s></p>"
    }
    ```
    {: codeblock}

### Exemple d'entrée avec des caractères de contrôle XML 
{: #xmlExamples}

Les exemples suivants envoient deux phrases à la méthode `POST /v1/synthesize`. Les exemples mettent correctement en échappement les caractères XML incorporés. 

```
"Qu'est-ce que j'ai appris ?" a-t-il demandé. "Tout !"
```
{: codeblock}

-   Entrée en texte brut : 

    ```javascript
    {
      "text": "&quot;Qu'est-ce que j'ai appris ?&quot; a-t-il demandé. &quot;Tout !&quot;"
    }
    ```
    {: codeblock}

-   Entrée SSML :

    ```javascript
    {
      "text": "<s>&quot;Qu'est-ce que j'ai appris ?&quot; a-t-il demandé. &quot;<express-as type=\"GoodNews\">Tout!</express-as>&quot;</s>" }
    ```
    {: codeblock}
