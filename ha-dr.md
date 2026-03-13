---

copyright:
  years: 2019, 2026
lastupdated: "2026-03-13"

subcollection: text-to-speech

---

{{site.data.keyword.attribute-definition-list}}

# High availability and disaster recovery
{: #ha-dr}

[IBM Cloud]{: tag-ibm-cloud}

The {{site.data.keyword.texttospeechfull}} service is highly available within any {{site.data.keyword.cloud_notm}} location (for example, Dallas or Washington, DC). However, recovering from potential disasters that affect an entire location requires planning and preparation.
{: shortdesc}

You are responsible for understanding your configuration, customization, and usage of the service. You are also responsible for being ready to re-create an instance of the service in a new location and to restore your data in any location.

## High availability
{: #high-availability}

The {{site.data.keyword.texttospeechshort}} service supports high availability with no single point of failure. The service achieves high availability automatically and transparently by means of the multi-zone region (MZR) feature provided by {{site.data.keyword.cloud_notm}}.

{{site.data.keyword.cloud_notm}} enables multiple zones that do not share a single point of failure within a single location. It also provides automatic load balancing across the zones within a region.

## Disaster recovery
{: #disaster-recovery}

Disaster recovery can become an issue if an {{site.data.keyword.cloud_notm}} location experiences a significant failure that includes the potential loss of data. Because MZR is not available across locations, you must wait for {{site.data.keyword.IBM_notm}} to bring a location back online if it becomes unavailable. If underlying data services are compromised by the failure, you must also wait for {{site.data.keyword.IBM_notm}} to restore those data services.

In the event of a catastrophic failure, {{site.data.keyword.IBM_notm}} might not be able to recover data from database backups. In this case, you need to restore your data to return your service instance to its most recent state. You can restore the data to the same or to a different location.

For the {{site.data.keyword.texttospeechshort}} service, only data for custom models, custom words, speaker models, and custom prompts is stored on {{site.data.keyword.cloud_notm}}. Your disaster recovery plan includes knowing, preserving, and being prepared to restore your customization information.

### Backing up custom models and speaker models
{: #disaster-recovery-backup}

Preserve the following information about your custom models, custom entries, speaker models, and custom prompts:

-   A list of all of your custom models and their definitions. To list information about your custom models:
    -   Use the `GET /v1/customizations` method to list information about all custom models. For more information, see [Querying all custom models](/docs/text-to-speech?topic=text-to-speech-customModels#cuModelsQueryAll).
    -   Use the `GET /v1/customizations/{customization_id}` method to list information about a specified custom model. For more information, see [Querying a custom model](/docs/text-to-speech?topic=text-to-speech-customModels#cuModelsQuery).
-   Information about all custom entries (word/translation pairs) in your custom models:
    -   Use the `GET /v1/customizations/{customization_id}/words` method to list information about all word/translation pairs from a custom model. For more information, see [Querying all words from a custom model](/docs/text-to-speech?topic=text-to-speech-customWords#cuWordsQueryModel).
    -   Use the `GET /v1/customizations/{customization_id}/words/{word}` method to list information about a specified word/translation pair from a custom model. For more information, see [Querying a single word from a custom model](/docs/text-to-speech?topic=text-to-speech-customWords#cuWordQueryModel).

It is a best practice to preserve this information in a format that you can use to re-create your customized resources in the event of a failure. Actively maintaining the information, and preparing the calls listed in the following section ahead of time, can enable you to recover as quickly as possible.

### Restoring custom models and speaker models
{: #disaster-recovery-restore}

If you need to recover from a disaster, you can use your backup information to re-create your custom models, custom entries, speaker models, and custom prompts:

1.  To re-create your custom models, use the `POST /v1/customizations` method. For more information, see [Creating a custom model](/docs/text-to-speech?topic=text-to-speech-customModels#cuModelsCreate).
1.  To add multiple word/translation pairs to a custom model, use the `POST /v1/customizations/{customization_id}/words` method. For more information, see [Adding multiple words to a custom model](/docs/text-to-speech?topic=text-to-speech-customWords#cuWordsAdd).
1.  To add a single word/translation pair to a custom model, use the `POST /v1/customizations/{customization_id}/words/{word}` method. For more information, see [Adding a single word to a custom model](/docs/text-to-speech?topic=text-to-speech-customWords#cuWordAdd).

You need to re-create your custom models, speaker models, and custom prompts individually. You can add all of your custom entries to a custom model at once, in groups, or one at a time.
