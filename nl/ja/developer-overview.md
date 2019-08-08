---

copyright:
  years: 2015, 2019
lastupdated: "2019-07-06"

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

# 開発者向けの概要
{: #overview}

{{site.data.keyword.texttospeechfull}} サービスの音声合成機能は、HTTP Representational State Transfer (REST) API または WebSocket インターフェースを介して利用できます。 多様なプログラミング言語でアプリケーション開発を簡単に行えるように、複数の Software Development Kit (SDK) も用意されています。 以下のセクションでは、このサービスを使用するアプリケーションの開発の概要を説明します。
{: shortdesc}

## HTTP インターフェース
{: #overview-http}

HTTP API を使用してテキストの音声合成を行うには、サービスの `GET` または `POST` バージョンの `/v1/synthesize` メソッドを呼び出します。 メソッドの 2 つのバージョンは、概して、同等の機能を備えています。

-   *入力テキスト:* 合成する入力テキストは、以下の 2 とおりの方法で渡します。
    -   `GET /v1/synthesize` メソッドは、入力テキストを照会パラメーターで受け取ります。 要求の最大サイズは 8 KB です。これには、入力テキスト、URL、ヘッダーが含まれます。
    -   `POST /v1/synthesize` メソッドは、入力テキストを要求本体の中で受け取ります。 要求の最大サイズは、URL とヘッダーが 8 KB、要求本体で送信する入力テキストが 5 KB です。

    サービスには、プレーン・テキストまたは SSML (Speech Synthesis Markup Language) でアノテーションが付けられたテキストを渡すことができます。 SSML は、{{site.data.keyword.texttospeechshort}} サービスなどの音声合成アプリケーション用のテキストのアノテーションが用意された XML ベースのマークアップ言語です。 このサービスでは、いくつかの標準米国英語の音声で使用可能な独自の感情表出要素と音声変換要素を追加して SSML を拡張しています。

    詳しくは、[入力テキストの指定](/docs/services/text-to-speech?topic=text-to-speech-usingHTTP#input)を参照してください。
-   *音声:* サービスはテキストを受け取り、さまざまな言語、音声、方言で出力を生成します。 このサービスでは、各言語について少なくとも 1 つの女性音声が用意されています。一部の言語の場合、サービスでは複数の音声が用意されていて、それには男性音声と女性音声の両方が含まれることがあります。このサービスでは、米国英語と英国英語など、さまざまな地方語も用意されています。ほとんどの音声では、標準 (連結的) と拡張ニューラルの両方のバージョンが用意されています。

    サービスの `GET /v1/voices` メソッドまたは `GET /v1/voices/{voice}` メソッドを使用して、サポートされる音声に関する詳細を取得できます。 サービスは、テキストから、指定された音声の言語を合成できます。 必ず、音声と入力テキストを一致させてください。

    詳しくは、[言語と音声](/docs/services/text-to-speech?topic=text-to-speech-voices)を参照してください。
-   *音声フォーマット:* サービスが生成できる音声のフォーマットは次のとおりです。Opus (デフォルト) または Vorbis コーデックを使用したOgg または Web メディア (WebM) フォーマット、MP3 (Motion Picture Experts Group、つまり MPEG) フォーマット、Waveform Audio ファイル・フォーマット (WAV)、Free Lossless Audio Codec (FLAC)、16 ビットのリニア Pulse-Code Modulation (PCM)、8 ビットの mu-law (u-law)、または基本音声。

    詳しくは、[音声フォーマット](/docs/services/text-to-speech?topic=text-to-speech-audioFormats)を参照してください。

## WebSocket インターフェース
{: #overview-websocket}

サービスには、テキストからの音声合成に使用できる WebSocket インターフェースが用意されています。 このインターフェースは、最大 5 KB の入力テキストを受け取る単一バージョンの `/v1/synthesize` メソッドを備えています。 合成するテキスト、使用する音声、および音声のフォーマットを指定します。 プレーン・テキスト、または SSML でアノテーションが付けられたテキストを指定できます。 詳しくは、[WebSocket インターフェース](/docs/services/text-to-speech?topic=text-to-speech-usingWebSocket)を参照してください。

WebSocket インターフェースは、音声の中の特定の位置を識別する SSML 要素 `<mark>` の使用をサポートしています。 また、入力テキストのすべての単語のタイミング情報を要求することもできます。 詳しくは、[単語のタイミングの取得](/docs/services/text-to-speech?topic=text-to-speech-timing)を参照してください。

## カスタマイズ・インターフェース
{: #overview-customization}

サービスは、音声合成時に使用するカスタム音声モデルを作成するために使用できるカスタマイズ・インターフェースを備えています。 カスタム音声モデルは、特定の言語の単語とそのトランスレーションから成る辞書です。 モデル内の各単語とトランスレーションのペアは、その単語が入力テキストに含まれていた場合の発音方法をサービスに指示します。

カスタム音声モデルを使用すると、サービスの標準の発音ルールでは適切な発音が生成されない非一般的な単語に対して、アプリケーション固有のトランスレーションを作成できます。 単語/トランスレーションのペアを表すカスタム項目を定義するときには、標準的な International Phonetic Alphabet (IPA) 表記または {{site.data.keyword.IBM_notm}} 専有の Symbolic Phonetic Representation (SPR) を使用できます。

例えば、ご使用のアプリケーションで、特殊な外来語、人名や地名、略語、頭字語が日常的に出現する場合があります。 カスタマイズを使用すれば、そのような用語をどのように発音すればよいのかをサービスに指示するトランスレーションを定義できます。 詳しくは、[カスタマイズの理解](/docs/services/text-to-speech?topic=text-to-speech-customIntro)を参照してください。

カスタマイズ・インターフェースはベータ・リリースです。また、音声モデルのカスタマイズを使用するには、標準価格プランが必要です。ライト・プランのユーザーは、カスタマイズ・インターフェースを使用できません。詳しくは、{{site.data.keyword.texttospeechshort}} サービスの[価格設定ページ](https://www.ibm.com/cloud/watson-text-to-speech/pricing){: external}を参照してください。
{: note}

## CORS サポート
{: #cors}

サービスは、Cross-Origin Resource Sharing (CORS) をサポートしています。 CORS を使用すると、Web ページから外部ドメインにあるリソースを直接要求できるようになります。 CORS は、そうした要求を禁止する同一生成元セキュリティー・ポリシーを回避できます。 サービスが CORS をサポートしているため、Web ページは、そのページをホストする Web サーバーを介して要求を渡さずに、サービスと直接通信できます。

例えば、{{site.data.keyword.cloud}} 内のサーバーからロードされた Web ページで、{{site.data.keyword.cloud_notm}} サーバーをバイパスして、カスタマイズ API を直接呼び出すことができます。 詳しくは、[enable-cors.org](https://enable-cors.org/){: external} を参照してください。

## Software Development Kit の使用
{: #sdks}

SDK を使用すれば、{{site.data.keyword.texttospeechshort}} サービスで音声アプリケーションを簡単に開発できます。 一般的なプログラミング言語やプラットフォーム用の {{site.data.keyword.ibmwatson}} SDK がいくつも用意されています。

-   SDK の一覧および GitHub 上の各 SDK へのリンクについては、[SDK の使用](/docs/services/watson?topic=watson-using-sdks)を参照してください。
-   {{site.data.keyword.texttospeechshort}} サービスの Node、Java&trade;、Python、Ruby、Swift、および Go SDK のすべてのメソッドについて詳しくは、[API リファレンス](https://{DomainName}/apidocs/text-to-speech){: external}を参照してください。

## アプリケーション開発に関する詳細
{: #learn}

{{site.data.keyword.watson}} サービスおよび {{site.data.keyword.cloud_notm}} の使用方法について詳しくは、以下を参照してください。

-   {{site.data.keyword.watson}} サービスおよび {{site.data.keyword.cloud_notm}} の使用方法の概要については、[{{site.data.keyword.watson}} と {{site.data.keyword.cloud_notm}} の概要](/docs/services/watson?topic=watson-about)を参照してください。
-   すべての新規サービス・インスタンスは、{{site.data.keyword.cloud_notm}} の IAM (ID およびアクセス管理) を使用して認証を行います。 古いサービス・インスタンスでは、まだ既存の Cloud Foundry サービス資格情報の `{username}` と `{password}` を使用して認証を行っている場合があります。 サービスの認証方法について詳しくは、リリース・ノートの [2018 年 19 月 30 日のサービスの更新](/docs/services/text-to-speech?topic=text-to-speech-release-notes#October2018)を参照してください。
-   すべての {{site.data.keyword.watson}} サービスについて実行されるデフォルトの要求ロギングの制御については、[{{site.data.keyword.watson}} サービスの要求ロギングの制御](/docs/services/watson?topic=watson-gs-logging-overview)を参照してください。
