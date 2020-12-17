---

copyright:
  years: 2015, 2020
lastupdated: "2020-12-16"

subcollection: text-to-speech

---

{:shortdesc: .shortdesc}
{:external: target="_blank" .external}
{:tip: .tip}
{:important: .important}
{:note: .note}
{:beta: .beta}
{:deprecated: .deprecated}
{:pre: .pre}
{:codeblock: .codeblock}
{:screen: .screen}
{:javascript: .ph data-hd-programlang='javascript'}
{:java: .ph data-hd-programlang='java'}
{:python: .ph data-hd-programlang='python'}
{:swift: .ph data-hd-programlang='swift'}

# Service features
{: #service-features}

You can access the speech synthesis capabilities of the {{site.data.keyword.texttospeechfull}} service via an HTTP or WebSocket interface. Both interfaces provide features that let you submit and receive different information from the service. And as with all {{site.data.keyword.watson}} services, SDKs are available to simplify application development in many programming languages.
{: shortdesc}

## Synthesizing speech with the service
{: #features-synthesis-interfaces}

The {{site.data.keyword.texttospeechshort}} service offers an HTTP Representational State Transfer (REST) interface and a WebSocket interface:

-   [The HTTP interface](/docs/text-to-speech?topic=text-to-speech-usingHTTP) provides both `GET` and `POST` versions of the service's `/v1/synthesize` method. The two versions of the method offer generally equivalent functionality. You pass the text that is to be synthesized as a query parameter with the `GET` method and as the body of the request with the `POST` method.
-   [The WebSocket interface](/docs/text-to-speech?topic=text-to-speech-usingWebSocket) provides a `/v1/synthesize` method. You pass the text that is to be synthesized over an established WebSocket connection.

With both the HTTP and WebSocket interfaces, you specify the language and voice that are to be used, and the format for the audio that is to be returned.

-   For an overview of the features that are available for speech synthesis, see [Using speech synthesis features](#features-synthesis).
-   For detailed descriptions and examples of the speech synthesis methods, see the [API & SDK reference](https://{DomainName}/apidocs/text-to-speech){: external}.

### Data limits
{: #features-data-limits}

The interfaces accept the following maximum amounts of text with a single request:

-   The HTTP `GET /v1/synthesize` method accepts a maximum of 8 KB of input, which includes the input text and the URL and headers.
-   The HTTP `POST /v1/synthesize` method accepts a maximum of 8 KB for the URL and headers, and a maximum of 5 KB for the input text that is sent in the body of the request.
-   The WebSocket `/v1/synthesize` method accepts a maximum of 5 KB of input text.

These limits include all characters of the input, including whitespace.

For billing purposes, whitespace characters are not counted. However, all other characters are counted, including those that are part of SSML elements.
{: note}

### Language and audio support
{: #features-languages-formats}

The service supports speech synthesis for many languages and audio formats.

-   For information about the supported languages, see [Language support](/docs/text-to-speech?topic=text-to-speech-about#about-languages).
-   For information about the supported audio formats, see [Audio formats](/docs/text-to-speech?topic=text-to-speech-about#about-formats).

## Using speech synthesis features
{: #features-synthesis}

The service supports additional features that you can use to tailor the text that you send and the audio that you receive.

### SSML
{: #features-ssml}

You can pass the service plain text or text that is annotated with the Speech Synthesis Markup Language (SSML). SSML is an XML-based markup language that provides annotations of text for speech synthesis applications such as the {{site.data.keyword.texttospeechshort}} service.

-   For more information about specifying input text, see [Specifying input text](/docs/text-to-speech?topic=text-to-speech-usingHTTP#input).
-   For more information about using SSML, see [Using SSML](/docs/text-to-speech?topic=text-to-speech-ssml).

### Word timings
{: #features-timings}

With the WebSocket interface, you can obtain timing information about the location of words in the audio that the service returns. Timing information is useful for synchronizing the input text and the audio.

You can use the SSML `<mark>` element to identify specific locations, such as word boundaries, in the audio. For languages other than Japanese, you can also request word timing information for all words of the input text. For more information, see [Obtaining word timings](/docs/text-to-speech?topic=text-to-speech-timing).

## Customizing the service
{: #features-customization}

The service includes a customization interface that you can use to create custom models for use during speech synthesis. A custom model is a dictionary of words and their translations for a specific language. Each word/translation pair in a model tells the service how to pronounce a word when it occurs in input text.

You can use custom models to create application-specific translations for unusual words for which the service's regular pronunciation rules might yield imperfect pronunciations. For example, your application might routinely encounter domain-specific terms, special terms with foreign origins, personal or geographic names, or abbreviations and acronyms. By using customization, you can define translations that tell the service how you want such terms to be pronounced.

You can define the custom entry for a word/translation pair based on other words, or you can create pronunciations based on phoneme symbols in the standard International Phonetic Alphabet (IPA) or the proprietary {{site.data.keyword.IBM_notm}} Symbolic Phonetic Representation (SPR). Customization is available for all languages. You must have the Standard or Premium pricing plan to use customization. Users of the Lite plan cannot use the customization interface.

-   For more information about customization, see [Understanding customization](/docs/text-to-speech?topic=text-to-speech-customIntro).
-   For more information about pricing plans, see the {{site.data.keyword.texttospeechshort}} service in the [{{site.data.keyword.cloud}} Catalog](https://{DomainName}/catalog/text-to-speech){: external}.

Premium customers can work with {{site.data.keyword.IBM_notm}} to train a new custom voice for their specific use case and target market. {{site.data.keyword.IBM_notm}} can train a new voice with as little as one hour of training data. For more information, contact your {{site.data.keyword.IBM_notm}} Sales Representative.
{: note}
## Understanding data security
{: #features-data-security}

The {{site.data.keyword.texttospeechshort}} service provides security for all user data both in motion and at rest:

-   Transport Layer Security (TLS) 1.2 is used to secure data in transit.
-   Advanced Encryption Standard (AES)-256 with Secure Hash Algorithm (SHA)-256 is used to secure data at rest.

For more information about data security for cloud applications, see [Security architecture for cloud applications](https://www.ibm.com/cloud/architecture/architectures/securityArchitecture/security-for-data){: external}.

The service offers Standard and Premium pricing plans for its users:

-   Standard plans are multi-tenant solutions that provide logical separation of data by using common encryption keys.
-   Premium plans are single-tenant solutions that provide physical separation of data. Premium plans provide dedicated data storage accounts that use unique encryption keys.

Users of Premium plans can also integrate with {{site.data.keyword.keymanagementservicefull}} to create, import, and manage their encryption keys. This process is commonly referred to as *Bring your own keys* (BYOK). For more information about using {{site.data.keyword.keymanagementserviceshort}}, see [Protecting sensitive information in your Watson service](/docs/watson?topic=watson-keyservice).

And finally, the service supports the European Union General Data Protection Regulation (GDPR) to mange user data. For Premium plans, it also offers US Health Insurance Portability and Accountability Act (HIPAA) readiness. For more information, see [Information security](/docs/text-to-speech?topic=text-to-speech-information-security).

## Leveraging CORS support
{: #features-cors}

The service supports Cross-Origin Resource Sharing (CORS). By using CORS, web pages can request resources directly from a foreign domain. CORS circumvents the same-origin security policy, which otherwise prevents such requests. Because the service supports CORS, a web page can communicate directly with the service without passing the request through the web server that hosts the page.

For instance, a web page that is loaded from a server in {{site.data.keyword.cloud}} can call the customization API directly, bypassing the {{site.data.keyword.cloud_notm}} server. For more information, see [enable-cors.org](https://enable-cors.org/){: external}.

## Learning more about application development
{: #features-learn}

For more information about working with {{site.data.keyword.watson}} services and {{site.data.keyword.cloud_notm}}:

-   For an introduction, see [Getting started with {{site.data.keyword.watson}} and {{site.data.keyword.cloud_notm}}](/docs/watson?topic=watson-about).
-   For information about using {{site.data.keyword.cloud_notm}} Identity and Access Management, see [Authenticating to {{site.data.keyword.watson}} services](/docs/watson?topic=watson-iam).
-   For information about controlling the default request logging that is performed for all {{site.data.keyword.watson}} services, see [Controlling request logging for {{site.data.keyword.watson}} services](/docs/watson?topic=watson-gs-logging-overview).

SDKs are available for the {{site.data.keyword.texttospeechshort}} service to simplify the development of speech applications. The SDKs support many popular programming languages and platforms.

-   For a complete list of SDKs and links to the SDKs on GitHub, see [{{site.data.keyword.watson}} SDKs](/docs/text-to-speech?topic=watson-using-sdks).
-   For more information about all methods of the SDKs for the {{site.data.keyword.texttospeechshort}} service, see the [API & SDK reference](https://{DomainName}/apidocs/text-to-speech){: external}.
