---

copyright:
  years: 2015, 2019
lastupdated: "2018-03-07"

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

# カスタム項目作成のルール
{: #rules}

カスタム・モデルへのカスタム項目 (単語/トランスレーションのペア) の設定には、次のルールとガイドラインが適用されます。

## 最大カスタム項目数

単一のカスタム・モデルには、最大で 20,000 個の項目を含められます。

## 文字エンコード

サービスは、*単語* および*トランスレーション* 項目に対して ASCII および  UTF-8 文字エンコードを受け入れます。 トランスレーションについては、SPR 表記を使用する場合は ASCII エンコードを、IPA 表記を使用する場合は UTF-8 エンコードを使用してください。

## 空白文字

*単語* に空白文字を含めることはできません。空白文字は、入力テキスト内の個々の単語を区切るために使用します。

## 大/小文字の区別

*単語* には、大/小文字の区別があります。例えば、カスタム・モデルに `{word='Sun', translation='Sunday'}` という項目が含まれているとします。サービスは、単語 `sun` にはデフォルトの発音を適用しますが、単語 `Sun` にはカスタム・トランスレーションを適用します (後者のみ、先頭文字が大文字であるため)。


## コンテキスト依存性

文脈によって発音が異なる単語があります。例えば、以下の入力文例について考えます。

```
St. Anthony lives on Henry St.
```
{: codeblock}

サービスのデフォルトの発音ルールでは、このテキストは以下のように正しく合成されます。

```
Saint Anthony lives on Henry Street
```
{: codeblock}

一方、ストリング `St.` を `saint` に変換するようにデフォルトの発音ルールをオーバーライドした場合、サービスは文脈に応じた単語の発音を行えなくなります。このようなトランスレーションが含まれたカスタム音声モデルを適用すると、サービスで上記入力文が以下のように発音されるようになります。

```
Saint Anthony lives on Henry saint
```
{: codeblock}

単語/トランスレーションのペアを作成する場合は、このようなケースを考慮してください。

## 末尾のピリオド

サービスがカスタム・モデルの単語を適用するのは、完全に同じ単語のストリングが入力テキスト内に出現した場合のみです。以下に示すように、登録した単語の末尾の `.` (ピリオド) によって、単語の音声合成方法は変わります。

-   *末尾にピリオドがない単語* は、実質的にすべての文字を含めることができます。ここで言う文字には、文字、数字、句読点 (末尾のピリオドは除く)、文字でない記号 (%、&amp;、@ など)、引用符、小括弧、大括弧などが含まれます。*トランスレーション* には、空白文字や SSML フォーマットの表音表記など、サービスに対する任意の正しい入力を含めることができます。
-   *末尾のピリオドがある単語* は、文字、ピリオド、内部のアポストロフィ (先頭文字および末尾文字としては不可) のみを含めることができます。単語の*トランスレーション* には、空白文字またはハイフンで区切った通常のつづりの通常の単語のみを含めることができます。表音表記を含めることはできません。

末尾ピリオドがある単語の例として、「`div.`」があります。 カスタム・モデルに `{word='div.', translation='division'}` という項目が含まれているとします。サービスは、ストリング「`div`」にトランスレーションを適用しません。このストリングには、末尾のピリオドが含まれておらず、項目に一致しないからです。

## IBM SPR 項目の処理
{: #sprNotes}

Symbolic Phonetic Representation (SPR) は、単語の発音を指定するために {{site.data.keyword.IBM_notm}} が開発した、言語に依存する専有のフォーマットです。サポートされる各言語について、SPR には、音素文字、音節境界記号、語彙強勢レベル記号が含まれます。 SPR 項目の作成には、以下の基本ルールが適用されます。

-   単語に対してカスタマイズ・インターフェースから返されるデフォルトの発音は、<code>&#96;</code> (逆引用符) で始まり、`[]` (大括弧) で囲まれています。例えば、このインターフェースは、単語 `tomato` に対して以下の発音を返します。

    ```xml
    `[.0tx.1ma.0to]
    ```
    {: codeblock}

    カスタマイズ・インターフェースのメソッドで単語のトランスレーションを指定する際には、逆引用符と大括弧は省略してください。
-   ピリオドを使用してトランスレーションの音節の開始を示すことができますが、ピリオドはオプションであり、単語の発音には影響しません。 単語のトランスレーションに含めた場合にのみ、単語の発音に表示されます。 音節境界を示すためにスペースを使用しないでください。
-   {{site.data.keyword.IBM_notm}} は、単語の第 1 強勢が置かれる母音の前に記号 `1` を置くことをお勧めします。しかし、これは厳密に必要なわけではありません。ユーザーが指定しない場合は、サービスが強勢を置く位置を決定します。記号 `2` を使用して第 2 強勢の位置を指定することもできますが、この記号 `2` の使用も任意です。単語のトランスレーションに含めた場合にのみ、単語の発音に表示されます。

SPR の使用方法について詳しくは、[IBM SPR の使用](/docs/services/text-to-speech/SPRs.html)を参照してください。

## 日本語の項目の処理
{: #jaNotes}

日本語のカスタム音声モデルの単語の項目を作成する際には、以下の追加のルールと `part_of_speech` フィールドが適用されます。

-   同音異字トランスレーションには*カタカナ* 文字しか含めることができません。 *漢字* および*ひらがな* 文字は許可されません。
-   単語のトランスレーション (同音異字または表音) を作成するときには、オプションの `part_of_speech` フィールドを使用して単語の品詞を指定することもできます。 サービスは、品詞を使用して、単語の正しいイントネーションを生成します。品詞の一覧については、[日本語の品詞](#partsOfSpeech)を参照してください。
-   どの単語についても項目は 1 つしか作成できません。また、単語の品詞は 1 つしか指定できません。同じ単語に対して複数の項目を作成し、異なる品詞 (名詞と動詞など) を指定することはできません。モデル内の既存の単語にトランスレーションを追加すると、その単語の既存のトランスレーション (品詞を含む) が上書きされます。
-   サービスは、カスタム音声モデルに定義されている単語/トランスレーションのペアのうち、一致する最も長い単語を適用します。例えば、カスタム・モデルに以下の 3 つの項目が登録されているとします。

    <pre><code>{
      "words": [
        {
          "word": "&#65326;&#65337;",
          "translation": "&#12491;&#12517;&#12540;&#12520;&#12540;&#12463;",
          "part_of_speech": "Mesi"
        },
        {
          "word": "&#65326;&#65337;&#65315;",
          "translation": "&#12491;&#12517;&#12540;&#12520;&#12540;&#12463;&#12471;&#12486;&#12451;",
          "part_of_speech": "Mesi"
        },
        {
          "word": "&#65337;&#65315;",
          "translation": "&#12520;&#12467;&#12495;&#12510;&#12481;&#12517;&#12540;&#12459;&#12460;&#12452;",
          "part_of_speech": "Mesi"
        }
      ]
    }</code></pre>

    これらの項目が登録されている状態で、サービスが入力テキスト「<code>&#19968;&#36913;&#38291;&#65326;&#65337;&#65315;&#12434;&#35370;&#21839;&#12375;&#12383;</code>」を受け取ったとします。この場合、サービスは、単語 <code>&#65326;&#65337;&#65315;</code> を適用します。<code>&#65326;&#65337;&#65315;</code> が <code>&#65326;&#65337;</code> より長く、<code>&#65326;&#65337;&#65315;</code> が <code>&#65337;&#65315;</code> より先に一致するからです。

### 日本語の品詞
{: #partsOfSpeech}

以下の表に、日本語のカスタム項目でサポートされる品詞をリストします。日本語のカスタム項目の品詞を指定する方法について詳しくは、[日本語のカスタム・モデルへの単語の追加](/docs/services/text-to-speech/custom-entries.html#cuJapaneseAdd)を参照してください。

<table style="width:75%">
  <caption>表 1. 日本語の品詞</caption>
  <tr>
    <th style="text-align:center"><code>part_of_speech</code> の引数</th>
    <th style="text-align:center; width:35%">日本語の意味</th>
    <th style="text-align:center; width:35%">英語の意味</th>
  </tr>
  <tr>
    <td style="text-align:center"><code>Josi</code></td>
    <td style="text-align:center"><em>助詞</em></td>
    <td style="text-align:center">Participle</td>
  </tr>
  <tr>
    <td style="text-align:center"><code>Mesi</code></td>
    <td style="text-align:center"><em>名詞</em></td>
    <td style="text-align:center">Noun</td>
  </tr>
  <tr>
    <td style="text-align:center"><code>Kigo</code></td>
    <td style="text-align:center"><em>記号</em></td>
    <td style="text-align:center">Symbol</td>
  </tr>
  <tr>
    <td style="text-align:center"><code>Gobi</code></td>
    <td style="text-align:center"><em>語尾</em></td>
    <td style="text-align:center">Inflection</td>
  </tr>
  <tr>
    <td style="text-align:center"><code>Dosi</code></td>
    <td style="text-align:center"><em>動詞</em></td>
    <td style="text-align:center">Verb</td>
  </tr>
  <tr>
    <td style="text-align:center"><code>Jodo</code></td>
    <td style="text-align:center"><em>助動詞</em></td>
    <td style="text-align:center">Auxiliary verb</td>
  </tr>
  <tr>
    <td style="text-align:center"><code>Koyu</code></td>
    <td style="text-align:center"><em>固有名詞</em></td>
    <td style="text-align:center">Proper noun</td>
  </tr>
  <tr>
    <td style="text-align:center"><code>Stbi</code></td>
    <td style="text-align:center"><em>接尾辞</em></td>
    <td style="text-align:center">Suffix</td>
  </tr>
  <tr>
    <td style="text-align:center"><code>Suji</code></td>
    <td style="text-align:center"><em>数字</em></td>
    <td style="text-align:center">Numeral</td>
  </tr>
  <tr>
    <td style="text-align:center"><code>Kedo</code></td>
    <td style="text-align:center"><em>形容動詞</em></td>
    <td style="text-align:center">Adjective verb</td>
  </tr>
  <tr>
    <td style="text-align:center"><code>Fuku</code></td>
    <td style="text-align:center"><em>副詞</em></td>
    <td style="text-align:center">Adverb</td>
  </tr>
  <tr>
    <td style="text-align:center"><code>Keyo</code></td>
    <td style="text-align:center"><em>形容詞</em></td>
    <td style="text-align:center">Adjective verb</td>
  </tr>
  <tr>
    <td style="text-align:center"><code>Stto</code></td>
    <td style="text-align:center"><em>接頭辞</em></td>
    <td style="text-align:center">Prefix</td>
  </tr>
  <tr>
    <td style="text-align:center"><code>Reta</code></td>
    <td style="text-align:center"><em>連体詞</em></td>
    <td style="text-align:center">Determiner</td>
  </tr>
  <tr>
    <td style="text-align:center"><code>Stzo</code></td>
    <td style="text-align:center"><em>接続詞</em></td>
    <td style="text-align:center">Conjunction</td>
  </tr>
  <tr>
    <td style="text-align:center"><code>Kato</code></td>
    <td style="text-align:center"><em>間投詞</em></td>
    <td style="text-align:center">Interjection</td>
  </tr>
  <tr>
    <td style="text-align:center"><code>Hoka</code></td>
    <td style="text-align:center"><em>他</em></td>
    <td style="text-align:center">Other</td>
  </tr>
</table>
