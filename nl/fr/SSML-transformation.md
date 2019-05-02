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

# SSML de la transformation vocale 
{: #transformation}

Le service {{site.data.keyword.texttospeechfull}}, comme la plupart des systèmes de synthèse vocale, ne peut parler que dans un nombre limité de voix. De plus, certaines langues n'offrent qu'une ou deux voix. Pour étendre la plage de voix possibles, le service étend SSML avec un élément `<voice-transformation>`. Vous pouvez utiliser cet élément pour réaliser différentes voix virtuelles en contrôlant les aspects d'une voix par défaut. Les applications de la fonction incluent
{: shortdesc}

-   *Donner une autre saveur à une voix.* Vous souhaitez qu'une voix soit un peu différente en général ou pour une application spécifique. 
-   *Personnalisation vocale.* Vous souhaitez utiliser une voix unique pour différencier vos applications. 
-   *Applications multi-rôles.* Vous avez besoin de plusieurs voix pour représenter différents personnages. 

Vous pouvez appliquer l'élément `<voice-transformation>` à la totalité du texte, à une phrase, à un mot ou à un fragment. L'élément accepte un attribut obligatoire, `type`, qui décrit le type de transformation vocale à appliquer au texte spécifié. Vous pouvez appliquer une transformation intégrée ou créer une transformation personnalisée en fonction de différents aspects de la voix. 

## Support de langue 
{: #languages-transformation}

Le service prend en charge la transformation vocale uniquement pour les voix anglo-américaines suivantes : 

-   `en-US_AllisonVoice`
-   `en-US_LisaVoice`
-   `en-US_MichaelVoice`

La transformation vocale n'est pas prise en charge avec les versions basées sur DNN `V2`, de ces voix (par exemple, `en-US_AllisonV2Voice`). L'utilisation de l'élément avec une voix non prise en charge renvoie une erreur. 

## Transformations intégrées 

Les transformations intégrées appliquent des modifications préconfigurées aux attributs d'une voix. Considérez-les comme des voix virtuelles mises à disposition par le service. Le service offre deux transformations intégrées. Pour les utiliser, vous spécifiez le nom sensible à la casse de la transformation intégrée avec l'attribut `type` : 

-   `Young` donne à la voix un son plus jeune.
-   `Soft` rend la voix plus douce.

Vous pouvez appliquer l'attribut facultatif `strength` à la voix intégrée pour contrôler la mesure dans laquelle le service applique la transformation. Considérez la valeur comme un facteur de mélange que le service applique à la voix d'origine. L'attribut accepte une valeur comprise entre 0 et 100 %. Si vous spécifiez `0 %` la voix reste inchangée ; spécifier `100 %` permet de d'obtenir toute l'étendue de la transformation. Si vous omettez l'attribut, la force par défaut est `100 %`. 
Le service ignore les attributs pour les transformations personnalisées lorsque vous utilisez une transformation intégrée.
{: note}

## Exemples de transformation intégrée 

Les exemples suivants appliquent les deux transformations intégrées à la même phrase avec des forces différentes : 

```xml
<voice-transformation type="Young" strength="80%">
  Pourriez-vous nous fournir de nouvelles informations ?
</voice-transformation>

<voice-transformation type="Soft" strength="60%">
  Pourriez-vous nous fournir de nouvelles informations ?
</voice-transformation>
```
{: codeblock}

## Transformations personnalisées 

Les transformations personnalisées vous donnent un contrôle plus fin sur différents aspects de la transformation vocale. Pour utiliser une transformation personnalisée, vous spécifiez `Custom` pour l'attribut `type`. Vous pouvez ensuite utiliser un ou plusieurs des attributs facultatifs suivants pour contrôler la transformation. 

<table>
  <caption>Tableau 1. Attributs de transformation personnalisés </caption>
  <tr>
    <th style="width:15%; text-align:left">Attribut</th>
    <th style="width:25%; text-align:center">Plage</th>
    <th style="text-align:left">Description</th>
  </tr>
  <tr>
    <td><code>pitch</code></td>
    <td style="text-align:center">[-100 %, 100 %],<br/>
      [<code>x-low</code>, <code>low</code>, <code>default</code>,
      <code>high</code>, <code>x-high</code>]</td>
    <td>
Changement relatif normalisé du niveau de contour de hauteur moyen dans les limites de sécurité. L'attribut contrôle le niveau de ton moyen perçu. Il est emprunté à l'attribut <code>pitch</code> de l'élément <code>&lt;prosody&gt;</code> SML. Il contribue à changer l'identité perçue du locuteur.
    </td>
  </tr>
  <tr>
    <td><code>pitch_range</code></td>
    <td style="text-align:center">[-100 %, 100 %],<br/>
      [<code>x-narrow</code>, <code>narrow</code>, <code>default</code>,
      <code>wide</code>, <code>x-wide</code>]</td>
    <td>
Changement relatif normalisé de la plage dynamique de contour de hauteur dans les limites de sécurité. L'augmentation ou la diminution de la plage de hauteur rend le style de discours plus ou moins expressif. L'attribut est emprunté à l'attribut <code>range</code> de l'élément <code>&lt;prosody&gt;</code> SML. </td>
  </tr>
  <tr>
    <td><code>glottal_tension</code></td>
    <td style="text-align:center">[-100 %, 100 %],<br/>
      [<code>x-low</code>, <code>low</code>, <code>default</code>,
      <code>high</code>, <code>x-high</code>]</td>
    <td>
Changement relatif normalisé de la tension glottale dans les limites de sécurité. L'augmentation ou la diminution de la tension glottale est perçue comme une qualité de parole plus tendue ou laxiste. Une valeur positive peut produire des bourdonnements que vous pouvez atténuer en augmentant la valeur de l'attribut <code>breathiness</code>. Une valeur négative est perçue comme plus aérée et généralement plus agréable.
    </td>
  </tr>
  <tr>
    <td><code>breathiness</code></td>
    <td style="text-align:center">[-100 %, 100 %],<br/>
      [<code>x-low</code>, <code>low</code>, <code>default</code>,
      <code>high</code>, <code>x-high</code>]</td>
    <td>
Changement relatif normalisé du niveau perçu du bruit d'aspiration dans les limites de sécurité. Les valeurs extrêmes peuvent produire un discours bruyant (pour une respiration positive) ou un bourdonnement (pour une respiration négative). Utilisez cet attribut pour compenser le bourdonnement ou le bruit supplémentaire généré en tant qu'effet secondaire d'autres attributs. </td>
  </tr>
  <tr>
    <td><code>rate</code></td>
    <td style="text-align:center">[-100 %, 100 %],<br/>
      [<code>x-slow</code>, <code>slow</code>, <code>default</code>,
      <code>fast</code>, <code>x-fast</code>]</td>
    <td>
Changement relatif normalisé du débit de la parole dans des limites de sécurité. Augmenter ou réduire le débit accélère ou ralentit la parole. Un débit positif (plus rapide) élargit la plage de hauteur perçue et un débit négatif (plus lent) réduit perceptuellement la plage de hauteur. L'attribut est emprunté à l'attribut <code>rate</code> de l'élément <code>&lt;prosody&gt;</code> SML. </td>
  </tr>
  <tr>
    <td><code>timbre</code></td>
    <td style="text-align:center">[<code>Sunrise</code>,
      <code>Breeze</code>]</td>
    <td>
      Nom sensible à la casse d'une des transformations intégrées de l'appareil vocal : <code>Sunrise</code> ou <code>Breeze</code>.
      Les noms sont symboliques. Faites des expériences avec les timbres pour comprendre leur impact sur la transformation de la voix. Cet attribut contribue à changer l'identité perçue du locuteur.
    </td>
  </tr>
  <tr>
    <td><code>timbre_extent</code></td>
    <td style="text-align:center">[0 %, 100 %]</td>
    <td>
L'étendue de la transformation de l'appareil vocal <code>timbre</code>, <code>0 %</code>, annule la transformation ; <code>100 %</code> représente l'application complète de la transformation. L'attribut quantifie la différence entre les voix transformées et originales. Il permet de mélanger le timbre sélectionné avec le timbre de la voix d'origine. Même avec des valeurs d'étendue de timbre modérées, l'attribut <code>timbre</code> contribue à changer l'identité perçue du locuteur.
 </td>
  </tr>
</table>

### Utilisation de plages
{: #ranges}

Les plages numériques des différents attributs indiquent dans quelle mesure l'attribut affecte la voix. Par exemple, l'attribut `rate` a une plage allant de -100 % à 100 % :

-   La valeur `100 %` ne signifie pas que la voix devient 100 % plus rapide. Elle signifie que le service augmente le débit de la voix au maximum autorisé par cette voix. 
-   La valeur `-100 %` signifie que le service utilise le débit minimal autorisé pour la voix. 
-   La valeur `0 %` représente le niveau inhérent de l'attribut pour la voix ; la voix reste inchangée. 

### Utilisation de valeurs littérales 
{: #literals}

Par commodité, de nombreux attributs définissent également des valeurs littérales que vous pouvez utiliser à la place de pourcentages. La signification de ces valeurs diffère de celle utilisée avec l'élément `<prosody>` SSML. L'élément `<voice-transformation>` utilise une échelle uniforme pour tous ses attributs. 

-   `x-low`, `x-slow` et `x-narrow` sont égaux à `-100 %`.
-   `low`, `slow` et `narrow` sont égaux à `-50 %`. 
-   `default` est égal à `0 %`, la valeur par défaut pour cet attribut et cette voix.
-   `high`, `fast` et `wide` sont égaux à `+50 %`.
-   `x-high`, `x-fast` et `x-wide` sont égaux à `+100%`.

### Instructions d’utilisation
{: #guidelines}

Respectez les instructions et les mises en garde suivantes : 

-   Pour les applications de personnalisation vocale ou multi-rôles, utilisez les attributs `timbre`, `pitch` et `glottal_tension` pour modifier l'identité perçue du locuteur. Vous pouvez utiliser des combinaisons de ces trois attributs pour créer des voix virtuelles. Considérez une voix virtuelle comme un point de l’espace multidimensionnel réalisé par le timbre, la hauteur et la tension glottale spécifiés. Des combinaisons d'attributs différentes produisent des voix virtuelles différentes. 
-   Vous pouvez utiliser les attributs `pitch_range`, `breathiness` et `rate` pour ajouter de la saveur à une voix virtuelle. Les autres utilisateurs peuvent choisir des valeurs d'attribut identiques ou similaires. Par conséquent, le service ne peut pas garantir le caractère unique de votre voix virtuelle. 
-   Soyez conscient des effets secondaires potentiels suivants de l'application des attributs : 
    -   Une tension glottale élevée, une hauteur élevée et un débit faible peuvent provoquer des bourdonnements. Augmentez la respiration pour atténuer l'effet. 
    -   Une tension glottale extrêmement basse peut produire un discours bruyant. Diminuez le souffle pour réduire le bruit.
    -   Augmenter ou réduire simultanément la plage de hauteur et le débit à des degrés extrêmes peut rendre la parole non naturelle. 
-   Comme indiqué précédemment, certains attributs sont empruntés à l'élément `<prosody>` SSML. Pour plus d'informations, voir [L'élément prosody](/docs/services/text-to-speech/SSML-elements.html#prosody_element). Pour activer le contrôle précis de la voix virtuelle par la prosodie, vous pouvez 
    -   Imbriquer des éléments `<prosody>` dans des éléments `<voice-transformation>`.
    -   Imbriquer des éléments `<voice-transformation>` dans des éléments `<prosody>`.

    Vous *ne pouvez pas* imbriquer des éléments `<voice-transformation>`. 

## Exemples de transformation personnalisée 

Les exemples suivants appliquent différents attributs pour illustrer les applications possibles de la transformation personnalisée. Le premier exemple diminue la tension glottal pour adoucir la voix. En outre, il augmente modérément la plage de hauteur et le débit pour introduire un style de parole plus dynamique. 

```xml
<voice-transformation type="Custom" glottal_tension="-50%"
  pitch_range="30%" rate="10%">
  Avez-vous plus d'informations ?
</voice-transformation>
```
{: codeblock}

Le deuxième exemple utilise la tension glottale maximale, la hauteur et le débit minimal. De telles combinaisons ne sont généralement pas favorables et peuvent produire un bourdonnement. L'exemple atténue cet effet en augmentant la respiration. 

```xml
<voice-transformation type="Custom" glottal_tension="100%" pitch="100%"
  rate="-100%" breathiness="60%">
  Avez-vous plus d'informations ?
</voice-transformation>
```
{: codeblock}

Les deux exemples suivants modifient l’identité perçue du locuteur en appliquant un timbre. La voix est modifiée par le contrôle de l’ampleur du mélange et le changement du niveau de hauteur. Le premier exemple utilise l'étendue de timbre par défaut, 100 %.


```xml
<voice-transformation type="Custom" timbre="Sunrise" pitch="40%">
  Avez-vous plus d'informations ?
</voice-transformation>

<voice-transformation type="Custom" timbre="Breeze" timbre_extent="30%"
  pitch="-30%">
  Avez-vous plus d'informations ?
</voice-transformation>
```
{: codeblock}

Le dernier exemple utilise plusieurs attributs pour transformer la voix. L'exemple utilise l'étendue de timbre par défaut et omet la respiration. 

```xml
<voice-transformation type="Custom" timbre="Sunrise" pitch="-30%"
  pitch_range="80%" rate="60%" glottal_tension="-80%">
  Avez-vous plus d'informations ?
</voice-transformation>
```
{: codeblock}
