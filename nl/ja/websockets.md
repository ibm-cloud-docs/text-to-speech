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

# WebSocket インターフェース
{: #usingWebSocket}

{{site.data.keyword.texttospeechfull}} サービスの WebSocket インターフェースを使用してテキストから音声を合成するには、まず、`/v1/synthesize` メソッドを呼び出してサービスとの接続を確立します。次に、その接続経由で合成対象テキストを JSON テキスト・メッセージとしてサービスに送信します。 要求の処理が完了すると、サービスは WebSocket 接続を自動的に閉じます。
{: shortdesc}

合成要求と応答のサイクルには、以下のステップが含まれます。

1.  [接続を開く](#WSopen)。
1.  [入力テキストを送信する](#WSsend)。
1.  [応答を受け取る](#WSreceive)。

WebSocket インターフェースは、HTTP インターフェースの `GET /v1/synthesize` および `POST /v1/synthesize` メソッドと同じ入力を取り、同じ結果を生成します。ただし、WebSocket インターフェースでは、ユーザー指定のマーカーが音声の中で出現する位置を識別するための SSML 要素 `<mark>` がサポートされます。入力テキストのすべてのストリングについてのタイミング情報も戻すことができます。詳しくは、[単語のタイミングの取得](/docs/services/text-to-speech/word-timing.html)を参照してください。

ここで紹介するコード例のスニペットは、HTML5 WebSocket API を使用して JavaScript で作成したものです。WebSocket プロトコルについて詳しくは、Internet Engineering Task Force (IETF) の [Request for Comment (RFC) 6455 ![外部リンクのアイコン](../../icons/launch-glyph.svg "外部リンクのアイコン")](http://tools.ietf.org/html/rfc6455){: new_window} を参照してください。
{: note}

## 接続を開く
{: #WSopen}

WebSocket Secure (WSS) プロトコルで `/v1/synthesize` メソッドを呼び出して、サービスに対する接続を開きます。このメソッドは、以下のエンドポイントで利用できます。

```
wss://{host_name}/text-to-speech/api/v1/synthesize
```
{: codeblock}

`{host_name}` は、アプリケーションがホストされている次のような場所です。

-   `stream.watsonplatform.net` (ダラス)(以下の例ではこのホスト名を使用しています)
-   `stream-fra.watsonplatform.net` (フランクフルト)
-   `gateway-syd.watsonplatform.net` (シドニー)
-   `gateway-wdc.watsonplatform.net` (ワシントン DC)
-   `gateway-tok.watsonplatform.net` (東京)
-   `gateway-lon.watsonplatform.net` (ロンドン)

WebSocket クライアントは、以下の照会パラメーターを指定してこのメソッドを呼び出し、認証を受けたうえでサービスとの接続を確立します。IAM (ID およびアクセス管理) 認証を使用する場合には、`access_token` 照会パラメーターを使用してください。Cloud Foundry サービス資格情報を使用する場合には、`watson-token` 照会パラメーターを使用してください。

<table>
  <caption>表 1. <code>/v1/synthesize</code>
    メソッドのパラメーター</caption>
  <tr>
    <th style="text-align:left; width:23%">パラメーター</th>
    <th style="text-align:center; width:12%">データ型</th>
    <th style="text-align:left">説明</th>
  </tr>
  <tr>
    <td style="text-align:left"><code>access_token</code>
      <br/><em>オプション</em></td>
    <td style="text-align:center">String</td>
    <td style="text-align:left">
      <em>IAM 認証を使用する場合は、</em>サービスの認証を受けるために
      有効な IAM アクセス・トークンを渡します。呼び出しで API 鍵を渡すのではなく、
      IAM アクセス・トークンを渡します。期限が切れていない
      アクセス・トークンを使用する必要があります。アクセス・トークンの
      取得方法については、
      [IAM トークンによる認証](/docs/services/watson/getting-started-iam.html)を参照してください。
    </td>
  </tr>
  <tr>
    <td style="text-align:left"><code>watson-token</code>
      <br/><em>オプション</em></td>
    <td style="text-align:center">String</td>
    <td style="text-align:left">
      <em>Cloud Foundry サービス資格情報を使用する場合は、</em>サービスの認証を受けるために
      有効な {{site.data.keyword.watson}} 認証トークンを渡します。
      呼び出しでサービス資格情報を渡すのではなく、{{site.data.keyword.watson}}
      トークンを渡します。
      {{site.data.keyword.watson}} トークンは Cloud Foundry
      サービス資格情報に基づくものであり、HTTP 基本認証用の `username` と
      `password` を使用します。
      {{site.data.keyword.watson}} トークンの取得方法について詳しくは、
      [{{site.data.keyword.watson}} トークン](/docs/services/watson/getting-started-tokens.html)を参照してください。
    </td>
  </tr>
  <tr>
    <td><code>voice</code><br/><em>オプション</em></td>
    <td style="text-align:center">String</td>
    <td>
      テキストを音声で発話する際の声を指定します。
      デフォルト音声 `en-US_MichaelVoice` を使用する場合は、このパラメーターを省略します。
      詳しくは、[言語と音声](/docs/services/text-to-speech/voices.html)を参照してください。</td>
  </tr>
  <tr>
    <td><code>customization_id</code><br/><em>オプション</em></td>
    <td style="text-align:center">String</td>
    <td>
      合成で使用するカスタム音声モデルの GUID (Globally Unique Identifier) を指定します。 カスタム音声モデルの
      動作が保証されるのは、そのモデルが合成に使用される音声の言語に一致している
      場合のみです。 カスタマイズ ID を含める場合、カスタム・モデルの
      所有者のサービス資格情報を指定してメソッドを呼び出す必要があります。
      カスタマイズなしで指定音声を使用する場合は、このパラメーターを省略します。
      詳しくは、[カスタマイズの理解](/docs/services/text-to-speech/custom-intro.html)を参照してください。
    </td>
  </tr>
  <tr>
    <td><code>x-watson-learning-opt-out</code><br/><em>オプション</em></td>
    <td style="text-align:center">Boolean</td>
    <td>
      この接続を使用して送信される要求および結果をサービスが記録するかどうかを
      指定します。全般的なサービス向上のためにデータにアクセスすることを IBM に
      許可しない場合には、このパラメーターに <code>true</code> を指定してください。詳しくは、[Watson サービスの要求ロギングの制御](/docs/services/watson/getting-started-logging.html)を参照してください。
    </td>
  </tr>
  <tr>
    <td style="text-align:left"><code>x-watson-metadata</code>
      <br/><em>オプション</em></td>
    <td style="text-align:center">String</td>
    <td style="text-align:left">
      接続を介して渡すデータに顧客 ID を関連
      付けます。このパラメーターは、<code>customer_id={id}</code>
      引数を取ります。この <code>id</code> は、
      データに関連付けるランダムなストリングまたは汎用的なストリングです。
      パラメーターの引数は URL エンコードする必要があります (例: `customer_id%3dmy_ID`)。
      デフォルトでは、データに顧客 ID は関連付けられません。
      詳しくは、
      [機密保護](/docs/services/text-to-speech/information-security.html)を参照してください。
    </td>
  </tr>
</table>

以下の JavaScript コード・スニペットでは、サービスとの接続をオープンしています。 `/v1/synthesize` メソッドの呼び出しで `voice` と `access_token` の照会パラメーターを渡しています。前者により、米国英語の Allison の音声を使用するようにサービスに命令しています。接続の確立後に、サービスからのイベントに応答するためにイベント・リスナー (`onOpen`、`onClose` など) を定義しています。

```javascript
var IAM_access_token = '{access_token}';
var wsURI = 'wss://stream.watsonplatform.net/text-to-speech/api/v1/synthesize'
  + '?access_token=' + IAM_access_token
  + '&voice=en-US_AllisonVoice';

var websocket = new WebSocket(wsURI);
websocket.onopen = function(evt) { onOpen(evt) };
websocket.onclose = function(evt) { onClose(evt) };
websocket.onmessage = function(evt) { onMessage(evt) };
websocket.onerror = function(evt) { onError(evt) };
```
{: codeblock}

## 入力テキストを送信する
{: #WSsend}

テキストを合成するために、クライアントは以下のパラメーターを使用して、単純な JSON テキスト・メッセージをサービスに渡します。

<table>
  <caption>表 2. JSON テキスト・メッセージのパラメーター</caption>
  <tr>
    <th style="text-align:left; width:23%">パラメーター</th>
    <th style="text-align:center; width:12%">データ型</th>
    <th style="text-align:left">説明</th>
  </tr>
  <tr>
    <td><code>text</code><br/><em>必須</em></td>
    <td style="text-align:center">String</td>
    <td>
      合成するテキストを指定します。 クライアントは、
      プレーン・テキストまたは SSML (Speech Synthesis
      Markup Language) のアノテーション付きのテキストを渡すことができます。クライアントは、
      要求で最大 5 KB の入力テキストを渡すことができます。この制限には、指定するすべての SSML が
      含まれます。詳しくは、
      [入力テキストの指定](/docs/services/text-to-speech/http.html#input)
      とその後のセクションを参照してください。<br/><br/>
      SSML 入力には、<code>&lt;mark&gt;</code> 要素を含めることもできます。
      詳しくは、
      [SSML マークの指定](/docs/services/text-to-speech/word-timing.html#mark)を参照してください。
    </td>
  </tr>
  <tr>
    <td><code>accept</code><br/><em>必須</em></td>
    <td style="text-align:center">String</td>
    <td>
      要求する音声フォーマット (MIME タイプ) を指定します。デフォルトの
      音声フォーマット <code>audio/ogg;codecs=opus</code> を要求するには、
      `*/*` を使用します。詳しくは、[音声フォーマット](/docs/services/text-to-speech/audio-formats.html)を参照してください。
    </td>
  </tr>
  <tr>
    <td><code>timings</code><br/><em>オプション</em></td>
    <td style="text-align:center">String[ ]</td>
    <td>
      入力テキストのすべてのストリングについての単語の
      タイミング情報をサービスから返すように指定します。サービスは、入力の各トークンの
      開始時間と終了時間を返します。単語のタイミングを要求するには、
      配列の唯一の要素として <code>words</code> を指定してください。空の配列を指定したり、このパラメーターを省略したりすると、
      単語のタイミングは受け取れません。
      詳しくは、
      [単語のタイミングの取得](/docs/services/text-to-speech/word-timing.html#timing)を参照してください。<em>日本語の入力テキストではサポートされません。</em>
    </td>
  </tr>
</table>

以下の JavaScript コード・スニペットでは、入力テキストとして「Hello world」というシンプルなメッセージを渡し、デフォルトの音声フォーマットを要求しています。呼び出しは、クライアントに対して定義された `onOpen` 関数に組み込まれて、接続の確立後のみに送られるようになっています。

```javascript
function onOpen(evt) {
  var message = {
    text: 'Hello world',
    accept: '*/*'
  };
  websocket.send(JSON.stringify(message));
}
```
{: codeblock}

サービスはこのメッセージへの応答として、音声応答のフォーマットを確認するテキスト・メッセージを送信します。以下の応答は、デフォルトの音声フォーマットを確認しています。

```javascript
{
  'binary_streams': [
    {
      content_type: 'audio/ogg;codecs=opus'
    }
  ]
}
```
{: codeblock}

## 応答の受信
{: #WSreceive}

音声フォーマットを確認すると、サービスは、指定されたフォーマットの合成音声をバイナリーのデータ・ストリームとして送信します。以下の場合は、タイミング情報を 1 つ以上のテキスト・メッセージとして送信します。

-   入力テキストに SSML 要素 `<mark>` が 1 つ以上含まれている場合。
-   要求に `timings` パラメーターが指定されている場合。

サービスは、警告またはエラーとともにテキスト・メッセージを送信することもできます。 入力テキストの合成が終了すると、サービスは自動的に WebSocket 接続を閉じます。

クライアントは、接続を介して受け取った音声結果に、サービスからのバイナリー応答を追加する必要があります。クライアントによるテキスト・メッセージの処理は、メッセージへの応答、メッセージの表示、またはアプリケーションでの使用のためのメッセージの取得 (例えば、メッセージにマークの位置が含まれている場合) によって行うことができます。 以下に示す `onMessage` 関数のシンプルな例では、サービスから受け取ったテキスト・メッセージとバイナリー・メッセージを、タイプに応じて適切な変数に追加しています。`onClose()` 関数が実行されると、音声ストリーム全体が受信されます。

```javascript
var messages;
var audioStream;

function onMessage(evt) {
  if (typeof evt.data === string) {
    messages += evt.data;
   } else {
    console.log('Received ' + evt.data.size() + ' binary bytes');
      audioStream += evt.data;
   }
}

function onClose(evt) {
  // 音声ストリームが完了します。
}
```
{: codeblock}

## WebSocket 戻りコード
{: #returnCodes}

サービスは、WebSocket 接続を介して、以下の戻りコードをクライアントに送信できます。

-   `1000`。接続の正常なクローズを示し、接続が確立された目的が満たされたことを意味します。
-   `1002`。プロトコル・エラーのため、サービスが接続をクローズすることを示します。
-   `1006`。接続が異常にクローズされたことを示します。
-   `1009`。フレーム・サイズが 4 MB の制限を超えたことを示します。
-   `1011`。要求を満たすことができなくなる予期しない状態 (無効な引数など) が発生したため、サービスが接続を終了することを示します。 この戻りコードは、入力テキストが大きすぎたことを示している可能性もあります。

ソケットがエラーでクローズされる場合、サービスはクローズされる前に、`{"error":"特定のエラー・メッセージ"}` という形式の情報メッセージをクライアントに送信します。 不明なパラメーターがある場合は、致命的ではない警告メッセージも送信します。

## エラー・メッセージと警告メッセージの例
{: #returnErrors}

以下に、エラー応答の例を示します。JSON テキスト・メッセージと、クライアントの `onClose` コールバック・メソッドからの定様式メッセージが含まれています。定様式メッセージは、接続が閉じているためブール値 `true` で始まります。また、クローズの原因となった WebSocket エラー・コードも含まれています。

-   以下の例は、`accept` パラメーターに無効な引数が指定されていた場合のエラー・メッセージを示しています。

    ```javascript
    {
      "error": "Unsupported mimetype. Supported mimetypes are: ['application/json', 'audio/flac', ...]"
    }
    (True, 1011, u'see the previous message for the error details.')
    ```
    {: codeblock}

-   以下の例は、`text` パラメーターが欠落していた場合のエラー・メッセージを示しています。

    ```javascript
    {
      "error": "Required parameter \"text\" is missing."
    }
    (True, 1011, u'see the previous message for the error details.')
    ```
    {: codeblock}

以下の例は、`invalid-parameter` という不明なパラメーターに対する警告応答を示しています。2 つ目のメッセージが含まれていないのは、この警告では接続がクローズされていないからです。

```javascript
{
  "warnings": "Unknown arguments: invalid-parameter."
}
```
{: codeblock}

WebSocket 戻りコードについて詳しくは、Internet Engineering Task Force (IETF) の [Request for Comments (RFC) 6455 ![外部リンクのアイコン](../../icons/launch-glyph.svg "外部リンクのアイコン")](http://tools.ietf.org/html/rfc6455){: new_window} を参照してください。
