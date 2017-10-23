---

copyright:
  years: 2015, 2017
lastupdated: "2017-10-20"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:tip: .tip}
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

With the {{site.data.keyword.texttospeechshort}} service, you can use SSML to control the synthesis of your text with all supported languages. This includes using the SSML `<phoneme>` element to define a word's pronunciation in either the International Phonetic Alphabet (IPA) or the {{site.data.keyword.IBM_notm}} Symbolic Phonetic Representation (SPR). The service also relies on the SSML `<phoneme>` element to define the phonetic translation for a word with its customization interface; for more information, see [Understanding customization](/docs/services/text-to-speech/custom-intro.html).

## Introduction to SSML
{: #introduction}

SSML operates by augmenting the plain text that is passed to a synthesizer with a predefined set of elements, or tags. An XML parser first separates the plain input text from the markup specifications. The specifications are then processed and sent as a set of instructions in a form that can be understood by the synthesizer to produce the desired effects. For the XML parser to carry out this job, the markup needs to be well formed; for example, elements must be closed and multiple elements must be properly nested. For an introduction to basic XML concepts, see [w3schools.com/xml/xml_whatis.asp ![External link icon](../../icons/launch-glyph.svg "External link icon")](http://www.w3schools.com/xml/xml_whatis.asp){: new_window}.

An SSML element is anything contained within, and including, an opening tag and its matching closing tag. As shown in the following example, an element can contain a combination of other elements (tags can be nested) and text. Additionally, elements can require or optionally accept attributes set to particular values.

```xml
<tag1>
  <tag2 attributeName="attributeValue">
    ... some text ...
  </tag2>
</tag1>
```
{: codeblock}

A full legal SSML document consists of an XML prolog, which contains information such as encoding and the schema against which to validate the SSML document, followed by the root element, `<speak>`. (For more information about the structure of the prolog, see [tizag.com/xmlTutorial/xmlprolog.php ![External link icon](../../icons/launch-glyph.svg "External link icon")](http://www.tizag.com/xmlTutorial/xmlprolog.php){: new_window}.) Within the span of the `<speak>` element, you specify the text that is to be synthesized, augmented with additional elements.

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

The {{site.data.keyword.texttospeechshort}} service bases its support on SSML Version 1.0, which was recommended by W3C on September 7, 2004. For more information about the W3C SSML recommendation, see [W3C Speech Synthesis Markup Language (SSML) Version 1.0 ![External link icon](../../icons/launch-glyph.svg "External link icon")](http://www.w3.org/TR/speech-synthesis/){: new_window}.

For more information about using SSML with the service, see the following:

-   For complete information about the service's level of support for all SSML elements, see [SSML elements](/docs/services/text-to-speech/SSML-elements.html). With a few exceptions, the service implements most of the W3C specification, as well as SSML fragments.
-   The service extends SSML with an `<express-as>` element that indicates how text is to be expressed when spoken (as good news, as an apology, or with uncertainty). The service currently supports expressiveness only for the US English Allison voice. See [Using expressive SSML](/docs/services/text-to-speech/SSML-expressive.html).
-   The service extends SSML with a `<voice-transformation>` element that expands the range of possible voices by letting you control the pitch, pitch range, glottal tension, breathiness, rate, and timbre of spoken text. The service also offers two built-in virtual voices, *Young* and *Soft*. The service currently supports voice transformation only for the US English voices. See [Using voice transformation SSML](/docs/services/text-to-speech/SSML-transformation).
-   The service's customization interface supports the use of the SSML `<phoneme>` element to specify the phonetic spelling that it uses to pronounce a word. The phonetic spelling represents the sounds of a word, how these sounds are divided into syllables, and which syllables receive stress.
    -   For information about the customization interface, see [Using customization](/docs/services/text-to-speech/custom-intro.html).
    -   For information about the valid symbols that you can use in an {{site.data.keyword.IBM_notm}} SPR or IPA specification for any supported language, see [Using IBM SPR](/docs/services/text-to-speech/SPRs.html).

## SSML validation
{: #errors}

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
-   *Invalid use of SSML `<express-as>` or `<voice-transformation>` element.* Currently, you can use these SSML extensions only with the specified US English voices.
-   *Unescaped XML control characters.* The input text itself contains a <code>&quot;</code>, <code>&apos;</code>, `&`, `<`, or `>` character instead of its equivalent escape string or character encoding. For more information, see [Escaping XML control characters](/docs/services/text-to-speech/http.html#escape).
