---

copyright:
  years: 2019
lastupdated: "2019-03-19"

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

# 高可用性と災害復旧
{: #ha-dr}

{{site.data.keyword.texttospeechfull}} サービスは、どの {{site.data.keyword.cloud_notm}} ロケーション (ダラスやワシントン DC など) でも高可用性が確保されています。ただし、ロケーション全体が影響を受けるような災害から復旧するためには、計画と準備が必要です。
{: shortdesc}

サービスの構成、カスタマイズ、使用法を把握しておく必要があります。新しいロケーションでサービスのインスタンスを再作成し、すべてのロケーションのデータを復元できるように準備しておく必要もあります。

## 高可用性
{: #high-availability}

{{site.data.keyword.texttospeechshort}} サービスは高可用性をサポートしており、単一障害点は存在しません。このサービスは、{{site.data.keyword.cloud_notm}} に用意されている複数ゾーン地域 (MZR) 機能によって、高可用性を自動的かつ透過的に実現します。

{{site.data.keyword.cloud_notm}} では、1 つのロケーションの中で、単一障害点を共有しない複数のゾーンを利用できます。1 つの地域の複数のゾーン間で自動的に負荷分散を行うこともできます。

## 災害復旧
{: #disaster-recovery}

{{site.data.keyword.cloud_notm}} のロケーションでデータ消失の可能性のある重大な障害が発生すると、災害復旧が問題になります。ロケーションをまたいで MZR を利用することはできないので、ロケーションが利用不能になった場合は、{{site.data.keyword.IBM_notm}} がそのロケーションを再びオンラインにするまで待たなければなりません。基盤になっているデータ・サービスがその障害でダメージを受けた場合は、{{site.data.keyword.IBM_notm}} がそのデータ・サービスを復旧するまで待つ必要もあります。

壊滅的な障害が発生した場合は、{{site.data.keyword.IBM_notm}} がデータベース・バックアップからデータを復旧できない可能性があります。その場合は、お客様がデータをリストアして、サービス・インスタンスを最新の状態に戻す必要があります。データのリストア先は、同じロケーションにすることも別のロケーションにすることもできます。

{{site.data.keyword.texttospeechshort}} サービスについては、{{site.data.keyword.cloud_notm}} に保管されるのはカスタム音声モデルのデータだけです。災害復旧計画の一環として、カスタム音声モデルの把握、保存、リストアの準備を行ってください。

### カスタム音声モデルのバックアップ
{: #disaster-recovery-backup}

カスタム音声モデルと各モデルのカスタム項目について以下の情報を保存しておいてください。

-   すべてのカスタム音声モデルと各モデルの定義のリスト。カスタム・モデルに関する情報をリストするには、以下のようにします。
    -   `GET /v1/customizations` メソッドを使用して、すべてのカスタム・モデルに関する情報をリストします。詳しくは、[すべてのカスタム・モデルの照会](/docs/services/text-to-speech/custom-models.html#cuModelsQueryAll)を参照してください。
    -   `GET /v1/customizations/{customization_id}` メソッドを使用して、指定したカスタム・モデルに関する情報をリストします。詳しくは、[カスタム・モデルの照会](/docs/services/text-to-speech/custom-models.html#cuModelsQuery)を参照してください。
-   カスタム音声モデルに含まれているすべてのカスタム項目 (単語/トランスレーションのペア) に関する情報。
    -   `GET /v1/customizations/{customization_id}/words` メソッドを使用して、カスタム・モデルに含まれているすべての単語/トランスレーションのペアに関する情報をリストします。詳しくは、[カスタム・モデルのすべての単語の照会](/docs/services/text-to-speech/custom-entries.html#cuWordsQueryModel)を参照してください。
    -   `GET /v1/customizations/{customization_id}/words/{word}` メソッドを使用して、カスタム・モデルに含まれている指定した単語/トランスレーションのペアに関する情報をリストします。詳しくは、[カスタム・モデルの単一の単語の照会](/docs/services/text-to-speech/custom-entries.html#cuWordQueryModel)を参照してください。

この情報を、障害発生時にカスタム音声モデルを再作成できる形式で保存しておくことがベスト・プラクティスです。カスタム・モデルとカスタム項目に関する情報を積極的に保守し、以下のセクションに記載する呼び出しを事前に準備しておけば、最速のリカバリーが可能になります。

### カスタム音声モデルのリストア
{: #disaster-recovery-restore}

復旧災害が必要な場合は、バックアップ情報を使用して、カスタム音声モデルと各モデルのカスタム項目を再作成できます。

1.  カスタム音声モデルを再作成するには、`POST /v1/customizations` メソッドを使用します。詳しくは、[カスタム・モデルの作成](/docs/services/text-to-speech/custom-models.html#cuModelsCreate)を参照してください。
1.  単語/トランスレーションの複数のペアをカスタム音声モデルに追加するには、`POST /v1/customizations/{customization_id}/words` メソッドを使用します。詳しくは、[カスタム・モデルへの複数の単語の追加](/docs/services/text-to-speech/custom-entries.html#cuWordsAdd)を参照してください。
1.  単語/トランスレーションの 1 つのペアをカスタム音声モデルに追加するには、`POST /v1/customizations/{customization_id}/words/{word}` メソッドを使用します。詳しくは、[カスタム・モデルへの単一の単語の追加](/docs/services/text-to-speech/custom-entries.html#cuWordAdd)を参照してください。

すべてのカスタム項目を 1 回で追加することも、グループに分けて追加することも、1 つずつ追加することも可能です。
