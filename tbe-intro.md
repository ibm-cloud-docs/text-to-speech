---

copyright:
  years: 2021, 2023
lastupdated: "2023-01-14"

subcollection: text-to-speech

---

{{site.data.keyword.attribute-definition-list}}

# Understanding Tune by Example
{: #tbe-intro}

The Tune by Example feature is beta functionality that is supported only for US English custom models and voices.
{: beta}

The Tune by Example feature lets you control exactly how specified text is spoken by the service. The feature lets you dictate the intonation, stress, tempo, cadence, rhythm, and pauses of the synthesized text. These aspects of speech are collectively referred to as *prosody*.
{: shortdesc}

You create a custom prompt by providing a sample recording that speaks the text as you want to hear it, and the service duplicates the qualities of the recorded speech with its voices. The spoken prompt can emphasize different syllables or words, introduce pauses, and generally make the synthesized audio sound more natural and appropriate for the context in which the prompt is used.

The feature provides a simpler mechanism than standard SSML for modifying how speech is synthesized. For example, using attributes of the SSML `<prosody>` element can be difficult. Tune by Example eliminates the need for such SSML by letting you record text as you want it to be spoken by the service rather than requiring you to emulate the intended prosody with SSML elements and attributes.

You can further enhance the quality of a prompt by creating an optional speaker model that contains information about a speaker's voice. You create a speaker model by providing an audio sample of a user's voice. The service extracts information from the sample audio to train itself on the voice, which can help it produce higher-quality prompts for that speaker.

For an overview of the Tune by Example feature, including a demo with example scripts, see the blog [Tune by Example: How to Tune Watson Text to Speech for Better Intonations](https://medium.com/ibm-data-ai/tune-by-example-how-to-tune-watson-text-to-speech-for-better-intonations-bcee8404d927){: external}.

## Status and support
{: #tbe-intro-support}

The following status and support information applies to Tune by Example:

-   Tune by Example is beta functionality that is available only for US English. You can add prompts only to custom models whose language is `en-US`. You can use a custom prompt only with with US English voices.
-   Custom models, custom prompts, and speaker models are owned by the instance of the service whose credentials are used to create them. Request logging and data privacy are supported for all customization components. For more information about these topics, see [Usage notes for customization](/docs/text-to-speech?topic=text-to-speech-customModels#customGuidelines).
-   [IBM Cloud]{: tag-ibm-cloud} You must have the Standard or Premium pricing plan to use Tune by Example. The feature is part of customization, which is restricted to these plans. For more information, see the {{site.data.keyword.texttospeechshort}} service in the [{{site.data.keyword.cloud}} Catalog](https://{DomainName}/catalog/text-to-speech){: external}.

## How Tune by Example works
{: #tbe-intro-how}

During testing of an application, you might find that the service does not adequately synthesize some aspects of your text. In some cases, for example, you might want to change specific aspects of the audio such as which words are emphasized and the location or duration of pauses. In other cases, you might want to change more subtle aspects of the synthesis. For instance, you might feel that the synthesized audio sounds robotic, unnatural, or that the tone is unsatisfactory. These are the types of problems that Tune by Example can address.

To use the Tune by Example feature, you record a user who reads your text as you would like to hear it spoken by one of the service's voices. You then add your text and audio to a custom model in the form of a custom prompt. The service learns the preferred prosody of the text from the audio sample. When you include the prompt in a speech synthesis request by using the SSML extension `<ibm:prompt id="{prompt_id}"/>`, the voice that speaks the text of the prompt emulates the prosody of the prompt.

You can create an optional but recommended speaker model for a user who records spoken prompts. You then associate the speaker model with prompts that are spoken by that user. The addition of a speaker model can make an appreciable difference in the quality of a synthesized prompt. For example, the service can produce short prompts with more confidence if it knows the speaker's regular intonation. Because the lack of a defined speaker can potentially compromise the quality of a prompt, you are strongly encouraged to associate a speaker model with each custom prompt.

Because custom prompts are added to custom models, you must specify a prompt's custom model with a speech synthesis request to use that prompt. Speaker models, however, are independent from custom models. The relationship of speaker models to both custom models and custom prompts is one-to-many. The same speaker model can be associated with multiple prompts that are defined in different custom models. Moreover, you do not specify a speaker model with a synthesis request.

### Tune by Example and word pronunciation
{: #tbe-intro-how-pronunciation}

The service’s default pronunciation and tokenization rules might cause an unusual word that occurs in a prompt to be pronounced in an unsatisfactory way. However, Tune by Example is not intended to change a word's pronunciation. For example, the service pronounces the word "catastrophic" as one expects to hear it. You can use Tune by Example to change what syllables of the word are emphasized (for instance, "cataSTROPHic") or the tempo of the word (for instance "cat-a-strophic"). But you cannot use Tune by Example to change the word's default pronunciation.

To change how a word is pronounced, you use the service's customization interface to define an alternative pronunciation for the word. You add a custom word with the altered pronunciation to the same custom model as the prompt. The service then applies the pronunciation of the custom word when it occurs in a prompt. For more information, see [Understanding customization](/docs/text-to-speech?topic=text-to-speech-customIntro).

If you add or modify a custom word that is part of an existing prompt, the service continues to honor the pronunciation of the word that was in place when the prompt was created. This occurs because the service creates a prompt at a point in time, and it employs the pronunciation rules that are in effect at that time. You need to re-create a prompt to take advantage of a new or updated custom word.

When you re-create a prompt, the service replaces the existing prompt. The new prompt reflects any changes to the text or the audio of the prompt along with any custom word pronunciations defined since the prompt was first created. You can always pass the same text and audio that you used to create the original prompt if you are rerecording the prompt after adding a custom word.

## Custom prompts
{: #tbe-intro-custom-prompts}

A *custom prompt* is defined by text and audio that speaks that text with the prosody that you want the service's voices to duplicate. The service extracts and analyzes the prosody from the prompt's audio. It then applies that prosodic information when it speaks the prompt's text with one of its own voices.

It is important to understand that when you use a prompt during speech synthesis, the service does *not* use the audio of the prompt itself. It instead uses the voice that you specify with the synthesis request. That voice adopts the prosody of the spoken audio from the prompt.

When you add a prompt to a custom model, you define the prompt by providing the text that is to be spoken, the recorded audio for that text, a unique user-specified identifier for the prompt, and an optional speaker model. The service generates and stores prosodic data for the prompt and uses the data to produce synthesized audio upon request. You must use credentials for the instance of the service that owns a custom model to add a prompt to it.

Always assign a meaningful name as the value of a prompt ID. For example, use a name like `goodbye` to indicate a prompt that speaks a standard farewell message. Prompt IDs must be unique within a given custom model, so you cannot define two prompts with the same ID for the same model. If you provide the ID of an existing prompt, the previously uploaded prompt is replaced by the new information. The service reprocesses the existing prompt by using the new text and audio, and it updates the prosodic data that is associated with the prompt.

When it processes a request to add a prompt, the service attempts to align the text and the audio that are provided for the prompt. The text that is passed with a prompt must match the spoken audio as closely as possible. Optimally, the text and audio match exactly. The service does its best to align the specified text with the audio, and it can often compensate for mismatches between the two. But if the service cannot effectively align the text and the audio because the magnitude of differences between the two is too great, processing of the prompt fails.

Prompts are supported for use only with US English custom models and voices. The quality of a prompt is undefined if the language of a prompt does not match the language of its custom model. This is consistent with any text that is specified for a speech synthesis request. The service makes a best-effort attempt to render the specified text for the prompt. It does not validate that the language of the text matches the language of the model.

## Speaker models
{: #tbe-intro-speaker-models}

A *speaker model* is defined by an audio sample of a user's voice from which the service extracts information to train itself on that voice's characteristics. When the speaker model is associated with a custom prompt that is spoken by the same user, the service leverages its understanding of the speaker's voice to identify how the prosody of the prompt compares to the speaker's normal speech patterns. The speaker model serves as a baseline to distinguish prosodic features in the audio of the prompt.

When you create a speaker model, you provide enrollment audio and a name for the model that is unique within the context of the owning service instance:

-   The enrollment audio must include speech that is spoken by the user who is associated with the model. The service extracts information about the speaker's voice from the audio sample that you provide.
-   The name provides a human-readable handle for the model. The service returns a speaker ID, which is a globally unique identifier (GUID) (for example, `823068b2-ed4e-11ea-b6e0-7b6456aa95cc`) that you use to identify the speaker in subsequent requests to the service.

The service uses the information that it extracts from the audio to train itself on the speaker's pitch, cadence, and intonation. This information can make a significant difference in the quality of prompts that are associated with the model, especially short prompts with relatively little audio.

You create a speaker model for a given instance of the service. A single speaker model can be associated with multiple prompts that are defined for multiple custom models within that service instance. The gender of the speaker who creates a speaker model does not need to match the gender of a voice that is used with prompts that are associated with that speaker model. For example, a speaker model that is created by a male speaker can be associated with prompts that are spoken by female voices.
