---

copyright:
  years: 2015, 2019
lastupdated: "2018-06-04"

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

# 사용자 정의 항목 작성을 위한 규칙
{: #rules}

사용자 정의 항목(단어/변환 쌍)으로 사용자 정의 모델을 채우는 데 다음 규칙 및 가이드라인이 적용됩니다.

## 최대 사용자 정의 항목

하나의 사용자 정의 모델에는 20,000개 미만의 사용자 정의 항목이 포함될 수 있습니다.

## 문자 인코딩

서비스는 *word* 및 *translation* 항목에 ASCII 및 UTF-8 문자를 허용합니다. 변환의 경우 ASCII 인코딩(SPR 표기법에 적합) 및 UTF-8 인코딩(IPA 표기법에 적합)을 사용합니다.

## 공백

*word*에는 공백이 포함될 수 없습니다. 서비스는 입력 텍스트에 개별 단어를 구분하기 위해 공백을 사용합니다.

## 대소문자 구분

*word*는 대소문자를 구분합니다. 예를 들어, 사용자 정의 모델에는 `{word='Sun', translation='Sunday'}` 항목이 포함된다고 가정하십시오. 서비스는 기본 발음을 `sun` 단어에 적용하지만 첫 번째 문자가 대문자라는 이유로만 사용자 정의 변환을 `Sun` 단어에 적용합니다.


## 컨텍스트

일부 단어의 발음은 컨텍스트입니다. 예를 들어, 다음과 같은 입력 문장 예를 고려하십시오.

```
St. Anthony lives on Henry St.
```
{: codeblock}

서비스의 기본 발음 규칙은 다음과 같이 이 텍스트를 올바르게 합성합니다.

```
Saint Anthony lives on Henry Street
```
{: codeblock}

그러나 `St.` 문자열에 대한 기본 발음 규칙 겹쳐써서 `saint`로 이를 변환하는 경우 서비스에서는 컨텍스트를 기반으로 한 단어를 더 이상 발음할 수 없습니다. 이러한 변환이 포함된 사용자 정의 음성 모델을 적용하면 서비스가 이전의 입력 문장을 다음과 같이 발음하게 됩니다.

```
Saint Anthony lives on Henry saint
```
{: codeblock}

단어/변환 쌍을 개발할 때 이러한 경우를 고려하십시오.

## 후행 마침표

서비스는 단어와 정확하게 일치하는 입력 텍스트의 해당 문자열에만 사용자 정의 모델의 단어를 적용합니다. 단어 항목의 후행 `.`(마침표)로 단어의 합성 방식이 변경됩니다.

-   *후행 마침표가 없는 단어*에는 실제적으로 어떠한 문자도 포함될 수 있습니다. 문자에는 문자, 숫자, 구두점(후행 마침표 제외), 문자가 아닌 기호(예: %, &amp; 및 @), 따옴표, 괄호, 대괄호 등이 포함됩니다. *변환*에는 공백 및 SSML 형식으로 된 음성 표시를 포함하여 서비스에 대한 법적사항 입력이 포함됩니다.
-   *후행 마침표가 포함된 단어*에는 문자, 마침표 및 내부 어포스트로피만 포함될 수 있습니다(첫 번째 또는 마지막 문자로는 아님). 단어의 *변환*에는 공백 또는 하이픈으로 구분되는 일반적인 철자를 사용한 정규 단어만 포함될 수 있습니다. 여기에는 음성 표시가 포함될 수 없습니다.

후행 마침표가 있는 단어의 예로 "`div.`"를 들 수 있습니다. 사용자 정의 모델에는 `{word='div.', translation='division'}` 항목이 있다고 가정하십시오. 서비스에는 후행 마침표가 포함되지 않고 이에 따라 항목과 일치하지 않으므로 변환이 "`div`" 문자열에 적용되지 않습니다.

## IBM SPR 항목 관련 작업
{: #sprNotes}

SPR(Symbolic Phonetic Representation)은 단어의 발음을 지정하기 위해 {{site.data.keyword.IBM_notm}}에서 개발한 자체 언어 종속 형식입니다. 지원되는 각 언어의 경우 SPR에는 음성 알파벳, 음절 경계에 대한 기호 및 어휘의 강세 수준에 대한 기호가 포함됩니다. 다음 기본 규칙은 SPR 항목의 작성에 적용됩니다.

-   사용자 정의 인터페이스가 단어에 대해 리턴하는 기본 발음은 <code>&#96;</code>(역 따옴표)를 사용하여 시작되고 `[]`(대괄호)로 묶입니다. 예를 들어, 인터페이스는 `tomato` 단어의 다음 발음을 리턴합니다.

    ```xml
    `[.0tx.1ma.0to]
    ```
    {: codeblock}

    사용자 정의 인터페이스의 메소드를 사용하여 단어의 변환을 지정할 때 역 따옴표(`) 및 대괄호([])를 생략하십시오.
-   마침표를 사용하여 변환에서 음절의 시작을 표시할 수 있으나 마침표는 선택사항이며 단어의 발음에 영향을 주지 않습니다. 마침표는 단어의 변환에 포함되는 경우에만 단어의 발음에 나타납니다. 음절 경계를 표시하는 데 공백을 사용하지 마십시오.
-   {{site.data.keyword.IBM_notm}}에서는 필수는 아니지만 `1` 기호로 단어의 기본 강세가 있는 모음을 앞에 배치할 것을 권장합니다. 서비스는 강세를 표시하지 않는 경우 강세가 발생하는 시점을 판별합니다. 또한 `2` 기호를 사용하여 각 보조 강세 위치를 나타낼 수 있으나 `2` 기호 사용도 선택사항입니다. 마침표는 단어의 변환에 포함되는 경우에만 단어의 발음에 나타납니다.

SPR 관련 작업에 대한 자세한 정보는 [IBM SPR 사용](/docs/services/text-to-speech?topic=text-to-speech-sprs)을 참조하십시오.

## 일본어 항목 관련 작업
{: #jaNotes}

추가 규칙 및 `part_of_speech` 필드는 일본어 사용자 정의 음성 모델에서 단어에 대한 항목의 작성에 적용됩니다.

-   유사 발음은 *가타카나* 문자만 포함될 수 있습니다. *간지* 및 *히라가나* 문자는 사용할 수 없습니다.
-   단어에 대한 변환(유사 발음 또는 음성)을 작성하는 경우 선택적인 `part_of_speech` 필드를 지정하여 단어의 품사를 식별할 수 있습니다. 서비스에서는 품사를 사용하여 단어에 대한 정확한 억양을 생성합니다. 완전한 목록은 [일본어 품사](#partsOfSpeech)를 참조하십시오.
-   단어당 하나의 항목만 작성할 수 있으며, 단어당 하나의 품사만 지정할 수 있습니다. 동일한 단어에 대해 다른 품사(예: 명사 및 동사)가 포함된 여러 항목을 작성할 수 없습니다. 모델에 존재하는 단어에 대한 변환을 추가하면 품사를 포함하여 변환의 기존 변환을 겹쳐씁니다.
-   서비스는 사용자 정의 음성 모델에 정의된 단어/변환 쌍에서 가장 긴 일치 단어를 적용합니다. 예를 들어, 사용자 정의 모델에 대해 다음 세 가지 항목을 고려하십시오.

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

    이 항목을 사용하여 서비스가 다음 입력 텍스트를 수신했음을 가정하십시오. <code>&#19968;&#36913;&#38291;&#65326;&#65337;&#65315;&#12434;&#35370;&#21839;&#12375;&#12383;</code>. <code>&#65326;&#65337;&#65315;</code>이 <code>&#65326;&#65337;</code>보다 길고 <code>&#65326;&#65337;&#65315;</code>가 <code>&#65337;&#65315;</code> 앞에서 일치하므로 이 경우 서비스가 <code>&#65326;&#65337;&#65315;</code> 단어와 일치합니다.

### 일본어 품사
{: #partsOfSpeech}

다음 표에서는 일본어 사용자 정의 항목에 대해 지원되는 품사가 나열됩니다. 일본어 사용자 정의 항목에 대한 품사 지정과 관련된 자세한 정보는 [일본어 사용자 정의 모델에 단어 추가](/docs/services/text-to-speech?topic=text-to-speech-customWords#cuJapaneseAdd)를 참조하십시오.

<table style="width:75%">
  <caption>표 1. 일본어 품사</caption>
  <tr>
    <th style="text-align:center"><code>part_of_speech</code> 인수</th>
    <th style="text-align:center; width:35%">일본어 의미</th>
    <th style="text-align:center; width:35%">영어 의미</th>
  </tr>
  <tr>
    <td style="text-align:center"><code>Josi</code></td>
    <td style="text-align:center"><em>Joshi</em></td>
    <td style="text-align:center">분사</td>
  </tr>
  <tr>
    <td style="text-align:center"><code>Mesi</code></td>
    <td style="text-align:center"><em>Meishi</em></td>
    <td style="text-align:center">명사</td>
  </tr>
  <tr>
    <td style="text-align:center"><code>Kigo</code></td>
    <td style="text-align:center"><em>Kigou</em></td>
    <td style="text-align:center">기호</td>
  </tr>
  <tr>
    <td style="text-align:center"><code>Gobi</code></td>
    <td style="text-align:center"><em>Gobi</em></td>
    <td style="text-align:center">굴절</td>
  </tr>
  <tr>
    <td style="text-align:center"><code>Dosi</code></td>
    <td style="text-align:center"><em>Doushi</em></td>
    <td style="text-align:center">동사</td>
  </tr>
  <tr>
    <td style="text-align:center"><code>Jodo</code></td>
    <td style="text-align:center"><em>Jodoushi</em></td>
    <td style="text-align:center">보조 동사</td>
  </tr>
  <tr>
    <td style="text-align:center"><code>Koyu</code></td>
    <td style="text-align:center"><em>Koyuumeishi</em></td>
    <td style="text-align:center">고유 명사</td>
  </tr>
  <tr>
    <td style="text-align:center"><code>Stbi</code></td>
    <td style="text-align:center"><em>Setsubiji</em></td>
    <td style="text-align:center">접미부</td>
  </tr>
  <tr>
    <td style="text-align:center"><code>Suji</code></td>
    <td style="text-align:center"><em>Suuji</em></td>
    <td style="text-align:center">숫자</td>
  </tr>
  <tr>
    <td style="text-align:center"><code>Kedo</code></td>
    <td style="text-align:center"><em>Keiyodoushi</em></td>
    <td style="text-align:center">형용 동사</td>
  </tr>
  <tr>
    <td style="text-align:center"><code>Fuku</code></td>
    <td style="text-align:center"><em>Fukishi</em></td>
    <td style="text-align:center">부사</td>
  </tr>
  <tr>
    <td style="text-align:center"><code>Keyo</code></td>
    <td style="text-align:center"><em>Keiyoshi</em></td>
    <td style="text-align:center">형용 동사</td>
  </tr>
  <tr>
    <td style="text-align:center"><code>Stto</code></td>
    <td style="text-align:center"><em>Settoji</em></td>
    <td style="text-align:center">접두부</td>
  </tr>
  <tr>
    <td style="text-align:center"><code>Reta</code></td>
    <td style="text-align:center"><em>Rentaishi</em></td>
    <td style="text-align:center">한정사</td>
  </tr>
  <tr>
    <td style="text-align:center"><code>Stzo</code></td>
    <td style="text-align:center"><em>Setsuzokushi</em></td>
    <td style="text-align:center">접속사</td>
  </tr>
  <tr>
    <td style="text-align:center"><code>Kato</code></td>
    <td style="text-align:center"><em>Kantoushi</em></td>
    <td style="text-align:center">감탄사</td>
  </tr>
  <tr>
    <td style="text-align:center"><code>Hoka</code></td>
    <td style="text-align:center"><em>Hoka</em></td>
    <td style="text-align:center">기타</td>
  </tr>
</table>
