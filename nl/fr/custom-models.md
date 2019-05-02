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

# Création et gestion de modèles vocaux personnalisés 
{: #customModels}

La première étape pour utiliser un modèle personnalisé consiste à en créer un. Une fois le modèle créé, vous pouvez le gérer en interrogeant ou en mettant à jour ses métadonnées et ses entrées, et en le supprimant lorsqu'il devient inutile. Avant de commencer, consultez les informations d'utilisation générale suivantes sur les modèles personnalisés.
{: shortdesc}

## Remarques d'utilisation 
{: #customGuidelines}

Prenez en compte les instructions suivantes lorsque vous utilisez l'interface de personnalisation. 

### Propriété de modèles vocaux personnalisés 
{: #customOwner}

Un modèle vocal personnalisé appartient à l'instance du service {{site.data.keyword.texttospeechshort}} dont les données d'identification sont utilisées pour le créer. Vous devez utiliser les données d'identification du service créées pour cette instance de service avec les méthodes de l'interface de personnalisation afin de pouvoir utiliser le modèle personnalisé de quelque manière que ce soit. 

Toutes les données d'identification de service obtenues pour la même instance du service {{site.data.keyword.texttospeechshort}} partagent l'accès à tous les modèles personnalisés créés pour cette instance de service. Pour limiter l'accès à un modèle personnalisé, créez une instance distincte du service et utilisez uniquement les données d'identification de cette instance de service pour créer et utiliser le modèle. Les données d'identification pour d'autres instances de service ne peuvent pas affecter le modèle personnalisé. 

Un des avantages du partage de la propriété entre les données d'identification du service est que vous pouvez annuler un ensemble de données d'identification, par exemple, si elles sont compromises. Vous pouvez ensuite créer de nouvelles données d'identification pour la même instance de service tout en conservant la propriété et l'accès aux modèles personnalisés créés avec les données d'identification d'origine. 

### Journalisation des demandes et confidentialité des données
{: #customLogging}

La façon dont le service gère la journalisation des demandes pour les appels de l'interface de personnalisation dépend de la demande : 

-   Le service *n'enregistre pas* les données (mots et traductions) utilisées pour créer des modèles vocaux personnalisés. Vous n'avez pas besoin de définir l'en-tête de demande `X-Watson-Learning-Opt-Out` lorsque vous utilisez l'interface de personnalisation pour gérer les mots et les traductions dans un modèle personnalisé. Vos données de formation ne sont jamais utilisées pour améliorer les modèles de base du service. 
-   Le service *enregistre* les données lorsqu'un modèle personnalisé est utilisé avec une demande de synthèse. Vous devez définir l'en-tête de demande `X-Watson-Learning-Opt-Out` sur `true` pour empêcher la journalisation des demandes de synthèse.

Pour plus d'informations, voir [Contrôle de la journalisation des demandes pour les services {{site.data.keyword.watson}}](/docs/services/watson/getting-started-logging.html).

### Sécurité des informations
{: #customSecurity}

Le service vous permet d'associer un ID client aux données ajoutées ou mises à jour pour les modèles vocaux personnalisés. Vous pouvez associer un ID client à des mots personnalisés en transmettant l'en-tête `X-Watson-Metadata` avec les méthodes suivantes :

-   `POST /v1/customizations/{customization_id}`
-   `POST /v1/customizations/{customization_id}/words`
-   `PUT /v1/customizations/{customization_id}/words/{word}`

Si nécessaire, vous pouvez ensuite supprimer les données associées à l'ID client à l'aide de la méthode `DELETE /v1/user_data`. Pour plus d'informations, voir [Sécurité des informations](/docs/services/text-to-speech/information-security.html).

## Création d'un modèle personnalisé
{: #cuModelsCreate}

Pour créer un nouveau modèle personnalisé, utilisez la méthode `POST /v1/customizations`. Un nouveau modèle est toujours vide lors de sa création. Vous devez utiliser d'autres méthodes pour le remplir avec des paires mot/traduction. Le nouveau modèle personnalisé appartient à l'utilisateur dont les données d'identification de service sont utilisées pour le créer. Pour plus d'informations, voir [Propriété des modèles vocaux personnalisés](#customOwner).

Vous transmettez les attributs suivants en tant qu’objet JSON avec le corps de la demande.

<table>
  <caption>Tableau 1. Paramètres de la méthode <code>POST /v1/customizations</code></caption>
  <tr>
    <th style="text-align:left; width:18%">Paramètre</th>
    <th style="text-align:center; width:12%">Type de données</th>
    <th style="text-align:left">Description</th>
  </tr>
  <tr>
    <td><code>name</code><br/><em>Obligatoire</em></td>
    <td style="text-align:center">Chaîne </td>
    <td>
Nom défini par l'utilisateur pour le nouveau modèle personnalisé. Le nom est utilisé pour étiqueter le modèle afin de faciliter son identification. Le nom doit être unique parmi tous les modèles personnalisés que vous possédez. </td>
  </tr>
  <tr>
    <td><code>language</code><br/><em>Facultatif</em></td>
    <td style="text-align:center">Chaîne </td>
    <td>
      Identificateur de la langue du modèle personnalisé. La valeur par défaut est <code>en-US</code> pour l'anglais américain.
    </td>
  </tr>
  <tr>
    <td><code>description</code><br/><em>Facultatif</em></td>
    <td style="text-align:center">Chaîne </td>
    <td>
Description du nouveau modèle. Bien qu'elle soit facultative, une description est vivement recommandée. </td>
  </tr>
</table>

L'exemple de commande `curl` suivant crée un nouveau modèle personnalisé appelé `curl Test`. L'en-tête `Content-Type` identifie le type de l'entrée en tant que `application/json`.

```bash
curl -X POST -u "apikey:{apikey}"
--header "Content-Type: application/json"
--data "{\"name\":\"curl Test\", \"language\":\"en-US\", \"description\":\"Customization test via curl\"}"
"https://stream.watsonplatform.net/text-to-speech/api/v1/customizations"
```
{: pre}

La méthode renvoie un objet JSON contenant un identificateur global unique (GUID) pour le nouveau modèle. L'identificateur global unique (GUID) est utilisé comme paramètre `customization_id` dans les appels d'accès au modèle, tels que ceux permettant d'interroger, de modifier et d'utiliser le modèle et ses mots. 

```javascript
{
  "customization_id": "64f4807f-a5f1-5867-924f-7bba1a84fe97"
}
```
{: codeblock}

## Demande d'un modèle personnalisé 
{: #cuModelsQuery}

Pour demander des informations sur un modèle personnalisé existant, utilisez la méthode `GET /v1/customizations/{customization_id}`. Il s'agit de la méthode la plus directe pour voir toutes les informations sur un modèle, à la fois ses métadonnées et les paires mot/traduction qu'il contient. 

```bash
curl -X GET -u "apikey:{apikey}"
"https://stream.watsonplatform.net/text-to-speech/api/v1/customizations/{customization_id}"
```
{: pre}

La méthode renvoie ses résultats sous forme d'objet JSON sous la forme suivante : 

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

Outre les informations saisies lors de la création du modèle, la sortie inclut les données d'identification du service du propriétaire du modèle, la langue du modèle, l'heure de création du modèle et l'heure de dernière modification. Dans la mesure où le modèle n'a pas été modifié depuis sa création, les deux horodatages de l'exemple sont identiques. 

La sortie inclut également un tableau `words` qui répertorie les entrées personnalisées du modèle. Dans la mesure où le modèle n'a pas encore été mis à jour, le tableau de l'exemple est vide. 

## Demande de tous les modèles personnalisés
{: #cuModelsQueryAll}

Pour afficher des informations sur tous les modèles personnalisés que vous possédez, utilisez la méthode `GET /v1/customizations` :

```bash
curl -X GET -u "apikey:{apikey}"
"https://stream.watsonplatform.net/text-to-speech/api/v1/customizations"
```
{: pre}

La méthode renvoie un tableau JSON qui inclut un objet pour chaque modèle personnalisé appartenant au demandeur. Les données d'identification du service du propriétaire sont affichées dans la zone `owner`. 

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

Les horodatages `created` et `last_modified` pour le premier modèle sont identiques car le modèle n'a pas encore été mis à jour. Les horodatages du deuxième modèle sont différents, ce qui indique qu’il a été modifié depuis sa création. Les informations n'incluent pas les entrées personnalisées définies pour les modèles. 

## Mise à jour d'un modèle personnalisé 
{: #cuModelsUpdate}

Pour mettre à jour des informations sur un modèle personnalisé, utilisez la méthode `POST /v1/customizations/{customization_id}`. Vous spécifiez les mises à jour en tant qu'objet JSON. En plus de modifier son nom et sa description, vous pouvez également utiliser cette méthode pour ajouter ou mettre à jour des paires de mots/traduction dans le modèle. Vous ne pouvez pas changer la langue d'un modèle une fois qu'il est créé. 

L'exemple suivant met à jour le nom et la description d'un modèle personnalisé. Un tableau JSON vide est envoyé avec le paramètre `words` pour indiquer que les entrées du modèle doivent rester inchangées. 

```bash
curl -X POST -u "apikey:{apikey}"
--header "Content-Type: application/json"
--data "{\"name\":\"curl Test Update\", \"description\":\"Customization test update via curl\", \"words\":[]}"
"https://stream.watsonplatform.net/text-to-speech/api/v1/customizations/{customization_id}"
```
{: pre}

Pour plus d'informations sur la mise à jour des mots dans un modèle, voir [Ajout de plusieurs mots à un modèle personnalisé](/docs/services/text-to-speech/custom-entries.html#cuWordsAdd).

## Suppression d'un modèle personnalisé
{: #cuModelsDelete}

Pour supprimer un modèle personnalisé dont vous n'avez plus besoin, utilisez la méthode `DELETE /v1/customizations/{customization_id}`. Utilisez cette méthode uniquement si vous êtes certain de ne plus avoir besoin du modèle, car la suppression est irréversible. 

```bash
curl -X DELETE -u "apikey:{apikey}"
"https://stream.watsonplatform.net/text-to-speech/api/v1/customizations/{customization_id}"
```
{: pre}
