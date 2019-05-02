---

copyright:
  years: 2015, 2019
lastupdated: "2019-03-07"

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

# Disciplines scientifiques sous-jacentes au service 
{: #science}

Le service {{site.data.keyword.texttospeechshort}} est un système concaténatif qui repose sur un inventaire d'unités acoustiques issu d'un grand corpus de synthèse afin de produire un discours en sortie correspondant à du texte d'entrée arbitraire. Il est basé sur le déroulement de processus suivant. Ces processus facilitent une recherche efficace et en temps réel sur cet inventaire d'unités suivi d'un post-traitement des unités.
{: shortdesc}

-   **Modèle acoustique** - Ce modèle consiste en un arbre de décision chargé de générer des unités candidates pour la recherche. Pour chacun des téléphones d'une séquence de téléphones à synthétiser, le modèle considère le téléphone dans le contexte des deux téléphones précédent et suivant. Il produit ensuite un ensemble d’unités acoustiques que la recherche évalue pour déterminer la pertinence. Cette étape réduit efficacement la complexité de la recherche en la limitant aux seules unités répondant à certains critères contextuels et en supprimant toutes les autres. 
-   **Modèles cibles de prosodie** - Ces modèles sont constitués de réseaux RNN (Deep Recurrent Neural Network). Les modèles sont chargés de générer des valeurs cibles pour les aspects prosodiques de la parole (telles que la durée et l'intonation) à partir d'une séquence de fonctions linguistiques extraites du texte en entrée. Cette liste comprend des attributs tels que partie du discours, accentuation lexicale, importance du mot et caractéristiques de positionnement (par exemple, la place de la syllabe ou du mot dans la phrase). Les modèles cibles de prosodie aident à orienter la recherche vers les unités qui répondent aux critères prosodiques prédits par ce modèle. 
-   **Recherche** - Etant donné la liste des candidats renvoyés par le modèle acoustique et la prosodie cible, ce module effectue une recherche de Viterbi. La recherche extrait une séquence d'unités acoustiques minimisant une fonction de coût, qui prend en compte à la fois les coûts de concaténation et les coûts cibles. En conséquence, les artefacts audibles issus de la jonction de deux unités sont minimisés et le module tente de se rapprocher de la prosodie cible suggérée par les modèles cibles de prosodie. Cette recherche favorise également les fragments contigus dans le corpus de synthèse afin de réduire davantage ces artefacts. 
-   **Génération de signal vocal** - Lorsque la recherche renvoie la séquence optimale d'unités, le système utilise la technique PSOLA (Pitch Synchronous Overlap and Add) temps-domaine pour générer le signal de sortie. PSOLA est une technique de traitement du signal numérique utilisée pour le traitement de la parole. Plus précisément, elle est utilisée pour la synthèse vocale. Elle permet de modifier la hauteur et la durée d'un signal vocal et de mélanger les unités renvoyées par la recherche de manière transparente. 

    Pour toutes les fonctionnalités linguistiques des processus d'arrière-plan précédents, le service utilise un système frontal de traitement de texte pour analyser le texte avant de le synthétiser sous forme audio. Le serveur frontal désinfecte le texte de tout artefact de formatage tel que les balises HTML. Il utilise ensuite un langage propriétaire basé sur des règles linguistiques dépendantes de la langue pour préparer le texte et générer des prononciations. Ce module normalise les caractéristiques du texte dépendantes de la langue, telles que les dates, les heures, les nombres et la devise. Par exemple, il effectue le développement des abréviations à partir d'un dictionnaire et le développement numérique à partir de règles pour les ordinaux et les cardinaux. 

    Certains mots ayant plusieurs prononciations autorisées, le système frontal de traitement de texte génère d'abord une prononciation unique et canonique au moment de l'exécution. Cette approche peut ne pas refléter la prononciation utilisée par le locuteur lors de l'enregistrement du corpus audio. Le service développe donc un ensemble candidat de prononciations à l'aide de formes alternatives inventoriées dans un dictionnaire de bases alternatives. Il permet à la recherche de choisir des formes qui réduisent le coût en termes de problèmes et de contraintes de hauteur, durée et contiguïté. Cet algorithme facilite la sélection de blocs contigus plus longs dans l'ensemble de données, ce qui permet d'obtenir un flux de parole optimal dans le résultat synthétisé. 

Le sujet de la synthèse vocale est par nature complexe et toute explication du service nécessite une explication bien plus détaillée que ce bref résumé. Pour plus d'informations sur la recherche scientifique à l'origine de ce service, voir les documents répertoriés dans [Références de recherche](/docs/services/text-to-speech/references.html).
