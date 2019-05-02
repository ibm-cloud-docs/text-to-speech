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

# Haute disponibilité et récupération après sinistre
{: #ha-dr}

Le service {{site.data.keyword.texttospeechfull}} est hautement disponible sur n'importe quel site {{site.data.keyword.cloud_notm}} (par exemple, Dallas ou Washington, DC). Cependant, la reprise après des incidents potentiels qui affectent un site entier nécessite une planification et une préparation.
{: shortdesc}

Vous êtes responsable de la compréhension de votre configuration, de la personnalisation et de l'utilisation du service. Vous devez également être prêt à recréer une instance du service dans un nouvel emplacement et à restaurer vos données sur n’importe quel site. 

## Haute disponibilité
{: #high-availability}

Le service {{site.data.keyword.texttospeechshort}} prend en charge la haute disponibilité sans point de défaillance unique. Le service atteint automatiquement et de manière transparente la haute disponibilité au moyen de la fonctionnalité de région multizone (MZR) fournie par {{site.data.keyword.cloud_notm}}. 

{{site.data.keyword.cloud_notm}} active plusieurs zones qui ne partagent pas un point de défaillance unique au sein du même site. Il fournit également un équilibrage automatique de la charge entre les zones d'une région. 

## Reprise après incident 
{: #disaster-recovery}

La reprise après incident peut devenir un problème si un site {{site.data.keyword.cloud_notm}} est confronté à un échec important incluant la perte potentielle de données. MZR n'étant pas disponible sur les sites, vous devez attendre qu'{{site.data.keyword.IBM_notm}} remette un site en ligne s'il est indisponible. Si les services de données sous-jacents sont compromis par la défaillance, vous devez également attendre qu'{{site.data.keyword.IBM_notm}} restaure ces services de données. 

En cas de défaillance grave, {{site.data.keyword.IBM_notm}} pourrait ne pas être en mesure de récupérer les données à partir des sauvegardes de la base de données. Dans ce cas, vous devez restaurer vos données pour que votre instance de service revienne à son état le plus récent. Vous pouvez restaurer les données sur le même site ou sur un site différent. 

Pour le service {{site.data.keyword.texttospeechshort}}, seules les données des modèles vocaux personnalisés sont stockées sur {{site.data.keyword.cloud_notm}}. Votre plan de reprise après incident comprend la connaissance, la préservation et la préparation à la restauration de vos modèles vocaux personnalisés. 

### Sauvegarde de modèles vocaux personnalisés 
{: #disaster-recovery-backup}

Conservez les informations suivantes sur vos modèles vocaux personnalisés et leurs entrées personnalisées : 

-   Une liste de tous vos modèles vocaux personnalisés et de leurs définitions. Pour répertorier des informations sur vos modèles personnalisés :
    -   Utilisez la méthode `GET /v1/customizations` pour répertorier des informations sur tous les modèles personnalisés. Pour plus d'informations, voir [Demande de tous les modèles personnalisés](/docs/services/text-to-speech/custom-models.html#cuModelsQueryAll).
    -   Utilisez la méthode `GET /v1/customizations/{customization_id}` pour répertorier des informations sur un modèle personnalisé spécifié. Pour plus d'informations, voir [Demande d'un modèle personnalisé](/docs/services/text-to-speech/custom-models.html#cuModelsQuery).
-   Des informations sur toutes les entrées personnalisées (paires mot/traduction) dans vos modèles vocaux personnalisés : 
    -   Utilisez la méthode `GET /v1/customizations/{customization_id}/words` pour répertorier des informations sur toutes les paires mot/traduction d'un modèle personnalisé. Pour plus d'informations, voir [Demande de tous les mots d'un modèle personnalisé](/docs/services/text-to-speech/custom-entries.html#cuWordsQueryModel).
    -   Utilisez la méthode `GET /v1/customizations/{customization_id}/words/{word}` pour répertorier des informations sur une paire mot/traduction spécifiée à partir d'un modèle personnalisé. Pour plus d'informations, voir [Demande d'un mot à partir d'un modèle personnalisé](/docs/services/text-to-speech/custom-entries.html#cuWordQueryModel).

Il est recommandé de conserver ces informations dans un format que vous pouvez utiliser pour recréer vos modèles vocaux personnalisés en cas de défaillance. Le fait de conserver activement les informations sur vos modèles et vos entrées personnalisés et de préparer à l'avance les appels répertoriés dans la section suivante peut vous permettre d'effectuer une reprise le plus rapidement possible. 

### Restauration de modèles vocaux personnalisés 
{: #disaster-recovery-restore}

Si vous devez effectuer une reprise après incident, vous pouvez utiliser les informations de sauvegarde pour recréer vos modèles vocaux personnalisés et leurs entrées personnalisées : 

1.  Pour recréer vos modèles vocaux personnalisés, utilisez la méthode `POST /v1/customizations`. Pour plus d'informations, voir [Création d'un modèle personnalisé](/docs/services/text-to-speech/custom-models.html#cuModelsCreate).
1.  Pour ajouter plusieurs paires mot/traduction à vos modèles vocaux personnalisés, utilisez la méthode `POST /v1/customizations/{customization_id}/words`. Pour plus d'informations, voir [Ajout de plusieurs mots à un modèle personnalisé](/docs/services/text-to-speech/custom-entries.html#cuWordsAdd).
1.  Pour ajouter une paire mot/traduction à vos modèles vocaux personnalisés, utilisez la méthode `POST /v1/customizations/{customization_id}/words/{word}`. Pour plus d'informations, voir [Ajout d'un mot à un modèle personnalisé](/docs/services/text-to-speech/custom-entries.html#cuWordAdd).

Vous pouvez ajouter toutes vos entrées personnalisées à la fois, groupées, ou une à la fois. 
