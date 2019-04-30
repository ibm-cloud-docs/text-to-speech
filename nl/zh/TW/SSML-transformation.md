---

copyright:
  years: 2015, 2019
lastupdated: "2019-04-09"

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

# 語音轉換 SSML
{: #transformation}

{{site.data.keyword.texttospeechfull}} 服務（例如大部分語音合成系統）只能說出有限數目的語音。此外，部分語言只提供一個或兩種語音。為了擴大可能的語音範圍，此服務使用 `<voice-transformation>` 元素來擴充 SSML。您可以使用此元素，藉由控制預設語音的各個層面，來實現不同的虛擬語音。特性的應用程式包括：
{: shortdesc}

-   *將另一個特性提供給語音。* 您想要語音在一般情況下或針對特定應用程序聽起來有一點不同。
-   *語音品牌。* 您想要使用獨特語音來區分您的應用程式。
-   *多重角色應用程式。* 您需要多個語音來代表不同的角色。

您可以將 `<voice-transformation>` 元素套用至整個文字內文、句子、字組或片段。此元素接受一個必要屬性 `type`，其說明要套用至指定文字的語音轉換類型。您可以套用內建轉換，或根據語音的不同層面來建立自訂轉換。

## 語言支援
{: #languages-transformation}

服務僅支援下列美式英文語音的語音轉換：

-   `en-US_AllisonVoice`
-   `en-US_LisaVoice`
-   `en-US_MichaelVoice`

不支援使用 `V2`（這些語音的 DNN 型版本，例如 `en-US_AllisonV2Voice`）進行語音轉換。使用元素與不受支援的語音搭配會傳回錯誤。

## 內建轉換

內建轉換會將預先配置的變更套用至語音屬性。將它們想像成可供服務使用的虛擬語音。服務提供兩個內建轉換。若要使用它們，請使用 `type` 屬性來指定內建轉換的區分大小寫名稱：

-   `Young` 讓語音聽起來朝氣蓬勃。
-   `Soft` 讓語音聽起來較為柔和。

您可以將選用的 `strength` 屬性套用至內建語音，來控制服務套用轉換的範圍。請將此值想像成服務套用至原始語音的混合因素。該屬性接受在 0 到 100% 範圍內的值。指定 `0%` 可讓語音保持不變；指定 `100%` 可達到完整的轉換範圍。如果您省略該屬性，預設強度為 `100%`。

當您使用內建轉換時，服務會忽略自訂轉換的屬性。
{: note}

## 內建轉換範例

下列範例將兩個內建轉換套用至強度不同的相同句子：

```xml
<voice-transformation type="Young" strength="80%">
  Could you provide us with new information?
</voice-transformation>

<voice-transformation type="Soft" strength="60%">
  Could you provide us with new information?
</voice-transformation>
```
{: codeblock}

## 自訂轉換

自訂轉換可讓您更細部控制語音轉換的不同層面。若要使用自訂轉換，請針對 `type` 屬性指定 `Custom`。然後，您可以使用下列一個以上選用屬性來控制轉換。

<table>
  <caption>表 1. 自訂轉換屬性</caption>
  <tr>
    <th style="width:15%; text-align:left">屬性</th>
    <th style="width:25%; text-align:center">範圍</th>
    <th style="text-align:left">說明</th>
  </tr>
  <tr>
    <td><code>pitch</code></td>
    <td style="text-align:center">[-100%, 100%]、<br/>
      [<code>x-low</code>, <code>low</code>, <code>default</code>,
      <code>high</code>, <code>x-high</code>]</td>
    <td>
      平均音高輪廓水平的正規化相對變更在安全限制內。此屬性控制認知的平均語氣水平。它是從 SSML <code>&lt;prosody&gt;</code> 元素的 <code>pitch</code> 屬性借來的。有助於變更認知的說話者身分。
    </td>
  </tr>
  <tr>
    <td><code>pitch_range</code></td>
    <td style="text-align:center">[-100%, 100%]、<br/>
      [<code>x-narrow</code>, <code>narrow</code>, <code>default</code>,
      <code>wide</code>, <code>x-wide</code>]</td>
    <td>
      音高輪廓動態範圍的正規化相對變更在安全限制內。增加或減少音高範圍可讓語音樣式更易或不易表示。此屬性是從 SSML <code>&lt;prosody&gt;</code> 元素的 <code>range</code> 屬性借來的。</td>
  </tr>
  <tr>
    <td><code>glottal_tension</code></td>
    <td style="text-align:center">[-100%, 100%]、<br/>
      [<code>x-low</code>, <code>low</code>, <code>default</code>,
      <code>high</code>, <code>x-high</code>]</td>
    <td>
      聲門張力的正規化相對變更在安全限制內。增加或減少聲門張力被認為是較緊張或鬆弛的語音品質。正值可能會產生嗡嗡聲，舒緩方式為增加 <code>breathiness</code> 屬性的值。負值被認為是較多的呼吸聲，一般是較愉快的。</td>
  </tr>
  <tr>
    <td><code>breathiness</code></td>
    <td style="text-align:center">[-100%, 100%]、<br/>
      [<code>x-low</code>, <code>low</code>, <code>default</code>,
      <code>high</code>, <code>x-high</code>]</td>
    <td>
      認知的呼氣噪音水平的正規化相對變更在安全限制內。極端值可能會產生嘈雜語音（適用於正呼吸聲）或嗡嗡聲（適用於負呼吸聲）。請使用此屬性，來補償由於其他屬性之負面影響所產生的嗡嗡聲或額外噪音。</td>
  </tr>
  <tr>
    <td><code>rate</code></td>
    <td style="text-align:center">[-100%, 100%]、<br/>
      [<code>x-slow</code>, <code>slow</code>, <code>default</code>,
      <code>fast</code>, <code>x-fast</code>]</td>
    <td>
      語音速度的正規化相對變更在安全限制內。增加或減少速度可讓語音更快或更慢。
      正（更快）速度可讓認知的音高範圍更寬，而負（更慢）速度則在感知上縮小音高範圍。
      此屬性是從 SSML <code>&lt;prosody&gt;</code> 元素的 <code>range</code> 屬性借來的。</td>
  </tr>
  <tr>
    <td><code>timbre</code></td>
    <td style="text-align:center">[<code>Sunrise</code>,
      <code>Breeze</code>]</td>
    <td>
      其中一個內建聲道轉換的區分大小寫名稱：<code>Sunrise</code> 或 <code>Breeze</code>。
      名稱是符號。實驗各種音色，以瞭解它們如何影響語音轉換。此屬性有助於變更認知的說話者身分。
    </td>
  </tr>
  <tr>
    <td><code>timbre_extent</code></td>
    <td style="text-align:center">[0%, 100%]</td>
    <td>
      <code>timbre</code> 聲道轉換的範圍：<code>0%</code> 取消轉換；<code>100%</code>
      代表完整應用轉換。此屬性會量化轉換後語音與原始語音之間的差異。它可讓您將選取的音色與原始語音的音色混合。
      即使在適中的音色範圍值內，<code>timbre</code> 屬性仍有助於變更認知的說話者身分。
    </td>
  </tr>
</table>

### 使用範圍
{: #ranges}

不同屬性的數值範圍指出屬性影響語音的範圍。例如，`rate` 屬性具有 -100% 到 100% 的範圍：

-   值 `100%` 不表示語音速度會加快 100%。這表示服務會將語音速度增加至其對該語音容許的上限。
-   值 `-100%` 表示服務會使用其對語音容許的速度下限。
-   值 `0%` 代表語音屬性的原有水平；語音則保持不變。

### 使用文字值
{: #literals}

為了方便起見，許多屬性也會定義可以代替百分比使用的文字值。這些值的意義不同於與 `<prosody>` 元素搭配使用的值。`<voice-transformation>` 元素會在其屬性之間使用一致的比例。

-   `x-low`、`x-slow` 及 `x-narrow` 等於 `-100%` 的值。
-   `low`、`slow` 及 `narrow` 等於 `-50%` 的值。
-   `default` 等於 `0%` 的值，這是屬性及語音的預設值。
-   `high`、`fast` 及 `wide` 等於 `+50%` 的值。
-   `x-high`、`x-fast` 及 `x-wide` 等於 `+100%` 的值。

### 使用準則
{: #guidelines}

請使用下列準則及警告資訊：

-   對於語音品牌或多角色應用程式，請使用 `timbre`、`pitch` 及 `glottal_tension` 屬性來變更認知的說話者身分。您可以使用這三個屬性的組合來建立虛擬語音。將虛擬語音視為多維空間中的一個點，此點是由指定的音色、音高和聲門張力所實現。不同的屬性組合會產生不同的虛擬語音。
-   您可以使用 `pitch_range`、`break` 和 `rate` 屬性，將特性新增至虛擬語音。其他使用者可以選擇相同或類似的屬性值，因此服務無法保證虛擬語音的唯一性。
-   請注意下列在套用屬性時可能產生的負面影響：
    -   高聲門張力、高音高及低速度，每個都可能導致發出嗡嗡聲。請增加呼吸聲來緩解此效果。
    -   極低聲門張力可能會產生嘈雜的語音。請降低呼吸聲來減少噪音。
    -   同時將音高範圍及速度升高或降低至極端程度，可能會讓語音聽起來非常不自然。
-   如上所述，部分屬性是從 SSML `<prosody>` 元素借來的。如需相關資訊，請參閱 [prosody 元素](/docs/services/text-to-speech/SSML-elements.html#prosody_element)。若要啟用虛擬語音的精細韻律控制，您可以：
    -   將 `<prosody>` 元素放在 `<voice-transformation>` 元素內以巢狀化。
    -   將 `<voice-transformation>` 元素放在 `<prosody>` 元素內以巢狀化。

    您*無法* 將 `<voice-transformation>` 元素巢狀化。

## 自訂轉換範例

下列範例會套用不同屬性，來示範自訂轉換的可能應用。第一個範例會降低聲門張力，讓語音聽起來較為柔和。它也會適度地增加音高範圍及速度，以引進較動態的說話樣式。

```xml
<voice-transformation type="Custom" glottal_tension="-50%"
  pitch_range="30%" rate="10%">
  Do you have more information?
</voice-transformation>
```
{: codeblock}

第二個範例使用最大聲門張力和最高音高，以及最低速度。這類組合通常不是偏好的，而且可能會產生嗡嗡聲。此範例會增加呼吸聲來緩解此效果。

```xml
<voice-transformation type="Custom" glottal_tension="100%" pitch="100%"
  rate="-100%" breathiness="60%">
  Do you have more information?
</voice-transformation>
```
{: codeblock}

接下來的兩個範例會套用音色來變更認知的說話者身分。藉由控制混合範圍以及變更音高水平來變更語音。第一個範例使用預設音色範圍，即 100%。

```xml
<voice-transformation type="Custom" timbre="Sunrise" pitch="40%">
  Do you have more information?
</voice-transformation>

<voice-transformation type="Custom" timbre="Breeze" timbre_extent="30%"
  pitch="-30%">
  Do you have more information?
</voice-transformation>
```
{: codeblock}

最終範例使用多個屬性來轉換語音。此範例使用預設音色範圍並省略呼吸聲。

```xml
<voice-transformation type="Custom" timbre="Sunrise" pitch="-30%"
  pitch_range="80%" rate="60%" glottal_tension="-80%">
  Do you have more information?
</voice-transformation>
```
{: codeblock}
