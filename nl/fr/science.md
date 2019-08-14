---

copyright:
  years: 2015, 2019
lastupdated: "2019-07-08"

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

# Disciplines scientifiques sous-jacentes au service
{: #science}

Le service {{site.data.keyword.texttospeechfull}} propose des voix qui s'appuient sur deux types de technologie, la première reposant sur les [voix neuronales](#science-neural), la seconde utilisant la fonctionnalité de [synthèse concaténative](#science-concatenative). Les deux technologies synthétisent le discours à partir d'un texte en entrée mais elles ne se servent pas de la même approche pour produire de l'audio via des caractéristiques différentes. Les voix neuronales (`V3`) sont des versions optimisées des voix concaténatives d'origine du service.
{: shortdesc}

La synthétisation du texte en parole est un sujet intrinsèquement complexe. Pour plus d'informations sur les recherches scientifiques relatives aux technologies vocales sur lesquelles repose ce service, voir les documents répertoriés dans [Références de recherche](/docs/services/text-to-speech?topic=text-to-speech-references).

## Technologie des voix neuronales
{: #science-neural}

La technologie des voix neuronales synthétise un discours similaire à celui d'un être humain à partir d'un texte entré par un utilisateur. Le service analyse d'abord le texte en entrée pour déterminer le contenu souhaité. Comme avec ses modèles concaténatifs, le service utilise un modèle acoustique composé d'un arbre de décision pour générer des unités candidates à la synthèse.

Pour chacun des phonèmes d'une séquence de phonèmes à synthétiser, le modèle considère le phonème dans le contexte du phonème qui précède et de celui qui suit. Il produit ensuite un ensemble d’unités acoustiques qui sont évaluées pour en déterminer la pertinence. Cette étape réduit la complexité de la recherche en la limitant aux seules unités répondant à certains critères contextuels et en supprimant toutes les autres.

Le service utilise ensuite trois réseaux DNN (Deep Neural Network) pour prédire les caractéristiques acoustiques (spectrales) du discours et encoder l'audio obtenu :

-   Prédiction de prosodie
-   Prédiction de fonction acoustique
-   Vocodeur neuronal

Lors de la synthèse, les réseaux DNN prédisent la tonalité et la durée du phonème (prosodie), la structure spectrale et la forme du signal vocal du discours. Ainsi, les modules de prédiction de prosodie génèrent des valeurs cible pour les fonctions linguistiques qui sont extraites du texte en entrée. Les fonctions proposées incluent par exemple les attributs suivants : partie du discours, accentuation lexicale, importance des niveaux de mots et caractéristiques de positionnement telles que la position de la syllabe ou du mot dans la phrase.

L'entraînement des réseaux DNN s'appuie sur le discours humain naturel pour prédire les fonctions acoustiques de l'audio. Cette approche modulaire a l'avantage de permettre une formation rapide et facile ainsi qu'un contrôle indépendant de chaque composant. Une fois que les réseaux de base ont été formés, ils peuvent être adaptés à de nouveaux styles de conversation ou à de nouvelles voix, afin de se conformer à une image de marque particulière ou à mettre en oeuvre une personnalisation spécifique.

Les voix neuronales produisent un discours net et clair, avec une qualité audio douce et très naturelle. Pour plus d'informations sur la technologie des voix neuronales, voir 

-   L'article de blogue [IBM Watson Text to Speech: Neural Voices Generally Available](https://medium.com/ibm-watson/ibm-watson-text-to-speech-neural-voices-added-to-service-e562106ff9c7){: external}
-   Le document de recherche [High quality, lightweight and adaptable TTS (Text to Speech) using LPCNet](https://arxiv.org/abs/1905.00590){: external}

## Synthèse concaténative
{: #science-concatenative}

La synthèse concaténative s'appuie sur un inventaire d'unités acoustiques issu d'un grand corpus de synthèse pour produire un discours en sortie correspondant à du texte en entrée arbitraire. Il est basé sur le déroulement de processus suivant. Ces processus facilitent une recherche efficace et en temps réel sur cet inventaire d'unités suivi d'un post-traitement des unités.

-   **Modèle acoustique** - ce modèle se compose d'un arbre de décision chargé de générer des unités candidates pour la recherche. Pour chacun des phonèmes d'une séquence de phonèmes à synthétiser, le modèle considère le phonème dans le contexte du phonème qui précède et de celui qui suit. Il produit ensuite un ensemble d’unités acoustiques que la recherche évalue pour en déterminer la pertinence. Cette étape réduit efficacement la complexité de la recherche en la limitant aux seules unités répondant à certains critères contextuels et en supprimant toutes les autres.
-   **Modèles cible de prosodie** - pour certaines voix, ces modèles sont basés sur les réseaux RNN (Deep Recurrent Neural Network). Pour d'autres voix, ils s'appuient sur des arbres de décision pour déterminer la prosodie. Dans les deux cas, les modèles sont chargés de générer des valeurs cible pour les aspects prosodiques du discours (telles que la durée et l'intonation) à partir d'une séquence de fonctions linguistiques extraites du texte en entrée. Cette liste comprend des attributs tels que partie du discours, accentuation lexicale, importance du mot et caractéristiques de positionnement (par exemple, la place de la syllabe ou du mot dans la phrase). Les modèles cible de prosodie aident à orienter la recherche vers les unités qui répondent aux critères prosodiques prédits par les modèles.
-   **Recherche** - Etant donné la liste des candidats renvoyés par le modèle acoustique et la prosodie cible, ce module effectue une recherche de Viterbi. La recherche extrait une séquence d'unités acoustiques minimisant une fonction de coût, qui prend en compte à la fois les coûts de concaténation et les coûts cibles. En conséquence, les artefacts audibles issus de la jonction de deux unités sont minimisés et le module tente de se rapprocher de la prosodie cible suggérée par les modèles cibles de prosodie. Cette recherche favorise également les fragments contigus dans le corpus de synthèse afin de réduire davantage ces artefacts.
-   **Génération de signal vocal** - Lorsque la recherche renvoie la séquence optimale d'unités, le système utilise la technique PSOLA (Pitch Synchronous Overlap and Add) temps-domaine pour générer le signal de sortie. PSOLA est une technique de traitement du signal numérique utilisée pour le traitement de la parole. Plus précisément, elle est utilisée pour la synthèse vocale. Elle permet de modifier la hauteur et la durée d'un signal vocal et de mélanger les unités renvoyées par la recherche de manière transparente.

    Pour toutes les fonctionnalités linguistiques des processus d'arrière-plan précédents, le service utilise un système frontal de traitement de texte pour analyser le texte avant de le synthétiser sous forme audio. Le serveur frontal désinfecte le texte de tout artefact de formatage tel que les balises HTML. Il utilise ensuite un langage propriétaire basé sur des règles linguistiques dépendantes de la langue pour préparer le texte et générer des prononciations. Ce module normalise les caractéristiques du texte dépendantes de la langue, telles que les dates, les heures, les nombres et la devise. Par exemple, il effectue le développement des abréviations à partir d'un dictionnaire et le développement numérique à partir de règles pour les ordinaux et les cardinaux.

    Certains mots ayant plusieurs prononciations autorisées, le système frontal de traitement de texte génère d'abord une prononciation unique et canonique au moment de l'exécution. Cette approche peut ne pas refléter la prononciation utilisée par le locuteur lors de l'enregistrement du corpus audio. Le service développe donc un ensemble candidat de prononciations à l'aide de formes alternatives inventoriées dans un dictionnaire de bases alternatives. Il permet à la recherche de choisir des formes qui réduisent le coût en termes de problèmes et de contraintes de hauteur, durée et contiguïté. Cet algorithme facilite la sélection de blocs contigus plus longs dans l'ensemble de données, ce qui permet d'obtenir un flux de parole optimal dans le résultat synthétisé.
