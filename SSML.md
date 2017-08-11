---

copyright:
  years: 2015, 2017
lastupdated: "2017-08-11"

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

The Speech Synthesis Markup Language (SSML) is an XML-based markup language designed to provide annotations of text for speech-synthesis applications. It is a recommendation of the W3C Voice-Browser Working Group that has been adopted as the standard markup language for speech synthesis by the VoiceXML 2.0 specification. SSML provides developers of speech applications with a standard way to control aspects of the synthesis process by enabling them to specify pronunciation, volume, pitch, speed, and so on via markup.
{: shortdesc}

With the {{site.data.keyword.texttospeechshort}} service, you can use SSML to control the synthesis of your text with all supported languages. This includes using the SSML `<phoneme>` element to define a word's pronunciation in either the International Phonetic Alphabet (IPA) or the {{site.data.keyword.IBM_notm}} Symbolic Phonetic Representation (SPR). The service also relies on the SSML `<phoneme>` tag to define the phonetic translation for a word with its customization interface; for more information, see [Understanding customization](/docs/services/text-to-speech/custom-intro.html) and [Using customization](/docs/services/text-to-speech/custom-using.html).

## Introduction to SSML
{: #introduction}

SSML operates by augmenting the plain text that is passed to a synthesizer with a predefined set of tags. An XML parser first separates the plain input text from the markup specifications. The specifications are then processed and sent as a set of instructions in a form that can be understood by the synthesizer to produce the desired effects. For the XML parser to carry out this job, the markup needs to be well formed; for example, tags must be closed and multiple tags must be properly nested. For an introduction to basic XML concepts, see [w3schools.com/xml/xml_whatis.asp ![External link icon](../../icons/launch-glyph.svg "External link icon")](http://www.w3schools.com/xml/xml_whatis.asp){: new_window}.

An SSML element is anything contained within, and including, an opening tag and its matching closing tag. As shown in the following example, an element can contain a combination of other elements (that is, tags can be nested) and text. Additionally, tags can require or optionally accept attributes set to particular values.

```xml
<tag1>
  <tag2 attributeName="attributeValue">
    ... some text ...
  </tag2>
</tag1>
```
{: codeblock}

A full legal SSML document consists of an XML prolog, which contains information such as encoding and the schema against which to validate the SSML document, followed by the root element, `<speak>`. (For more information about the structure of the prolog, see [tizag.com/xmlTutorial/xmlprolog.php ![External link icon](../../icons/launch-glyph.svg "External link icon")](http://www.tizag.com/xmlTutorial/xmlprolog.php){: new_window}.) Within the span of the `<speak>` element, you specify the text that is to be synthesized, augmented with any tags.

```xml
<!-- The XML Prolog -->
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE speak PUBLIC "-//W3C//DTD SYNTHESIS 1.0//EN"
  "http://www.w3.org/TR/speech-synthesis/synthesis.dtd">

<!-- Root Element -->
<speak version="1.0" xmlns="www.w3.org/2001/10/synthesis"
  ... the body containing text to be synthesized plus markup ...
</speak>
```
{: codeblock}

## SSML support
{: #ssmlSupport}

Implementation of SSML support in the {{site.data.keyword.texttospeechshort}} service is based on SSML Version 1.0, which was recommended by W3C on September 7, 2004: [W3C Speech Synthesis Markup Language (SSML) Version 1.0 ![External link icon](../../icons/launch-glyph.svg "External link icon")](http://www.w3.org/TR/speech-synthesis/){: new_window}. The service implements most of the W3C specification, as well as SSML fragments (SSML tags without the full XML header), with a few exceptions. The following table summarizes the supported SSML elements; for more information about each tag, see [SSML tags](#tags) or click on the name of the tag in the table.

<table>
  <caption>Table 1. Supported SSML elements</caption>
  <tr>
    <th style="text-align:left; width:40%">Feature</th>
    <th style="text-align:center; width:13%">Supported</th>
    <th></th>
    <th style="text-align:left; width:33%">Feature</th>
    <th style="text-align:center; width:13%">Supported</th>
  </tr>
  <tr>
    <td><a href="#speak_tag"><strong>Speak</strong></a></td>
    <td style="text-align:center">yes</td>
    <td></td>
    <td><a href="#phoneme_tag"><strong>Phoneme</strong></a></td>
    <td style="text-align:center"></td>
  </tr>
  <tr>
    <td><a href="#ps_tag"><strong>Paragraph</strong></a></td>
    <td style="text-align:center">yes</td>
    <td></td>
    <td style="padding-left:25px">IBM SPR</td>
    <td style="text-align:center">yes</td>
  </tr>
  <tr>
    <td><a href="#ps_tag"><strong>Sentence</strong></a></td>
    <td style="text-align:center">yes</td>
    <td></td>
    <td style="padding-left:25px">IPA</td>
    <td style="text-align:center">yes</td>
  </tr>
  <tr>
    <td><a href="#say-as_tag"><strong>Say-as</strong></a></td>
    <td style="text-align:center"></td>
    <td></td>
    <td><a href="#prosody_tag"><strong>Prosody</strong></a></td>
    <td style="text-align:center"></td>
  </tr>
  <tr>
    <td style="padding-left:25px">Letters</td>
    <td style="text-align:center">yes</td>
    <td></td>
    <td style="padding-left:25px">Pitch</td>
    <td style="text-align:center">yes</td>
  </tr>
  <tr>
    <td style="padding-left:25px">Digits</td>
    <td style="text-align:center">yes</td>
    <td></td>
    <td style="padding-left:25px">Rate</td>
    <td style="text-align:center">yes</td>
  </tr>
  <tr>
    <td style="padding-left:25px">Date</td>
    <td style="text-align:center">yes</td>
    <td></td>
    <td style="padding-left:25px">Volume</td>
    <td style="text-align:center">yes</td>
  </tr>
  <tr>
    <td style="padding-left:25px">Ordinal</td>
    <td style="text-align:center">yes</td>
    <td></td>
    <td style="padding-left:25px">Contour</td>
    <td style="text-align:center">no</td>
  </tr>
  <tr>
    <td style="padding-left:25px">Cardinal</td>
    <td style="text-align:center">yes</td>
    <td></td>
    <td style="padding-left:25px">Duration</td>
    <td style="text-align:center">no</td>
  </tr>
  <tr>
    <td style="padding-left:25px">Number</td>
    <td style="text-align:center">yes</td>
    <td></td>
    <td style="padding-left:25px">Range</td>
    <td style="text-align:center">no</td>
  </tr>
  <tr>
    <td style="padding-left:50px">Ordinal</td>
    <td style="text-align:center">yes</td>
    <td></td>
    <td><a href="#sub_tag"><strong>Sub</strong></a></td>
    <td style="text-align:center">yes</td>
  </tr>
  <tr>
    <td style="padding-left:50px">Cardinal</td>
    <td style="text-align:center">yes</td>
    <td></td>
    <td><a href="#break_tag"><strong>Break</strong></a></td>
    <td style="text-align:center">yes</td>
  </tr>
  <tr>
    <td style="padding-left:50px">Telephone</td>
    <td style="text-align:center">yes</td>
    <td></td>
    <td><a href="#mark_tag"><strong>Mark</strong></a></td>
    <td style="text-align:center">yes</td>
  </tr>
  <tr>
    <td style="padding-left:75px">with punctuation</td>
    <td style="text-align:center">yes</td>
    <td></td>
    <td><a href="#ad_tag"><strong>Audio</strong></a></td>
    <td style="text-align:center">no</td>
  </tr>
  <tr>
    <td style="padding-left:25px">vxml:digits</td>
    <td style="text-align:center">yes</td>
    <td></td>
    <td><a href="#ad_tag"><strong>Desc</strong></a></td>
    <td style="text-align:center">no</td>
  </tr>
  <tr>
    <td style="padding-left:25px">vxml:date</td>
    <td style="text-align:center">yes</td>
    <td></td>
    <td><a href="#emphasis_tag"><strong>Emphasis</strong></a></td>
    <td style="text-align:center">no</td>
  </tr>
  <tr>
    <td style="padding-left:25px">vxml:currency</td>
    <td style="text-align:center">yes</td>
    <td></td>
    <td><a href="#lexicon_tagpx"><strong>Lexicon</strong></a></td>
    <td style="text-align:center">no</td>
  </tr>
  <tr>
    <td style="padding-left:25px">vxml:phone</td>
    <td style="text-align:center">yes</td>
    <td></td>
    <td><a href="#mm_tag"><strong>Meta</strong></a></td>
    <td style="text-align:center">no</td>
  </tr>
  <tr>
    <td style="padding-left:25px">vxml:boolean</td>
    <td style="text-align:center">yes</td>
    <td></td>
    <td><a href="#mm_tag"><strong>Metadata</strong></a></td>
    <td style="text-align:center">no</td>
  </tr>
  <tr>
    <td></td>
    <td></td>
    <td></td>
    <td><a href="#voice_tag"><strong>Voice</strong></a></td>
    <td style="text-align:center">no</td>
  </tr>
</table>

The remainder of this documentation indicates when an SSML tag is only partially supported (that is, its W3C specification allows for some attributes that are not supported) or when its implementation differs from the W3C specification.

### SSML phonemes
{: #phoneme}

The service supports the use of the SSML `<phoneme>` element to define word pronunciation. The element lets you specify the phonetic spelling that is to be used by the service to pronounce the word enclosed within the tag. The phonetic spelling represents the sounds of a word, how these sounds are divided into syllables, and which syllables receive stress.

The optional `alphabet` attribute of the `<phoneme>` element specifies the phonetic alphabet to be used for pronunciation:

-   The standard International Phonetic Alphabet (IPA): `alphabet="ipa"`
-   The {{site.data.keyword.IBM_notm}} Symbolic Phonetic Representation (SPR): `alphabet="ibm"`

If the alphabet is not specified, the service uses {{site.data.keyword.IBM_notm}} SPR as the default. The following examples present the pronunciation of *tomato* in both the IPA and SPR notations. The required `ph` attribute defines the pronunciation in each case.

<pre><code data-copy="false" class="language-xml">&lt;phoneme alphabet="ipa" ph="t&#601;&#712;me&#618;.&#638;o&#650;"&gt;tomato&lt;/phoneme&gt;
&lt;phoneme alphabet="ibm" ph=".0tx.1me.0Fo"&gt;tomato&lt;/phoneme&gt;</code></pre>

For a detailed description of the valid symbols that you can use in an {{site.data.keyword.IBM_notm}} SPR or IPA specification for any supported language, see [Using SPRs](/docs/services/text-to-speech/SPRs.html).

### Expressive SSML
{: #expressive}

The service augments SSML with an `<express-as>` element that you can use to indicate how text is to be expressed when spoken (as good news, as an apology, or with uncertainty). The service currently supports expressiveness only for the US English Allison voice. For more information, see [Using expressive SSML](/docs/services/text-to-speech/http.html#expressive).

### Voice transformation SSML
{: #transformation}

The service further extends SSML with a `<voice-transformation>` element that you can use to expand the range of possible voices by controlling pitch, pitch range, glottal tension, breathiness, rate, and timbre. The service also offers two built-in virtual voices, *Young* and *Soft*. The service currently supports voice transformation only for the US English Allison voice. For more information, see [Using voice transformation SSML](/docs/services/text-to-speech/http.html#transformation).

### SSML parsing

The SSML processor of the {{site.data.keyword.texttospeechshort}} service silently ignores unsupported tags. The text contained inside an unsupported tag or a tag that uses unsupported features is synthesized as-is; only the tag is ignored. If the syntax of the input text contains a markup error, the service returns an error.

### SSML validation
{: #errors}

The service validates all SSML elements that you submit in any content, either as input text for synthesis or as the definition of a word's pronunciation for customization. All SSML input must be correct and well formed. If you submit an invalid tag, the service reports an HTTP 400 response code that includes a descriptive message, and the method fails. Examples of cases for which the service returns an error include

-   An invalid element. For example, you specify a tag incorrectly, omit a required attribute, or include an opening tag but no equivalent closing tag.
-   An invalid symbol. The `ph` attribute of a `<phoneme>` element includes an unsupported IPA or SPR symbol for the specified language.
-   No vowels. The `ph` attribute of a `<phoneme>` element specifies a word pronunciation that includes no vowels.
-   French liaison in invalid location. For example, in the `ph` attribute of a `<phoneme>` element, the liaison character does not follow a consonant or occurs in the middle of the word pronunciation.
-   Japanese `:` symbol does not precede a vowel. In the `ph` attribute of a `<phoneme>` element, a `:` character does not occur before a vowel (possibly with other symbols, such as syllable boundary, in between).
-   Invalid syllable stress. The `ph` attribute of a `<phoneme>` element for an {{site.data.keyword.IBM_notm}} SPR includes invalid syllable stress. For French, a syllable stress symbol does not immediately precede a vowel. For Spanish (Castilian or North American) or Italian, a secondary (`2`) or no stress (`0`) symbol is used. For Japanese, a secondary stress symbol (`2`) is used.
-   Invalid use of an SSML `<express-as>` or `<voice-transformation>` element. Currently, you can use these SSML extensions only with the US English Allison voice.
-   Unescaped XML control characters. The input text itself contains a <code>&quot;</code>, <code>&apos;</code>, `&`, `<`, or `>` character instead of its equivalent escape string or character encoding. For more information, see [Escaping XML control characters](/docs/services/text-to-speech/http.html#escape).

The service cannot determine ahead of time whether text submitted for synthesis contains SSML elements. Therefore, the service validates all input text, regardless of whether it contains any SSML tags.

## SSML tags
{: #tags}

This section presents a list of SSML elements and attributes, along with examples of how to use them.

### The speak tag
{: #speak_tag}

The `<speak>` tag is the root element for SSML documents. Valid attributes are

-   `version` is a required attribute that specifies the SSML specification. The accepted value is `1.0`.
-   `xml:lang` is not required by the service. Omit the attribute when using this tag.
-   `xml:base` has no effect.

```xml
<speak version="1.0">
  The text to be spoken.
</speak>
```
{: codeblock}

### The paragraph and sentence tags
{: #ps_tag}

The `<paragraph>` (or `<p>`) and `<sentence>` (or `<s>`) elements are optional tags that can be used to give hints about textual structure. The only valid attribute for either tag is `xml:lang`, which allows a value to be specified even though language switching is not supported.

```xml
<speak version="1.0">
  <paragraph>
    <sentence>Text within a sentence tag.</sentence>
    <s>More text in another sentence.<s>
  </paragraph>
</speak>
```
{: codeblock}

> **Note:** If the text enclosed in a `<paragraph>` or `<sentence>` tag does not end with an end-of-sentence punctuation character (like a period), a longer than normal pause is added to the synthesized audio for the text.

### The say-as tag
{: #say-as_tag}

The `<say-as>` tag provides information about the type of text contained within the tag and specifies the level of detail for rendering the text. This tag is only partially supported for languages other than US English. The tag has one required attribute, `interpret-as`, which indicates how the enclosed text is to be interpreted. It has two optional attributes, `format` and `detail`, which are used only with particular values within the `interpret-as` attribute, as illustrated in the following examples.

Acceptable values for the `interpret-as` attribute and examples of each follow:

-   `letters` spells out the characters in the word within the tag. The following example spells the word *hello*.

    ```xml
    <speak version="1.0">
      <say-as interpret-as="letters">Hello</say-as>
    </speak>
    ```
    {: codeblock}

-   `digits` speaks the digits in the number within the tag. The following example speaks the digits *123456*.

    ```xml
    <speak version="1.0">
      <say-as interpret-as="digits">123456</say-as>
    </speak>
    ```
    {: codeblock}

-   `date` speaks the date within the tag according to the format given in the associated `format` attribute. The `format` attribute is required for the `date` value, but if no `format` is present, the service still attempts to pronounce the date. The following examples speak the indicated dates in the specified formats, where `d`, `m`, and `y` represent day, month, and year.

    ```xml
    <speak version="1.0">
      <say-as interpret-as="date" format="mdy">12/17/2005</say-as>
      <say-as interpret-as="date" format="ymd">2005/12/17</say-as>
      <say-as interpret-as="date" format="dmy">17/12/2005</say-as>
      <say-as interpret-as="date" format="ydm">2005/17/12</say-as>
      <say-as interpret-as="date" format="my">12/2005</say-as>
      <say-as interpret-as="date" format="md">12/17</say-as>
      <say-as interpret-as="date" format="ym">2005/12</say-as>
    </speak>
    ```
    {: codeblock}

-   `ordinal` speaks the ordinal value for the digit within the tag. The following example says *second first*.

    ```xml
    <speak version="1.0">
      <say-as interpret-as="ordinal">2</say-as>
      <say-as interpret-as="ordinal">1</say-as>
    </speak>
    ```
    {: codeblock}

-   `cardinal` speaks the cardinal number for the Roman numeral within the tag. The following example says *Super Bowl thirty-nine*.

    ```xml
    <speak version="1.0">
      Super Bowl <say-as interpret-as="cardinal">XXXIX</say-as>
    </speak>
    ```
    {: codeblock}

-   `number` offers an alternative to the previous values. By using the `format` attribute to indicate how a number is to be interpreted, you can enter one series of numbers and have it pronounced several different ways, as shown in the example. The example also includes two different ways of pronouncing a series of numbers as a telephone number; to have the series pronounced with the punctuation included, specify the `detail` attribute with the value `punctuation`.

    ```xml
    <speak version="1.0">
      <say-as interpret-as="number">123456</say-as>
      <say-as interpret-as="number" format="ordinal">123456</say-as>
      <say-as interpret-as="number" format="cardinal">123456</say-as>
      <say-as interpret-as="number" format="telephone">555-555-5555</say-as>
      <say-as interpret-as="number" format="telephone" detail="punctuation">555-555-5555</say-as>
    </speak>
    ```
    {: codeblock}

-   `vxml:digits` performs the same function as `digits`.
-   `vxml:date` works like the `date` value, but the format is predefined as `YYYYMMDD`. If a day, month, or year value is not known or if you do not want it to be spoken, replace the value with a `?` (question mark), as shown in the second and third examples.

    ```xml
    <speak version="1.0">
      <say-as interpret-as="vxml:date">20050720</say-as>
      <say-as interpret-as="vxml:date">????0720</say-as>
      <say-as interpret-as="vxml:date">200507??</say-as>
    </speak>
    ```
    {: codeblock}

-   `vxml:currency` is used to control the synthesis of monetary values. The string must be written in the format `UUUmm.nn`, where `UUU` is the three-character currency indicator specified by ISO standard 4217 and `mm.nn` is the quantity. The following example says *forty-five dollars and thirty cents*.

    ```xml
    <speak version="1.0">
      <say-as interpret-as="vxml:currency">USD45.30</say-as>
    </speak>
    ```
    {: codeblock}

    If the specified number includes more than two decimal places, the amount is synthesized as a decimal number followed by the currency indicator. If the three-character currency indicator is not present, the amount is synthesized as a decimal number only and the currency type is not pronounced. The following example says *forty-five point three two nine US dollars*.

    ```xml
    <speak version="1.0">
      <say-as interpret-as="vxml:currency">USD45.329</say-as>
    </speak>
    ```
    {: codeblock}

-   `vxml:phone` speaks a phone number with both digits and punctuation, similar to the example of the `number` value that specifies the `format` as `telephone` and the `detail` as `punctuation`.

    ```xml
    <speak version="1.0">
      <say-as interpret-as="vxml:phone">555-555-5555</say-as>
    </speak>
    ```
    {: codeblock}

-   `vxml:boolean` speaks *yes* or *no* depending on the `true` or `false` value within the tag.

    ```xml
    <speak version="1.0">
      <say-as interpret-as="vxml:boolean">true</say-as>
      <say-as interpret-as="vxml:boolean">false</say-as>
    </speak>
    ```
    {: codeblock}

### The phoneme tag
{: #phoneme_tag}

The `<phoneme>` tag lets you provide a phonetic pronunciation for the enclosed text. The tag has two attributes:

-   `alphabet` is an optional attribute that specifies the phonology to be used. The supported alphabets are `ipa` for the standard International Phonetic Alphabet and `ibm` for {{site.data.keyword.IBM_notm}} SPR. If no alphabet is designated, the default value is `ibm`.
-   `ph` is a required attribute that provides the pronunciation in the indicated alphabet. The following two examples show alternative definitions for *tomato* in the IPA phonology. The first example specifies Unicode symbols, and the second specifies IPA symbols.

    <pre><code data-copy="false" class="language-xml">&lt;speak version="1.0"&gt;
      &lt;phoneme alphabet="ipa" ph="t&amp;&#35;x259;mei&amp;&#35;x27E;o&amp;&#35;x028A"&gt;tomato&lt;/phoneme&gt;
    &lt;/speak&gt;

    &lt;speak version="1.0"&gt;
      &lt;phoneme alphabet="ipa" ph="t&#601;mei&#638;o&#650;"&gt;tomato&lt;/phoneme&gt;
    &lt;/speak&gt;</code></pre>

    The following example specifies a pronunciation for *tomato* in {{site.data.keyword.IBM_notm}} SPR phonology.

    ```xml
    <speak version="1.0">
      <phoneme alphabet="ibm" ph=".0tx.1me.0fo">tomato</phoneme>
    </speak>
    ```
    {: codeblock}

For more information about using SPR and IPA notations with the `<phoneme>` element, see [Using SPRs](/docs/services/text-to-speech/SPRs.html).

### The prosody tag
{: #prosody_tag}

The `<prosody>` tag controls the pitch, range, speaking rate, and volume of the text. All attributes are optional, but an error occurs if no attribute is specified. The SSML specification allows for three attributes that the service does not currently support: `contour`, `range`, and `duration`. The service does support the following attributes:

-   `pitch` modifies the baseline pitch for the text within the tag. Accepted values are
    -   A number followed by the `Hz` (Hertz) designation: the baseline pitch is transposed (up or down) to the specified value.
    -   A relative change value (in semitones): a number, preceded by `+` (an increase) or `-` (a decrease) and followed by `st` (semitones), that causes an absolute shift with respect to the current baseline (for example, `+5st`).
    -   A relative change in percent: a number, preceded by `+` (an increase) or `-` (a decrease) and followed by `%` (percent sign), that causes a relative shift with respect to the current baseline (for example, `-10%`).
    -   One of the following six keywords, which modify the pitch to the corresponding predefined values:
        -   `default` uses the service's default baseline pitch.
        -   `x-low` shifts the pitch baseline down by 12 semitones.
        -   `low` shifts the pitch baseline down by 6 semitones.
        -   `medium` produces the same behavior as `default`.
        -   `high` shifts the pitch baseline up by 6 semitones.
        -   `x-high` shifts the pitch baseline up by 12 semitones.

        ```xml
        <speak version="1.0">
          <prosody pitch="150Hz">Transpose pitch to 150 Hz</prosody>
          <prosody pitch="-20Hz">Lower pitch by 20 Hz from baseline</prosody>
          <prosody pitch="+20Hz">Increase pitch by 20 Hz from baseline</prosody>
          <prosody pitch="-12st">Lower pitch by 12 semitones from baseline</prosody>
          <prosody pitch="+12st">Increase pitch by 12 semitones from baseline</prosody>
          <prosody pitch="x-low">Lower pitch by 12 semitones from baseline</prosody>
        </speak>
        ```
        {: codeblock}

-   `rate` indicates a change in the speaking rate for the text within the tag. The rate is specified in terms of words per minute; if the speaking rate is 50 words per minute, then `rate` equals `50`. Note that when `rate` is set to a positive number, the implementation does not comply with the current W3C prosody rate attribute specification. Also, relative value changes (for example, `+15`) are not supported (though relative percent changes are). Accepted values are
    -   A relative percentage increase or decrease: `+10%`.
    -   A number of words per minute as a positive number: `75`.
    -   `default` uses the service's default rate.
    -   `x-slow` to decrease the rate by 50 percent.
    -   `slow` to decrease the rate by 25 percent.
    -   `medium` for the same behavior as `default`.
    -   `fast` increases the rate by 25 percent.
    -   `x-fast` increases the rate by 50 percent.

    ```xml
    <speak version="1.0">
      <prosody rate="slow">Decrease speaking rate by 25%</prosody>
      <prosody rate="50">Set speaking rate at 50 words per minute</prosody>
      <prosody rate="+5%">Increase speaking rate by 5 words per minute</prosody>
    </speak>
    ```
    {: codeblock}

-   `volume` modifies the volume for the text within the tag. Specify an integer or decimal value in the range of 1.0 to 100.0 (maximum volume), or use one of the following attributes, which correspond to predefined values in the range of 0 to 100. (Note that the `silent` attribute is not supported.)
    -   `x-soft` has the value 30.
    -   `soft` has the value 50.
    -   `medium` has the value 80.
    -   `loud` has the value 90.
    -   `default` has the value 92.
    -   `x-loud` has the value 100.

    ```xml
    <speak version="1.0">
      <prosody volume="75">Modified volume is 75</prosody>
      <prosody volume="88.9">Modified volume is 88.9</prosody>
      <prosody volume="loud">Modified volume is 90</prosody>
    </speak>
    ```
    {: codeblock}

### The sub tag
{: #sub_tag}

The `<sub>` tag indicates that the text specified in the `alias` attribute is to replace the text enclosed within the tag when speech is synthesized. The `alias` attribute is the only attribute of the tag and is required. An error occurs if it is not defined.

```xml
<speak version="1.0">
  <sub alias="International Business Machines">IBM</sub>
</speak>
```
{: codeblock}

### The break tag
{: #break_tag}

The `<break>` tag inserts a pause into the spoken text. It has the following optional attributes:

-   `strength` specifies the length of the pause in terms of varying strength values: `none`, `x-weak`, `weak`, `medium`, `strong`, or `x-strong`.
-   `time` specifies the length of the pause in terms of seconds or milliseconds. Valid value formats are `NNNs` for seconds or `NNNms` for milliseconds.

```xml
<speak version="1.0">
  Different sized <break strength="none">no pause</break>
  Different sized <break strength="x-weak">x-weak pause</break>
  Different sized <break strength="weak">weak pause</break>
  Different sized <break strength="medium">medium pause</break>
  Different sized <break strength="strong">strong pause</break>
  Different sized <break strength="x-strong">x-strong pause</break>
  Different sized <break time="1s">one-second pause</break>
  Different sized <break time="1500ms">1500-millisecond pause</break>
</speak>
```
{: codeblock}

### The mark tag
{: #mark_tag}

The `<mark>` tag is an empty element that places a marker into the text to be synthesized. The client is notified when all of the text that precedes the `<mark>` element has been synthesized. The element accepts a single `name` attribute that specifies a string that uniquely identifies the mark; the name must begin with an alphanumeric character. The name is returned along with the time at which the mark occurs in the synthesized audio.

```xml
<speak version="1.0">
  Hello <mark name="here"/> world.
</speak>
```
{: codeblock}

> **Note:** The `<mark>` tag is supported only by the service's WebSocket interface, not by its HTTP interface, which ignores the element. For information about using the element, see [Specifying an SSML mark](/docs/services/text-to-speech/websockets.html#mark).

### The audio and desc tags
{: #ad_tag}

This `<audio>` tag inserts recorded elements into the service-generated audio. It is not currently supported. The related SSML element `<desc>` is a tag that can occur only within the content of an `<audio>` element and is therefore also unsupported.

### The emphasis tag
{: #emphasis_tag}

The `<emphasis>` tag requests that the enclosed text be spoken with emphasis. It is not currently supported.

### The lexicon tag
{: #lexicon_tag}

This `<lexicon>` tag introduces pronunciation dictionaries for the given SSML document. It is not currently supported.

### The meta and metadata tags
{: #mm_tag}

The `<meta>` and `<metadata>` tags are containers in which you can place information about the document. They are not currently supported.

### The voice tag
{: #voice_tag}

This `<voice>` tag requests a change in voice. It is not currently supported.
