---

copyright:
  years: 2015, 2019
lastupdated: "2019-06-21"

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

# 瞭解自訂作業
{: #customIntro}

當您使用 {{site.data.keyword.texttospeechfull}} 合成文字時，服務會套用和語言有關的發音規則。服務會套用這些規則將每個字組的普通（正寫法）拼字轉換為語音拼字。字組的語音拼字會使用標音符號來定義字組如何發音。這些符號是相異的聲音單位，用來區分語言中的字組、音節之間的界限，以及音節的重音符號。
{: shortdesc}

服務的一般發音規則正常適用於一般字組。不過，它們可能會對不常用的字組產生不完美的結果。這類字組包括含有外來語、個人姓名或地理名稱，以及縮寫或字首語等等的特殊術語。如果應用程式的辭彙包含這類字組，您可以使用自訂作業介面來指定服務對於這類字組如何發音。

自訂作業介面是所有語言都可以使用的測試版功能。您必須具有標準定價方案，才能使用語音模型自訂作業。精簡方案的使用者無法使用自訂作業介面。如需相關資訊，請參閱 {{site.data.keyword.texttospeechshort}} 服務的[定價頁面](https://www.ibm.com/cloud/watson-text-to-speech/pricing){: external}。
{: note}

## 自訂作業的運作方式
{: #ciHow}

{{site.data.keyword.texttospeechshort}} 服務的自訂作業介面會針對特定語言建立字組及其轉換的字典。此字典稱為*自訂語音模型*，或只稱為自訂模型。自訂語音模型中的每個自訂項目都由*字組*/*轉換* 配對所組成。字組的轉換告訴服務在輸入文字中出現該字組時如何發音。

自訂作業介面提供一些方法來建立及管理您的自訂語音模型，而服務會永久儲存這些模型。建立自訂模型之後，就可以在合成期間將其與 `/v1/synthesize` 方法的任何版本搭配使用。當服務合成輸入文字時，它會藉由直接或間接套用自訂模型中出現之字組的轉換，來決定這些字組的發音。由於您為特定語言建立了自訂語音模型，因此自訂模型可搭配以該語言提供的任何語音（標準或神經）使用。

您可以將自訂語音模型中的字組轉換指定為*類似音轉換* 或*語音轉換*。您可以對相同自訂模型中的項目使用這兩種方法，也可以在相同轉換中混合這兩種方法。有若干規則和準則適用於自訂項目。如需相關資訊，請參閱[建立自訂項目的規則](/docs/services/text-to-speech?topic=text-to-speech-rules)。

## 類似音轉換
{: #soundsLike}

*類似音轉換* 會使用服務的一般發音規則，來間接代表目標字組的發音。類似音轉換是由一個以上其他字組的一般發音構成。服務首先會將輸入文字中出現的任何該字組，替換為指定的轉換。然後，將其一般發音規則套用至轉換，將此轉換化為其語音表示法，以取得發音。

例如，服務的一般發音規則會適當地轉換許多常用的縮寫及字首語。服務會將縮寫 *cm* 發音為 *centimeter*。它會針對較不常用的縮寫逐字母地發音。例如，服務會將字串 *Str*（*street* 的縮寫）發音為 *S T R*，每個字母單獨發音。您可以使用類似音方法，為字串 *Str* 指定轉換 *street*。

字首語的另一個範例為字組 *IEEE*，其代表 Institute of Electrical and Electronic Engineers。依預設，服務會將此字首語發音為 *I E E E*。但字首語一般發音為 *I triple E*，您可以藉由使用簡單的類似音轉換 *I triple E* 輕鬆地進行此定義。如果字組 *IEEE* 搭配使用此轉換出現在您的自訂模型中，則服務會將每次出現的該字組替換為此轉換。然後，它會將其一般發音規則套用至個別字組 *I*、*triple* 及 *E* 來產生常用發音。

類似音方法的應用不僅只是縮寫和字首語。它同樣非常適用於複雜或不常用的字組。例如，對於服務的一般發音規則無法完美處理的不常用字組，下列這對類似音轉換可為其產生正確的發音。尋找這類字組的適當轉換，可能比簡單縮寫更具挑戰性。下列轉換使用一般發音規則來變更字組的拼字。

<table style="width:35%">
  <caption>表 1. 類似音轉換範例</caption>
  <tr>
    <th style="text-align:left">字組</th>
    <th style="text-align:left">轉換</th>
  </tr>
  <tr>
    <td>ayurvedic</td>
    <td>aayervedic</td>
  </tr>
  <tr>
    <td>gastroenteritis</td>
    <td>gastro enteritis</td>
  </tr>
</table>

如同這些範例所示，開發類似音轉換可能比公式化需要進行更多的試誤法。您可以根據直覺和經驗，用服務來建立候選轉換。然後，將候選轉換的字組合成為輸入文字，並聆聽產生的音訊。如果此發音符合您的要求，就可以在自訂模型中使用此轉換，否則便修改轉換然後重新測試。

## 語音轉換
{: #phonetic}

類似音方法是一種相對簡單而實用的發音實現方法。但是，不一定都可以開發類似音轉換。直接的替代方案，也就是語音方法，可能看似較複雜且耗時，但它可以實現任何字組的發音。

*語音轉換* 會根據置換服務之一般發音規則的標音符號、音節重音符號及選用性的音節界限，來指定發音。您可以使用下列其中一種格式來指定語音轉換：

-   標準國際音標 (IPA) 表示法
-   專屬的 {{site.data.keyword.IBM_notm}} 符號語音表示法 (SPR)

在任何一種情況下，您都可以使用以「語音合成標記語言 (SSML)」為基礎的特定標音格式來指定轉換。SSML 是 XML 型標記語言，可為語音合成應用程式提供文字註釋。您可以使用 SSML `<phoneme>` 元素，為字組指定語音轉換：

<pre><code>&lt;phoneme alphabet="{ipa | ibm}" ph="{translation}"&gt;&lt;/phoneme&gt;</code></pre>

`alphabet` 屬性指定語音表示法類型：`ipa` 或 `ibm`。`ph` 屬性指定語音轉換字串。

例如，請考量字組 `trinitroglycerin`。服務的一般發音規則會產生與化學家及醫生常用發音不同的發音。正確的發音可以透過語音轉換來實現。

<table style="width:35%">
  <caption>表 2. 語音轉換範例</caption>
  <tr>
    <th style="text-align:left">英文字母</th>
    <th style="text-align:left">轉換</th>
  </tr>
  <tr>
    <td>IPA</td>
    <td>t&#633;a&#618;n&#712;a&#618;t&#633;&#601;gl&#618;s&#601;&#633;&#616;n</td>
  </tr>
  <tr>
    <td>SPR</td>
    <td>trYn1YtrxglIsxrXn</td>
  </tr>
</table>

在這些範例中，語音轉換字串是由標音符號與單一主要重音符號組成。在 IPA 中，主要重音符號是由 <code>&#712;</code> 表示，而在 SPR 中，則是由 `1` 表示。在這兩種情況下，它都放在重母音的符號之前。雖然範例並未顯示它，但是您也可以在語音轉換中指定音節界限和次重音位置。這些元素並非必要，而且通常不是實現發音所需的元素。如同類似音轉換一樣，您可以透過多個以空格分隔的字串來編寫語音轉換。

您也可以將 IPA 轉換指定為 IPA Unicode 值。如需相關資訊，請參閱[使用 IBM SPR](/docs/services/text-to-speech?topic=text-to-speech-sprs)，以及在[支援的語言](/docs/services/text-to-speech?topic=text-to-speech-sprs#supportedLanguages)中所提及頁面上的語言特定表格。如需使用 IPA Unicode 值的轉換範例，請參閱 [phoneme 元素](/docs/services/text-to-speech?topic=text-to-speech-elements#phoneme_element)。
{: note}

### 使用現有的語音轉換
{: #phoneticMethod}

除非您是語音學專家，否則組合語音轉換不是件簡單的作業。編輯現有語音轉換一定比從頭開始組合語音轉換更輕鬆。為了協助您建立語音轉換，服務的 API 包含了一個 `GET /v1/pronunciation` 方法。此方法會針對指定語言中的字組，傳回服務之一般發音規則所產生的 IPA 或 SPR 表示法。您也可以從指定的自訂語音模型要求字組的發音，以查看該模型之語言中的轉換。

您可以使用 `/GET v/1/pronunciation` 方法，來取得字組的起始語音轉換。然後，您可以修改轉換來達到您要的發音。與類似音方法一樣，您要遵循試誤法的處理程序。請將候選轉換提交給服務、將字組合成為輸入文字、聆聽產生的音訊，然後編輯候選轉換。您可以重複此處理程序，直到發音符合您的要求為止。

如需相關資訊，請參閱[從語言查詢字組](/docs/services/text-to-speech?topic=text-to-speech-customWords#cuWordsQueryLanguage)。

### 語音轉換的相關資訊
{: #phoneticInfo}

下列資源提供語音轉換的相關資訊：

-   如需使用 SSML 及其 `<phoneme>` 元素的相關資訊，請參閱[使用 SSML](/docs/services/text-to-speech?topic=text-to-speech-ssml)。
-   如需指定 SPR 轉換及其對等 IPA 符號的相關資訊，請參閱[使用 IBM SPR](/docs/services/text-to-speech?topic=text-to-speech-sprs)。
-   如需使用 IPA 符號的相關資訊，以及這些符號的音訊範例，請參閱 Web 上的來源。您可以在 [International Phonetic Alphabet](https://wikipedia.org/wiki/International_Phonetic_Alphabet){: external} 中找到詳細的介紹性討論。

## 混合的類似音及語音轉換

您可以在相同轉換中混合類似音和語音方法。這個特性可以減少組合轉換時所涉及的工作。

例如，假設您使用類似音方法讓字組的某部分發音令人滿意。但是，您現在需要細部調整字組的其餘元素。您可以使用語音方法，來指定字組的困難層面。下列範例會將混合的轉換套用至字組 `trinitroglycerin`：

<pre><code>try&lt;phoneme alphabet="ipa" ph="n&#712;a&#618;t&#633;&#601;gl&#618;s&#601;&#633;&#616;n"&gt;&lt;/phoneme&gt;</code></pre>
