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

# 사용자 정의 이해
{: #customIntro}

텍스트를 {{site.data.keyword.texttospeechfull}}로 합성하는 경우 서비스는 언어 종속 발음 규칙을 적용합니다. 서비스는 규칙을 적용하여 각 단어의 일반 철자(철자법을 준수함)를 음성 철자로 변환합니다. 단어의 발음 철자는 발음 기호를 사용하여 단어가 발음되는 방식을 정의합니다. 이 기호는 언어에서 단어를 구분하는 소리의 개별 단위, 음절 간 경계 및 음절의 강세 표시입니다.
{: shortdesc}

서비스의 일반 발음 규칙은 일반적인 단어에 적합합니다. 그러나 특이한 단어에 대해서는 불완전한 결과가 발생될 수 있습니다. 이러한 단어에는 외국어의 어원, 개인 또는 지리 이름 및 약어 또는 두문자어를 비롯한 특수 용어가 포함됩니다. 애플리케이션의 용어집에 이러한 단어가 포함된 경우 사용자 정의 인터페이스를 사용하여 서비스에서 해당 단어를 발음하는 방식을 지정할 수 있습니다.

사용자 정의 인터페이스는 모든 언어로 사용할 수 있는 베타 기능입니다. 음성 모델 사용자 정의를 사용하려면 표준 가격 플랜이 있어야 합니다. Lite 플랜의 사용자는 사용자 정의 인터페이스를 사용할 수 없습니다. 자세한 정보는 {{site.data.keyword.texttospeechshort}} 서비스의 [가격 페이지](https://www.ibm.com/cloud/watson-text-to-speech/pricing){: external}를 참조하십시오.
{: note}

## 사용자 정의 작동 방식
{: #ciHow}

{{site.data.keyword.texttospeechshort}} 서비스의 사용자 정의 인터페이스는 특정 언어를 위한 단어 및 변환의 사전을 작성합니다. 이 사전은 *사용자 정의 음성 모델*(또는 사용자 정의 모델)이라고 합니다. 사용자 정의 음성 모델의 각 사용자 정의 항목은 *단어*/*변환* 쌍으로 구성됩니다. 단어의 변환은 단어가 입력 텍스트에 표시될 때 발음하는 방법을 서비스에게 알려줍니다.

사용자 정의 인터페이스는 서비스가 영구적으로 저장하는 사용자 정의 음성 모델을 작성하고 관리할 수 있는 메소드를 제공합니다. 사용자 정의 모델을 작성한 후 모든 버전의 `/v1/synthesize` 메소드를 통해 합성 중에 이 모델을 사용할 수 있습니다. 서비스가 입력 텍스트를 합성하는 경우 변환을 직접적으로 또는 간접적으로 적용하여 사용자 정의 모델에 표시되는 단어의 발음을 판별합니다. 특정 언어의 사용자 정의 음성 모델을 작성하므로 사용자 정의 모델은 해당 언어로 사용 가능한 모든 음성(표준 또는 신경)으로 사용할 수 있습니다.

*유사 발음 변환* 또는 *음성 변환*으로 사용자 정의 음성 모델의 단어에 대한 변환을 지정합니다. 동일한 사용자 정의 모델의 항목에 두 메소드를 모두 사용할 수 있고 동일한 변환 내에서 두 가지 메소드를 결합할 수 있습니다. 여러 규칙 및 지시사항이 사용자 정의 항목에 적용됩니다. 자세한 정보는 [사용자 정의 항목의 작성 규칙](/docs/services/text-to-speech?topic=text-to-speech-rules)을 참조하십시오.

## 유사 발음 변환
{: #soundsLike}

*유사 발음 변환*은 서비스의 일반 발음 규칙을 사용하여 대상 단어의 발음을 간접적으로 표시합니다. 유사 발음 변환은 하나 이상의 기타 단어의 일반 발음으로 형성됩니다. 서비스는 먼저 입력 텍스트에 표시되는 단어에 대해 지정된 변환을 대체합니다. 그런 다음 발음을 가져오기 위해 변환을 음성 표현으로 변환하여 일반 발음 규칙을 변환에 적용합니다.

예를 들어, 서비스의 일반 발음 규칙으로 다수의 일반 약어 및 두문자어가 적절하게 변환됩니다. 서비스는 *cm* 약어를 *centimeter*로 발음합니다. 덜 일반적인 약어는 한 자씩 발음합니다. 예를 들어, 서비스는 *Str*(*street*의 약어) 문자열을 한 자씩 발음하여 *S T R*로 발음합니다. 유사 발음 메소드를 사용하여 *Str* 문자열에 대해 *street* 변환을 지정할 수 있습니다.

약어의 다른 예로 Institute of Electrical and Electronic Engineers를 의미하는 *IEEE*를 들 수 있습니다. 기본적으로 서비스는 이 약어를 *I E E E*로 발음합니다. 그러나 두문자어는 일반적으로 *I triple E*로 발음되며, 단순 유사 발음 변환인 *I triple E*를 사용하여 쉽게 정의할 수 있습니다. *IEEE* 단어가 이 변환을 사용하여 사용자 정의 모델에 표시되는 경우 서비스는 각 단어를 변환으로 대체합니다. 그런 다음 일반 발음 규칙을 개별 단어인 *I*, *triple* 및 *E*에 적용하여 일반적인 발음을 생성합니다.

유사 발음 메소드를 약어 및 두문자어 외의 항목에도 적용할 수 있습니다. 복잡하거나 특이한 단어의 경우에도 해당됩니다. 예를 들어, 다음과 같은 유사 발음 변환 쌍은 서비스의 일반 발음 규칙으로 불완전하게 처리되는 특이한 단어에 대한 올바른 발음을 생성합니다. 이러한 단어에 대한 적절한 변환을 찾는 것은 단순 약어를 찾는 것보다 어려울 수 있습니다. 다음 변환에서는 단어의 철자를 변경하도록 일반 발음 규칙을 사용합니다.

<table style="width:35%">
  <caption>표 1. 유사 발음 변환 예</caption>
  <tr>
    <th style="text-align:left">단어</th>
    <th style="text-align:left">변환</th>
  </tr>
  <tr>
    <td>ayurvedic</td>
    <td>aayervedic</td>
  </tr>
  <tr>
    <td>gastroenteritis</td>
    <td>gastro enteritis</td>
  </tr>
</table>

이 예에서와 같이 유사 발음 변환이 개발됨에 따라 정형화된 변환보다 더 많은 시행착오가 발생할 수 있습니다. 서비스를 사용하여 얻은 직관 및 경험을 기반으로 후보 변환을 작성합니다. 그런 다음 입력 텍스트로 후보 변환의 대상이 될 단어를 합성하고 생성되는 오디오를 청취합니다. 발음에 만족하는 경우 사용자 정의 모델에서 변환을 사용할 수 있습니다. 만족하지 않으면 변환을 수정하고 다시 테스트하십시오.

## 음성 변환
{: #phonetic}

유사 발음 메소드는 발음하기 위한 비교적 단순하고 유용한 방법입니다. 그러나 항상 유사 발음 변환을 개발할 수 있는 것은 아닙니다. 직접적인 대안인 음성 메소드는 더욱 복잡하고 시간이 걸릴 수 있으나 어떠한 단어도 발음할 수 있습니다.

*음성 변환*은 서비스의 일반 발음 규칙을 대체하는 발음 기호, 음절 강세 표시 및 음절 경계(선택사항)를 지정합니다. 다음 형식 중 하나로 음성 변환을 지정합니다.

-   표준 IPA(International Phonetic Alphabet) 표시
-   자체 {{site.data.keyword.IBM_notm}} Symbolic Phonetic Representation(SPR)

두 경우 모두 SSML(Speech Synthesis Markup Language)을 기반으로 한 특정 음소 형식을 사용하여 변환을 지정합니다. SSML은 음성 합성 애플리케이션을 위해 텍스트의 어노테이션을 제공하는 XML 기반 마크업 언어입니다. 다음과 같은 SSML `<phoneme>` 요소를 사용하여 단어의 음성 변환을 지정합니다.

<pre><code>&lt;phoneme alphabet="{ipa | ibm}" ph="{translation}"&gt;&lt;/phoneme&gt;</code></pre>

`alphabet` 속성은 `ipa` 또는 `ibm`의 음성 표시 유형을 지정합니다. `ph` 속성은 음성 변환 문자열을 지정합니다.

예를 들어, `trinitroglycerin` 단어를 고려해보십시오. 서비스의 일반 발음 규칙은 화학자 및 의사들이 공통으로 사용하는 발음과는 다른 발음을 생성합니다. 올바른 발음은 음성 변환으로 구현될 수 있습니다.

<table style="width:35%">
  <caption>표 2. 음성 변환 예</caption>
  <tr>
    <th style="text-align:left">알파벳</th>
    <th style="text-align:left">변환</th>
  </tr>
  <tr>
    <td>IPA</td>
    <td>t&#633;a&#618;n&#712;a&#618;t&#633;&#601;gl&#618;s&#601;&#633;&#616;n</td>
  </tr>
  <tr>
    <td>SPR</td>
    <td>trYn1YtrxglIsxrXn</td>
  </tr>
</table>

이 예에서 음성 변환 문자열은 발음 기호 및 하나의 기본 강세 표시로 구성됩니다. 기본 강세 표시는 <code>&#712;</code>(IPA) 및 `1`(SPR)로 표시됩니다. 두 경우 모두 강세 모음의 기호 바로 앞에 위치합니다. 예에서는 표시되지 않지만 음성 변환에서 음절 경계 및 보조 강세 위치를 지정할 수도 있습니다. 이 요소는 필수가 아니며 일반적으로 발음하는 데 필요하지 않습니다. 유사 발음 변환과 같이 공백으로 구분되는 여러 문자열에서 음성 변환을 구성할 수 있습니다.

IPA 유니코드 값으로 IPA 변환을 지정할 수도 있습니다. 자세한 정보는 [IBM SPR 사용](/docs/services/text-to-speech?topic=text-to-speech-sprs) 및 언어별 테이블([지원되는 언어](/docs/services/text-to-speech?topic=text-to-speech-sprs#supportedLanguages)에서 언급되는 페이지에 있음)을 참조하십시오. IPA 유니코드 값을 사용하는 변환의 예는 [발음 요소](/docs/services/text-to-speech?topic=text-to-speech-elements#phoneme_element)를 참조하십시오.
{: note}

### 기존 음성 변환 관련 작업
{: #phoneticMethod}

음운론의 전문가가 아닌 경우 음성 변환 구성은 쉬운 작업이 아닙니다. 처음부터 음성 변환을 구성하는 것보다 기존 음성 변환을 편집하는 것이 훨씬 더 쉽습니다. 음성 변환 작성에 도움이 되도록 서비스의 API에는 `GET /v1/pronunciation` 메소드가 포함됩니다. 이 메소드는 지정된 언어로 된 단어에 대한 서비스의 일반 발음 규칙으로 생성되는 IPA 또는 SPR 표시를 리턴합니다. 해당 모델의 언어로 된 변환을 확인하려면 지정된 사용자 정의 음성 모델에서 단어의 발음을 요청할 수도 있습니다.

`/GET v/1/pronunciation` 메소드를 사용하여 단어의 초기 음성 변환을 가져올 수 있습니다. 그런 다음 원하는 대로 발음할 수 있도록 변환을 수정할 수 있습니다. 유사 발음 메소드와 같이 시행착오 프로세스를 따릅니다. 후보 변환을 서비스에 제출하고, 입력 텍스트로 단어를 합성하고, 생성되는 오디오를 청취하고, 후보 변환을 편집합니다. 발음에 만족할 때까지 프로세스를 반복할 수 있습니다.

자세한 정보는 [언어에서 단어 조회](/docs/services/text-to-speech?topic=text-to-speech-customWords#cuWordsQueryLanguage)를 참조하십시오.

### 음성 변환에 대한 자세한 정보
{: #phoneticInfo}

다음 리소스는 음성 변환에 대한 정보를 제공합니다.

-   SSML 및 `<phoneme>` 요소 사용에 대한 자세한 정보는 [SSML 사용](/docs/services/text-to-speech?topic=text-to-speech-ssml)을 참조하십시오.
-   SPR 변환 및 동등한 IPA 기호 지정에 대한 자세한 정보는 [IBM SPR 사용](/docs/services/text-to-speech?topic=text-to-speech-sprs)을 참조하십시오.
-   IPA 기호 사용에 대한 자세한 정보 및 기호의 오디오 샘플은 웹에 있는 소스를 참조하십시오. [International Phonetic Alphabet](https://wikipedia.org/wiki/International_Phonetic_Alphabet){: external}에서 자세한 소개 내용을 찾을 수 있습니다.

## 유사 발음 및 음성 변환의 결합

동일한 변환에서 유사 발음 및 음성 메소드를 결합할 수 있습니다. 이 기능으로 변환 구성과 관련된 작업이 줄어들 수 있습니다.

예를 들어, 만족스러운 수준으로 발음된 단어를 제거하는 데 유사 발음 메소드를 사용했다고 가정합니다. 그러나 단어의 나머지 요소를 세부적으로 조정해야 합니다. 음성 메소드를 사용하여 단어의 어려운 측면을 지정할 수 있습니다. 다음 예에서는 `trinitroglycerin` 단어의 결합된 변환이 적용되었습니다.

<pre><code>try&lt;phoneme alphabet="ipa" ph="n&#712;a&#618;t&#633;&#601;gl&#618;s&#601;&#633;&#616;n"&gt;&lt;/phoneme&gt;</code></pre>
