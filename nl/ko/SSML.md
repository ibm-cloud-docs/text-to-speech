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

# SSML 사용
{: #ssml}

SSML(Speech Synthesis Markup Language)은 음성 합성 애플리케이션을 위해 텍스트의 어노테이션을 제공하는 XML 기반 마크업 언어입니다. 이는 VoiceXML 2.0 스펙으로 음성 합성을 위해 표준 마크업 언어로 채택된 W3C Voice-Browser Working Group의 권장사항입니다. SSML은 개발자가 마크업을 통해 발음, 볼륨, 음역, 속도 및 기타 속성을 지정하도록 하여 합성 프로세스의 측면을 제어하기 위한 표준 방식으로 음성 애플리케이션의 개발자를 제공합니다.
{: shortdesc}

{{site.data.keyword.texttospeechfull}} 서비스를 통해 SSML을 사용하여 지원되는 모든 언어로 텍스트의 합성을 제어할 수 있습니다. 여기에는 IPA(International Phonetic Alphabet) 또는 {{site.data.keyword.IBM_notm}} Symbolic Phonetic Representation(SPR)을 사용하여 단어의 발음을 정의하기 위한 SSML `<phoneme>` 요소 사용이 포함됩니다. 서비스는 사용자 정의 인터페이스로 단어의 음성 변환을 정의하기 위한 SSML `<phoneme>` 요소도 필요로 합니다. 자세한 정보는 [사용자 정의 이해](/docs/services/text-to-speech/custom-intro.html)를 참조하십시오.

## SSML 소개
{: #introduction-SSML}

SSML은 사전 정의된 요소 또는 태그 세트를 사용하여 합성기에 전달되는 일반 텍스트를 기능 보강하여 작동됩니다. XML 구분 분석기는 먼저 마크업 스펙에서 일반 입력 텍스트를 구분합니다. 그런 다음 스펙은 원하는 효과를 위해 합성기를 사용하여 이해할 수 있는 형식으로 작성된 일련의 소개로 처리되고 전송됩니다. XML 구문 분석기가 이 작업을 수행하려면 마크업은 올바르게 구성되어야 합니다. 예를 들어, 요소는 닫히고 여러 요소는 적절하게 중첩되어야 합니다. 기본 XML 개념에 대한 소개는 [w3schools.com/xml/xml_whatis.asp ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](http://www.w3schools.com/xml/xml_whatis.asp){: new_window}를 참조하십시오.

SSML 요소는 여는 태그 및 해당 닫는 태그를 포함하여 내부에 포함되는 모든 항목이 될 수 있습니다. 다음 예에서 표시된 대로 요소에는 기타 요소(태그가 중첩될 수 있음) 및 텍스트의 조합이 포함될 수 있습니다. 또한 요소는 특정 값으로 설정된 속성을 필요로 하거나 선택적으로 허용할 수 있습니다. 

```xml
<tag1>
  <tag2 attributeName="attributeValue">
    ... some text ...
  </tag2>
</tag1>
```
{: codeblock}

전체 법적 SSML 문서는 인코딩과 같은 정보와 SSML 문서를 유효성 검증하기 위한 스키마가 포함되어 있으며 XML 프롤로그(루트 요소 `<speak>` 앞에 위치함)로 구성됩니다. (프롤로그의 구조에 대한 자세한 정보는 [tizag.com/xmlTutorial/xmlprolog.php ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](http://www.tizag.com/xmlTutorial/xmlprolog.php){: new_window}를 참조하십시오.) `<speak>` 요소의 범위 내에서 추가 요소로 합성되고 기능 보강될 텍스트를 지정합니다. 

```xml
<!-- The XML Prolog -->
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE speak PUBLIC "-//W3C//DTD SYNTHESIS 1.0//EN"
  "http://www.w3.org/TR/speech-synthesis/synthesis.dtd">

<!-- Root Element -->
<speak version="1.0" xmlns="www.w3.org/2001/10/synthesis"
  ... the body that contains text to be synthesized plus markup ...
</speak>
```
{: codeblock}

서비스는 전체 XML 헤더를 포함하지 않는 SSML 요소인 SSML 단편을 지원한다.

## SSML 지원
{: #ssmlSupport}

{{site.data.keyword.texttospeechshort}} 서비스는 SSML 버전 1.0의 지원을 기반으로 하며, 이는 2004년 9월 7일에 W3C에서 권장된 사항입니다. W3C SSML 권장사항에 대한 자세한 정보는 [W3C Speech Synthesis Markup Language(SSML) 버전 1.0 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](http://www.w3.org/TR/speech-synthesis/){: new_window}을 참조하십시오.

서비스를 통한 SSM 사용에 대한 자세한 정보는 다음을 참조하십시오. 

-   모든 SSML 요소와 관련된 서비스의 지원 레벨에 대한 전체 정보는 [SSML 요소](/docs/services/text-to-speech/SSML-elements.html)를 참조하십시오. 일부 예외와 함께 서비스는 SSML 단편을 비롯하여 대부분의 W3C 스펙을 구현합니다. 
-   서비스는 음성화될 때 (좋은 소식, 사과 또는 불확실성으로) 텍스트가 표시되는 방식을 나타내는 `<express-as>` 요소로 SSML을 확장합니다. 서비스는 미국 영어의 Allison 음성으로만 표현성을 지원합니다. [표현 SSML 사용](/docs/services/text-to-speech/SSML-expressive.html)을 참조하십시오.
-   서비스는 사용자가 음성의 음역, 음역 범위, 성문 장력, 호흡, 속도 및 음색을 제어하도록 하여 가능한 음성 범위를 확장하는 `<voice-transformation>`을 확장합니다. 서비스는 두 가지 기본 제공 가상 음성인 *Young* 및 *Soft*를 제공합니다. 서비스는 미국 영어 음성으로만 음성 변환을 지원합니다. [음성 변환 SSML 사용](/docs/services/text-to-speech/SSML-transformation.html)을 참조하십시오.
-   서비스의 사용자 정의 인터페이스는 SSML `<phoneme>` 요소의 사용을 지원하여 단어를 발음하는 데 사용하는 음성 철자를 지정합니다. 음성 철자는 단어의 소리, 소리가 음절로 구분되는 방식 및 강세가 표시되는 음절을 나타냅니다. 
    -   사용자 정의 인터페이스에 대한 자세한 정보는 [사용자 정의 사용](/docs/services/text-to-speech/custom-intro.html)을 참조하십시오.
    -   모든 지원되는 언어로 {{site.data.keyword.IBM_notm}} SPR 또는 IPA 스펙에서 사용할 수 있는 유효한 기호에 대한 자세한 정보는 [IBM SPR 사용](/docs/services/text-to-speech/SPRs.html)을 참조하십시오.

## SSML 유효성 검증
{: #errors}

서비스는 합성을 위한 입력 텍스트로 또는 사용자 정의를 위해 단어의 변환의 정의로 모든 컨텐츠에 제출하는 모든 SSML 요소를 유효성 검증합니다. 서비스는 합성을 위해 제출된 텍스트에 SSML 요소가 포함되는지 여부를 미리 판별할 수 없습니다. 그러므로 SSML 포함 여부에 관계 없이 모든 입력 텍스트에 대해 동일한 유효성 검증을 수행합니다. 

-   *모든 SSML 입력이 올바르며 올바르게 구성되어야 합니다.* 서비스는 지원되지 않는 SSML 요소를 자동으로 무시합니다. 서비스는 지원되지 않는 요소 또는 지원되지 않는 기능을 사용하는 요소가 내부에 포함된 텍스트를 합성하며, 요소만 무시됩니다. 
-   *서비스는 올바르지 않은 요소로 인해 HTTP 400 오류 코드를 보고합니다.* 오류 응답에는 설명 메시지가 포함되고 요청이 실패합니다. 

특히 서비스는 다음과 같은 경우 오류를 리턴합니다. 

-   *올바르지 않은 요소.* 예를 들어, 태그를 올바르지 않게 지정하거나, 필수 속성을 생략하거나, 닫는 태그 없이 여는 태그만 포함합니다. 
-   *올바르지 않은 기호.* `<phoneme>` 요소의 `ph` 속성은 지정된 언어로 지원되지 않은 IPA 또는 SPR 기호를 포함합니다. 
-   *모음 없음.* `<phoneme>` 요소의 `ph` 속성은 모음을 포함하지 않은 단어 발음을 지정합니다. 
-   *올바르지 않은 위치의 프랑스어 연음.* `<phoneme>` 요소의 `ph` 속성에서 연음 문자는 자음 뒤에 나오지 않거나 단어 발음의 중간에 표시됩니다.
-   *일본어`:` 기호는 모음 앞에 나오지 않습니다.* `<phoneme>` 요소의 `ph` 속성에서 `:` 문자는 모음 앞에 표시되지 않습니다(음절 경계와 같이 다른 기호와 함께 사이에 표시될 수 있음). 
-   *올바르지 않은 음절 강세.* {{site.data.keyword.IBM_notm}} SPR에서 `<phoneme>` 요소의 `ph` 속성에는 올바르지 않은 음절 강세가 포함됩니다. 프랑스어의 경우, 음절 강세는 바로 모음 앞에 나오지 않습니다. 스페인어 또는 이탈리아어의 경우, 보조(`2`) 또는 강세 없는(`0`) 기호가 사용됩니다. 일본어의 경우, 보조 강세 기호(`2`)가 사용됩니다.
-   *`<express-as>` 또는 `<voice-transformation>` 요소의 SSML에 대한 올바르지 않은 사용.* 지정된 미국 영어 음성으로만 SSML 확장을 사용할 수 있습니다. 
-   *SSML `<prosody>` 요소의 올바르지 않은 사용.* DNN 기반 음성인 `V2`(예: `en-US_AllisonV2Voice`)로 이 요소를 사용할 수 없습니다. 
-   *이스케이프되지 않은 XML 제어 문자.* 입력 텍스트에는 동등한 이스케이프 문자열 또는 문자 인코딩 대신<code>&quot;</code>, <code>&apos;</code>, `&`, `<` 또는 `>` 문자가 자체적으로 포함됩니다. 자세한 정보는 [XML 제어 문자 이스케이프](/docs/services/text-to-speech/http.html#escape)를 참조하십시오.
