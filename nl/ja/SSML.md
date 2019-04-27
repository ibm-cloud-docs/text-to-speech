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

# SSML の使用
{: #ssml}

Speech Synthesis Markup Language (SSML) は、音声合成アプリケーション用のテキストのアノテーションが用意された XML ベースのマークアップ言語です。これは、VoiceXML 2.0 仕様による音声合成の標準マークアップ言語として採用された、W3C Voice-Browser Working Group の勧告です。 SSML は、マークアップを介して発音、音量、ピッチ、速度、およびその他の属性を指定できるので、音声アプリケーションの開発者が合成プロセスの各側面を制御するための標準手段になります。
{: shortdesc}

{{site.data.keyword.texttospeechfull}} サービスでは、SSML を使用して、サポートされているすべての言語のテキストの合成を制御できます。 例えば、SSML の `<phoneme>` 要素を使用すると、International Phonetic Alphabet (IPA) 表記または {{site.data.keyword.IBM_notm}} Symbolic Phonetic Representation (SPR) 表記で単語の発音を定義できます。サービスのカスタム・インターフェースで単語の表音トランスレーションを定義するときにも、SSML の `<phoneme>` 要素を使用します。詳しくは、[カスタマイズの理解](/docs/services/text-to-speech/custom-intro.html)を参照してください。

## SSML の概要
{: #introduction-SSML}

SSML は、事前定義の要素セットまたはタグ・セットを使用して、合成器に渡されるプレーン・テキストを拡張することで動作します。 XML パーサーはまず、プレーン入力テキストとマークアップ指定内容を分離します。 次に、指定内容が処理され、合成器が目的の効果を生成するために理解できる形式の一連の命令として送信されます。 XML パーサーがこのジョブを実行するには、マークアップが適切な形式になっている必要があります。例えば、要素は閉じられている必要があり、また複数の要素がある場合は、適切にネストされている必要があります。 基本的な XML の概念の概要については、[w3schools.com/xml/xml_whatis.asp ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](http://www.w3schools.com/xml/xml_whatis.asp){: new_window} を参照してください。

SSML 要素は、開始タグとそれに対応する閉じタグの内部に含まれているすべての項目です (開始/閉じタグも含む)。 以下の例に示すように、1 つの要素に、他の要素の組み合わせ (タグをネストできます) とテキストを含めることができます。また、要素では、特定の値に設定された属性が必須の場合もあれば、オプションとしてそうした属性を受け入れる場合もあります。

```xml
<tag1>
  <tag2 attributeName="attributeValue">
      ... some text ...
  </tag2>
</tag1>
```
{: codeblock}

完全に正しい SSML 文書は、SSML 文書を検証する際に使用するスキーマやエンコードなどの情報が含まれた XML プロローグと、それに続くルート要素 `<speak>` で構成されます (プロローグの構造について詳しくは、[tizag.com/xmlTutorial/xmlprolog.php ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](http://www.tizag.com/xmlTutorial/xmlprolog.php){: new_window} を参照してください)。`<speak>` 要素の範囲内に合成するテキストを指定し、他の要素を指定して拡張します。

```xml
<!-- XML プロローグ -->
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE speak PUBLIC "-//W3C//DTD SYNTHESIS 1.0//EN"
  "http://www.w3.org/TR/speech-synthesis/synthesis.dtd">

<!-- ルート要素 -->
<speak version="1.0" xmlns="www.w3.org/2001/10/synthesis"
  ... 合成するテキストとマークアップが含まれた本文 ...
</speak>
```
{: codeblock}

サービスは SSML フラグメント (完全な XML ヘッダーが含まれていない SSML 要素) をサポートしています。

## SSML のサポート
{: #ssmlSupport}

{{site.data.keyword.texttospeechshort}} サービスは、SSML バージョン 1.0 のサポートに基づいています。このバージョンは、W3C で 2004 年 9 月 7 日に勧告されました。W3C SSML 勧告について詳しくは、[W3C Speech Synthesis Markup Language (SSML) Version 1.0 ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](http://www.w3.org/TR/speech-synthesis/){: new_window} を参照してください。

サービスで SSML を使用する方法について詳しくは、以下の資料を参照してください。

-   すべての SSML 要素に対するサービスのサポートのレベルについて詳しくは、[SSML 要素](/docs/services/text-to-speech/SSML-elements.html)を参照してください。いくつかの例外を除き、このサービスにはほとんどの W3C 仕様と SSML フラグメントが実装されています。
-   このサービスでは、`<express-as>` 要素を追加して SSML を拡張しています。この要素は、発話時のテキストの感情表出 (Good News (朗報)、Apology (謝罪)、Uncertainty (不安)) を指定します。サービスで感情表出がサポートされるのは、米国英語 Allison 音声のみです。 [感情表出 SSML の使用方法](/docs/services/text-to-speech/SSML-expressive.html)を参照してください。
-   このサービスでは、`<voice-transformation>` 要素を追加して SSML を拡張しています。この要素によって、発話されるテキストのピッチ、ピッチ範囲、声門閉鎖音強度、気息音、速度、および音色を制御することで、使用できる音声の幅を広げられます。サービスには、組み込まれた 2 つの仮想音声 *Young* および *Soft* もあります。 音声変換がサポートされるのは、米国英語の音声のみです。[音声変換 SSML の使用](/docs/services/text-to-speech/SSML-transformation.html)を参照してください。
-   サービスのカスタマイズ・インターフェースでは、単語の発音に使用する表音つづりを指定するために、SSML の `<phoneme>` 要素の使用がサポートされています。表音つづりは、単語の音、音の音節への分割方法、および強勢が置かれる音節を表します。
    -   カスタマイズ・インターフェースについては、[カスタマイズの使用](/docs/services/text-to-speech/custom-intro.html)を参照してください。
    -   サポートされる言語の {{site.data.keyword.IBM_notm}} SPR 表記または IPA 表記で使用できる有効な記号については、[IBM SPR の使用](/docs/services/text-to-speech/SPRs.html)を参照してください。

## SSML 検証
{: #errors}

このサービスでは、合成用の入力テキストまたはカスタマイズ用の単語のトランスレーションの定義としてコンテンツに含めて送信されたすべての SSML 要素が検証されます。サービスは、合成用に送られたテキストに SSML 要素が含まれているかどうかを事前に判別することはできません。 したがって、入力テキストに SSML が含まれているかどうかに関係なく、すべての入力テキストに同じ検証が実行されます。

-   *すべての SSML 入力は、正確かつ適切な形式になっている必要があります。* サービスは、サポートされていない SSML 要素をサイレントに無視します。サポートされない要素や、サポートされない機能を使用している要素の内側のテキストは音声合成されます。要素のみが無視されます。
-   *サービスは、無効な要素に対して HTTP 400 エラー・コードを報告します。*このエラー応答には説明のメッセージが含まれており、要求は失敗します。

具体的には、サービスは以下のような場合にエラーを返します。

-   *無効な要素。*例えば、タグの指定が誤っている、必須属性が省略されている、開始タグが指定されているのに対応する閉じタグがない、などです。
-   *無効な記号。*`<phoneme>` 要素の `ph` 属性に、指定された言語ではサポートされない IPA 記号または SPR 記号が含まれている。
-   *母音がない。* `<phoneme>` 要素の `ph` 属性に、母音のない単語の発音が指定されている。
-   *フランス語のリエゾンの位置が無効である。* `<phoneme>` 要素の `ph` 属性内で、リエゾン文字が子音の後にないか、単語の発音の真ん中にある。
-   *日本語`:` 記号が母音の前にない。* `<phoneme>` 要素の `ph` 属性内で、`:` 記号が母音の前にない (場合によっては、その間に音節境界などの他の記号がある)。
-   *無効な音節の強勢。* {{site.data.keyword.IBM_notm}} SPR の `<phoneme>` 要素の `ph` 属性に、無効な音節の強勢が含まれている。 フランス語の場合、音節の強勢記号が母音の直前にない。 スペイン語またはイタリア語の場合、第二強勢 (`2`) 記号または強勢なし (`0`) 記号が使用されている。 日本語の場合、第二強勢記号 (`2`) が使用されている。
-   *SSML の `<express-as>` 要素または `<voice-transformation>` 要素の無効な使用。*これらの SSML 拡張は、指定された米国英語の音声でのみ使用できます。
-   *SSML の `<prosody>` 要素の無効な使用。*この要素は、`V2` の DNN ベースの音声 (`en-US_AllisonV2Voice` など) では使用できません。
-   *エスケープされていない XML 制御文字。* 入力テキスト自体に、<code>&quot;</code>、<code>&apos;</code>、`&`、`<`、または `>` 文字が、対応するエスケープ・ストリングや文字エンコードではなく、そのまま指定されている。詳しくは、[XML 制御文字のエスケープ](/docs/services/text-to-speech/http.html#escape)を参照してください。
