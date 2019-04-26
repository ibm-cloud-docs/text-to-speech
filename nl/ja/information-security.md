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

# 機密保護
{: #information-security}

{{site.data.keyword.IBM}} は、お客様やパートナーに、データ・プライバシー、セキュリティー、およびガバナンスに関する革新的なソリューションを提供します。
{: shortdesc}

お客様自身が欧州連合の一般データ保護規則を含む各種法令を遵守するために必要な措置を講ずるのはお客様の責任です。 お客様のビジネスに影響を及ぼす可能性のある関連法令の特定およびそれらの解釈、ならびにかかる関連法令を遵守するためにお客様が講ずるべき必要措置に関する助言は、お客様の責任により適格な弁護士から得るものとします。
{: important}

本書に記載の製品、サービス、および他の機能が、すべてのお客様の状況に適しているとは限らず、使用する際に制約を受ける場合があります。 {{site.data.keyword.IBM_notm}} は、法律、会計または監査に関する助言を提供することはしませんし、IBM のサービスまたは製品が、お客様のあらゆる法令遵守の裏付けとなる表明または保証もいたしません。

作成した {{site.data.keyword.cloud}} {{site.data.keyword.watson}} リソースについて GDPR に関するサポートを要請する必要がある場合

-   欧州連合 (EU) 内のリソースについては、[EU で作成された {{site.data.keyword.cloud_notm}} Watson リソースについてのサポートの要求](/docs/services/watson/getting-started-gdpr-sar.html#request-EU)を参照してください。
-   EU 外のリソースについては、[EU 外にあるリソースについてのサポートの要求](/docs/services/watson/getting-started-gdpr-sar.html#request-non-EU)を参照してください。

## 欧州連合一般データ保護規則 (GDPR)
{: #gdpr}

{{site.data.keyword.IBM_notm}} は、お客様やパートナーにデータ・プライバシー、セキュリティー、およびガバナンスに関する革新的なソリューションを提供して、GDPR に準拠するための準備を支援します。

{{site.data.keyword.IBM_notm}} 自身の GDPR 対応準備、ならびに、お客様の準拠の準備を支援するために IBM が提供している GDPR 機能とオファリングについて詳しくは、[こちら ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](../../icons/launch-glyph.svg "外部リンク・アイコン")](http://www.ibm.com/gdpr){: new_window} を参照してください。

## Text to Speech サービスでのデータのラベル付けと削除
{: #gdpr-text-to-speech}

{{site.data.keyword.texttospeechfull}} サービスでは、音声合成要求とカスタム音声モデルに関連付けられたすべてのデータを削除できます。データを削除するには、以下を実行する必要があります。

1.  `X-Watson-Metadata` ヘッダーを使用して、要求を介してサービスに渡すデータに顧客 ID を関連付けます ([顧客 ID の指定](#specify-customer-id)を参照)。
1.  `DELETE /v1/user_data` メソッドを使用して、指定した顧客 ID に関連付けられたすべてのデータを削除します ([データの削除](#delete-pi)を参照)。

デフォルトでは、データに顧客 ID は関連付けられません。

試験的な機能およびベータ機能は実稼働環境で使用するためのものではないので、データのラベル付けおよび削除が期待どおりに機能することは保証されません。データのラベル付けと削除を必要とするソリューションを実装する場合は、試験的な機能およびベータ機能を使用しないでください。
{: note}

### 顧客 ID の指定
{: #specify-customer-id}

顧客 ID をデータに関連付けるには、要求に `X-Watson-Metadata` ヘッダーを指定して情報を渡します。このヘッダーの引数としてストリング `customer_id={id}` を渡します。次の例では、`POST /v1/synthesize` 要求で渡すデータに、顧客 ID `my_ID` を関連付けています。

```bash
curl -X POST -u "apikey:{apikey}"
--header "X-Watson-Metadata: customer_id=my_ID"
--header "Content-Type: application/json"
--header "Accept: audio/wav"
--data "{\"text\":\"hello world\"}"
--output hello_world.wav
"https://stream.watsonplatform.net/text-to-speech/api/v1/synthesize"
```

顧客 ID には、`;` (セミコロン) と `=` (等号) を除く任意の文字を含めることができます。顧客 ID には、ランダムなストリングまたは汎用的なストリングを指定してください。E メール・アドレスや Twitter ID など、個人の特定が可能なストリングは使用しないでください。要求ごとに別の顧客 ID を指定できます。指定した顧客 ID は、要求に使用した資格情報を持つサービス・インスタンスに関連付けられます。そのため、そのサービス・インスタンスの資格情報を使用しないと、ID に関連付けられたデータは削除できません。

`X-Watson-Metadata` ヘッダーは、以下のメソッドで使用します。

-   HTTP 要求の場合
    -   `POST /v1/synthesize`
    -   `GET /v1/synthesize`

    顧客 ID が、要求で送信するデータに関連付けられます。

-   WebSocket 要求の場合
    -   `/v1/synthesize`

    `x-watson-metadata` 照会パラメーターに顧客 ID を指定して、要求で送信するデータにその ID を関連付けます。照会パラメーターの引数は URL エンコードする必要があります (例：`customer_id%3dmy_ID`)。

-   カスタム音声モデルにカスタム単語を追加する要求の場合
    -   `POST /v1/customizations/{customization_id}`
    -   `POST /v1/customizations/{customization_id}/words`
    -   `PUT /v1/customizations/{customization_id}/words/{word}`

    顧客 ID が、要求で追加または更新するカスタム単語に関連付けられます。

### データの削除
{: #delete-pi}

顧客 ID に関連付けられたすべてのデータを削除するには、`DELETE /v1/user_data` メソッドを使用します。ストリング `customer_id={id}` を要求の照会パラメーターとして渡します。次の例は、顧客 ID `my_ID` のすべてのデータを削除します。

```bash
curl -X DELETE -u "apikey:{apikey}"
"https://stream.watsonplatform.net/text-to-speech/api/v1/user_data?customer_id=my_ID"
```

`/v1/user_data` メソッドは、情報の追加に使用されたメソッドにかかわらず、指定した顧客 ID に関連付けられているすべてのデータを削除します。顧客 ID に関連付けられたデータがない場合は、このメソッドを実行しても何の効果もありません。要求を発行するときには、顧客 ID をデータに関連付けたときに使用した同じサービス・インスタンスの資格情報を使用する必要があります。
