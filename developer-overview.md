---

copyright:
  years: 2015, 2018
lastupdated: "2018-12-12"

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

# Overview for developers
{: #overview}

You can access the speech synthesis capabilities of the {{site.data.keyword.texttospeechshort}} service via an HTTP Representational State Transfer (REST) API or a WebSocket interface. Several Software Development Kits (SDKs) are also available to simplify application development in various programming languages. The following sections provide an overview of application development with the service.
{: shortdesc}

## HTTP interface
{: #http}

To synthesize text with the HTTP REST API, you call the `GET` or `POST` version of the service's `/v1/synthesize` method. The two versions of the method offer generally equivalent functionality:

-   *Input text:* The `GET /v1/synthesize` method accepts the text to be synthesized via a query parameter. The `POST /v1/synthesize` method accepts the text in the body of the request. Both methods impose a size limit of 5 KB on the text to be synthesized.

    You can pass the service plain text or text that is annotated with the Speech Synthesis Markup Language (SSML). SSML is an XML-based markup language that provides annotations of text for speech synthesis applications such as the {{site.data.keyword.texttospeechshort}} service. The service augments SSML with service-specific expressive and voice-transformation elements.
-   *Voices:* The service accepts text and produces audio in various languages, voices, and dialects. The service offers at least one male or female voice, sometimes both, for each supported language and different dialects such as US and British English. You can use the service's `GET /v1/voices` or `GET /v1/voices/{voice}` methods to learn more about the supported voices. The service synthesizes the text into the language of the specified voice; be sure to match the voice to the input text.
-   *Audio formats:* The service can produce audio in the following formats: Ogg or Web Media (WebM) format with the Opus (default) or Vorbis codec, MP3 (Motion Picture Experts Group, or MPEG) format, Waveform Audio File Format (WAV), Free Lossless Audio Codec (FLAC), Linear 16-bit Pulse-Code Modulation (PCM), 8-bit mu-law (u-law), or basic audio.

For more information, see [The HTTP REST interface](/docs/services/text-to-speech/http.html).

## WebSocket interface
{: #websocket}

The service offers a WebSocket interface that you can use to synthesize text. The interface provides a single version of the `/v1/synthesize` method that accepts a maximum of 5 KB of text. You specify the text to be synthesized, the voice to be used, and the format for the audio. You can provide plain text or text that is annotated with SSML. For more information, see [The WebSocket interface](/docs/services/text-to-speech/websockets.html).

The WebSocket interface supports use of the SSML `<mark>` element to identify specific locations in audio. You can also request word timing information for all words of the input text. For more information, see [Obtaining word timings](/docs/services/text-to-speech/word-timing.html).

## Customization interface
{: #customization}

The service includes a customization interface that you can use to create custom voice models for use during speech synthesis. A custom voice model is a dictionary of words and their translations for a specific language. Each word/translation pair in a model tells the service how to pronounce the word when it occurs in input text.

You can use custom voice models to create application-specific translations for unusual words for which the service's regular pronunciation rules might yield imperfect pronunciations. You can define the custom entry for a word/translation pair in the standard International Phonetic Alphabet (IPA) representation or in the proprietary {{site.data.keyword.IBM_notm}} Symbolic Phonetic Representation (SPR).

For example, your application might routinely encounter special terms with foreign origins, personal or geographic names, or abbreviations and acronyms. By using customization, you can define translations that tell the service how you want such terms to be pronounced. For more information, see [Understanding customization](/docs/services/text-to-speech/custom-intro.html).

The customization interface is a beta release.
{: note}

## CORS support
{: #cors}

The service supports Cross-Origin Resource Sharing (CORS). By using CORS, web pages can request resources directly from a foreign domain. CORS circumvents the same-origin security policy, which otherwise prevents such requests. Because the service supports CORS, a web page can communicate directly with the service without passing the request through the web server that hosts the page.

For instance, a web page that is loaded from a server in {{site.data.keyword.cloud}} can call the customization API directly, bypassing the {{site.data.keyword.cloud_notm}} server. For more information, see [enable-cors.org ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://enable-cors.org/){: new_window}.

## Using Software Development Kits
{: #sdks}

SDKs are available for the {{site.data.keyword.texttospeechshort}} service to simplify the development of speech applications. {{site.data.keyword.ibmwatson}} SDKs are available for many popular programming languages and platforms.

-   For a complete list of SDKs and links to the SDKs on GitHub, see [Using SDKs](/docs/services/watson/getting-started-sdks.html).
-   For detailed information about all methods of the Node, Java, Python, and Ruby SDKs for the {{site.data.keyword.texttospeechshort}} service, see the [API reference ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://{DomainName}/apidocs/text-to-speech){: new_window}.

## Learning more about application development
{: #learn}

For more information about working with {{site.data.keyword.watson}} services and {{site.data.keyword.cloud_notm}}, see

-   For an introduction to working with {{site.data.keyword.watson}} services and {{site.data.keyword.cloud_notm}}, see [Getting started with {{site.data.keyword.watson}} and {{site.data.keyword.cloud_notm}}](/docs/services/watson/index.html).
-   All new service instances use {{site.data.keyword.cloud_notm}} Identity and Access Management (IAM) for authentication. Older service instances might continue to use the `{username}` and `{password}` from their existing Cloud Foundry service credentials for authentication. For more information about authenticating to the service, see the [30 October 2018 service update](/docs/services/text-to-speech/release-notes.html#October2018) in the release notes.
-   For information about controlling the default request logging that is performed for all {{site.data.keyword.watson}} services, see [Controlling request logging for {{site.data.keyword.watson}} services](/docs/services/watson/getting-started-logging.html).
