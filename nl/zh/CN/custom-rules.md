---

copyright:
  years: 2015, 2019
lastupdated: "2018-03-07"

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

# 用于创建定制条目的规则
{: #rules}

以下规则和准则适用于使用定制条目（词/转换项对）填充定制模型。

## 最大定制条目数

单个定制模型最多可以包含 20,000 个定制条目。

## 字符编码

服务接受对 *word* 和 *translation* 条目进行 ASCII 和 UTF-8 字符编码。对于转换项，请将 ASCII 编码用于 SPR 表示法，将 UTF-8 编码用于 IPA 表示法。

## 空格

*word* 不能包含空格。服务使用空格来对输入文本中各个词定界。

## 区分大小写

*word* 是区分大小写的。例如，假定定制模型包含条目 `{word='Sun', translation='Sunday'}`。服务会将其缺省发音应用于词 `sun`，但会将定制转换项应用于词 `Sun`，因为只有后者的首字母大写。


## 上下文相关

一些词的发音是上下文相关的。例如，假设有以下示例输入语句：

```
St. Anthony lives on Henry St.
```
{: codeblock}

服务的缺省发音规则会正确地将此文本合成为：

```
Saint Anthony lives on Henry Street
```
{: codeblock}

但是，如果覆盖字符串 `St.` 的缺省发音规则，以将其转换为 `saint`，那么服务就无法再根据上下文对该词发音。应用包含此类转换项的定制声音模型会导致服务将上述输入语句发音为：

```
Saint Anthony lives on Henry saint
```
{: codeblock}

在开发词/转换项对时，请考虑此类情况。

## 尾部句点

服务仅将定制模型中的词应用于输入文本中与该词完全匹配的那些字符串。word 条目中的尾部 `.`（句点）会更改词的合成方式：

-   *没有结尾句点的词*几乎可以包含任何字符。字符包括字母、数字、标点（非尾部句点）、非字母符号（例如，%、&amp; 和 @）、引号、圆括号、方括号等。该词的*转换项*可以包含对服务的任何合法输入，包括 SSML 格式的空格和拼音表示法。
-   *具有尾部句点的词*只能包含字母、句点和内部撇号（不作为第一个或最后一个字符）。该词的*转换项*只能包含用空格或连字符分隔的正常拼写的普通词。不能包含拼音表示法。

具有尾部句点的词的示例为“`div.`”。假定定制模型包含条目 `{word='div.', translation='division'}`。服务不会将转换项应用于字符串“`div`”，因为它不包含尾部句点，因此与该条目不匹配。

## 使用 IBM SPR 条目
{: #sprNotes}

符号拼音表示法 (SPR) 是一种专有的语言相关格式，由 {{site.data.keyword.IBM_notm}} 开发，用于指定词的发音。对于每种支持的语言，SPR 都包含音位 alphabet、表示音节边界的符号以及表示词重音级别的符号。以下基本规则适用于创建 SPR 条目：

-   定制接口对词返回的缺省发音以 <code>&#96;</code>（反引号）开头，并用 `[]`（方括号）括起。例如，对于词 `tomato`，接口会返回以下发音：

    ```xml
    `[.0tx.1ma.0to]
    ```
    {: codeblock}

    使用定制接口的方法来指定词的转换项时，请省略反引号和方括号。
-   可以使用句点来指示转换项中音节的开头，但句点是可选的，不会影响词的发音。仅当在词的转换项中包含句点时，句点才会出现在词的发音中。不要使用空格来指示音节边界。
-   {{site.data.keyword.IBM_notm}} 建议您在词的主重读元音前面添加 `1` 符号，但这并不是严格必需的。如果未使用该符号指示，服务会自行确定出现重音的位置。您还可以使用 `2` 符号来指示每个次重音位置，但 `2` 符号的使用也是可选的。仅当在词的转换项中包含这些符号时，这些符号才会出现在词的发音中。

有关使用 SPR 的更多信息，请参阅[使用 IBM SPR](/docs/services/text-to-speech/SPRs.html)。

## 使用日语条目
{: #jaNotes}

额外规则和 `part_of_speech` 字段适用于创建日语定制声音模型中词的条目：

-   近似读音转换项只能包含*片假名*字符。不允许使用*日本汉字*和*平假名*字符。
-   创建词的转换项（近似读音或拼音）时，还可以指定可选的 `part_of_speech` 字段来标识词的词性。服务会使用词性来为词生成正确的语调。有关完整列表，请参阅[日语词性](#partsOfSpeech)。
-   对于任何词，都只能创建一个条目，并且只能指定一个词性。对于同一个词，不能创建具有不同词性（例如，名词和动词）的多个条目。向模型中存在的词添加转换项会覆盖该词的现有转换项，包括其词性。
-   服务会从为定制声音模型定义的词/转换项对中，选择最长的匹配词来应用。例如，假设定制模型有以下三个条目。

    <pre><code>{
      "words": [
        {
          "word": "&#65326;&#65337;",
          "translation": "&#12491;&#12517;&#12540;&#12520;&#12540;&#12463;",
          "part_of_speech": "Mesi"
        },
        {
          "word": "&#65326;&#65337;&#65315;",
          "translation": "&#12491;&#12517;&#12540;&#12520;&#12540;&#12463;&#12471;&#12486;&#12451;",
          "part_of_speech": "Mesi"
        },
        {
          "word": "&#65337;&#65315;",
          "translation": "&#12520;&#12467;&#12495;&#12510;&#12481;&#12517;&#12540;&#12459;&#12460;&#12452;",
          "part_of_speech": "Mesi"
        }
      ]
    }</code></pre>

    对于上述条目，假定服务收到以下输入文本：<code>&#19968;&#36913;&#38291;&#65326;&#65337;&#65315;&#12434;&#35370;&#21839;&#12375;&#12383;</code>. 在本例中，服务匹配的是词 <code>&#65326;&#65337;&#65315;</code>，因为 <code>&#65326;&#65337;&#65315;</code> 比 <code>&#65326;&#65337;</code> 长，并且 <code>&#65326;&#65337;&#65315;</code> 在 <code>&#65337;&#65315;</code> 之前匹配。

### 日语词性
{: #partsOfSpeech}

下表列出了日语定制条目支持的词性。有关指定日语定制条目词性的更多信息，请参阅[向日语定制模型添加词](/docs/services/text-to-speech/custom-entries.html#cuJapaneseAdd)。

<table style="width:75%">
  <caption>表 1. 日语词性</caption>
  <tr>
    <th style="text-align:center"><code>part_of_speech</code> 自变量</th>
    <th style="text-align:center; width:35%">日语含义</th>
    <th style="text-align:center; width:35%">英语含义</th>
  </tr>
  <tr>
    <td style="text-align:center"><code>Josi</code></td>
    <td style="text-align:center"><em>Joshi</em></td>
    <td style="text-align:center">分词</td>
  </tr>
  <tr>
    <td style="text-align:center"><code>Mesi</code></td>
    <td style="text-align:center"><em>Meishi</em></td>
    <td style="text-align:center">名词</td>
  </tr>
  <tr>
    <td style="text-align:center"><code>Kigo</code></td>
    <td style="text-align:center"><em>Kigou</em></td>
    <td style="text-align:center">符号</td>
  </tr>
  <tr>
    <td style="text-align:center"><code>Gobi</code></td>
    <td style="text-align:center"><em>Gobi</em></td>
    <td style="text-align:center">词形变化</td>
  </tr>
  <tr>
    <td style="text-align:center"><code>Dosi</code></td>
    <td style="text-align:center"><em>Doushi</em></td>
    <td style="text-align:center">动词</td>
  </tr>
  <tr>
    <td style="text-align:center"><code>Jodo</code></td>
    <td style="text-align:center"><em>Jodoushi</em></td>
    <td style="text-align:center">助动词</td>
  </tr>
  <tr>
    <td style="text-align:center"><code>Koyu</code></td>
    <td style="text-align:center"><em>Koyuumeishi</em></td>
    <td style="text-align:center">专有名词</td>
  </tr>
  <tr>
    <td style="text-align:center"><code>Stbi</code></td>
    <td style="text-align:center"><em>Setsubiji</em></td>
    <td style="text-align:center">后缀</td>
  </tr>
  <tr>
    <td style="text-align:center"><code>Suji</code></td>
    <td style="text-align:center"><em>Suuji</em></td>
    <td style="text-align:center">数词</td>
  </tr>
  <tr>
    <td style="text-align:center"><code>Kedo</code></td>
    <td style="text-align:center"><em>Keiyodoushi</em></td>
    <td style="text-align:center">形容词</td>
  </tr>
  <tr>
    <td style="text-align:center"><code>Fuku</code></td>
    <td style="text-align:center"><em>Fukishi</em></td>
    <td style="text-align:center">副词</td>
  </tr>
  <tr>
    <td style="text-align:center"><code>Keyo</code></td>
    <td style="text-align:center"><em>Keiyoshi</em></td>
    <td style="text-align:center">形容词</td>
  </tr>
  <tr>
    <td style="text-align:center"><code>Stto</code></td>
    <td style="text-align:center"><em>Settoji</em></td>
    <td style="text-align:center">前缀</td>
  </tr>
  <tr>
    <td style="text-align:center"><code>Reta</code></td>
    <td style="text-align:center"><em>Rentaishi</em></td>
    <td style="text-align:center">限定词</td>
  </tr>
  <tr>
    <td style="text-align:center"><code>Stzo</code></td>
    <td style="text-align:center"><em>Setsuzokushi</em></td>
    <td style="text-align:center">连词</td>
  </tr>
  <tr>
    <td style="text-align:center"><code>Kato</code></td>
    <td style="text-align:center"><em>Kantoushi</em></td>
    <td style="text-align:center">感叹词</td>
  </tr>
  <tr>
    <td style="text-align:center"><code>Hoka</code></td>
    <td style="text-align:center"><em>Hoka</em></td>
    <td style="text-align:center">其他</td>
  </tr>
</table>
