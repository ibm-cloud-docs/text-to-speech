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

# Formatos de audio
{: #audioFormats}

El servicio {{site.data.keyword.texttospeechfull}} puede devolver audio sintetizado en diversos formatos. Para la mayoría de los formatos, el servicio devuelve el audio con una frecuencia de muestreo predeterminada de 22.050 Hz. Para algunos formatos, puede o debe especificar la frecuencia de muestreo del audio. El servicio siempre devuelve un audio de un solo canal para todos los formatos.
{: shortdesc}

## Formatos de audio soportados
{: #formatsSupported}

En la Tabla 1 se enumeran los formatos de audio (tipos MIME) en los que se puede solicitar el audio sintetizado. De forma predeterminada, el servicio devuelve el audio en formato Ogg con el códec Opus (`audio/ogg;codecs=opus`).

<table>
  <caption>Tabla 1. Formatos de audio soportados</caption>
  <tr>
    <th style="text-align:left; width:25%">Formato de audio</th>
    <th style="text-align:left">Descripción</th>
  </tr>
  <tr>
    <td>
      <code>audio/basic</code>
    </td>
    <td>
      <em>Basic audio</em>, un formato de audio de un solo canal, con mucha pérdida
      que se codifica utilizando datos u-law (o mu-law) de 8 bits muestreados a 8 kHz.
      Este formato proporciona un tipo de soporte de mínimo común denominador. Para obtener más
      información, consulte el IETF
      <a target="_blank" href="https://tools.ietf.org/html/rfc2046">Request
        for Comment (RFC) 2046 ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")</a> e
      <a target="_blank" href="http://www.iana.org/assignments/media-types/audio/basic">iana.org/assignments/media-types/audio/basic ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")</a>.
    </td>
  </tr>
  <tr>
    <td>
      <code>audio/flac</code>
    </td>
    <td>
      <em>Free Lossless Audio Codec (FLAC)</em> (<code>.flac</code>),
      un formato de código de audio comprimido sin pérdidas. Para obtener más información, consulte
      <a target="_blank" href="https://en.wikipedia.org/wiki/FLAC">en.wikipedia.org/wiki/FLAC ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")</a>.
    </td>
  </tr>
  <tr>
    <td>
      <code>audio/l16;rate={rate}</code>
    </td>
    <td>
      <em>Linear 16-bit Pulse-Code Modulation (PCM)</em>, un formato de datos de
      audio sin comprimir (a menudo <code>.raw</code> o <code>.pcm</code>). Para
      obtener más información, consulte Internet Engineering Task Force (IETF)
      <a target="_blank" href="https://tools.ietf.org/html/rfc2586">Request
        for Comment (RFC) 2586 ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")</a> y
      <a target="_blank" href="https://en.wikipedia.org/wiki/Pulse-code_modulation">en.wikipedia.org/wiki/Pulse-code_modulation ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")</a>.<br/><br/>
      Con este formato de audio, debe especificar la frecuencia de muestreo. Por ejemplo,
      especifique <code>audio/l16;rate=16000</code> para audio muestreado a
      16 kHz. Opcionalmente, también puede especificar la endianness como
      <code>audio/l16;rate={rate};endianness=big-endian</code> o como
      <code>audio/l16;rate={rate};endianness=little-endian</code>.
      El valor predeterminado es little endian.
    </td>
  </tr>
  <tr>
    <td>
      <code>audio/mp3</code><br/>
      <code>audio/mpeg</code>
    </td>
    <td>
      <em>MP3</em> o <em>Motion Picture Experts Group (MPEG)</em>, un formato de
      compresión de datos con mucha pérdida (MP3 y MPEG se refieren al mismo formato).
      Para obtener más información, consulte
      <a target="_blank" href="https://en.wikipedia.org/wiki/MP3">en.wikipedia.org/wiki/MP3 ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")</a>.
    </td>
  </tr>
  <tr>
    <td>
      <code>audio/mulaw;rate={rate}</code>
    </td>
    <td>
      <em>audio mu-law (o u-law) de 8 bits</em>, un formato de audio de un solo canal
      con mucha pérdida que se codifica utilizando datos u-law (o mu-law) de 8 bits. Con este
      formato de audio, debe especificar la frecuencia de muestreo. Para obtener más información,
      consulte
      <a target="_blank" href="https://en.wikipedia.org/wiki/M-law_algorithm">en.wikipedia.org/wiki/M-law_algorithm ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")</a>.
    </td>
  </tr>
  <tr>
    <td>
      <code>audio/ogg</code><br/>
      <code>audio/ogg;codecs=opus</code><br/>
      <code>audio/ogg;codecs=vorbis</code>
    </td>
    <td>
      <em>Formato Ogg</em> (<code>.ogg</code>), un formato de contenedor abierto y
      gratuito que mantiene la Fundación Xiph.org. Para obtener más información, consulte
      <a target="_blank" href="https://www.xiph.org/ogg/">xiph.org/ogg/ ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")</a>.
      Puede solicitar secuencias de audio comprimidas con los siguientes
      códecs:
      <ul style="margin-left:20px; padding:0px;">
        <li style="margin:10px 0px; line-height:120%;">
          <em>Opus</em>. Para obtener más información, consulte
          <a target="_blank" href="https://www.opus-codec.org/">opus-codec.org ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")</a> y
          <a target="_blank" href="https://en.wikipedia.org/wiki/Opus">en.wikipedia.org/wiki/Opus (formato de audio) ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")</a>.
          En la página <em>Opus (formato de audio)</em>, consulte especialmente la sección
          <em>Contenedores</em>.
        </li>
        <li style="margin:10px 0px; line-height:120%;">
          <em>Vorbis</em>. Para obtener más información, consulte
          <a target="_blank" href="https://xiph.org/vorbis/">xiph.org/vorbis ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")</a> y
          <a target="_blank" href="https://en.wikipedia.org/wiki/Vorbis">en.wikipedia.org/wiki/Vorbis ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")</a>.
        </li>
      </ul>
      Los dos códecs son formatos de compresión de audio con mucha pérdida, gratuitos, y abiertos. Opus
      es el códec preferido, pero en la especificación Ogg, el servicio devuelve
      el audio en formato Vorbis si se omite el códec. Si además se
      omite el formato de audio, de forma predeterminada, el
      servicio devuelve el audio en formato Ogg con el códec Opus.
    </td>
  </tr>
  <tr>
    <td>
      <code>audio/wav</code>
    </td>
    <td>
      <em>Waveform Audio File Format (WAV)</em> (<code>.wav</code>) es un formato
      de contenedor estándar que se utiliza a menudo para las secuencias de bits
      de audio no comprimido, pero también puede contener audio comprimido. Debido
      a la naturaleza de streaming del audio devuelto, puede ser que el archivo WAV
      generado no funcione en todos los reproductores de audio. Concretamente,
      el atributo <code>numSamples</code> de la cabecera del archivo está
      definido a <code>0</code> independientemente  de la longitud del audio.
      Para obtener más información, consulte
      <a target="_blank" href="https://en.wikipedia.org/wiki/WAV">en.wikipedia.org/wiki/WAV ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")</a>.
    </td>
  </tr>
  <tr>
    <td>
      <code>audio/webm</code><br/>
      <code>audio/webm;codecs=opus</code><br/>
      <code>audio/webm;codecs=vorbis</code>
    </td>
    <td>
      <em>Web Media (WebM)</em> (<code>.webm</code>), un formato de archivo
      multimedia que ofrece soporte para secuencias de audio comprimidas con
      los códecs de audio Opus y Vorbis. Si se omite el códec, el servicio
      devuelve el audio en formato Opus. Para obtener más información, consulte
      <a target="_blank" href="https://www.webmproject.org/">webmproject.org ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")</a>.
    </td>
  </tr>
</table>

## Especificar un formato de audio
{: #formatSpecify}

Especificar un formato de audio es opcional. De forma predeterminada, el servicio devuelve el audio en formato `audio/ogg;codecs=opus`. Sin embargo, puede especificar un formato para la interfaz HTTP o la interfaz WebSocket:

-   Con los métodos HTTP `GET` y `POST /v1/synthesize`, se puede especificar un formato utilizando la cabecera de la solicitud `Accept` o el parámetro de consulta `accept`. Para recibir audio en el formato predeterminado, se debe omitir tanto la cabecera como el parámetro de consulta. Para obtener más información, consulte [Sintetizar texto a audio](/docs/services/text-to-speech/http.html#synthesize).

    Si utiliza el parámetro de consulta `accept`, codifique como URL el argumento en el parámetro. Por ejemplo, codifique como URL el siguiente argumento

    ```
    audio/l16;rate=16000;endianness=little-endian
    ```
    {: codeblock}

    como

    ```
    audio%2Fl16%3Brate%3D16000%3Bendianness%3Dlittle-endian
    ```
    {: codeblock}

-   Para especificar un formato con la interfaz WebSocket, se utiliza el parámetro `accept` del mensaje de texto que se pasa para iniciar la síntesis. Para recibir audio en el formato predeterminado, se especifica el valor `*/*` en el parámetro. Para obtener más información, consulte [Enviar texto de entrada](/docs/services/text-to-speech/websockets.html#WSsend).

## Especificar una frecuencia de muestreo
{: #formatRate}

El servicio siempre sintetiza el audio con una frecuencia de muestreo de 22.050 Hz. Para la mayoría de los formatos de audio, el servicio devuelve el audio con esta frecuencia de muestreo predeterminada. Para algunos formatos, puede especificar una frecuencia de muestreo distinta incluyendo el parámetro `rate={rate}`. Para los formatos `audio/l16` y `audio/mulaw`, es *necesario* especificar una frecuencia de muestreo.

Cuando se especifica una frecuencia de muestreo, el servicio vuelve a muestrear el audio y lo devuelve a la velocidad especificada. Una frecuencia de muestreo especificada debe estar en el rango de 8 kHz a 192 kHz.

En la tabla 2 se muestra la frecuencia de muestreo predeterminada del audio que se devuelve para cada formato y se indican los formatos para los que se puede o se debe especificar una frecuencia de muestreo.

<table style="width:90%">
  <caption>Tabla 2. Frecuencias de muestreo de los formatos de audio</caption>
  <tr>
    <th style="text-align:left">Formato de audio</th>
    <th style="text-align:center">Frecuencia de muestreo predeterminada</th>
    <th style="text-align:center">Uso del parámetro <code>rate</code></th>
  </tr>
  <tr>
    <td>
      <code>audio/basic</code>
    </td>
    <td style="text-align:center">
      8000 Hz
    </td>
    <td style="text-align:center">
      No permitido
    </td>
  </tr>
  <tr>
    <td>
      <code>audio/flac</code>
    </td>
    <td style="text-align:center">
      22.050 Hz
    </td>
    <td style="text-align:center">
      Opcional
    </td>
  </tr>
  <tr>
    <td>
      <code>audio/l16;rate={rate}</code>
    </td>
    <td style="text-align:center">
      Ninguno
    </td>
    <td style="text-align:center">
      Obligatorio; por ejemplo<br />
      <code>audio/l16;rate=22050</code>
    </td>
  </tr>
  <tr>
    <td>
      <code>audio/mp3</code><br/>
      <code>audio/mpeg</code>
    </td>
    <td style="text-align:center">
      22.050 Hz
    </td>
    <td style="text-align:center">
      Opcional
    </td>
  </tr>
  <tr>
    <td>
      <code>audio/mulaw;rate={rate}</code>
    </td>
    <td style="text-align:center">
      Ninguno
    </td>
    <td style="text-align:center">
      Obligatorio; por ejemplo<br />
      <code>audio/mulaw;rate=8000</code>
    </td>
  </tr>
  <tr>
    <td>
      <code>audio/ogg</code><br/>
      <code>audio/ogg;codecs=vorbis</code>
    </td>
    <td style="text-align:center">
      22.050 Hz
    </td>
    <td style="text-align:center">
      Opcional
    </td>
  </tr>
  <tr>
    <td>
      <code>audio/ogg;codecs=opus</code>
    </td>
    <td style="text-align:center">
      22.050 Hz [consulte la <strong>Nota</strong>]
    </td>
    <td style="text-align:center">
      Opcional
    </td>
  </tr>
  <tr>
    <td>
      <code>audio/wav</code>
    </td>
    <td style="text-align:center">
      22.050 Hz
    </td>
    <td style="text-align:center">
      Opcional
    </td>
  </tr>
  <tr>
    <td>
      <code>audio/webm</code><br/>
      <code>audio/webm;codecs=opus</code>
    </td>
    <td style="text-align:center">
      48.000 Hz [consulte la <strong>Nota</strong>]
    </td>
    <td style="text-align:center">
      No permitido
    </td>
  </tr>
  <tr>
    <td>
      <code>audio/webm;codecs=vorbis</code>
    </td>
    <td style="text-align:center">
      22.050 Hz
    </td>
    <td style="text-align:center">
      Opcional
    </td>
  </tr>
</table>

La forma más fiable de identificar la frecuencia de muestreo para cualquier secuencia de audio que devuelva el servicio es extraer la información de la propia secuencia. Puede determinar la frecuencia llamando al método `/v1/synthesize` con algún texto simple (por ejemplo, "hello world") y especificando el formato y el códec que tiene previsto utilizar. A continuación, puede obtener el códec y la frecuencia de muestreo guardando la secuencia de audio en un archivo y abriéndola en un reproductor de audio.

El estándar Opus requiere que la frecuencia de muestreo de salida coincida con las capacidades del reproductor de audio. Para obtener más información, consulte la sección 5.1 de Internet Engineering Task Force (IETF) [Request for Comments (RFC) 7845 ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](http://tools.ietf.org/html/rfc6455){: new_window}. Para los reproductores de audio de software, la tabla indica la frecuencia de muestreo de salida típica, pero la frecuencia de muestreo real del audio varía con el tiempo dentro de la secuencia. Tal como se ha mencionado, el servicio sintetiza el audio de origen a 22.050 Hz.
{: note}

## Reproducir un archivo de audio
{: #formatsPlay}

Para reproducir un archivo de audio que haya generado el servicio, utilice una de las siguientes herramientas:

-   Un navegador web como por ejemplo Google Chrome&trade;, Firefox&reg; o Microsoft&reg; Internet Explorer&reg;.
-   Un reproductor de audio como por ejemplo Audacity&reg; ([audacityteam.org ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](http://www.audacityteam.org/){: new_window}) o FFmpeg ([ffmpeg.org ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://www.ffmpeg.org){: new_window}).
