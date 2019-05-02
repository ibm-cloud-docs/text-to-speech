---

copyright:
  years: 2015, 2019
lastupdated: "2019-04-08"

subcollection: text-to-speech

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

# A propos
{: #about}

> ** Mise à jour du service :** *le service {{site.data.keyword.texttospeechshort}} a été mis à jour le 24 mars 2019. Le service propose désormais des versions DNN (Deep Neural Network) de ses voix allemandes. Toutes les voix basées sur DNN prennent désormais en charge les attributs `pitch` et `rate` de l'élément `<prosody>` SSML. Pour plus d'informations, voir la [mise à jour du service du 24 mars 2019](/docs/services/text-to-speech/release-notes.html#March2019c) dans les notes sur l'édition*.

Le service {{site.data.keyword.texttospeechfull}} fournit une interface de programme d'application (API) qui utilise les fonctionnalités de synthèse vocale d'{{site.data.keyword.IBM_notm}} pour convertir le texte écrit en parole naturelle. Le service retransmet les résultats au client dans un délai minimal. Le service propose des interfaces [HTTP](/docs/services/text-to-speech/http.html) et [WebSocket](/docs/services/text-to-speech/websockets.html). 

## Fonctions et capacités

Le service {{site.data.keyword.texttospeechshort}} offre les fonctions et les capacités suivantes : 

-   **Formats audio** - Produit un son au format Ogg ou WebM avec les codecs Opus ou Vorbis, WAV, FLAC, MP3 (MPEG), l16 (PCM), mulaw ou au format de base. Pour plus d'informations, voir [Formats audio](/docs/services/text-to-speech/audio-formats.html).
-   **Voix** - Synthétise le texte en audio dans différentes langues, voix et dialectes. Le service propose des versions basées sur DNN de certaines voix. Pour plus d'informations, voir [Langues et voix](/docs/services/text-to-speech/voices.html).
-   **SSML** - Accepte le texte brut ou le texte marqué avec le langage XML (Speech Synthesis Markup Language). Pour plus d'informations, voir [Utilisation de SSML](/docs/services/text-to-speech/SSML.html).
-   **Expressivité** - Etend SSML avec un élément expressif que vous pouvez utiliser pour indiquer un style oral *GoodNews* (Bonnes nouvelles), *Apology* (Excuses) ou *Uncertainty* (Incertitude). Disponible uniquement pour la voix US English Allison qui n'est pas basée sur DNN. Pour plus d'informations, voir [SSML d'expressivité](/docs/services/text-to-speech/SSML-expressive.html).
-   **Transformation vocale** - Etend SSML en ajoutant un élément de transformation vocale. Vous pouvez utiliser cet élément pour élargir la plage de voix possibles en contrôlant des aspects tels que la hauteur, le débit et le timbre. Offre également deux voix virtuelles intégrées *Jeune* et *Douce*. Fonctionnalité disponible uniquement pour les voix en anglais américain qui ne sont pas basées sur DNN. Pour plus d'informations, voir [SSML de la transformation vocale](/docs/services/text-to-speech/SSML-transformation.html).
-   **Synchronisation des mots** - Avec l'interface WebSocket, prend en charge l'élément `<mark>` SSML et des informations facultatives de minutage des mots pour toutes les chaînes du texte en entrée. Les informations de minutage permettent de synchroniser le texte d'entrée et l'audio obtenu. Pour plus d'informations, voir [Obtention du minutage des mots](/docs/services/text-to-speech/word-timing.html).
-   **Personnalisation** - Offre une interface de personnalisation qui vous permet de spécifier la façon dont le service prononce les mots inhabituels qui apparaissent dans votre saisie. Vous pouvez définir des prononciations avec l'alphabet phonétique international (IPA) ou la représentation phonétique symbolique {{site.data.keyword.IBM_notm}} (SPR). Pour plus d'informations, voir [Compréhension de la personnalisation](/docs/services/text-to-speech/custom-intro.html).

Pour plus d'informations sur les forfaits du service, voir le service {{site.data.keyword.texttospeechshort}} dans le [Catalogue {{site.data.keyword.cloud_notm}} ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://{DomainName}/catalog/services/text-to-speech){: new_window}.

## Support de langue 
{: #languages-index}

Le service prend en charge les voix dans les langues suivantes : portugais brésilien, anglais (dialectes britannique et américain), français, allemand, italien, japonais et espagnol (dialectes castillan, latino-américain et nord-américain). Le service offre au moins une voix masculine ou féminine, parfois les deux, pour chaque langue. Chaque voix utilise une cadence et une intonation appropriées pour son dialecte. Pour plus d'informations sur les voix disponibles pour chaque langue, voir [Langues et voix](/docs/services/text-to-speech/voices.html).

## Scénarios d'utilisation 
{: #usecases}

Ce service convient aux applications vocales et sans écran, où l'audio est la méthode de sortie préférée: 

-   Interfaces pour les personnes handicapées, tels que des outils d'assistance pour les malvoyants 
-   Lecture de texte et de messages électroniques à voix haute aux conducteurs 
-   Narration de scénario vidéo et voix off de vidéo 
-   Outils pédagogiques basés sur la lecture 
-   Solutions domotiques 

## Essayez le service 

Pour des exemples du service en action, voir 

-   Une [démonstration rapide ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://text-to-speech-demo.ng.bluemix.net/){: new_window} du service {{site.data.keyword.texttospeechshort}} qui accepte du texte et génère la parole avec différentes voix. Il offre les fonctionnalités d'expressivité et de transformation vocale lorsqu'elles sont prises en charge. 
-   Des applications dans les [kits de démarrage {{site.data.keyword.ibmwatson}} ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](http://www.ibm.com/watson/developercloud/starter-kits.html){: new_window} qui illustrent le service {{site.data.keyword.texttospeechshort}}.
