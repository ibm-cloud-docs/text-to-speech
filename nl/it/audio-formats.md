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

# Formati audio
{: #audioFormats}

Il servizio {{site.data.keyword.texttospeechfull}} può restituire l'audio sintetizzato in numerosi formati. Per la maggior parte dei formati, il servizio restituisce l'audio con una velocità di campionamento predefinita di 22.050 Hz. Per alcuni formati, puoi o devi specificare la velocità di campionamento dell'audio. Il servizio restituisce sempre l'audio a canale singolo per tutti i formati.
{: shortdesc}

## Formati audio supportati
{: #formatsSupported}

La Tabella 1 elenca i formati audio (tipi MIME) in cui puoi richiedere l'audio sintetizzato. Per impostazione predefinita, il servizio restituisce l'audio in formato Ogg con il codec Opus (`audio/ogg;codecs=opus`).

<table>
  <caption>Tabella 1. Formati audio supportati</caption>
  <tr>
    <th style="text-align:left; width:25%">Formato audio</th>
    <th style="text-align:left">Descrizione</th>
  </tr>
  <tr>
    <td>
      <code>audio/basic</code>
    </td>
    <td>
      <em>Audio di base</em>, un formato audio con perdita di dati a canale singolo
      che viene codificato utilizzando dati u-law (o mu-law) a 8 bit campionati a 8 kHz.
      Questo formato fornisce un tipo di supporto con un minimo comune denominatore. Per ulteriori
      informazioni, vedi IETF
      <a target="_blank" href="https://tools.ietf.org/html/rfc2046">Request
        for Comment (RFC) 2046 ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")</a> e
      <a target="_blank" href="http://www.iana.org/assignments/media-types/audio/basic">iana.org/assignments/media-types/audio/basic ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")</a>.
    </td>
  </tr>
  <tr>
    <td>
      <code>audio/flac</code>
    </td>
    <td>
      <em>FLAC (Free Lossless Audio Codec)</em> (<code>.flac</code>),
      un formato di codifica audio compresso senza perdita di dati. Per ulteriori informazioni, vedi
      <a target="_blank" href="https://en.wikipedia.org/wiki/FLAC">en.wikipedia.org/wiki/FLAC ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")</a>.
    </td>
  </tr>
  <tr>
    <td>
      <code>audio/l16;rate={rate}</code>
    </td>
    <td>
      <em>PCM (Pulse-Code Modulation) lineare a 16 bit</em>, un formato di dati
      audio non compresso (spesso <code>.raw</code> o <code>.pcm</code>). Per
      ulteriori informazioni, vedi IETF (Internet Engineering Task Force)
      <a target="_blank" href="https://tools.ietf.org/html/rfc2586">Request
        for Comment (RFC) 2586 ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")</a> e
      <a target="_blank" href="https://en.wikipedia.org/wiki/Pulse-code_modulation">en.wikipedia.org/wiki/Pulse-code_modulation ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")</a>.<br/><br/>
      Con questo formato audio devi specificare la velocità di campionamento. Ad esempio,
      specifica <code>audio/l16;rate=16000</code> per l'audio campionato a
      16 kHz. Facoltativamente, puoi anche specificare la proprietà endian come
      <code>audio/l16;rate={rate};endianness=big-endian</code> o
      <code>audio/l16;rate={rate};endianness=little-endian</code>.
      L'impostazione predefinita è little endian.
    </td>
  </tr>
  <tr>
    <td>
      <code>audio/mp3</code><br/>
      <code>audio/mpeg</code>
    </td>
    <td>
      <em>MP3</em> o <em>MPEG (Motion Picture Experts Group)</em>, un formato di
      compressione dati con perdita di dati (MP3 e MPEG si riferiscono allo stesso formato).
      Per ulteriori informazioni, vedi
      <a target="_blank" href="https://en.wikipedia.org/wiki/MP3">en.wikipedia.org/wiki/MP3 ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")</a>.
    </td>
  </tr>
  <tr>
    <td>
      <code>audio/mulaw;rate={rate}</code>
    </td>
    <td>
      <em>Audio mu-law (o u-law) a 8 bit</em>, un formato audio con perdita di dati a canale
      singolo che viene codificato utilizzando dati u-law (o mu-law) a 8 bit. Con questo formato
      audio devi specificare la velocità di campionamento. Per ulteriori informazioni,
      vedi
      <a target="_blank" href="https://en.wikipedia.org/wiki/M-law_algorithm">en.wikipedia.org/wiki/M-law_algorithm ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")</a>.
    </td>
  </tr>
  <tr>
    <td>
      <code>audio/ogg</code><br/>
      <code>audio/ogg;codecs=opus</code><br/>
      <code>audio/ogg;codecs=vorbis</code>
    </td>
    <td>
      <em>Formato Ogg</em> (<code>.ogg</code>), un formato contenitore aperto
      e gratuito gestito da Xiph.org Foundation. Per ulteriori informazioni, vedi
      <a target="_blank" href="https://www.xiph.org/ogg/">xiph.org/ogg/ ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")</a>.
      Puoi richiedere flussi audio compressi con i seguenti
      codec:
      <ul style="margin-left:20px; padding:0px;">
        <li style="margin:10px 0px; line-height:120%;">
          <em>Opus</em>. Per ulteriori informazioni, vedi
          <a target="_blank" href="https://www.opus-codec.org/">opus-codec.org ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")</a> e
          <a target="_blank" href="https://en.wikipedia.org/wiki/Opus">en.wikipedia.org/wiki/Opus (audio format) ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")</a>.
          Nella pagina <em>Opus (audio format)</em>, consulta in particolare la sezione
          <em>Containers</em>.
        </li>
        <li style="margin:10px 0px; line-height:120%;">
          <em>Vorbis</em>. Per ulteriori informazioni, vedi
          <a target="_blank" href="https://xiph.org/vorbis/">xiph.org/vorbis ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")</a> e
          <a target="_blank" href="https://en.wikipedia.org/wiki/Vorbis">en.wikipedia.org/wiki/Vorbis ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")</a>.
        </li>
      </ul>
      Entrambi i codec sono formati di compressione audio gratuiti, aperti e con perdita di dati. Opus
      è il codec preferito, ma secondo la specifica Ogg, il servizio
      restituisce l'audio in formato Vorbis se ometti il codec. Se
      ometti del tutto il formato audio, il servizio restituisce l'audio in
      formato Ogg con il codec Opus per impostazione predefinita.
    </td>
  </tr>
  <tr>
    <td>
      <code>audio/wav</code>
    </td>
    <td>
      <em>WAV (Waveform Audio File Format)</em> (<code>.wav</code>) è
      un formato contenitore standard che viene spesso utilizzato per i
      bitstream audio non compressi, ma può contenere anche audio compresso. A causa della
      natura streaming dell'audio restituito, il file WAV generato
      potrebbe non funzionare in tutti i lettori audio. In particolare,
      l'attributo <code>numSamples</code> nell'intestazione del file
      è impostato su <code>0</code> indipendentemente dalla lunghezza dell'audio.
      Per ulteriori informazioni, vedi
      <a target="_blank" href="https://en.wikipedia.org/wiki/WAV">en.wikipedia.org/wiki/WAV ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")</a>.
    </td>
  </tr>
  <tr>
    <td>
      <code>audio/webm</code><br/>
      <code>audio/webm;codecs=opus</code><br/>
      <code>audio/webm;codecs=vorbis</code>
    </td>
    <td>
      <em>WebM (Web Media)</em> (<code>.webm</code>), un formato di file multimediale
      aperto che fornisce supporto per i flussi audio compressi con
      i codec audio Opus e Vorbis. Se ometti il codec, il
      servizio restituisce l'audio in formato Opus. Per ulteriori informazioni, vedi
      <a target="_blank" href="https://www.webmproject.org/">webmproject.org ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")</a>.
    </td>
  </tr>
</table>

## Specifica di un formato audio
{: #formatSpecify}

La specifica di un formato audio è facoltativa. Per impostazione predefinita, il servizio restituisce l'audio in formato `audio/ogg;codecs=opus`. Tuttavia, puoi specificare un formato per l'interfaccia HTTP o WebSocket:

-   Con i metodi HTTP `GET` e `POST /v1/synthesize`, specifica un formato utilizzando l'intestazione della richiesta `Accept` o il parametro di query `accept`. Per ricevere l'audio nel formato predefinito, ometti sia l'intestazione che il parametro di query. Per ulteriori informazioni, vedi [Sintetizzazione del testo in audio](/docs/services/text-to-speech/http.html#synthesize).

    Se utilizzi il parametro di query `accept`, codifica in URL l'argomento nel parametro. Ad esempio, codifica in URL il seguente argomento

    ```
    audio/l16;rate=16000;endianness=little-endian
    ```
    {: codeblock}

    come

    ```
    audio%2Fl16%3Brate%3D16000%3Bendianness%3Dlittle-endian
    ```
    {: codeblock}

-   Con l'interfaccia WebSocket, specifica un formato utilizzando il parametro `accept` del messaggio di testo che passi per avviare la sintesi. Per ricevere l'audio nel formato predefinito, specifica il valore `*/*` per il parametro. Per ulteriori informazioni, vedi [Invia il testo di input](/docs/services/text-to-speech/websockets.html#WSsend).

## Specifica di una velocità di campionamento
{: #formatRate}

Il servizio sintetizza l'audio sempre con una velocità di campionamento di 22.050 Hz. Per la maggior parte dei formati audio, il servizio restituisce l'audio con questa velocità di campionamento predefinita. Per alcuni formati, puoi specificare una velocità di campionamento diversa includendo il parametro `rate={rate}`. Per i formati `audio/l16` e `audio/mulaw`, *devi* specificare una velocità di campionamento.

Quando specifichi una velocità di campionamento, il servizio ricampiona l'audio e lo restituisce alla velocità specificata. Una velocità di campionamento specificata deve essere compresa tra 8 kHz e 192 kHz.

La Tabella 2 mostra la velocità di campionamento predefinita dell'audio che viene restituita per ciascun formato e indica quei formati per i quali puoi o devi specificare una velocità di campionamento.

<table style="width:90%">
  <caption>Tabella 2. Velocità di campionamento per i formati audio</caption>
  <tr>
    <th style="text-align:left">Formato audio</th>
    <th style="text-align:center">Velocità di campionamento predefinita</th>
    <th style="text-align:center">Utilizzo del parametro <code>rate</code></th>
  </tr>
  <tr>
    <td>
      <code>audio/basic</code>
    </td>
    <td style="text-align:center">
      8000 Hz
    </td>
    <td style="text-align:center">
      Non consentito
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
      Facoltativo
    </td>
  </tr>
  <tr>
    <td>
      <code>audio/l16;rate={rate}</code>
    </td>
    <td style="text-align:center">
      Nessuno
    </td>
    <td style="text-align:center">
      Obbligatorio; ad esempio<br />
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
      Facoltativo
    </td>
  </tr>
  <tr>
    <td>
      <code>audio/mulaw;rate={rate}</code>
    </td>
    <td style="text-align:center">
      Nessuno
    </td>
    <td style="text-align:center">
      Obbligatorio; ad esempio<br />
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
      Facoltativo
    </td>
  </tr>
  <tr>
    <td>
      <code>audio/ogg;codecs=opus</code>
    </td>
    <td style="text-align:center">
      22.050 Hz [vedi <strong>Nota</strong>]
    </td>
    <td style="text-align:center">
      Facoltativo
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
      Facoltativo
    </td>
  </tr>
  <tr>
    <td>
      <code>audio/webm</code><br/>
      <code>audio/webm;codecs=opus</code>
    </td>
    <td style="text-align:center">
      48.000 Hz [vedi <strong>Nota</strong>]
    </td>
    <td style="text-align:center">
      Non consentito
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
      Facoltativo
    </td>
  </tr>
</table>

Il modo più affidabile per identificare la velocità di campionamento per qualsiasi flusso audio restituito dal servizio è estrarre le informazioni dal flusso stesso. Puoi determinare la velocità chiamando il metodo `/v1/synthesize` con un testo semplice (ad esempio, "hello world") e specificando il formato e il codec che prevedi di utilizzare. Puoi quindi ottenere il codec e la velocità di campionamento salvando il flusso audio in un file e aprendolo in un lettore audio.

Lo standard Opus richiede che la velocità di campionamento in uscita corrisponda alle capacità del lettore audio. Per ulteriori informazioni, vedi la Sezione 5.1 dell'IETF (Internet Engineering Task Force) [Request for Comments (RFC) 7845 ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](http://tools.ietf.org/html/rfc6455){: new_window}. Per i lettori audio software, la tabella indica la velocità di campionamento in uscita tipica, ma la velocità di campionamento effettiva dell'audio varia con il tempo all'interno del flusso. Come accennato, il servizio sintetizza l'audio di origine a 22.050 Hz.
{: note}

## Riproduzione di un file audio
{: #formatsPlay}

Per riprodurre un file audio generato dal servizio, utilizza uno dei seguenti strumenti:

-   Un browser web come Google Chrome&trade;, Firefox&reg; o Microsoft&reg; Internet Explorer&reg;.
-   Un lettore audio come Audacity&reg; ([audacityteam.org ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](http://www.audacityteam.org/){: new_window}) o FFmpeg ([ffmpeg.org ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://www.ffmpeg.org){: new_window}).
