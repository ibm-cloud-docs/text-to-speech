---

copyright:
  years: 2015, 2018
lastupdated: "2018-05-21"

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

# The science behind the service
{: #science}

The {{site.data.keyword.texttospeechshort}} service is a concatenative system that relies on an inventory of acoustic units from a large synthesis corpus to produce output speech for arbitrary input text. It is based on the following pipeline of processes. These processes facilitate an efficient, real-time search over this inventory of units followed by a post-processing of the units.
{: shortdesc}

-   **Acoustic model** - This model consists of a decision tree that is responsible for generating candidate units for the search. For each of the phones in a sequence of phones to be synthesized, the model considers the phone in the context of the preceding and following two phones. It then produces a set of acoustic units that the search evaluates for fitness. This step effectively reduces the complexity of the search by restricting it to only those units that meet some contextual criteria and discarding all others.
-   **Prosody target models** - These models consist of Deep Recurrent Neural Networks (RNNs). The models are responsible for generating target values for prosodic aspects of the speech (such as duration and intonation) given a sequence of linguistic features that are extracted from the input text. This list includes attributes such as part of speech, lexical stress, word-level prominence, and positional features (for example, the position of the syllable or word in the sentence). The prosody target models help guide the search toward those units that meet the prosodic criteria that are predicted by this model.
-   **Search** - Given the list of candidates that are returned by the acoustic model and the target prosody, this module carries out a Viterbi search. The search extracts a sequence of acoustic units that minimizes a cost function, which considers both concatenation and target costs. As a result, audible artifacts from joining two units are minimized, and the module tries to approximate the target prosody suggested by the prosody target models. This search also favors contiguous chunks in the synthesis corpus to further reduce such artifacts.
-   **Waveform generation** - When the search returns the optimal sequence of units, the system uses time-domain Pitch Synchronous Overlap and Add (PSOLA) to generate the output waveform. PSOLA is a digital signal-processing technique that is used for speech processing. Specifically, it is used for speech synthesis. It can modify the pitch and duration of a speech signal and blend the units that are returned by the search in a seamless way.

    For all of the linguistic features in the previous back-end processes, the service uses a text-processing front end to parse the text before it synthesizes the text into audio form. The front end sanitizes the text of any formatting artifacts such as HTML tags. It then uses a proprietary language that is driven by language-dependent linguistic rules to prepare the text and generate pronunciations. This module normalizes language-dependent features of the text such as dates, times, numbers, and currency. For example, it performs abbreviation expansion from a dictionary and numeric expansion from rules for ordinals and cardinals.

    Some words have multiple permissible pronunciations, so the text-processing front-end first produces a single, canonical pronunciation at run time. This approach might not reflect the pronunciation that the speaker used when the audio corpus was recorded. So the service augments a candidate set of pronunciations with alternative forms that are inventoried in an alternate-baseform dictionary. It lets the search choose forms that reduce cost in terms of pitch, duration, and contiguity concerns and constraints. This algorithm facilitates selection of longer contiguous chunks from the data set, resulting in an optimal flow of speech in the synthesized result.

The topic of synthesizing text to speech is inherently complex, and any explanation of the service requires more explanatory depth than this brief summary can accommodate. For more information about the scientific research behind the service, see the documents that are listed in [Research references](/docs/services/text-to-speech/references.html).
