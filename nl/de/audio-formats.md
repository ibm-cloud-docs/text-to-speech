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

# Audioformate
{: #audioFormats}

Der {{site.data.keyword.texttospeechfull}}-Service kann synthetisch erstellte Audioausgabe in einer Reihe von Formaten zurückgeben. Bei den meisten Formaten gibt der Service die Audioausgabe mit einer Standardabtastfrequenz von 22.050 Hz zurück. Bei einigen Formaten können oder müssen Sie die Abtastfrequenz der Audioausgabe angeben. Für alle Formate gibt der Service die Ausgabe stets im Einkanalton zurück.
{: shortdesc}

## Unterstützte Audioformate
{: #formatsSupported}

In Tabelle 1 sind die Audioformate (MIME-Typen) aufgelistet, in denen Sie synthetisch erstellte Audioausgabe anfordern können. Standardmäßig gibt der Service die Audioausgabe im Format 'Ogg' mit Opus-Codec zurück (`audio/ogg;codecs=opus`).

<table>
  <caption>Tabelle 1. Unterstützte Audioformate</caption>
  <tr>
    <th style="text-align:left; width:25%">Audioformat</th>
    <th style="text-align:left">Beschreibung</th>
  </tr>
  <tr>
    <td>
      <code>audio/basic</code>
    </td>
    <td>
      Das <em>Basisaudioformat</em> ist ein verlustbehaftetes
      Einkanalaudioformat, das unter Verwendung von mit 8 kHz abgetasteten
      8-Bit-U-Law-Daten (oder Mu-Law-Daten) codiert wird. Dieses Format stellt
      einen Medientyp mit dem kleinsten gemeinsamen Nenner bereit. Weitere
Informationen finden Sie auf der IETF-Seite
      <a target="_blank" href="https://tools.ietf.org/html/rfc2046">Request
        for Comment (RFC) 2046![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")</a> sowie unter der Adresse <a target="_blank" href="http://www.iana.org/assignments/media-types/audio/basic">iana.org/assignments/media-types/audio/basic.![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")</a>
    </td>
  </tr>
  <tr>
    <td>
      <code>audio/flac</code>
    </td>
    <td>
      <em>Free Lossless Audio Codec (FLAC)</em> ist ein
      verlustfreies komprimiertes Audiocodierungsformat
      (Dateierweiterung <code>.flac</code>). Weitere Informationen finden Sie unter der Adresse <a target="_blank" href="https://en.wikipedia.org/wiki/FLAC">en.wikipedia.org/wiki/FLAC.![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")</a>
    </td>
  </tr>
  <tr>
    <td>
      <code>audio/l16;rate={rate}</code>
    </td>
    <td>
      Die <em>lineare 16-Bit-PCM (Pulse-Code Modulation)</em> ist ein
unkomprimiertes Audiodatenformat (häufig mit der Dateierweiterung
<code>.raw</code> oder <code>.pcm</code>). Weitere Informationen finden Sie auf der von der Internet Engineering Task Force (IETF) betriebenen Seite       <a target="_blank" href="https://tools.ietf.org/html/rfc2586">Request for Comment (RFC) 2586![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")</a> sowie unter der Adresse <a target="_blank" href="https://en.wikipedia.org/wiki/Pulse-code_modulation">en.wikipedia.org/wiki/Pulse-code_modulation.![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")</a><br/><br/>
      Bei diesem Audioformat müssen Sie die Abtastfrequenz angeben. Geben Sie
beispielsweise <code>audio/l16;rate=16000</code> für eine Audioausgabe an, die
mit 16 kHz abgetastet wird. Optional können Sie die Endianess-Einstellung
entweder mit <code>audio/l16;rate={rate};endianness=big-endian</code> oder mit
      <code>audio/l16;rate={rate};endianness=little-endian</code> angeben.
      Standardeinstellung ist 'Little Endian'.
    </td>
  </tr>
  <tr>
    <td>
      <code>audio/mp3</code><br/>
      <code>audio/mpeg</code>
    </td>
    <td>
      <em>MP3</em> oder <em>Motion Picture Experts Group (MPEG)</em> ist ein
verlustbehaftetes Datenkomprimierungsformat (MP3 und MPEG bezeichnen dasselbe
Format). Weitere Informationen finden Sie unter der Adresse <a target="_blank" href="https://en.wikipedia.org/wiki/MP3">en.wikipedia.org/wiki/MP3.![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")</a>
    </td>
  </tr>
  <tr>
    <td>
      <code>audio/mulaw;rate={rate}</code>
    </td>
    <td>
      <em>8-Bit-Mu-Law-Audio (oder U-Law-Audio)</em> ist ein verlustbehaftetes
Einkanalaudioformat, das unter Verwendung von 8-Bit-U-Law-Daten (oder Mu-Law-Daten) codiert wird. 
Bei diesem Audioformat müssen Sie die Abtastfrequenz angeben. Weitere Informationen finden Sie unter der Adresse <a target="_blank" href="https://en.wikipedia.org/wiki/M-law_algorithm">en.wikipedia.org/wiki/M-law_algorithm.![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")</a>
    </td>
  </tr>
  <tr>
    <td>
      <code>audio/ogg</code><br/>
      <code>audio/ogg;codecs=opus</code><br/>
      <code>audio/ogg;codecs=vorbis</code>
    </td>
    <td>
      Das Format <em>Ogg</em> (<code>.ogg</code>) ist ein freigegebenes offenes
Containerformat, das von der Xiph.org Foundation verwaltet wird. Weitere Informationen finden Sie unter der Adresse <a target="_blank" href="https://www.xiph.org/ogg/">xiph.org/ogg/.![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")</a>
      Sie können Audiodatenströme anfordern, die mit den folgenden Codecs
komprimiert wurden:
      <ul style="margin-left:20px; padding:0px;">
        <li style="margin:10px 0px; line-height:120%;">
          <em>Opus</em>. Weitere Informationen finden Sie unter den Adressen <a target="_blank" href="https://www.opus-codec.org/">opus-codec.org![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")</a> und <a target="_blank" href="https://en.wikipedia.org/wiki/Opus">en.wikipedia.org/wiki/Opus (audio format).![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")</a>
          Lesen Sie auf der Seite <em>Opus (audio format)</em> insbesondere
den Abschnitt <em>Containers</em>.
</li>
        <li style="margin:10px 0px; line-height:120%;">
          <em>Vorbis</em>. Weitere Informationen finden Sie unter den Adressen <a target="_blank" href="https://xiph.org/vorbis/">xiph.org/vorbis![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")</a> und <a target="_blank" href="https://en.wikipedia.org/wiki/Vorbis">en.wikipedia.org/wiki/Vorbis.![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")</a>
        </li>
      </ul>
      Beide Codecs sind freigegebene offene Audiokomprimierungsformate mit Verlusten. Opus ist der bevorzugte Codec, aber gemäß der Ogg-Spezifikation gibt der Service die Audioausgabe im Vorbis-Format zurück, falls Sie den Codec nicht angeben. Wenn Sie das Audioformat gänzlich weglassen, gibt der Service die Audioausgabe standardmäßig im Format 'Ogg' mit Opus-Codec zurück.</td>
  </tr>
  <tr>
    <td>
      <code>audio/wav</code>
    </td>
    <td>
      <em>Waveform Audio File Format (WAV)</em> ist ein
Standardcontainerformat, das häufig für unkomprimierte Audiobitdatenströme
verwendet wird, jedoch auch komprimierte Audiodaten enthalten kann
(die Dateierweiterung lautet <code>.wav</code>). Da es sich bei den
zurückgegebenen Audiodaten um einen Datenstrom handelt, funktioniert die
generierte WAV-Datei möglicherweise nicht bei allen Audiowiedergabegeräten. Speziell
ist das Attribut <code>numSamples</code> im Header der Datei ungeachtet der
Länge der Audioausgabe auf <code>0</code> gesetzt. Weitere Informationen finden Sie unter der Adresse <a target="_blank" href="https://en.wikipedia.org/wiki/WAV">en.wikipedia.org/wiki/WAV.![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")</a>
    </td>
  </tr>
  <tr>
    <td>
      <code>audio/webm</code><br/>
      <code>audio/webm;codecs=opus</code><br/>
      <code>audio/webm;codecs=vorbis</code>
    </td>
    <td>
      <em>Web Media (WebM)</em> ist ein offenes Mediendateiformat
(Dateierweiterung <code>.webm</code>), das Unterstützung für Audiodatenströme
bereitstellt, die mit den Audio-Codecs 'Opus' und 'Vorbis' komprimiert wurden.
Wenn Sie den Codec nicht angeben, gibt der Service die Audioausgabe in Opus-Format
zurück. Weitere Informationen finden Sie unter der Adresse <a target="_blank" href="https://www.webmproject.org/">webmproject.org.![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")</a>
    </td>
  </tr>
</table>

## Audioformat angeben
{: #formatSpecify}

Die Angabe eines Audioformats ist optional. Standardmäßig gibt der Service die Audioausgabe im Format `audio/ogg;codecs=opus` zurück. Sie können jedoch ein Format für die HTTP- oder WebSocket-Schnittstelle angeben:

-   Bei den HTTP-Methoden `GET` und `POST /v1/synthesize` geben Sie ein Format mithilfe des Anforderungsheaders `Accept` oder des Abfrageparameters `accept` an. Wenn Sie die Audioausgabe im Standardformat erhalten wollen, lassen Sie sowohl den Header als auch den Abfrageparameter weg. Weitere Informationen enthält der Abschnitt [Audioausgabe synthetisch aus Text erstellen](/docs/services/text-to-speech/http.html#synthesize).

    Wenn Sie den Abfrageparameter `accept` verwenden, codieren Sie das Argument für den Parameter als URL. Codieren Sie beispielsweise das Argument

    ```
    audio/l16;rate=16000;endianness=little-endian
    ```
    {: codeblock}

    wie folgt als URL:

    ```
    audio%2Fl16%3Brate%3D16000%3Bendianness%3Dlittle-endian
    ```
    {: codeblock}

-   Bei der WebSocket-Schnittstelle geben Sie ein Format mithilfe des Parameters `accept` der Textnachricht an, die Sie zur Initialisierung der Synthese übergeben. Um die Audioausgabe im Standardformat zu erhalten, geben Sie den Wert `*/*` für den Parameter an. Weitere Informationen finden Sie im Abschnitt [Eingabetext senden](/docs/services/text-to-speech/websockets.html#WSsend).

## Abtastfrequenz angeben
{: #formatRate}

Der Service erstellt synthetisch Audioausgabe immer mit einer Abtastfrequenz von 22.050 Hz. Bei den meisten Audioformaten gibt der Service Audioausgabe mit dieser Standardabtastfrequenz zurück. Bei einigen Formaten können Sie mit dem Parameter `rate={rate}` eine andere Abtastfrequenz angeben. Bei den Formaten `audio/l16` und `audio/mulaw` *müssen* Sie eine Abtastfrequenz angeben.

Wenn Sie eine Abtastfrequenz angeben, wird die Audioausgabe vom Service erneut abgetastet und mit der angegebenen Frequenz zurückgegeben. Die angegebene Abtastfrequenz muss im Bereich zwischen 8 kHz und 192 kHz liegen.

Tabelle 2 zeigt die Standardabtastfrequenz der Audioausgabe, die für das jeweilige Format zurückgegeben wird; außerdem ist aufgeführt, bei welchen Formaten Sie eine Abtastfrequenz angeben können oder müssen.

<table style="width:90%">
  <caption>Tabelle 2. Abtastfrequenzen für Audioformate</caption>
  <tr>
    <th style="text-align:left">Audioformat</th>
    <th style="text-align:center">Standardabtastfrequenz</th>
    <th style="text-align:center">Verwendung des Parameters <code>rate</code></th>
  </tr>
  <tr>
    <td>
      <code>audio/basic</code>
    </td>
    <td style="text-align:center">
      8000 Hz
    </td>
    <td style="text-align:center">
      Nicht zulässig
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
      Optional
    </td>
  </tr>
  <tr>
    <td>
      <code>audio/l16;rate={rate}</code>
    </td>
    <td style="text-align:center">
      Keine
    </td>
    <td style="text-align:center">
      Erforderlich. Beispiel:<br />
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
      Optional
    </td>
  </tr>
  <tr>
    <td>
      <code>audio/mulaw;rate={rate}</code>
    </td>
    <td style="text-align:center">
      Keine
    </td>
    <td style="text-align:center">
      Erforderlich. Beispiel:<br />
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
      Optional
    </td>
  </tr>
  <tr>
    <td>
      <code>audio/ogg;codecs=opus</code>
    </td>
    <td style="text-align:center">
      22.050 Hz [siehe <strong>Hinweis</strong>]
    </td>
    <td style="text-align:center">
      Optional
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
      Optional
    </td>
  </tr>
  <tr>
    <td>
      <code>audio/webm</code><br/>
      <code>audio/webm;codecs=opus</code>
    </td>
    <td style="text-align:center">
      48.000 Hz [siehe <strong>Hinweis</strong>]
    </td>
    <td style="text-align:center">
      Nicht zulässig
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
      Optional
    </td>
  </tr>
</table>

Die Abtastfrequenz für einen Audiodatenstrom, der vom Service zurückgegeben wird, kann am zuverlässigsten dadurch angegeben werden, dass die Informationen aus dem Datenstrom selbst extrahiert werden. Sie können die Frequenz bestimmen, indem Sie die Methode `/v1/synthesize` mit einem einfachen Text aufrufen (z. B. 'hello world') und das Format sowie den Codec angeben, die Sie verwenden wollen. Anschließend können Sie den Codec und die Abtastfrequenz abrufen, indem Sie den Audiodatenstrom in einer Datei speichern und in einem Audioplayer öffnen.

Beim Standard 'Opus' muss die Ausgabeabtastfrequenz unbedingt mit der Funktionalität des Audioplayers übereinstimmen. Weitere Informationen enthält Abschnitt 5.1 auf der von der Internet Engineering Task Force (IETF) betriebenen Seite [Request for Comments (RFC) 7845.![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](http://tools.ietf.org/html/rfc6455){: new_window} Für als Software bereitgestellte Audioplayer ist in der Tabelle die typische Ausgabeabtastfrequenz aufgeführt; die tatsächliche Abtastfrequenz der Audioausgabe variiert jedoch im Datenstrom von Zeit zu Zeit. Wie bereits erläutert, erstellt der Service die Audioausgabe aus der Quelle mit 22.050 Hz.
{: note}

## Audiodatei wiedergeben
{: #formatsPlay}

Verwenden Sie zur Wiedergabe einer durch den Service generierten Audiodatei eines der folgenden Tools:

-   Web-Browser wie beispielsweise Google Chrome&trade;, Firefox&reg; oder Microsoft&reg; Internet Explorer&reg;
-   Audioplayer wie beispielsweise Audacity&reg; ([audacityteam.org ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](http://www.audacityteam.org/){: new_window}) oder FFmpeg ([ffmpeg.org ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://www.ffmpeg.org){: new_window}).
