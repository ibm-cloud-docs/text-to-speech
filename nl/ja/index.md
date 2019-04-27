---

copyright:
  years: 2015, 2019
lastupdated: "2019-04-08"

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

# 製品情報
{: #about}

> **サービスの更新:** *{{site.data.keyword.texttospeechshort}} サービスは 2019 年 3 月 24 日に更新されました。ドイツ語音声にディープ・ニューラル・ネットワーク (DNN) のバージョンが導入され、また、DNN ベースのすべての音声が SSML 要素 `<prosody>` の `pitch` 属性と `rate` 属性に対応するようになりました。詳しくは、リリース・ノートにある [2019 年 3 月 24 日のサービスの更新](/docs/services/text-to-speech/release-notes.html#March2019c)を参照してください。*

{{site.data.keyword.texttospeechfull}} サービスは、{{site.data.keyword.IBM_notm}} の音声合成機能を使用して、記述テキストを自然に聞こえる音声に変換するアプリケーション・プログラミング・インターフェース (API) を備えています。このサービスでは、遅延を最小限に抑えて、結果がストリーミングでクライアントに戻されます。 このサービスには、[HTTP](/docs/services/text-to-speech/http.html) インターフェースと [WebSocket](/docs/services/text-to-speech/websockets.html) インターフェースの両方が用意されています。

## 特徴および機能

{{site.data.keyword.texttospeechshort}} サービスには以下の特徴と機能があります。

-   **音声フォーマット** - Opus または Vorbis のコーデックを使用する Ogg または WebM、WAV、FLAC、MP3 (MPEG)、l16 (PCM)、mulaw、基本フォーマットの音声を生成します。詳しくは、[音声フォーマット](/docs/services/text-to-speech/audio-formats.html)を参照してください。
-   **音声** - テキストからさまざまな言語、音声、方言による出力を合成します。一部の音声には DNN ベースのバージョンが用意されています。詳しくは、[言語と音声](/docs/services/text-to-speech/voices.html)を参照してください。
-   **SSML** - プレーン・テキストまたは XML ベースの Speech Synthesis Markup Language (SSML) でマークアップしたテキストを取ります。詳しくは、[SSML の使用](/docs/services/text-to-speech/SSML.html)を参照してください。
-   **感情表出** - 感情表出要素を使用して SSML を拡張できます。この要素には、*GoodNews* (朗報)、*Apology* (謝罪)、*Uncertainty* (不安) の発話スタイルを指定できます。DNN ベースではない米国英語の Allison の音声でのみ利用できます。詳しくは、[感情表出 SSML](/docs/services/text-to-speech/SSML-expressive.html) を参照してください。
-   **音声変換** - 音声変換要素を追加して SSML を拡張できます。この要素を使用して、ピッチ、速度、音色などの側面を制御することで、使用できる音声の幅を広げられます。*Young* と *Soft* という 2 つの仮想音声も標準装備されています。DNN ベースではない米国英語の音声でのみ利用できます。詳しくは、[音声変換 SSML](/docs/services/text-to-speech/SSML-transformation.html) を参照してください。
-   **単語のタイミング** - WebSocket インターフェースは、SSML の `<mark>` 要素に対応しています。オプションとして、入力テキストのすべてのストリングについての単語のタイミング情報も取得できます。タイミング情報を使用すれば、入力テキストと合成音声を同期することができます。詳しくは、[単語のタイミングの取得](/docs/services/text-to-speech/word-timing.html)を参照してください。
-   **カスタマイズ** - カスタマイズ・インターフェースを使用して、入力に含まれている一般的でない単語の発音方法を指定できます。International Phonetic Alphabet (IPA) または {{site.data.keyword.IBM_notm}} Symbolic Phonetic Representation (SPR) を使用して、発音を定義できます。 詳しくは、[カスタマイズの理解](/docs/services/text-to-speech/custom-intro.html)を参照してください。

このサービスの価格プランの詳細については、[{{site.data.keyword.cloud_notm}} カタログ ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://{DomainName}/catalog/services/text-to-speech){: new_window} の {{site.data.keyword.texttospeechshort}} サービスを参照してください。

## 言語サポート
{: #languages-index}

このサービスは、ブラジル・ポルトガル語、英語 (英国方言と米国方言)、フランス語、ドイツ語、イタリア語、日本語、スペイン語 (カスティリャ方言、中南米方言、北米方言) の音声に対応しています。どの言語についても、男性または女性の声のどちらか一方、または両方が用意されています。音声ごとに、方言に応じた抑揚とイントネーションが使用されます。各言語で利用できる音声の詳細については、[言語と音声](/docs/services/text-to-speech/voices.html)を参照してください。

## ユース・ケース
{: #usecases}

このサービスは、画面のない音声主体のアプリケーション (優先される出力方式が音声であるアプリケーション) に適しています。

-   障がい者向けのインターフェース (視覚障がい者向けの支援ツールなど)
-   テキストや E メール・メッセージを作業者に対して読み上げるアプリケーション
-   ビデオ・スクリプトのナレーションやビデオのナレーション
-   読むことが主体の教育ツール
-   ホーム・オートメーション・ソリューション

## このサービスをお試しください

このサービスの実際の動作の例については、以下を参照してください。

-   テキストを受け取ってさまざまな種類の音声を生成する {{site.data.keyword.texttospeechshort}} サービスの[クイック・デモ ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://text-to-speech-demo.ng.bluemix.net/){: new_window}。感情表出と変換がサポートされている場合は、その機能も利用できます。
-   {{site.data.keyword.texttospeechshort}} サービスのデモを示す{{site.data.keyword.ibmwatson}} [スターター・キット ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](http://www.ibm.com/watson/developercloud/starter-kits.html){: new_window} のアプリケーション。
