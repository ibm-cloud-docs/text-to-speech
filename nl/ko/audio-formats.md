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

# 오디오 형식
{: #audioFormats}

{{site.data.keyword.texttospeechfull}} 서비스는 여러 형식으로 합성된 오디오를 리턴할 수 있습니다. 대부분의 형식의 경우, 서비스는 22,050Hz의 기본 샘플링 속도로 오디오를 리턴합니다. 일부 형식의 경우, 오디오의 샘플링 속도를 지정할 수 있거나 지정해야 합니다. 서비스는 항상 모든 형식에 맞게 단일 채널 오디오를 리턴합니다.
{: shortdesc}

## 지원되는 오디오 형식
{: #formatsSupported}

표 1에는 합성된 오디오를 요청할 수 있는 오디오 형식(MIME 유형)이 나열되어 있습니다. 기본적으로 서비스는 Opus 코덱이 포함된 Ogg 형식(`audio/ogg;codecs=opus`)으로 오디오를 리턴합니다.

<table>
  <caption>표 1. 지원되는 오디오 형식</caption>
  <tr>
    <th style="text-align:left; width:25%">오디오 형식</th>
    <th style="text-align:left">설명</th>
  </tr>
  <tr>
    <td>
      <code>audio/basic</code>
    </td>
    <td>
      <em>기본 오디오</em>. 8kHz에서 샘플링되는 8비트 u-law(또는 mu-law)
      데이터를 사용하여 인코딩된 단일 채널의 손실 압축 오디오 형식입니다.
      이 형식은 최소 공통 요소의 매체 유형을 제공합니다. 자세한 정보는
      IETF
      <a target="_blank" href="https://tools.ietf.org/html/rfc2046">RFC(Request
        for Comment) 2046 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")</a> 및
      <a target="_blank" href="http://www.iana.org/assignments/media-types/audio/basic">iana.org/assignments/media-types/audio/basic ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")</a>을 참조하십시오.
    </td>
  </tr>
  <tr>
    <td>
      <code>audio/flac</code>
    </td>
    <td>
      <em>FLAC(Free Lossless Audio Codec)</em>(<code>.flac</code>).
      무손실 압축 오디오 코딩 형식입니다. 자세한 정보는
      <a target="_blank" href="https://en.wikipedia.org/wiki/FLAC">en.wikipedia.org/wiki/FLAC ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")</a>를 참조하십시오.
    </td>
  </tr>
  <tr>
    <td>
      <code>audio/l16;rate={rate}</code>
    </td>
    <td>
      <em>선형 16비트 PCM(Pulse-Code Modulation)</em>. 압축되지 않은 오디오 데이터
      형식입니다(종종 <code>.raw</code> 또는 <code>.pcm</code>). 자세한 정보는
      IETF(Internet Engineering Task Force)
      <a target="_blank" href="https://tools.ietf.org/html/rfc2586">RFC(Request
        for Comment) 2586 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")</a> 및
      <a target="_blank" href="https://en.wikipedia.org/wiki/Pulse-code_modulation">en.wikipedia.org/wiki/Pulse-code_modulation ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")</a>을 참조하십시오.<br/><br/>
      이 오디오 형식으로 샘플링 속도를 지정해야 합니다. 예를 들어,
      16kHz에서 샘플링되는 오디오의 경우 <code>audio/l16;rate=16000</code>을
      지정하십시오. 선택적으로
      <code>audio/l16;rate={rate};endianness=big-endian</code> 또는
      <code>audio/l16;rate={rate};endianness=little-endian</code>으로 엔디언도 지정할 수 있습니다.
      기본값은 리틀 엔디언입니다.
    </td>
  </tr>
  <tr>
    <td>
      <code>audio/mp3</code><br/>
      <code>audio/mpeg</code>
    </td>
    <td>
      <em>MP3</em> 또는 <em>MPEG(Motion Picture Experts Group)</em>. 손실
      데이터 압축 형식입니다(MP3 및 MPEG는 같은 형식을 나타냄).
      자세한 정보는
      <a target="_blank" href="https://en.wikipedia.org/wiki/MP3">en.wikipedia.org/wiki/MP3 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")</a>를 참조하십시오.
    </td>
  </tr>
  <tr>
    <td>
      <code>audio/mulaw;rate={rate}</code>
    </td>
    <td>
      <em>8비트 mu-law(또는 u-law) 오디오</em>. 8비트 u-law(또는 mu-law) 데이터를 사용하여
      인코딩된 단일 채널의 손실 압축 오디오 형식입니다. 이 오디오 형식과 함께 샘플링 속도를
      지정해야 합니다. 자세한
      정보는
      <a target="_blank" href="https://en.wikipedia.org/wiki/M-law_algorithm">en.wikipedia.org/wiki/M-law_algorithm ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")</a>을 참조하십시오.
    </td>
  </tr>
  <tr>
    <td>
      <code>audio/ogg</code><br/>
      <code>audio/ogg;codecs=opus</code><br/>
      <code>audio/ogg;codecs=vorbis</code>
    </td>
    <td>
      <em>Ogg 형식</em>(<code>.ogg</code>). Xiph.org Foundation에서 유지보수하는
      개방형 컨테이너 형식입니다. 자세한 정보는
      <a target="_blank" href="https://www.xiph.org/ogg/">xiph.org/ogg/ ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")</a>를 참조하십시오.
      다음 코덱으로 압축된 오디오 스트림을 요청할 수
      있습니다.
      <ul style="margin-left:20px; padding:0px;">
        <li style="margin:10px 0px; line-height:120%;">
          <em>Opus</em>. 자세한 정보는
          <a target="_blank" href="https://www.opus-codec.org/">opus-codec.org ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")</a> 및
          <a target="_blank" href="https://en.wikipedia.org/wiki/Opus">en.wikipedia.org/wiki/Opus(오디오 형식) ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")</a>를 참조하십시오.
          <em>Opus(오디오 형식)</em> 페이지에서 특히
          <em>컨테이너</em> 섹션을 살펴보십시오.
        </li>
        <li style="margin:10px 0px; line-height:120%;">
          <em>Vorbis</em>. 자세한 정보는
          <a target="_blank" href="https://xiph.org/vorbis/">xiph.org/vorbis ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")</a> 및
          <a target="_blank" href="https://en.wikipedia.org/wiki/Vorbis">en.wikipedia.org/wiki/Vorbis ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")</a>를 참조하십시오.
        </li>
      </ul>
      두 코텍은 무료로 제공되는 개방형 손실 오디오 압축 형식입니다. Opus는
      선호되는 코덱이지만 Ogg 스펙당 코덱을 생략하는 경우 서비스는
      Vorbis 형식으로 오디오를 리턴합니다. 오디오
      형식을 함께 생략하는 경우 기본적으로 서비스는 Opus 코덱이
      포함된 Ogg 형식으로 오디오를 리턴합니다.
    </td>
  </tr>
  <tr>
    <td>
      <code>audio/wav</code>
    </td>
    <td>
      <em>파형 오디오 파일 형식(WAV)</em>(<code>.wav</code>)은
      압축되지 않은 오디오 비트스트림에 종종 사용되는 표준 컨테이너
      형식이지만 압축된 오디오도 포함될 수 있습니다. 리턴된 오디오의
      스트리밍 특성으로 인해 생성되는 WAV 파일은 모든 오디오 플레이어에서
      작동하지 않을 수 있습니다. 특히 파일의 헤더에 있는
      <code>numSamples</code> 속성은 오디오 길이에 관계 없이
      <code>0</code>으로 설정됩니다.
      자세한 정보는
      <a target="_blank" href="https://en.wikipedia.org/wiki/WAV">en.wikipedia.org/wiki/WAV ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")</a>를 참조하십시오.
    </td>
  </tr>
  <tr>
    <td>
      <code>audio/webm</code><br/>
      <code>audio/webm;codecs=opus</code><br/>
      <code>audio/webm;codecs=vorbis</code>
    </td>
    <td>
      <em>WebM(Web Media)</em>(<code>.webm</code>)은 Opus 및 Vorbis 오디오 코덱으로
      압축되는 오디오 스트림에 대한 지원을 제공하는 개방형 매체 파일
      형식입니다. 코덱을 생략하는 경우 서비스는 Opus 형식으로
      오디오를 리턴합니다. 자세한 정보는
      <a target="_blank" href="https://www.webmproject.org/">webmproject.org ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")</a>를 참조하십시오.
    </td>
  </tr>
</table>

## 오디오 형식 지정
{: #formatSpecify}

오디오 형식 지정은 선택사항입니다. 기본적으로 서비스는 `audio/ogg;codecs=opus` 형식으로 오디오를 리턴합니다. 그러나 HTTP 또는 WebSocket 인터페이스에 대한 형식을 지정할 수 있습니다. 

-   HTTP `GET` 및 `POST /v1/synthesize` 메소드를 통해 `Accept` 요청 헤더 또는 `accept` 조회 매개변수를 사용하여 형식을 지정합니다. 기본 형식으로 오디오를 수신하려면 헤더 및 조회 매개변수를 모두 생략하십시오. 자세한 정보는 [텍스트-오디오 변환 합성](/docs/services/text-to-speech/http.html#synthesize)을 참조하십시오.

    `accept` 조회 매개변수를 사용하는 경우 매개변수에 대한 인수를 URL로 인코딩하십시오. 예를 들어, 다음 인수를 아래와 같이 URL로 인코딩하십시오. 

    ```
    audio/l16;rate=16000;endianness=little-endian
    ```
    {: codeblock}

    ->

    ```
    audio%2Fl16%3Brate%3D16000%3Bendianness%3Dlittle-endian
    ```
    {: codeblock}

-   WebSocket 인터페이스를 통해 합성을 시작하기 위해 전달하는 텍스트 메시지의 `accept` 매개변수를 사용하여 형식을 지정합니다. 기본 형식으로 오디오를 수신하려면 매개변수에 `*/*` 값을 지정하십시오. 자세한 정보는 [입력 텍스트 전송](/docs/services/text-to-speech/websockets.html#WSsend)을 참조하십시오.

## 샘플링 속도 지정
{: #formatRate}

서비스는 항상 22,050Hz의 샘플링 속도로 오디오를 합성합니다. 대부분의 오디오 형식의 경우 서비스는 기본 샘플링 속도로 오디오를 리턴합니다. 일부 형식의 경우 `rate={rate}` 매개변수를 포함하여 여러 샘플링 속도를 지정할 수 있습니다. `audio/l16` 및 `audio/mulaw` 형식의 경우 샘플링 속도를 *지정해야* 합니다. 

샘플링 속도를 지정하는 경우 서비스는 지정된 속도로 오디오를 다시 샘플링하여 리턴합니다. 지정된 샘플링 속도의 범위는 8kHz - 192kHz 사이여야 합니다. 

표 2에서는 각 형식에 대해 리턴된 오디오의 기본 샘플링 속도를 표시하고 샘플링 속도를 지정할 수 있거나 지정해야 하는 형식을 나타냅니다. 

<table style="width:90%">
  <caption>표 2. 오디오 형식에 대한 샘플링 속도</caption>
  <tr>
    <th style="text-align:left">오디오 형식</th>
    <th style="text-align:center">기본 샘플링 속도</th>
    <th style="text-align:center"><code>rate</code> 매개변수 사용</th>
  </tr>
  <tr>
    <td>
      <code>audio/basic</code>
    </td>
    <td style="text-align:center">
      8000Hz
    </td>
    <td style="text-align:center">
      허용되지 않음
    </td>
  </tr>
  <tr>
    <td>
      <code>audio/flac</code>
    </td>
    <td style="text-align:center">
      22,050Hz
    </td>
    <td style="text-align:center">
      선택사항
    </td>
  </tr>
  <tr>
    <td>
      <code>audio/l16;rate={rate}</code>
    </td>
    <td style="text-align:center">
없음
    </td>
    <td style="text-align:center">
      필수. 예를 들면, 다음과 같습니다. <br />
      <code>audio/l16;rate=22050</code>
    </td>
  </tr>
  <tr>
    <td>
      <code>audio/mp3</code><br/>
      <code>audio/mpeg</code>
    </td>
    <td style="text-align:center">
      22,050Hz
    </td>
    <td style="text-align:center">
      선택사항
    </td>
  </tr>
  <tr>
    <td>
      <code>audio/mulaw;rate={rate}</code>
    </td>
    <td style="text-align:center">
없음
    </td>
    <td style="text-align:center">
      필수. 예를 들면, 다음과 같습니다. <br />
      <code>audio/mulaw;rate=8000</code>
    </td>
  </tr>
  <tr>
    <td>
      <code>audio/ogg</code><br/>
      <code>audio/ogg;codecs=vorbis</code>
    </td>
    <td style="text-align:center">
      22,050Hz
    </td>
    <td style="text-align:center">
      선택사항
    </td>
  </tr>
  <tr>
    <td>
      <code>audio/ogg;codecs=opus</code>
    </td>
    <td style="text-align:center">
      22,050Hz [<strong>참고</strong>를 참조하십시오.]
    </td>
    <td style="text-align:center">
      선택사항
    </td>
  </tr>
  <tr>
    <td>
      <code>audio/wav</code>
    </td>
    <td style="text-align:center">
      22,050Hz
    </td>
    <td style="text-align:center">
      선택사항
    </td>
  </tr>
  <tr>
    <td>
      <code>audio/webm</code><br/>
      <code>audio/webm;codecs=opus</code>
    </td>
    <td style="text-align:center">
      48,000Hz [<strong>참고</strong>를 참조하십시오.]
    </td>
    <td style="text-align:center">
      허용되지 않음
    </td>
  </tr>
  <tr>
    <td>
      <code>audio/webm;codecs=vorbis</code>
    </td>
    <td style="text-align:center">
      22,050Hz
    </td>
    <td style="text-align:center">
      선택사항
    </td>
  </tr>
</table>

서비스가 리턴하는 오디오 스트림에 대한 샘플링 속도를 식별하는 가장 확실한 방법은 자체적으로 스트림에서 정보를 추출하는 것입니다. 일부 단순 텍스트(예:"hello world")를 사용하여 `/v1/synthesize` 메소드를 호출하고 사용할 계획인 형식 및 코덱을 지정하여 속도를 결정할 수 있습니다. 그런 다음 오디오 스트림을 파일에 저장하고 오디오 플레이어에서 열어 코덱 및 샘플링 속도를 가져올 수 있습니다. 

Opus 표준에는 오디오 플레이어의 기능과 일치하는 출력 샘플링 속도가 필요합니다. 자세한 정보는 IETF(Internet Engineering Task Force)의 5.1 절 [RFC(Request for Comments) 7845 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](http://tools.ietf.org/html/rfc6455){: new_window}를 참조하십시오. 소프트웨어 오디오 플레이어의 경우 표에는 일반적인 출력 샘플링 속도가 표시되지만 오디오의 실제 샘플링 속도는 스트림 내의 시간에 따라 달라집니다. 언급된 대로, 서비스는 22,050Hz에서 소스 오디오를 합성합니다.
{: note}

## 오디오 파일 재생
{: #formatsPlay}

서비스가 생성하는 오디오 파일을 재생하려면 다음 도구 중 하나를 사용하십시오.

-   웹 브라우저(예: Google Chrome&trade;, Firefox&reg; 또는 Microsoft&reg; Internet Explorer&reg;)
-   오디오 플레이어(예: Audacity&reg; ([audacityteam.org ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](http://www.audacityteam.org/){: new_window}) 또는 FFmpeg([ffmpeg.org ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://www.ffmpeg.org){: new_window}))
