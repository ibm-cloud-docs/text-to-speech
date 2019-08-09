---

copyright:
  years: 2015, 2019
lastupdated: "2019-06-06"

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

# IBM SPR 사용
{: #sprs}

{{site.data.keyword.texttospeechfull}} 서비스는 단어의 소리를 나타내도록 표준 IPA(International Phonetic Alphabet) 및 {{site.data.keyword.IBM}} Symbolic Phonetic Representation(SPR) 표기법을 모두 지원합니다. SPR은 단어의 발음, 단어를 구성하는 소리, 소리가 음절로 구분되는 방식 및 강조되는 음절을 나타내는 음성 코딩입니다. SPR은 IPA의 대체 표시입니다.
{: shortdesc}

다음 절에서는 {{site.data.keyword.IBM_notm}} SPR 표기법을 소개합니다. IPA가 표준 표기법이므로 문서는 IPA에 대한 기본 사용 정보를 제공하지 않습니다. 간략한 사용 지침을 보려면 [IPA 관련 작업](#ipa)을 참조하십시오.

## IBM SPR에 대한 소개
{: #introduction-SPRs}

SPR 발음은 SSML(SSpeech Synthesis Markup Language )의 [음소 요소](/docs/services/text-to-speech?topic=text-to-speech-elements#phoneme_element)로 정의됩니다. 이는 큰따옴표로 묶은 지정된 언어에 적합한 일련의 허용 가능한 기호로 구성됩니다. 기호는 `<phoneme>` 요소 내의 단어가 발음되는 방식을 정의합니다. 요소의 `alphabet` 속성에는 발음이 SPR에 정의되고 `ph` 속성이 발음을 정의함을 나타내는 `ibm` 값이 있습니다. 다음은 미국 영어의 *through* 및 *shocking* 단어에 대한 올바른 SPR 표기법의 예입니다.

```xml
<phoneme alphabet="ibm" ph=".1Tru">through</phoneme>
<phoneme alphabet="ibm" ph=".1Sa.0kIG">shocking</phoneme>
```
{: codeblock}

정의에서 `.`(마침표)는 새 음절의 시작 부분을 표시하고, 숫자 `1` 및 `0`은 음절의 강세 레벨을 나타내고, 문자는 미국 영어 발음의 특정 소리를 나타냅니다. 필수 스펙을 따르지 않은 SPR 항목은 올바르지 않습니다.

## 음절 경계

`.`(마침표)를 사용하여 각 음절의 시작 부분을 표시할 수 있습니다. 그러나 언어의 올바른 음성을 보존하기 위해 서비스는 일부 경우에서 마침표를 사용하지 않도록 선택할 수 있습니다(예를 들어, 음절 경계가 언어의 올바르지 않거나 부자연스러운 위치에 배치된 경우). 일반적으로 사용자가 음절 경계 또는 단어 발음의 다른 측면에서 유효한 환경 설정을 표시할 수 있는 경우 서비스는 이러한 요청을 따릅니다.

## 음절 강세

다음 표의 기호를 사용하여 발음에 필요한 음절 강세를 표시할 수 있습니다. {{site.data.keyword.IBM_notm}}에서는 SPR 또는 IPA에서 발음의 기본 강세를 표시할 것을 권장합니다. 그러나 두 형식 모두에서 음절 강세 표시는 선택사항입니다. 서비스는 강세를 표시하지 않는 경우 강세가 발생하는 시점을 판별합니다.

<table style="width:80%">
  <caption>표 1. 음절 강세</caption>
  <tr>
    <th style="width:22%; text-align:center; vertical-align:bottom">
      IBM SPR 기호
    </th>
    <th style="width:22%; text-align:center; vertical-align:bottom">
      IPA 기호
    </th>
    <th style="width:22%; text-align:center; vertical-align:bottom">
      IPA 유니코드
    </th>
    <th style="text-align:left; vertical-align:bottom">
      의미
    </th>
  </tr>
  <tr>
    <td style="text-align:center">
1
    </td>
    <td style="text-align:center">
      <code>&#712;</code>
    </td>
    <td style="text-align:center">
      02C8
    </td>
    <td>
      기본 강세
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
2
    </td>
    <td style="text-align:center">
      <code>&#716;</code>
    </td>
    <td style="text-align:center">
      02CC
    </td>
    <td>
      보조 강세
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      0
    </td>
    <td style="text-align:center">기호 없음</td>
    <td style="text-align:center">값 없음</td>
    <td>
      강세 없음
    </td>
  </tr>
</table>

**참고:**

-   프랑스어의 IPA에서는 음절 강세 기호가 무시됩니다 프랑스어의 SPR에서는 음절 강세는 무시되지 않습니다. 지정된 경우 음절 강세는 음절의 모음 앞에 바로 와야 합니다. SPR에서 프랑스어의 음절 강세는 다른 언어보다 더 엄격합니다. 강세 기호가 올바르지 않은 위치에 있으면 오류가 발생합니다.
-   스페인어 및 이탈리아어의 SPR에서는 `1`(기본 강세)만 지정할 수 있습니다. 보조 강세를 지정하거나 강세 없음으로 지정하는 경우 오류가 발생합니다.
-   일본어의 SPR에서는 `1`(기본 강세) 및 `0`(강세 없음)이 지원됩니다. 보조 강세를 지정하는 경우 오류가 발생합니다.

사용자는 음절 경계 내에 음절 강세 마커를 배치해야 하지만 항상 음절의 모음에서 왼쪽에 배치되어야 합니다. 강세 모음의 왼쪽 어느 위치에서나 마커를 배치할 수 있습니다. 예를 들어, 다음 SPR의 각 예에서는 *construction* 단어의 올바른 모음에 기본 강세를 배치합니다.

```xml
<phoneme alphabet="ibm" ph="kXn1strHkSXn">construction</phoneme>
<phoneme alphabet="ibm" ph="kXns1trHkSXn">construction</phoneme>
<phoneme alphabet="ibm" ph="kXnst1rHkSXn">construction</phoneme>
<phoneme alphabet="ibm" ph="kXnstr1HkSXn">construction</phoneme>
```
{: codeblock}

## 언어음 기호

각 언어는 해당 언어의 언어음을 표시하기 위해 SPR 기호의 자체 인벤토리를 사용합니다. 다음 규칙은 SPR 기호를 지정하는 데 적용됩니다.

-   문자는 대소문자를 구분함에 따라 `e` 및 `E`와 같이 두 가지 다른 소리를 나타냅니다.
-   2자 및 3자 기호는 작은따옴표으로 묶여야 합니다. 예를 들어, 독일어 단어의 *heim*의 `aj` 기호는 `"h'aj'm"`입니다.
-   서비스는 언어에서 허용되지 않은 소리 기호가 포함된 올바르지 않은 SPR 정의를 고려합니다.

SPR 형식에서 단어의 발음을 정의할 때 다음 사항도 고려하십시오.

-   모든 언어의 소리에는 해당 언어 내에서 특정한 분포 특성이 있습니다. 예를 들어, 영어의 모든 통용어에서 *sing*(`".1sIG"`)의 `G` 소리는 단어의 시작 부분에서 발음되지 않습니다. 특히 분포도가 좁은 기타 미국 영어 소리는 성문 파열음(`?`), 설탄음(`F`) 및 음절의 비음(`N`)입니다. 컨텍스트에서 일반적으로 표시되지 않는 소리 기호를 입력하는 경우 생성되는 음성이 비정상적으로 발음될 수 있습니다.
-   {{site.data.keyword.texttospeechshort}} 서비스는 소리가 자연어의 특정 컨텍스트에서 변경되는 프로세스를 반영하기 위해 정교한 언어적 규칙 세트를 입력에 적용합니다. 예를 들어, 미국 영어에서 *write* 단어(`".1r1Yt"`)의 `t` 소리는 *writer*(`".1rY.0FR"`)의 설탄음(`F`)으로 발음됩니다. SPR 입력에는 일반적인 입력 텍스트와 같은 수정사항이 발생합니다. 이 예에서 `".1rY.0tR"` 또는 `".1rY.0FR"`은 생성된 음성에 영향을 주지 않습니다.

## IPA 관련 작업
{: #ipa}

다음 정보는 IPA 표기법의 발음 관련 작업에 적용됩니다.

-   문서화된 IPA 기호만 사용합니다. 여러 IPA 기호(또는 기호 조합)가 SPR 기호에 맞게 나열되는 경우 모든 항목은 단일 SPR 기호와 동등합니다. 이 경우 서비스는 모든 IPA 기호를 동일하게 간주하고 IPA 시스템에서 설명할 미묘하거나 지역적 차이를 인식하지 못합니다.
-   IPA 유니코드 값으로 IPA 발음을 지정할 수도 있습니다. 다음 절에 나열된 언어별 표에는 IPA 기호 및 동등한 IPA 유니코드 값이 문서화되어 있습니다. IPA 유니코드 값을 사용하는 발음의 예는 [발음 요소](/docs/services/text-to-speech?topic=text-to-speech-elements#phoneme_element)를 참조하십시오.

자세히 알아보려면 다음을 참조하십시오.

-   IPA에 관한 자세한 정보는 [International Phonetic Alphabet](https://wikipedia.org/wiki/International_Phonetic_Alphabet){: external}을 참조하십시오.
-   유니코드의 음성 기호에 대한 자세한 정보는 [유니코드의 음성 기호](https://wikipedia.org/wiki/Phonetic_symbols_in_Unicode){: external}를 참조하십시오.

## 지원되는 언어
{: #supportedLanguages}

다음 페이지에서는 각 언어별로 SPR 기호, IPA 기호 및 동등한 IPA 유니코드 값을 문서화합니다. 해당 언어의 단어로 각 기호의 예가 표시됩니다. 통용어 차이로 인해 예가 발음과 항상 일치하지 않을 수 있습니다.

-   [브라질 포르투갈어 기호](/docs/services/text-to-speech?topic=text-to-speech-ptSymbols)
-   [영국 영어 기호](/docs/services/text-to-speech?topic=text-to-speech-gbSymbols)
-   [프랑스어 기호](/docs/services/text-to-speech?topic=text-to-speech-frSymbols)
-   [독일어 기호](/docs/services/text-to-speech?topic=text-to-speech-deSymbols)
-   [이탈리아어 기호](/docs/services/text-to-speech?topic=text-to-speech-itSymbols)
-   [일본어 기호](/docs/services/text-to-speech?topic=text-to-speech-jaSymbols)
-   [스페인어 기호](/docs/services/text-to-speech?topic=text-to-speech-esSymbols)
-   [미국 영어 기호](/docs/services/text-to-speech?topic=text-to-speech-usSymbols)
