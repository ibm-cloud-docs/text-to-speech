---

copyright:
  years: 2015, 2019
lastupdated: "2019-06-04"

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

# Sécurité des informations
{: #information-security}

{{site.data.keyword.IBM}} s'engage à fournir à ses clients et partenaires des solutions innovantes en matière de confidentialité, de sécurité et de gouvernance des données.
{: shortdesc}

Il incombe aux clients de veiller à leur propre conformité aux différentes lois et réglementations, y compris au Règlement général sur la protection des données (RGPD) de l'Union européenne. Il est de la seule responsabilité du client de faire appel à un conseiller juridique compétent pour identifier et interpréter les lois et règlements pertinents, susceptibles d’affecter ses opérations et toutes les actions qu'il pourrait être amené à entreprendre pour se conformer à ces lois et règlements.
{: important}

Les produits, services et autres fonctionnalités décrits dans le présent document ne conviennent pas à toutes les situations client et leur disponibilité peut être limitée. {{site.data.keyword.IBM_notm}} ne fournit ni audit ni conseil juridique, ni déclaration, ni garantie que ses services ou produits assurent au client d'être en conformité avec la loi.

Si vous avez besoin d'une assistance RGPD pour les ressources {{site.data.keyword.cloud}} {{site.data.keyword.watson}} qui sont créées

-   Dans l'Union européenne (UE), voir [Demande de support pour des ressources Watson {{site.data.keyword.cloud_notm}} créées dans l'Union européenne](/docs/services/watson?topic=watson-gdpr-sar#request-EU).
-   Hors UE, voir [Demande de support pour des ressources hors Union européenne](/docs/services/watson?topic=watson-gdpr-sar#request-non-EU).

## Règlement général sur la protection des données (RGPD) de l'Union Européenne
{: #gdpr}

{{site.data.keyword.IBM_notm}} s'engage à fournir à ses clients et partenaires des solutions innovantes en matière de confidentialité, de sécurité et de gouvernance des données pour les aider dans leur processus de mise en conformité avec le RGPD.

Pour en savoir plus sur le processus de préparation au règlement RGPD d'{{site.data.keyword.IBM_notm}} ainsi que sur les fonctionnalités et offres RGPD proposées pour prendre en charge votre processus de conformité, cliquez [ici](http://www.ibm.com/gdpr){: external}.

## Etiquetage et suppression de données dans le service Text to Speech
{: #gdpr-text-to-speech}

Le service {{site.data.keyword.texttospeechfull}} vous permet de supprimer toutes les données associées aux demandes de synthèse vocale et aux modèles vocaux personnalisés. Pour supprimer des données, vous devez procéder comme suit :

1.  Utilisez l'en-tête `X-Watson-Metadata` pour associer un ID client aux données transmises par une demande au service, voir [Spécification d'un ID client](#specify-customer-id).
1.  Utilisez la méthode `DELETE /v1/user_data` pour supprimer toutes les données associées à un ID client spécifié, voir [Suppression de données](#delete-pi).

Par défaut, aucun ID client n'est associé aux données.

Les fonctionnalités expérimentales et bêta ne sont pas destinées à être utilisées dans un environnement de production et ne sont donc pas garanties pour fonctionner comme prévu lors de l'étiquetage et de la suppression de données. Les fonctions expérimentales et bêta ne doivent pas être utilisées lors de l'implémentation d'une solution nécessitant l'étiquetage et la suppression de données.
{: note}

### Spécification d'un ID client
{: #specify-customer-id}

Pour associer un ID client aux données, incluez l'en-tête `X-Watson-Metadata` dans la demande qui transmet les informations. Vous transmettez la chaîne `customer_id={id}` en tant qu'argument de l'en-tête. L'exemple suivant associe l'ID client `my_ID` aux données transmises avec une demande `POST /v1/synthesize` :

```bash
curl -X POST -u "apikey:{apikey}"
--header "X-Watson-Metadata: customer_id=my_ID"
--header "Content-Type: application/json"
--header "Accept: audio/wav"
--data "{\"text\":\"hello world\"}"
--output hello_world.wav
"https://stream.watsonplatform.net/text-to-speech/api/v1/synthesize"
```

Un identifiant client peut inclure n’importe quel caractère sauf `;` (point-virgule) et `=` (signe égal). Spécifiez une chaîne aléatoire ou générique pour l'ID client ; ne spécifiez pas de chaîne identifiable personnellement, telle qu'une adresse électronique ou un identifiant Twitter. Vous pouvez spécifier différents ID de client avec différentes demandes. Un ID client que vous spécifiez est associé à l'instance du service dont les données d'identification sont utilisées avec la demande ; seules les données d'identification de cette instance du service peuvent supprimer les données associées à l'ID.

Utilisez l'en-tête `X-Watson-Metadata` avec les méthodes suivantes :

-   Avec les demandes HTTP :
    -   `POST /v1/synthesize`
    -   `GET /v1/synthesize`

    L'ID client est associé aux données envoyées avec la demande.

-   Avec les demandes WebSocket :
    -   `/v1/synthesize`

    Vous spécifiez l'ID client avec le paramètre de requête `x-watson-metadata` pour associer l'ID aux données envoyées avec la demande. Vous devez coder dans l'URL l'argument associé au paramètre de requête, par exemple, `customer_id%3dmy_ID`.

-   Avec les demandes d’ajout de mots personnalisés à des modèles vocaux personnalisés :
    -   `POST /v1/customizations/{customization_id}`
    -   `POST /v1/customizations/{customization_id}/words`
    -   `PUT /v1/customizations/{customization_id}/words/{word}`

    L'ID client est associé aux mots personnalisés ajoutés ou mis à jour par la demande.

### Suppression des données
{: #delete-pi}

Pour supprimer toutes les données associées à un ID client, utilisez la méthode `DELETE /v1/user_data`. Vous transmettez la chaîne `customer_id={id}` en tant que paramètre de requête avec la demande. L'exemple suivant supprime toutes les données de l'ID client `my_ID` :

```bash
curl -X DELETE -u "apikey:{apikey}"
"https://stream.watsonplatform.net/text-to-speech/api/v1/user_data?customer_id=my_ID"
```

La méthode `/v1/user_data` supprime toutes les données associées à l'ID client spécifié, quelle que soit la méthode utilisée pour ajouter les informations. La méthode n'a aucun effet si aucune donnée n'est associée à l'ID client. Vous devez émettre la demande avec les données d'identification de l'instance du service ayant servi à associer l'ID client aux données.
