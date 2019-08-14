---

copyright:
  years: 2015, 2019
lastupdated: "2019-06-23"

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

# Utilisation de SSML
{: #ssml}

SSML (Speech Synthesis Markup Language) est un langage de balisage basé sur XML qui fournit des annotations de texte pour les applications de synthèse vocale. Il s'agit d'une recommandation du groupe de travail Voice Browser du W3C qui a été adoptée comme langage de balisage standard pour la synthèse vocale par la spécification VoiceXML 2.0. SSML fournit aux développeurs d'applications vocales un moyen standard de contrôler certains aspects du processus de synthèse en leur permettant de spécifier la prononciation, le volume, la hauteur, la vitesse et d'autres attributs via un balisage.
{: shortdesc}

Avec le service {{site.data.keyword.texttospeechfull}}, vous pouvez utiliser SSML pour contrôler la synthèse de votre texte avec toutes les langues prises en charge. Cela inclut l'utilisation de l'élément `<phoneme>` pour définir la prononciation d'un mot dans l'alphabet phonétique international (IPA) ou la représentation phonétique symbolique {{site.data.keyword.IBM_notm}} (SPR). Le service s'appuie également sur l'élément `<phoneme>` SSML pour définir la traduction phonétique d'un mot avec son interface de personnalisation. Pour plus d'informations, voir [Compréhension de la personnalisation](/docs/services/text-to-speech?topic=text-to-speech-customIntro).

## Introduction à SSML
{: #introduction-SSML}

SSML agit en augmentant le texte brut transmis à un synthétiseur avec un ensemble prédéfini d’éléments ou balises. Un analyseur XML sépare d’abord le texte brut en entrée des spécifications du balisage. Les spécifications sont ensuite traitées et envoyées en tant qu'un ensemble d'instructions sous une forme que le synthétiseur peut comprendre pour produire les effets souhaités. Pour que l'analyseur XML puisse effectuer ce travail, le balisage doit être correctement formé. Par exemple, les éléments doivent être fermés et plusieurs éléments doivent être correctement imbriqués. Pour une introduction aux concepts XML de base, voir [Introduction to XML](http://www.w3schools.com/xml/xml_whatis.asp){: external}.

Un élément SSML est tout ce qui est contenu entre des balises d'ouverture et de fermeture, balises comprises. Comme illustré dans l'exemple suivant, un élément peut contenir une combinaison d'autres éléments (les balises peuvent être imbriquées) et du texte. De plus, les éléments peuvent nécessiter ou accepter éventuellement des attributs définis avec des valeurs particulières.

```xml
<tag1>
  <tag2 attributeName="attributeValue">
    ... some text ...
  </tag2>
</tag1>
```
{: codeblock}

Un document SSML légal complet consiste en un prologue XML, contenant des informations telles que le codage et le schéma permettant de valider le document SSML, suivi de l'élément racine `<speak>`. (Pour plus d'informations sur la structure du prologue, voir [tizag.com/xmlTutorial/xmlprolog.php](http://www.tizag.com/xmlTutorial/xmlprolog.php){: external}.) Dans la plage de l'élément `<speak>`, indiquez le texte à synthétiser, complété par des éléments supplémentaires.

```xml
<!-- The XML Prolog -->
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE speak PUBLIC "-//W3C//DTD SYNTHESIS 1.0//EN"
  "http://www.w3.org/TR/speech-synthesis/synthesis.dtd">

<!-- Root Element -->
<speak version="1.0" xmlns="www.w3.org/2001/10/synthesis"
  ... the body that contains text to be synthesized plus markup ...
</speak>
```
{: codeblock}

Le service prend en charge les fragments SSML, qui sont des éléments SSML qui n'incluent pas l'en-tête XML complet.

## Prise en charge de SSML
{: #ssmlSupport}

Le service {{site.data.keyword.texttospeechshort}} se base sur la version 1.0 de SSML, recommandée par le W3C le 7 septembre 2004. Pour plus d'informations sur la recommandation W3C SSML, voir[W3C - Speech Synthesis Markup Language (SSML) Version 1.1](http://www.w3.org/TR/speech-synthesis/){: external}.

Pour plus d'informations sur l'utilisation de SSML avec le service, voir :

-   Pour des informations complètes sur le niveau de prise en charge du service pour tous les éléments SSML, voir [Eléments SSML](/docs/services/text-to-speech?topic=text-to-speech-elements). A quelques exceptions près, le service implémente la plupart des spécifications W3C, ainsi que des fragments SSML.
-   Le service étend SSML avec un élément `<express-as>` qui indique comment le texte doit être exprimé lorsqu'il est parlé (ton de bonne nouvelle, excuse ou incertitude). Le service prend en charge l’expressivité uniquement pour la voix en anglais américain Allison. Voir [Utilisation de SSML expressif](/docs/services/text-to-speech?topic=text-to-speech-expressive).
-   Le service étend SSML avec un élément `<voice-transformation>` qui élargit la plage de voix possibles en vous permettant de contrôler la hauteur, la plage de hauteur, la tension glottale, la respiration, le débit et le timbre du texte parlé. Le service propose également deux voix virtuelles intégrées, *Young* et *Soft*. Le service prend en charge la transformation de la voix uniquement pour la voix en anglais américain. Voir [Utilisation de la transformation vocale SSML](/docs/services/text-to-speech?topic=text-to-speech-transformation).
-   L'interface de personnalisation du service prend en charge l'utilisation de l'élément `<phoneme>` SSML pour spécifier l'orthographe phonétique utilisée pour prononcer un mot. L'orthographe phonétique représente les sons d'un mot, la façon dont les sons sont divisés en syllabes et quelles syllabes sont accentuées.
    -   Pour plus d'informations sur l'interface de personnalisation, voir [Compréhension de la personnalisation](/docs/services/text-to-speech?topic=text-to-speech-customIntro).
    -   Pour plus d'informations sur les symboles valides que vous pouvez utiliser dans une spécification {{site.data.keyword.IBM_notm}} SPR ou IPA pour toute langue prise en charge, voir [Utilisation d'IBM SPR](/docs/services/text-to-speech?topic=text-to-speech-sprs).

## Validation du SSML
{: #errors}

Le service valide tous les éléments SSML que vous soumettez dans n'importe quel contenu, en tant que texte d'entrée pour la synthèse ou en tant que définition de la traduction d'un mot pour la personnalisation. Le service ne peut pas déterminer à l'avance si le texte soumis à la synthèse contient des éléments SSML. Par conséquent, il effectue la même validation pour tout le texte en entrée, qu'il contienne ou non du code SSML.

-   *Toutes les entrées SSML doivent être correctes et bien formées.* Le service ignore en mode silencieux les éléments SSML non pris en charge. Le service synthétise le texte contenu dans un élément non pris en charge ou un élément utilisant des fonctionnalités non prises en charge ; seul l'élément est ignoré.
-   *Le service signale un code d'erreur HTTP 400 pour les éléments non valides.* La réponse d'erreur inclut un message descriptif et la demande échoue.

Plus précisément, le service renvoie une erreur dans les cas suivants :

-   *Elément non valide.* Par exemple, vous spécifiez une balise de manière incorrecte, omettez un attribut obligatoire ou incluez une balise d'ouverture mais aucune balise de fermeture correspondante.
-   *Symbole non valide.* L'attribut `ph` d'un élément `<phoneme>` inclut un symbole IPA ou SPR non pris en charge pour le langage spécifié.
-   *Absence de voyelles.* L'attribut `ph` d'un élément `<phoneme>` spécifie une prononciation du mot qui n'inclut pas de voyelles.
-   *Liaison en français à un emplacement non valide.* Dans l'attribut `ph` d'un élément `<phoneme>`, le caractère de liaison ne suit pas une consonne ou apparaît au milieu de la prononciation du mot.
-   *Japonais` : le symbole ` ne précède pas une voyelle.* Dans l'attribut `ph` d'un élément `<phoneme>`, le caractère `:` n'apparaît pas avant une voyelle (éventuellement avec d'autres symboles, tels que la limite de syllabe, entre les deux).
-   *Accentuation de syllabe non valide. * L'attribut `ph` d'un élément `<phoneme>` pour un SPR {{site.data.keyword.IBM_notm}} inclut l'accentuation de syllabe non valide. Pour le français, un symbole d'accentuation de syllabe ne précède pas immédiatement une voyelle. Pour l'espagnol ou l'italien, un symbole secondaire (`2`) ou d'absence d'accentuation (`0`) est utilisé. Pour le japonais, un symbole d'accentuation secondaire (`2`) est utilisé.
-   *Utilisation non valide de l'élément `<express-as>` ou `<voice-transformation>` SSML.* Vous pouvez utiliser ces extensions SSML uniquement avec les voix standard en anglais américain spécifiées.
-   *Utilisation non valide de l'élément `<prosody>` SSML.* Vous ne pouvez pas utiliser les attributs `contour`, `duration` et `range` de l'élément `<prosody>` avec aucune voix. De plus, vous ne pouvez pas vous servir de l'attribut `volume` de l'élément `<prosody>` avec les voix neuronales (`en-US_AllisonV3Voice`, par exemple).
-   *Caractères de contrôle XML non mis en échappement.* Le texte d'entrée lui-même contient un caractère <code>&quot;</code>, <code>&apos;</code>, `&`, `<` ou `>` à la place de la chaîne d'échappement équivalente ou du codage de caractères. Pour plus d'informations, voir [Mise en échappement des caractères de contrôle XML](/docs/services/text-to-speech?topic=text-to-speech-usingHTTP#escape).
