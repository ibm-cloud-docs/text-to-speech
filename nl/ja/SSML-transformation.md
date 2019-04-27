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

# 音声変換 SSML
{: #transformation}

多くの音声合成システムと同じく、{{site.data.keyword.texttospeechfull}} サービスも発話できる音声の種類が限られています。さらに、一部の言語では用意されている音声は 1 つか 2 つのみです。 使用できる音声の幅を広げるために、このサービスでは `<voice-transformation>` 要素を追加して SSML を拡張しています。この要素を使用すると、デフォルトの音声のさまざまな側面を制御して多様な仮想音声を実現できます。この機能の用途には以下があります。
{: shortdesc}

-   *音声への特色付け。* 全般的または特定の用途のために、音声が少し異なって聞こえるようにする場合。
-   *音声のブランディング。* 用途を差別化するために固有の音声を使用する場合。
-   *複数役の適用。* さまざまな人物を表現するために複数の音声が必要な場合。

`<voice-transformation>` 要素は、テキストの本文全体、文、単語、またはフラグメントに適用できます。 要素は、1 つの必須属性 `type` を受け入れます。この属性では、指定テキストに適用する音声変換タイプを記述します。 組み込みの変換を適用することも、音声のさまざまな部分に基づいてカスタム変換を作成することもできます。

## 言語サポート
{: #languages-transformation}

音声変換は、以下の米国英語音声でのみサポートされています。

-   `en-US_AllisonVoice`
-   `en-US_LisaVoice`
-   `en-US_MichaelVoice`

上記の音声の DNN ベース・バージョンである `V2` (`en-US_AllisonV2Voice` など) では、音声変換はサポートされません。サポートされない音声でこの要素を使用すると、エラーが返されます。

## 組み込み変換

組み込み変換では、音声の属性に事前構成された変更を適用します。 組み込み変換は、このサービスに用意されている仮想音声と考えてください。サービスには 2 つの組み込み変換が用意されています。 これを使用するには、`type` 属性を使用して、大/小文字の区別のある以下の組み込み変換の名前を指定します。

-   `Young`。音声をより若々しい音にします。
-   `Soft`。音声をより柔らかい音にします。

オプションの `strength` 属性をいずれかの組み込み音声に適用すると、サービスが変換を適用する範囲を制御できます。 この値は、サービスが元の音声に適用するブレンド係数と考えてください。 この属性には、0% から 100% までの範囲の値を指定できます。`0%` を指定すると、音声は変更されません。`100%` を指定すると、最大限の変換が実行されます。この属性を省略した場合のデフォルトの strength は、`100%` です。

組み込み変換を使用する場合、サービスではカスタム変換の属性が無視されます。
{: note}

## 組み込み変換の例

以下の例では、2 つの組み込み変換を異なる強さで同じ文に適用しています。

```xml
<voice-transformation type="Young" strength="80%">
  Could you provide us with new information?
</voice-transformation>

<voice-transformation type="Soft" strength="60%">
  Could you provide us with new information?
</voice-transformation>
```
{: codeblock}

## カスタム変換

カスタム変換を使用すると、音声変換のさまざまな要素に対して微細化された制御を行うことができます。 カスタム変換を使用するには、`type` 属性に `Custom` を指定します。 こうすると、以下のオプションの属性を 1 つ以上使用して、変換を制御できます。

<table>
  <caption>表 1. カスタム変換属性</caption>
  <tr>
    <th style="width:15%; text-align:left">属性</th>
    <th style="width:25%; text-align:center">範囲</th>
    <th style="text-align:left">説明</th>
  </tr>
  <tr>
    <td><code>pitch</code></td>
    <td style="text-align:center">[-100%、100%]、<br/>
      [<code>x-low</code>、<code>low</code>、<code>default</code>、
      <code>high</code>、<code>x-high</code>]</td>
    <td>
      安全限度内における平均ピッチ高低レベルの正規化された相対的変動。 この属性は、認識される平均トーン・レベルを制御します。 これは SSML の <code>&lt;prosody&gt;</code> 要素の <code>pitch</code> 属性から借用したものです。認識される話者の個性を変化させるのに役立ちます。
    </td>
  </tr>
  <tr>
    <td><code>pitch_range</code></td>
    <td style="text-align:center">[-100%、100%]、<br/>
      [<code>x-narrow</code>、<code>narrow</code>、<code>default</code>、
      <code>wide</code>、<code>x-wide</code>]</td>
    <td>
      安全限度内におけるピッチ高低のダイナミック・レンジの正規化された相対的変動。 ピッチ範囲を増減すると、音声スタイルの感情表出を強めたり弱めたりすることができます。 この属性は
      SSML の <code>&lt;prosody&gt;</code> 要素の <code>range</code> 属性から
      借用したものです。</td>
  </tr>
  <tr>
    <td><code>glottal_tension</code></td>
    <td style="text-align:center">[-100%、100%]、<br/>
      [<code>x-low</code>、<code>low</code>、<code>default</code>、
      <code>high</code>、<code>x-high</code>]</td>
    <td>
      安全限度内における声門閉鎖音強度の正規化された相対的変動。 声門閉鎖音の強弱は、音声品質の緊張または弛緩として認識されます。 正の値は、ブーンという音を発生させる可能性がありますが、<code>breathiness</code> 属性の値を大きくすると緩和できます。 負の値では気息音が強くなり、一般的により心地よい音と認識されます。
    </td>
  </tr>
  <tr>
    <td><code>breathiness</code></td>
    <td style="text-align:center">[-100%、100%]、<br/>
      [<code>x-low</code>、<code>low</code>、<code>default</code>、
      <code>high</code>、<code>x-high</code>]</td>
    <td>
      安全限度内における気音の認識レベルの正規化された相対的変動。 極端な値にすると、ノイズの多い音声 (正の気息音) またはブーンという音 (負の気息音) が発生する可能性があります。 この属性を使用して、他の属性の副産物として生じるブーンという音や余計なノイズを緩和できます。
    </td>
  </tr>
  <tr>
    <td><code>rate</code></td>
    <td style="text-align:center">[-100%、100%]、<br/>
      [<code>x-slow</code>、<code>slow</code>、<code>default</code>、
      <code>fast</code>、<code>x-fast</code>]</td>
    <td>
      安全限度内における発話速度の正規化された相対的変動。
      速度を増減すると、発話が速くなったり遅くなったりします。
      正の (速い) 速度にすると、認識されるピッチ範囲が広くなり、負の (遅い) 速度にするとピッチ範囲が知覚的に狭くなります。
      この属性は SSML の <code>&lt;prosody&gt;</code> 要素の
      <code>rate</code> 属性から借用したものです。</td>
  </tr>
  <tr>
    <td><code>timbre</code></td>
    <td style="text-align:center">[<code>Sunrise</code>、
        <code>Breeze</code>]</td>
    <td>
      組み込まれた声道変換の大/小文字の区別のある名前。<code>Sunrise</code> または <code>Breeze</code>。
      これらは象徴的な名前です。音声変換にどのような影響を与えるかは、実際に音色を試して確認してください。この属性は、認識される話者の個性を変化させるのに役立ちます。</td>
  </tr>
  <tr>
    <td><code>timbre_extent</code></td>
    <td style="text-align:center">[0%、100%]</td>
    <td>
<code>timbre</code> 声道変換を行う程度。<code>0%</code> にすると変換は取り消され、<code>100%</code> にすると最大限の変換が適用されます。この属性は、変換後の音声と元の音声の違いを定量化するものです。これによって、選択した音色と元の音声の音色をブレンドできます。中程度の音色範囲値でも、<code>timbre</code> 属性は認識される話者の個性を変化させるのに役立ちます。
    </td>
  </tr>
</table>

### 範囲の使用
{: #ranges}

さまざまな属性の数値範囲は、属性が音声に影響を及ぼす範囲を示します。 例えば、`rate` 属性の範囲は -100% から 100% までです。

-   `100%` の値は、音声が 100% 速くなるというわけではありません。サービスが、ある音声で許可される最大値までその音声の速度を上昇させることを意味します。
-   `-100%` の値は、サービスがその音声で許可される最低速度を使用することを意味します。
-   `0%` の値は、その音声の属性に固有のレベルを表します。つまり音声は変更されません。

### リテラル値の使用
{: #literals}

便宜上、多くの属性ではパーセンテージの代わりに使用できるリテラル値も定義されています。 それらの値の意味は、SSML の `<prosody>` 要素で使用される値とは異なります。`<voice-transformation>` 要素では、属性間で一貫したスケールを使用します。

-   `x-low`、`x-slow`、および `x-narrow` は、値 `-100%` と等しい。
-   `low`、`slow`、および `narrow` は、値 `-50%` と等しい。
-   `default` は、その属性および音声のデフォルト値である `0%` と等しい。
-   `high`、`fast`、および `wide` は、値 `+50%` と等しい。
-   `x-high`、`x-fast`、および `x-wide` は、値 `+100%` と等しい。

### 使用ガイドライン
{: #guidelines}

以下のガイドラインと注意事項を考慮してください。

-   音声ブランディングまたは複数役を適用する場合は、`timbre`、`pitch`、および `glottal_tension` の各属性を使用して、認識される話者の個性を変化させます。これらの 3 つの属性を組み合わせて使用すると、仮想音声を作成できます。 仮想音声は、指定された音色、ピッチ、および声門閉鎖音強度で構成される多次元空間内の点であると考えてください。これらの属性をさまざまに組み合わせることで、多様な仮想音声を生成できます。
-   `pitch_range`、`breathiness`、および `rate` の各属性を使用して、仮想音声に特色を追加できます。他のユーザーも同じ属性値または類似した属性値を選択できるので、仮想音声の固有性は保証されません。
-   これらの属性を適用すると以下の副産物が生じる可能性があるので注意してください。
    -   高い声門閉鎖音強度、高いピッチ、および低い速度は、それぞれブーンという音を発生させる可能性があります。 気息音を高くして、影響を緩和してください。
    -   声門閉鎖音強度を極端に低くすると、ノイズ音声が生成される可能性があります。 気息音を低くして、ノイズを減らしてください。
    -   ピッチ範囲および速度を同時に極端に高くしたり低くしたりすると、発話が不自然に聞こえる可能性があります。
-   前述したように、一部の属性は SSML の `<prosody>` 要素から借用されたものです。詳しくは、[prosody 要素](/docs/services/text-to-speech/SSML-elements.html#prosody_element)を参照してください。以下のようにして、仮想音声の韻律を細かく制御することができます。
    -   `<voice-transformation>` 要素内に `<prosody>` 要素をネストする。
    -   `<prosody>` 要素内に `<voice-transformation>` 要素をネストする。

    `<voice-transformation>` 要素をネストすることは*できません*。

## カスタム変換の例

以下の例では、さまざまな属性を適用して、カスタム変換の考えられる応用を示します。 最初の例では、声門閉鎖音強度を低くして音声を柔らかくしています。また、ピッチ範囲および速度を中程度に高めてダイナミックな発話スタイルにしています。

```xml
<voice-transformation type="Custom" glottal_tension="-50%"
  pitch_range="30%" rate="10%">
  Do you have more information?
</voice-transformation>
```
{: codeblock}

2 つ目の例では、声門閉鎖音強度およびピッチを最大にし、速度を最低にしています。 このような組み合わせは一般的に好ましくなく、ブーンという音が発生する可能性があります。 この例では、気息音を高くすることで、影響を和らげています。

```xml
<voice-transformation type="Custom" glottal_tension="100%" pitch="100%"
  rate="-100%" breathiness="60%">
  Do you have more information?
</voice-transformation>
```
{: codeblock}

次の 2 つの例では、音色を適用することで、認識される話者の構成を変化させています。 音声は、ブレンド範囲の制御およびピッチ・レベルの変更によって変更されています。 最初の例では、デフォルトの音色範囲である 100% を使用しています。

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

最後の例では、複数の属性を使用して音声を変換しています。 この例では、デフォルトの音色の程度を使用し、気息音を省略しています。

```xml
<voice-transformation type="Custom" timbre="Sunrise" pitch="-30%"
  pitch_range="80%" rate="60%" glottal_tension="-80%">
  Do you have more information?
</voice-transformation>
```
{: codeblock}
