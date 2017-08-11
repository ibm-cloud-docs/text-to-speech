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

# The science behind the service
{: #science}

The {{site.data.keyword.texttospeechshort}} service is a concatenative system that relies on an inventory of acoustic units from a large synthesis corpus to produce output speech for arbitrary input text. It is based on the following pipeline of processes that facilitate an efficient, real-time search over this inventory of units followed by a post-processing of the units:
{: shortdesc}

-   **Acoustic model:** This model consists of a Decision Tree (DT) that is responsible for generating candidate units for the search. For each of the phones in a sequence of phones to be synthesized, the model takes the phone (plus a context of the preceding and following two phones) and produces a set of acoustic units that the search evaluates for fitness. This step effectively reduces the complexity of the search by restricting it to only those units that meet some contextual criteria and discarding all others.
-   **Prosody target models:** These models consist of Deep Recurrent Neural Networks (RNNs). The models are responsible for generating target values for prosodic aspects of the speech (such as duration and intonation) given a sequence of linguistic features extracted from the input text. This list includes attributes such as part of speech, lexical stress, word-level prominence, and positional features (for example, the position of the syllable or word in the sentence). The prosody target models help guide the search toward those units that meet the prosodic criteria predicted by this model.
-   **Search:** Given the list of candidates returned by the acoustic model and the target prosody, this module carries out a Viterbi search to extract a sequence of acoustic units that minimizes a cost function that takes into account both concatenation and target costs. As a result, audible artifacts from joining two units are minimized while trying to approximate the target prosody suggested by the prosody target models. This search also favors contiguous chunks in the synthesis corpus to further reduce such artifacts.
-   **Waveform generation:** Once the search has returned the optimal sequence of units, the system uses time-domain Pitch Synchronous Overlap and Add (PSOLA) to generate the output waveform. PSOLA is a digital signal-processing technique that is used for speech processing and, more specifically, for speech synthesis. It can modify the pitch and duration of a speech signal and blend the units that are returned by the search in a seamless way.

    For all of the linguistic features needed in the the previous back-end processes, the service uses a text-processing front-end to parse the text before synthesizing it into audio form. This front-end sanitizes the text of any formatting artifacts such as HTML tags. It then uses a proprietary language that is driven by language-dependent linguistic rules to prepare the text and generate pronunciations. This module normalizes language-dependent features of the text such as dates, times, numbers, currency, and so on. For example, it performs abbreviation expansion from a dictionary and numeric expansion from rules for ordinals and cardinals.

    Some words have multiple permissible pronunciations, so the text-processing front-end first produces a single, canonical pronunciation at runtime. Because this approach may not reflect the pronunciation the speaker used when the audio corpus was recorded, the service augments a candidate set of pronunciations with alternative forms inventoried in an alternate-baseform dictionary and lets the search choose forms that result in lower cost in terms of pitch, duration, and contiguity concerns and constraints. This algorithm facilitates selection of longer contiguous chunks from the data set, resulting in an optimal flow of speech in the synthesized result.

The topic of synthesizing text to speech is inherently complex, and any explanation of the service requires more explanatory depth than this brief summary can accommodate. For more information about the scientific research behind the service, see the documents listed in [Research references](/docs/services/text-to-speech/references.html).
