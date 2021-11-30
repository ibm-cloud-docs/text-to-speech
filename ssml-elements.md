---

copyright:
  years: 2015, 2021
lastupdated: "2020-11-22"

subcollection: text-to-speech

---

{{site.data.keyword.attribute-definition-list}}

# SSML elements
{: #elements}

With the {{site.data.keyword.texttospeechfull}} service, you can use most Speech Synthesis Markup Language (SSML) elements and attributes to control the synthesis of your text.
{: shortdesc}

## Supported elements and attributes
{: #elements-summary-table}

Table 1 summarizes the service's support for SSML elements and attributes:

-   *Full* means that the service fully supports the element or attribute with its HTTP and WebSocket interfaces.
-   *Partial* means that the service does not support all aspects of the element or attribute. It can also mean that the service supports the element or attribute with only one of its interfaces, or that the element or attribute is not supported with all voices.
-   *None* means that the service does not support the element or attribute.

The following sections provide descriptions of each element or attribute, including examples, restrictions, and whether the service's support differs from standard SSML. Support for some attributes and values differs slightly from the SSML specification. For more information, see [W3C Speech Synthesis Markup Language (SSML) Version 1.0](http://www.w3.org/TR/speech-synthesis/){: external}.

| Element or attribute | Support | Element or attribute | Support |
|----------------------|:-------:|----------------------|:-------:|
| [`<audio>` element](#audio_element) | None | [`<prosody>` element](#prosody_element) | Partial |
| [`<break>` element](#break_element) | Full | - contour attribute | None |
| [`<desc>` element](#desc_element) | None | - duration attribute | None |
| [`<emphasis>` element](#emphasis_element) | None | - [pitch attribute](#prosody-pitch) | Full |
| [`<lexicon>` element](#lexicon_element) | None | - range attribute | None |
| [`<mark>` element](#mark_element) | Partial | - [rate attribute](#prosody-rate) | Full |
| [`<meta>` element](#mm_element) | None | - volume attribute | None |
| [`<metadata>` element](#mm_element) | None | [`<say-as>` element](#say-as_element) | Partial |
| [`<paragraph>` element](#ps_element) | Full | - [interpret-as attribute](#say-as-interpret-as) | Partial |
| [`<phoneme>` element](#phoneme_element) | Full | [`<sentence>` element](#ps_element) | Full |
| | | [`<speak>` element](#speak_element) | Full |
| | | [`<sub>` element](#sub_element) | Full |
| | | [`<voice>` element](#voice_element) | None |
{: caption="Table 1. SSML elements and attributes"}

## The `<audio>` element
{: #audio_element}

This `<audio>` element inserts recorded elements into the service-generated audio. It is not supported.

## The `<break>` element
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

## The `<desc>` element
{: #desc_element}

The `<desc>` element can occur only within an `<audio>` element. Because the `<audio>` element is not supported, neither is the `<desc>` element.

## The `<emphasis>` element
{: #emphasis_element}

The `<emphasis>` element requests that the enclosed text is spoken with emphasis. It is not supported.

## The `<lexicon>` element
{: #lexicon_element}

This `<lexicon>` element introduces pronunciation dictionaries for the given SSML document. It is not supported.

You can use the service's customization interface to define a dictionary of custom entries (word/translation pairs) for use during speech synthesis. For more information, see [Understanding customization](/docs/text-to-speech?topic=text-to-speech-customIntro).

## The `<mark>` element
{: #mark_element}

The `<mark>` element is supported only by the service's WebSocket interface, not by its HTTP interface, which ignores the element. For more information, see [Specifying an SSML mark](/docs/text-to-speech?topic=text-to-speech-timing#timing-mark).
{: note}

The `<mark>` element is an empty element that places a marker into the text to be synthesized. The client is notified when all of the text that precedes the `<mark>` element has been synthesized. The element accepts a single `name` attribute that specifies a string that uniquely identifies the mark; the name must begin with an alphanumeric character. The name is returned along with the time at which the mark occurs in the synthesized audio.

```xml
<speak version="1.0">
  Hello <mark name="here"/> world.
</speak>
```
{: codeblock}

## The `<meta>` and `<metadata>` elements
{: #mm_element}

The `<meta>` and `<metadata>` elements are containers in which you can place information about the document. They are not supported.

## The `<paragraph>` and `<sentence>` elements
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

## The `<phoneme>` element
{: #phoneme_element}

The `<phoneme>` element provides a phonetic pronunciation for the enclosed text. The phonetic spelling represents the sounds of a word, how the sounds are divided into syllables, and which syllables receive stress. The element has two attributes:

-   `alphabet` is an optional attribute that specifies the phonology to be used. The supported alphabets are
    -   *The standard International Phonetic Alphabet (IPA):* `alphabet="ipa"`. All voices support IPA.
    -   *The {{site.data.keyword.IBM_notm}} Symbolic Phonetic Representation (SPR):* `alphabet="ibm"`. Only enhanced neural voices support SPR in addition to IPA.

    If no alphabet is specified, the service uses {{site.data.keyword.IBM_notm}} SPR by default. For more information, see [Language support for IPA and SPR](/docs/text-to-speech?topic=text-to-speech-symbols#supportedLanguages).
-   `ph` is a required attribute that provides the pronunciation in the indicated alphabet. The following examples show the pronunciation for the word *tomato* in both formats:

    -   IPA format:

        ```xml
        <speak version="1.0">
          <phoneme alphabet="ipa" ph="təˈmeɪ.ɾoʊ">tomato</phoneme>
        </speak>
        ```
        {: codeblock}

    -   IPA format with Unicode symbols:

        ```xml
        <speak version="1.0">
          <phoneme alphabet="ipa" ph="t&#x0259;&#x02C8;me&#x026A;.&#x027E;o&#x028A;">tomato</phoneme>
        </speak>
        ```
        {: codeblock}

    -   {{site.data.keyword.IBM_notm}} SPR format:

        ```xml
        <speak version="1.0">
          <phoneme alphabet="ibm" ph=".0tx.1me.0Fo">tomato</phoneme>
        </speak>
        ```
        {: codeblock}

For more information about using SPR and IPA notations with the `<phoneme>` element, see [Understanding phonetic symbols](/docs/text-to-speech?topic=text-to-speech-symbols).

## The `<prosody>` element
{: #prosody_element}

The `<prosody>` element controls the pitch and speaking rate of the text. All attributes are optional, but an error occurs if you do not specify at least one attribute with the element.

The service supports the following two attributes of the SSML specification:

-   [The `pitch` attribute](#prosody-pitch)
-   [The `rate` attribute](#prosody-rate)

The SSML specification also offers four attributes that the service does not support:

-   The `contour` attribute
-   The `range` attribute
-   The `duration` attribute
-   The `volume` attribute

### The `pitch` attribute
{: #prosody-pitch}

The `pitch` attribute modifies the baseline pitch for the text within the element. Accepted values are

-   _A number followed by the `Hz` (Hertz) designation:_ The baseline pitch is transposed (up or down) to the specified value. For example, `150Hz`.
-   _A relative change value (in semitones):_ A number that causes an absolute shift from the current baseline. The number is preceded by `+` (an increase) or `-` (a decrease) and followed by `st` (semitones). For example, `+5st`.
-   _A relative change in percent:_ A number that causes a relative shift from the current baseline. The number is preceded by `+` (an increase) or `-` (a decrease) and followed by `%` (percent sign). For example, `-10%`.
-   _A keyword:_ One of the following six keywords, which modify the pitch to the corresponding predefined values:
    -   `default` uses the service's default baseline pitch.
    -   `x-low` shifts the pitch baseline down by 12 semitones.
    -   `low` shifts the pitch baseline down by six semitones.
    -   `medium` produces the same behavior as `default`.
    -   `high` shifts the pitch baseline up by six semitones.
    -   `x-high` shifts the pitch baseline up by 12 semitones.

    Make adjustments based on percentages and experiment with different values to determine what works best for you. When lowering the pitch, do not exceed a value of `-50%`. When raising the pitch, do not exceed a value of `+100%`, which doubles the baseline pitch and represents an absolute limit that is quite extreme. Whether lowering or raising the pitch, experiment with incremental changes before trying the extreme values.
    {: tip}

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

### The `rate` attribute
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

## The `<say-as>` element
{: #say-as_element}

The `<say-as>` element provides information about the type of text that is contained within the element and specifies the level of detail for rendering the text.

-   The element has one required attribute, `interpret-as`, which indicates how the enclosed text is to be interpreted.
-   The element has two optional attributes, `format` and `detail`, which are used only with particular values of the `interpret-as` attribute, as shown in the following examples.

The service supports the `<say-as>` element with the following languages:

-   The service fully supports the `<say-as>` element for US English.
-   For most other languages, the service supports only the `digits` and `letters` attributes of the element.
-   For Japanese, the service supports only the `digits` attribute.

### The `interpret-as` attribute
{: #say-as-interpret-as}

Acceptable values for the `interpret-as` attribute and examples of each value follow. The service supports the following values as arguments to the `interpret-as` attribute:

-   [`cardinal`](#say-as-cardinal)
-   [`date`](#say-as-date)
-   [`digits`](#say-as-digits)
-   [`letters`](#say-as-letters)
-   [`number`](#say-as-number)
-   [`ordinal`](#say-as-ordinal)
-   [`vxml:boolean`](#vxml-boolean)
-   [`vxml:currency`](#vxml-currency)
-   [`vxml:date`](#vxml-date)
-   [`vxml:digits`](#vxml-digits)
-   [`vxml:phone`](#vxml-phone)

#### `cardinal`
{: #say-as-cardinal}

The `cardinal` value speaks the cardinal number for the numeral within the element. The following examples say *Super Bowl forty-nine*. The first is superfluous, since it does not change the service's default behavior.

```xml
<speak version="1.0">
  Super Bowl <say-as interpret-as="cardinal">49</say-as>
  Super Bowl <say-as interpret-as="cardinal">XLIX</say-as>
</speak>
```
{: codeblock}

#### `date`
{: #say-as-date}

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

#### `digits`
{: #say-as-digits}

The `digits` value speaks the digits in the number within the element. The following example speaks the individual digits *123456*.

```xml
<speak version="1.0">
  <say-as interpret-as="digits">123456</say-as>
</speak>
```
{: codeblock}

#### `letters`
{: #say-as-letters}

The `letters` value spells out the characters in the word within the element. The following example spells the letters of the word *hello*.

```xml
<speak version="1.0">
  <say-as interpret-as="letters">Hello</say-as>
</speak>
```
{: codeblock}

#### `number`
{: #say-as-number}

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
  <say-as interpret-as="number" format="telephone"
    detail="punctuation">555-555-5555</say-as>
</speak>
```
{: codeblock}

#### `ordinal`
{: #say-as-ordinal}

The `ordinal` value speaks the ordinal value for the digit within the element. The following example says *second first*.

```xml
<speak version="1.0">
  <say-as interpret-as="ordinal">2</say-as>
  <say-as interpret-as="ordinal">1</say-as>
</speak>
```
{: codeblock}

#### `vxml:boolean`
{: #vxml-boolean}

The `vxml:boolean` value speaks *yes* or *no* depending on the `true` or `false` value within the element.

```xml
<speak version="1.0">
  <say-as interpret-as="vxml:boolean">true</say-as>
  <say-as interpret-as="vxml:boolean">false</say-as>
</speak>
```
{: codeblock}

#### `vxml:currency`
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

#### `vxml:date`
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

#### `vxml:digits`
{: #vxml-digits}

The `vxml:digits` value provides the same capabilities as the `digits` value.

#### `vxml:phone`
{: #vxml-phone}

The `vxml:phone` value speaks a phone number with both digits and punctuation. It is equivalent to using the `number` value and specifying `telephone` for the `format` attribute and `punctuation` for the `detail` attribute.

```xml
<speak version="1.0">
  <say-as interpret-as="vxml:phone">555-555-5555</say-as>
</speak>
```
{: codeblock}

## The `<speak>` element
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

## The `<sub>` element
{: #sub_element}

The `<sub>` element indicates that the text that is specified by the `alias` attribute is to replace the text that is enclosed within the element when speech is synthesized. The `alias` attribute is the only attribute of the element and is required.

```xml
<speak version="1.0">
  <sub alias="International Business Machines">IBM</sub>
</speak>
```
{: codeblock}

## The `<voice>` element
{: #voice_element}

This `<voice>` element requests a change in voice. It is not supported.
