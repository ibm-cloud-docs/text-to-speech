---

copyright:
  years: 2015, 2019
lastupdated: "2019-03-28"

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

# Notes sur l'édition 
{: #release-notes}

Les sections suivantes décrivent les nouvelles fonctionnalités et les modifications incluses pour chaque version et mise à jour du service {{site.data.keyword.texttospeechfull}}. Ces informations incluent toutes les limitations connues. Sauf indication contraire, toutes les modifications sont compatibles avec les versions précédentes et sont automatiquement et de manière transparente disponibles pour toutes les applications nouvelles et existantes.
{: shortdesc}

## Limitations connues
{: #limitations}

Un problème lié au déploiement des voix `V2`, Deep Neural Network (DNN), provoque un bruit de fond dans la parole synthétisée. {{site.data.keyword.IBM_notm}} travaille pour résoudre le problème.

## 24 mars 2019 
{: #March2019c}

-   Le service propose désormais des versions DNN (Deep Neural Network) de ses voix allemandes :
    -   `de-DE_BirgitV2Voice`
    -   `de-DE_DieterV2Voice`

    Pour plus d'informations sur les voix basées sur DNN, voir [Technologies de synthèse vocale](/docs/services/text-to-speech/voices.html#technologiesVoices).
-   Toutes les voix du service basées sur DNN prennent désormais en charge les attributs `pitch` et `rate` de l'élément SSML `<prosody>`. Les voix basées sur DNN ne prennent pas en charge l'attribut `volume` de l'élément `<prosody>`. Pour plus d'informations, voir [L'élément prosody](/docs/services/text-to-speech/SSML-elements.html#prosody_element).

## 21 mars 2019 
{: #March2019b}

Les utilisateurs ne peuvent désormais voir que les données d'identification du service associées au rôle attribué à leur compte {{site.data.keyword.cloud_notm}}. Par exemple, si un rôle de lecteur (`reader`) vous est attribué, vous ne pouvez plus voir les niveaux auteur (`writer`)ou supérieur de données d'identification de service. 

Cette modification n'affecte pas l'accès à l'API des utilisateurs ou des applications avec des données d'identification de service existantes. La modification affecte uniquement l'affichage des données d'identification dans {{site.data.keyword.cloud_notm}}.

Pour plus d'informations sur les clés de service et les rôles d'utilisateur, voir [Clés d'API de service IAM](/docs/services/watson?topic=watson-api-key-bp#api-key-bp).

## 4 mars 2019 
{: #March2019a}

Le service propose désormais quatre nouvelles voix qui utilisent une synthèse d’apprentissage en profondeur pour générer de l’audio : 

-   `it-IT_FrancescaV2Voice`
-   `en-US_AllisonV2Voice`
-   `en-US_LisaV2Voice`
-   `en-US_MichaelV2Voice`

Ces nouvelles voix utilisent l'apprentissage automatique et un DNN pour synthétiser du texte en parole. La synthèse basée sur l'apprentissage en profondeur ou DNN produit un audio avec une prosodie plus naturelle et une qualité globale plus uniforme. 

Cependant, ces nouvelles voix produisent également un son avec des qualités de signal différentes de celles des voix existantes, de sorte qu'elles pourraient ne pas convenir à toutes les applications. De plus, les nouvelles voix ne prennent pas en charge les éléments SSML `<prosody>`, `<express-as>` et `<voice-transformation>`.

Pour plus d'informations sur les voix basées sur DNN et sur leurs différences par rapport aux voix existantes, voir [Technologies de synthèse vocale](/docs/services/text-to-speech/voices.html#technologiesVoices).

## Editions antérieures
{: #older}

-   [28 janvier 2019](#January2019)
-   [13 décembre 2018](#December2018)
-   [7 novembre 2018](#November2018)
-   [30 octobre 2018](#October2018)
-   [12 juin 2018](#June2018)
-   [15 mai 2018](#May2018)
-   [2 octobre 2017](#October2017)
-   [14 juillet 2017](#July2017)
-   [10 avril 2017](#April2017)
-   [1er décembre 2016](#December2016)
-   [22 septembre 2016](/docs/services/text-to-speech/release-notes.html#September2016)
-   [23 juin 2016](/docs/services/text-to-speech/release-notes.html#June2016)
-   [10 mars 2016](/docs/services/text-to-speech/release-notes.html#March2016)
-   [22 février 2016](/docs/services/text-to-speech/release-notes.html#February2016)
-   [17 décembre 2015](/docs/services/text-to-speech/release-notes.html#December2015)
-   [21 septembre 2015](/docs/services/text-to-speech/release-notes.html#September2015)
-   [1er juillet 2015](/docs/services/text-to-speech/release-notes.html#July2015)

### 28 janvier 2019
{: #January2019}

L'interface WebSocket prend désormais en charge l'authentification IAM (Identity and Access Management) basée sur un jeton à partir de code JavaScript basé sur un navigateur. La limitation contraire a été supprimée. Pour établir une connexion authentifiée avec la méthode `/v1/synthesize` WebSocket :

-   Si vous utilisez l'authentification IAM, incluez le paramètre de requête `access_token`.
-   Si vous utilisez les données d'identification du service Cloud Foundry, incluez le paramètre de requête `watson-token`.

Pour plus d'informations, voir [Ouverture d'une connexion](/docs/services/text-to-speech/websockets.html#WSopen).

### 13 décembre 2018
{: #December2018}

Le service {{site.data.keyword.texttospeechshort}} est maintenant disponible sur le site {{site.data.keyword.cloud}} de Londres (**eu-gb**). Comme tous les sites, Londres utilise une authentification IAM (Identity and Access Management) basée sur des jetons. Toutes les nouvelles instances de service que vous créez à cet emplacement utilisent l'authentification IAM.

### 7 novembre 2018
{: #November2018}

Le service {{site.data.keyword.texttospeechshort}} est maintenant disponible sur le site {{site.data.keyword.cloud}} de Tokyo (**jp-tok**). Comme tous les sites, Tokyo utilise une authentification IAM (Identity and Access Management) basée sur des jetons. Toutes les nouvelles instances de service que vous créez à cet emplacement utilisent l'authentification IAM.

### 30 octobre 2018
{: #October2018}

Le service {{site.data.keyword.texttospeechshort}} a migré vers l'authentification IAM (Identity and Access Management) par jeton pour tous les sites. Tous les services {{site.data.keyword.cloud_notm}} utilisent maintenant l'authentification IAM. Le service {{site.data.keyword.texttospeechshort}} a migré sur chaque site aux dates suivantes :

-   Dallas (**us-south**) : 30 octobre 2018
-   Francfort (**eu-de**) : 30 octobre 2018
-   Washington, DC (**us-east**) : 12 juin 2018
-   Sydney (**au-syd**): 15 mai 2018

La migration vers l'authentification IAM affecte différemment les nouvelles instances de service et celles existantes :

-   *Toutes les nouvelles instances de service que vous créez à n’importe quel emplacement* utilisent désormais l’authentification IAM pour accéder au service. Vous pouvez transmettre un jeton bearer ou une clé d'API : les jetons prennent en charge les demandes authentifiées sans incorporer les données d'identification du service dans chaque appel ; les clés d'API utilisent l'authentification de base HTTP. Lorsque vous utilisez l'un des logiciels SDK de {{site.data.keyword.ibmwatson}}, vous pouvez transmettre la clé d'API et laisser le SDK gérer le cycle de vie des jetons.
-   *Les instances de service existantes que vous avez créées sur un site avant la date de migration indiquée* continuent à utiliser les `{username}` et `{password}` issus de leurs donnéesd'identification précédentes du service Cloud Foundry pour l'authentification jusqu'à ce que vous les migriez pour utiliser l'authentification IAM. Pour plus d'informations sur la migration vers l'authentification IAM, voir [Migration des instances de service Cloud Foundry vers un groupe de ressources](https://{DomainName}/docs/resources/instance_migration.html).

Pour plus d'informations, consultez la documentation suivante : 

-   Pour connaître le mécanisme d'authentification utilisé par votre instance de service, affichez vos données d'identification de service en cliquant sur l'instance dans le [tableau de bord {{site.data.keyword.cloud_notm}}![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://{DomainName}/dashboard/apps){: new_window}.
-   Pour plus d'informations sur l'utilisation des jetons IAM avec les services {{site.data.keyword.watson}}, voir [Authentification avec des jetons IAM](/docs/services/watson/getting-started-iam.html).
-   Pour plus d'informations sur l'utilisation des clés d'API IAM avec les services {{site.data.keyword.watson}}, voir [Clés d'API de service IAM](/docs/services/watson/apikey-bp.html).
-   Pour des exemples utilisant l'authentification IAM, voir la page de [référence d'API ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://{DomainName}/apidocs/text-to-speech){: new_window}.

### 12 juin 2018
{: #June2018}

Les fonctionnalités suivantes sont activées pour les applications hébergées à Washington, DC (**us-east**) :

-   Le service prend désormais en charge un nouveau processus d'authentification par API. Pour plus d'informations, voir la [mise à jour du service du 30 octobre 2018](#October2018).
-   Le service prend désormais en charge l'en-tête `X-Watson-Metadata` et la méthode `DELETE /v1/user_data`. Pour plus d'informations, voir [Sécurité des informations](/docs/services/text-to-speech/information-security.html).

### 15 mai 2018
{: #May2018}

Les fonctionnalités suivantes sont activées pour les applications hébergées à Sydney, (**au-syd**) :

-   Le service prend désormais en charge un nouveau processus d'authentification par API. Pour plus d'informations, voir la [mise à jour du service du 30 octobre 2018](#October2018).
-   Le service prend désormais en charge l'en-tête `X-Watson-Metadata` et la méthode `DELETE /v1/user_data`. Pour plus d'informations, voir [Sécurité des informations](/docs/services/text-to-speech/information-security.html).

### 2 octobre 2017
{: #October2017}

Pour le format `audio/l16`, vous pouvez désormais spécifier l'ordre d'octets de l’audio renvoyé. (Vous devez déjà spécifier la fréquence d'échantillonnage.) Exemples : `audio/l16;rate=22050;endianness=big-endian` et `audio/l16;rate=22050;endianness=little-endian` ; la valeur par défaut est big endian. Pour plus d'informations, voir [Formats audio](/docs/services/text-to-speech/audio-formats.html).

### 14 juillet 2017
{: #July2017}

Le service prend désormais en charge le format audio MP3 ou MPEG (Motion Picture Experts Group). Pour plus d'informations sur les formats audio pris en charge, voir [Formats audio](/docs/services/text-to-speech/audio-formats.html).

### 10 avril 2017
{: #April2017}

-   Le service prend désormais en charge le format audio Web Media (WebM) avec le codec Opus ou Vorbis. Le service prend désormais également en charge le format audio Ogg avec le codec Vorbis en plus du codec Opus. Pour plus d'informations sur les formats audio pris en charge, voir [Formats audio](/docs/services/text-to-speech/audio-formats.html).
-   Le service prend désormais en charge le partage de ressources d'origine croisée (CORS) pour permettre aux clients basés sur le navigateur d'appeler directement le service. Pour plus d'informations, voir [Prise en charge de CORS](/docs/services/text-to-speech/developer-overview.html#cors).
-   Les codes de réponse HTTP permettant de mener à bien certaines méthodes de l'interface de personnalisation ont été modifiés : 
    -   La méthode `POST /v1/customizations` renvoie désormais 201 (au lieu de 200).
    -   La méthode `POST /v1/customizations/{customization_id}` renvoie désormais 200 (au lieu de 201).
    -   La méthode `POST /v1/customizations/{customization_id}/words` renvoie désormais 200 (au lieu de 201).
    -   La méthode `PUT /v1/customizations/{customization_id}/words/{word}` renvoie désormais 200 (au lieu de 201).
-   Les méthodes `POST /v1/customizations/{custom_id}/words` et `PUT /v1/customizations/{customization_id}/words/{word}` renvoient maintenant le code de réponse HTTP 400 avec le message d'erreur `Part of speech is supported for ja-JP language only` si vous tentez de spécifier une partie `part_of_speech` dans une langue autre que le japonais.
-   La méthode `POST /v1/customizations/{custom_id}/words` renvoie désormais un corps de réponse vide (`{}`).

### 1er décembre 2016
{: #December2016}

-   Le service comprend une nouvelle voix, `es-LA_SofiaVoice`, qui est l'équivalent latino-américain de la voix `es-US_SofiaVoice`. La différence la plus significative entre les deux voix concerne la manière dont elles interprètent le signe dollar `$` : la version latino-américaine utilise le terme *pesos*, tandis que la version nord-américaine utilise le terme *dolares*. D'autres différences mineures pourraient également exister entre les deux voix. 
-   En plus de la voix `en-US_AllisonVoice`, deux autres voix peuvent désormais être transformées avec la transformation de voix SSML : `en-US_LisaVoice` et `en-US_MichaelVoice`. Pour plus d'informations sur la transformation de la voix, voir [SSML de la transformation vocale](/docs/services/text-to-speech/SSML-transformation.html).
-   Lorsque vous utilisez l'interface de personnalisation avec le japonais, le service correspond maintenant au mot le plus long issu des paires mot/traduction définies pour un modèle vocal personnalisé. Par exemple, considérons les deux entrées suivantes pour une voix personnalisée : 

    <pre><code data-copy="false" class="language-javascript">  {
      "words": [
        {"word":"&#65326;&#65337;", "translation":"&#12491;&#12517;&#12540;&#12520;&#12540;&#12463;", "part_of_speech":"Mesi"},
        {"word":"&#65326;&#65337;&#65315;", "translation":"&#12491;&#12517;&#12540;&#12520;&#12540;&#12463;&#12471;&#12486;&#12451;", "part_of_speech":"Mesi"}
      ]
    }</code></pre>

    Si le service trouve la chaîne <code>&#65326;&#65337;&#65315;</code> dans le texte d'entrée, il correspond à ce mot car il s'agit d'une correspondance plus longue que<code>&#65326;&#65337;</code>. Auparavant, le service aurait correspondu à la chaîne <code>&#65326;&#65337;</code>. Pour plus d'informations sur l'utilisation des entrées en japonais pour un modèle vocal personnalisé, voir [Utilisation des entrées en japonais](/docs/services/text-to-speech/custom-rules.html#jaNotes).

### 22 septembre 2016
{: #September2016}

-   L'interface de personnalisation, qui inclut la personnalisation et les méthodes `GET /v1/pronunciation` , est désormais disponible pour toutes les langues prises en charge par le service. L'interface reste une version bêta. Pour plus d'informations, voir [Compréhension de la personnalisation](/docs/services/text-to-speech/custom-intro.html).
-   Le service prend désormais en charge le langage SSML (Speech Synthesis Markup Language) pour le japonais. Pour des informations générales sur la prise en charge de SSML, voir [ Utilisation de SSML](/docs/services/text-to-speech/SSML.html). Pour plus d'informations sur les symboles japonais SPR et IPA, voir [Japanese symbols](/docs/services/text-to-speech/ja-JP-SPRs.html). Des considérations supplémentaires et une zone `part_of_speech` s'appliquent lors de la création d'entrées pour des mots dans un modèle vocal personnalisé japonais. Pour plus d'informations, voir [Utilisation des entrées en japonais](/docs/services/text-to-speech/custom-rules.html#jaNotes).
-   Le service offre maintenant une transformation vocale SSML via le nouvel élément `<voice-transformation>`. Vous pouvez élargir la plage de voix possibles en créant des transformations vocales personnalisées qui modifient la hauteur, la plage, la tension glottale, la respiration, le débit et le timbre d'une voix. Le service propose également deux voix virtuelles intégrées, *Young* et *Soft*. Le service prend actuellement en charge la transformation de la voix uniquement pour la voix en anglais américain, Allison. Pour plus d'informations, voir [SSML de la transformation vocale](/docs/services/text-to-speech/SSML-transformation.html).
-   Le service peut maintenant renvoyer des informations de minutage des mots pour toutes les chaînes du texte saisi que vous transmettez à l'interface WebSocket. Pour recevoir l'heure de début et de fin de chaque chaîne de l'entrée, spécifiez un tableau contenant la chaîne `words` pour le paramètre facultatif `timings` de l'objet JSON que vous transmettez au service. La fonctionnalité n'est actuellement pas disponible pour le texte saisi en japonais. Pour plus d'informations, voir [Obtention du minutage des mots](/docs/services/text-to-speech/word-timing.html).
-   Le service valide maintenant tous les éléments SSML que vous soumettez dans n'importe quel contexte. S'il trouve une balise non valide, le service signale un code de réponse HTTP 400 avec un message descriptif et la méthode échoue. Dans les versions précédentes, le service traitait les erreurs de manière incohérente, indiquer une prononciation de mot non valide, par exemple, peut conduire à un comportement imprévisible ou incohérent. Pour plus d'informations, voir [Validation du SSML](/docs/services/text-to-speech/SSML.html#errors).
-   L'utilisation de `spr` est déconseillée en tant qu'argument de l'option `format` de la méthode `GET /v1/pronunciation` et pour une utilisation avec l'attribut `alphabet` d'un élément SSML `<phoneme>`. Pour utiliser la notation {{site.data.keyword.IBM_notm}} Symbolic Phonetic Representation (SPR), utilisez l'argument `ibm` au lieu de `spr` dans tous les cas.
-   La liste des formats audio pris en charge inclut désormais `audio/mulaw;rate=8000`. De même qu'`audio/basic`, ce format offre un son monocanal codé à l'aide de données u-law (ou mu-law) sur 8 bits, échantillonnées à 8 kHz. Pour plus d'informations, voir [Formats audio](/docs/services/text-to-speech/audio-formats.html).
-   Les méthodes `GET /v1/voices` et `GET /v1/voices/{voice}` renvoient maintenant un objet `supported_features` dans le cadre de leur sortie pour chaque voix. L'objet indique si la voix prend en charge la personnalisation et l'élément SSML `<voice_transformation>`. Pour plus d'informations, voir [Langues et voix](/docs/services/text-to-speech/voices.html).

### 23 juin 2016
{: #June2016}

-   Le service offre maintenant une interface WebSocket pour la synthèse vocale. L'interface offre les mêmes fonctionnalités que la méthode `/v1/synthesize` de l'interface HTTP. Elle accepte le texte brut ou le texte marqué avec SSML. En outre, elle prend en charge l’utilisation de l’élément `<mark>` SSML pour identifier l’heure dans l'audio à laquelle il finit de synthétiser l’ensemble du texte précédant la marque. Pour plus d'informations, voir [Interface WebSocket](/docs/services/text-to-speech/websockets.html).
-   Le service prend désormais en charge le texte annoté avec SSML pour le castillan, l'espagnol nord-américain, l'italien et le brésilien. Le service prenait déjà en charge l’utilisation de SSML pour l’anglais américain et britannique, le français et l'allemand. À compter de cette mise à jour, le service prend en charge SSML pour toutes les langues, sauf le japonais. De plus, vous pouvez utiliser les notations {{site.data.keyword.IBM_notm}} SPR et IPA pour définir les prononciations de mots avec l'élément `<phoneme>` SSML. Pour plus d'informations, voir [Utilisation de SSML](/docs/services/text-to-speech/SSML.html) et [Utilisation d'IBM SPR](/docs/services/text-to-speech/SPRs.html).

    Pour l'anglais américain, vous pouvez également utiliser l'élément `<phoneme>` SSML pour créer des entrées de mot dans un modèle vocal personnalisé. La personnalisation n'est prise en charge que pour l'anglais américain. Pour plus d'informations, voir [Compréhension de la personnalisation](/docs/services/text-to-speech/custom-intro.html).
-   Le service propose une expressivité et un naturel améliorés pour les voix les plus fréquemment utilisées. Les améliorations reposent sur la prédiction de prosodie basée sur un réseau de neurones récurrents (RNN) à partir du texte saisi. Elles sont mises à disposition en tant que nouveau moteur de service et mises à jour de modèles vocaux dans les langues suivantes :

    -   `en-US_AllisonVoice`
    -   `en-US_LisaVoice`
    -   `en-US_MichaelVoice`
    -   `es-ES_EnriqueVoice`
    -   `fr-FR_ReneeVoice`
-   La méthode `GET /v1/pronunciation` accepte désormais un paramètre de requête facultatif `customization_id`. Le paramètre obtient la traduction d'un mot à partir d'un modèle vocal personnalisé spécifié. Si le modèle vocal ne contient pas le mot, la méthode renvoie la prononciation par défaut du mot. Pour plus d'informations, voir la page de [référence d'API ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://{DomainName}/apidocs/text-to-speech){: new_window}.

Lorsque vous utilisez la méthode `GET /v1/pronunciation` sans ID de personnalisation et pour une langue autre que l'anglais américain, vous pouvez demander la prononciation d'un mot uniquement en notation {{site.data.keyword.IBM_notm}} SPR. Pour une langue autre que l'anglais américain, vous devez spécifier `spr` avec l'option `format` de la méthode. {: note}
-   La liste des formats audio pris en charge inclut désormais `audio/basic`, qui fournit un son monocanal codé à l'aide de données u-law (ou mu-law) sur 8 bits, échantillonnées à 8 kHz. Pour plus d'informations, voir [Format audio](/docs/services/text-to-speech/audio-formats.html).
-   Les méthodes HTTP et WebSocket `/v1/synthesize` peuvent renvoyer une réponse `warnings` comprenant des messages relatifs aux paramètres de requête non valides ou des zones JSON incluses dans une demande. Le format des avertissements a changé. L'exemple suivant montre le format précédent :

    `"warnings": "Unknown arguments: [u'{invalid_arg_1}', u'{invalid_arg_2}']."`

    Le même avertissement a maintenant le format suivant : 

    `"warnings": "Unknown arguments: {invalid_arg_1}, {invalid_arg_2}."`

### 10 mars 2016
{: #March2016}

-   Les méthodes `GET` et `POST /v1/synthesize` peuvent désormais renvoyer un en-tête de réponse `Warnings` comprenant une liste de messages d'avertissement concernant des paramètres de requête non valides ou des zones JSON incluses dans la demande. Chaque élément de la liste comprend une chaîne décrivant la nature de l'avertissement, suivie d'un tableau de chaînes d'arguments non valides. Par exemple, `Unknown arguments: [u'{invalid_arg_1}', u'{invalid_arg_2}'].` Pour plus d'informations, voir la page de [référence d'API ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://{DomainName}/apidocs/text-to-speech){: new_window}.
-   Le kit de développement logiciel (SDK) *{{site.data.keyword.watson}} Speech pour le système d'exploitation Apple&reg; iOS* est obsolète et remplacé par le *kit de développement logiciel {{site.data.keyword.watson}} Swift*. Le nouveau SDK est disponible à partir du [référentiel swift-sdk ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://github.com/watson-developer-cloud/swift-sdk){: new_window} dans l'espace de noms `watson-developer-cloud` sur GitHub.

### 22 février 2016
{: #February2016}

Le service a été mis à jour avec une nouvelle fonctionnalité SSML d'expressivité. Le service étend le langage SSML (Speech Synthesis Markup Language) avec un élément `<express-as>` que vous pouvez utiliser pour indiquer l'expressivité dans l'un des trois styles de conversation suivants : `GoodNews` (bonnes nouvelles), `Apology` (excuses) ou `Uncertainty` (incertitude). Vous pouvez appliquer l'élément à l'intégralité du texte, à une phrase, une expression ou un mot. Le service ne prend actuellement en charge l’expressivité que pour la voix en anglais américain Allison (`en-US_AllisonVoice`). Pour plus d'informations, voir [SSML d'expressivité](/docs/services/text-to-speech/SSML-expressive.html).

### 17 décembre 2015
{: #December2015}

-   Le service offre une nouvelle interface de personnalisation que vous pouvez utiliser pour spécifier la façon dont il prononce les mots inhabituels qui apparaissent dans votre saisie. L'interface comprend un certain nombre de nouvelles méthodes que vous pouvez utiliser pour créer et gérer des modèles vocaux personnalisés et les paires mot/traduction qu'ils contiennent. Vous pouvez ensuite utiliser vos modèles personnalisés lors de la synthèse de texte en audio. 

    Le service prend en charge les traductions sous forme de sons et les traductions phonétiques. Les traductions phonétiques peuvent utiliser la représentation standard Alphabet international phonétique (IPA) ou la représentation phonétique symbolique IBM {{site.data.keyword.IBM_notm}}. Vous utilisez le langage SSML (Speech Synthesis Markup Language) pour spécifier les traductions phonétiques. 

    L'interface de personnalisation comprend un ensemble de nouvelles méthodes HTTP portant les noms `POST /v1/customizations`, `POST /v1/customizations/{customization_id}`, `POST /v1/customizations/{customization_id}/words` et `PUT /v1/customizations/{customization_id}/words/{word}`. Le service fournit également une nouvelle méthode `GET /v1/pronunciation` qui renvoie la prononciation de n'importe quel mot et une nouvelle méthode `GET /v1/voices/{voice}` qui renvoie des informations détaillées sur une voix spécifique. De plus, les méthodes existantes de l'interface du service acceptent désormais des paramètres personnalisés de modèle vocal en fonction des besoins. 

    Pour plus d'informations sur la personnalisation et son interface, voir [Compréhension de la personnalisation](/docs/services/text-to-speech/custom-intro.html) et la page de [référence d'API ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://{DomainName}/apidocs/text-to-speech){: new_window}.

    L'interface de personnalisation est une version bêta qui prend actuellement en charge l'anglais américain uniquement. Toutes les méthodes de personnalisation et la méthode `GET /v1/pronunciation` peuvent actuellement être utilisées pour créer et manipuler des modèles vocaux personnalisés et des traductions de mots uniquement en anglais américain.
    {: note}
-   Le service prend en charge une nouvelle voix, `pt-BR_IsabelaVoice`, permettant de synthétiser de l'audio en portugais brésilien avec une voix féminine. Pour plus d'informations, voir [Langues et voix](/docs/services/text-to-speech/voices.html).

### 21 septembre 2015
{: #September2015}

-   Deux nouveaux kits de développement logiciel (SDK) bêta mobiles sont disponibles pour les services vocaux. Les SDK permettent aux applications mobiles d’interagir avec les services {{site.data.keyword.texttospeechshort}} et {{site.data.keyword.speechtotextshort}}. Vous pouvez utiliser les kits de développement logiciel pour envoyer du texte au service {{site.data.keyword.texttospeechshort}} et recevoir une réponse audio. 
    -   *Le SDK {{site.data.keyword.watson}} Swift* est disponible à partir du [référentiel swift-sdk ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://github.com/watson-developer-cloud/swift-sdk){: new_window} dans l'espace de noms `watson-developer-cloud` sur GitHub.
    -   Le *SDK {{site.data.keyword.watson}} Speech Android* est disponible à partir du [référentiel speech-android-sdk ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://github.com/watson-developer-cloud/speech-android-sdk){: new_window} dans l'espace de noms `watson-developer-cloud` sur GitHub.

    Les deux SDK prennent en charge l'authentification avec les services de conversation en utilisant vos données d'identification du service {{site.data.keyword.cloud_notm}} ou un jeton d'authentification. 

Les SDK étant des fonctionnalités bêta, ils sont susceptibles de changer à l'avenir. {: note}
-   Le service prend en charge une nouvelle langue, le japonais. La voix `ja-JP_EmiVoice` est une voix féminine japonaise.

### 1er juillet 2015
{: #July2015}

Le service est passé de la version bêta à la disponibilité générale le 1er juillet 2015. Les différences suivantes existaient entre les versions bêta et GA de l'API {{site.data.keyword.texttospeechshort}}. La version GA nécessitait que les utilisateurs passent à la nouvelle version du service.

-   Un nouveau modèle de programmation prend en charge les interactions directes entre un client et le service. En utilisant ce modèle, un client peut obtenir un jeton d'authentification pour communiquer directement avec le service. A l'aide de ce jeton, le client peut éviter le recours à une application proxy côté serveur dans {{site.data.keyword.cloud_notm}} pour appeler le service en son nom. Les jetons sont le moyen privilégié par les clients pour interagir avec le service. 

Le service continue à prendre en charge l'ancien modèle de programmation reposant sur un proxy côté serveur pour relayer les communications et les données entre le client et le service. Mais le nouveau modèle est plus efficace et fournit un débit plus élevé. Pour plus d'informations sur le nouveau modèle de programmation, voir [Modèles de programmation pour les services {{site.data.keyword.watson}}](/docs/services/watson/getting-started-develop.html).
-   Vous pouvez maintenant passer du langage SSML (Speech Synthesis Markup Language) aux versions HTTP `GET` et `POST` de la méthode `/v1/synthesize`. SSML est un langage de balisage basé sur XML conçu pour fournir des annotations de texte aux applications de synthèse vocale telles que le service {{site.data.keyword.texttospeechshort}}. Pour plus d'informations sur la transmission d'une entrée SSML au service, voir [Spécification du texte d'entrée](/docs/services/text-to-speech/http.html#input).

Le service ne prend initialement en charge l'utilisation de SSML que pour l'anglais britannique et américain, le français et l'allemand. Le service ne prend pas en charge SSML pour une utilisation avec l'italien et l'espagnol. Lorsque vous utilisez SSML, veillez à ne pas sélectionner de voix pour l'audio dans l'une des langues non prises en charge. Les résultats dans ce cas ne sont pas significatifs.
-   Les voix prises en charge pour la synthèse vocale ont été modifiées et étendues. Le service prend désormais en charge un certain nombre de voix, langues et dialectes supplémentaires avec les méthodes `/v1/synthesize`. Pour plus d'informations sur les voix prises en charge, voir [Langues et voix](/docs/services/text-to-speech/voices.html).

    Les trois voix disponibles en version bêta sont renommées pour la disponibilité générale (GA) : 
    -   `VoiceEnUsMichael` s'appelle maintenant `en-US_MichaelVoice`
    -   `VoiceEnUsLisa` s'appelle maintenant `en-US_LisaVoice`
    -   `VoiceEsEsEnrique` s'appelle maintenant `es-ES_EnriqueVoice`

    Les noms précédents de ces voix continuent de fonctionner avec la version bêta du service (via les noeuds finaux de l'API `-beta`) tant que cette version reste disponible. Cependant, vous devez utiliser les nouveaux noms avec la version GA du service.
-   Vous pouvez maintenant demander au service de renvoyer de l'audio au format FLAC (Free Lossless Audio Codec). Le service peut toujours renvoyer de l'audio au format Ogg avec le codec Opus (par défaut) et au format WAV (Waveform Audio File Format). Pour plus d'informations sur l'utilisation de formats audio avec les méthodes `/v1/synthesize`, voir [Formats audio](/docs/services/text-to-speech/audio-formats.html).
-   Le texte que vous envoyez à la méthode `/v1/synthesize` dans l'URL d'une requête HTTP `GET` ou dans le corps d'une requête HTTP `POST` est désormais limité à 5 Ko maximum. Le texte avait une taille maximale de 4 Mo pour la version bêta. 
-   Les méthodes `/v1/synthesize` incluent désormais l’en-tête `X-WDC-PL-OPT-OUT` pour contrôler si le service utilise les résultats texte et audio d’une opération afin d'améliorer les résultats futurs. Spécifiez la valeur `1` pour l'en-tête afin d'empêcher le service d'utiliser des résultats de texte et audio. Le paramètre s'applique uniquement à la demande en cours. Le nouvel en-tête remplace l'en-tête `X-logging` provenant des méthodes bêta. Pour plus d'informations, voir [Contrôle de la journalisation des demandes pour les services {{site.data.keyword.watson}}](/docs/services/watson/getting-started-logging.html).
-   Pour les méthodes `/v1/synthesize`, les codes d'erreur suivants ont été modifiés :
    -   Le code d'erreur 406 ("Not acceptable. Unsupported MIME type.") est supprimé.
    -   Le code d'erreur 415 ("Unsupported Media Type") est ajouté.
    -   Le code d'erreur 503 ("Service Unavailable") est ajouté.
-   Pour la méthode `GET /v1/voices`, les codes d'erreur suivants ont été modifiés :
    -   Le code d'erreur 406 ("Not acceptable. Unsupported MIME type.") est supprimé.
    -   Le code d'erreur 415 ("Unsupported Media Type") est ajouté.
