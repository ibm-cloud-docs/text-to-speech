---

copyright:
  years: 2015, 2019
lastupdated: "2019-06-06"

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

# IBM SPR の使用
{: #sprs}

{{site.data.keyword.texttospeechfull}} サポートは、単語の音を表すために、標準の International Phonetic Alphabet (IPA) 表記と {{site.data.keyword.IBM}} Symbolic Phonetic Representation (SPR) 表記の両方をサポートしています。 SPR は、単語の発音、単語を構成する音、音の音節への分割方法、および音節の強勢を表す表音コーディングです。 SPR は、IPA の代替表記です。
{: shortdesc}

以下のセクションでは、{{site.data.keyword.IBM_notm}} SPR 表記の概要を説明します。 IPA は標準表記であるため、この資料では IPA の基本的な使用法情報は提供しません。 使用法の簡単な説明については、[IPA の使用法](#ipa)を参照してください。

## IBM SPR の概要
{: #introduction-SPRs}

SPR の発音は、Speech Synthesis Markup Language (SSML) の [phoneme 要素](/docs/services/text-to-speech?topic=text-to-speech-elements#phoneme_element)で定義します。二重引用符で囲まれた、特定の言語の許容される記号のシーケンスで構成されます。 これらの記号を使用して、`<phoneme>` 要素で囲んだ単語の発音を定義します。 この要素の `alphabet` 属性に値 `ibm` を設定して、SPR 表記で発音を定義することを示し、`ph` 属性で発音を定義します。 以下に、米国英語の単語 *through* と *shocking* に対する有効な SPR 表記の例を示します。

```xml
<phoneme alphabet="ibm" ph=".1Tru">through</phoneme>
<phoneme alphabet="ibm" ph=".1Sa.0kIG">shocking</phoneme>
```
{: codeblock}

これらの定義中の `.` (ピリオド) は、新規音節の開始を示します。数字 `1` と `0` は、音節の強勢レベルを示し、文字は米国英語音声の具体的な音を表します。 必要な仕様に準拠していない SPR 項目は無効になります。

## 音節境界

`.` (ピリオド) は、各音節の開始を示すために使用できます。 ただし、言語の有効な表音を保持するために、場合によってはサービスでピリオドが尊重されないことがあります (例えば、音節境界が言語の正しくない位置または不自然な位置に置かれている場合)。 一般に、音響境界またはその他の単語の発音についてユーザーが有効な設定を示すことができる場合は、サービスでそれらの要求が尊重されます。

## 音節の強勢

発音の音節の強勢は、次の表の記号を使用して表せます。 {{site.data.keyword.IBM_notm}} は、SPR と IPA のどちらを使用する場合も、発音の第 1 強勢を指定することをお勧めします。 ただし、どちらのフォーマットについても音節の強勢の指定はオプションです。ユーザーが指定しなければ、サービスが強勢を置く位置を決定します。

<table style="width:80%">
  <caption>表 1. 音節の強勢</caption>
  <tr>
    <th style="width:22%; text-align:center; vertical-align:bottom">
      IBM SPR の記号
    </th>
    <th style="width:22%; text-align:center; vertical-align:bottom">
      IPA の記号
    </th>
    <th style="width:22%; text-align:center; vertical-align:bottom">
      IPA Unicode
    </th>
    <th style="text-align:left; vertical-align:bottom">
      意味
    </th>
  </tr>
  <tr>
    <td style="text-align:center">
      1
    </td>
    <td style="text-align:center">
      <code>&#712;</code>
    </td>
    <td style="text-align:center">
      02C8
    </td>
    <td>
      第 1 強勢
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      2
    </td>
    <td style="text-align:center">
      <code>&#716;</code>
    </td>
    <td style="text-align:center">
      02CC
    </td>
    <td>
      第 2 強勢
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      0
    </td>
    <td style="text-align:center">記号なし</td>
    <td style="text-align:center">値なし</td>
    <td>
      強勢なし
    </td>
  </tr>
</table>

**注:**

-   フランス語の IPA の場合、音節の強勢記号は無視されます。 フランス語の SPR の場合、音節の強勢は無視されません。指定する場合、音節の強勢は音節の母音の直前に置く必要があります。 SPR では、フランス語の音節の強勢は他の言語より大幅に厳密になります。強勢記号が無効な位置に置かれると、エラーが発生します。
-   スペイン語とイタリア語の SPR で指定できるのは、`1` (第 1 強勢) のみです。 第二強勢または強勢なしを指定すると、エラーが発生します。
-   日本語の SPR では、`1` (第一強勢) および `0` (強勢なし) のみがサポートされます。 第二強勢を指定すると、エラーが発生します。

音節強勢マーカーは、音節境界の内側に指定します。必ず、その音節の母音の左に置く必要があります。 このマーカーは、強勢が置かれる母音の左側の任意の位置に配置できます。 例えば、以下の SPR の例はすべて、単語 *construction* の正しい母音に第 1 強勢が置かれます。

```xml
<phoneme alphabet="ibm" ph="kXn1strHkSXn">construction</phoneme>
<phoneme alphabet="ibm" ph="kXns1trHkSXn">construction</phoneme>
<phoneme alphabet="ibm" ph="kXnst1rHkSXn">construction</phoneme>
<phoneme alphabet="ibm" ph="kXnstr1HkSXn">construction</phoneme>
```
{: codeblock}

## 発音記号

各言語では、その言語の発音を表す独自の SPR 記号インベントリーを使用します。 SPR 記号の指定には、以下のルールが適用されます。

-   文字では大/小文字が区別されます。そのため、例えば、`e` と `E` は 2 つの異なる音を表します。
-   2 文字および 3 文字の記号は、単一引用符で囲む必要があります (例えば、ドイツ語の単語 *heim* の記号 `aj` の場合、`"h'aj'm"` とします)。
-   サービスは、言語で許可されない音記号が含まれている SPR 定義はすべて無効と見なします。

単語の発音を SPR フォーマットで定義する場合は、以下の点も考慮してください。

-   各言語の音は、その言語内で特定の分布パターンを持ちます。 例えば、英語のすべての方言では、*sing* (`".1sIG"`) の `G` の音は、語頭に出現することがありません。 特に狭い分布を持つ他の米国英語の音としては、声門閉鎖音 (`?`)、弾音 (`F`)、および撥音 (`N`) があります。 通常は出現しないコンテキストで音記号を入力した場合、結果の音声は不自然に聞こえる可能性があります。
-   {{site.data.keyword.texttospeechshort}} サービスは、高度な言語学のルール・セットを入力に適用し、自然言語の特定のコンテキストで音が変化する際のプロセスを反映します。 例えば、米国英語で、単語 *write* (`".1r1Yt"`) の音 `t` は、*writer* (`".1rY.0FR"`) では弾音 (`F`) として発音されます。 SPR の入力には、通常の入力テキストと同様に、このような変更が適用されます。 この例では、`".1rY.0tR"` と入力しても、`".1rY.0FR"` と入力しても、生成される音声には影響しません。

## IPA の使用法
{: #ipa}

IPA 表記の発音を使用する場合には、以下の情報が適用されます。

-   記載されている IPA 記号のみを使用してください。 1 つの SPR 記号に対して複数の IPA 記号 (または記号の組み合わせ) がリストされている場合は、そのすべてが単一の SPR 記号と同じであるということです。 その場合、サービスはそれらのすべての IPA 記号を同じものとして処理するので、元の IPA 体系で表される微妙な違いや地域的な違いは実現されません。
-   IPA の発音は、IPA Unicode 値として指定することもできます。 次のセクションにリストしている言語別の表に、IPA 記号および記号に対応する IPA Unicode 値の両方を記載しています。 IPA Unicode 値を使用する発音の例については、[phoneme 要素](/docs/services/text-to-speech?topic=text-to-speech-elements#phoneme_element)を参照してください。

詳しくは、以下を参照してください。

-   IPA について詳しくは、[International Phonetic Alphabet](https://wikipedia.org/wiki/International_Phonetic_Alphabet){: external} を参照してください。
-   Unicode の音素記号について詳しくは、[Phonetic symbols in Unicode](https://wikipedia.org/wiki/Phonetic_symbols_in_Unicode){: external} を参照してください。

## サポートされる言語
{: #supportedLanguages}

以下のページに、各言語の SPR 記号、IPA 記号、対応する IPA Unicode 値を記載しています。 言語ごとに各記号を含む単語の例も示しています。 方言差のため、例が常にご使用の発音に一致するわけではありません。

-   [ブラジル・ポルトガル語の記号](/docs/services/text-to-speech?topic=text-to-speech-ptSymbols)
-   [英国英語の記号](/docs/services/text-to-speech?topic=text-to-speech-gbSymbols)
-   [フランス語の記号](/docs/services/text-to-speech?topic=text-to-speech-frSymbols)
-   [ドイツ語の記号](/docs/services/text-to-speech?topic=text-to-speech-deSymbols)
-   [イタリア語の記号](/docs/services/text-to-speech?topic=text-to-speech-itSymbols)
-   [日本語の記号](/docs/services/text-to-speech?topic=text-to-speech-jaSymbols)
-   [スペイン語の記号](/docs/services/text-to-speech?topic=text-to-speech-esSymbols)
-   [米国英語の記号](/docs/services/text-to-speech?topic=text-to-speech-usSymbols)
