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

# 声音变换 SSML
{: #transformation}

像大多数语音合成系统一样，{{site.data.keyword.texttospeechfull}} 服务也只能使用有限数量的声音来发音。此外，某些语言仅提供一种或两种声音。为了扩展可能的声音的范围，服务通过 `<voice-transformation>` 元素来扩展 SSML。您可以使用此元素通过控制缺省声音的各个方面来实现不同的虚拟声音。此功能的应用包括：
{: shortdesc}

-   *为声音提供另一种风格*。您希望声音在一般情况下或针对特定应用听起来有一点不同。
-   *声音品牌形象*。您希望使用独特的声音，使您的应用与众不同。
-   *多角色应用*。您需要有多种声音来表示不同的角色。

可以将 `<voice-transformation>` 元素应用于文本的整个主体，也可应用于句子、词或片段。此元素接受一个必需属性 `type`，用于描述要应用于指定文本的声音变换的类型。可以应用内置变换，也可以根据声音的不同方面创建定制变换。

## 语言支持
{: #languages-transformation}

服务仅支持对以下美国英语声音进行声音变换：

-   `en-US_AllisonVoice`
-   `en-US_LisaVoice`
-   `en-US_MichaelVoice`

这些声音的基于 DNN 的 `V2` 版本（例如，`en-US_AllisonV2Voice`）不支持声音变换。将此元素用于不支持的声音会返回错误。

## 内置变换

内置变换会将预配置的更改应用于声音的各个属性。请将其视为服务提供的虚拟声音。服务提供了两种内置变换。要使用这两种变换，请使用 `type` 属性指定内置变换的区分大小写名称：

-   `Young` 使声音听起来更年轻。
-   `Soft` 使声音听起来更柔和。

可以将可选的 `strength` 属性应用于内置声音，以控制服务应用变换的程度。请将值视为服务应用于原始声音的混合因子。此属性接受 0 到 100% 范围内的值。指定 `0%` 会使声音保留不变；指定 `100%` 可实现完全程度的变换。如果省略此属性，缺省 strength 为 `100%`。

使用内置变换时，服务会忽略定制变换的属性。
{: note}

## 内置变换示例

以下示例使用不同的 strength 将两个内置变换应用于同一句子：

```xml
<voice-transformation type="Young" strength="80%">
  Could you provide us with new information?
</voice-transformation>

<voice-transformation type="Soft" strength="60%">
  Could you provide us with new information?
</voice-transformation>
```
{: codeblock}

## 定制变换

通过定制变换，可以对声音变换的不同方面进行更细颗粒度的控制。要使用定制变换，请为 `type` 属性指定 `Custom`。然后，可以使用下列一个或多个可选属性来控制变换。

<table>
  <caption>表 1. 定制变换属性</caption>
  <tr>
    <th style="width:15%; text-align:left">属性</th>
    <th style="width:25%; text-align:center">范围</th>
    <th style="text-align:left">描述</th>
  </tr>
  <tr>
    <td><code>pitch</code></td>
    <td style="text-align:center">[-100%, 100%],<br/>
      [<code>x-low</code>, <code>low</code>, <code>default</code>,
      <code>high</code>, <code>x-high</code>]</td>
    <td>
      在安全限制内，经过规范化的平均音高轮廓级别相对变化。此属性控制感受的平均音调级别。此属性是从 SSML <code>&lt;prosody&gt;</code> 元素的 <code>pitch</code> 属性借用的。它有助于更改感受的说话者身份。
    </td>
  </tr>
  <tr>
    <td><code>pitch_range</code></td>
    <td style="text-align:center">[-100%, 100%],<br/>
      [<code>x-narrow</code>, <code>narrow</code>, <code>default</code>,
      <code>wide</code>, <code>x-wide</code>]</td>
    <td>
      在安全限制内，经过规范化的音高轮廓动态范围相对变化。增大或减小音高范围可提高或降低语音风格的表达性。此属性是从 SSML <code>&lt;prosody&gt;</code> 元素的 <code>range</code> 属性借用的。</td>
  </tr>
  <tr>
    <td><code>glottal_tension</code></td>
    <td style="text-align:center">[-100%, 100%],<br/>
      [<code>x-low</code>, <code>low</code>, <code>default</code>,
      <code>high</code>, <code>x-high</code>]</td>
    <td>
      在安全限制内，经过规范化的喉音张力相对变化。增大或减小喉音张力可感受到音质更紧或更松。正值可能会产生嗡嗡声，您可以通过增大 <code>breathiness</code> 属性的值来缓解此问题。负值感受到的声音带有更多气息，通常感觉更愉快。
    </td>
  </tr>
  <tr>
    <td><code>breathiness</code></td>
    <td style="text-align:center">[-100%, 100%],<br/>
      [<code>x-low</code>, <code>low</code>, <code>default</code>,
      <code>high</code>, <code>x-high</code>]</td>
    <td>
      在安全限制内，经过规范化的感受送气噪声级别的相对变化。极值可能会产生有噪声的语音（对于正值 breathiness）或嗡嗡声（对于负值 breathiness）。使用此属性可补偿因其他属性的副作用而产生的嗡嗡声或额外噪声。
    </td>
  </tr>
  <tr>
    <td><code>rate</code></td>
    <td style="text-align:center">[-100%, 100%],<br/>
      [<code>x-slow</code>, <code>slow</code>, <code>default</code>,
      <code>fast</code>, <code>x-fast</code>]</td>
    <td>
      在安全限制内，经过规范化的语速相对变化。增大或减小 rate 可使语速更快或更慢。rate 为正值（更快）可使感受的音高范围更宽，而 rate 为负值（更慢）可使感受的音高范围更窄。此属性是从 SSML <code>&lt;prosody&gt;</code> 元素的 <code>rate</code> 属性借用的。</td>
  </tr>
  <tr>
    <td><code>timbre</code></td>
    <td style="text-align:center">[<code>Sunrise</code>,
      <code>Breeze</code>]</td>
    <td>
      其中一个内置声道变换的区分大小写名称：<code>Sunrise</code> 或 <code>Breeze</code>。这些名称是象征性的。请对音色进行试验，以了解音色如何影响声音变换。此属性有助于改变感受的说话者身份。
    </td>
  </tr>
  <tr>
    <td><code>timbre_extent</code></td>
    <td style="text-align:center">[0%, 100%]</td>
    <td>
      <code>timbre</code> 声道变换的范围：<code>0%</code> 表示取消变换；<code>100%</code> 表示完全应用变换。此属性用于量化已变换声音与原始声音之间的差异。它支持将所选音色与原始声音的音色进行混合。即使音色范围值为中值段，<code>timbre</code> 属性也有助于更改感受的说话者身份。
    </td>
  </tr>
</table>

### 使用范围
{: #ranges}

不同属性的数值范围指示该属性影响声音的程度。例如，`rate` 属性的范围为 -100% 到 100%：

-   值 `100%` 并不意味着语速会快 100%。而是意味着服务会将语速提高到针对该声音允许的最大语速。
-   值 `-100%` 意味着服务将使用针对该声音允许的最小语速。
-   值 `0%` 表示声音的此属性的固有级别；声音会保持不变。

### 使用字面值
{: #literals}

为了方便起见，许多属性还定义了字面值，您可使用这些字面值，而不使用百分比。这些值的含义与用于 SSML `<prosody>` 元素的相应值的含义不同。`<voice-transformation>` 元素在其属性中使用一致的量程。

-   `x-low`、`x-slow` 和 `x-narrow` 等于值 `-100%`。
-   `low`、`slow` 和 `narrow` 等于值 `-50%`。
-   `default` 等于值 `0%`，即该属性和声音的缺省值。
-   `high`、`fast` 和 `wide` 等于值 `+50%`。
-   `x-high`、`x-fast` 和 `x-wide` 等于值 `+100%`。

### 用法准则
{: #guidelines}

使用以下准则和警告信息：

-   对于声音品牌形象或多角色应用，请使用 `timbre`、`pitch` 和 `glottal_tension` 属性来改变感受的说话者身份。可以使用这三个属性的组合来创建虚拟声音。请将虚拟声音视为多维空间中通过指定的音色、音高和喉音张力实现的点。这些属性的不同组合会生成不同的虚拟声音。
-   可以使用 `pitch_range`、`breathiness` 和 `rate` 属性为虚拟声音添加风格。其他用户可以选择相同或类似的属性值，因此服务无法保证虚拟声音的独特性。
-   请注意，应用属性会产生以下潜在副作用：
    -   喉音张力高、音高大、语速低，都会产生嗡嗡声。增大气息声可减轻此影响。
    -   极低的喉音张力可能会产生有噪声的语音。减小气息声可降低噪声。
    -   同时将音高范围和语速增大或减小到极值，会使语音听起来不自然。
-   请注意，某些属性是从 SSML `<prosody>` 元素中借用的。有关更多信息，请参阅 [prosody 元素](/docs/services/text-to-speech/SSML-elements.html#prosody_element)。要实现对虚拟声音的精细韵律控制，您可以：
    -   在 `<voice-transformation>` 元素内嵌套 `<prosody>` 元素
    -   在 `<prosody>` 元素内嵌套 `<voice-transformation>` 元素

    *不能*嵌套 `<voice-transformation>` 元素。

## 定制变换示例

以下示例应用不同的属性来演示定制变换的可能应用。第一个示例降低了喉音张力，使声音更柔和。此示例还适度增大了音调范围和语速，从而引入了更有活力的说话风格。

```xml
<voice-transformation type="Custom" glottal_tension="-50%"
  pitch_range="30%" rate="10%">
  Do you have more information?
</voice-transformation>
```
{: codeblock}

第二个示例使用最大喉音张力和音高以及最小语速。这种组合通常不大有利，并且可能会产生嗡嗡声。此示例通过增大气息声来缓解此影响。

```xml
<voice-transformation type="Custom" glottal_tension="100%" pitch="100%"
  rate="-100%" breathiness="60%">
  Do you have more information?
</voice-transformation>
```
{: codeblock}

接下来的两个示例通过应用音色来改变感受的说话者身份。通过控制混音程度和更改音高级别来改变声音。第一个示例使用的是缺省音色范围 100%。

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

最后一个示例使用多个属性来变换声音。此示例使用的是缺省音色范围，并省略了气息声。

```xml
<voice-transformation type="Custom" timbre="Sunrise" pitch="-30%"
  pitch_range="80%" rate="60%" glottal_tension="-80%">
  Do you have more information?
</voice-transformation>
```
{: codeblock}
