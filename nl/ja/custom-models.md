---

copyright:
  years: 2015, 2019
lastupdated: "2019-03-07"

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

# カスタム音声モデルの作成と管理
{: #customModels}

カスタム・モデルでの作業の最初のステップは、カスタム・モデルの作成です。 作成後は、メタデータおよび項目を照会または更新したり、不要になったモデルを削除したりすることで、モデルを管理できます。 始める前に、カスタム・モデルの使用法に関する以下の一般的な情報を確認してください。
{: shortdesc}

## 使用上の注意
{: #customGuidelines}

カスタマイズ・インターフェースを使用する際には、以下のガイドラインを考慮してください。

### カスタム音声モデルの所有権
{: #customOwner}

カスタム音声モデルの所有者は、そのモデルの作成に使用した資格情報を持つ {{site.data.keyword.texttospeechshort}} サービスのインスタンスです。カスタマイズ・インターフェースのメソッドを使用してカスタム・モデルを操作するときには、そのサービス・インスタンス用に作成したサービス資格情報を使用する必要があります。

{{site.data.keyword.texttospeechshort}} サービスの同じインスタンス用に取得したサービス資格情報はすべて、そのサービス・インスタンスで作成されたすべてのカスタム・モデルに同じようにアクセスできます。特定のカスタム・モデルへのアクセスを制限するには、別のサービス・インスタンスを作成し、そのサービス・インスタンスの資格情報のみを使用してモデルを操作してください。他のサービス・インスタンスの資格情報では、そのカスタム・モデルを操作対象にすることはできません。

複数のサービス資格情報で所有権を共有する利点は、例えば、いくつかの資格情報が漏えいした場合に、それらを取り消せることです。そうすれば、同じサービス・インスタンス用に新しい資格情報を作成して、元の資格情報で作成されたカスタム・モデルの所有権と利用を維持することができます。

### 要求の記録とデータ・プライバシー
{: #customLogging}

カスタマイズ・インターフェースの呼び出しの要求をサービスが記録するかどうかは、以下のように、要求によって異なります。

-   カスタム音声モデルの作成に使用されたデータ (単語とトランスレーション) は、*記録されません*。カスタム・インターフェースを使用してカスタム音声モデル内の単語とトランスレーションを管理するときに、`X-Watson-Learning-Opt-Out` 要求ヘッダーを設定する必要はありません。サービスの基本モデルを改善するためにお客様のトレーニング・データが使用されることはありません。
-   合成要求でカスタム音声モデルが使用された場合は、データが*記録されます*。合成要求を記録させないようにするには、`X-Watson-Learning-Opt-Out` 要求ヘッダーを `true` に設定する必要があります。

詳しくは、[{{site.data.keyword.watson}} サービスの要求ロギングの制御](/docs/services/watson/getting-started-logging.html)を参照してください。

### 機密保護
{: #customSecurity}

サービスでは、カスタム音声モデルの追加または更新したデータに顧客 ID を関連付けることができます。顧客 ID をカスタム単語に関連付けるには、以下のメソッドで `X-Watson-Metadata` ヘッダーを渡します。

-   `POST /v1/customizations/{customization_id}`
-   `POST /v1/customizations/{customization_id}/words`
-   `PUT /v1/customizations/{customization_id}/words/{word}`

顧客 ID が関連付けられたデータは、必要に応じて `DELETE /v1/user_data` メソッドを使用して削除できます。詳しくは、[機密保護](/docs/services/text-to-speech/information-security.html)を参照してください。

## カスタム・モデルの作成
{: #cuModelsCreate}

新規カスタム・モデルを作成するには、`POST /v1/customizations` メソッドを使用します。新規モデルは、最初に作成したとき、必ず空です。他のメソッドを使用して、そのモデルに単語/トランスレーションのペアを取り込む必要があります。 新規カスタム・モデルの所有者は、そのモデルの作成に使用したサービス資格情報を持つユーザーになります。詳しくは、[カスタム音声モデルの所有権](#customOwner)を参照してください。

要求の本体で、以下の属性を JSON オブジェクトとして渡します。

<table>
  <caption>表 1. <code>POST /v1/customizations</code>
    メソッドのパラメーター</caption>
  <tr>
    <th style="text-align:left; width:18%">パラメーター</th>
    <th style="text-align:center; width:12%">データ型</th>
    <th style="text-align:left">説明</th>
  </tr>
  <tr>
    <td><code>name</code><br/><em>必須</em></td>
    <td style="text-align:center">String</td>
    <td>
      新規カスタム・モデルのユーザー定義の名前。 この名前は、モデルを簡単に識別できるようにラベル付けするために使用されます。 この名前は、
      所有するすべてのカスタム・モデルの間で一意でなければなりません。
    </td>
  </tr>
  <tr>
    <td><code>language</code><br/><em>オプション</em></td>
    <td style="text-align:center">String</td>
    <td>
      カスタム・モデルの言語の ID。デフォルトは <code>en-US</code> です (米国英語の場合)。
    </td>
  </tr>
  <tr>
    <td><code>description</code><br/><em>オプション</em></td>
    <td style="text-align:center">String</td>
    <td>
      新規モデルの説明。 説明はオプションですが、指定することを強くお勧めします。
    </td>
  </tr>
</table>

以下の `curl` コマンドの例では、`curl Test` という名前の新規カスタム・モデルを作成しています。`Content-Type` ヘッダーで、入力のタイプを `application/json` と指定しています。

```bash
curl -X POST -u "apikey:{apikey}"
--header "Content-Type: application/json"
--data "{\"name\":\"curl Test\", \"language\":\"en-US\", \"description\":\"Customization test via curl\"}"
"https://stream.watsonplatform.net/text-to-speech/api/v1/customizations"
```
{: pre}

このメソッドは、新規モデルの GUID (Globally Unique Identifier) が含まれた JSON オブジェクトを返します。この GUID は、モデルおよびその単語を照会、変更、および使用するための呼び出しなど、モデルにアクセスする呼び出しで `customization_id` パラメーターとして使用されます。

```javascript
{
  "customization_id": "64f4807f-a5f1-5867-924f-7bba1a84fe97"
}
```
{: codeblock}

## カスタム・モデルの照会
{: #cuModelsQuery}

既存のカスタム・モデルに関する情報を照会するには、`GET /v1/customizations/{customization_id}` メソッドを使用します。これは、モデルに関するすべての情報 (メタデータと含まれている単語/トランスレーションのペアの両方) を表示する最も直接的な手段です。

```bash
curl -X GET -u "apikey:{apikey}"
"https://stream.watsonplatform.net/text-to-speech/api/v1/customizations/{customization_id}"
```
{: pre}

このメソッドは、以下の形式の JSON オブジェクトとして結果を返します。

```javascript
{
  "customization_id": "64f4807f-a5f1-5867-924f-7bba1a84fe97",
  "owner": "297cfd08-330a-22ba-93ce-1a73f454dd98",
  "created": "2016-07-15T18:12:31.743Z",
  "name": "curl Test",
  "language": "en-US",
  "description": "Customization test via curl",
  "last_modified": "2016-07-15T18:12:31.743Z",
  "words": []
}
```
{: codeblock}

出力には、モデルの作成時に入力された情報に加え、モデルの所有者のサービス資格情報、モデルの言語、およびモデルの作成時刻と最終変更時刻が含まれます。この例の 2 つの時刻は、モデルが作成時以降に変更されていないため、同じになっています。

出力には、モデルのカスタム項目がリストされた `words` 配列も含まれます。このモデルはまだ更新されていないので、この例の配列は空になっています。

## すべてのカスタム・モデルの照会
{: #cuModelsQueryAll}

所有しているすべてのカスタム・モデルに関する情報を表示するには、以下のように `GET /v1/customizations` メソッドを使用します。

```bash
curl -X GET -u "apikey:{apikey}"
"https://stream.watsonplatform.net/text-to-speech/api/v1/customizations"
```
{: pre}

このメソッドは、要求者が所有している各カスタム・モデルのオブジェクトが含まれている JSON 配列を返します。 所有者のサービス資格情報が、`owner` フィールドに表示されます。

```javascript
{
  "customizations": [
      {
      "customization_id": "64f4807f-a5f1-5867-924f-7bba1a84fe97",
      "owner": "297cfd08-330a-22ba-93ce-1a73f454dd98",
      "created": "2016-07-15T19:15:17.926Z",
      "name": "curl Test",
      "language": "en-US",
      "description": "Customization test via curl",
      "last_modified": "2016-07-15T19:15:17.926Z"
    },
    {
      "customization_id": "63f5807f-a4f2-5766-914e-7abb1a84fe97",
      "owner": "297cfd08-330a-22ba-93ce-1a73f454dd98",
      "created": "2016-07-15T18:12:31.743Z",
      "name": "curl Test Two",
      "language": "en-US",
      "description": "Second customization test via curl",
      "last_modified": "2016-07-15T18:23:50.912Z"
    }
  ]
}
```
{: codeblock}

最初のモデルはまだ更新されていないため、`created` 時刻と `last_modified` 時刻が同じになっています。 2 番目のモデルの時刻は異なっており、初期作成時以降に変更されていることを示しています。 この情報には、各モデルに定義されているカスタム項目は含まれません。

## カスタム・モデルの更新
{: #cuModelsUpdate}

カスタム・モデルに関する情報を更新するには、`POST /v1/customizations/{customization_id}` メソッドを使用します。更新は JSON オブジェクトとして指定します。 このメソッドを使用することで、名前や説明の変更に加え、モデル内の単語/トランスレーションのペアの追加や更新も行うことができます。 モデルの作成後にその言語を変更することはできません。

以下の例では、カスタム・モデルの名前と説明を更新しています。 モデルの項目を変更しないことを示すために、`words` パラメーターで空の JSON 配列が送信されています。

```bash
curl -X POST -u "apikey:{apikey}"
--header "Content-Type: application/json"
--data "{\"name\":\"curl Test Update\", \"description\":\"Customization test update via curl\", \"words\":[]}"
"https://stream.watsonplatform.net/text-to-speech/api/v1/customizations/{customization_id}"
```
{: pre}

モデルの単語を更新する方法については、[カスタム・モデルへの複数の単語の追加](/docs/services/text-to-speech/custom-entries.html#cuWordsAdd)を参照してください。

## カスタム・モデルの削除
{: #cuModelsDelete}

不要になったカスタム・モデルを破棄するには、`DELETE /v1/customizations/{customization_id}` メソッドを使用します。削除は永続的なものであるため、このメソッドを使用するのは、モデルが確実に不要になった場合のみにしてください。

```bash
curl -X DELETE -u "apikey:{apikey}"
"https://stream.watsonplatform.net/text-to-speech/api/v1/customizations/{customization_id}"
```
{: pre}
