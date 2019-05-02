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

# SSML d'expressivité 
{: #expressive}

Par défaut, le service {{site.data.keyword.texttospeechfull}} synthétise le texte dans un style déclaratif neutre. Le service étend SSML avec un élément `<express-as>` qui produit une expressivité en convertissant du texte en parole synthétisée dans divers styles de conversation. L'élément est analogue à l'élément SSML `<say-as>`, qui spécifie la normalisation de texte pour le texte mis en forme, tel que les dates, les heures et les nombres.
{: shortdesc}

## Support de langue 
{: #languages-expressive}

Le service prend en charge l’expressivité uniquement pour la voix en anglais américain Allison (`en-US_AllisonVoice`). L'expressivité n'est pas prise en charge avec la voix `en-US_AllisonV2Voice`. L'utilisation de l'élément avec une voix non prise en charge renvoie une erreur. 

## L'élément express-as

Vous pouvez appliquer l'élément `<express-as>` à la totalité du texte, à une phrase ou à un fragment, tel qu'une phrase ou un mot. L'élément accepte un attribut obligatoire, `type`, qui décrit le type d'expression à utiliser pour le texte spécifié : `GoodNews`, `Apology` ou `Uncertainty`.

### GoodNews
{: #goodnews}

`GoodNews` exprime un message positif et optimiste.

```xml
<express-as type="GoodNews">
  Je suis heureux de vous informer que votre demande de prêt a été approuvée.
</express-as>

<express-as type="GoodNews">
  Bonne nouvelle, j'ai pu réduire les paiements sur votre facture mensuelle !!
</express-as>

<express-as type="GoodNews">
  Félicitations pour vos fiançailles ! Vous êtes faits l'un pour l'autre !
</express-as>

<express-as type="GoodNews">
  Super, excellent pour votre promotion ! C'est un poste vraiment prestigieux !
</express-as>
```
{: codeblock}

### Apology
{: #apology}

`Apology` exprime un message de regret.

```xml
<express-as type="Apology">
  Malheureusement, le prochain vol ne partira pas avant cinq heures.
</express-as>

<express-as type="Apology">
  Je suis terriblement désolé pour la qualité du service que vous avez reçu.
</express-as>

<express-as type="Apology">
  Je vous prie de m'excuser pour la suppression de vos fichiers. C'était un accident.
</express-as>

<express-as type="Apology">
  Y a-t-il un moyen de réparer cette erreur ?
</express-as>
```
{: codeblock}

### Uncertainty
{: #uncertainty}

`Uncertainty` véhicule un message incertain et interrogatif.

```xml
<express-as type="Uncertainty">
  Pourrait-elle encore être au bureau ? Elle m'a dit qu'elle pourrait partir plus tôt.
</express-as>

<express-as type="Uncertainty">
  Désolé, je pense avoir mal compris. Etait-ce vendredi ou samedi ?
</express-as>

<express-as type="Uncertainty">
  Pourriez-vous s'il vous plaît expliquer à nouveau ? Je ne suis pas sûr de comprendre.
</express-as>

<express-as type="Uncertainty">
  Je suis désolé, mais je n'ai pas compris votre nom. Pourriez-vous le répéter s'il vous plaît ?
</express-as>
```
{: codeblock}

## Exemples d'expressivité

Les exemples suivants illustrent l'utilisation des trois formes d'expressivité dans l'attribut `text` de la méthode `POST /v1/synthesize`. Le texte à synthétiser est situé dans la plage de l'élément `<speak>` racine SSML. 

```xml
{
  "text": "<speak>
     J'ai été chargé de traiter votre demande de statut de commande.
    <express-as type=\"Apology\">
       Je suis désolé de vous informer que les articles que vous avez demandés sont en rupture de stock.
      Nous vous prions de nous excuser pour la gêne occasionnée.
    </express-as>
    <express-as type=\"Uncertainty\">
       Nous ne savons pas quand les articles seront disponibles.
       Peut-être la semaine prochaine, mais nous n'en sommes pas sûrs pour le moment.
    </express-as>
    <express-as type=\"GoodNews\">
       Mais nous tenons à votre satisfaction, nous vous offrons donc une remise de 50 % sur votre commande !
    </express-as>
  </speak>"
}
```
{: codeblock}
