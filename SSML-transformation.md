---

copyright:
  years: 2015, 2018
lastupdated: "2018-05-19"

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

# Voice transformation SSML
{: #transformation}

The {{site.data.keyword.texttospeechshort}} service, like most speech synthesis systems, can speak in only a limited number of voices. Moreover, some languages offer only one or two voices. To expand the range of possible voices, the service extends SSML with a `<voice-transformation>` element. You can use this element to realize different virtual voices by controlling aspects of a default voice. Applications of the feature include
{: shortdesc}

-   *Giving another flavor to a voice.* You want a voice to sound a bit different in general or for a specific application.
-   *Voice branding.* You want to use a unique voice to differentiate your applications.
-   *Multi-role applications.* You need multiple voices to represent different personae.

You can apply the `<voice-transformation>` element to the entire body of the text, a sentence, or a word or fragment. The element accepts one required attribute, `type`, which describes the type of voice transformation to be applied to the specified text. You can apply a built-in transformation or create a custom transformation based on different aspects of the voice.

## Language support
{: #languages}

The service currently supports voice transformation for the following US English voices only:

-   `en-US_AllisonVoice`
-   `en-US_LisaVoice`
-   `en-US_MichaelVoice`

Using the element with any other voice returns an error.

## Built-in transformations

Built-in transformations apply pre-configured changes to the attributes of a voice. Think of them as virtual voices that are made available by the service. The service offers two built-in transformations. To use them, you specify the case-sensitive name of the built-in transformation with the `type` attribute:

-   `Young` gives the voice a more youthful sound.
-   `Soft` makes the voice sound softer.

You can apply the optional `strength` attribute to either built-in voice to control the extent to which the service applies the transformation. Think of the value as a blending factor that the service applies to the original voice. The attribute accepts a value in the range of 0 to 100 percent. Specifying `0%` leaves the voice unaltered; specifying `100%` achieves the full extent of transformation. If you omit the attribute, the default strength is `100%`.

> **Note:** The service ignores attributes for custom transformations when you use a built-in transformation.

## Built-in transformation examples

The following examples apply the two built-in transformations to the same sentence with different strengths:

```xml
<voice-transformation type="Young" strength="80%">
  Could you provide us with new information?
</voice-transformation>

<voice-transformation type="Soft" strength="60%">
  Could you provide us with new information?
</voice-transformation>
```
{: codeblock}

## Custom transformations

Custom transformations give you more fine-grained control over different aspects of the voice transformation. To use a custom transformation, you specify `Custom` for the `type` attribute. You can then use one or more of the following optional attributes to control the transformation.

<table>
  <caption>Table 1. Custom transformation attributes</caption>
  <tr>
    <th style="width:15%; text-align:left">Attribute</th>
    <th style="width:25%; text-align:center">Range</th>
    <th style="text-align:left">Description</th>
  </tr>
  <tr>
    <td><code>pitch</code></td>
    <td style="text-align:center">[-100%, 100%],<br/>
      [<code>x-low</code>, <code>low</code>, <code>default</code>,
      <code>high</code>, <code>x-high</code>]</td>
    <td>
      Normalized relative change of the average pitch contour
      level within safe limits. The attribute controls the perceived
      average tone level. It is borrowed from the <code>pitch</code>
      attribute of the SSML <code>&lt;prosody&gt;</code> element. It
      contributes to changing perceived speaker identity.
    </td>
  </tr>
  <tr>
    <td><code>pitch_range</code></td>
    <td style="text-align:center">[-100%, 100%],<br/>
      [<code>x-narrow</code>, <code>narrow</code>, <code>default</code>,
      <code>wide</code>, <code>x-wide</code>]</td>
    <td>
      Normalized relative change of the pitch contour dynamic range
      within safe limits. Increasing or decreasing the pitch range
      makes the speech style more or less expressive. The attribute
      is borrowed from the <code>range</code> attribute of the SSML
      <code>&lt;prosody&gt;</code> element.</td>
  </tr>
  <tr>
    <td><code>glottal_tension</code></td>
    <td style="text-align:center">[-100%, 100%],<br/>
      [<code>x-low</code>, <code>low</code>, <code>default</code>,
      <code>high</code>, <code>x-high</code>]</td>
    <td>
      Normalized relative change of the glottal tension within safe
      limits. Increasing or decreasing the glottal tension is perceived
      as a more tense or lax speech quality. A positive value might
      produce buzzing sounds, which you can alleviate by increasing
      the value of the <code>breathiness</code> attribute. A negative
      value is perceived as more breathy and generally more pleasant.
    </td>
  </tr>
  <tr>
    <td><code>breathiness</code></td>
    <td style="text-align:center">[-100%, 100%],<br/>
      [<code>x-low</code>, <code>low</code>, <code>default</code>,
      <code>high</code>, <code>x-high</code>]</td>
    <td>
      Normalized relative change of the perceived level of the aspiration
      noise within safe limits. Extreme values might produce either noisy
      speech (for positive breathiness) or a buzzing sound (for negative
      breathiness). Use this attribute to compensate for buzz or extra
      noise that is produced as a side effect of other attributes.
    </td>
  </tr>
  <tr>
    <td><code>rate</code></td>
    <td style="text-align:center">[-100%, 100%],<br/>
      [<code>x-slow</code>, <code>slow</code>, <code>default</code>,
      <code>fast</code>, <code>x-fast</code>]</td>
    <td>
      Normalized relative change of the speech rate within safe limits.
      Increasing or decreasing the rate makes speech faster or slower.
      A positive (faster) rate makes the perceived pitch range wider,
      and a negative (slower) rate perceptually narrows the pitch range.
      The attribute is borrowed from the <code>rate</code> attribute of
      the SSML <code>&lt;prosody&gt;</code> element.</td>
  </tr>
  <tr>
    <td><code>timbre</code></td>
    <td style="text-align:center">[<code>Sunrise</code>,
      <code>Breeze</code>]</td>
    <td>
      The case-sensitive name of one of the built-in vocal-tract
      transformations: <code>Sunrise</code> or <code>Breeze</code>.
      The names are symbolic. Experiment with the timbres to learn
      how they impact voice transformation. The attribute contributes
      to changing perceived speaker identity.
    </td>
  </tr>
  <tr>
    <td><code>timbre_extent</code></td>
    <td style="text-align:center">[0%, 100%]</td>
    <td>
      The extent of the <code>timbre</code> vocal-tract transformation:
      <code>0%</code> cancels the transformation; <code>100%</code>
      represents full application of the transformation. The attribute
      quantifies the difference between the transformed and original
      voices. It enables blending of the selected timbre with the timbre
      of the original voice. Even at moderate timbre extent values, the
      <code>timbre</code> attribute contributes to changing perceived
      speaker identity.
    </td>
  </tr>
</table>

### Using ranges
{: #ranges}

The numeric ranges of the different attributes indicate the extent to which the attribute affects the voice. For example, the `rate` attribute has a range of -100% to 100%:

-   A value of `100%` does not mean that the voice becomes 100% faster. It means that the service increases the rate of the voice to the maximum that it allows for that voice.
-   A value of `-100%` means that the service uses the minimum rate that it allows for the voice.
-   A value of `0%` represents the inherent level of the attribute for the voice; the voice remains unchanged.

### Using literal values
{: #literals}

As a convenience, many of the attributes also define literal values that you can use instead of percentages. The meanings of these values differ from the values that are used with the SSML `<prosody>` element. The `<voice-transformation>` element uses a scale that is consistent across its attributes.

-   `x-low`, `x-slow`, and `x-narrow` equal a value of `-100%`.
-   `low`, `slow`, and `narrow` equal a value of `-50%`.
-   `default` equals a value of `0%`, the default value for that attribute and voice.
-   `high`, `fast`, and `wide` equal a value of `+50%`.
-   `x-high`, `x-fast`, and `x-wide` equal a value of `+100%`.

### Usage guidelines
{: #guidelines}

Use the following guidelines and cautionary information:

-   For voice branding or multi-role applications, use the `timbre`, `pitch`, and `glottal_tension` attributes to change perceived speaker identity. You can use combinations of these three attributes to create virtual voices. Consider a virtual voice as a point in the multi-dimensional space that is realized by the specified timbre, pitch, and glottal tension. Different combinations of the attributes yield different virtual voices.
-   You can use the `pitch_range`, `breathiness`, and `rate` attributes to add flavor to a virtual voice. Other users can choose the same or similar attribute values, so the service cannot guarantee the uniqueness of your virtual voice.
-   Be aware of the following potential side effects of applying the attributes:
    -   High glottal tension, high pitch, and low rate can each cause buzzing sounds to occur. Increase the breathiness to mitigate the effect.
    -   Extremely low glottal tension can produce noisy speech. Decrease the breathiness to reduce the noise.
    -   Raising or lowering pitch range and rate to extreme degrees simultaneously can make speech sound unnatural.
-   As noted, some of the attributes are borrowed from the SSML `<prosody>` element. For more information, see [The prosody element](/docs/services/text-to-speech/SSML-elements.html#prosody_element). To enable fine prosody control of a virtual voice, you can
    -   Nest `<prosody>` elements within `<voice-transformation>` elements.
    -   Nest `<voice-transformation>` elements within `<prosody>` elements.

    You *cannot* nest `<voice-transformation>` elements.

## Custom transformation examples

The following examples apply different attributes to demonstrate possible applications of custom transformation. The first example decreases the glottal tension to make the voice softer. It also increases the pitch range and rate moderately to introduce a more dynamic speaking style.

```xml
<voice-transformation type="Custom" glottal_tension="-50%"
  pitch_range="30%" rate="10%">
  Do you have more information?
</voice-transformation>
```
{: codeblock}

The second example uses maximum glottal tension and pitch and minimum rate. Such combinations are generally not favorable and can produce a buzzing sound. The example mitigates this effect by increasing breathiness.

```xml
<voice-transformation type="Custom" glottal_tension="100%" pitch="100%"
  rate="-100%" breathiness="60%">
  Do you have more information?
</voice-transformation>
```
{: codeblock}

The next two examples change perceived speaker identity by applying timbre. The voice is altered by controlling the extent of the blending and by changing the pitch level. The first example uses the default timbre extent, 100%.

```xml
<voice-transformation type="Custom" timbre="Sunrise" pitch="40%">
  Do you have more information?
</voice-transformation>

<voice-transformation type="Custom" timbre="Breeze" timbre_extent="30%"
  pitch="-30%">
  Do you have more information?
</voice-transformation>
```
{: codeblock}

The final example uses multiple attributes to transform the voice. The example uses the default timbre extent and omits breathiness.

```xml
<voice-transformation type="Custom" timbre="Sunrise" pitch="-30%"
  pitch_range="80%" rate="60%" glottal_tension="-80%">
  Do you have more information?
</voice-transformation>
```
{: codeblock}
