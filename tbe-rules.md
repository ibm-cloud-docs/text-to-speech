---

copyright:
  years: 2021, 2022
lastupdated: "2022-01-19"

subcollection: text-to-speech

---

{{site.data.keyword.attribute-definition-list}}

# Rules for creating custom prompts and speaker models
{: #tbe-rules}

The Tune by Example feature is beta functionality that is supported only for US English custom models and voices.
{: beta}

The service enforces the following rules for custom prompts and speakers models. Among the rules are guidelines for making the most effective use of the feature.
{: shortdesc}

## Rules for creating custom prompts
{: #tbe-rules-prompts}

The following rules apply to the identifier, text, and audio that you provide when adding a custom prompt to a custom model.

### Rules for prompt identifiers
{: #tbe-rules-prompts-identifiers}

For the identifier of a prompt:

-   Include a maximum of 49 characters.
-   Include only alphanumeric characters and `_` (underscores).
-   Do not include XML sensitive characters (double quotes, single quotes, ampersands, angle brackets, and slashes).
-   To add a new prompt, the ID must be unique for the specified custom model. Otherwise, the information for the prompt overwrites the existing prompt that has that ID.

### Rules for prompt text
{: #tbe-rules-prompts-text}

For the written text of a prompt:

-   Write the text of a prompt as you would normally, with commas and sentence-ending punctuation. However, Tune by Example bases the prosody and intonation of the prompt on the prompt audio, not on the punctuation of the prompt text as it does for regular speech synthesis. Only the spoken audio impacts the prosody of the synthesized prompt.
-   A prompt cannot contain more than 1000 characters of text. Speaking one or two sentences of text is the recommended limit.
-   A prompt can include only fixed, static text. It cannot include variable data, which is data that changes for different uses of the prompt. For example, "Your account balance is $500" contains variable data: namely, "$500," which is a variable value that changes depending on a user's account balance. In this case, the prompt needs to speak "Your account balance is," and a second synthesis request needs to say the balance.
-   Escape XML sensitive characters (double quotes, single quotes, ampersands, angle brackets, and slashes) that appear in the text of a prompt by applying the same rules that you use to provide text for a synthesis request. For more information, see [Escaping XML control characters](/docs/text-to-speech?topic=text-to-speech-usingHTTP#escape).
-   You can include SSML elements in the text of a prompt. For example, the pronunciation of words such as *read* or input that includes things like dates or numbers might be ambiguous. You might need to tell the service how to pronounce such words so that it knows for certain how to synchronize the input text with the audio. In most cases, however, the mapping of the phonemes and the text is obvious.

    For example, the SSML `<say-as>` element is used to indicate how the services says numbers, letters, and dates. This example directs the service to speak the individual digits of the value `123456` rather than to speak the value as a quantity in the hundreds of thousands:

    ```xml
    <speak version="1.1">
      <say-as interpret-as="digits">123456</say-as>
    </speak>
    ```
    {: codeblock}

    For more information, see [SSML elements](/docs/text-to-speech?topic=text-to-speech-elements) and [The say-as element](/docs/text-to-speech?topic=text-to-speech-elements#say-as_element).

### Rules for prompt audio
{: #tbe-rules-prompts-audio}

For the spoken audio of a prompt:

-   The audio must be in WAV format and must have a minimum sampling rate of 16 kHz. The service accepts audio with higher sampling rates, which it transcodes to 16 kHz before processing it.
-   The length of the prompt audio is limited to 30 seconds.
-   Ensure that the audio speaks the text of the prompt with prosody that reflects how you would like the prompt to be spoken by one of the service's voices. Here are some examples of ways to change prosody with a prompt:
    -   If you speak a question, make it sound like a question. For example, intonation tends to rise at the end of a question.
    -   If you speak a command, make it sound like a command. Emphasize the words of the phrase that indicate the command.
    -   Affect the speaking rate by accelerating or decelerating the voice at the word and syllable levels.
    -   Control the pitch by making words and syllables sound higher or lower. Pitch control is much more effective for prompts that have speaker models.
    -   Insert pauses to emphases certain aspects of the phrase. Leading and trailing pauses are removed.
-   You cannot change the pronunciation of a word. The service pronounces words according to its default vocabulary and any custom words that are defined for the model of the custom prompt. For more information, see [Tune by Example and word pronunciation](/docs/text-to-speech?topic=text-to-speech-tbe-intro#tbe-intro-how-pronunciation).
-   You cannot control the expressiveness (for example, happiness or sadness) of a phrase. These qualities are different from intonation and cannot be adequately captured by the feature.
-   You cannot control the loudness of a phrase. The service ignores the loudness of the spoken prompt.

## Rules for creating speaker models
{: #tbe-rules-speakers}

The following rules apply to the name and enrollment audio that you provide when creating a speaker model.

### Rules for speaker names
{: #tbe-rules-speakers-names}

For the name of a speaker model:

-   Include a maximum of 49 characters.
-   Include only alphanumeric characters and `_` (underscores).
-   Do not include XML sensitive characters (double quotes, single quotes, ampersands, angle brackets, and slashes).
-   Do not use the name of an existing speaker model that is already defined for the service instance. The name of a speaker model must be unique for its service instance. To re-create a speaker model for an existing speaker name, you must first delete the existing model that has that name.

### Rules for speaker audio
{: #tbe-rules-speakers-audio}

For the enrollment audio of a speaker model:

-   The audio must be in WAV format and must have a minimum sampling rate of 16 kHz. The service accepts audio with higher sampling rates, which it transcodes to 16 kHz before processing it.
-   The length of the enrollment audio is limited to 1 minute. Speaking one or two paragraphs of text that include five to ten sentences is recommended.
-   Say the enrollment audio as you would normally speak. This allows the service to determine your normal speaking voice and apply that information to prompts that are associated with the speaker model.
