---

copyright:
  years: 2015, 2019
lastupdated: "2019-06-21"

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

# 表现力 SSML
{: #expressive}

缺省情况下，{{site.data.keyword.texttospeechfull}} 服务会以中性陈述风格来合成文本。服务扩展了 SSML：增加了 `<express-as>` 元素，通过将文本转换为各种说话风格的合成语音来提供表现力。此元素类似于 SSML 元素 `<say-as>`，后者用于为日期、时间和数字等格式化文本指定文本规范化。
{: shortdesc}

## 语言支持
{: #languages-expressive}

服务仅支持对标准美国英语 Allison 声音 (`en-US_AllisonVoice`) 使用表现力。神经 `en-US_AllisonV3Voice` 声音不支持表现力。将此元素用于不支持的声音会返回错误。

## express-as 元素
{: #ssml-express-as}

可以将 `<express-as>` 元素应用于整个文本、一个句子或片段（如短语或词）。此元素接受一个必需属性 `type`，描述要用于指定文本的表达的类型：`GoodNews`、`Apology` 或 `Uncertainty`。

### GoodNews
{: #goodnews}

`GoodNews` 表达积极、乐观的消息。

```xml
<express-as type="GoodNews">
  很高兴通知您，您的按揭贷款申请已获批准。
</express-as>

<express-as type="GoodNews">
  好消息：我能帮您减少每月帐单的付款金额！
</express-as>

<express-as type="GoodNews">
  恭喜订婚！你们真是天造地设的一对！
</express-as>
<express-as type="GoodNews">
  哇，祝贺您升职！这真是重要的职位！
</express-as>
```
{: codeblock}

### Apology
{: #apology}

`Apology` 表达令人遗憾的消息。

```xml
<express-as type="Apology">
  很遗憾，下一班飞机将在 5 小时后起飞。
</express-as>

<express-as type="Apology">
  非常抱歉对您的服务不周。
</express-as>

<express-as type="Apology">
  请原谅我删除了您的文件。这是意外。
</express-as>
<express-as type="Apology">
  有什么办法能让我弥补我的过失吗？
</express-as>
```
{: codeblock}

### Uncertainty
{: #uncertainty}

`Uncertainty` 传达不确定的询问消息。

```xml
<express-as type="Uncertainty">
  她有可能还在办公室吗？她告诉我说她可能会早走。
</express-as>

<express-as type="Uncertainty">
  抱歉，我想是我听错了。是周五还是周六？
</express-as>

<express-as type="Uncertainty">
  您能再解释一遍吗？我不确定是否理解了。
</express-as>
<express-as type="Uncertainty">
  很抱歉，我没听清您的姓名。请您再重复一遍好吗？
</express-as>
```
{: codeblock}

## 表现力示例

以下示例说明了如何在 `POST /v1/synthesize` 方法的 `text` 属性中使用所有三种形式的表现力。要合成的文本位于 SSML 根 `<speak>` 元素范围内。

```xml
{
  "text": "<speak>
    我被指派来处理您的订单状态请求。
    <express-as type=\"Apology\">
      我很遗憾地通知您，您请求的货品延期交货了。
      给您带来不便，我们深表歉意。
    </express-as>
    <express-as type=\"Uncertainty\">
      我们不清楚货品何时有货。可能是下周，
      但目前我们并不确定。
    </express-as>
    <express-as type=\"GoodNews\">
      但为了让您满意，我们将给予您的订单 50% 的折扣！
    </express-as>
  </speak>"
}
```
{: codeblock}
