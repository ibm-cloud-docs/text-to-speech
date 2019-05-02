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

# Utilisation d'IBM SPR 
{: #sprs}

Le service {{site.data.keyword.texttospeechfull}} prend en charge la notation standard Alphabet phonétique international (IPA) et la représentation phonétique symbolique {{site.data.keyword.IBM}} pour symboliser le son des mots. SPR est un codage phonétique qui représente la prononciation d'un mot, les sons qui le composent, la façon dont les sons sont divisés en syllabes et les syllabes accentuées. SPR est une représentation alternative à IPA
{: shortdesc}

Les sections suivantes présentent la notation {{site.data.keyword.IBM_notm}} SPR. Dans la mesure où IPA est une notation standard, la documentation ne fournit pas d'informations d'utilisation de base pour IPA. Pour des instructions d'utilisation succinctes, voir [Utilisation d'IPA](#ipa).

## Introduction à IBM SPR 
{: #introduction-SPRs}

Une prononciation SPR est définie avec l'élément `<phoneme>` du langage SSML (Speech Synthesis Markup Language) (voir [L'élément phoneme](/docs/services/text-to-speech/SSML-elements.html#phoneme_element)). Elle consiste en une séquence de symboles autorisés pour une langue donnée entre guillemets. Les symboles définissent comment le mot inclus dans l'élément `<phoneme>` doit être prononcé. L'attribut `alphabet` de l'élément comporte la valeur `ibm` pour indiquer que la prononciation est définie dans SPR et l'attribut `ph` définit la prononciation.  Voici des exemples de notation SPR valide pour les mots *through* et *shocking* en anglais américain : 

```xml
<phoneme alphabet="ibm" ph=".1Tru">through</phoneme>
<phoneme alphabet="ibm" ph=".1Sa.0kIG">shocking</phoneme>
```
{: codeblock}

Dans les définitions, un `.` (point) marque le début d'une nouvelle syllabe, les chiffres `1` et `0` indiquent le niveau d'accentuation des syllabes et les lettres représentent des sons spécifiques du discours en anglais américain. Une entrée SPR non conforme à la spécification requise n'est pas valide. 

## Limites de syllabe

Vous pouvez utiliser le signe `.` (point) pour marquer le début de chaque syllabe. Cependant, afin de préserver la phonétique valide d'une langue, le service peut choisir de ne pas respecter les points dans certains cas (par exemple, si une limite de syllabe est placée à une position non admise ou non naturelle pour une langue). En général, dans les cas où l'utilisateur peut indiquer une préférence valide pour une limite de syllabe ou un autre aspect de la prononciation d'un mot, le service honore ces demandes. 

## Accentuation de syllabe

Vous pouvez utiliser les symboles du tableau ci-dessous pour marquer l'accentuation d'une syllabe dans une prononciation. {{site.data.keyword.IBM_notm}} vous recommande d'indiquer l'accentuation principale pour les prononciations dans SPR ou IPA. Toutefois, l’indication d'une accentuation syllabique est facultative pour les deux formats ; le service détermine où l'accentuation se produit si vous ne l'indiquez pas. 

<table style="width:80%">
  <caption>Tableau 1. Accentuation de syllabe</caption>
  <tr>
    <th style="width:22%; text-align:center; vertical-align:bottom">
      Symbole IBM SPR
    </th>
    <th style="width:22%; text-align:center; vertical-align:bottom">
      Symbole IPA
    </th>
    <th style="width:22%; text-align:center; vertical-align:bottom">
      Unicode IPA
    </th>
    <th style="text-align:left; vertical-align:bottom">
      Signification
</th>
  </tr>
  <tr>
    <td style="text-align:center">
      1
    </td>
    <td style="text-align:center">
      <code>&#712;</code>
    </td>
    <td style="text-align:center">
      02C8
    </td>
    <td>
      Accentuation principale
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      2
    </td>
    <td style="text-align:center">
      <code>&#716;</code>
    </td>
    <td style="text-align:center">
      02CC
    </td>
    <td>
      Accentuation secondaire
    </td>
  </tr>
  <tr>
    <td style="text-align:center">
      0
    </td>
    <td style="text-align:center">Aucun symbole</td>
    <td style="text-align:center">Aucune valeur</td>
    <td>
      Aucune accentuation
    </td>
  </tr>
</table>

**Remarques :**

-   Dans IPA pour le français, les symboles d'accentuation de syllabe sont ignorés. Dans SPR pour le français, l'accentuation de syllabe n'est pas ignorée ; si elle est précisée, l'accentuation de syllabe doit précéder immédiatement la voyelle de la syllabe. Dans SPR, l'accentuation de syllabe pour le français est beaucoup plus stricte que pour les autres langues ; une erreur se produit si le symbole d'accentuation se trouve à un emplacement non valide. 
-   Dans SPR pour l'espagnol et l'italien, vous ne pouvez spécifier que `1` (accentuation principale). Une erreur se produit si vous spécifiez une accentuation secondaire ou nulle. 
-   Dans SPR pour le japonais, seuls `1` (accentuation principale) et `0` (pas d'accentuation) sont pris en charge. Une erreur se produit si vous spécifiez une accentuation secondaire. 

Vous devez placer un marqueur d'accentuation de syllabe dans une limite de syllabe, mais toujours à gauche de la voyelle de la syllabe. Vous pouvez placer un marqueur n'importe où à gauche de la voyelle stressée. Par exemple, chacun des exemples SPR suivants place l'accentuation principale sur la voyelle correcte du mot *construction* :

```xml
<phoneme alphabet="ibm" ph="kXn1strHkSXn">construction</phoneme>
<phoneme alphabet="ibm" ph="kXns1trHkSXn">construction</phoneme>
<phoneme alphabet="ibm" ph="kXnst1rHkSXn">construction</phoneme>
<phoneme alphabet="ibm" ph="kXnstr1HkSXn">construction</phoneme>
```
{: codeblock}

## Symboles sonores de la parole 

Chaque langue utilise son propre inventaire de symboles SPR pour représenter les sons de la parole de cette langue. Les règles suivantes s'appliquent à la spécification d'un symbole SPR : 

-   Les lettres sont sensibles à la casse. Ainsi, `e` et `E`, par exemple, représentent deux sons différents. 
-   Les symboles à deux et à trois caractères doivent figurer entre guillemets simples ; par exemple, le symbole `aj` dans le mot allemand *heim* : `"h'aj'm"`.
-   Le service considère comme non valide toute définition SPR contenant des symboles sonores interdits dans une langue. 

Tenez également compte des éléments suivants lors de la définition de la prononciation d'un mot au format SPR : 

-   Les sons de toutes les langues ont des schémas de distribution spécifiques dans cette langue. Par exemple, dans tous les dialectes anglais, le son `G` dans *sing* (`".1sIG"`) ne se produit pas au début d'un mot. L'arrêt glottal (`?`), le rabat (`F`) et la nasal syllabique (`N`) sont d'autres sons anglais américains à la distribution particulièrement étroite. Si vous entrez un symbole sonore dans un contexte dans lequel il ne se produit pas normalement, la parole obtenue peut sembler non naturelle. 
-   Le service {{site.data.keyword.texttospeechshort}} applique à son entrée un ensemble sophistiqué de règles linguistiques afin de refléter les processus par lesquels les sons changent dans des contextes spécifiques en langage naturel. Par exemple, en anglais américain, le son `t` du mot *write* (`".1r1Yt"`) est prononcé comme un rabat (`F`) dans *writer* (`".1rY.0FR"`). L'entrée SPR subit ces modifications, tout comme le texte d'entrée ordinaire. Dans cet exemple, que vous entriez `".1rY.0tR"` ou `".1rY.0FR"` n'affecte pas le discours généré.

## Utilisation d'IPA
{: #ipa}

Les informations suivantes s'appliquent à l'utilisation des prononciations en notation IPA : 

-   Utilisez uniquement les symboles IPA documentés. Lorsque plusieurs symboles IPA (ou combinaisons de symboles) sont répertoriés pour un symbole SPR, tous sont équivalents au symbole SPR unique. Dans ce cas, le service traite tous les symboles IPA de la même manière et ne réalise pas les différences subtiles ou régionales que le système IPA est censé décrire. 
-   Vous pouvez également spécifier des prononciations IPA en tant que valeurs Unicode IPA. Les tableaux spécifiques à une langue répertoriés dans la section suivante décrivent à la fois les symboles IPA et leurs valeurs Unicode IPA équivalentes. Pour un exemple de prononciation utilisant les valeurs Unicode IPA, voir [L'élément phoneme](/docs/services/text-to-speech/SSML-elements.html#phoneme_element).

Pour en savoir plus, reportez-vous aux rubriques suivantes :

-   Pour plus d'informations sur IPA, voir [en.wikipedia.org/wiki/International_Phonetic_Alphabet ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://en.wikipedia.org/wiki/International_Phonetic_Alphabet){: new_window}.
-   Pour plus d'informations sur les symboles phonétiques pour Unicode, voir [en.wikipedia.org/wiki/Phonetic_symbols_in_Unicode ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://en.wikipedia.org/wiki/Phonetic_symbols_in_Unicode){: new_window}.

## Langues prises en charge 
{: #supportedLanguages}

Les pages suivantes décrivent les symboles SPR, les symboles IPA et les valeurs Unicode IPA équivalentes pour chaque langue. Elles montrent des exemples de chaque symbole en mots dans la langue. En raison des différences dialectales, les exemples ne correspondent pas toujours à votre prononciation. 

-   [Symboles portugais brésiliens](/docs/services/text-to-speech/pt-BR-SPRs.html)
-   [Symboles anglais britanniques](/docs/services/text-to-speech/en-GB-SPRs.html)
-   [Symboles français](/docs/services/text-to-speech/fr-FR-SPRs.html)
-   [Symboles allemands](/docs/services/text-to-speech/de-DE-SPRs.html)
-   [Symboles italiens](/docs/services/text-to-speech/it-IT-SPRs.html)
-   [Symboles japonais](/docs/services/text-to-speech/ja-JP-SPRs.html)
-   [Symboles espagnols](/docs/services/text-to-speech/es-ES-SPRs.html)
-   [Symboles anglais américains](/docs/services/text-to-speech/en-US-SPRs.html)
