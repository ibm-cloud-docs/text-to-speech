---

copyright:
  years: 2019
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

# 高可用性和灾难恢复
{: #ha-dr}

{{site.data.keyword.texttospeechfull}} 服务在任何 {{site.data.keyword.cloud_notm}} 位置（例如，达拉斯或华盛顿）都具有高可用性。但是，要从影响整个位置的潜在灾难中恢复，需要进行规划和准备。
{: shortdesc}

了解服务的配置、定制和使用情况是您的责任。您还应负责准备好在新位置重新创建服务实例，并在任何位置复原数据。

## 高可用性
{: #high-availability}

{{site.data.keyword.texttospeechshort}} 服务支持高可用性，没有单点故障。服务通过 {{site.data.keyword.cloud_notm}} 提供的多专区区域 (MZR) 功能，自动、透明地实现高可用性。

{{site.data.keyword.cloud_notm}} 支持在单个位置中不共享单点故障的多个专区。它还提供区域内各专区之间的自动负载均衡。

## 灾难恢复
{: #disaster-recovery}

如果 {{site.data.keyword.cloud_notm}} 位置遇到重大故障，包括潜在的数据丢失，那么灾难恢复可能会成为问题。由于 MZR 不能跨位置使用，因此您必须等待 {{site.data.keyword.IBM_notm}} 将不可用的位置恢复为联机状态。如果底层数据服务受到故障影响，那么还必须等待 {{site.data.keyword.IBM_notm}} 复原这些数据服务。

对于灾难性故障，{{site.data.keyword.IBM_notm}} 可能无法从数据库备份恢复数据。在这种情况下，您需要复原数据，以将服务实例恢复为其最新状态。您可以将数据复原到同一位置，也可以复原到其他位置。

对于 {{site.data.keyword.texttospeechshort}} 服务，只有定制声音模型的数据会存储在 {{site.data.keyword.cloud_notm}} 上。因此，您的灾难恢复计划应包括了解和保留定制声音模型的相关信息，并准备好复原定制声音模型。

### 备份定制声音模型
{: #disaster-recovery-backup}

保留有关定制声音模型及其定制条目的以下信息：

-   所有定制声音模型及其定义的列表。要列出有关定制模型的信息：
    -   使用 `GET /v1/customizations` 方法可列出有关所有定制模型的信息。有关更多信息，请参阅[查询所有定制模型](/docs/services/text-to-speech?topic=text-to-speech-customModels#cuModelsQueryAll)。
    -   使用 `GET /v1/customizations/{customization_id}` 方法可列出有关指定定制模型的信息。有关更多信息，请参阅[查询定制模型](/docs/services/text-to-speech?topic=text-to-speech-customModels#cuModelsQuery)。
-   有关定制声音模型中所有定制条目（词/转换项对）的信息：
    -   使用 `GET /v1/customizations/{customization_id}/words` 方法可列出有关定制模型中所有词/转换项对的信息。有关更多信息，请参阅[查询定制模型中的所有词](/docs/services/text-to-speech?topic=text-to-speech-customWords#cuWordsQueryModel)。
    -   使用 `GET /v1/customizations/{customization_id}/words/{word}` 方法可列出有关定制模型中指定词/转换项对的信息。有关更多信息，请参阅[查询定制模型中的单个词](/docs/services/text-to-speech?topic=text-to-speech-customWords#cuWordQueryModel)。

保留这些信息时，最好采用在发生故障时可以用于重新创建定制声音模型的格式。主动维护有关定制模型和定制条目的信息，并提前准备以下部分中列出的调用，能使您尽快实现恢复。

### 复原定制声音模型
{: #disaster-recovery-restore}

如果需要从灾难恢复，您可以使用备份信息来重新创建定制声音模型及其定制条目：

1.  要重新创建定制声音模型，请使用 `POST /v1/customizations` 方法。有关更多信息，请参阅[创建定制模型](/docs/services/text-to-speech?topic=text-to-speech-customModels#cuModelsCreate)。
1.  要向定制声音模型添加多个词/转换项对，请使用 `POST /v1/customizations/{customization_id}/words` 方法。有关更多信息，请参阅[向定制模型添加多个词](/docs/services/text-to-speech?topic=text-to-speech-customWords#cuWordsAdd)。
1.  要向定制声音模型添加单个词/转换项对，请使用 `POST /v1/customizations/{customization_id}/words/{word}` 方法。 有关更多信息，请参阅[向定制模型添加单个词](/docs/services/text-to-speech?topic=text-to-speech-customWords#cuWordAdd)。

您可以一次性添加所有定制条目，也可以分组添加定制条目，或一次添加一个定制条目。
