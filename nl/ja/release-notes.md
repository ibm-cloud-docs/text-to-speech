---

copyright:
  years: 2015, 2019
lastupdated: "2019-03-28"

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

# リリース・ノート
{: #release-notes}

以下のセクションでは、{{site.data.keyword.texttospeechfull}} サービスの各リリースと更新で導入された新機能と変更点について説明します。この情報には、既知の制限事項が含まれています。特に記載がない限り、すべての変更点はそれまでのリリースと互換性があり、すべての新規および既存のアプリケーションで自動的かつ透過的に使用可能です。
{: shortdesc}

## 既知の制限事項
{: #limitations}

`V2` のディープ・ニューラル・ネットワーク (DNN) 音声のデプロイメントに問題があるために、合成音声にバックグラウンド・ノイズが含まれます。{{site.data.keyword.IBM_notm}} は、この問題に取り組んでいます。

## 2019 年 3 月 24 日
{: #March2019c}

-   ドイツ語音声のディープ・ニューラル・ネットワーク (DNN) バージョンがサービスで提供されるようになりました。
    -   `de-DE_BirgitV2Voice`
    -   `de-DE_DieterV2Voice`

    DNN ベースの音声について詳しくは、[音声合成テクノロジー](/docs/services/text-to-speech/voices.html#technologiesVoices)を参照してください。
-   このサービスの DNN ベースの音声はすべて、SSML の `<prosody>` 要素の `pitch` 属性と `rate` 属性をサポートするようになりました。`<prosody>` 要素の `volume` 属性は、DNN ベースの音声ではサポートされません。詳しくは、[prosody 要素](/docs/services/text-to-speech/SSML-elements.html#prosody_element)を参照してください。

## 2019 年 3 月 21 日
{: #March2019b}

ユーザーは、自分の {{site.data.keyword.cloud_notm}} アカウントに割り当てられた役割に関連付けられたサービス資格情報のみを表示できるようになりました。例えば、`reader` 役割が割り当てられている場合、`writer` 以上のレベルのサービス資格情報は表示されなくなりました。

この変更は、既存のサービス資格情報を使用しているユーザーやアプリケーションの API アクセスに影響を与えません。この変更で影響を受けるのは、{{site.data.keyword.cloud_notm}} 内の資格情報の表示のみです。

サービス鍵とユーザー役割について詳しくは、[IAM のサービス API 鍵](/docs/services/watson?topic=watson-api-key-bp#api-key-bp)を参照してください。

## 2019 年 3 月 4 日
{: #March2019a}

ディープ・ラーニング合成を使用して音声を生成する以下の 4 つの新しい音声が提供されるようになりました。

-   `it-IT_FrancescaV2Voice`
-   `en-US_AllisonV2Voice`
-   `en-US_LisaV2Voice`
-   `en-US_MichaelV2Voice`

これらの新しい音声では、機械学習と DNN を使用して、テキストから音声が合成されます。ディープ・ラーニング合成、すなわち DNN ベースの合成では、より自然な韻律で全体的に一貫した品質の音声が生成されます。

しかし、これらの新しい音声を使用して生成される音声信号品質は既存の音声とは異なるので、どのアプリケーションにも適しているというわけではありません。また、新しい音声では、SSML 要素 `<prosody>`、`<express-as>`、および `<voice-transformation>` はサポートされません。

これらの DNN ベースの音声、およびそれらの音声と既存の音声の違いについて詳しくは、[音声合成テクノロジー](/docs/services/text-to-speech/voices.html#technologiesVoices)を参照してください。

## さらに前のリリース
{: #older}

-   [2019 年 1 月 28 日](#January2019)
-   [2018 年 12 月 13 日](#December2018)
-   [2018 年 11 月 7 日](#November2018)
-   [2018 年 10 月 30 日](#October2018)
-   [2018 年 6 月 12 日](#June2018)
-   [2018 年 5 月 15 日](#May2018)
-   [2017 年 10 月 2 日](#October2017)
-   [2017 年 7 月 14 日](#July2017)
-   [2017 年 4 月 10 日](#April2017)
-   [2016 年 12 月 1 日](#December2016)
-   [2016 年 9 月 22 日](/docs/services/text-to-speech/release-notes.html#September2016)
-   [2016 年 6 月 23 日](/docs/services/text-to-speech/release-notes.html#June2016)
-   [2016 年 3 月 10 日](/docs/services/text-to-speech/release-notes.html#March2016)
-   [2016 年 2 月 22 日](/docs/services/text-to-speech/release-notes.html#February2016)
-   [2015 年 12 月 17 日](/docs/services/text-to-speech/release-notes.html#December2015)
-   [2015 年 9 月 21 日](/docs/services/text-to-speech/release-notes.html#September2015)
-   [2015 年 7 月 1 日](/docs/services/text-to-speech/release-notes.html#July2015)

### 2019 年 1 月 28 日
{: #January2019}

WebSocket インターフェースで、ブラウザー・ベースの JavaScript コードからトークン・ベースの IAM (ID およびアクセス管理) 認証を行えるようになりました。これに矛盾する制限は削除されました。認証を受けた接続を WebSocket の `/v1/synthesize` メソッドを使用して確立するには、次のようにします。

-   IAM 認証を使用する場合は、`access_token` 照会パラメーターを指定します。
-   Cloud Foundry サービス資格情報を使用する場合は、`watson-token` 照会パラメーターを指定します。

詳しくは、[接続を開く](/docs/services/text-to-speech/websockets.html#WSopen)を参照してください。

### 2018 年 12 月 13 日
{: #December2018}

{{site.data.keyword.texttospeechshort}} サービスが、{{site.data.keyword.cloud}} ロンドン・ロケーション (**eu-gb**) でも提供されるようになりました。他のすべてのロケーションと同様に、ロンドンでもトークン・ベースの IAM (ID およびアクセス管理) 認証が使用されます。このロケーションで作成するすべての新規サービス・インスタンスは、IAM 認証を使用します。

### 2018 年 11 月 7 日
{: #November2018}

{{site.data.keyword.texttospeechshort}} サービスが、{{site.data.keyword.cloud}} 東京ロケーション (**jp-tok**) でも提供されるようになりました。他のすべてのロケーションと同様に、東京でもトークン・ベースの IAM (ID およびアクセス管理) 認証が使用されます。このロケーションで作成するすべての新規サービス・インスタンスは、IAM 認証を使用します。

### 2018 年 10 月 30 日
{: #October2018}

{{site.data.keyword.texttospeechshort}} サービスは、すべてのロケーションでトークン・ベースの IAM (ID およびアクセス管理) 認証を行うように移行しました。すべての {{site.data.keyword.cloud_notm}} サービスが IAM 認証を使用するようになります。{{site.data.keyword.texttospeechshort}} サービスでは、以下の日付で各ロケーションで移行が行なわれました。

-   ダラス (**us-south**): 2018 年 10 月 30 日
-   フランクフルト (**eu-de**): 2018 年 10 月 30 日
-   ワシントン DC (**us-east**): 2018 年 6 月 12 日
-   シドニー (**au-syd**): 2018 年 5 月 15 日

IAM 認証への移行による影響は、新規のサービス・インスタンスと既存のサービス・インスタンスとで異なります。

-   *ロケーションにかかわらず、ユーザーが作成するすべての新規サービス・インスタンス* は、サービスへのアクセスに IAM 認証を使用するようになりました。ベアラー・トークンまたは API 鍵のいずれかを渡すことができます。トークンを使用すれば、呼び出すたびにサービス資格情報を組み込むことなく、要求の認証を受けることができます。API 鍵では HTTP 基本認証が使用されます。{{site.data.keyword.ibmwatson}} SDK を使用する場合は、API 鍵を渡して SDK にトークンのライフサイクルを管理させることができます。
-   *上記の移行日より前にロケーションに作成されていた既存のサービス・インスタンス* は、お客様が IAM 認証を使用するように移行するまで、以前の Cloud Foundry サービスの資格情報の `{username}` と `{password}` を認証に使用し続けます。IAM 認証に移行する方法について詳しくは、[リソース・グループへの Cloud Foundry サービス・インスタンスのマイグレーション](https://{DomainName}/docs/resources/instance_migration.html)を参照してください。

詳しくは、以下の資料を参照してください。

-   サービス・インスタンスで使用されている認証メカニズムを確認するには、[{{site.data.keyword.cloud_notm}} ダッシュボード ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://{DomainName}/dashboard/apps){: new_window} で対象のインスタンスをクリックして、サービス資格情報を表示します。
-   {{site.data.keyword.watson}} サービスで IAM トークンを使用する方法について詳しくは、[IAM トークンによる認証](/docs/services/watson/getting-started-iam.html)を参照してください。
-   {{site.data.keyword.watson}} サービスで IAM の API 鍵を使用する方法について詳しくは、[IAM のサービス API 鍵](/docs/services/watson/apikey-bp.html)を参照してください。
-   IAM 認証の使用例については、[API リファレンス ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://{DomainName}/apidocs/text-to-speech){: new_window} を参照してください。

### 2018 年 6 月 12 日
{: #June2018}

ワシントン DC (**us-east**) でホストされるアプリケーションで、以下の機能を使用できるようになりました。

-   サービスで、新しい API 認証プロセスがサポートされるようになりました。詳しくは、[2018 年 10 月 30 日のサービスの更新](#October2018)を参照してください。
-   サービスで、`X-Watson-Metadata` ヘッダーと `DELETE /v1/user_data` メソッドがサポートされるようになりました。詳しくは、[機密保護](/docs/services/text-to-speech/information-security.html)を参照してください。

### 2018 年 5 月 15 日
{: #May2018}

シドニー (**au-syd**) でホストされるアプリケーションで、以下の機能を使用できるようになりました。

-   サービスで、新しい API 認証プロセスがサポートされるようになりました。詳しくは、[2018 年 10 月 30 日のサービスの更新](#October2018)を参照してください。
-   サービスで、`X-Watson-Metadata` ヘッダーと `DELETE /v1/user_data` メソッドがサポートされるようになりました。詳しくは、[機密保護](/docs/services/text-to-speech/information-security.html)を参照してください。

### 2017 年 10 月 2 日
{: #October2017}

`audio/l16` フォーマットを使用する場合に、返される音声のエンディアンネスをオプションで指定できるようになりました (サンプリング・レートを指定しておく必要があります)。例えば、`audio/l16;rate=22050;endianness=big-endian` や `audio/l16;rate=22050;endianness=little-endian` と指定できます。デフォルトはビッグ・エンディアンです。詳しくは、[音声フォーマット](/docs/services/text-to-speech/audio-formats.html)を参照してください。

### 2017 年 7 月 14 日
{: #July2017}

サービスで、MP3 つまり Motion Picture Experts Group (MPEG) 音声フォーマットがサポートされるようになりました。サポートされる音声フォーマットについて詳しくは、[音声フォーマット](/docs/services/text-to-speech/audio-formats.html)を参照してください。

### 2017 年 4 月 10 日
{: #April2017}

-   サービスで、Opus または Vorbis コーデックを使用した Web メディア (WebM) 音声フォーマットがサポートされるようになりました。サービスで、Opus コーデックのほかに Vorbis コーデックを使用した Ogg 音声フォーマットもサポートされるようになりました。サポートされる音声フォーマットについて詳しくは、[音声フォーマット](/docs/services/text-to-speech/audio-formats.html)を参照してください。
-   サービスは、Cross-Origin Resource Sharing (CORS) をサポートして、ブラウザー・ベースのクライアントが直接サービスを呼び出すことを許可するようになりました。 詳しくは、『[CORS サポート](/docs/services/text-to-speech/developer-overview.html#cors)』を参照してください。
-   カスタマイズ・インターフェースの一部のメソッドについて、正常実行を示す HTTP 応答コードが以下のように変更されました。
    -   `POST /v1/customizations` メソッドが、(200 ではなく) 201 を返すようになりました。
    -   `POST /v1/customizations/{customization_id}` メソッドが、(201 ではなく) 200 を返すようになりました。
    -   `POST /v1/customizations/{customization_id}/words` メソッドが、(201 ではなく) 200 を返すようになりました。
    -   `PUT /v1/customizations/{customization_id}/words/{word}` メソッドが、(201 ではなく) 200 を返すようになりました。
-   `POST /v1/customizations/{custom_id}/words` メソッドおよび `PUT /v1/customizations/{customization_id}/words/{word}` メソッドが、日本語以外の言語に `part_of_speech` を指定しようとした場合に、`Part of speech is supported for ja-JP language only` というエラー・メッセージと HTTP 応答コード 400 を返すようになりました。
-   `POST /v1/customizations/{custom_id}/words` メソッドが、空の応答本体 (`{}`) を返すようになりました。

### 2016 年 12 月 1 日
{: #December2016}

-   `es-US_SofiaVoice` 音声の中南米バージョンである新しい音声 `es-LA_SofiaVoice` がサービスに追加されました。この 2 つの音声の重要な違いは、`$` (ドル記号) の訳です。中南米バージョンでは *ペソ* という用語が使用されますが、北米バージョンでは *ドル* という用語が使用されます。他にもこの 2 つの音声には小さな違いが存在します。

-   `en-US_AllisonVoice` に加えて、`en-US_LisaVoice` と `en-US_MichaelVoice` という 2 つの音声が SSML 音声変換で変換可能になりました。音声変換について詳しくは、[音声変換 SSML](/docs/services/text-to-speech/SSML-transformation.html) を参照してください。
-   日本語でカスタマイズ・インターフェースを使用する場合に、カスタム音声モデルに定義されている単語/トランスレーションのペアのうち、最も長い一致単語が適用されるようになりました。例えば、カスタム音声モデルに次の 2 つの項目が登録されているとします。

    <pre><code data-copy="false" class="language-javascript">  {
      "words": [
        {"word":"&#65326;&#65337;", "translation":"&#12491;&#12517;&#12540;&#12520;&#12540;&#12463;", "part_of_speech":"Mesi"},
        {"word":"&#65326;&#65337;&#65315;", "translation":"&#12491;&#12517;&#12540;&#12520;&#12540;&#12463;&#12471;&#12486;&#12451;", "part_of_speech":"Mesi"}
      ]
    }</code></pre>

    入力テキスト内にストリング <code>&#65326;&#65337;&#65315;</code> が見つかると、サービスはその単語を適用します。<code>&#65326;&#65337;</code> より長い一致単語であるからです。これまでは、ストリング <code>&#65326;&#65337;</code> が適用されていました。カスタム音声モデルの日本語の項目の使用方法について詳しくは、[日本語の項目の処理](/docs/services/text-to-speech/custom-rules.html#jaNotes)を参照してください。

### 2016 年 9 月 22 日
{: #September2016}

-   customization メソッドおよび `GET /v1/pronunciation` メソッドを含むカスタマイズ・インターフェースが、サービスでサポートされるすべての言語で使用できるようになりました。 このインターフェースは、ベータ版のままです。詳しくは、[カスタマイズの理解](/docs/services/text-to-speech/custom-intro.html)を参照してください。
-   サービスでは、日本語で SSML (Speech Synthesis Markup Language) がサポートされるようになりました。 SSML サポートに関する一般情報については、[SSML の使用](/docs/services/text-to-speech/SSML.html)を参照してください。日本語の SPR 記号および IPA 記号については、[日本語の記号](/docs/services/text-to-speech/ja-JP-SPRs.html)を参照してください。日本語のカスタム音声モデルに単語の項目を作成する場合は、追加の考慮事項および `part_of_speech` フィールドが適用されます。詳しくは、[日本語の項目の処理](/docs/services/text-to-speech/custom-rules.html#jaNotes)を参照してください。
-   サービスでは、新しい `<voice-transformation>` 要素を使用した SSML 音声変換が提供されるようになりました。 音声のピッチ、ピッチ範囲、声門閉鎖音強度、気息音、速度、および音色を変更するカスタム音声変換を作成することにより、使用可能な音声の選択の幅を広げることができます。 サービスには、組み込まれた 2 つの仮想音声 *Young* および *Soft* もあります。 現在、サービスで音声変換がサポートされるのは、米国英語 Allison 音声のみです。 詳しくは、[音声変換 SSML](/docs/services/text-to-speech/SSML-transformation.html) を参照してください。
-   WebSocket インターフェースで渡した入力テキストのすべてのストリングについての単語のタイミング情報を取得できるようになりました。入力内のすべてのストリングの開始時間と終了時間を受け取るには、サービスに渡す JSON オブジェクトのオプション・パラメーター `timings` にストリング `words` が含まれている配列を指定します。この機能は、現在、日本語の入力テキストでは使用できません。 詳しくは、[単語のタイミングの取得](/docs/services/text-to-speech/word-timing.html)を参照してください。
-   サービスでは、あらゆるコンテキストで送信するすべての SSML 要素が検証されるようになりました。 無効なタグが検出されると、サービスは説明のメッセージとともに HTTP 400 応答コードを報告し、メソッドが失敗します。 以前のリリースでは、サービスによるエラーの処理に整合性がありませんでした。例えば、無効な単語の発音を指定すると、予測不能または整合性のない動作が発生することがありました。 詳しくは、[SSML 検証](/docs/services/text-to-speech/SSML.html#errors)を参照してください。
-   `spr` を `GET /v1/pronunciation` メソッドの `format` オプションの引数として使用したり、SSML の `<phoneme>` 要素の `alphabet` 属性として使用したりすることが非推奨になりました。{{site.data.keyword.IBM_notm}} Symbolic Phonetic Representation (SPR) 表記を使用するには、すべてのケースで `spr` の代わりに `ibm` 引数を使用します。
-   サポートされている音声フォーマットのリストに、`audio/mulaw;rate=8000` が含まれるようになりました。 `audio/basic` と同様に、このフォーマットは、サンプリング・レート 8 KHz で 8 ビットの u-law (または mu-law) データを使用してエンコードされた単一チャネル音声を生成します。詳しくは、[音声フォーマット](/docs/services/text-to-speech/audio-formats.html)を参照してください。
-   `GET /v1/voices` メソッドおよび `GET /v1/voices/{voice}` メソッドが、各音声の出力の一部として、`supported_features` オブジェクトを返すようになりました。このオブジェクトは、その音声がカスタマイズおよび SSML の `<voice_transformation>` 要素をサポートするかどうかを表すものです。詳しくは、[言語と音声](/docs/services/text-to-speech/voices.html)を参照してください。

### 2016 年 6 月 23 日
{: #June2016}

-   サービスでは、テキストから音声を合成するための WebSocket インターフェースが提供されるようになりました。 このインターフェースには、HTTP インターフェースの `/v1/synthesize` メソッドと同じ機能が用意されています。 プレーン・テキスト、または SSML でマークアップされたテキストが受け入れられます。 また、SSML の `<mark>` 要素もサポートされており、音声内でマークの前にあるすべてのテキストの合成が終了する時間を指定することができます。 詳しくは、[WebSocket インターフェース](/docs/services/text-to-speech/websockets.html)を参照してください。
-   サービスでは、SSML でアノテーションが付けられたテキストが、カスティリャ・スペイン語、北米スペイン語、イタリア語、ブラジル・ポルトガル語でサポートされるようになりました。 SSML の使用は、米国英語、英国英語、フランス語、およびドイツ語では、既にサポートされています。 この更新時点で、サービスでは日本語以外のすべての言語で SSML がサポートされています。 さらに、SSML の `<phoneme>` 要素では、{{site.data.keyword.IBM_notm}} SPR 表記と IPA 表記の両方を使用して単語の発音を定義できます。詳しくは、[SSML の使用](/docs/services/text-to-speech/SSML.html)および [IBM SPR の使用](/docs/services/text-to-speech/SPRs.html)を参照してください。

    米国英語では、SSML の `<phoneme>` 要素を使用して、カスタム音声モデルの単語項目を作成することもできます。カスタマイズがサポートされるのは米国英語のみです。詳しくは、[カスタマイズの理解](/docs/services/text-to-speech/custom-intro.html)を参照してください。
-   サービスでは、最もよく使用される音声について、感情表出および自然らしさが改善されています。 この改善は、入力テキストからの RNN (Recursive Neural Network) ベースの韻律予測に基づいています。 これらは以下の言語について、新しいサービス・エンジンおよび音声モデルの更新として使用できます。

    -   `en-US_AllisonVoice`
    -   `en-US_LisaVoice`
    -   `en-US_MichaelVoice`
    -   `es-ES_EnriqueVoice`
    -   `fr-FR_ReneeVoice`
-   `GET /v1/pronunciation` メソッドでは、オプションの `customization_id` クエリー・パラメーターが受け入れられるようになりました。 このパラメーターを使用すると、指定したカスタム音声モデルに含まれている単語トランスレーションを取得できます。音声モデルに単語が含まれていない場合、メソッドからは単語のデフォルトの発音が返されます。 詳しくは、[API リファレンス ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://{DomainName}/apidocs/text-to-speech){: new_window} を参照してください。

    米国英語以外の言語で、カスタマイズ ID を指定せずに `GET /v1/pronunciation` メソッドを使用する場合、{{site.data.keyword.IBM_notm}} SPR 表記のみで単語の発音を要求できます。 米国英語以外の言語では、このメソッドの `format` オプションとともに `spr` を指定する必要があります。
    {: note}
-   サポートされる音声フォーマットのリストに、`audio/basic` が追加されました。このフォーマットは、サンプリング・レート 8 KHz で 8 ビットの u-law (mu-law) データを使用してエンコードされた単一チャネル音声を生成します。詳しくは、[音声フォーマット](/docs/services/text-to-speech/audio-formats.html)を参照してください。
-   HTTP および WebSocket の `/v1/synthesize` メソッドは、要求に含まれていた無効な照会パラメーターまたは JSON フィールドに関するメッセージが入った `warnings` 応答を返すことがあります。この警告のフォーマットが変更されました。以前のフォーマットの例を以下に示します。

    `"warnings": "Unknown arguments: [u'{invalid_arg_1}', u'{invalid_arg_2}']."`

    同じ警告が以下のフォーマットに変更されました。

    `"warnings": "Unknown arguments: {invalid_arg_1}, {invalid_arg_2}."`

### 2016 年 3 月 10 日
{: #March2016}

-   `GET` メソッドおよび `POST /v1/synthesize` メソッドが、要求に含まれていた無効な照会パラメーターまたは JSON フィールドに関する警告メッセージのリストが入った `Warnings` 応答ヘッダーを返すようになりました。リストの各要素には、警告の性質を表すストリングと、それに続いて無効な引数ストリングの配列が含まれます。例えば、`Unknown arguments: [u'{invalid_arg_1}', u'{invalid_arg_2}']` です。詳しくは、[API リファレンス ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://{DomainName}/apidocs/text-to-speech){: new_window} を参照してください。
-   *Apple&reg; iOS オペレーティング・システム用の {{site.data.keyword.watson}} Speech Software Development Kit (SDK)* (ベータ) は非推奨となり、*{{site.data.keyword.watson}} Swift SDK* に置き換えられました。新しい SDK は、GitHub 上の `watson-developer-cloud` 名前空間の [swift-sdk リポジトリー ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://github.com/watson-developer-cloud/swift-sdk){: new_window} から入手できます。

### 2016 年 2 月 22 日
{: #February2016}

感情表出のための SSML の新機能の導入によって、サービスが更新されました。感情を表出できる `<express-as>` 要素を追加することで、サービスは Speech Synthesis Markup Language (SSML) を拡張しました。この要素は、`GoodNews` (朗報)、`Apology` (謝罪)、 `Uncertainty` (不安) という 3 つの発話スタイルで感情を表出できます。この要素は、テキストの本文全体、文、句、または単語に適用できます。 現在、サービスで感情表出がサポートされるのは、米国英語 Allison 音声 (`en-US_AllisonVoice`) のみです。 詳しくは、[感情表出 SSML](/docs/services/text-to-speech/SSML-expressive.html) を参照してください。

### 2015 年 12 月 17 日
{: #December2015}

-   サービスに、入力に含まれている一般的ではない単語の発音方法を指定するために使用できる新規カスタマイズ・インターフェースが追加されました。 このインターフェースは、カスタム音声モデル、およびモデルに含まれている単語/トランスレーションのペアの作成および管理に使用できるいくつかの新規メソッドを備えています。テキストを音声に合成する際に、作成したカスタム・モデルを使用できます。

    サービスで同音異字トランスレーションと表音トランスレーションがサポートされるようになりました。表音トランスレーションでは、標準の International Phonetic Alphabet (IPA) 表記または {{site.data.keyword.IBM_notm}} 専有の Symbolic Phonetic Representation (SPR) のいずれかを使用できます。表音トランスレーションを指定するには、Speech Synthesis Markup Language (SSML) を使用します。

    カスタマイズ・インターフェースは、`POST /v1/customizations`、`POST /v1/customizations/{customization_id}`、`POST /v1/customizations/{customization_id}/words`、および `PUT /v1/customizations/{customization_id}/words/{word}` という一連の新規 HTTP メソッドを備えています。また、任意の単語の発音を返す新しい `GET /v1/pronunciation` メソッドと、特定の音声に関する詳細情報を返す新しい `GET /v1/voices/{voice}` メソッドも導入されました。さらに、サービスのインターフェースの既存メソッドが、必要に応じてカスタム音声モデルのパラメーターを受け取るようになりました。

    カスタマイズおよびそのインターフェースについて詳しくは、[カスタマイズの理解](/docs/services/text-to-speech/custom-intro.html)および [API リファレンス ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://{DomainName}/apidocs/text-to-speech){: new_window} を参照してください。

    カスタマイズ・インターフェースは、米国英語でのみ現在サポートされるベータ・リリースです。 現在、すべての customization メソッドおよび `GET /v1/pronunciation` メソッドは、米国英語でのみ、カスタム音声モデルおよび単語トランスレーションを作成および操作するために使用できます。
    {: note}
-   女性の声でブラジル・ポルトガル語の音声を合成できる新しい音声 `pt-BR_IsabelaVoice` がサポートされるようになりました。詳しくは、[言語と音声](/docs/services/text-to-speech/voices.html)を参照してください。

### 2015 年 9 月 21 日
{: #September2015}

-   2 つの新しいベータ・モバイル Software Development Kit (SDK) が音声サービスで使用可能になりました。 これらの SDK を使用すると、モバイル・アプリケーションで {{site.data.keyword.texttospeechshort}} サービスと {{site.data.keyword.speechtotextshort}} サービスの両方と対話できるようになります。SDK を使用して、{{site.data.keyword.texttospeechshort}} サービスにテキストを送信したり、音声応答を受け取ったりできます。
    -   *{{site.data.keyword.watson}} Swift SDK* は、GitHub 上の `watson-developer-cloud` 名前空間の [swift-sdk リポジトリー ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://github.com/watson-developer-cloud/swift-sdk){: new_window} から入手できます。
    -   *{{site.data.keyword.watson}} Speech Android SDK* は、GitHub 上の `watson-developer-cloud` 名前空間の [speech-android-sdk リポジトリー ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://github.com/watson-developer-cloud/speech-android-sdk){: new_window} から入手できます。

    いずれの SDK も、{{site.data.keyword.cloud_notm}} サービス資格情報と認証トークンの両方による音声サービスの認証に対応しています。

    SDK の機能はベータ版であるため、今後変更されることがあります。
    {: note}
-   サービスでは、新規言語の日本語がサポートされるようになりました。 音声 `ja-JP_EmiVoice` は日本語の女性の声です。

### 2015 年 7 月 1 日
{: #July2015}

サービスは、2015 年 7 月 1 日に、ベータから一般出荷版 (GA) に移行しました。 {{site.data.keyword.texttospeechshort}} API のベータ版と GA 版では、以下の違いが存在します。 GA リリースにより、ユーザーはサービスの新しいバージョンにアップグレードする必要があります。

-   新規プログラミング・モデルにより、クライアントとサービス間の直接対話がサポートされるようになりました。 このモデルを使用すると、クライアントは、サービスと直接通信するための認証トークンを取得できます。トークンを使用すれば、{{site.data.keyword.cloud_notm}} のサーバー・サイドのプロキシー・アプリケーションがクライアントの代わりにサービスを呼び出す必要はなくなります。トークンは、クライアントとサービスが対話する手段として望ましい手段です。

    サービスでは引き続き、クライアントとサービス間での通信およびデータの中継についてサーバー・サイドのプロキシーに依拠していた古いプログラミング・モデルがサポートされます。 ただし、新しいモデルの方が効率的であり、スループットも高くなります。 新しいプログラミング・モデルについて詳しくは、[{{site.data.keyword.watson}} サービスのプログラミング・モデル](/docs/services/watson/getting-started-develop.html)を参照してください。
-   SSML (Speech Synthesis Markup Language) を HTTP `GET` および `POST` バージョンの `/v1/synthesize` メソッドに渡すことができるようになりました。 SSML は、{{site.data.keyword.texttospeechshort}} サービスなどの音声合成アプリケーションにテキストのアノテーションを提供するために設計された XML ベースのマークアップ言語です。 SSML 入力をサービスに渡す方法について詳しくは、[入力テキストの指定](/docs/services/text-to-speech/http.html#input)を参照してください。

    サービスによる SSML の使用の初期サポートは、英国英語、米国英語、フランス語、およびドイツ語の各言語に対してのみ提供されます。 サービスでは、SSML のイタリア語およびスペイン語での使用はサポートされません。 SSML を使用する際には、サポートされない言語の音声を選択していないことを確認してください。選択した場合は、意味のない結果になります。
-   合成音声でサポートされる音声が変更され、拡張されました。サービスでは、`/v1/synthesize` メソッドで多くの追加の音声、言語、および方言がサポートされるようになりました。 サポートされる音声について詳しくは、[言語と音声](/docs/services/text-to-speech/voices.html)を参照してください。

    ベータで提供されていた以下の 3 つの音声の名前が、GA 向けに変更されました。
    -   `VoiceEnUsMichael` は、`en-US_MichaelVoice` になりました。
    -   `VoiceEnUsLisa` は、`en-US_LisaVoice` になりました。
    -   `VoiceEsEsEnrique` は、`es-ES_EnriqueVoice` になりました。

    ベータ版のサービスでは、そのベータ版が提供されている限りは、以前の音声の名前を (`-beta` API エンドポイントを介して) 使用できます。ただし、サービスの GA 版では、新規名を使用する必要があります。
-   Free Lossless Audio Codec (FLAC) フォーマットの音声を返すようにサービスに要求できるようになりました。引き続き Opus コーデックを使用した Ogg フォーマット (デフォルト) および Waveform Audio ファイル・フォーマット (WAV) の音声を返すこともできます。`/v1/synthesize` メソッドで音声フォーマットを使用する方法について詳しくは、[音声フォーマット](/docs/services/text-to-speech/audio-formats.html)を参照してください。
-   HTTP `GET` 要求の URL および HTTP `POST` 要求の本体に指定して `/v1/synthesize` メソッドに送信するテキストのサイズの制限が、最大 5 KB になりました。ベータ版では、テキストの最大サイズは 4 MB でした。
-   `/v1/synthesize` メソッドに、ヘッダー `X-WDC-PL-OPT-OUT` が含まれるようになりました。このヘッダーは、サービスで操作のテキストおよび音声の結果を使用して将来の結果を改善するかどうかを制御します。 サービスがテキストおよび音声の結果を使用しないようにするには、このヘッダーに値 `1` を指定します。 このパラメーターは、現在の要求にのみ適用されます。 ベータ版のメソッドの `X-logging` ヘッダーは新しいヘッダーによって置き換えられています。 詳しくは、[{{site.data.keyword.watson}} サービスの要求ロギングの制御](/docs/services/watson/getting-started-logging.html)を参照してください。
-   `/v1/synthesize` メソッドの以下のエラー・コードが変更されました。
    -   エラー・コード 406 (「許可されていません。サポートされない MIME タイプです。」) が削除されました。
    -   エラー・コード 415 (「サポートされないメディア・タイプ」) が追加されました。
    -   エラー・コード 503 (「サービスを利用できません」) が追加されました。
-   `GET /v1/voices` メソッドの以下のエラー・コードが変更されました。
    -   エラー・コード 406 (「許可されていません。サポートされない MIME タイプです。」) が削除されました。
    -   エラー・コード 415 (「サポートされないメディア・タイプ」) が追加されました。
