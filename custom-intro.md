---

copyright:
  years: 2015, 2023
lastupdated: "2023-03-30"

subcollection: text-to-speech

---

{{site.data.keyword.attribute-definition-list}}

# Understanding customization
{: #customIntro}

When you synthesize text with {{site.data.keyword.texttospeechfull}}, the service applies language-dependent pronunciation rules. The service applies the rules to convert the ordinary (orthographic) spelling of each word to a phonetic spelling. A word's phonetic spelling uses phoneme symbols to define how the word is pronounced. These symbols are the distinct units of sound that distinguish words in a language, the boundaries between syllables, and the stress marks for the syllables.
{: shortdesc}

The service's regular pronunciation rules work well for common words. However, they can yield imperfect results for unusual words. Such words include domain-specific terms, words with foreign origins, personal or geographic names, and abbreviations or acronyms. If your application's lexicon includes such words, you can use the customization interface to specify how the service pronounces the words.

A custom model can also include custom prompts that you define for the Tune by Example feature. For more information about Tune by Example, custom prompts, and speaker models, see [Understanding Tune by Example](/docs/text-to-speech?topic=text-to-speech-tbe-intro).
{: note}

## Status and support
{: #customIntro-support}

The following status and support information applies to customization:

-   Customization is available for all languages.
-   [IBM Cloud]{: tag-ibm-cloud} You must have the Standard or Premium pricing plan to use customization. Users of the Lite plan cannot use the customization interface. For more information, see the {{site.data.keyword.texttospeechshort}} service in the [{{site.data.keyword.cloud}} Catalog](https://{DomainName}/catalog/text-to-speech){: external}.
-   [IBM Cloud]{: tag-ibm-cloud} Premium customers can work with {{site.data.keyword.IBM_notm}} to train a new custom voice for their specific application needs.To request a custom voice or for more information, complete and submit this [{{site.data.keyword.IBM_notm}} Request Form](https://forms.monday.com/forms/5fd92c54536a18f9afab8a47404bf828?r=use1){: external}.

## How customization works
{: #ciHow}

The customization interface of the {{site.data.keyword.texttospeechshort}} service creates a dictionary of words and their translations for a specific language. This dictionary is referred to as a *custom model*. Each custom entry in a custom model consists of a *word*/*translation* pair. A word's translation tells the service how to pronounce the word when it occurs in input text.

The customization interface provides methods to create and manage your custom models, which the service stores permanently. After you create a custom model, you can use it during synthesis with any version of the `/v1/synthesize` method. When the service synthesizes input text, it determines the pronunciation of words that appear in the custom model by applying their translations either directly or indirectly. Because you create a custom model for a specific language, a custom model can be used with any voice that is available in that language.

You specify the translation for a word in a custom model as a *sounds-like translation* or a *phonetic translation*. You can use both methods for entries in the same custom model, and you can mix the two methods within the same translation. A number of rules and guidelines apply to custom entries. For more information, see [Rules for creating custom entries](/docs/text-to-speech?topic=text-to-speech-rules).

## Sounds-like translation
{: #soundsLike}

*Sounds-like translation* uses the service's regular pronunciation rules to represent the pronunciation of a target word indirectly. A sounds-like translation is formed from the regular pronunciations of one or more other words. The service first substitutes the specified translation for any occurrence of the word that appears in the input text. It then applies its regular pronunciation rules to the translation, converting the translation to its phonetic representation to obtain the pronunciation.

For example, the service's regular pronunciation rules properly translate many common abbreviations and acronyms. The service pronounces the abbreviation *cm* as *centimeter*. It pronounces less common abbreviations letter by letter. For instance, the service pronounces the string *Str* (an abbreviation for *street*) as *S T R*, with each letter pronounced individually. You can use the sounds-like method to specify the translation *street* for the string *Str*.

Another example of an acronym is the word *IEEE*, which stands for Institute of Electrical and Electronic Engineers. By default, the service pronounces this acronym as *I E E E*. But the acronym is commonly pronounced *I triple E*, which you can easily define by using the simple sounds-like translation *I triple E*. If the word *IEEE* appears in your custom model with this translation, the service substitutes each occurrence of the word with the translation. It then applies its regular pronunciation rules to the individual words *I*, *triple*, and *E* to yield the common pronunciation.

You can apply the sounds-like method to more than just abbreviations and acronyms. It works equally well for complex or unusual words. For example, the following pair of sounds-like translations yields correct pronunciations for unusual words that are handled imperfectly by the service's regular pronunciation rules. Finding proper translations for such words can be more challenging than for simple abbreviations. The following examples use the regular pronunciation rules to alter the words' spelling for translation:

-   *Word*: `ayurvedic`, *Translation*: `aayervedic`
-   *Word*: `gastroenteritis`, *Translation*: `gastro enteritis`

As these examples show, developing sounds-like translations can be more trial-and-error than formulaic. You create a candidate translation based on your intuition and experience with the service. You then synthesize the word for the candidate translation as input text and listen to the resulting audio. If you are satisfied with the pronunciation, you can use the translation in your custom model; otherwise, you modify the translation and test it again.

## Phonetic translation
{: #phonetic}

The sounds-like method is a relatively simple and useful way of achieving a pronunciation. But it is not always possible to develop sounds-like translations. The direct alternative, the phonetic method, might appear to be more complicated and time-consuming, but it can achieve the pronunciation of any word.

*Phonetic translation* specifies a pronunciation in terms of phoneme symbols, syllable stress marks, and optional syllable boundaries that override the service's regular pronunciation rules. You specify a phonetic translation in one of the following formats:

-   The standard International Phonetic Alphabet (IPA) representation
-   The proprietary {{site.data.keyword.IBM_notm}} Symbolic Phonetic Representation (SPR)

In either case, you specify a translation by using a specific phoneme format that is based on the Speech Synthesis Markup Language (SSML). SSML is an XML-based markup language that provides annotations of text for speech-synthesis applications. You specify the phonetic translation for a word by using the SSML `<phoneme>` element:

`<phoneme alphabet="{ipa | ibm}" ph="{translation}"></phoneme>`

The `alphabet` attribute specifies the phonetic representation type: `ipa` or `ibm`. The `ph` attribute specifies the phonetic translation string.

For example, consider the word `trinitroglycerin`. The service's regular pronunciation rules produce a pronunciation that differs from the one commonly used by chemists and physicians. The correct pronunciation can be achieved with a phonetic translation:

-   *IPA*: `tɹaɪnˈaɪtɹəglɪsəɹɨn`
-   *SPR*: `trYn1YtrxglIsxrXn`

In these examples, the phonetic translation string is composed of phoneme symbols and a single primary stress mark. The primary stress mark is represented by `ˈ` in IPA and by `1` in SPR. It is placed just before the symbol for the stressed vowel in both cases. Although the examples do not show it, you can also specify syllable boundaries and secondary stress positions in a phonetic translation. These elements are not required and normally are not needed to achieve a pronunciation. As with sounds-like translations, you can compose a phonetic translation from multiple strings that are delimited by spaces.

You can also specify IPA translations as IPA Unicode values. For more information, see [Understanding phonetic symbols](/docs/text-to-speech?topic=text-to-speech-symbols) and the language-specific tables on the pages that are referred to from [Phonetic symbols for supported languages](/docs/text-to-speech?topic=text-to-speech-symbols#supportedLanguages). For an example translation that uses IPA Unicode values, see [The phoneme element](/docs/text-to-speech?topic=text-to-speech-elements#phoneme_element).
{: note}

### Working with an existing phonetic translation
{: #phoneticMethod}

Unless you are an expert in phonology, composing phonetic translations is not an easy task. It is always easier to edit an existing phonetic translation than to compose one from scratch. To help you create phonetic translations, the service's API includes a `GET /v1/pronunciation` method. The method returns the IPA or SPR representation that is generated by the service's regular pronunciation rules for a word in a specified language. You can also request the pronunciation for a word from a specified custom model to see the translation in the language of that model.

You can use the `/GET v/1/pronunciation` method to obtain an initial phonetic translation for a word. You can then modify the translation to achieve the pronunciation that you want. As with the sounds-like method, you follow a trial-and-error process. You submit your candidate translation to the service, synthesize the word as input text, listen to the resulting audio, and edit the candidate translation. You can repeat the process until you are satisfied with the pronunciation.

For more information, see [Querying a word from a language](/docs/text-to-speech?topic=text-to-speech-customWords#cuWordsQueryLanguage).

### More information about phonetic translation
{: #phoneticInfo}

The following resources provide information about phonetic translation:

-   For more information about using SSML and its `<phoneme>` element, see [Understanding SSML](/docs/text-to-speech?topic=text-to-speech-ssml).
-   For more information about specifying SPR and IPA symbols and translations, see [Understanding phonetic symbols](/docs/text-to-speech?topic=text-to-speech-symbols).

## Mixed sounds-like and phonetic translation
{: #mixed-translation}

You can mix the sounds-like and phonetic methods in the same translation. This feature can reduce the work that is involved in composing a translation.

For instance, assume that you used the sounds-like method to get part of a word pronounced satisfactorily. But you now need to fine-tune the remaining elements of the word. You can use the phonetic method to specify the difficult aspects of the word. The following example applies mixed translation to the word `trinitroglycerin`:

`try<phoneme alphabet="ipa" ph="nˈaɪtɹəglɪsəɹɨn"></phoneme>`
