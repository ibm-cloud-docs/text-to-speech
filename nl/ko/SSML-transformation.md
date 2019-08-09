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

# 음성 변환 SSML
{: #transformation}

{{site.data.keyword.texttospeechfull}} 서비스는 대부분의 음성 합성 시스템과 같이 제한된 수의 음성만 나타낼 수 있습니다. 또한 일부 언어는 하나 또는 두 가지 음성만 제공합니다. 가능한 음성의 범위를 확장하기 위해 서비스는 `<voice-transformation>` 요소로 SSML을 확장합니다. 기본 음성의 측면을 제어하여 여러 가상 음성을 실현하는 데 이 요소를 사용할 수 있습니다. 애플리케이션 기능에는 다음 항목이 포함됩니다.
{: shortdesc}

-   *음성에 다른 특성 지정.* 일반적으로 또는 특정 애플리케이션에서 음성을 다른 소리로 지정하려고 합니다.
-   *음성 브랜딩.* 고유한 음성을 사용하여 애플리케이션을 구분하려고 합니다.
-   *여러 역할이 있는 애플리케이션.* 여러 명의 개인을 나타내려면 다양한 음성이 필요합니다.

`<voice-transformation>` 요소를 텍스트, 문장 또는 단어나 단편의 전체 본문에 적용할 수 있습니다. 요소는 지정된 텍스트에 적용될 음성 변환의 유형에 대해 설명하는 하나의 필수 속성인 `type`을 허용합니다. 기본 제공 변환을 적용하거나 음성의 여러 측면을 기반으로 한 사용자 정의 변환을 작성할 수 있습니다.

## 언어 지원
{: #languages-transformation}

서비스는 다음과 같은 미국 영어 음성으로만 음성 변환을 지원합니다.

-   `en-US_AllisonVoice`
-   `en-US_LisaVoice`
-   `en-US_MichaelVoice`

음성 변환은 이 음성의 신경 버전(예: `en-US_AllisonV3Voice`)에서는 지원되지 않습니다. 지원되지 않는 음성에 요소를 사용하면 오류가 리턴됩니다.

## 기본 제공 변환
{: #ssml-built-in}

기본 제공 변환은 사전 구성된 변경사항을 음성의 속성에 적용합니다. 기본 제공 변환을 서비스에서 사용할 수 있는 가상 서비스로 간주하십시오. 서비스는 두 가지 기본 제공 변환을 제공합니다. 해당 변환을 사용하기 위해 `type` 속성을 사용하여 기본 제공 변환의 이름(대소문자로 구분됨)을 지정합니다.

-   `Young`은 음성에 좀 더 어린 듯한 소리를 지정합니다.
-   `Soft`는 소리를 좀 더 부드럽게 합니다.

서비스가 변환을 적용하는 범위를 제어하기 위해 둘 중 하나의 기본 제공 음성에 선택적인 `strength` 속성을 적용할 수 있습니다. 값을 서비스가 원래의 음성에 적용하는 결합 요인으로 간주하십시오. 속성에는 0 - 100% 범위의 값이 허용됩니다. `0%`를 지정하면 음성이 변경되지 않고, `100%`를 지정하면 변환의 전체 범위까지 달성할 수 있습니다. 속성을 생략하는 경우 기본 수준은 `100%`입니다.

서비스는 기본 변환을 사용할 때 사용자 정의 변환에 대한 속성을 무시합니다.
{: note}

## 기본 제공 변환 예
{: #ssml-built-in-examples}

다음 예는 두 가지 기본 제공 변환을 다른 수준의 동일 문장에 적용합니다.

```xml
<voice-transformation type="Young" strength="80%">
  Could you provide us with new information?
</voice-transformation>

<voice-transformation type="Soft" strength="60%">
  Could you provide us with new information?
</voice-transformation>
```
{: codeblock}

## 사용자 정의 변환
{: #ssml-custom-transforms}

사용자 정의 변환 속성을 통해 음성 변환의 여러 측면을 더욱 세부적으로 제어할 수 있습니다. 사용자 정의 변환을 사용하려면 `type` 속성에 `Custom`을 지정하십시오. 그러면 하나 이상의 다음 선택적인 속성을 사용하여 변환을 제어할 수 있습니다.

<table>
  <caption>표 1. 사용자 정의 변환 속성</caption>
  <tr>
    <th style="width:15%; text-align:left">속성</th>
    <th style="width:25%; text-align:center">범위</th>
    <th style="text-align:left">설명</th>
  </tr>
  <tr>
    <td><code>pitch</code></td>
    <td style="text-align:center">[-100%, 100%],<br/>
      [<code>x-low</code>, <code>low</code>, <code>default</code>,
      <code>high</code>, <code>x-high</code>]</td>
    <td>
      안전한 한도 내에 있는 평균 음역 등고선 레벨의 정규화된 상대
      변경입니다. 속성은 인식된 평균 어조 레벨을
      제어합니다. SSML <code>&lt;prosody&gt;</code> 요소의
      <code>pitch</code> 속성에서 가져옵니다. 이로 인해
      인식된 화자의 ID가 변경될 수 있습니다.
    </td>
  </tr>
  <tr>
    <td><code>pitch_range</code></td>
    <td style="text-align:center">[-100%, 100%],<br/>
      [<code>x-narrow</code>, <code>narrow</code>, <code>default</code>,
      <code>wide</code>, <code>x-wide</code>]</td>
    <td>
      안전한 한도 내의 음역 등고선 동적 범위의 정규화된 상대
      변경입니다. 음역 범위를 늘리거나 줄이면 말하기 방식이
      더 많거나 더 적게 표시될 수 있습니다. 속성은
      SSML <code>&lt;prosody&gt;</code> 요소의
      <code>range</code> 속성에서 가져옵니다.</td>
  </tr>
  <tr>
    <td><code>glottal_tension</code></td>
    <td style="text-align:center">[-100%, 100%],<br/>
      [<code>x-low</code>, <code>low</code>, <code>default</code>,
      <code>high</code>, <code>x-high</code>]</td>
    <td>
      안전한 한도 내의 성문 장력의 정규화된 상대
      변경입니다. 성문 장력을 늘리거나 줄이면 음성이
      좀 더 긴장되거나 이완된 발음으로 인식됩니다. 양수를 사용하면
      웅웅거리는 소리가 발생할 수 있습니다. 이는 <code>breathiness</code> 속성 값을 늘려
      줄일 수 있습니다. 음수 값은
      좀 더 많이 호흡하고 일반적으로 더욱 편안한 소리로 인식됩니다.
    </td>
  </tr>
  <tr>
    <td><code>breathiness</code></td>
    <td style="text-align:center">[-100%, 100%],<br/>
      [<code>x-low</code>, <code>low</code>, <code>default</code>,
      <code>high</code>, <code>x-high</code>]</td>
    <td>
      안전한 한도 내의 인식되는 흡출음 레벨의 정규화된 상대
      변경입니다. 극단값으로 소음(양수 기식성) 또는
      웅웅거리는 소리(음수 기식성)가
      생성될 수 있습니다. 웅웅거리거나 추가 소음을 줄이는 데 이 속성을 사용하면
      다른 속성의 부작용이 발생할 수 있습니다.
    </td>
  </tr>
  <tr>
    <td><code>rate</code></td>
    <td style="text-align:center">[-100%, 100%],<br/>
      [<code>x-slow</code>, <code>slow</code>, <code>default</code>,
      <code>fast</code>, <code>x-fast</code>]</td>
    <td>
      안전한 한도 내에 있는 음성 속도의 정규화된 상대
      변경입니다.
      속도를 높이거나 줄이면 음성이 더 빨라지거나 느려집니다.
      양의(더 빠른) 속도는 인지된 음역 범위를 좀 더 늘리고
      음의(더 느린) 속도는 지각적으로 음역 범위를 좁힙니다.
      속성은 SSML <code>&lt;prosody&gt;</code> 요소의
      <code>rate</code> 속성에서 가져옵니다.</td>
  </tr>
  <tr>
    <td><code>timbre</code></td>
    <td style="text-align:center">[<code>Sunrise</code>,
      <code>Breeze</code>]</td>
    <td>
      기본 제공 성도 변환 중 하나(<code>Sunrise</code> 또는 <code>Breeze</code>)의
      이름(대소문자 구분)입니다.
      이름은 상징적입니다. 음성 변환에 영향을 주는 방법을 알아보기 위해
      음색을 실험합니다. 속성으로 인해
      인식된 화자의 ID가 변경될 수 있습니다.
    </td>
  </tr>
  <tr>
    <td><code>timbre_extent</code></td>
    <td style="text-align:center">[0%, 100%]</td>
    <td>
      <code>timbre</code> 성도 변환의 범위입니다.
      <code>0%</code>으로 설정하면 변환이 취소되고, <code>100%</code>는
      변환이 전체적으로 적용됨을 나타냅니다. 속성은 변환된 음성과
      원래 음성의 차이를 수치화합니다. 이를 통해 선택된 음색과 원래 음성의 음색을 결합할
      수 있습니다. 중간 정도의 음색 범위 값을 사용해도
      <code>timbre</code> 속성으로 인해 인식된 화자의 ID가
      변경될 수 있습니다.
    </td>
  </tr>
</table>

### 범위 사용
{: #ranges}

여러 속성의 숫자 범위는 속성이 음성에 영향을 주는 범위를 나타냅니다. 예를 들어, `rate` 속성의 범위는 -100% - 100% 사이입니다.

-   `100%` 값은 음성의 속도가 100% 빨라진 다는 것을 의미하지 않습니다. 서비스가 해당 음성에 허용된 최대값으로 음성의 속도를 높이는 것을 의미합니다.
-   `-100%` 값은 서비스가 음성에 허용된 최소 속도를 사용함을 의미합니다.
-   `0%` 값은 음성에 대한 속성의 고유 레벨을 나타내며, 이때 음성은 변경되지 않습니다.

### 리터럴 값 사용
{: #literals}

편의상 많은 속성이 백분율 대신 사용할 수 있는 리터럴 값도 정의합니다. 이 값의 의미는 SSML `<prosody>` 요소로 사용되는 값과는 다릅니다. `<voice-transformation>` 요소는 속성 간에 일치되는 스케일을 사용합니다.

-   `x-low`, `x-slow` 및 `x-narrow`는 `-100%` 값과 동일합니다.
-   `low`, `slow` 및 `narrow`는 `-50%` 값과 동일합니다.
-   `default`는 해당 속성 및 음성의 기본값인 `0%` 값과 동일합니다.
-   `high`, `fast` 및 `wide`는 `+50%` 값과 동일합니다.
-   `x-high`, `x-fast` 및 `x-wide`는 `+100%` 값과 동일합니다.

### 사용 가이드라인
{: #guidelines}

다음 가이드라인 및 주의 정보를 따르십시오.

-   음성 브랜딩 또는 여러 역할이 있는 애플리케이션의 경우 인식된 화자 ID를 변경하려면 `timbre`, `pitch` 및 `glottal_tension` 속성을 사용하십시오. 세 가지 속성의 조합을 사용하여 가상 음성을 작성할 수 있습니다. 가상 음성을 지정된 음색, 음역 및 성문 장력으로 실현되는 다차원 공간의 지점으로 간주하십시오. 속성의 여러 조합으로 서로 다른 가상 음성이 생성됩니다.
-   `pitch_range`, `breathiness` 및 `rate` 속성을 사용하여 가상 음성에 특성을 추가할 수 있습니다. 다른 사용자는 동일하거나 유사한 속성 값을 선택할 수 있으며, 이에 따라 서비스는 가상 음성의 고유성을 보장할 수 없습니다.
-   속성 적용 시 다음 잠재적인 부작용에 유의하십시오.
    -   높은 성문 장력, 높은 음역, 낮은 속도가 설정되면 웅웅거리는 소리가 발생할 수 있습니다. 기식성을 늘리면 이 현상이 줄어듭니다.
    -   극도로 낮은 성문 장력이 설정되면 소음이 생성될 수 있습니다. 소음을 줄이려면 기식성을 줄이십시오.
    -   음역 범위 및 속도를 동시에 극단적인 수준으로 높이거나 낮추면 음성이 비정상적으로 발생할 수 있습니다.
-   언급한 대로, 일부 속성은 SSML `<prosody>` 요소에서 가져옵니다. 자세한 정보는 [prosody 요소](/docs/services/text-to-speech?topic=text-to-speech-elements#prosody_element)를 참조하십시오. 가상 음성의 운율을 세부적으로 제어하기 위해 다음을 수행할 수 있습니다.
    -   `<voice-transformation>` 요소 내의 중첩 `<prosody>` 요소
    -   `<prosody>` 요소 내의 중첩 `<voice-transformation>` 요소

    `<voice-transformation>` 요소를 중첩할 수 *없습니다*.

## 사용자 정의 변환 예
{: #ssml-custom-transforms-examples}

다음 예는 사용자 정의 변환의 가능한 적용을 보여주도록 여러 속성을 적용합니다. 첫 번째 예에서는 성문 장력을 줄여 좀 더 부드러운 음성이 발생하도록 합니다. 또한 음역 범위 및 속도를 적절하게 늘려서 좀 더 동적인 말하기 방식을 도입할 수도 있습니다.

```xml
<voice-transformation type="Custom" glottal_tension="-50%"
  pitch_range="30%" rate="10%">
  Do you have more information?
</voice-transformation>
```
{: codeblock}

두 번째 예에서는 최대 성문 장력 및 음역과 최저 속도를 사용합니다. 일반적으로 이러한 조합은 선호되지 않으며 웅웅거리는 소음이 생성될 수 있습니다. 예에서는 기식성을 늘려 이 현상을 줄입니다.

```xml
<voice-transformation type="Custom" glottal_tension="100%" pitch="100%"
  rate="-100%" breathiness="60%">
  Do you have more information?
</voice-transformation>
```
{: codeblock}

다음 두 가지 예에서는 음색을 적용하여 인식되는 화자 ID를 변경할 수 있습니다. 음성은 결합의 범위를 제어하고 음역 레벨을 변경하여 바뀔 수 있습니다. 첫 번째 예에서는 기본 음색 범위인 100%를 사용합니다.

```xml
<voice-transformation type="Custom" timbre="Sunrise" pitch="40%">
  Do you have more information?
</voice-transformation>

<voice-transformation type="Custom" timbre="Breeze" timbre_extent="30%"
  pitch="-30%">
  Do you have more information?
</voice-transformation>
```
{: codeblock}

다음 예에서는 다중 속성을 사용하여 음성을 변환합니다. 여기에서는 기본 음색 범위를 사용하고 기식성을 생략합니다.

```xml
<voice-transformation type="Custom" timbre="Sunrise" pitch="-30%"
  pitch_range="80%" rate="60%" glottal_tension="-80%">
  Do you have more information?
</voice-transformation>
```
{: codeblock}
