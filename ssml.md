---

copyright:
  years: 2015, 2023
lastupdated: "2023-03-30"

subcollection: text-to-speech

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}

# Understanding SSML
{: #ssml}

The Speech Synthesis Markup Language (SSML) is an XML-based markup language that provides annotations of text for speech-synthesis applications. It is a recommendation of the W3C Voice-Browser Working Group that has been adopted as the standard markup language for speech synthesis by the VoiceXML 2.0 specification. SSML provides developers of speech applications with a standard way to control aspects of the synthesis process by enabling them to specify pronunciation, volume, pitch, speed, and other attributes via markup. You can use SSML to control the synthesis of your text with all supported languages.
{: shortdesc}

The {{site.data.keyword.texttospeechfull}} service bases its support on SSML version 1.1, which was recommended by W3C on 7 September 2010. For more information about the W3C SSML recommendation, see [W3C Speech Synthesis Markup Language (SSML) Version 1.1](http://www.w3.org/TR/speech-synthesis/){: external}.

## Introduction to SSML
{: #introduction-SSML}
{: help}
{: support}

SSML operates by augmenting the plain text that is passed to a synthesizer with a predefined set of elements, or tags. An XML parser first separates the plain input text from the markup specifications. The specifications are then processed and sent as a set of instructions in a form that can be understood by the synthesizer to produce the desired effects. For the XML parser to carry out this job, the markup needs to be well formed; for example, elements must be closed and multiple elements must be properly nested. For an introduction to basic XML concepts, see [w3schools.com/xml/xml_whatis.asp](http://www.w3schools.com/xml/xml_whatis.asp){: external}.

An SSML element is anything contained within, and including, an opening tag and its matching closing tag. As shown in the following example, an element can contain a combination of other elements (tags can be nested) and text. Additionally, elements can require or optionally accept attributes set to particular values.

```xml
<tag1>
  <tag2 attributeName="attributeValue">
    ... some text ...
  </tag2>
</tag1>
```
{: codeblock}

A full legal SSML document consists of an XML prolog, which contains information such as encoding and the schema against which to validate the SSML document, followed by the root element, `<speak>`. Within the span of the `<speak>` element, you specify the text that is to be synthesized, augmented with additional elements.

```xml
<!-- The XML Prolog -->
<?xml version="1.0" encoding="UTF-8"?>

<!-- Root Element -->
<speak version="1.1">
  ... the body that contains text to be synthesized plus markup ...
</speak>
```
{: codeblock}

The XML prolog is not needed for text that you pass to the service. The service supports SSML fragments, which are SSML elements that do not include the full XML header and do not need to include their parent elements. For example, the `<?xml>` and `<speak>` elements are always optional for SSML that you send for synthesis.
{: note}

## SSML support
{: #ssmlSupport}
{: troubleshoot}
{: support}

For more information about using SSML and related features with the service, see the following:

-   The service implements most of the W3C specification and supports SSML fragments.
    -   For complete information about the service's level of support for all SSML elements, see [SSML elements](/docs/text-to-speech?topic=text-to-speech-elements).
    -   For examples of using SSML elements with the `text` of a speech synthesis request, see [Examples of input text](/docs/text-to-speech?topic=text-to-speech-usingHTTP#httpExamples).
-   The service supports additional synthesis features for enhanced neural and expressive neural voices:
    -   [Modifying the speaking rate](/docs/text-to-speech?topic=text-to-speech-synthesis-params#params-rate-percentage)
    -   [Modifying the speaking pitch](/docs/text-to-speech?topic=text-to-speech-synthesis-params#params-pitch-percentage)
-   The service supports additional synthesis features for expressive neural voices:
    -   [Using speaking styles](/docs/text-to-speech?topic=text-to-speech-synthesis-expressive#syntheses-expressive-styles)
    -   [Emphasizing interjections](/docs/text-to-speech?topic=text-to-speech-synthesis-expressive#syntheses-expressive-interjections)
    -   [Emphasizing words](/docs/text-to-speech?topic=text-to-speech-synthesis-expressive#emphasizing-words)
-   The service supports a synthesis feature that lets you control how alphanumeric strings are spelled out for German voices. For more information, see [Specifying how strings are spelled out](/docs/text-to-speech?topic=text-to-speech-synthesis-params#params-spell-out-mode).
-   The service supports the use of the SSML `<mark>` element with the WebSocket interface to obtain timing information for words of the resulting audio. The WebSocket interface also allows you to request information for all strings of the input text. For more information, see
    -   [Specifying an SSML mark](/docs/text-to-speech?topic=text-to-speech-timing#timing-mark)
    -   [Requesting word timings for all words](/docs/text-to-speech?topic=text-to-speech-timing#timing-request)
-   The service's customization interface supports the use of the SSML `<phoneme>` element to specify the phonetic spelling that it uses to pronounce a word. The phonetic spelling represents the sounds of a word, how those sounds are divided into syllables, and which syllables receive stress.
    -   For information about the customization interface, see [Understanding customization](/docs/text-to-speech?topic=text-to-speech-customIntro).
    -   For information about the valid symbols that you can use in an International Phonetic Alphabet (IPA) or the {{site.data.keyword.IBM_notm}} Symbolic Phonetic Representation (SPR) specification for any supported language, see [Understanding phonetic symbols](/docs/text-to-speech?topic=text-to-speech-symbols).

## SSML validation
{: #ssml-errors}
{: troubleshoot}
{: support}

The service validates all SSML elements that you submit in any content, either as input text for synthesis or as the definition of a word's translation for customization. The service cannot determine ahead of time whether text submitted for synthesis contains SSML elements. Therefore, it performs the same validation for all input text, regardless of whether it contains SSML.

### Validation of elements and attributes
{: #ssml-errors-rules}

The service performs the following validation of SSML elements and attributes:

-   *All SSML input must be correct and well formed.*
-   *The service silently ignores unsupported SSML elements.* The service synthesizes the text that is contained within the tags of an unsupported element; only the element is ignored.
-   *The service returns an HTTP 400 error code for invalid SSML elements or attributes.* When specifying SSML elements that require an attribute:
    -   You must specify the required attribute.
    -   You must specify a valid value for the required attribute.
    -   If you include additional invalid attributes or values, they are ignored.

    If the request fails, the error response includes a descriptive message. For example, suppose you specify the following input text, which includes the `<say-as>` element:

    ```text
    "text": "The price is <say-as interpret-as=\"currency\">$2,500.00</say-as>."
    ```
    {: codeblock}

    In this example, the `interpret-as` attribute is required and is specified, but its value is invalid. A valid value for the attribute is `vxml:currency`, not `currency`. The error response includes the following message:

    ```text
    The connection to the Watson Text to Speech service closed with the following error: Tag <say-as> has invalid attribute interpret-as=currency
    ```
    {: codeblock}

### Summary of SSML errors
{: #ssml-errors-summary}

Table 1 describes many common SSML validation errors. In each case, the request fails and the service returns a 400 error code.

| Validation error | Description of problem |
|------------------|------------------------|
| Invalid SSML element | For example, you specify a tag incorrectly, omit a required attribute, or include an opening tag but no matching closing tag. |
| Unescaped XML control characters | The input text itself contains a `"`, `'`, `&`, `<`, `>`, or `/` character instead of its equivalent escape string or character encoding. For more information, see [Escaping XML control characters](/docs/text-to-speech?topic=text-to-speech-usingHTTP#escape). |
| Invalid syllable stress | The `ph` attribute of a `<phoneme>` element for {{site.data.keyword.IBM_notm}} SPR includes invalid syllable stress. For more information about indicating syllables and syllable stress, see [Specifying syllables](/docs/text-to-speech?topic=text-to-speech-symbols#syllables). |
| Invalid phonetic symbol | The `ph` attribute of a `<phoneme>` element includes an unsupported IPA or SPR symbol for the specified language. |
| No vowels | The `ph` attribute of a `<phoneme>` element specifies a word pronunciation that includes no vowels. |
| French liaison in invalid location | In the `ph` attribute of a `<phoneme>` element, the liaison character does not follow a consonant or it occurs in the middle of a word's pronunciation. |
| Japanese `:` symbol does not precede a vowel | In the `ph` attribute of a `<phoneme>` element in Japanese, a `:` character does not occur before a vowel (possibly with other symbols, such as syllable boundary, in between). |
| Invalid use of the SSML `<prosody>` element | You cannot use the `contour`, `duration`, `range`, and `volume` attributes of the `<prosody>` element with any voice. |
| Invalid use of the SSML `<express-as>` element | You can use the `<express-as>` element only with expressive neural voices. |
{: caption="Table 1. SSML validation errors"}
