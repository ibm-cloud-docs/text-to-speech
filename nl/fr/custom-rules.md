---

copyright:
  years: 2015, 2019
lastupdated: "2018-03-07"

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

# Règles de création d'entrées personnalisées 
{: #rules}

Les règles et consignes suivantes s'appliquent pour remplir un modèle personnalisé avec des entrées personnalisées (paires mot/traduction). 

## Nombre maximal d'entrées personnalisées 

Un modèle personnalisé peut inclure 20 000 entrées personnalisées au maximum. 

## Codage des caractères

Le service accepte le codage de caractères ASCII et UTF-8 pour les entrées *mot* et *traduction*. Pour les traductions, utilisez le codage ASCII pour les notations SPR et le codage UTF-8 pour les notations IPA. 

## Espace blanc

Un *mot* ne peut pas comporter d'espace. Le service utilise des espaces pour délimiter chaque mot individuel dans le texte en entrée. 

## Sensibilité à la casse

Un *mot* est sensible à la casse. Par exemple, supposons qu'un modèle personnalisé contienne l'entrée `{word='Sun', translation='Sunday'}`. Le service applique sa prononciation par défaut au mot `sun`, mais il applique la traduction personnalisée au mot `Sun`, car seul ce dernier a une lettre majuscule initiale. 


## Sensibilité au contexte 

La prononciation de certains mots dépend du contexte. Par exemple, considérons l'exemple de phrase en entrée suivant : 

```
St. Anthony lives on Henry St.
```
{: codeblock}

Les règles de prononciation par défaut du service synthétisent correctement ce texte comme suit 

```
Saint Anthony lives on Henry Street
```
{: codeblock}

Toutefois, si vous remplacez les règles de prononciation par défaut pour que la chaîne `St.` soit traduite par `saint`, le service ne peut plus prononcer le mot en fonction du contexte. L’application d’un modèle vocal personnalisé incluant une telle traduction force le service à prononcer la phrase entrée précédente comme suit : 

```
Saint Anthony lives on Henry saint
```
{: codeblock}

Envisagez ce type de cas lorsque vous développez des paires de mots/traduction. 

## Points finaux

Le service applique un mot d'un modèle personnalisé uniquement aux chaînes du texte d'entrée qui correspondent exactement au mot. Un point final (`.`) dans une entrée de mot change la façon dont le mot est synthétisé :

-   *Un mot qui ne comporte pas de point final* peut contenir pratiquement n'importe quel caractère. Les caractères incluent des lettres, des chiffres, des signes de ponctuation (autres que les points finaux), des symboles autres que des lettres (tels que %, &, et @), des guillemets, des parenthèses, des crochets, etc. Sa *traduction* peut inclure toute entrée admise par le service, y compris les espaces blancs et les représentations phonétiques au format SSML. 
-   *Un mot qui contient un point final* ne peut contenir que des lettres, des points et des apostrophes internes (et non en tant que premier ou dernier caractère). La *traduction* de ce mot ne peut contenir que des mots ordinaires, orthographiés normalement, séparés par des espaces ou des traits d'union. Elle ne peut pas contenir de représentation phonétique. 

Un exemple de mot avec un point final est "`div.`". Supposons qu'un modèle personnalisé comporte l'entrée `{word='div.', translation='division'}`. Le service n'applique pas la traduction à la chaîne "`div`" car elle n'inclut pas de point final et ne correspond donc pas à l'entrée. 

## Utilisation des entrées IBM SPR 
{: #sprNotes}

La représentation phonétique symbolique (SPR) est un format propriétaire, dépendant de la langue, développé par {{site.data.keyword.IBM_notm}} pour spécifier la prononciation d'un mot. Pour chaque langue prise en charge, SPR comprend un alphabet de phonèmes, des symboles pour les limites des syllabes et des symboles pour les niveaux de d'accentuation lexicale. Les règles de base suivantes s'appliquent à la création d'entrées SPR : 

-   La prononciation par défaut que l'interface de personnalisation renvoie pour un mot commence par un guillemet (<code>&#96;</code>) et est placée entre crochets (`[]`). Par exemple, l'interface renvoie la prononciation suivante pour le mot `tomato` :

    ```xml
    `[.0tx.1ma.0to]
    ```
    {: codeblock}

Omettez le guillemet et les crochets lorsque vous spécifiez la traduction d'un mot à l'aide des méthodes de l'interface de personnalisation.
-   Vous pouvez utiliser un point pour indiquer le début d'une syllabe dans une traduction, mais les points sont facultatifs et n'influencent pas la prononciation du mot. Ils n'apparaissent dans la prononciation d'un mot que si vous les incluez dans la traduction du mot. N'utilisez pas d'espaces pour indiquer les limites des syllabes. 
-   {{site.data.keyword.IBM_notm}} vous recommande de faire précéder la voyelle sur laquelle l'accentuation principale est mise dans un mot par le symbole `1`, bien que cela ne soit pas strictement nécessaire. Le service détermine où l'accentuation se produit si vous ne l'indiquez pas. Vous pouvez également utiliser le symbole `2` pour indiquer chaque position d'accentuation secondaire, mais l'utilisation du symbole `2` est également facultative. Ils n'apparaissent dans la prononciation d'un mot que si vous les incluez dans la traduction du mot. 

Pour plus d'informations sur l'utilisation de SPR, voir [Utilisation d'IBM SPR](/docs/services/text-to-speech/SPRs.html).

## Utilisation des entrées en japonais 
{: #jaNotes}

Des règles supplémentaires et une zone `part_of_speech` s'appliquent à la création d'entrées de mots dans un modèle vocal personnalisé japonais : 

-   Une traduction basée sur la sonorité ne peut contenir que des caractères *Katakana*. Les caractères *Kanji* et *Hiragana* ne sont pas autorisés.
-   Lorsque vous créez une traduction (basée sur la sonorité ou phonétique) pour un mot, vous pouvez également spécifier une zone facultative `part_of_speech` pour identifier la partie de discours de ce mot. Le service utilise la partie du discours pour produire l'intonation correcte du mot. Pour une liste complète, voir [Partie du discours en japonais](#partsOfSpeech).
-   Vous ne pouvez créer qu'une seule entrée pour un mot et vous ne pouvez spécifier qu'une seule partie du discours pour un mot. Vous ne pouvez pas créer plusieurs entrées avec différentes parties du discours (par exemple, nom et verbe) pour le même mot. L'ajout d'une traduction pour un mot existant dans un modèle écrase la traduction existante du mot, y compris sa partie du discours. 
-   Le service applique le mot correspondant le plus long parmi les paires mot/traduction définies pour un modèle vocal personnalisé. Par exemple, considérons les trois entrées suivantes pour un modèle personnalisé. 

    <pre><code>{
      "words": [
        {
          "word": "&#65326;&#65337;",
          "translation": "&#12491;&#12517;&#12540;&#12520;&#12540;&#12463;",
          "part_of_speech": "Mesi"
        },
        {
          "word": "&#65326;&#65337;&#65315;",
          "translation": "&#12491;&#12517;&#12540;&#12520;&#12540;&#12463;&#12471;&#12486;&#12451;",
          "part_of_speech": "Mesi"
        },
        {
          "word": "&#65337;&#65315;",
          "translation": "&#12520;&#12467;&#12495;&#12510;&#12481;&#12517;&#12540;&#12459;&#12460;&#12452;",
          "part_of_speech": "Mesi"
        }
      ]
    }</code></pre>

    Avec ces entrées, supposons que le service reçoive le texte en entrée suivant : <code>&#19968;&#36913;&#38291;&#65326;&#65337;&#65315;&#12434;&#35370;&#21839;&#12375;&#12383;</code>. Dans ce cas, le service correspond au mot <code>&#65326;&#65337;&#65315;</code> car <code>&#65326;&#65337;&#65315;</code> est plus long que <code>&#65326;&#65337;</code> et parce que <code>&#65326;&#65337;&#65315;</code> correspond avant <code>&#65337;&#65315;</code>.

### Parties du discours en japonais 
{: #partsOfSpeech}

Le tableau suivant répertorie les parties du discours prises en charge pour les entrées personnalisées en japonais. Pour plus d'informations sur la spécification de la partie du discours pour une entrée personnalisée en japonais, voir [Ajout de mots à un modèle personnalisé japonais](/docs/services/text-to-speech/custom-entries.html#cuJapaneseAdd).

<table style="width:75%">
  <caption>Tableau 1. Parties du discours en japonais </caption>
  <tr>
    <th style="text-align:center">Argument <code>part_of_speech</code></th>
    <th style="text-align:center; width:35%">Signification en japonais</th>
    <th style="text-align:center; width:35%">Signification en anglais</th>
  </tr>
  <tr>
    <td style="text-align:center"><code>Josi</code></td>
    <td style="text-align:center"><em>Joshi</em></td>
    <td style="text-align:center">Participe</td>
  </tr>
  <tr>
    <td style="text-align:center"><code>Mesi</code></td>
    <td style="text-align:center"><em>Meishi</em></td>
    <td style="text-align:center">Nom</td>
  </tr>
  <tr>
    <td style="text-align:center"><code>Kigo</code></td>
    <td style="text-align:center"><em>Kigou</em></td>
    <td style="text-align:center">Symbole</td>
  </tr>
  <tr>
    <td style="text-align:center"><code>Gobi</code></td>
    <td style="text-align:center"><em>Gobi</em></td>
    <td style="text-align:center">Inflexion</td>
  </tr>
  <tr>
    <td style="text-align:center"><code>Dosi</code></td>
    <td style="text-align:center"><em>Doushi</em></td>
    <td style="text-align:center">Verbe </td>
  </tr>
  <tr>
    <td style="text-align:center"><code>Jodo</code></td>
    <td style="text-align:center"><em>Jodoushi</em></td>
    <td style="text-align:center">Verbe auxiliaire </td>
  </tr>
  <tr>
    <td style="text-align:center"><code>Koyu</code></td>
    <td style="text-align:center"><em>Koyuumeishi</em></td>
    <td style="text-align:center">Nom propre </td>
  </tr>
  <tr>
    <td style="text-align:center"><code>Stbi</code></td>
    <td style="text-align:center"><em>Setsubiji</em></td>
    <td style="text-align:center">Suffixe </td>
  </tr>
  <tr>
    <td style="text-align:center"><code>Suji</code></td>
    <td style="text-align:center"><em>Suuji</em></td>
    <td style="text-align:center">Valeur numérique</td>
  </tr>
  <tr>
    <td style="text-align:center"><code>Kedo</code></td>
    <td style="text-align:center"><em>Keiyodoushi</em></td>
    <td style="text-align:center">Verbe adjectif </td>
  </tr>
  <tr>
    <td style="text-align:center"><code>Fuku</code></td>
    <td style="text-align:center"><em>Fukishi</em></td>
    <td style="text-align:center">Adverbe</td>
  </tr>
  <tr>
    <td style="text-align:center"><code>Keyo</code></td>
    <td style="text-align:center"><em>Keiyoshi</em></td>
    <td style="text-align:center">Verbe adjectif </td>
  </tr>
  <tr>
    <td style="text-align:center"><code>Stto</code></td>
    <td style="text-align:center"><em>Settoji</em></td>
    <td style="text-align:center">Préfixe</td>
  </tr>
  <tr>
    <td style="text-align:center"><code>Reta</code></td>
    <td style="text-align:center"><em>Rentaishi</em></td>
    <td style="text-align:center">Déterminant</td>
  </tr>
  <tr>
    <td style="text-align:center"><code>Stzo</code></td>
    <td style="text-align:center"><em>Setsuzokushi</em></td>
    <td style="text-align:center">Conjonction</td>
  </tr>
  <tr>
    <td style="text-align:center"><code>Kato</code></td>
    <td style="text-align:center"><em>Kantoushi</em></td>
    <td style="text-align:center">Interjection</td>
  </tr>
  <tr>
    <td style="text-align:center"><code>Hoka</code></td>
    <td style="text-align:center"><em>Hoka</em></td>
    <td style="text-align:center">Autre</td>
  </tr>
</table>
