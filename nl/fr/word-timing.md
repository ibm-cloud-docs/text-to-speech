---

copyright:
  years: 2015, 2019
lastupdated: "2019-06-04"

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

# Obtention du minutage des mots
{: #timing}

L'interface WebSocket fournit les mêmes fonctionnalités que les méthodes HTTP `GET` et `POST /v1/synthesize`. Vous pouvez également utiliser l'interface WebSocket pour obtenir des informations de minutage pour des emplacements spécifiques ou pour tous les mots de l'entrée :
{: shortdesc}

-   Incluez l'élément `<mark>` SSML dans le texte d'entrée pour identifier l'heure à laquelle le marqueur apparaît dans l'audio.
-   Spécifiez le paramètre `timings` d'un message texte JSON pour obtenir des informations de minutage pour toutes les chaînes du texte en entrée.

Les informations de minutage sont utiles pour synchroniser l'audio et le texte en entrée. Par exemple, vous pouvez coordonner les gestes d'un robot avec le contenu de la parole synthétisée.

Le paramètre `timings` n'est pas pris en charge pour le texte d'entrée en japonais.
{: note}

## Comment le service renvoie le minutage des mots
{: #timingHow}

Pour renvoyer des informations de marque ou de minutage des mots, le service multiplexe des flux binaires et textuels indépendants pour construire sa réponse :

-   Pour chaque élément `<mark`, le service renvoie un message texte JSON. Chaque message indique l'heure exacte à partir du début de l'audio synthétisé, à laquelle la marque apparaît.
-   Pour le minutage de mots de toutes les chaînes, le service renvoie un ou plusieurs messages texte JSON. Chaque message contient un tableau de mots et leurs temps de début et de fin, à partir du début de l'audio synthétisé.

Les flux binaires et texte envoyés par le service sont indépendants. Par conséquent, le service exerce un contrôle limité sur le nombre de blocs audio qu'il fournit, et sur le moment où l'utilisateur reçoit les messages texte et audio. Par exemple, si le son est synthétisé plus rapidement qu'il n'est compressé, tous les messages texte peuvent arriver avant leur équivalent audio.

Concrètement, le service peut envoyer un nombre arbitraire de blocs audio, y compris plusieurs blocs audio avant et après chaque message texte. Il est également possible qu'un seul bloc binaire contienne des données audio qui précèdent et suivent les informations de minutage d'une marque ou d'un mot.

Cependant, le message texte contenant les informations de minutage arrive toujours avant le bloc binaire qui contient l'audio correspondant. En outre, les messages audio arrivent toujours dans l’ordre afin que vous puissiez construire une synthèse audio précise du texte à partir des résultats binaires.

## Spécification d'une marque SSML
{: #mark}

L'élément `<mark>` SSML facultatif est un élément vide qui place un marqueur dans le texte à synthétiser. Le client est averti lorsque tout le texte qui précède l'élément `<mark>` a été synthétisé.

L'élément accepte un attribut `name` unique qui spécifie une chaîne identifiant de manière unique la marque. Le nom doit commencer par un caractère alphanumérique. Le service renvoie le nom avec l'heure à laquelle la marque apparaît à partir du début de l'audio synthétisé. Vous pouvez inclure n'importe quel nombre de marques dans le texte en entrée.

Le fragment de code JavaScript suivant inclut une instance de l'élément `<mark>` portant le nom `here` :

```javascript
function onOpen(evt) {
  var message = {
    text: 'Hello <mark name="here"/> world',
    accept: '*/*'
  };
  websocket.send(JSON.stringify(message));
}
```
{: codeblock}

Lorsqu'il termine de synthétiser le texte qui précède la marque, le service envoie un message texte identifiant le nom de la marque et le temps en secondes auquel la marque apparaît dans l'audio :

```javascript
{
  "marks": [
    ["here", 0.5019387755102041]
  ]
}
```
{: codeblock}

Le message texte contenant les informations de minutage arrive toujours avant le bloc audio contenant l'emplacement de la marque.

## Demande du minutage de tous les mots
{: #timingRequest}

Le paramètre `timings` facultatif de l'objet JSON que vous transmettez au service pour une demande renvoie des informations de minutage pour toutes les chaînes du texte en entrée. Cette commodité élimine la nécessité de spécifier l'élément `<mark>` SSML pour chaque mot de l'entrée. Transmettez un tableau contenant la chaîne `words` pour demander le minutage des mots. Transmettez un tableau vide ou omettez le paramètre pour ne recevoir aucune information de minutage.

Le service renvoie le minutage des mots sur la connexion WebSocket de la même manière qu'il renvoie les informations de minutage pour chaque élément `<mark>`. Il renvoie un ou plusieurs messages texte JSON. Chaque message contient un tableau de mots et leurs temps de début et de fin en secondes, à partir du début de l'audio synthétisé. Par exemple, l'exemple suivant demande des informations de minutage des mots :

```javascript
function onOpen(evt) {
  var message = {
    text: 'I have a pet bird.',
    accept: '*/*',
    timings: ['words']
  };
  websocket.send(JSON.stringify(message));
}
```
{: codeblock}

En réponse, le service peut renvoyer les messages texte suivants :

```javascript
{
  "words": [
    ["I", [0.0690258394023930, 0.1655782733012873]]
    ["have", [0.1655789302434486, 0.3722901056092351]]
    ["a", [0.3722906798320199, 0.4012192331086645]]
  ]
}
{
  "words": [
    ["pet", [0.4012195492838347, 0.5798213856109801]]
    ["bird.", [0.5798218710823425, 0.7440360383928273]]
  ]
}
```
{: codeblock}

La réponse est simplement un exemple. Le service peut renvoyer un ou plusieurs messages texte contenant des informations de minutage sur le texte en entrée. De plus, les messages peuvent être entrecoupés de réponses contenant des blocs binaires d'audio. Mais le message texte contenant les informations de minutage d'un mot arrive toujours avant le bloc audio qui contient ce mot.

### Minutage du texte brut
{: #timingText}

Le processus de synthèse du service implique une étape de normalisation du texte qui épelle les nombres, les dates, les heures, les montants en devises, les acronymes et les abréviations. Les résultats correspondent à la façon dont ces chaînes sont prononcées. Par exemple, la chaîne *$200* est prononcée en trois mots : *deux*, *cents* et *dollars*. Dans la mesure où les informations de minutage des mots sont utilisées pour synchroniser l'audio avec le texte en entrée, le service renvoie des informations de minutage correspondant à l'orthographe non normalisée de l'entrée.

Par exemple, considérons le texte d'entrée suivant :

```
The coldest recorded temperature is -89.2 degrees Celsius in Antarctica on July 21, 1983!
```
{: codeblock}

Le service renvoie des minutages audio pour les chaînes suivantes :

"*The*", "*coldest*", "*recorded*", "*temperature*", "*is*", "*-89.2*", "*degrees*", "*Celsius*", "*in*", "*Antarctica*", "*on*", "*July*", "*21,*", "*1983!*"

Bien que "*-89.2*" soit prononcé dans l’audio en cinq mots distincts (*minus*, *eighty*, *nine*, *point*, *two*), le message texte fournit des informations de minutage pour la chaîne sous la forme d’une seule unité, avec le temps de début *minus* et le temps de fin *two*.

Comme dans l'exemple précédent, les chaînes non normalisées peuvent également contenir de la ponctuation. Le service inclut la ponctuation qui précède ou suit un mot dans le message texte renvoyé avec le minutage. Par exemple, les chaînes "*21,*" et "*1983!*" incluent la ponctuation renvoyée par le service dans son message texte. Bien que la ponctuation entraîne le silence, le minutage audio du mot *n'inclut pas* ce silence.

Par exemple, considérons un texte en entrée contenant l'instruction conditionnelle suivante :

```
If it is sunny, I will go to the beach.
```
{: codeblock}

Le service renvoie des informations de minutage pour toutes les chaînes de l'entrée, y compris "*sunny,*" et "*beach.*"qui se terminent toutes deux par une ponctuation qui produit un silence. Mais les informations de minutage pour "*sunny,*" n'incluent pas le silence généré par la virgule et les informations de minutage pour "*beach.*" n'incluent pas le silence du point. Les informations reflètent uniquement le minutage des chaînes parlées.

### Minutage du texte SSML
{: #timingSSML}

Lorsque le service synthétise du texte brut, il renvoie tous les caractères saisis, à l'exception des espaces, avec les chaînes de sa réponse de minutage des mots. Il n'en va pas de même pour SSML, car certains éléments SSML ne génèrent pas d’audio. La liste suivante résume les éléments SSML pouvant avoir une incidence sur les informations de minutage des mots :

-   `<say-as>` indique comment le texte placé entre les balises `<say-as>` d'ouverture et de fermeture doit être traité dans l'étape de normalisation. Les attributs spécifient comment le texte incorporé doit être prononcé. L'exemple suivant indique comment la date doit être prononcée :

    ```xml
    The baby was born on <say-as interpret-as="date" format="mdy">3/4/2016</say-as>.
    ```
    {: codeblock}

    Le service renvoie des informations de minutage pour les chaînes suivantes : "*The*", "*baby*", "*was*", "*born*", "*on*", "*3/4/2016.*" Le service normalise la chaîne "*3/4/2016*" sous la forme "*march fourth two thousand sixteen*". Les informations de synchronisation des mots pour la chaîne reflètent le temps de début "*march*" et le temps de fin "*sixteen*".

    L'exemple suivant indique que le mot `Hello` doit être épelé :

    ```xml
    <say-as interpret-as="letters">Hello</say-as>.
    ```
    {: codeblock}

    Le service renvoie les informations de minutage pour la chaîne "*Hello*". Le service épelle le mot lettre à lettre lors de l'étape de normalisation. Les informations de minutage des mots dans la réponse reflètent le temps de début de la lettre "*h*" et le temps de fin de la lettre "*o*".
-   `<phoneme>` fournit une prononciation pour le texte qui est inclus dans les balises `<phoneme>` d'ouverture et de fermeture. Mais le texte et la balise de fermeture sont facultatifs. L'exemple suivant inclut du texte incorporé et une balise de fermeture :

    ```xml
    The <phoneme alphabet="ibm" ph=".0tx.1me.0fo">tomato</phoneme> was ripe.
    ```
    {: codeblock}

    Le service renvoie des informations de minutage pour les chaînes suivantes : "*The*", "*tomato*", "*was*", "*ripe.*"

    Inversement, l'exemple suivant fournit un élément `<phoneme>` unaire sans texte incorporé ni balise de fermeture :

    ```xml
    The <phoneme alphabet="ibm" ph=".0tx.1me.0fo"/> was ripe.
    ```
    {: codeblock}

    Dans ce cas, le service renvoie des informations de minutage pour les chaînes suivantes : "*The*", "*&lt;phoneme&gt;*", "*was*", "*ripe.*"
-   `<sub>` remplace le texte inclus dans l'attribut `alias` de l'élément par le texte placé entre les balises `<sub>` d'ouverture et de fermeture de l'audio parlé. Par exemple, l'entrée suivante comprend une seule balise `<sub>` :

    ```xml
    I work at <sub alias="International Business Machines">IBM</sub>.
    ```
    {: codeblock}

    Le service produit des informations de minutage pour les chaînes suivantes : "*I*", "*work*", "*at*", "*{{site.data.keyword.IBM_notm}}.*". Le service normalise la chaîne "*{{site.data.keyword.IBM_notm}}*" sous la forme "*International Business Machines*". Les informations de minutage de la chaîne reflètent le temps de début "*International*" et le temps de fin "*Machines*".
-   `<break>` insère une pause dans le texte parlé. Le service reflète le silence obtenu dans le minutage des mots sous la forme d'un écart entre le temps de fin du mot qui précède l'élément `<break>` et le temps de début du mot qui suit l'élément.
- `<paragraph>` (ou `<p>`) peut ajouter un silence à l'audio. Le service ne renvoie pas d'informations de minutage pour les silences.
- `<sentence>` (ou `<s>`) peut ajouter un silence à l'audio. Le service ne renvoie pas d'informations de minutage pour les silences.

Les éléments SSML qui ne sont pas mentionnés dans la liste n'ont aucune incidence sur les informations de minutage des mots. Pour plus d'informations sur la prise en charge de SSML par le service, voir [Utilisation de SSML](/docs/services/text-to-speech?topic=text-to-speech-ssml).

## Exemples avec les éléments mark
{: #timingExample}

Les exemples suivants illustrent une session WebSocket simple entre un client et le service. Les exemples se concentrent sur l'échange de données, et non sur l'ouverture de la connexion. Le client envoie un message texte comprenant deux éléments `<mark>` nommés `SIMPLE` et `EXAMPLE`s et demande que l’audio soit renvoyé au format WAV :

```javascript
{
  "text": "This is a <mark name=\"SIMPLE\"/>simple <mark name=\"EXAMPLE\"/> example.",
  "accept": "audio/wav"
}
```
{: codeblock}

Le service envoie d'abord un message pour confirmer le format audio. Il envoie ensuite plusieurs messages avec les résultats. Le service ne peut pas garantir le nombre de blocs audio qu'il envoie au client ni l'ordre dans lequel les messages texte et audio sont remis.

Les deux réponses suivantes sont possibles. Dans chaque cas, le service envoie deux messages texte qui identifient les emplacements des marques dans le flux binaire. Mais il envoie un nombre arbitraire de messages binaires contenant l'audio. Les informations de minutage d'une marque arrivent toujours avant le bloc audio contenant l'emplacement de la marque.

### Premier exemple de réponse

Dans le premier exemple de réponse, les messages texte sont entrecoupés de plusieurs messages audio.

```javascript
{
  "binary_streams": [
    {
      "content_type": "audio/wav"
    }
  ]
}
... un ou plusieurs blocs d'audio binaire
    tout l'audio précède la marque SIMPLE ...
{
  "marks": [
    [
      "SIMPLE",
      0.7848991042702103
    ]
  ]
}
... un ou plusieurs blocs d'audio binaire
     l'audio peut précéder et suivre la marque SIMPLE
    tout l'audio précède la marque EXAMPLE ...
{
  "marks": [
    [
      "EXAMPLE", 1.0034702987337102
    ]
  ]
}
... un ou plusieurs blocs d'audio binaire
     l'audio peut précéder et suivre la marque EXAMPLE ...
```
{: codeblock}

### Deuxième exemple de réponse

Dans le deuxième exemple de réponse, les messages texte arrivent avant les messages audio.

```javascript
{
  "binary_streams": [
    "content_type": "audio/wav"}
  ]
}
{
  "marks": [
    [
      "SIMPLE", 0.7848991042702103
    ]
  ]
}
{
  "marks": [
    [
      "EXAMPLE", 1.0034702987337102
    ]
  ]
}
... un ou plusieurs blocs d'audio binaire ...
```
{: codeblock}
