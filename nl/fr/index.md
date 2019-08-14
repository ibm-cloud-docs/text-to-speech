---

copyright:
  years: 2015, 2019
lastupdated: "2019-07-30"

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

# A propos
{: #about}

> ** Mise à jour du service :** *le service {{site.data.keyword.texttospeechshort}} a été mis à jour le 30 juillet 2019. Il prend désormais en charge une voix neuronale en japonais : `ja-JP_EmiV3Voice`. Pour plus d'informations, voir la [mise à jour du service du 30 juillet 2019](/docs/services/text-to-speech?topic=text-to-speech-release-notes#July2019) dans les notes sur l'édition*.

Le service {{site.data.keyword.texttospeechfull}} fournit une interface de programme d'application (API) qui utilise les fonctionnalités de synthèse vocale d'{{site.data.keyword.IBM_notm}} pour convertir le texte écrit en parole naturelle. Le service retransmet les résultats au client dans un délai minimal. Le service propose des interfaces [HTTP](/docs/services/text-to-speech?topic=text-to-speech-usingHTTP) et [WebSocket](/docs/services/text-to-speech?topic=text-to-speech-usingWebSocket).

## Fonctions et capacités

Le service {{site.data.keyword.texttospeechshort}} offre les fonctions et les capacités suivantes :

-   **Formats audio** - Produit un son au format Ogg ou WebM avec les codecs Opus ou Vorbis, WAV, FLAC, MP3 (MPEG), l16 (PCM), mulaw ou au format de base. Pour plus d'informations, voir [Formats audio](/docs/services/text-to-speech?topic=text-to-speech-audioFormats).
-   **Voix** - Synthétise le texte en audio dans différentes langues, voix et dialectes. Le service offre à la fois des versions standard (concaténatives) et des versions neuronales de la plupart des voix. Pour plus d'informations, voir [Langues et voix](/docs/services/text-to-speech?topic=text-to-speech-voices).
-   **SSML** - Accepte le texte brut ou le texte marqué avec le langage XML (Speech Synthesis Markup Language). Pour plus d'informations, voir [Utilisation de SSML](/docs/services/text-to-speech?topic=text-to-speech-ssml).
-   **Expressivité** - Etend SSML avec un élément expressif que vous pouvez utiliser pour indiquer un style oral *GoodNews* (Bonnes nouvelles), *Apology* (Excuses) ou *Uncertainty* (Incertitude). Disponible uniquement pour la voix standard Allison en anglais américain. Pour plus d'informations, voir [SSML d'expressivité](/docs/services/text-to-speech?topic=text-to-speech-expressive).
-   **Transformation vocale** - Etend SSML en ajoutant un élément de transformation vocale. Vous pouvez utiliser cet élément pour élargir la plage de voix possibles en contrôlant des aspects tels que la hauteur, le débit et le timbre. Offre également deux voix virtuelles intégrées *Jeune* et *Douce*. Disponible uniquement pour les voix standard en anglais américain. Pour plus d'informations, voir [SSML de la transformation vocale](/docs/services/text-to-speech?topic=text-to-speech-transformation).
-   **Synchronisation des mots** - Avec l'interface WebSocket, prend en charge l'élément `<mark>` SSML et des informations facultatives de minutage des mots pour toutes les chaînes du texte en entrée. Les informations de minutage permettent de synchroniser le texte d'entrée et l'audio obtenu. Pour plus d'informations, voir [Obtention du minutage des mots](/docs/services/text-to-speech?topic=text-to-speech-timing).
-   **Personnalisation** - Offre une interface de personnalisation qui vous permet de spécifier la façon dont le service prononce les mots inhabituels qui apparaissent dans votre saisie. Vous pouvez définir des prononciations avec l'alphabet phonétique international (IPA) ou la représentation phonétique symbolique {{site.data.keyword.IBM_notm}} (SPR). Pour plus d'informations, voir [Compréhension de la personnalisation](/docs/services/text-to-speech?topic=text-to-speech-customIntro).

Pour plus d'informations sur les plans de tarification du service, voir le service {{site.data.keyword.texttospeechshort}} dans le catalogue [{{site.data.keyword.cloud_notm}}](https://{DomainName}/catalog/services/text-to-speech){: external}.

## Support de langue
{: #languages-index}

Le service prend en charge les voix dans les langues suivantes : portugais brésilien, anglais (dialectes britannique et américain), français, allemand, italien, japonais et espagnol (dialectes castillan, latino-américain et nord-américain).

Le service offre au moins une voix féminine pour chaque langue. Pour certaines langues, le service propose plusieurs voix, incluant des voix masculines et féminines. Chaque voix utilise une cadence et une intonation appropriées pour son dialecte. Le service offre à la fois des versions standard et neuronales de la plupart des voix.

Pour plus d'informations sur les voix disponibles pour chaque langue, voir [Langues et voix](/docs/services/text-to-speech?topic=text-to-speech-voices).

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

-   [Une démonstration rapide](https://text-to-speech-demo.ng.bluemix.net/){: external} du service {{site.data.keyword.texttospeechshort}}, qui accepte du texte et génère un discours prononcé avec des voix différentes, choisies par l'utilisateur. Ce service offre les fonctionnalités d'expressivité et de transformation vocale, si elles sont prises en charge.
-   Des applications dans les kits de démarrage {{site.data.keyword.ibmwatson}} [](http://www.ibm.com/watson/developercloud/starter-kits.html){: external} qui illustrent le service {{site.data.keyword.texttospeechshort}}.
