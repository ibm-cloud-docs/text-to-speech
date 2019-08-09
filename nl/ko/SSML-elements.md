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

# SSML 요소
{: #elements}

{{site.data.keyword.texttospeechfull}} 서비스를 통해 대부분의 SSML(Speech Synthesis Markup Language) 요소를 사용하여 텍스트의 합성을 제어할 수 있습니다. 요소는 지원되는 모든 언어에 사용할 수 있습니다. 다음 표에서는 SSML 요소 및 속성에 대한 서비스의 지원을 요약합니다.

-   *전체*는 서비스가 HTTP 및 WebSocket 인터페이스를 사용하여 요소 또는 속성을 완전히 지원함을 의미합니다.
-   *부분*은 서비스가 요소 또는 속성의 모든 측면을 지원하지 않음을 의미합니다. 또한 서비스가 하나의 인터페이스만 사용하여 요소 또는 속성을 지원하거나 모든 음성에 요소 또는 속성이 지원되지 않음을 의미합니다.
-   *없음*은 서비스가 요소 또는 속성을 지원하지 않음을 의미합니다.

요소 또는 속성에 대한 자세한 정보는 해당 설명을 참조하십시오. 이 설명에 따르면 일부 속성 및 값은 SSML 스펙과는 약간 다릅니다. 자세한 정보는 [W3C SSML(Speech Synthesis Markup Language) 버전 1.0](http://www.w3.org/TR/speech-synthesis/){: external}을 참조하십시오.

<table>
  <caption>표 1. SSML 요소</caption>
  <tr>
    <th style="text-align:left; width:30%">요소 또는 속성</th>
    <th style="text-align:center; width:12%">지원</th>
    <th style="text-align:left; width:46%; padding-left:75px">요소 또는 속성</th>
    <th style="text-align:center; width:12%">지원</th>
  </tr>
  <tr>
    <td>[Audio](#audio_element)</td>
    <td style="text-align:center">없음</td>
    <td style="padding-left:75px">[Say-as](#say-as_element)</td>
    <td style="text-align:center">부분</td>
  </tr>
  <tr>
    <td>[Break](#break_element)</td>
    <td style="text-align:center">전체</td>
    <td style="padding-left:100px">[cardinal](#sayAsCardinal)</td>
    <td style="text-align:center">부분</td>
  </tr>
  <tr>
    <td>[Desc](#desc_element)</td>
    <td style="text-align:center">없음</td>
    <td style="padding-left:100px">[date](#sayAsDate)</td>
    <td style="text-align:center">부분</td>
  </tr>
  <tr>
    <td>[Emphasis](#emphasis_element)</td>
    <td style="text-align:center">없음</td>
    <td style="padding-left:100px">[digits](#sayAsDigits)</td>
    <td style="text-align:center">부분</td>
  </tr>
  <tr>
    <td>[Lexicon](#lexicon_element)</td>
    <td style="text-align:center">없음</td>
    <td style="padding-left:100px">[letters](#sayAsLetters)</td>
    <td style="text-align:center">부분</td>
  </tr>
  <tr>
    <td>[Mark](#mark_element)</td>
    <td style="text-align:center">부분</td>
    <td style="padding-left:100px">[number](#sayAsNumber)</td>
    <td style="text-align:center">부분</td>
  </tr>
  <tr>
    <td>[Meta](#mm_element)</td>
    <td style="text-align:center">없음</td>
    <td style="padding-left:125px">cardinal</td>
    <td style="text-align:center">부분</td>
  </tr>
  <tr>
    <td>[Metadata](#mm_element)</td>
    <td style="text-align:center">없음</td>
    <td style="padding-left:125px">ordinal</td>
    <td style="text-align:center">부분</td>
  </tr>
  <tr>
    <td>[Paragraph](#ps_element)</td>
    <td style="text-align:center">전체</td>
    <td style="padding-left:125px">telephone</td>
    <td style="text-align:center">부분</td>
  </tr>
  <tr>
    <td>[Phoneme](#phoneme_element)</td>
    <td style="text-align:center">전체</td>
    <td style="padding-left:150px">punctuation</td>
    <td style="text-align:center">부분</td>
  </tr>
  <tr>
    <td style="padding-left:25px">IBM SPR</td>
    <td style="text-align:center">전체</td>
    <td style="padding-left:100px">[ordinal](#sayAsOrdinal)</td>
    <td style="text-align:center">부분</td>
  </tr>
  <tr>
    <td style="padding-left:25px">IPA</td>
    <td style="text-align:center">전체</td>
    <td style="padding-left:100px">[vxml:boolean](#vxml-boolean)</td>
    <td style="text-align:center">부분</td>
  </tr>
  <tr>
    <td>[Prosody](#prosody_element)</td>
    <td style="text-align:center">부분</td>
    <td style="padding-left:100px">[vxml:currency](#vxml-currency)</td>
    <td style="text-align:center">부분</td>
  </tr>
  <tr>
    <td style="padding-left:25px">contour</td>
    <td style="text-align:center">없음</td>
    <td style="padding-left:100px">[vxml:date](#vxml-date)</td>
    <td style="text-align:center">부분</td>
  </tr>
  <tr>
    <td style="padding-left:25px">duration</td>
    <td style="text-align:center">없음</td>
    <td style="padding-left:100px">[vxml:digits](#vxml-digits)</td>
    <td style="text-align:center">부분</td>
  </tr>
  <tr>
    <td style="padding-left:25px">[pitch](#prosody-pitch)</td>
    <td style="text-align:center">전체</td>
    <td style="padding-left:100px">[vxml:phone](#vxml-phone)</td>
    <td style="text-align:center">부분</td>
  </tr>
  <tr>
    <td style="padding-left:25px">range</td>
    <td style="text-align:center">없음</td>
    <td style="padding-left:75px">[Sentence](#ps_element)</td>
    <td style="text-align:center">전체</td>
  </tr>
  <tr>
    <td style="padding-left:25px">[rate](#prosody-rate)</td>
    <td style="text-align:center">전체</td>
    <td style="padding-left:75px">[Speak](#speak_element)</td>
    <td style="text-align:center">전체</td>
  </tr>
  <tr>
    <td style="padding-left:25px">[volume](#prosody-volume)</td>
    <td style="text-align:center">부분</td>
    <td style="padding-left:75px">[Sub](#sub_element)</td>
    <td style="text-align:center">전체</td>
  </tr>
  <tr>
    <td></td>
    <td></td>
    <td style="padding-left:75px">[Voice](#voice_element)</td>
    <td style="text-align:center">없음</td>
  </tr>
</table>

## audio 요소
{: #audio_element}

이 `<audio>` 요소는 기록된 요소를 서비스 생성 오디오에 삽입합니다. 이는 지원되지 않습니다.

## break 요소
{: #break_element}

`<break>` 요소는 일시정지를 음성화된 텍스트에 삽입합니다. 여기에는 다음과 같은 선택적인 속성이 있습니다.

-   `strength`는 다양한 수준 값으로 일시정지의 시간을 지정합니다.
    -   `none` 처리 중에 생성될 수 있는 중단을 억제합니다.
    -   `x-weak`, `weak`, `medium`, `strong` 또는 `x-strong`은 더욱 강력한 중단을 삽입합니다.
-   `time`은 초 또는 밀리초로 일시중단의 시간을 지정합니다. 올바른 값 형식은 `{integer}s`(초) 또는 `{integer}ms`(밀리초)입니다.

```xml
<speak version="1.0">
  Different sized <break strength="none">no pause</break>
  Different sized <break strength="x-weak">x-weak pause</break>
  Different sized <break strength="weak">weak pause</break>
  Different sized <break strength="medium">medium pause</break>
  Different sized <break strength="strong">strong pause</break>
  Different sized <break strength="x-strong">x-strong pause</break>
  Different sized <break time="1s">one-second pause</break>
  Different sized <break time="1500ms">1500-millisecond pause</break>
</speak>
```
{: codeblock}

## desc 요소
{: #desc_element}

`<desc>` 요소는 `<audio>` 요소 내에서만 발생할 수 있습니다. `<audio>` 요소가 지원되지 않으므로 `<desc>` 요소도 지원되지 않습니다.

## emphasis 요소
{: #emphasis_element}

`<emphasis>` 요소는 포함된 텍스트가 강조되어 음성화되도록 요청합니다. 이는 지원되지 않습니다.

## lexicon 요소
{: #lexicon_element}

이 `<lexicon>` 요소에는 제공된 SSML 문서에 필요한 발음 사전이 도입됩니다. 이는 지원되지 않습니다.

서비스의 사용자 정의 인터페이스를 사용하여 음성 합성 중에 사용할 사용자 정의 항목(단어/변환 쌍)의 사전을 정의할 수 있습니다. 자세한 정보는 [사용자 정의 이해](/docs/services/text-to-speech?topic=text-to-speech-customIntro)를 참조하십시오.

## mark 요소
{: #mark_element}

`<mark>` 요소는 서비스의 WebSocket 인터페이스에서만 지원되며, 요소를 무시하는 HTTP 인터페이스에서는 지원되지 않습니다. 자세한 정보는 [SSML 표시 지정](/docs/services/text-to-speech?topic=text-to-speech-timing#mark)을 참조하십시오.
{: note}

`<mark>` 요소는 마커를 합성될 텍스트에 배치하는 비어 있는 요소입니다. `<mark>` 요소 앞에 오는 모든 텍스트가 합성되면 클라이언트에게 알립니다. 요소는 고유하게 마크를 식별하는 문자열을 지정하는 단일 `name` 속성을 허용하며, 이름은 영문자로 시작되어야 합니다. 이름은 표시가 합성된 오디오에서 발생하는 시간과 함께 리턴됩니다.

```xml
<speak version="1.0">
  Hello <mark name="here"/> world.
</speak>
```
{: codeblock}

## meta 및 metadata 요소
{: #mm_element}

`<meta>` 및 `<metadata>` 요소는 문서에 대한 정보를 보관할 수 있는 컨테이너입니다. 이는 지원되지 않습니다.

## paragraph 및 sentence 요소
{: #ps_element}

`<paragraph>`(또는 `<p>`) 및 `<sentence>`(또는 `<s>`) 요소는 텍스트 구조에 대한 힌트를 제공하는 데 사용될 수 있는 선택적인 요소입니다. `<paragraph>` 또는 `<sentence>` 요소 내에 있는 텍스트가 문장 끝의 구분 문자(예: 마침표)로 끝나지 않는 경우 서비스는 합성된 오디오에 평소보다 더 긴 일시정지를 추가합니다.

요소 중 하나에 대한 유일한 유효 속성은 `xml:lang`이며, 언어를 변경하는 데 사용할 수 있습니다. 속성은 지원되지 않습니다.

```xml
<speak version="1.0">
  <paragraph>
    <sentence>Text within a sentence element.</sentence>
    <s>More text in another sentence.</s>
  </paragraph>
</speak>
```
{: codeblock}

## phoneme 요소
{: #phoneme_element}

`<phoneme>` 요소는 포함된 텍스트에 대한 음성 발음을 제공합니다. 음성 철자는 단어의 소리, 소리가 음절로 구분되는 방식 및 강세가 표시되는 음절을 나타냅니다. 요소에는 두 가지 속성이 있습니다.

-   `alphabet`은 사용될 음운 체계를 지정하는 선택적인 속성입니다. 지원되는 알파벳은 다음과 같습니다.
    -   표준 IPA(International Phonetic Alphabet): `alphabet="ipa"`
    -   {{site.data.keyword.IBM_notm}} Symbolic Phonetic Representation(SPR): `alphabet="ibm"`

    알파벳이 지정되지 않으면 서비스는 기본적으로 IBM SPR을 사용합니다.
-   `ph`는 표시된 알파벳으로 발음을 제공하는 필수 속성입니다. 다음 예에서는 두 가지 형식으로 *tomato* 단어의 발음을 보여줍니다.

    -   IPA 형식:

        <pre><code>&lt;speak version="1.0"&gt;
          &lt;phoneme alphabet="ipa" ph="t&#601;&#712;me&#618;.&#638;o&#650;"&gt;tomato&lt;/phoneme&gt;
        &lt;/speak&gt;</code></pre>

    -   유니코드 기호가 포함된 IPA 형식:

        <pre><code>&lt;speak version="1.0"&gt;
          &lt;phoneme alphabet="ipa" ph="t&amp;&#35;x259;mei&amp;&#35;x027E;o&amp;&#035;x028A;"&gt;tomato&lt;/phoneme&gt;
        &lt;/speak&gt;</code></pre>

    -   IBM SPR 형식:

        <pre><code>&lt;speak version="1.0"&gt;
          &lt;phoneme alphabet="ibm" ph=".0tx.1me.0Fo"&gt;tomato&lt;/phoneme&gt;
        &lt;/speak&gt;</code></pre>

`<phoneme>` 요소가 포함된 SPR 및 IPA 표기법 사용에 대한 자세한 정보는 [IBM SPR 사용](/docs/services/text-to-speech?topic=text-to-speech-sprs)을 참조하십시오.

## prosody 요소
{: #prosody_element}

`<prosody>` 요소는 음역, 말하기 속도 및 텍스트의 볼륨을 제어합니다. 모든 속성은 선택사항이지만 속성이 지정되지 않으면 오류가 발생합니다. SSML 스펙은 서비스에서 지원하지 않는 세 가지 속성 즉, `contour`, `range` 및 `duration`에 사용할 수 있습니다. 서비스는 `pitch`, `rate` 및 `volume` 속성을 지원합니다.

### pitch 속성
{: #prosody-pitch}

`pitch` 속성은 요소 내 텍스트의 기준선 음역을 수정합니다. 허용되는 값은 다음과 같습니다.

-   `Hz`(헤르츠) 지정 앞에 오는 숫자: 기본선 음역은 지정된 값으로 변환됩니다(위 또는 아래로).
-   상대적인 변경 값(반음): 현재 기준선에서 절대 이동의 원인이 되는 숫자입니다. 숫자는 `+`(증가) 또는 `-`(감소) 뒤에 오고 `st`(반음) 앞에 옵니다(예: `+5st`).
-   상대적인 변경 값(백분율): 현재 기준선에서 상대 이동의 원인이 되는 숫자입니다. 숫자는 `+`(증가) 또는 `-`(감소) 뒤에 오고 `%`(백분율 기호) 앞에 옵니다(예: `-10%`).
-   해당 사전 정의된 값으로 음역을 수정하는 다음 여섯 개의 키워드 중 하나가 사용됩니다.
    -   `default`: 서비스의 기본 기준선 음역을 사용합니다.
    -   `x-low`: 12 반음까지 음역 기준선을 하향 이동합니다.
    -   `low`: 6 반음까지 음역 기준선을 하향 이동합니다.
    -   `medium`: `default`과 동일한 동작이 발생합니다.
    -   `high`: 6 반음까지 음역 기준선을 상향 이동합니다.
    -   `x-high`: 12 반음까지 음역 기준선을 상향 이동합니다.

    ```xml
    <speak version="1.0">
      <prosody pitch="150Hz">Transpose pitch to 150 Hz</prosody>
      <prosody pitch="-20Hz">Lower pitch by 20 Hz from baseline</prosody>
      <prosody pitch="+20Hz">Increase pitch by 20 Hz from baseline</prosody>
      <prosody pitch="-12st">Lower pitch by 12 semitones from baseline</prosody>
      <prosody pitch="+12st">Increase pitch by 12 semitones from baseline</prosody>
      <prosody pitch="x-low">Lower pitch by 12 semitones from baseline</prosody>
    </speak>
    ```
    {: codeblock}

### rate 속성
{: #prosody-rate}

`rate` 속성은 요소 내 텍스트에 대한 말하기 속도의 변경사항을 표시합니다. 속도는 분당 단어의 수로 지정됩니다. 말하기 속도가 분당 50개의 단어인 경우 `rate`는 `50`입니다. `rate`가 양수로 설정되면 구현 시 현재 W3C 운율 속도 속성 스펙을 준수하지 않습니다. 또한 서비스가 상대 백분율 변경(예: `+15%`)은 지원하지만 상대 값 변경(예: `+15`)은 지원하지 않습니다. 허용되는 값은 다음과 같습니다.

-   상대 백분율 증가 또는 감소: `+10%`.
-   분당 단어 수(양수): `75`
-   `default`: 서비스의 기본 속도를 사용합니다.
-   `x-slow`: 속도가 50%까지 감소합니다.
-   `slow`: 속도가 25%까지 감소합니다.
-   `medium`: `default`과 동일한 동작이 발생합니다.
-   `fast`: 속도가 25%까지 증가합니다.
-   `x-fast`: 속도가 50%까지 증가합니다.

```xml
<speak version="1.0">
  <prosody rate="slow">Decrease speaking rate by 25%</prosody>
  <prosody rate="50">Set speaking rate at 50 words per minute</prosody>
  <prosody rate="+5%">Increase speaking rate by 5 percent</prosody>
</speak>
```
{: codeblock}

### volume 속성
{: #prosody-volume}

서비스는 신경 음성(예: `en-US_AllisonV3Voice`)이 사용된 `<prosody>` 요소의 `volume` 속성을 지원하지 않습니다. 자세한 정보는 [신경 음성](/docs/services/text-to-speech?topic=text-to-speech-voices#neuralVoices)을 참조하십시오.
{: note}

`volume` 속성은 요소 내 텍스트의 볼륨을 수정합니다. 1.0 - 100.0(최대 볼륨)의 범위로 정수 또는 10진수 값을 지정할 수 있습니다. 0 - 100의 범위로 사전 정의된 설정과 일치하는 다음 문자열 값 중 하나를 사용할 수도 있습니다. (`silent` 값은 지원되지 않습니다.)

-   `x-soft`의 값은 30입니다.
-   `soft`의 값은 50입니다.
-   `medium`의 값은 값은 80입니다.
-   `loud`의 값은 90입니다.
-   `default`의 값은 92입니다.
-   `x-loud`의 값은 100입니다.

```xml
<speak version="1.0">
  <prosody volume="75">Modified volume is 75</prosody>
  <prosody volume="88.9">Modified volume is 88.9</prosody>
  <prosody volume="loud">Modified volume is 90</prosody>
</speak>
```
{: codeblock}

## say-as 요소
{: #say-as_element}

`<say-as>` 요소는 대부분의 언어에서 부분적으로만 지원됩니다. 미국 영어 이외의 언어의 경우 서비스는 일반적으로 요소의 `digits` 및 `letters` 속성만 지원합니다.
{: note}

`<say-as>` 요소는 요소 내에 포함된 텍스트 유형에 대한 정보를 제공하고 텍스트 렌더링을 위한 세부사항 레벨을 지정합니다. 요소에는 하나의 필수 속성인 `interpret-as`가 있습니다. 이 속성은 포함된 텍스트가 해석되는 방식을 표시합니다. 다음 예에서 설명된 대로 `interpret-as` 속성 내의 특정 값에만 사용되는 두 가지 선택적인 속성 즉, `format` 및 `detail`이 있습니다.

`interpret-as` 속성에 허용 가능한 값 및 각각의 예가 표시됩니다.

### cardinal
{: #sayAsCardinal}

`cardinal` 값은 요소 내의 기수를 나타냅니다. 다음 예는 *Super Bowl forty-nine*을 발음합니다. 첫 번째는 서비스의 기본 동작을 변경하지 않으므로 필요하지 않습니다.

```xml
<speak version="1.0">
  Super Bowl <say-as interpret-as="cardinal">49</say-as>
  Super Bowl <say-as interpret-as="cardinal">XLIX</say-as>
</speak>
```
{: codeblock}

### date
{: #sayAsDate}

`date` 값은 연관된 `format` 속성에 지정된 형식에 따라 요소 내의 날짜를 나타냅니다. `format` 속성은 `date` 값에 필요합니다. `format`이 없으면 서비스는 계속해서 날짜의 발음을 시도합니다. 다음 예는 지정된 형식으로 표시된 날짜를 나타냅니다. 여기서, `d`, `m` 및 `y`는 일, 월, 년입니다.

```xml
<speak version="1.0">
  <say-as interpret-as="date" format="mdy">12/17/2005</say-as>
  <say-as interpret-as="date" format="ymd">2005/12/17</say-as>
  <say-as interpret-as="date" format="dmy">17/12/2005</say-as>
  <say-as interpret-as="date" format="ydm">2005/17/12</say-as>
  <say-as interpret-as="date" format="my">12/2005</say-as>
  <say-as interpret-as="date" format="md">12/17</say-as>
  <say-as interpret-as="date" format="ym">2005/12</say-as>
</speak>
```
{: codeblock}

### digits
{: #sayAsDigits}

`digits` 값이 요소 내의 자릿수를 나타냅니다. 다음 예는 *123456*의 개별 자릿수를 나타냅니다.

```xml
<speak version="1.0">
  <say-as interpret-as="digits">123456</say-as>
</speak>
```
{: codeblock}

### letters
{: #sayAsLetters}

`letters` 값은 요소 내에서 단어의 철자를 표시합니다. 다음 예에서는 *hello*라는 단어의 철자를 음성으로 표시합니다.

```xml
<speak version="1.0">
  <say-as interpret-as="letters">Hello</say-as>
</speak>
```
{: codeblock}

### number
{: #sayAsNumber}

`number` 값은 `cardinal` 및 `ordinal` 값에 대한 대체 항목을 제공합니다. 선택적인 `format` 속성을 사용하여 일련의 숫자가 해석되는 방식을 표시할 수 있습니다. 첫 번째 예에서는 기수 값으로 숫자를 발음하기 위해 `format` 속성을 생략합니다. 두 번째 예에서는 숫자가 `cardinal` 값으로 발음되도록 명시적으로 지정합니다. 세 번째 예에서는 숫자가 `ordinal` 값으로 발음되도록 지정합니다.

```xml
<speak version="1.0">
  <say-as interpret-as="number">123456</say-as>
  <say-as interpret-as="number" format="cardinal">123456</say-as>
  <say-as interpret-as="number" format="ordinal">123456</say-as>
</speak>
```
{: codeblock}

`format` 속성에 `telephone` 값도 지정할 수 있습니다. 이 예에서는 일련의 숫자를 전화 번호로 발음하는 두 가지 방식을 보여줍니다. 구두점을 포함하여 숫자를 발음하려면 선택적인 `detail` 속성에 `punctuation` 값을 지정하십시오.

```xml
<speak version="1.0">
  <say-as interpret-as="number" format="telephone">555-555-5555</say-as>
  <say-as interpret-as="number" format="telephone" detail="punctuation">555-555-5555</say-as>
</speak>
```
{: codeblock}

### ordinal
{: #sayAsOrdinal}

`ordinal` 값은 요소 내의 자릿수에 대한 서수 값입니다. 다음 예에서는 *second first*라고 발음합니다.

```xml
<speak version="1.0">
  <say-as interpret-as="ordinal">2</say-as>
  <say-as interpret-as="ordinal">1</say-as>
</speak>
```
{: codeblock}

### vxml:boolean
{: #vxml-boolean}

`vxml:boolean` 값은 요소 내의 `true` 또는 `false` 값에 따라 *yes* 또는 *no*를 나타냅니다.

```xml
<speak version="1.0">
  <say-as interpret-as="vxml:boolean">true</say-as>
  <say-as interpret-as="vxml:boolean">false</say-as>
</speak>
```
{: codeblock}

### vxml:currency
{: #vxml-currency}

`vxml:currency` 값은 화폐 가치의 합성을 제어하는 데 사용됩니다. 문자열은 `UUUmm.nn` 형식으로 작성되어야 합니다. 여기서, `UUU`는 ISO 표준 4217로 지정된 3자의 통화 지표이며 `mm.nn`은 양입니다. 다음 예에서는 *forty-five dollars and thirty cents*라고 발음합니다.

```xml
<speak version="1.0">
  <say-as interpret-as="vxml:currency">USD45.30</say-as>
</speak>
```
{: codeblock}

지정된 숫자에 소수 셋째 자리 이상이 포함된 경우 금액은 통화 지표 앞에 표시되는 10진수로 합성됩니다. 3자로 된 통화 지표가 표시되지 않으면 금액은 10진수로 합성되지 않으며 통화 유형은 발음되지 않습니다. 다음 예에서는 *forty-five point three two nine US dollars*라고 발음합니다.

```xml
<speak version="1.0">
  <say-as interpret-as="vxml:currency">USD45.329</say-as>
</speak>
```
{: codeblock}

### vxml:date
{: #vxml-date}

`vxml:date` 값은 `date` 값과 같이 표시되지만 형식은 `YYYYMMDD`로 사전 정의됩니다. 일, 월, 년을 알 수 없거나 음성화되길 원하지 않는 경우 값을 `?`(물음표)로 대체하십시오. 두 번째 및 세 번째 예에는 물음표가 포함됩니다.

```xml
<speak version="1.0">
  <say-as interpret-as="vxml:date">20050720</say-as>
  <say-as interpret-as="vxml:date">????0720</say-as>
  <say-as interpret-as="vxml:date">200507??</say-as>
</speak>
```
{: codeblock}

### vxml:digits
{: #vxml-digits}

`vxml:digits` 값은 `digits` 값과 동일한 기능을 제공합니다.

### vxml:phone
{: #vxml-phone}

`vxml:phone` 값은 숫자 및 구두점으로 전화 번호를 나타냅니다. `number` 값을 사용하고, `format` 속성에 `telephone`을 지정하고 `detail` 속성에 `punctuation`을 지정하는 것과 동등합니다.

```xml
<speak version="1.0">
  <say-as interpret-as="vxml:phone">555-555-5555</say-as>
</speak>
```
{: codeblock}

## speak 요소
{: #speak_element}

`<speak>` 요소는 SSML 문서의 루트 요소입니다. 올바른 속성은 다음과 같습니다.

-   `version`은 SSML 스펙을 지정하는 필수 속성입니다. 허용되는 값은 `1.0`입니다.
-   `xml:lang`은 서비스에 필요하지 않습니다. 이 요소 사용 시 속성을 생략하십시오.
-   `xml:base`에는 영향이 없습니다.

```xml
<speak version="1.0">
  The text to be spoken.
</speak>
```
{: codeblock}

## sub 요소
{: #sub_element}

`<sub>` 요소는 `alias` 속성으로 지정되는 텍스트가 음성 합성 시 요소 내에 포함된 텍스트를 대체하는 것을 나타냅니다. `alias` 속성은 요소의 유일한 속성이며 필수 항목입니다.

```xml
<speak version="1.0">
  <sub alias="International Business Machines">IBM</sub>
</speak>
```
{: codeblock}

## voice 요소
{: #voice_element}

이 `<voice>` 요소는 음성으로 변경을 요청합니다. 이는 지원되지 않습니다.
