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

# 高可用性及災難回復
{: #ha-dr}

在任何 {{site.data.keyword.cloud_notm}} 位置（例如，達拉斯或華盛頓特區）內，{{site.data.keyword.texttospeechfull}} 服務都具有高可用性。不過，從影響整個位置的潛在災難回復需要規劃和準備。
{: shortdesc}

您負責瞭解服務的配置、自訂作業和使用情形。您也負責準備好以在新的位置重建服務實例，以及在任何位置還原資料。

## 高可用性
{: #high-availability}

{{site.data.keyword.texttospeechshort}} 服務支援沒有單一失敗點的高可用性。此服務會藉由 {{site.data.keyword.cloud_notm}} 所提供的多區域地區 (MZR) 特性，自動且明確地達到高可用性。

{{site.data.keyword.cloud_notm}} 會啟用未在單一位置內有共同單一失敗點的多個區域。它也在地區內的各個區域之間提供自動的負載平衡。

## 災難回復
{: #disaster-recovery}

如果 {{site.data.keyword.cloud_notm}} 位置遇到包括潛在資料流失的重大失敗，則災難回復可能會變成問題。因為在各個位置都無法使用 MZR，如果位置變成無法使用，您必須等待 {{site.data.keyword.IBM_notm}} 將該位置重新帶回線上。如果失敗導致基礎資料服務受損，則您還必須等待 {{site.data.keyword.IBM_notm}} 還原那些資料服務。

如果發生災難性失敗，{{site.data.keyword.IBM_notm}} 可能無法從資料庫備份回復資料。在此情況下，您需要還原資料，以讓服務實例回復至其最新狀態。您可以將資料還原至相同或不同的位置。

對於 {{site.data.keyword.texttospeechshort}} 服務，只有自訂語音模型的資料才會儲存在 {{site.data.keyword.cloud_notm}} 上。您的災難回復計劃包括了知道、保留及準備還原自訂語音模型。

### 備份自訂語音模型
{: #disaster-recovery-backup}

保留自訂語音模型及其自訂項目的下列相關資訊：

-   所有自訂語音模型及其定義的清單。若要列出自訂模型的相關資訊，請執行下列動作：
    -   使用 `GET /v1/customizations` 方法，列出所有自訂模型的相關資訊。如需相關資訊，請參閱[查詢所有自訂模型](/docs/services/text-to-speech?topic=text-to-speech-customModels#cuModelsQueryAll)。
    -   使用 `GET /v1/customizations/{customization_id}` 方法，列出所指定自訂模型的相關資訊。如需相關資訊，請參閱[查詢自訂模型](/docs/services/text-to-speech?topic=text-to-speech-customModels#cuModelsQuery)。
-   自訂語音模型中所有自訂項目（字組/轉換配對）的相關資訊：
    -   使用 `GET /v1/customizations/{customization_id}/words` 方法，列出自訂模型中所有字組/轉換配對的相關資訊。如需相關資訊，請參閱[從自訂模型查詢所有字組](/docs/services/text-to-speech?topic=text-to-speech-customWords#cuWordsQueryModel)。
    -   使用 `GET /v1/customizations/{customization_id}/words/{word}` 方法，列出自訂模型中所指定字組/轉換配對的相關資訊。如需相關資訊，請參閱[從自訂模型查詢單一字組](/docs/services/text-to-speech?topic=text-to-speech-customWords#cuWordQueryModel)。

最佳作法是以您可以在發生失敗時用來重建自訂語音模型的格式保留此資訊。主動維護自訂模型和自訂項目的相關資訊，並提前準備好下節列出的呼叫，可讓您盡快回復。

### 還原自訂語音模型
{: #disaster-recovery-restore}

如果您需要從災難回復，可以使用備份資訊來重建自訂語音模型及其自訂項目：

1.  若要重建自訂語音模型，請使用 `POST /v1/customizations` 方法。如需相關資訊，請參閱[建立自訂模型](/docs/services/text-to-speech?topic=text-to-speech-customModels#cuModelsCreate)。
1.  若要將多個字組/轉換配對新增至自訂語音模型，請使用 `POST /v1/customizations/{customization_id}/words` 方法。如需相關資訊，請參閱[將多個字組新增至自訂模型](/docs/services/text-to-speech?topic=text-to-speech-customWords#cuWordsAdd)。
1.  若要將單一字組/轉換配對新增至自訂語音模型，請使用 `POST /v1/customizations/{customization_id}/words/{word}` 方法。如需相關資訊，請參閱[將單一字組新增至自訂模型](/docs/services/text-to-speech?topic=text-to-speech-customWords#cuWordAdd)。

您可以用群組方式一次新增所有自訂項目，或一次新增一個。
