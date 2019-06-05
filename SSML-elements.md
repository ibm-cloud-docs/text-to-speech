---

copyright:
  years: 2015, 2019
lastupdated: "2019-06-04"

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

# SSML elements
{: #elements}

With the {{site.data.keyword.texttospeechfull}} service, you can use most Speech Synthesis Markup Language (SSML) elements to control the synthesis of your text. The elements are available for all supported languages. The following table summarizes the service's support for SSML elements and attributes.

-   *Full* means that the service fully supports the element or attribute with its HTTP and WebSocket interfaces.
-   *Partial* means that the service does not support all aspects of the element or attribute. It can also mean that the service supports the element or attribute with only one of its interfaces, or that the element or attribute is not supported with all voices.
-   *None* means that the service does not support the element or attribute.

For more information about an element or attribute, see its description. Where noted, support for some attributes and values differs slightly from the SSML specification. For more information, see [W3C Speech Synthesis Markup Language (SSML) Version 1.0](http://www.w3.org/TR/speech-synthesis/){: external}.

<table>
  <caption>Table 1. SSML elements</caption>
  <tr>
    <th style="text-align:left; width:30%">Element or attribute</th>
    <th style="text-align:center; width:12%">Support</th>
    <th style="text-align:left; width:46%; padding-left:75px">Element or attribute</th>
    <th style="text-align:center; width:12%">Support</th>
  </tr>
  <tr>
    <td>[Audio](#audio_element)</td>
    <td style="text-align:center">None</td>
    <td style="padding-left:75px">[Say-as](#say-as_element)</td>
    <td style="text-align:center">Partial</td>
  </tr>
  <tr>
    <td>[Break](#break_element)</td>
    <td style="text-align:center">Full</td>
    <td style="padding-left:100px">[cardinal](#sayAsCardinal)</td>
    <td style="text-align:center">Partial</td>
  </tr>
  <tr>
    <td>[Desc](#desc_element)</td>
    <td style="text-align:center">None</td>
    <td style="padding-left:100px">[date](#sayAsDate)</td>
    <td style="text-align:center">Partial</td>
  </tr>
  <tr>
    <td>[Emphasis](#emphasis_element)</td>
    <td style="text-align:center">None</td>
    <td style="padding-left:100px">[digits](#sayAsDigits)</td>
    <td style="text-align:center">Partial</td>
  </tr>
  <tr>
    <td>[Lexicon](#lexicon_element)</td>
    <td style="text-align:center">None</td>
    <td style="padding-left:100px">[letters](#sayAsLetters)</td>
    <td style="text-align:center">Partial</td>
  </tr>
  <tr>
    <td>[Mark](#mark_element)</td>
    <td style="text-align:center">Partial</td>
    <td style="padding-left:100px">[number](#sayAsNumber)</td>
    <td style="text-align:center">Partial</td>
  </tr>
  <tr>
    <td>[Meta](#mm_element)</td>
    <td style="text-align:center">None</td>
    <td style="padding-left:125px">cardinal</td>
    <td style="text-align:center">Partial</td>
  </tr>
  <tr>
    <td>[Metadata](#mm_element)</td>
    <td style="text-align:center">None</td>
    <td style="padding-left:125px">ordinal</td>
    <td style="text-align:center">Partial</td>
  </tr>
  <tr>
    <td>[Paragraph](#ps_element)</td>
    <td style="text-align:center">Full</td>
    <td style="padding-left:125px">telephone</td>
    <td style="text-align:center">Partial</td>
  </tr>
  <tr>
    <td>[Phoneme](#phoneme_element)</td>
    <td style="text-align:center">Full</td>
    <td style="padding-left:150px">punctuation</td>
    <td style="text-align:center">Partial</td>
  </tr>
  <tr>
    <td style="padding-left:25px">IBM SPR</td>
    <td style="text-align:center">Full</td>
    <td style="padding-left:100px">[ordinal](#sayAsOrdinal)</td>
    <td style="text-align:center">Partial</td>
  </tr>
  <tr>
    <td style="padding-left:25px">IPA</td>
    <td style="text-align:center">Full</td>
    <td style="padding-left:100px">[vxml:boolean](#vxml-boolean)</td>
    <td style="text-align:center">Partial</td>
  </tr>
  <tr>
    <td>[Prosody](#prosody_element)</td>
    <td style="text-align:center">Partial</td>
    <td style="padding-left:100px">[vxml:currency](#vxml-currency)</td>
    <td style="text-align:center">Partial</td>
  </tr>
  <tr>
    <td style="padding-left:25px">contour</td>
    <td style="text-align:center">None</td>
    <td style="padding-left:100px">[vxml:date](#vxml-date)</td>
    <td style="text-align:center">Partial</td>
  </tr>
  <tr>
    <td style="padding-left:25px">duration</td>
    <td style="text-align:center">None</td>
    <td style="padding-left:100px">[vxml:digits](#vxml-digits)</td>
    <td style="text-align:center">Partial</td>
  </tr>
  <tr>
    <td style="padding-left:25px">[pitch](#prosody-pitch)</td>
    <td style="text-align:center">Full</td>
    <td style="padding-left:100px">[vxml:phone](#vxml-phone)</td>
    <td style="text-align:center">Partial</td>
  </tr>
  <tr>
    <td style="padding-left:25px">range</td>
    <td style="text-align:center">None</td>
    <td style="padding-left:75px">[Sentence](#ps_element)</td>
    <td style="text-align:center">Full</td>
  </tr>
  <tr>
    <td style="padding-left:25px">[rate](#prosody-rate)</td>
    <td style="text-align:center">Full</td>
    <td style="padding-left:75px">[Speak](#speak_element)</td>
    <td style="text-align:center">Full</td>
  </tr>
  <tr>
    <td style="padding-left:25px">[volume](#prosody-volume)</td>
    <td style="text-align:center">Partial</td>
    <td style="padding-left:75px">[Sub](#sub_element)</td>
    <td style="text-align:center">Full</td>
  </tr>
  <tr>
    <td></td>
    <td></td>
    <td style="padding-left:75px">[Voice](#voice_element)</td>
    <td style="text-align:center">None</td>
  </tr>
</table>

## The audio element
{: #audio_element}

This `<audio>` element inserts recorded elements into the service-generated audio. It is not supported.

## The break element
{: #break_element}

The `<break>` element inserts a pause into the spoken text. It has the following optional attributes:

-   `strength` specifies the length of the pause in terms of varying strength values:
    -   `none` suppresses a break that might otherwise be produced during processing.
    -   `x-weak`, `weak`, `medium`, `strong`, or `x-strong` insert increasingly stronger breaks.
-   `time` specifies the length of the pause in terms of seconds or milliseconds. Valid value formats are `{integer}s` for seconds or `{integer}ms` for milliseconds.

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

## The desc element
{: #desc_element}

The `<desc>` element can occur only within an `<audio>` element. Because the `<audio>` element is not supported, neither is the `<desc>` element.

## The emphasis element
{: #emphasis_element}

The `<emphasis>` element requests that the enclosed text is spoken with emphasis. It is not supported.

## The lexicon element
{: #lexicon_element}

This `<lexicon>` element introduces pronunciation dictionaries for the given SSML document. It is not supported.

You can use the service's customization interface to define a dictionary of custom entries (word/translation pairs) for use during speech synthesis. For more information, see [Understanding customization](/docs/services/text-to-speech?topic=text-to-speech-customIntro).

## The mark element
{: #mark_element}

The `<mark>` element is supported only by the service's WebSocket interface, not by its HTTP interface, which ignores the element. For more information, see [Specifying an SSML mark](/docs/services/text-to-speech?topic=text-to-speech-timing#mark).
{: note}

The `<mark>` element is an empty element that places a marker into the text to be synthesized. The client is notified when all of the text that precedes the `<mark>` element has been synthesized. The element accepts a single `name` attribute that specifies a string that uniquely identifies the mark; the name must begin with an alphanumeric character. The name is returned along with the time at which the mark occurs in the synthesized audio.

```xml
<speak version="1.0">
  Hello <mark name="here"/> world.
</speak>
```
{: codeblock}

## The meta and metadata elements
{: #mm_element}

The `<meta>` and `<metadata>` elements are containers in which you can place information about the document. They are not supported.

## The paragraph and sentence elements
{: #ps_element}

The `<paragraph>` (or `<p>`) and `<sentence>` (or `<s>`) elements are optional elements that can be used to give hints about textual structure. If the text that is enclosed in a `<paragraph>` or `<sentence>` element does not end with an end-of-sentence punctuation character (like a period), the service adds a longer than normal pause to the synthesized audio.

The only valid attribute for either element is `xml:lang`, which allows for language switching. The attribute is not supported.

```xml
<speak version="1.0">
  <paragraph>
    <sentence>Text within a sentence element.</sentence>
    <s>More text in another sentence.</s>
  </paragraph>
</speak>
```
{: codeblock}

## The phoneme element
{: #phoneme_element}

The `<phoneme>` element provides a phonetic pronunciation for the enclosed text. The phonetic spelling represents the sounds of a word, how the sounds are divided into syllables, and which syllables receive stress. The element has two attributes:

-   `alphabet` is an optional attribute that specifies the phonology to be used. The supported alphabets are
    -   The standard International Phonetic Alphabet (IPA): `alphabet="ipa"`
    -   The {{site.data.keyword.IBM_notm}} Symbolic Phonetic Representation (SPR): `alphabet="ibm"`

    If no alphabet is specified, the service uses IBM SPR by default.
-   `ph` is a required attribute that provides the pronunciation in the indicated alphabet. The following examples show the pronunciation for the word *tomato* in both formats:

    -   IPA format:

        <pre><code>&lt;speak version="1.0"&gt;
          &lt;phoneme alphabet="ipa" ph="t&#601;&#712;me&#618;.&#638;o&#650;"&gt;tomato&lt;/phoneme&gt;
        &lt;/speak&gt;</code></pre>

    -   IPA format with Unicode symbols:

        <pre><code>&lt;speak version="1.0"&gt;
          &lt;phoneme alphabet="ipa" ph="t&amp;&#35;x259;mei&amp;&#35;x027E;o&amp;&#035;x028A;"&gt;tomato&lt;/phoneme&gt;
        &lt;/speak&gt;</code></pre>

    -   IBM SPR format:

        <pre><code>&lt;speak version="1.0"&gt;
          &lt;phoneme alphabet="ibm" ph=".0tx.1me.0Fo"&gt;tomato&lt;/phoneme&gt;
        &lt;/speak&gt;</code></pre>

For more information about using SPR and IPA notations with the `<phoneme>` element, see [Using IBM SPR](/docs/services/text-to-speech?topic=text-to-speech-sprs).

## The prosody element
{: #prosody_element}

The `<prosody>` element controls the pitch, speaking rate, and volume of the text. All attributes are optional, but an error occurs if no attribute is specified. The SSML specification allows for three attributes that the service does not support: `contour`, `range`, and `duration`. The service supports the `pitch`, `rate`, and `volume` attributes.

### The pitch attribute
{: #prosody-pitch}

The `pitch` attribute modifies the baseline pitch for the text within the element. Accepted values are

-   A number followed by the `Hz` (Hertz) designation: The baseline pitch is transposed (up or down) to the specified value.
-   A relative change value (in semitones): A number that causes an absolute shift from the current baseline. The number is preceded by `+` (an increase) or `-` (a decrease) and followed by `st` (semitones), for example, `+5st`.
-   A relative change in percent: A number that causes a relative shift from the current baseline. The number is preceded by `+` (an increase) or `-` (a decrease) and followed by `%` (percent sign), for example, `-10%`.
-   One of the following six keywords, which modify the pitch to the corresponding predefined values:
    -   `default` uses the service's default baseline pitch.
    -   `x-low` shifts the pitch baseline down by 12 semitones.
    -   `low` shifts the pitch baseline down by six semitones.
    -   `medium` produces the same behavior as `default`.
    -   `high` shifts the pitch baseline up by six semitones.
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

### The rate attribute
{: #prosody-rate}

The `rate` attribute indicates a change in the speaking rate for the text within the element. The rate is specified in terms of words per minute; if the speaking rate is 50 words per minute, then `rate` equals `50`. When `rate` is set to a positive number, the implementation does not comply with the current W3C prosody rate attribute specification. Also, the service supports relative percent changes (for example, `+15%`) but not relative value changes (for example, `+15`). Accepted values are

-   A relative percentage increase or decrease: `+10%`.
-   A number of words per minute as a positive number: `75`.
-   `default` uses the service's default rate.
-   `x-slow` decreases the rate by 50 percent.
-   `slow` decreases the rate by 25 percent.
-   `medium` produces the same behavior as `default`.
-   `fast` increases the rate by 25 percent.
-   `x-fast` increases the rate by 50 percent.

```xml
<speak version="1.0">
  <prosody rate="slow">Decrease speaking rate by 25%</prosody>
  <prosody rate="50">Set speaking rate at 50 words per minute</prosody>
  <prosody rate="+5%">Increase speaking rate by 5 percent</prosody>
</speak>
```
{: codeblock}

### The volume attribute
{: #prosody-volume}

The service does not support the `volume` attribute of the `<prosody>` element with its DNN-based voices (for example, `en-US_AllisonV2Voice`). For more information about these voices, see [Speech synthesis technologies](/docs/services/text-to-speech?topic=text-to-speech-voices#technologiesVoices).
{: note}

The `volume` attribute modifies the volume for the text within the element. You can specify an integer or decimal value in the range of 1.0 to 100.0 (maximum volume). You can also use one of the following string values, which correspond to predefined settings in the range of 0 to 100. (The `silent` value is not supported.)

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

## The say-as element
{: #say-as_element}

The `<say-as>` element is only partially supported for most languages. For languages other than US English, the service typically supports only the `digits` and `letters` attributes of the element.
{: note}

The `<say-as>` element provides information about the type of text that is contained within the element and specifies the level of detail for rendering the text. The element has one required attribute, `interpret-as`, which indicates how the enclosed text is to be interpreted. It has two optional attributes, `format` and `detail`, which are used only with particular values within the `interpret-as` attribute, as illustrated in the following examples.

Acceptable values for the `interpret-as` attribute and examples of each follow.

### cardinal
{: #sayAsCardinal}

The `cardinal` value speaks the cardinal number for the numeral within the element. The following examples say *Super Bowl forty-nine*. The first is superfluous, since it does not change the service's default behavior.

```xml
<speak version="1.0">
  Super Bowl <say-as interpret-as="cardinal">49</say-as>
  Super Bowl <say-as interpret-as="cardinal">XLIX</say-as>
</speak>
```
{: codeblock}

### date
{: #sayAsDate}

The `date` value speaks the date within the element according to the format given in the associated `format` attribute. The `format` attribute is required for the `date` value. If no `format` is present, the service still attempts to pronounce the date. The following examples speak the indicated dates in the specified formats, where `d`, `m`, and `y` represent day, month, and year.

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

### digits
{: #sayAsDigits}

The `digits` value speaks the digits in the number within the element. The following example speaks the individual digits *123456*.

```xml
<speak version="1.0">
  <say-as interpret-as="digits">123456</say-as>
</speak>
```
{: codeblock}

### letters
{: #sayAsLetters}

The `letters` value spells out the characters in the word within the element. The following example spells the letters of the word *hello*.

```xml
<speak version="1.0">
  <say-as interpret-as="letters">Hello</say-as>
</speak>
```
{: codeblock}

### number
{: #sayAsNumber}

The `number` value offers an alternative to the `cardinal` and `ordinal` values. You can use the optional `format` attribute to indicate how a series of numbers is to be interpreted. The first example omits the `format` attribute to pronounce the number as a cardinal value. The second example explicitly specifies that the number is to be pronounced as a `cardinal` value. The third example specifies that the number is to be pronounced as an `ordinal` value.

```xml
<speak version="1.0">
  <say-as interpret-as="number">123456</say-as>
  <say-as interpret-as="number" format="cardinal">123456</say-as>
  <say-as interpret-as="number" format="ordinal">123456</say-as>
</speak>
```
{: codeblock}

You can also specify the value `telephone` for the `format` attribute. The examples show two different ways of pronouncing a series of numbers as a telephone number. To pronounce the numbers with the punctuation included, specify the value `punctuation` for the optional `detail` attribute.

```xml
<speak version="1.0">
  <say-as interpret-as="number" format="telephone">555-555-5555</say-as>
  <say-as interpret-as="number" format="telephone" detail="punctuation">555-555-5555</say-as>
</speak>
```
{: codeblock}

### ordinal
{: #sayAsOrdinal}

The `ordinal` value speaks the ordinal value for the digit within the element. The following example says *second first*.

```xml
<speak version="1.0">
  <say-as interpret-as="ordinal">2</say-as>
  <say-as interpret-as="ordinal">1</say-as>
</speak>
```
{: codeblock}

### vxml:boolean
{: #vxml-boolean}

The `vxml:boolean` value speaks *yes* or *no* depending on the `true` or `false` value within the element.

```xml
<speak version="1.0">
  <say-as interpret-as="vxml:boolean">true</say-as>
  <say-as interpret-as="vxml:boolean">false</say-as>
</speak>
```
{: codeblock}

### vxml:currency
{: #vxml-currency}

The `vxml:currency` value is used to control the synthesis of monetary values. The string must be written in the format `UUUmm.nn`, where `UUU` is the three-character currency indicator that is specified by ISO standard 4217 and `mm.nn` is the quantity. The following example says *forty-five dollars and thirty cents*.

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

### vxml:date
{: #vxml-date}

The `vxml:date` value works like the `date` value, but the format is predefined as `YYYYMMDD`. If a day, month, or year value is not known or if you do not want it to be spoken, replace the value with a `?` (question mark). The second and third examples include question marks.

```xml
<speak version="1.0">
  <say-as interpret-as="vxml:date">20050720</say-as>
  <say-as interpret-as="vxml:date">????0720</say-as>
  <say-as interpret-as="vxml:date">200507??</say-as>
</speak>
```
{: codeblock}

### vxml:digits
{: #vxml-digits}

The `vxml:digits` value provides the same function as the `digits` value.

### vxml:phone
{: #vxml-phone}

The `vxml:phone` value speaks a phone number with both digits and punctuation. It is equivalent to using the `number` value and specifying `telephone` for the `format` attribute and `punctuation` for the `detail` attribute.

```xml
<speak version="1.0">
  <say-as interpret-as="vxml:phone">555-555-5555</say-as>
</speak>
```
{: codeblock}

## The speak element
{: #speak_element}

The `<speak>` element is the root element for SSML documents. Valid attributes are

-   `version` is a required attribute that specifies the SSML specification. The accepted value is `1.0`.
-   `xml:lang` is not required by the service. Omit the attribute when you use this element.
-   `xml:base` has no effect.

```xml
<speak version="1.0">
  The text to be spoken.
</speak>
```
{: codeblock}

## The sub element
{: #sub_element}

The `<sub>` element indicates that the text that is specified by the `alias` attribute is to replace the text that is enclosed within the element when speech is synthesized. The `alias` attribute is the only attribute of the element and is required.

```xml
<speak version="1.0">
  <sub alias="International Business Machines">IBM</sub>
</speak>
```
{: codeblock}

## The voice element
{: #voice_element}

This `<voice>` element requests a change in voice. It is not supported.
