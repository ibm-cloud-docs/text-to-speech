---

copyright:
  years: 2015, 2019
lastupdated: "2019-03-28"

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

# Langues et voix
{: #voices}

Le service {{site.data.keyword.texttospeechfull}} prend en charge une variété de langues, de voix et de dialectes. Le service offre au moins une voix masculine ou féminine, parfois les deux, pour chaque langue. Chaque voix utilise une cadence et une intonation appropriées pour son dialecte.
{: shortdesc}

## Langues et voix prises en charge
{: #languageVoices}

Le tableau 1 répertorie les voix disponibles pour chaque langue et dialecte, y compris leur genre. Si vous omettez le paramètre facultatif `voice` dans une demande, le service utilise la voix `en-US_MichaelVoice` par défaut. Pour comprendre pourquoi le service propose deux versions de certaines voix, voir [Technologies de synthèse vocale](#technologiesVoices).

Un problème avec le déploiement des voix `V2` provoque actuellement un bruit de fond dans la synthèse vocale. Pour plus d'informations, voir [Limitations connues](/docs/services/text-to-speech/release-notes.html#limitations).
{: note}

<table style="width:90%">
  <caption>Tableau 1. Langues et voix prises en charge </caption>
  <tr>
    <th style="text-align:left">Langue</th>
    <th style="text-align:center">Voix </th>
    <th style="text-align:center">Genre</th>
  </tr>
  <tr>
    <td style="text-align:left">Portugais brésilien </td>
    <td style="text-align:center"><code>pt-BR_IsabelaVoice</code></td>
    <td style="text-align:center">Féminin</td>
  </tr>
  <tr>
    <td style="text-align:left">Espagnol castillan </td>
    <td style="text-align:center"><code>es-ES_EnriqueVoice</code></td>
    <td style="text-align:center">Masculin</td>
  </tr>
  <tr>
    <td></td>
    <td style="text-align:center"><code>es-ES_LauraVoice</code></td>
    <td style="text-align:center">Féminin</td>
  </tr>
  <tr>
    <td style="text-align:left">Français</td>
    <td style="text-align:center"><code>fr-FR_ReneeVoice</code></td>
    <td style="text-align:center">Féminin</td>
  </tr>
  <tr>
    <td style="text-align:left">Allemand </td>
    <td style="text-align:center"><code>de-DE_BirgitVoice</code><br/>
      <code>de-DE_BirgitV2Voice</code></td>
    <td style="text-align:center">Féminin</td>
  </tr>
  <tr>
    <td></td>
    <td style="text-align:center"><code>de-DE_DieterVoice</code><br/>
      <code>de-DE_DieterV2Voice</code></td>
    <td style="text-align:center">Masculin</td>
  </tr>
  <tr>
    <td style="text-align:left">Italien</td>
    <td style="text-align:center"><code>it-IT_FrancescaVoice</code><br/>
      <code>it-IT_FrancescaV2Voice</code></td>
    <td style="text-align:center">Féminin</td>
  </tr>
  <tr>
    <td style="text-align:left">Japonais </td>
    <td style="text-align:center"><code>ja-JP_EmiVoice</code></td>
    <td style="text-align:center">Féminin</td>
  </tr>
  <tr>
    <td style="text-align:left">Espagnol latino-américain</td>
    <td style="text-align:center"><code>es-LA_SofiaVoice</code></td>
    <td style="text-align:center">Féminin</td>
  </tr>
  <tr>
    <td style="text-align:left">Espagnol nord-américain</td>
    <td style="text-align:center"><code>es-US_SofiaVoice</code></td>
    <td style="text-align:center">Féminin</td>
  </tr>
  <tr>
    <td style="text-align:left">Anglais britannique </td>
    <td style="text-align:center"><code>en-GB_KateVoice</code></td>
    <td style="text-align:center">Féminin</td>
  </tr>
  <tr>
    <td style="text-align:left">Anglais américain </td>
    <td style="text-align:center"><code>en-US_AllisonVoice</code><br/>
      <code>en-US_AllisonV2Voice</code></td>
    <td style="text-align:center">Féminin</td>
  </tr>
  <tr>
    <td></td>
    <td style="text-align:center"><code>en-US_LisaVoice</code><br/>
      <code>en-US_LisaV2Voice</code></td>
    <td style="text-align:center">Féminin</td>
  </tr>
  <tr>
    <td></td>
    <td style="text-align:center"><code>en-US_MichaelVoice</code><br/>
      <code>en-US_MichaelV2Voice</code></td>
    <td style="text-align:center">Masculin</td>
  </tr>
</table>

Les voix `es-LA_SofiaVoice` et `es-US_SofiaVoice` sont essentiellement la même voix. La différence la plus significative concerne la façon dont les deux voix interprètent le signe $ (dollar). La version latino-américaine utilise le terme *pesos*, tandis que la version nord-américaine utilise le terme *d&oacute;lares*. D'autres différences mineures pourraient également exister entre les deux voix.
{: note}

### Technologies de synthèse vocale 
{: #technologiesVoices}

Le service met à disposition deux versions de certaines voix, par exemple, `en-US_AllisonVoice` et `en-US_AllisonV2Voice`. La principale différence entre les deux versions reflète la technologie utilisée par le service pour synthétiser la parole : 

-   La *synthèse concaténative* assemble des segments (ou unités) de parole enregistrée pour générer l'audio demandé. Elle génère un audio qui pourrait être considéré comme un son plus net, mais les points de concaténation des segments enregistrés entraînent parfois des distorsions de la parole. 

    Les voix qui n'incluent pas la chaîne `V2` dans leurs noms (par exemple, `en-US_AllisonVoice`) sont basées sur la synthèse concaténative.
-   La *synthèse d'apprentissage en profondeur* utilise un réseau DNN (Deep Neural Network) pour synthétiser la parole avec le texte spécifié. Plutôt que de relier ensemble des segments audio enregistrés, cette approche repose sur l'apprentissage automatique pour former un DNN sur les données de parole enregistrées. La synthèse basée sur l'apprentissage en profondeur ou DNN produit un audio avec une prosodie plus naturelle et une qualité globale plus uniforme. 

    Les voix qui incluent la chaîne `V2` dans leurs noms (par exemple, `en-US_AllisonV2Voice`) sont des voix plus récentes utilisant la synthèse basée sur DNN.

Vous devez expérimenter les nouvelles voix avant de les adopter pour votre application. Les deux technologies produisent un audio avec différentes qualités de signal, de sorte que les nouvelles voix pourraient ne pas être meilleures pour toutes les applications. De plus, les voix basées sur DNN ne prennent pas en charge les éléments ou attributs SSML suivants : 

-   L'attribut `volume` de l'élément `<prosody>`
-   L'élément `<express-as>`
-   L'élément `<voice-transformation>`

Si votre application utilise ces éléments, continuez à utiliser les voix basées sur la synthèse concaténative. 

### Personnalisation de la voix 
{: #customizeVoice}

Lorsque vous synthétisez du texte, le service applique des règles de prononciation dépendantes de la langue pour convertir l'orthographe ordinaire de chaque mot en orthographe phonétique. Les règles de prononciation du service fonctionnent bien pour les mots courants, mais elles peuvent donner des résultats imparfaits pour des mots inhabituels, tels que des termes d'origine étrangère, des noms personnels, des abréviations ou des acronymes. 

Si le lexique de votre application inclut des mots de ce type, vous pouvez utiliser l'interface de personnalisation pour spécifier comment le service les prononce. Pour plus d'informations, voir [Compréhension de la personnalisation](/docs/services/text-to-speech/custom-intro.html).

## Spécification d'une voix
{: #specifyVoice}

Les méthodes HTTP `GET` et `POST /v1/synthesize`, ainsi que la méthode WebSocket `/v1/synthesize`, acceptent un paramètre de requête `voice` facultatif pour spécifier la voix de l'audio synthétisé. Pour plus d'informations, voir [Interface HTTP](/docs/services/text-to-speech/http.html) et [Interface WebSocket](/docs/services/text-to-speech/websockets.html).

Le service base sa compréhension de la langue du texte en entrée sur la voix spécifiée. Veillez à spécifier une voix qui correspond à la langue du texte en entrée. Par exemple, si vous spécifiez la voix française (`fr-FR_ReneeVoice`), le service suppose que le texte en entrée est écrit en français. Si vous transmettez un texte qui n'est pas écrit dans la langue de la voix (par exemple, du texte anglais pour la voix française), le service risque de ne pas produire de résultats significatifs. 

## Affichage de toutes les voix disponibles
{: #listVoices}

La méthode `GET /v1/voices` répertorie les informations relatives à toutes les voix disponibles. Elle ne nécessite aucun argument et renvoie un tableau JSON nommé `voices`. Le tableau comprend un objet distinct pour chaque voix. 

```javascript
{
  "voices": [
    {
      "name": "en-US_LisaVoice",
      "language": "en-US",
      "gender": "female",
      "url": "https://stream.watsonplatform.net/text-to-speech/api/v1/voices/en-US_LisaVoice",
      "description": "Lisa: American English female voice.",
      "customizable": true,
      "supported_features": {
        "voice_transformation": true,
        "custom_pronunciation": true
      }
    },
    . . .
  ]
}
```
{: codeblock}

Les zones des objets vocaux fournissent les informations suivantes : 

-   `name` est un identifiant pour la voix (par exemple, `en-US_LisaVoice`). Indiquez cette valeur pour le paramètre `voice` de la méthode `/v1/synthesize`.
-   `language` spécifie la langue et la région de la voix (par exemple, `en-US`).
-   `gender` identifie la voix comme `male` ou `female`.
-   `url` identifie l'URL pour la voix.
-   `description` fournit une brève description de la voix.
-   `customizable` est une valeur booléenne qui indique si la voix peut être personnalisée avec l'interface de personnalisation du service. (Cette zone, qui fournit les mêmes informations que la zone `custom_pronunciation`, est conservée pour des raisons de compatibilité amont.) 
-   `supported_features` décrit les fonctionnalités de service supplémentaires prises en charge par la voix :
    -   `voice_transformation` est une valeur booléenne qui indique si la voix peut être transformée à l'aide de l'élément `<voice-transformation>` SSML.
    -   `custom_pronunciation` est une valeur booléenne qui indique si la voix peut être personnalisée avec l'interface de personnalisation du service.

## Affichage d'une voix spécifique
{: #listVoice}

La méthode `GET /v1/voices/{voice}` répertorie les informations relatives à une voix spécifique. Elle accepte deux paramètres. 

<table>
  <caption>Tableau 2. Paramètres de la méthode <code>voices</code> </caption>
  <tr>
    <th style="text-align:left; width:18%">Paramètre</th>
    <th style="text-align:center; width:12%">Type</th>
    <th style="text-align:center; width:12%">Type de données</th>
    <th style="text-align:left">Description</th>
  </tr>
  <tr>
    <td><code>voice</code><br/><em>Obligatoire</em></td>
    <td style="text-align:center">Chemin</td>
    <td style="text-align:center">Chaîne </td>
    <td>
      Identifie la voix pour laquelle les informations doivent être renvoyées. Vous spécifiez une voix par son nom (par exemple, <code>en-US_LisaVoice</code>).
    </td>
  </tr>
  <tr>
    <td><code>customization_id</code><br/><em>Facultatif</em></td>
    <td style="text-align:center">Requête</td>
    <td style="text-align:center">Chaîne </td>
    <td>
Fournit l'identificateur global unique (GUID) d'un modèle vocal personnalisé défini pour la voix spécifiée. Si vous incluez un ID de personnalisation, vous devez appeler la méthode avec les données d'identification de service du propriétaire du modèle personnalisé. </td>
  </tr>
</table>

Si vous omettez le paramètre `customization_id`, la méthode renvoie une sortie JSON pour la voix spécifiée, identique aux informations renvoyées pour une voix par la méthode `GET /v1/voices`. Si vous spécifiez `customization_id`, le résultat inclut une zone `customization` contenant des informations sur le modèle vocal personnalisé spécifié. 

```javascript
{
  "name": "en-US_LisaVoice",
  "language": "en-US",
  "gender": "female",
  "url": "https://stream.watsonplatform.net/text-to-speech/api/v1/voices/en-US_LisaVoice",
  "description": "Lisa: American English female voice.",
  "customizable": true,
  "supported_features": {
    "voice_transformation": true,
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

Les attributs de la zone `customization` supplémentaire fournissent des informations telles que l'identificateur global unique (GUID), le nom, la langue et la description du modèle vocal personnalisé. Ils indiquent également les donnée d'identification de service du propriétaire du modèle, la date et l'heure de création du modèle et la date et l'heure de sa dernière modification. 
