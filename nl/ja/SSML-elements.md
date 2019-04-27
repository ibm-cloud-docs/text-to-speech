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

# SSML 要素
{: #elements}

{{site.data.keyword.texttospeechfull}} サービスでは、SSML (Speech Synthesis Markup Language) のほとんどの要素を使用してテキストの音声合成を制御できます。これらの要素は、サポートされているすべての言語で利用できます。以下の表に、このサービスでサポートされる SSML の要素と属性をまとめます。

-   *完全* は、その要素または属性がサービスの HTTP インターフェースおよび WebSocket インターフェースで完全にサポートされていることを意味します。
-   *一部* は、その要素および属性の一部の側面がサービスでサポートされていないことを意味します。また、要素または属性が片方のサービス・インターフェースだけでサポートされていることや、要素または属性が一部の音声ではサポートされていないことを意味する場合もあります。
-   *なし* は、その要素および属性がサービスでサポートされていないことを意味します。

要素または属性について詳しくは、その説明を参照してください。注記があるところは、属性と値のサポートが SSML 仕様とわずかに異なるところです。詳しくは、[W3C Speech Synthesis Markup Language (SSML) Version 1.0 ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](http://www.w3.org/TR/speech-synthesis/){: new_window} を参照してください。

<table>
  <caption>表 1. SSML 要素</caption>
  <tr>
    <th style="text-align:left; width:30%">要素または属性</th>
    <th style="text-align:center; width:12%">サポート</th>
    <th style="text-align:left; width:46%; padding-left:75px">要素または属性</th>
    <th style="text-align:center; width:12%">サポート</th>
  </tr>
  <tr>
    <td>[audio](#audio_element)</td>
    <td style="text-align:center">なし</td>
    <td style="padding-left:75px">[say-as](#say-as_element)</td>
    <td style="text-align:center">一部</td>
  </tr>
  <tr>
    <td>[break](#break_element)</td>
    <td style="text-align:center">完全</td>
    <td style="padding-left:100px">[cardinal](#sayAsCardinal)</td>
    <td style="text-align:center">一部</td>
  </tr>
  <tr>
    <td>[desc](#desc_element)</td>
    <td style="text-align:center">なし</td>
    <td style="padding-left:100px">[date](#sayAsDate)</td>
    <td style="text-align:center">一部</td>
  </tr>
  <tr>
    <td>[emphasis](#emphasis_element)</td>
    <td style="text-align:center">なし</td>
    <td style="padding-left:100px">[digits](#sayAsDigits)</td>
    <td style="text-align:center">一部</td>
  </tr>
  <tr>
    <td>[lexicon](#lexicon_element)</td>
    <td style="text-align:center">なし</td>
    <td style="padding-left:100px">[letters](#sayAsLetters)</td>
    <td style="text-align:center">一部</td>
  </tr>
  <tr>
    <td>[mark](#mark_element)</td>
    <td style="text-align:center">一部</td>
    <td style="padding-left:100px">[number](#sayAsNumber)</td>
    <td style="text-align:center">一部</td>
  </tr>
  <tr>
    <td>[meta](#mm_element)</td>
    <td style="text-align:center">なし</td>
    <td style="padding-left:125px">cardinal</td>
    <td style="text-align:center">一部</td>
  </tr>
  <tr>
    <td>[metadata](#mm_element)</td>
    <td style="text-align:center">なし</td>
    <td style="padding-left:125px">ordinal</td>
    <td style="text-align:center">一部</td>
  </tr>
  <tr>
    <td>[paragraph](#ps_element)</td>
    <td style="text-align:center">完全</td>
    <td style="padding-left:125px">telephone</td>
    <td style="text-align:center">一部</td>
  </tr>
  <tr>
    <td>[phoneme](#phoneme_element)</td>
    <td style="text-align:center">完全</td>
    <td style="padding-left:150px">punctuation</td>
    <td style="text-align:center">一部</td>
  </tr>
  <tr>
    <td style="padding-left:25px">IBM SPR</td>
    <td style="text-align:center">完全</td>
    <td style="padding-left:100px">[ordinal](#sayAsOrdinal)</td>
    <td style="text-align:center">一部</td>
  </tr>
  <tr>
    <td style="padding-left:25px">IPA</td>
    <td style="text-align:center">完全</td>
    <td style="padding-left:100px">[vxml:boolean](#vxml-boolean)</td>
    <td style="text-align:center">一部</td>
  </tr>
  <tr>
    <td>[prosody](#prosody_element)</td>
    <td style="text-align:center">一部</td>
    <td style="padding-left:100px">[vxml:currency](#vxml-currency)</td>
    <td style="text-align:center">一部</td>
  </tr>
  <tr>
    <td style="padding-left:25px">contour</td>
    <td style="text-align:center">なし</td>
    <td style="padding-left:100px">[vxml:date](#vxml-date)</td>
    <td style="text-align:center">一部</td>
  </tr>
  <tr>
    <td style="padding-left:25px">duration</td>
    <td style="text-align:center">なし</td>
    <td style="padding-left:100px">[vxml:digits](#vxml-digits)</td>
    <td style="text-align:center">一部</td>
  </tr>
  <tr>
    <td style="padding-left:25px">[pitch](#prosody-pitch)</td>
    <td style="text-align:center">完全</td>
    <td style="padding-left:100px">[vxml:phone](#vxml-phone)</td>
    <td style="text-align:center">一部</td>
  </tr>
  <tr>
    <td style="padding-left:25px">range</td>
    <td style="text-align:center">なし</td>
    <td style="padding-left:75px">[sentence](#ps_element)</td>
    <td style="text-align:center">完全</td>
  </tr>
  <tr>
    <td style="padding-left:25px">[rate](#prosody-rate)</td>
    <td style="text-align:center">完全</td>
    <td style="padding-left:75px">[speak](#speak_element)</td>
    <td style="text-align:center">完全</td>
  </tr>
  <tr>
    <td style="padding-left:25px">[作成](#prosody-volume)</td>
    <td style="text-align:center">一部</td>
    <td style="padding-left:75px">[sub](#sub_element)</td>
    <td style="text-align:center">完全</td>
  </tr>
  <tr>
    <td></td>
    <td></td>
    <td style="padding-left:75px">[voice](#voice_element)</td>
    <td style="text-align:center">なし</td>
  </tr>
</table>

## audio 要素
{: #audio_element}

この `<audio>` 要素は、録音された要素をサービス生成の音声に挿入します。 サポートされていません。

## break 要素
{: #break_element}

`<break>` 要素は、休止を発話テキストに挿入します。 以下のオプション属性があります。

-   `strength`。強度を示す多様な値を使用して休止の長さを指定します。
    -   `none`: 処理中に生成される可能性がある中断を抑制します。
    -   `x-weak`、`weak`、`medium`、`strong`、または `x-strong`: 右に行くに従って強くなる中断を挿入します。

-   `time`。秒またはミリ秒単位で休止の長さを指定します。 有効な値の形式は、秒の場合は `{integer}s`、ミリ秒の場合は `{integer}ms` です。

```xml
<speak version="1.0">
  Different sized <break strength="none">no pause</break>
  Different sized <break strength="x-weak">x-weak pause</break>
  Different sized <break strength="weak">weak pause</break>
  Different sized <break strength="medium">medium pause</break>
  Different sized <break strength="strong">strong pause</break>
  Different sized <break strength="x-strong">x-strong pause</break>
  Different sized <break time="1s">one-second pause</break>
  Different sized <break time="1500ms">1500-millisecond pause</break>
</speak>
```
{: codeblock}

## desc 要素
{: #desc_element}

`<desc>` 要素は、`<audio>` 要素内にのみ指定できます。`<audio>` 要素はサポートされていないため、`<desc>` 要素もサポートされていません。

## emphasis 要素
{: #emphasis_element}

`<emphasis>` 要素は、囲まれているテキストを強調して発話するように要求します。サポートされていません。

## lexicon 要素
{: #lexicon_element}

この `<lexicon>` 要素は、指定した SSML 文書用の発音辞書を導入します。 サポートされていません。

サービスのカスタマイズ・インターフェースを使用して、音声合成時に使用するカスタム項目 (単語/トランスレーションのペア) の辞書を定義できます。詳しくは、[カスタマイズの理解](/docs/services/text-to-speech/custom-intro.html)を参照してください。

## mark 要素
{: #mark_element}

`<mark>` 要素がサポートされるのは、サービスの WebSocket インターフェースのみです。HTTP インターフェースではサポートされず、この要素は無視されます。 詳しくは、[SSML マークの指定](/docs/services/text-to-speech/word-timing.html#mark)を参照してください。
{: note}

`<mark>` 要素は、合成するテキストにマーカーを配置する空要素です。 `<mark>` 要素の前にあるすべてのテキストが合成されると、クライアントに通知されます。 この要素は、マークを一意的に識別するストリングを指定する単一の `name` 属性を受け入れます。この名前の先頭は英数字にする必要があります。 合成音声内でマークが出現する時間とともに名前が返されます。

```xml
<speak version="1.0">
   Hello <mark name="here"/> world.
</speak>
```
{: codeblock}

## meta 要素および metadata 要素
{: #mm_element}

`<meta>` 要素および `<metadata>` 要素は、文書に関する情報を配置できるコンテナーです。 サポートされていません。

## paragraph 要素および sentence 要素
{: #ps_element}

`<paragraph>` (または `<p>`) および `<sentence>` (または `<s>`) 要素は、テキスト構造に関するヒントを示すために使用できるオプション要素です。`<paragraph>` 要素または `<sentence>` 要素で囲まれているテキストが文末を示す句読点文字 (ピリオドなど) で終わっていない場合、サービスは、通常より長い休止を合成音声に追加します。

どちらの要素も、有効な属性は、言語を切り替えるための `xml:lang` のみです。この属性はサポートされていません。

```xml
<speak version="1.0">
  <paragraph>
    <sentence>Text within a sentence element.</sentence>
    <s>More text in another sentence.</s>
  </paragraph>
</speak>
```
{: codeblock}

## phoneme 要素
{: #phoneme_element}

`<phoneme>` 要素では、囲まれているテキストの表音表記を指定できます。表音つづりによって、単語の音、音を構成する音節、強勢が置かれる音節を表せます。この要素には、以下の 2 つの属性があります。

-   `alphabet`。使用する音韻体系を指定するオプション属性です。 サポートされる表音文字は以下のとおりです。
    -   標準 International Phonetic Alphabet (IPA): `alphabet="ipa"`
    -   {{site.data.keyword.IBM_notm}} Symbolic Phonetic Representation (SPR): `alphabet="ibm"`

表音文字を指定しなかった場合、サービスはデフォルトとして IBM の SPR を使用します。
-   `ph`。指定されている表音文字で発音を指定する必須属性です。 次の例は、*tomato* という単語の発音を両方の形式で表したものです。

    -   IPA 形式の場合

        <pre><code>&lt;speak version="1.0"&gt;
          &lt;phoneme alphabet="ipa" ph="t&#601;&#712;me&#618;.&#638;o&#650;"&gt;tomato&lt;/phoneme&gt;
        &lt;/speak&gt;</code></pre>

    -   IPA 形式でユニコード記号を使用する場合

        <pre><code>&lt;speak version="1.0"&gt;
          &lt;phoneme alphabet="ipa" ph="t&amp;&#35;x259;mei&amp;&#35;x027E;o&amp;&#035;x028A;"&gt;tomato&lt;/phoneme&gt;
        &lt;/speak&gt;</code></pre>

    -   IBM SPR 形式の場合

        <pre><code>&lt;speak version="1.0"&gt;
          &lt;phoneme alphabet="ibm" ph=".0tx.1me.0Fo"&gt;tomato&lt;/phoneme&gt;
        &lt;/speak&gt;</code></pre>

`<phoneme>` 要素で SPR 表記および IPA 表記を使用する方法について詳しくは、[IBM SPR の使用](/docs/services/text-to-speech/SPRs.html)を参照してください。

## prosody 要素
{: #prosody_element}

`<prosody>` 要素は、テキストのピッチ、発話速度、および音量を制御します。 すべての属性がオプションですが、どの属性も指定されていない場合には、エラーが発生します。 SSML 仕様では、サービスでサポートされていない 3 つの属性 `contour`、`range`、および `duration` が使用可能です。 サービスでは、`pitch` 属性、`rate` 属性、および `volume` 属性がサポートされています。

### pitch 属性
{: #prosody-pitch}

`pitch` 属性は、要素内のテキストのベースライン・ピッチを変更します。受け入れられる値は、以下のとおりです。

-   数値と、それに続く `Hz` (Hertz) の指定: ベースライン・ピッチは、指定値に (上または下に) 転調されます。
-   相対的な変更値 (半音単位): 現行ベースラインから絶対シフトを行う数値。数値の前に `+` (上昇) または `-` (下降) を指定し、数値の後に `st` (semitones (半音)) を指定します (`+5st` など)。
-   相対的な変更値 (パーセント): 現行ベースラインから絶対シフトを行う数値。数値の前に `+` (上昇) または `-` (下降) を指定し、数値の後に `%` (パーセント記号) を指定します (`-10%` など)。
-   ピッチを対応する事前定義値に変更する以下の 6 つのキーワードのいずれか:
    -   `default`。サービスのデフォルト・ベースライン・ピッチを使用します。
    -   `x-low`。ピッチ・ベースラインを 12 半音下にシフトします。
    -   `low`。ピッチ・ベースラインを 6 半音下にシフトします。
    -   `medium`。`default` と同じ動作が行われます。
    -   `high`。ピッチ・ベースラインを 6 半音上にシフトします。
    -   `x-high`。ピッチ・ベースラインを 12 半音上にシフトします。

    ```xml
    <speak version="1.0">
      <prosody pitch="150Hz">Transpose pitch to 150 Hz</prosody>
      <prosody pitch="-20Hz">Lower pitch by 20 Hz from baseline</prosody>
      <prosody pitch="+20Hz">Increase pitch by 20 Hz from baseline</prosody>
      <prosody pitch="-12st">Lower pitch by 12 semitones from baseline</prosody>
      <prosody pitch="+12st">Increase pitch by 12 semitones from baseline</prosody>
      <prosody pitch="x-low">Lower pitch by 12 semitones from baseline</prosody>
    </speak>
    ```
    {: codeblock}

### rate 属性
{: #prosody-rate}

`rate` 属性は、要素内のテキストの発話速度の変更を指定します。速度は、単語/分単位で指定します。発話速度が 50 単語/分の場合、`rate` は `50` になります。 `rate` に正数を設定した場合の動作は、現在の W3C の prosody の rate 属性の仕様には準拠していません。また、サービスでは、相対的な変更をパーセントで表す (`+15%` など) ことはできますが、相対的な変更を値で表す (`+15` など) ことはできません。受け入れられる値は、以下のとおりです。

-   相対的なパーセントの増加または減少: `+10%`。
-   正数としての単語/分の数値: `75`。
-   `default`。サービスのデフォルト値を使用します。
-   `x-slow`。速度を 50% 下げます。
-   `slow`。速度を 25% 下げます。
-   `medium`。`default` と同じ動作が行われます。
-   `fast`。速度を 25% 上げます。
-   `x-fast`。速度を 50% 上げます。

```xml
<speak version="1.0">
  <prosody rate="slow">Decrease speaking rate by 25%</prosody>
  <prosody rate="50">Set speaking rate at 50 words per minute</prosody>
  <prosody rate="+5%">Increase speaking rate by 5 percent</prosody>
</speak>
```
{: codeblock}

### volume 属性
{: #prosody-volume}

サービスで DNN ベースの音声 (`en-US_AllisonV2Voice` など) を使用する場合は、`<prosody>` 要素の `volume` 属性はサポートされません。これらの音声について詳しくは、[音声合成テクノロジー](/docs/services/text-to-speech/voices.html#technologiesVoices)を参照してください。
{: note}

`volume` 属性は、要素内のテキストの音量を変更します。1.0 から 100.0 (最大音量) までの範囲の整数または小数の値を指定できます。0 から 100 までの範囲の事前定義設定値に対応する以下のストリング値のいずれかを使用することもできます (`silent` 値はサポートされていません)。

-   `x-soft`。値は 30 です。
-   `soft`。値は 50 です。
-   `medium`。値は 80 です。
-   `loud`。値は 90 です。
-   `default`。値は 92 です。
-   `x-loud`。値は 100 です。

```xml
<speak version="1.0">
  <prosody volume="75">変更後の音量は 75</prosody>
  <prosody volume="88.9">変更後の音量は 88.9</prosody>
  <prosody volume="loud">変更後の音量は 90</prosody>
</speak>
```
{: codeblock}

## say-as 要素
{: #say-as_element}

ほとんどの言語では、`<say-as>` 要素は部分的にしかサポートされていません。米国英語を除き、一般にこの要素の属性としてサポートされるのは、`digits` 属性と `letters` 属性のみです。
{: note}

`<say-as>` 要素には、要素内に含まれているテキストのタイプについての情報を指定し、テキストを発話するときの詳細なレベルを表します。この要素には、1 つの必須属性 `interpret-as` があります。この属性は、囲まれているテキストの解釈方法を指定します。 2 つのオプション属性 `format` および `detail` があります。これらの属性は、以下の例に示すように、`interpret-as` 属性内の特定の値でのみ使用されます。

以下に、`interpret-as` 属性の許容値および各値の例を示します。

### cardinal
{: #sayAsCardinal}

値 `cardinal` を指定すると、要素内の数字が基数として発話されます。以下の例はどちらとも、*Super Bowl forty-nine* と発話されます。最初の例は冗長です。指定してもサービスのデフォルトの動作は変わりません。

```xml
<speak version="1.0">
  Super Bowl <say-as interpret-as="cardinal">49</say-as>
  Super Bowl <say-as interpret-as="cardinal">XLIX</say-as>
</speak>
```
{: codeblock}

### date
{: #sayAsDate}

値 `date` を指定すると、関連する `format` 属性で指定したフォーマットに従って、要素内の日付が発話されます。`format` 属性は、値 `date` には必須です。`format` を指定しなくても、サービスは日付を発音しようとします。以下の例では、指定された日付を指定フォーマットで発話します (ここで、`d`、`m`、および `y` はそれぞれ日、月、および年を表します)。

```xml
<speak version="1.0">
  <say-as interpret-as="date" format="mdy">12/17/2005</say-as>
  <say-as interpret-as="date" format="ymd">2005/12/17</say-as>
  <say-as interpret-as="date" format="dmy">17/12/2005</say-as>
  <say-as interpret-as="date" format="ydm">2005/17/12</say-as>
  <say-as interpret-as="date" format="my">12/2005</say-as>
  <say-as interpret-as="date" format="md">12/17</say-as>
  <say-as interpret-as="date" format="ym">2005/12</say-as>
</speak>
```
{: codeblock}

### digits
{: #sayAsDigits}

値 `digits` を指定すると、要素内の数値に含まれている数字が発話されます。以下の例では、*123456* の数字が 1 つずつ発話されます。

```xml
<speak version="1.0">
  <say-as interpret-as="digits">123456</say-as>
</speak>
```
{: codeblock}

### letters
{: #sayAsLetters}

値 `letters` を指定すると、要素内の単語に含まれている文字が読み上げられます。以下の例では、単語 *hello* を構成する文字が 1 つずつ読み上げられます。

```xml
<speak version="1.0">
  <say-as interpret-as="letters">Hello</say-as>
</speak>
```
{: codeblock}

### number
{: #sayAsNumber}

`number` 値は、`cardinal` 値および `ordinal` 値に代わるものです。オプションの `format` 属性を使用して、一連の数字の解釈方法を指定できます。最初の例は、`format` 属性を省略して、数字を基数値として発音しています。2 番目の例は、数字を `cardinal` 値として発音するように明示的に指定しています。3 番目の例は、数字を `ordinal` 値として発音するように指定しています。

```xml
<speak version="1.0">
  <say-as interpret-as="number">123456</say-as>
  <say-as interpret-as="number" format="cardinal">123456</say-as>
  <say-as interpret-as="number" format="ordinal">123456</say-as>
</speak>
```
{: codeblock}

`format` 属性に値 `telephone` を指定することもできます。一連の数字を電話番号として発音する 2 つの異なる方法を、以下の例で表しています。区切り記号を含めて数字を発音するためには、オプションの `detail` 属性に値 `punctuation` を指定します。

```xml
<speak version="1.0">
  <say-as interpret-as="number" format="telephone">555-555-5555</say-as>
  <say-as interpret-as="number" format="telephone" detail="punctuation">555-555-5555</say-as>
</speak>
```
{: codeblock}

### ordinal
{: #sayAsOrdinal}

値 `ordinal` を指定すると、要素内の数字の序数値が発話されます。以下の例では、*second first* と発話されます。

```xml
<speak version="1.0">
  <say-as interpret-as="ordinal">2</say-as>
  <say-as interpret-as="ordinal">1</say-as>
</speak>
```
{: codeblock}

### vxml:boolean
{: #vxml-boolean}

値 `vxml:boolean` を指定すると、要素内の値が `true` か `false` かに応じて、*yes* または *no* が発話されます。

```xml
<speak version="1.0">
  <say-as interpret-as="vxml:boolean">true</say-as>
  <say-as interpret-as="vxml:boolean">false</say-as>
</speak>
```
{: codeblock}

### vxml:currency
{: #vxml-currency}

値 `vxml:currency` は、通貨値の合成を制御するために使用します。ストリングは `UUUmm.nn` のフォーマットで記述する必要があります。ここで、`UUU` は、ISO 標準 4217 で規定されている 3 文字の通貨標識であり、`mm.nn` は数量です。 以下の例では、*forty-five dollars and thirty cents* と読み上げられます。

```xml
<speak version="1.0">
  <say-as interpret-as="vxml:currency">USD45.30</say-as>
</speak>
```
{: codeblock}

指定した数値の小数点以下の桁数が 3 以上である場合、金額は、10 進数と、それに続く通貨標識として合成されます。 3 文字の通過標識が存在しない場合は、金額は、10 進数としてのみ合成され、通貨タイプは発音されません。 以下の例では、*forty-five point three two nine US dollars* と発話されます。

```xml
<speak version="1.0">
  <say-as interpret-as="vxml:currency">USD45.329</say-as>
</speak>
```
{: codeblock}

### vxml:date
{: #vxml-date}

値 `vxml:date` は、値 `date` と同様に動作しますが、フォーマットは `YYYYMMDD` として事前定義されています。日、月、または年が不明である場合、または日、月、または年を発音しないようにする場合は、その値を `?` (疑問符) に置き換えます。2 番目と 3 番目の例に疑問符が含まれています。

```xml
<speak version="1.0">
  <say-as interpret-as="vxml:date">20050720</say-as>
  <say-as interpret-as="vxml:date">????0720</say-as>
  <say-as interpret-as="vxml:date">200507??</say-as>
</speak>
```
{: codeblock}

### vxml:digits
{: #vxml-digits}

値 `vxml:digits` は、`digits` 値と同じ機能を提供します。

### vxml:phone
{: #vxml-phone}

値 `vxml:phone` を指定すると、数字と区切り記号の両方を含めて電話番号が発話されます。これは、`number` 値を使用して `telephone` (`format` 属性) および `punctuation` (`detail` 属性) を指定することと同じです。

```xml
<speak version="1.0">
  <say-as interpret-as="vxml:phone">555-555-5555</say-as>
</speak>
```
{: codeblock}

## speak 要素
{: #speak_element}

`<speak>` 要素は、SSML 文書のルート要素です。 有効な属性は、以下のとおりです。

-   `version`。SSML 仕様を指定する必須属性です。 受け入れられる値は `1.0` です。
-   `xml:lang`。サービスに必要ありません。 この要素を使用するときはこの属性を省略します。
-   `xml:base`。効果がありません。

```xml
<speak version="1.0">
音声化するテキスト。
</speak>
```
{: codeblock}

## sub 要素
{: #sub_element}

`<sub>` 要素は、音声の合成時に、`alias` 属性で指定したテキストで、要素で囲まれているテキストを置き換えることを指定します。`alias` 属性は、この要素の唯一の属性であり、必須です。

```xml
<speak version="1.0">
  <sub alias="International Business Machines">IBM</sub>
</speak>
```
{: codeblock}

## voice 要素
{: #voice_element}

この `<voice>` 要素は、音声の変更を要求します。 サポートされていません。
