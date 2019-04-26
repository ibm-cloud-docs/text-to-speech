---

copyright:
  years: 2015, 2019
lastupdated: "2019-03-14"

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
{:go: .ph data-hd-programlang='go'}
{:python: .ph data-hd-programlang='python'}
{:swift: .ph data-hd-programlang='swift'}
{:download: .download}
{:apikey: data-credential-placeholder='apikey'}
{:url: data-credential-placeholder='url'}
{:hide-dashboard: .hide-dashboard}

# 入門チュートリアル
{: #gettingStarted}

{{site.data.keyword.texttospeechfull}} サービスは、記述テキストを自然に聞こえる音声に変換して、アプリケーションに音声合成機能を提供します。この curl ベースのチュートリアルを参考にして、このサービスの利用をすぐに開始することができます。サービスの `POST /v1/synthesize` メソッドと `GET /v1/synthesize` メソッドを呼び出して音声ストリームを要求する方法を、例を通して確認できます。
{: shortdesc}

このチュートリアルでは、{{site.data.keyword.cloud}} の IAM (ID およびアクセス管理) の API 鍵を使用して認証を受けます。古いサービス・インスタンスでは、まだ既存の Cloud Foundry サービス資格情報の `{username}` と `{password}` を使用して認証を行っている場合があります。使用するサービス・インスタンスに応じて適切な方式で認証を受けてください。サービスで IAM 認証を使用する方法について詳しくは、リリース・ノートにある [2018 年10 月 30 日のサービスの更新](/docs/services/text-to-speech/release-notes.html#October2018)を参照してください。
{: important}

## 始めに
{: #before-you-begin}

- {: hide-dashboard}  サービスのインスタンスを作成します。
    1.  {: hide-dashboard}{{site.data.keyword.cloud_notm}} カタログの [{{site.data.keyword.texttospeechshort}} ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://{DomainName}/catalog/services/text-to-speech){: new_window} ページに移動します。
    1.  {: hide-dashboard} 無料の {{site.data.keyword.cloud_notm}} アカウントを登録するか、ログインします。
    1.  {: hide-dashboard} **「作成」**をクリックします。
-   サービス・インスタンスに認証されるための資格情報をコピーします。
    1.  {: hide-dashboard}[{{site.data.keyword.cloud_notm}} ダッシュボード ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://{DomainName}/dashboard/apps){: new_window} で対象の {{site.data.keyword.texttospeechshort}} サービス・インスタンスをクリックして、{{site.data.keyword.texttospeechshort}} サービスのダッシュボード・ページに進みます。
    1.  **「管理」**ページで、 **「表示」**をクリックして資格情報を表示します。
    1.  `API 鍵`と `URL` の値をコピーします。
-   `curl` コマンドが存在することを確認します。
    -   例では、`curl` コマンドを使用して HTTP インターフェースのメソッドを呼び出します。 オペレーティング・システムに適したバージョンを [curl.haxx.se ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://curl.haxx.se/){: new_window} からインストールしてください。 Secure Sockets Layer (SSL) プロトコルをサポートするバージョンをインストールします。 必ず、インストールしたバイナリー・ファイルを `PATH` 環境変数に含めてください。

コマンドを入力するときに、`{apikey}` と `{url}` を実際の API 鍵と URL に置き換えてください。中括弧は変数値を示す記号ですので、コマンドでは省略してください。実際の値は以下の例のようになります。
{: hide-dashboard}

```bash
curl -X POST -u "apikey:L_HALhLVIksh1b73l97LSs6R_3gLo4xkujAaxm7i-b9x"
. . .
"https://stream.watsonplatform.net/text-to-speech/api/v1/synthesize"
```
{:pre}
{: hide-dashboard}

このチュートリアルの例で生成される音声ファイルは、ブラウザーや他のツールを使用して再生できます。詳しくは、[音声ファイルの再生](/docs/services/text-to-speech/audio-formats.html#formatsPlay)を参照してください。
{: note}

## ステップ 1: 米国英語のテキストの音声合成
{: #synthesizeEnglish}

以下のコマンドでは、`POST /v1/synthesize` メソッドを使用して、米国英語の入力から 2 種類のフォーマットの音声ファイルを合成します。両方の要求で、デフォルトの米国英語の音声 `en-US_MichaelVoice` を使用します。

1.  以下のコマンドを実行して、「hello world」というストリングから音声を合成して `hello_world.wav` という名前の WAV ファイルを生成します。
    -   {: hide-dashboard}`{apikey}` と `{url}` は、実際の API 鍵と URL に置き換えてください。

    ```bash
    curl -X POST -u "apikey:{apikey}"{: apikey} \
    --header "Content-Type: application/json" \
    --header "Accept: audio/wav" \
    --data "{\"text\":\"hello world\"}" \
    --output hello_world.wav \
    "{url}/v1/synthesize"{: url}
    ```
    {: pre}

1.  以下のコマンドを実行して、同じテキストから音声を合成しますが、`hello_world.ogg` という名前の Ogg ファイル (デフォルト・フォーマット) を生成します。
    -   {: hide-dashboard}`{apikey}` と `{url}` は、実際の API 鍵と URL に置き換えてください。

    ```bash
    curl -X POST -u "apikey:{apikey}"{: apikey} \
    --header "Content-Type: application/json" \
    --data "{\"text\":\"hello world\"}" \
    --output hello_world.ogg \
    "{url}/v1/synthesize"{: url}
    ```
    {: pre}

## ステップ 2: スペイン語のテキストの音声合成
{: #synthesizeSpanish}

以下のコマンドでは、`GET /v1/synthesize` メソッドを使用してスペイン語の入力から音声ファイルを合成します。

1.  以下のコマンドを実行して、「hola mundo」というストリングから音声を合成して `hola_mundo.wav` という名前の WAV ファイルを生成します。入力テキストは URL エンコードします。このメソッドに照会パラメーター `accept` を含めて音声フォーマットを指定し、`voice` を含めてスペイン語の音声 `es-ES_EnriqueVoice` を指定します。
    -   {: hide-dashboard}`{apikey}` と `{url}` は、実際の API 鍵と URL に置き換えてください。

    ```bash
    curl -X GET -u "apikey:{apikey}"{: apikey} \
    --output hola_mundo.wav \
    "{url}/v1/synthesize?accept=audio%2Fwav&text=hola%20mundo&voice=es-ES_EnriqueVoice"{: url}
    ```
    {: pre}

## 次のステップ

-   サービスの HTTP インターフェースの詳細を [HTTP インターフェース](/docs/services/text-to-speech/http.html)で確認します。
-   サービスの WebSocket インターフェースの情報を [WebSocket インターフェース](/docs/services/text-to-speech/websockets.html)で確認します。
-   サービスのインターフェースのメソッドの詳細を [API リファレンス ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://{DomainName}/apidocs/text-to-speech){: new_window} で確認します。
