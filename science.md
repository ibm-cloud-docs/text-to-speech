---

copyright:
  years: 2015, 2023
lastupdated: "2023-03-30"

subcollection: text-to-speech

---

{{site.data.keyword.attribute-definition-list}}

# The science behind the service
{: #science}

The {{site.data.keyword.texttospeechfull}} service offers only voices that rely on [neural voice technology](#science-neural): *expressive neural* and *enhanced neural* voices. A brief overview of neural voice technology follows. But the topic of synthesizing text to speech is inherently complex. For more information about the scientific research behind the service's speech technology, see the documents that are listed in [Research references](/docs/text-to-speech?topic=text-to-speech-references).
{: shortdesc}

## Neural voice technology
{: #science-neural}

Neural voice technology synthesizes human-quality speech from input text. The service first analyzes the input text to determine the desired content. The service uses an acoustic model that consists of a decision tree to generate candidate units for synthesis.

For each of the phones in a sequence of phones to be synthesized, the model considers the phone in the context of the preceding and following two phones. It then produces a set of acoustic units that are evaluated for fitness. This step reduces the complexity of the search by restricting it to only those units that meet some contextual criteria and discarding all others.

The service then uses three Deep Neural Networks (DNNs) to predict the acoustic (spectral) features of the speech and encode the resulting audio:

-   Prosody prediction
-   Acoustic feature prediction
-   Neural vocoder

During synthesis, the DNNs predict the pitch and phoneme duration (prosody), spectral structure, and waveform of the speech. For example, the prosody prediction module generates target values for the linguistic features that are extracted from the input text. The features include such attributes as part of speech, lexical stress, word-level prominence, and positional features such as the position of the syllable or word in the sentence.

The DNNs are trained on natural human speech to predict the acoustic features of the audio. This modular approach has the advantage of enabling fast and easy training, as well as independent control of each component. Once the base networks are trained, they can then be adapted to new speaking styles or voices for branding and personalization purposes.

Neural voices produce speech that is crisp and clear, with a very natural-sounding and smooth audio quality. For more information about the service's neural voice technology, see

-   The documentation [Languages and voices](/docs/text-to-speech?topic=text-to-speech-voices)
-   The research paper [High quality, lightweight and adaptable {{site.data.keyword.texttospeechshort}} using LPCNet](https://arxiv.org/abs/1905.00590){: external}
-   The research paper [Transplantation of Conversational Speaking Style with Interjections in Sequence-to-Sequence Speech Synthesis](https://arxiv.org/abs/2207.12262){: external}

## Concatenative synthesis
{: #science-concatenative}

All concatenative voices, also referred to as standard voices, were deprecated as of 2 December 2020. The following information is maintained for general information purposes only. For more information about the deprecation of the concatenative voices, see the [2 December 2020 service update](/docs/text-to-speech?topic=text-to-speech-release-notes#text-to-speech-2december2020) in the release notes for {{site.data.keyword.cloud_notm}}.
{: note}

Concatenative synthesis relies on an inventory of acoustic units from a large synthesis corpus to produce output speech for arbitrary input text. It is based on the following pipeline of processes. These processes facilitate an efficient, real-time search over this inventory of units followed by a post-processing of the units.

-   **Acoustic model** - This model consists of a decision tree that is responsible for generating candidate units for the search. For each of the phones in a sequence of phones to be synthesized, the model considers the phone in the context of the preceding and following two phones. It then produces a set of acoustic units that the search evaluates for fitness. This step effectively reduces the complexity of the search by restricting it to only those units that meet some contextual criteria and discarding all others.
-   **Prosody target models** - The prosody target models for some voices are based on Deep Recurrent Neural Networks (RNNs). For other voices, the models rely on decision trees to determine the prosody. In both cases, the models are responsible for generating target values for prosodic aspects of the speech (such as duration and intonation) given a sequence of linguistic features that are extracted from the input text. This list includes attributes such as part of speech, lexical stress, word-level prominence, and positional features (for example, the position of the syllable or word in the sentence). The prosody target models help guide the search toward those units that meet the prosodic criteria that are predicted by the models.
-   **Search** - Given the list of candidates that are returned by the acoustic model and the target prosody, this module carries out a Viterbi search. The search extracts a sequence of acoustic units that minimizes a cost function, which considers both concatenation and target costs. As a result, audible artifacts from joining two units are minimized, and the module tries to approximate the target prosody suggested by the prosody target models. This search also favors contiguous chunks in the synthesis corpus to further reduce such artifacts.
-   **Waveform generation** - When the search returns the optimal sequence of units, the system uses time-domain Pitch Synchronous Overlap and Add (PSOLA) to generate the output waveform. PSOLA is a digital signal-processing technique that is used for speech processing. Specifically, it is used for speech synthesis. It can modify the pitch and duration of a speech signal and blend the units that are returned by the search in a seamless way.

    For all of the linguistic features in the previous back-end processes, the service uses a text-processing front end to parse the text before it synthesizes the text into audio form. The front end sanitizes the text of any formatting artifacts such as HTML tags. It then uses a proprietary language that is driven by language-dependent linguistic rules to prepare the text and generate pronunciations. This module normalizes language-dependent features of the text such as dates, times, numbers, and currency. For example, it performs abbreviation expansion from a dictionary and numeric expansion from rules for ordinals and cardinals.

    Some words have multiple permissible pronunciations, so the text-processing front-end first produces a single, canonical pronunciation at run time. This approach might not reflect the pronunciation that the speaker used when the audio corpus was recorded. So the service augments a candidate set of pronunciations with alternative forms that are inventoried in an alternate-baseform dictionary. It lets the search choose forms that reduce cost in terms of pitch, duration, and contiguity concerns and constraints. This algorithm facilitates selection of longer contiguous chunks from the data set, resulting in an optimal flow of speech in the synthesized result.
