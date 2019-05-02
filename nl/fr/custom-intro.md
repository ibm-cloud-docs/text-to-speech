---

copyright:
  years: 2015, 2019
lastupdated: "2019-04-09"

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

# Compréhension de la personnalisation 
{: #customIntro}

Lorsque vous synthétisez du texte avec {{site.data.keyword.texttospeechfull}}, le service applique des règles de prononciation dépendantes de la langue. Le service applique les règles pour convertir l'orthographe ordinaire de chaque mot en orthographe phonétique. L'orthographe phonétique d'un mot utilise des symboles de phonème pour définir la prononciation du mot. Ces symboles sont les unités distinctes de son qui distinguent les mots dans une langue, les limites entre les syllabes et les marques d'accentuation des syllabes.
{: shortdesc}

Les règles de prononciation habituelles du service fonctionnent bien pour les mots courants. Cependant, elles peuvent donner des résultats imparfaits pour des mots inhabituels. Ces mots peuvent être des termes spéciaux d’origine étrangère, des noms de propres ou géographiques, des abréviations ou des acronymes. Si le lexique de votre application inclut des mots de ce type, vous pouvez utiliser l'interface de personnalisation pour spécifier comment le service prononce ces mots. 

L'interface de personnalisation est une fonctionnalité bêta disponible pour toutes les langues.
{: note}

## Fonctionnement de la personnalisation 
{: #ciHow}

L'interface de personnalisation du service {{site.data.keyword.texttospeechshort}} crée un dictionnaire de mots et leurs traductions pour une langue spécifique. Ce dictionnaire est appelé *modèle vocal personnalisé* ou simplement modèle personnalisé. Chaque entrée personnalisée dans un modèle vocal personnalisé consiste en une paire *mot*/*traduction*. La traduction d'un mot indique au service comment prononcer le mot lorsqu'il apparaît dans le texte en entrée. 

L'interface de personnalisation fournit des méthodes pour créer et gérer vos modèles vocaux personnalisés, que le service stocke de manière permanente. Une fois que vous avez créé un modèle personnalisé, vous pouvez l’utiliser pendant la synthèse avec n’importe quelle version de la méthode `/v1/synthesize`. Lorsque le service synthétise le texte en entrée, il détermine la prononciation des mots apparaissant dans le modèle personnalisé en appliquant leurs traductions directement ou indirectement. 

Vous spécifiez la traduction d'un mot dans un modèle vocal personnalisé en tant que *traduction basée sur la sonorité* ou *traduction phonétique*. Vous pouvez utiliser les deux méthodes pour des entrées dans le même modèle personnalisé et vous pouvez combiner les deux méthodes dans la même traduction. Un certain nombre de règles et de directives s'appliquent aux entrées personnalisées. Pour plus d'informations, voir [Règles de création d'entrées personnalisées](/docs/services/text-to-speech/custom-rules.html).

## Traduction basée sur la sonorité
{: #soundsLike}

La *traduction basée sur la sonorité* utilise les règles de prononciation habituelles du service pour représenter la prononciation d'un mot cible indirectement. Une traduction basée sur la sonorité est formée à partir des prononciations régulières d'un ou plusieurs autres mots. Le service substitue d'abord la traduction spécifiée à toute occurrence du mot figurant dans le texte en entrée. Il applique ensuite ses règles de prononciation habituelles à la traduction, en convertissant la traduction en sa représentation phonétique pour obtenir la prononciation. 

Par exemple, les règles de prononciation habituelles du service traduisent correctement un grand nombre d'abréviations et d'acronymes courants. Le service prononce l'abréviation *cm*, *centimètre*. Il prononce lettre par lettre les abréviations moins courantes. Par exemple, le service prononce la chaîne *Str* (abréviation de *street*) *S T R*, chaque lettre étant prononcée individuellement. Vous pouvez utiliser la méthode basée sur la sonorité pour spécifier la traduction *street* de la chaîne *Str*.

Un autre exemple d'acronyme est le mot *IEEE*, qui signifie Institute of Electrical and Electronic Engineers. Par défaut, le service prononce cet acronyme *I E E E*. Mais l’acronyme est généralement prononcé *I triple E*, que vous pouvez facilement définir à l’aide de la traduction simple basée sur la sonorité *I triple E*. Si le mot *IEEE* apparaît dans votre modèle personnalisé avec cette traduction, le service remplace chaque occurrence du mot par la traduction. Il applique ensuite ses règles de prononciation habituelles aux mots individuels *I*, *triple* et *E* pour obtenir la prononciation commune. 

Vous pouvez appliquer la méthode basée sur la sonorité à plus que de simples abréviations et acronymes. Elle fonctionne également pour les mots complexes ou inhabituels. Par exemple, la paire suivante de traductions basées sur la sonorité produit des prononciations correctes pour des mots inhabituels gérés de manière imparfaite par les règles de prononciation habituelles du service. Trouver des traductions appropriées pour ces mots peut être plus difficile que pour de simples abréviations. Les traductions suivantes utilisent les règles de prononciation habituelles pour modifier l'orthographe des mots. 

<table style="width:35%">
  <caption>Tableau 1. Exemples de traduction basée sur la sonorité</caption>
  <tr>
    <th style="text-align:left">Mot</th>
    <th style="text-align:left">Traduction </th>
  </tr>
  <tr>
    <td>ayurvedic</td>
    <td>aayervedic</td>
  </tr>
  <tr>
    <td>gastroentérite </td>
    <td>gastro-entérite</td>
  </tr>
</table>

Comme le montrent ces exemples, le développement de traductions basées sur la sonorité peut être plus empirique que conventionnel. Vous créez une traduction candidate en fonction de votre intuition et de votre expérience du service. Vous synthétisez ensuite le mot correspondant à la traduction candidate en tant que texte d’entrée et écoutez le résultat audio. Si vous êtes satisfait de la prononciation, vous pouvez utiliser la traduction dans votre modèle personnalisé ; sinon, modifiez la traduction et testez-la à nouveau. 

## Traduction phonétique 
{: #phonetic}

La méthode basée sur la sonorité est un moyen relativement simple et utile d’obtenir une prononciation. Mais il n'est pas toujours possible de développer des traductions basées sur la sonorité. L’alternative directe, la méthode phonétique, peut sembler plus compliquée et plus longue, mais elle permet d’obtenir la prononciation de n’importe quel mot. 

La *traduction phonétique* spécifie une prononciation en termes de symboles de phonèmes, marques d'accentuation des syllabes et de limites de syllabes facultatives qui remplacent les règles de prononciation habituelles du service. Vous spécifiez une traduction phonétique dans l'un des formats suivants :

-   La représentation standard de l'alphabet phonétique international (IPA) 
-   Représentation phonétique symbolique (SPR) {{site.data.keyword.IBM_notm}} exclusive 

Dans les deux cas, vous spécifiez une traduction en utilisant un format de phonème spécifique basé sur le langage SSML (Speech Synthesis Markup Language). SSML est un langage de balisage basé sur XML qui fournit des annotations de texte pour les applications de synthèse vocale. Vous spécifiez la traduction phonétique d'un mot à l'aide de l'élément `<phoneme>` SSML : 

<pre><code>&lt;phoneme alphabet="{ipa | ibm}" ph="{translation}"&gt;&lt;/phoneme&gt;</code></pre>

L'attribut `alphabet` spécifie le type de représentation phonétique : `ipa` ou `ibm`. L'attribut `ph` spécifie la chaîne de traduction phonétique. 

Par exemple, considérons le mot `trinitroglycerin`. Les règles de prononciation habituelles du service produisent une prononciation différente de celle couramment utilisée par les chimistes et les médecins. La prononciation correcte peut être obtenue avec une traduction phonétique. 

<table style="width:35%">
  <caption>Tableau 2. Exemples de traduction phonétique  </caption>
  <tr>
    <th style="text-align:left">Alphabet</th>
    <th style="text-align:left">Traduction </th>
  </tr>
  <tr>
    <td>IPA</td>
    <td>t&#633;a&#618;n&#712;a&#618;t&#633;&#601;gl&#618;s&#601;&#633;&#616;n</td>
  </tr>
  <tr>
    <td>SPR</td>
    <td>trYn1YtrxglIsxrXn</td>
  </tr>
</table>

Dans ces exemples, la chaîne de traduction phonétique est composée de symboles de phonème et d'une marque d'accentuation principale unique. L'accentuation principale est représentée par <code>&#712;</code> dans IPA et par `1` dans SPR. Elle est placée juste avant le symbole de la voyelle accentuée dans les deux cas. Bien que les exemples ne le montrent pas, vous pouvez également spécifier des limites de syllabes et des positions d'accentuation secondaires dans une traduction phonétique. Ces éléments ne sont pas obligatoires et ne sont normalement pas nécessaires pour obtenir une prononciation. Comme pour les traductions basées sur la sonorité, vous pouvez composer une traduction phonétique à partir de plusieurs chaînes délimitées par des espaces. 

Vous pouvez également spécifier des traductions IPA en tant que valeurs Unicode IPA. Pour plus d'informations, voir [Utilisation d'IBM SPR](/docs/services/text-to-speech/SPRs.html) et les tableaux spécifiques aux langues dans les pages auxquelles il est fait référence dans [Langues prises en charge.](/docs/services/text-to-speech/SPRs.html#supportedLanguages). Pour un exemple de traduction utilisant les valeurs Unicode IPA, voir [L'élément phoneme](/docs/services/text-to-speech/SSML-elements.html#phoneme_element).
{: note}

### Utilisation d'une traduction phonétique existante 
{: #phoneticMethod}

Excepté si vous êtes un expert en phonologie, composer des traductions phonétiques n'est pas une tâche facile. Il est toujours plus facile d'éditer une traduction phonétique existante que d'en composer une nouvelle. Pour vous aider à créer des traductions phonétiques, l'API du service inclut une méthode `GET /v1/pronunciation`. La méthode renvoie la représentation IPA ou SPR générée par les règles de prononciation habituelles du service pour un mot dans une langue spécifiée. Vous pouvez également demander la prononciation d'un mot à partir d'un modèle vocal personnalisé spécifié pour voir la traduction dans la langue de ce modèle. 

Vous pouvez utiliser la méthode `/GET v/1/pronunciation` pour obtenir la traduction phonétique initiale d'un mot. Vous pouvez ensuite modifier la traduction pour obtenir la prononciation que vous souhaitez. De même que pour la méthode basée sur la sonorité, vous appliquez un processus empirique. Vous soumettez votre traduction candidate au service, synthétisez le mot en tant que texte de saisie, écoutez l'audio obtenu et modifiez la traduction candidate. Vous pouvez répéter le processus jusqu'à ce qu'à obtenir une prononciation satisfaisante. 

Pour plus d'informations, voir [Interrogation d'un mot dans une langue](/docs/services/text-to-speech/custom-entries.html#cuWordsQueryLanguage).

### Informations supplémentaires sur la traduction phonétique 
{: #phoneticInfo}

Les ressources suivantes fournissent des informations sur la traduction phonétique : 

-   Pour plus d'informations sur l'utilisation de SSML et son élément `<phoneme>`, voir [Utilisation de SSML](/docs/services/text-to-speech/SSML.html).
-   Pour plus d'informations sur la spécification des traductions SPR et de leurs symboles IPA équivalents, voir [Utilisation d'IBM SPR](/docs/services/text-to-speech/SPRs.html). 
-   Pour plus d'informations sur l'utilisation des symboles IPA et pour des exemples audio des symboles, consultez des sources sur le Web. Vous trouverez une discussion introductive détaillée à l'adresse [en.wikipedia.org/wiki/International_Phonetic_Alphabet ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://en.wikipedia.org/wiki/International_Phonetic_Alphabet){: new_window}.

## Traduction mixte basée sur la sonorité et phonétique

Vous pouvez combiner les méthodes basée sur la sonorité et phonétique dans la même traduction. Cette fonctionnalité peut réduire le travail nécessaire à la composition d'une traduction. 

Par exemple, supposons que vous utilisiez la méthode basée sur la sonorité pour qu'une partie d’un mot soit prononcée de façon satisfaisante. Mais vous devez ensuite affiner les éléments restants du mot. Vous pouvez alors utiliser la méthode phonétique pour spécifier les aspects difficiles du mot. L'exemple suivant applique une traduction mixte au mot `trinitroglycerin` :

<pre><code>try&lt;phoneme alphabet="ipa" ph="n&#712;a&#618;t&#633;&#601;gl&#618;s&#601;&#633;&#616;n"&gt;&lt;/phoneme&gt;</code></pre>
