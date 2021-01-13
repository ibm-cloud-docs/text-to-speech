---

copyright:
  years: 2015, 2021
lastupdated: "2021-01-13"

subcollection: text-to-speech

content-type: troubleshoot

---

{:help: data-hd-content-type='help'}
{:troubleshoot: data-hd-content-type='troubleshoot'}
{:support: data-reuse='support'}
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

# Using SSML
{: #ssml}

The Speech Synthesis Markup Language (SSML) is an XML-based markup language that provides annotations of text for speech-synthesis applications. It is a recommendation of the W3C Voice-Browser Working Group that has been adopted as the standard markup language for speech synthesis by the VoiceXML 2.0 specification. SSML provides developers of speech applications with a standard way to control aspects of the synthesis process by enabling them to specify pronunciation, volume, pitch, speed, and other attributes via markup.
{: shortdesc}

With the {{site.data.keyword.texttospeechfull}} service, you can use SSML to control the synthesis of your text with all supported languages. This includes using the SSML `<phoneme>` element to define a word's pronunciation in either the International Phonetic Alphabet (IPA) or the {{site.data.keyword.IBM_notm}} Symbolic Phonetic Representation (SPR). The service also relies on the SSML `<phoneme>` element to define the phonetic translation for a word with its customization interface; for more information, see [Understanding customization](/docs/text-to-speech?topic=text-to-speech-customIntro).

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

A full legal SSML document consists of an XML prolog, which contains information such as encoding and the schema against which to validate the SSML document, followed by the root element, `<speak>`. (For more information about the structure of the prolog, see [tizag.com/xmlTutorial/xmlprolog.php](http://www.tizag.com/xmlTutorial/xmlprolog.php){: external}.) Within the span of the `<speak>` element, you specify the text that is to be synthesized, augmented with additional elements.

```xml
<!-- The XML Prolog -->
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE speak PUBLIC "-//W3C//DTD SYNTHESIS 1.0//EN"
  "http://www.w3.org/TR/speech-synthesis/synthesis.dtd">

<!-- Root Element -->
<speak version="1.0" xmlns="www.w3.org/2001/10/synthesis"
  ... the body that contains text to be synthesized plus markup ...
</speak>
```
{: codeblock}

The service supports SSML fragments, which are SSML elements that do not include the full XML header.

## SSML support
{: #ssmlSupport}
{: troubleshoot}
{: support}

The {{site.data.keyword.texttospeechshort}} service bases its support on SSML Version 1.0, which was recommended by W3C on September 7, 2004. For more information about the W3C SSML recommendation, see [W3C Speech Synthesis Markup Language (SSML) Version 1.0](http://www.w3.org/TR/speech-synthesis/){: external}.

For more information about using SSML with the service, see the following:

-   For complete information about the service's level of support for all SSML elements, see [SSML elements](/docs/text-to-speech?topic=text-to-speech-elements). With a few exceptions, the service implements most of the W3C specification, as well as SSML fragments.
-   The service's customization interface supports the use of the SSML `<phoneme>` element to specify the phonetic spelling that it uses to pronounce a word. The phonetic spelling represents the sounds of a word, how those sounds are divided into syllables, and which syllables receive stress.
    -   For information about the customization interface, see [Understanding customization](/docs/text-to-speech?topic=text-to-speech-customIntro).
    -   For information about the valid symbols that you can use in an {{site.data.keyword.IBM_notm}} SPR or IPA specification for any supported language, see [Using phonetic symbols](/docs/text-to-speech?topic=text-to-speech-sprs).

## SSML validation
{: #errors}
{: troubleshoot}
{: support}

The service validates all SSML elements that you submit in any content, either as input text for synthesis or as the definition of a word's translation for customization. The service cannot determine ahead of time whether text submitted for synthesis contains SSML elements. Therefore, it performs the same validation for all input text, regardless of whether it contains SSML.

-   *All SSML input must be correct and well formed.* The service silently ignores unsupported SSML elements. The service synthesizes the text contained inside an unsupported element or an element that uses unsupported features; only the element is ignored.
-   *The service reports an HTTP 400 error code for invalid elements.* The error response includes a descriptive message, and the request fails.

Specifically, the service returns an error in the following cases:

-   *Invalid element.* For example, you specify a tag incorrectly, omit a required attribute, or include an opening tag but no matching closing tag.
-   *Invalid symbol.* The `ph` attribute of a `<phoneme>` element includes an unsupported IPA or SPR symbol for the specified language.
-   *No vowels.* The `ph` attribute of a `<phoneme>` element specifies a word pronunciation that includes no vowels.
-   *French liaison in invalid location.* In the `ph` attribute of a `<phoneme>` element, the liaison character does not follow a consonant or occurs in the middle of the word pronunciation.
-   *Japanese `:` symbol does not precede a vowel.* In the `ph` attribute of a `<phoneme>` element, a `:` character does not occur before a vowel (possibly with other symbols, such as syllable boundary, in between).
-   *Invalid syllable stress.* The `ph` attribute of a `<phoneme>` element for an {{site.data.keyword.IBM_notm}} SPR includes invalid syllable stress. For French, a syllable stress symbol does not immediately precede a vowel. For Spanish or Italian, a secondary (`2`) or no stress (`0`) symbol is used. For Japanese, a secondary stress symbol (`2`) is used.
-   *Unescaped XML control characters.* The input text itself contains a <code>&quot;</code>, <code>&apos;</code>, `&`, `<`, or `>` character instead of its equivalent escape string or character encoding. For more information, see [Escaping XML control characters](/docs/text-to-speech?topic=text-to-speech-usingHTTP#escape).
-   *Invalid use of the SSML `<prosody>` element.* You cannot use the `contour`, `duration`, and `range` attributes of the `<prosody>` element with any voice.

The service also returns an error for invalid use of deprecated features:

-   *Invalid use of the SSML `volume` attribute with the `<prosody>` element.* You cannot use the `volume` attribute of the `<prosody>` element with neural voices. The attribute was valid only with the deprecated standard voices.
-   *Invalid use of the SSML `<express-as>` or `<voice-transformation>` element.* You cannot use these SSML extensions with neural voices. The elements were valid only with deprecated standard US English voices.

For more information about these elements and about migrating to neural voices, see [Migrating from standard to neural voices](/docs/text-to-speech?topic=text-to-speech-voices#migrateVoice).
