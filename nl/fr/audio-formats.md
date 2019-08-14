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

# Formats audio
{: #audioFormats}

Le service {{site.data.keyword.texttospeechfull}} peut renvoyer de l'audio synthétisé dans un certain nombre de formats. Pour la plupart des formats, le service renvoie l'audio avec une fréquence d'échantillonnage par défaut de 22 050 Hz. Pour certains formats, vous pouvez ou devez spécifier la fréquence d'échantillonnage de l'audio. Le service renvoie toujours l'audio sur un canal unique pour tous les formats.
{: shortdesc}

## Formats audio pris en charge
{: #formatsSupported}

Le tableau 1 répertorie les formats audio (types MIME) dans lesquels vous pouvez demander un son synthétisé. Par défaut, le service renvoie l'audio au format Ogg avec le codec Opus (`audio/ogg;codecs=opus`).

<table>
  <caption>Tableau 1. Formats audio pris en charge</caption>
  <tr>
    <th style="text-align:left; width:25%">Format audio</th>
    <th style="text-align:left">Description</th>
  </tr>
  <tr>
    <td>
      <code>audio/basic</code>
    </td>
    <td>
      <em>Audio de base</em>, format audio monocanal avec pertes, codé à l'aide de données u-law (ou mu-law) sur 8 bits, échantillonnées à 8 kHz.
      Ce format fournit un type de support avec le plus petit dénominateur commun. Pour plus d'informations, voir [ Request for Comments: 2046](https://tools.ietf.org/html/rfc2046) et [iana.org/assignments/media-types/audio/basic](http://www.iana.org/assignments/media-types/audio/basic).
    </td>
  </tr>
  <tr>
    <td>
      <code>audio/flac</code>
    </td>
    <td>
      <em>Free Lossless Audio Codec (FLAC)</em> (<code>.flac</code>),
       format de codage audio compressé sans perte. Pour plus d'informations, voir [FLAC](https://wikipedia.org/wiki/FLAC).
    </td>
  </tr>
  <tr>
    <td>
      <code>audio/l16;rate={rate}</code>
    </td>
    <td>
      <em>Modulation linéaire 16 bits par impulsions et codage (PCM),</em> format de données audio non compressé (souvent <code>.raw</code> ou <code>.pcm</code>). Pour plus d'informations, voir [Request for Comments: 2586](https://tools.ietf.org/html/rfc2586), norme IETF (Internet Engineering Task Force) et [Pulse-code modulation](https://wikipedia.org/wiki/Pulse-code_modulation).<br/><br/>
      Vous devez spécifier la fréquence d'échantillonnage avec ce format audio. Par exemple, spécifiez <code>audio/l16;rate=16000</code> pour l'audio échantillonné à 16 kHz. Vous pouvez également éventuellement définir l'ordre d'octets sous la forme
      <code>audio/l16;rate={rate};endianness=big-endian</code> ou
      <code>audio/l16;rate={rate};endianness=little-endian</code>.
      La valeur est little endian.
    </td>
  </tr>
  <tr>
    <td>
      <code>audio/mp3</code><br/>
      <code>audio/mpeg</code>
    </td>
    <td>
      <em>MP3</em> ou <em>Motion Picture Experts Group (MPEG)</em>, un format de compression de données avec perte (MP3 et MPEG désignent le même format).
      Pour plus d'informations, voir [MP3](https://wikipedia.org/wiki/MP3).
    </td>
  </tr>
  <tr>
    <td>
      <code>audio/mulaw;rate={rate}</code>
    </td>
    <td>
      <em>Audio mu-law (ou u-law) 8 bits</em>, format audio monocanal avec perte, codé à l’aide de données u-law (ou mu-law) sur 8 bits. Vous devez spécifier la fréquence d'échantillonnage avec ce format audio. Pour plus d'informations, voir [M-law algorithm](https://wikipedia.org/wiki/M-law_algorithm).
    </td>
  </tr>
  <tr>
    <td>
      <code>audio/ogg</code><br/>
      <code>audio/ogg;codecs=opus</code><br/>
      <code>audio/ogg;codecs=vorbis</code>
    </td>
    <td>
      <em>Format ogg</em> (<code>.ogg</code>), format de conteneur libre et ouvert géré par Xiph.org Foundation. Pour plus d'informations, voir [xiph.org/ogg/](https://www.xiph.org/ogg/).
      Vous pouvez demander des flux audio compressés avec les codecs suivants :
      <ul style="margin-left:20px; padding:0px;">
        <li style="margin:10px 0px; line-height:120%;">
          <em>Opus</em>. Pour plus d'informations, voir [opus-codec.org](https://www.opus-codec.org/) et [Opus (audio format)](https://wikipedia.org/wiki/Opus_%28audio_format%29). Intéressez-vous particulièrement à la section <em>Containers</em>.
        </li>
        <li style="margin:10px 0px; line-height:120%;">
          <em>Vorbis</em>. Pour plus d'informations, voir [xiph.org/vorbis](https://xiph.org/vorbis/) et [Vorbis](https://wikipedia.org/wiki/Vorbis).
        </li>
      </ul>
      Les deux codecs sont des formats de compression audio gratuits, ouverts et avec pertes. Opus est le codec préféré, mais selon la spécification Ogg, le service renvoie l'audio au format Vorbis si vous omettez le codec. Si vous omettez complètement un format audio, le service renvoie l'audio au format Ogg avec le codec Opus par défaut.
    </td>
  </tr>
  <tr>
    <td>
      <code>audio/wav</code>
    </td>
    <td>
      <em>Waveform Audio File Format (WAV)</em> (<code>.wav</code>) est un format de conteneur standard qui est souvent utilisé pour les flots de bits audio non compressés, mais peut également contenir de l’audio compressé. En raison de la nature en continu de l'audio renvoyé, le fichier WAV généré peut ne pas fonctionner sur tous les lecteurs audio. Spécifiquement, l'attribut <code>numSamples</code> dans l'en-tête du fichier est défini sur <code>0</code> quelle que soit la longueur de l'audio.
      Pour plus d'informations, voir [WAV](https://wikipedia.org/wiki/WAV).
    </td>
  </tr>
  <tr>
    <td>
      <code>audio/webm</code><br/>
      <code>audio/webm;codecs=opus</code><br/>
      <code>audio/webm;codecs=vorbis</code>
    </td>
    <td>
      <em>Web Media (WebM)</em> (<code>.webm</code>), format de fichier multimédia ouvert prenant en charge les flux audio compressés avec les codecs audio Opus et Vorbis. Si vous omettez le codec, le service renvoie l'audio au format Opus. Pour plus d'informations, voir [webmproject.org](https://www.webmproject.org/).
    </td>
  </tr>
</table>

## Spécification d'un format audio
{: #formatSpecify}

La spécification d'un format audio est facultative. Par défaut, le service renvoie l'audio au format `audio/ogg;codecs=opus`. Mais vous pouvez spécifier un format pour l'interface HTTP ou WebSocket :

-   Avec les méthodes HTTP `GET` et `POST /v1/synthesize`, vous spécifiez un format à l'aide de l'en-tête de requête `Accept` ou du paramètre de requête `accept`. Pour recevoir de l'audio au format par défaut, omettez à la fois l'en-tête et le paramètre de requête. Pour plus d'informations, voir [Synthèse de texte en audio](/docs/services/text-to-speech?topic=text-to-speech-usingHTTP#synthesize).

    Si vous utilisez le paramètre de requête `accept`, codez dans l'URL l'argument associé au paramètre. Par exemple, codez dans l'URL l'argument suivant

    ```
    audio/l16;rate=16000;endianness=little-endian
    ```
    {: codeblock}

    en tant que

    ```
    audio%2Fl16%3Brate%3D16000%3Bendianness%3Dlittle-endian
    ```
    {: codeblock}

-   Si vous utilisez l'interface WebSocket, vous spécifiez un format à l'aide du paramètre `accept` du message texte que vous transmettez pour lancer la synthèse. Pour recevoir de l'audio au format par défaut, spécifiez la valeur `*/*` pour le paramètre. Pour plus d'informations, voir [Envoi d'un texte en entrée](/docs/services/text-to-speech?topic=text-to-speech-usingWebSocket#WSsend).

## Spécification d'une fréquence d'échantillonnage
{: #formatRate}

Le service synthétise toujours l'audio avec une fréquence d'échantillonnage de 22 050 Hz. Pour la plupart des formats audio, le service renvoie l'audio avec cette fréquence d'échantillonnage par défaut. Pour certains formats, vous pouvez spécifier une fréquence d'échantillonnage différente en incluant le paramètre `rate={rate}`. Pour les formats `audio/l16` et `audio/mulaw`, vous *devez* spécifier une fréquence d'échantillonnage.

Lorsque vous spécifiez une fréquence d'échantillonnage, le service ré-échantillonne l'audio et le renvoie à la fréquence spécifiée. Une fréquence d'échantillonnage spécifiée doit être comprise entre 8 kHz et 192 kHz.

Le tableau 2 indique la fréquence d'échantillonnage par défaut de l'audio renvoyé pour chaque format et indique les formats pour lesquels vous pouvez ou devez spécifier une fréquence d'échantillonnage.

<table style="width:90%">
  <caption>Tableau 2. Fréquences d'échantillonnage pour les formats audio</caption>
  <tr>
    <th style="text-align:left">Format audio</th>
    <th style="text-align:center">Fréquence d'échantillonnage par défaut</th>
    <th style="text-align:center">Utilisation du paramètre <code>rate</code></th>
  </tr>
  <tr>
    <td>
      <code>audio/basic</code>
    </td>
    <td style="text-align:center">
      8000 Hz
    </td>
    <td style="text-align:center">
      Non autorisé
    </td>
  </tr>
  <tr>
    <td>
      <code>audio/flac</code>
    </td>
    <td style="text-align:center">
      22 050 Hz
    </td>
    <td style="text-align:center">
      Facultatif
    </td>
  </tr>
  <tr>
    <td>
      <code>audio/l16;rate={rate}</code>
    </td>
    <td style="text-align:center">
      Néant
    </td>
    <td style="text-align:center">
      Obligatoire ; par exemple<br />
      <code>audio/l16;rate=22050</code>
    </td>
  </tr>
  <tr>
    <td>
      <code>audio/mp3</code><br/>
      <code>audio/mpeg</code>
    </td>
    <td style="text-align:center">
      22 050 Hz
    </td>
    <td style="text-align:center">
      Facultatif
    </td>
  </tr>
  <tr>
    <td>
      <code>audio/mulaw;rate={rate}</code>
    </td>
    <td style="text-align:center">
      Néant
    </td>
    <td style="text-align:center">
      Obligatoire ; par exemple<br />
      <code>audio/mulaw;rate=8000</code>
    </td>
  </tr>
  <tr>
    <td>
      <code>audio/ogg</code><br/>
      <code>audio/ogg;codecs=vorbis</code>
    </td>
    <td style="text-align:center">
      22 050 Hz
    </td>
    <td style="text-align:center">
      Facultatif
    </td>
  </tr>
  <tr>
    <td>
      <code>audio/ogg;codecs=opus</code>
    </td>
    <td style="text-align:center">
      22 050 Hz [voir <strong>Remarque</strong>]
    </td>
    <td style="text-align:center">
      Facultatif
    </td>
  </tr>
  <tr>
    <td>
      <code>audio/wav</code>
    </td>
    <td style="text-align:center">
      22 050 Hz
    </td>
    <td style="text-align:center">
      Facultatif
    </td>
  </tr>
  <tr>
    <td>
      <code>audio/webm</code><br/>
      <code>audio/webm;codecs=opus</code>
    </td>
    <td style="text-align:center">
      48 000 Hz [voir <strong>Remarque</strong>]
    </td>
    <td style="text-align:center">
      Non autorisé
    </td>
  </tr>
  <tr>
    <td>
      <code>audio/webm;codecs=vorbis</code>
    </td>
    <td style="text-align:center">
      22 050 Hz
    </td>
    <td style="text-align:center">
      Facultatif
    </td>
  </tr>
</table>

Le moyen le plus fiable d'identifier la fréquence d'échantillonnage de tout flux audio renvoyé par le service consiste à extraire les informations du flux lui-même. Vous pouvez déterminer la fréquence en appelant la méthode `/v1/synthesize` avec un texte simple (par exemple, "hello world") et en spécifiant le format et le codec que vous prévoyez d'utiliser. Vous pouvez alors obtenir le codec et la fréquence d'échantillonnage en enregistrant le flux audio dans un fichier et en l'ouvrant dans un lecteur audio.

La norme Opus exige que la fréquence d’échantillonnage de sortie corresponde aux capacités du lecteur audio. Pour plus d'informations, voir la section 5.1 de [Request for Comments: 6455](http://tools.ietf.org/html/rfc6455){: external}, norme IETF (Internet Engineering Task Force). Pour les lecteurs audio logiciels, le tableau indique la fréquence d'échantillonnage de sortie type, mais la fréquence d'échantillonnage réelle de l'audio varie avec le temps dans le flux. Comme mentionné, le service synthétise l'audio source à 22 050 Hz.
{: note}

## Lecture d'un fichier audio
{: #formatsPlay}

Pour lire un fichier audio généré par le service, utilisez l'un des outils suivants :

-   Un navigateur Web tel que Google Chrome&trade;, Firefox&reg; ou Microsoft&reg; Internet Explorer&reg;.
-   Un lecteur audio tel qu'Audacity&reg; ([audacityteam.org](http://www.audacityteam.org/){: external}) ou FFmpeg ([ffmpeg.org](https://www.ffmpeg.org){: external}).
