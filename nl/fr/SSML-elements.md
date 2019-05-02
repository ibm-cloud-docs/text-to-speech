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

# Eléments SSML
{: #elements}

Avec le service {{site.data.keyword.texttospeechfull}}, vous pouvez utiliser la plupart des éléments SSML (Speech Synthesis Markup Language) pour contrôler la synthèse de votre texte. Les éléments sont disponibles pour toutes les langues prises en charge. Le tableau suivant récapitule la prise en charge des éléments et attributs SSML par le service. 

-   *Complète* signifie que le service prend entièrement en charge l'élément ou l'attribut avec ses interfaces HTTP et WebSocket.
-   *Partielle* signifie que le service ne prend pas en charge tous les aspects de l'élément ou de l'attribut. Cela peut également signifier que le service prend en charge l'élément ou l'attribut avec une seule de ses interfaces ou que l'élément ou l'attribut n'est pas pris en charge avec toutes les voix. 
-   *Aucune* signifie que le service ne prend pas en charge l'élément ou l'attribut.

Pour plus d'informations sur un élément ou un attribut, consultez sa description. Lorsque cela est indiqué, la prise en charge de certains attributs et valeurs diffère légèrement de la spécification SSML. Pour plus d'informations, voir [W3C Speech Synthesis Markup Language (SSML) Version 1.0 ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](http://www.w3.org/TR/speech-synthesis/){: new_window}.

<table>
  <caption>Tableau 1. Eléments SSML </caption>
  <tr>
    <th style="text-align:left; width:30%">Elément ou attribut</th>
    <th style="text-align:center; width:12%">Prise en charge</th>
    <th style="text-align:left; width:46%; padding-left:75px">Elément ou attribut</th>
    <th style="text-align:center; width:12%">Prise en charge</th>
  </tr>
  <tr>
    <td>[Audio](#audio_element)</td>
    <td style="text-align:center">Aucune</td>
    <td style="padding-left:75px">[Say-as](#say-as_element)</td>
    <td style="text-align:center">Partielle</td>
  </tr>
  <tr>
    <td>[Break](#break_element)</td>
    <td style="text-align:center">Complète</td>
    <td style="padding-left:100px">[cardinal](#sayAsCardinal)</td>
    <td style="text-align:center">Partielle</td>
  </tr>
  <tr>
    <td>[Desc](#desc_element)</td>
    <td style="text-align:center">Aucune</td>
    <td style="padding-left:100px">[date](#sayAsDate)</td>
    <td style="text-align:center">Partielle</td>
  </tr>
  <tr>
    <td>[Emphasis](#emphasis_element)</td>
    <td style="text-align:center">Aucune</td>
    <td style="padding-left:100px">[digits](#sayAsDigits)</td>
    <td style="text-align:center">Partielle</td>
  </tr>
  <tr>
    <td>[Lexicon](#lexicon_element)</td>
    <td style="text-align:center">Aucune</td>
    <td style="padding-left:100px">[letters](#sayAsLetters)</td>
    <td style="text-align:center">Partielle</td>
  </tr>
  <tr>
    <td>[Mark](#mark_element)</td>
    <td style="text-align:center">Partielle</td>
    <td style="padding-left:100px">[number](#sayAsNumber)</td>
    <td style="text-align:center">Partielle</td>
  </tr>
  <tr>
    <td>[Meta](#mm_element)</td>
    <td style="text-align:center">Aucune</td>
    <td style="padding-left:125px">cardinal</td>
    <td style="text-align:center">Partielle</td>
  </tr>
  <tr>
    <td>[Metadata](#mm_element)</td>
    <td style="text-align:center">Aucune</td>
    <td style="padding-left:125px">ordinal</td>
    <td style="text-align:center">Partielle</td>
  </tr>
  <tr>
    <td>[Paragraph](#ps_element)</td>
    <td style="text-align:center">Complète</td>
    <td style="padding-left:125px">telephone</td>
    <td style="text-align:center">Partielle</td>
  </tr>
  <tr>
    <td>[Phoneme](#phoneme_element)</td>
    <td style="text-align:center">Complète</td>
    <td style="padding-left:150px">punctuation</td>
    <td style="text-align:center">Partielle</td>
  </tr>
  <tr>
    <td style="padding-left:25px">IBM SPR</td>
    <td style="text-align:center">Complète</td>
    <td style="padding-left:100px">[ordinal](#sayAsOrdinal)</td>
    <td style="text-align:center">Partielle</td>
  </tr>
  <tr>
    <td style="padding-left:25px">IPA</td>
    <td style="text-align:center">Complète</td>
    <td style="padding-left:100px">[vxml:boolean](#vxml-boolean)</td>
    <td style="text-align:center">Partielle</td>
  </tr>
  <tr>
    <td>[Prosody](#prosody_element)</td>
    <td style="text-align:center">Partielle</td>
    <td style="padding-left:100px">[vxml:currency](#vxml-currency)</td>
    <td style="text-align:center">Partielle</td>
  </tr>
  <tr>
    <td style="padding-left:25px">contour</td>
    <td style="text-align:center">Aucune</td>
    <td style="padding-left:100px">[vxml:date](#vxml-date)</td>
    <td style="text-align:center">Partielle</td>
  </tr>
  <tr>
    <td style="padding-left:25px">duration</td>
    <td style="text-align:center">Aucune</td>
    <td style="padding-left:100px">[vxml:digits](#vxml-digits)</td>
    <td style="text-align:center">Partielle</td>
  </tr>
  <tr>
    <td style="padding-left:25px">[pitch](#prosody-pitch)</td>
    <td style="text-align:center">Complète</td>
    <td style="padding-left:100px">[vxml:phone](#vxml-phone)</td>
    <td style="text-align:center">Partielle</td>
  </tr>
  <tr>
    <td style="padding-left:25px">range</td>
    <td style="text-align:center">Aucune</td>
    <td style="padding-left:75px">[Sentence](#ps_element)</td>
    <td style="text-align:center">Complète</td>
  </tr>
  <tr>
    <td style="padding-left:25px">[rate](#prosody-rate)</td>
    <td style="text-align:center">Complète</td>
    <td style="padding-left:75px">[Speak](#speak_element)</td>
    <td style="text-align:center">Complète</td>
  </tr>
  <tr>
    <td style="padding-left:25px">[volume](#prosody-volume)</td>
    <td style="text-align:center">Partielle</td>
    <td style="padding-left:75px">[Sub](#sub_element)</td>
    <td style="text-align:center">Complète</td>
  </tr>
  <tr>
    <td></td>
    <td></td>
    <td style="padding-left:75px">[Voice](#voice_element)</td>
    <td style="text-align:center">Aucune</td>
  </tr>
</table>

## L'élément audio 
{: #audio_element}

L'élément `<audio>` insère des éléments enregistrés dans l'audio généré par le service. Il n'est pas pris en charge.

## L'élément break
{: #break_element}

L'élément `<break>` insère une pause dans le texte parlé. Il possède les attributs facultatifs suivants :

-   `strength` spécifie la longueur de la pause en termes de valeurs de force variables :
    -   `none` supprime une pause qui, sinon, pourrait se produire pendant le traitement.
    -   `x-weak`, `weak`, `medium`, `strong` ou `x-strong` insèrent des pauses de plus en plus marquées.
-   `time` spécifie la durée de la pause en secondes ou en millisecondes. Les formats de valeur valides sont `{integer}s` pour les secondes ou `{integer}ms` pour les millisecondes.

```xml
<speak version="1.0">
  Different sized <break strength="none">no pause</break>
  Different sized <break strength="x-weak">x-weak pause</break>
  Different sized <break strength="weak">weak pause</break>
  Different sized <break strength="medium">medium pause</break>
  Different sized <break strength="strong">strong pause</break>
  Different sized <break strength="x-strong">x-strong pause</break>
  Different sized <break time="1s">one-second pause</break>
  Different sized <break time="1500ms">1500-millisecond pause</break>
</speak>
```
{: codeblock}

## L'élément desc
{: #desc_element}

L'élément `<desc>` ne peut apparaître que dans un élément `<audio>`. Dans la mesure où l'élément `<audio>` n'est pas pris en charge, l'élément `<desc>` ne l'est pas non plus. 

## L'élément emphasis
{: #emphasis_element}

L'élément `<emphasis>` demande que le texte inclus soit prononcé avec emphase. Il n'est pas pris en charge.

## L'élément lexicon
{: #lexicon_element}

L'élément `<lexicon>` introduit les dictionnaires de prononciation pour le document SSML donné. Il n'est pas pris en charge.

Vous pouvez utiliser l'interface de personnalisation du service pour définir un dictionnaire d'entrées personnalisées (paires de mots/traductions) à utiliser lors de la synthèse vocale. Pour plus d'informations, voir [Compréhension de la personnalisation](/docs/services/text-to-speech/custom-intro.html).

## L'élément mark
{: #mark_element}

L'élément `<mark>` est pris en charge uniquement par l'interface WebSocket du service, et non par son interface HTTP, qui ignore l'élément. Pour plus d'informations, voir [Spécification d'une marque SSML](/docs/services/text-to-speech/word-timing.html#mark).
{: note}

L'élément `<mark>` est un élément vide qui place un marqueur dans le texte à synthétiser. Le client est averti lorsque tout le texte qui précède l'élément `<mark>` a été synthétisé. L'élément accepte un attribut `name` unique qui spécifie une chaîne identifiant de manière unique la marque ; ce nom doit commencer par un caractère alphanumérique. Le nom est renvoyé avec l'heure à laquelle la marque apparaît dans l'audio synthétisé. 

```xml
<speak version="1.0">
  Hello <mark name="here"/> world.
</speak>
```
{: codeblock}

## Eléments meta et metadata
{: #mm_element}

Les éléments `<meta>` et `<metadata>` sont des conteneurs dans lesquels vous pouvez placer des informations relatives au document. Ils ne sont pas pris en charge.

## Les éléments paragraph et sentence
{: #ps_element}

Les éléments `<paragraph>` (ou `<p>`) et `<sentence>` (ou `<s>`) sont des éléments facultatifs qui peuvent être utilisés pour donner des indications sur la structure textuelle. Si le texte inclus dans un élément `<paragraph>` ou `<sentence>` ne se termine pas par un caractère de ponctuation de fin de phrase (par exemple, un point), le service ajoute une pause plus longue que la normale à l'audio synthétisé. 

Le seul attribut valide pour l'un ou l'autre élément est `xml:lang`, qui permet le changement de langue. L'attribut n'est pas pris en charge.

```xml
<speak version="1.0">
  <paragraph>
    <sentence>Text within a sentence element.</sentence>
    <s>More text in another sentence.</s>
  </paragraph>
</speak>
```
{: codeblock}

## L'élément phoneme
{: #phoneme_element}

L'élément `<phoneme>` fournit une prononciation phonétique pour le texte inclus. L'orthographe phonétique représente les sons d'un mot, la façon dont les sons sont divisés en syllabes et quelles syllabes sont accentuées. L'élément a deux attributs :

-   `alphabet` est un attribut facultatif qui spécifie la phonologie à utiliser. Les alphabets supportés sont
    -   L'alphabet phonétique international standard (IPA) : `alphabet="ipa"`
    -   La représentation phonétique symbolique (SPR) {{site.data.keyword.IBM_notm}} : `alphabet="ibm"`

    Si aucun alphabet n'est spécifié, le service utilise IBM SPR par défaut.
-   `ph` est un attribut requis qui fournit la prononciation dans l'alphabet indiqué. Les exemples suivants montrent la prononciation du mot *tomato* dans les deux formats :

    -   Format IPA : 

        <pre><code>&lt;speak version="1.0"&gt;
          &lt;phoneme alphabet="ipa" ph="t&#601;&#712;me&#618;.&#638;o&#650;"&gt;tomato&lt;/phoneme&gt;
        &lt;/speak&gt;</code></pre>

    -   Format IPA avec symboles Unicode : 

        <pre><code>&lt;speak version="1.0"&gt;
          &lt;phoneme alphabet="ipa" ph="t&amp;&#35;x259;mei&amp;&#35;x027E;o&amp;&#035;x028A;"&gt;tomato&lt;/phoneme&gt;
        &lt;/speak&gt;</code></pre>

    -   Format IBM SPR : 

        <pre><code>&lt;speak version="1.0"&gt;
          &lt;phoneme alphabet="ibm" ph=".0tx.1me.0Fo"&gt;tomato&lt;/phoneme&gt;
        &lt;/speak&gt;</code></pre>

Pour plus d'informations sur l'utilisation des notations SPR et IPA avec l'élément `<phoneme>`, voir [Utilisation d'IBM SPR](/docs/services/text-to-speech/SPRs.html).

## L'élément prosody
{: #prosody_element}

L'élément `<prosody>` contrôle la hauteur, le débit et le volume du texte. Tous les attributs sont facultatifs, mais une erreur se produit si aucun attribut n'est spécifié. La spécification SSML autorise trois attributs non pris en charge par le service : `contour`, `range` et `duration`. Le service prend en charge les attributs `pitch`, `rate` et `volume`.

### L'attribut pitch
{: #prosody-pitch}

L'attribut `pitch` modifie la hauteur de la ligne de base du texte dans l'élément. Les valeurs acceptées sont 

-   Nombre suivi de la désignation `Hz` (Hertz) : la hauteur de la ligne de base est transposée (vers le haut ou vers le bas) à la valeur spécifiée. 
-   Valeur de changement relatif (en demi-tons) : nombre qui provoque un décalage absolu par rapport à la ligne de base en cours. Le nombre est précédé de `+` (augmentation) ou `-` (diminution) et suivi de `st` (demi-tons), par exemple `+5st`.
-   Changement relatif en pourcentage : nombre entraînant un décalage relatif par rapport à la ligne de base en cours. Le nombre est précédé de `+` (augmentation) ou `-` (diminution) et suivi de `%` (signe de pourcentage), par exemple `-10 %`.
-   L'un des six mots clés suivants, qui modifie la hauteur selon les valeurs prédéfinies correspondantes : 
    -   `default` utilise la hauteur de base par défaut du service.
    -   `x-low` réduit la base de la hauteur tonale de 12 demi-tons.
    -   `low` réduit la base de la hauteur tonale de six demi-tons.
    -   `medium` produit le même comportement que `default`.
    -   `high` élève la base de la hauteur tonale de six demi-tons.
    -   `x-high` élève la base de la hauteur tonale de 12 demi-tons.

    ```xml
    <speak version="1.0">
      <prosody pitch="150Hz">Transpose pitch to 150 Hz</prosody>
      <prosody pitch="-20Hz">Lower pitch by 20 Hz from baseline</prosody>
      <prosody pitch="+20Hz">Increase pitch by 20 Hz from baseline</prosody>
      <prosody pitch="-12st">Lower pitch by 12 semitones from baseline</prosody>
      <prosody pitch="+12st">Increase pitch by 12 semitones from baseline</prosody>
      <prosody pitch="x-low">Lower pitch by 12 semitones from baseline</prosody>
    </speak>
    ```
    {: codeblock}

### L'attribut rate
{: #prosody-rate}

L'attribut `rate` indique une modification du débit de parole pour le texte contenu dans l'élément. Le débit est spécifié en termes de mots par minute ; si le débit de parole est de 50 mots par minute, `rate` est égal à `50`. Lorsque l'attribut `rate` est défini sur un nombre positif, la mise en oeuvre n'est pas conforme à la spécification d'attribut du débit de prosodie W3C en vigueur. En outre, le service prend en charge les changements en pourcentage relatif (par exemple, `+15 %`) mais pas les changements en valeur relative (par exemple, `+15`). Les valeurs acceptées sont 

-   Augmentation ou diminution en pourcentage relatif : `+10 %`.
-   Nombre de mots par minute en tant que nombre positif : `75`.
-   `default` utilise le débit par défaut du service.
-   `x-slow` diminue le débit de 50 %.
-   `slow` diminue le débit de 25 %.
-   `medium` produit le même comportement que `default`.
-   `fast` augmente le débit de 25 %.
-   `x-fast` augmente le débit de 50 %.

```xml
<speak version="1.0">
  <prosody rate="slow">Decrease speaking rate by 25%</prosody>
  <prosody rate="50">Set speaking rate at 50 words per minute</prosody>
  <prosody rate="+5%">Increase speaking rate by 5 percent</prosody>
</speak>
```
{: codeblock}

### L'attribut volume
{: #prosody-volume}

Le service ne prend pas en charge l'attribut `volume` de l'élément `<prosody>` avec ses voix basées sur DNN (par exemple, `en-US_AllisonV2Voice`). Pour plus d'informations sur ces voix, voir [Technologies de synthèse vocale](/docs/services/text-to-speech/voices.html#technologiesVoices).
{: note}

L'attribut `volume` modifie le volume du texte dans l'élément. Vous pouvez spécifier un nombre entier ou décimal compris entre 1 et 100 (volume maximum). Vous pouvez également utiliser l'une des valeurs de chaîne suivantes, correspondant aux paramètres prédéfinis dans la plage de 0 à 100. (La valeur `silent` n'est pas prise en charge.)

-   `x-soft` a la valeur 30.
-   `soft` a la valeur 50.
-   `medium` a la valeur 80.
-   `loud` a la valeur 90.
-   `default` a la valeur 92.
-   `x-loud` a la valeur 100.

```xml
<speak version="1.0">
  <prosody volume="75">Modified volume is 75</prosody>
  <prosody volume="88.9">Modified volume is 88.9</prosody>
  <prosody volume="loud">Modified volume is 90</prosody>
</speak>
```
{: codeblock}

## L'élément say-as
{: #say-as_element}

L'élément `<say-as>` n'est que partiellement pris en charge pour la plupart des langues. Pour les langues autres que l'anglais américain, le service ne prend généralement en charge que les attributs `digits` et `letters` de l'élément.
{: note}

L'élément `<say-as>` fournit des informations sur le type de texte contenu dans l'élément et spécifie le niveau de détail pour le rendu du texte. L'élément comporte un attribut obligatoire, `interpret-as`, qui indique comment le texte inclus doit être interprété. Il comporte deux attributs facultatifs, `format` et `detail`, qui ne sont utilisés qu'avec des valeurs particulières dans l'attribut `interpret-as`, comme illustré dans les exemples suivants.

Ci-après les valeurs admises pour l'attribut `interpret-as` et des exemples pour chacun d'eux.

### cardinal
{: #sayAsCardinal}

La valeur `cardinal` prononce le nombre cardinal correspondant au numéral dans l'élément. Les exemples suivants prononcent *Super Bowl quarante-neuf*. Le premier est superflu, car il ne modifie pas le comportement par défaut du service.

```xml
<speak version="1.0">
  Super Bowl <say-as interpret-as="cardinal">49</say-as>
  Super Bowl <say-as interpret-as="cardinal">XLIX</say-as>
</speak>
```
{: codeblock}

### date
{: #sayAsDate}

La valeur `date` prononce la date dans l'élément conformément au format indiqué dans l'attribut `format` associé. L'attribut `format` est requis pour la valeur `date`. Si aucun `format` n'est présent, le service tente tout de même de prononcer la date. Les exemples suivants prononcent les dates indiquées aux formats spécifiés, où `d`, `m` et `y` représentent le jour, le mois et l'année.

```xml
<speak version="1.0">
  <say-as interpret-as="date" format="mdy">12/17/2005</say-as>
  <say-as interpret-as="date" format="ymd">2005/12/17</say-as>
  <say-as interpret-as="date" format="dmy">17/12/2005</say-as>
  <say-as interpret-as="date" format="ydm">2005/17/12</say-as>
  <say-as interpret-as="date" format="my">12/2005</say-as>
  <say-as interpret-as="date" format="md">12/17</say-as>
  <say-as interpret-as="date" format="ym">2005/12</say-as>
</speak>
```
{: codeblock}

### digits
{: #sayAsDigits}

La valeur `digits` prononce les chiffres du nombre au sein de l'élément. L'exemple suivant prononce chaque chiffre *123456*.

```xml
<speak version="1.0">
  <say-as interpret-as="digits">123456</say-as>
</speak>
```
{: codeblock}

### letters
{: #sayAsLetters}

La valeur `letters` épelle les caractères du mot dans l'élément. L'exemple suivant épelle les lettres du mot *hello*.

```xml
<speak version="1.0">
  <say-as interpret-as="letters">Hello</say-as>
</speak>
```
{: codeblock}

### number
{: #sayAsNumber}

La valeur `number` offre une alternative aux valeurs `cardinal` et `ordinal`. Vous pouvez utiliser l'attribut facultatif `format` pour indiquer comment une série de nombres doit être interprétée. Le premier exemple omet l'attribut `format` pour prononcer le nombre comme une valeur cardinale. Le deuxième exemple spécifie explicitement que le nombre doit être prononcé comme une valeur `cardinale`. Le troisième exemple spécifie que le nombre doit être prononcé comme une valeur `ordinale`.

```xml
<speak version="1.0">
  <say-as interpret-as="number">123456</say-as>
  <say-as interpret-as="number" format="cardinal">123456</say-as>
  <say-as interpret-as="number" format="ordinal">123456</say-as>
</speak>
```
{: codeblock}

Vous pouvez également spécifier la valeur `telephone` pour l'attribut `format`. Les exemples montrent deux manières différentes de prononcer une série de nombres sous forme de numéro de téléphone. Pour prononcer les nombres avec la ponctuation incluse, indiquez la valeur `punctuation` pour l'attribut `detail` facultatif.

```xml
<speak version="1.0">
  <say-as interpret-as="number" format="telephone">555-555-5555</say-as>
  <say-as interpret-as="number" format="telephone" detail="punctuation">555-555-5555</say-as>
</speak>
```
{: codeblock}

### ordinal
{: #sayAsOrdinal}

La valeur `ordinal` prononce la valeur ordinale correspondant au chiffre dans l'élément. L'exemple suivant prononce *deuxième en premier*.

```xml
<speak version="1.0">
  <say-as interpret-as="ordinal">2</say-as>
  <say-as interpret-as="ordinal">1</say-as>
</speak>
```
{: codeblock}

### vxml:boolean
{: #vxml-boolean}

La valeur `vxml:boolean` prononce *yes* ou *no* en fonction de la valeur `true` ou `false` dans l'élément.

```xml
<speak version="1.0">
  <say-as interpret-as="vxml:boolean">true</say-as>
  <say-as interpret-as="vxml:boolean">false</say-as>
</speak>
```
{: codeblock}

### vxml:currency
{: #vxml-currency}

La valeur `vxml:currency` permet de contrôler la synthèse des valeurs monétaires. La chaîne doit être écrite au format `UUUmm.nn`, `UUU` étant l'indicateur de devise à trois caractères spécifié par la norme ISO 4217 et `mm.nn` étant la quantité. L'exemple suivant prononce *quarante-cinq dollars et trente cents*.

```xml
<speak version="1.0">
  <say-as interpret-as="vxml:currency">USD45.30</say-as>
</speak>
```
{: codeblock}

Si le nombre spécifié comprend plus de deux décimales, le montant est synthétisé sous la forme d'un nombre décimal suivi de l'indicateur de devise. Si l'indicateur de devise à trois caractères est omis, le montant est synthétisé sous forme de nombre décimal uniquement et le type de devise n'est pas prononcé. L'exemple suivant prononce *quarante-cinq point trois deux neuf dollars américains*.

```xml
<speak version="1.0">
  <say-as interpret-as="vxml:currency">USD45.329</say-as>
</speak>
```
{: codeblock}

### vxml:date
{: #vxml-date}

La valeur `vxml:date` fonctionne comme la valeur `date`, mais le format est prédéfini comme étant `AAAAMMJJ`. Si vous ne connaissez pas la valeur d'un jour, d'un mois ou d'une année ou si vous ne souhaitez pas qu'elle soit prononcée, remplacez la valeur par un point d'interrogation (`?`). Les deuxième et troisième exemples incluent des points d'interrogation. 

```xml
<speak version="1.0">
  <say-as interpret-as="vxml:date">20050720</say-as>
  <say-as interpret-as="vxml:date">????0720</say-as>
  <say-as interpret-as="vxml:date">200507??</say-as>
</speak>
```
{: codeblock}

### vxml:digits
{: #vxml-digits}

La valeur `vxml:digits` fournit la même fonction que la valeur `digits`.

### vxml:phone
{: #vxml-phone}

La valeur `vxml:phone` prononce un numéro de téléphone composé de chiffres et de signes de ponctuation. Cela revient à utiliser la valeur `number` et à spécifier `telephone` pour l'attribut `format` et `punctuation` pour l'attribut `detail`.

```xml
<speak version="1.0">
  <say-as interpret-as="vxml:phone">555-555-5555</say-as>
</speak>
```
{: codeblock}

## L'élément speak
{: #speak_element}

L'élément `<speak>` est l'élément racine des documents SSML. Les attributs valides sont

-   `version` est un attribut obligatoire qui indique la spécification SSML. La valeur acceptée est `1.0`.
-   `xml:lang` n'est pas requis par le service. Omettez l'attribut lorsque vous utilisez cet élément.
-   `xml:base` est sans effet.

```xml
<speak version="1.0">
  The text to be spoken.
</speak>
```
{: codeblock}

## L'élément sub
{: #sub_element}

L'élément `<sub>` indique que le texte spécifié par l'attribut `alias` doit remplacer le texte contenu dans l'élément lorsque la parole est synthétisée. L'attribut `alias` est le seul attribut de l'élément et est obligatoire. 

```xml
<speak version="1.0">
  <sub alias="International Business Machines">IBM</sub>
</speak>
```
{: codeblock}

## L'élément voice
{: #voice_element}

L'élément `<voice>` demande un changement de voix. Il n'est pas pris en charge.
