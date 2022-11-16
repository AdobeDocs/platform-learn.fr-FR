---
title: Mise en oeuvre du consentement avec une plateforme de gestion des consentements (CMP)
description: Découvrez comment mettre en oeuvre et activer les données de consentement obtenues à partir d’une plateforme de gestion du consentement (CMP) à l’aide de l’extension SDK Web Adobe Experience Platform dans Data Collection.
feature: Web SDK, Tags
role: Developer, Data Engineer
doc-type: tutorial
exl-id: bee792c3-17b7-41fb-a422-289ca018097d
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '3347'
ht-degree: 2%

---

# Mise en oeuvre du consentement avec une plateforme de gestion du consentement (CMP) à l’aide de l’extension SDK Web Platform

De nombreuses réglementations juridiques relatives à la confidentialité ont introduit des exigences de consentement principal et spécifique en ce qui concerne la collecte de données, la personnalisation et d’autres cas d’utilisation marketing. Pour répondre à ces exigences, Adobe Experience Platform vous permet de capturer les informations de consentement dans des profils client individuels et d’utiliser ces préférences comme facteur déterminant dans la manière dont les données de chaque client sont utilisées dans les workflows Platform en aval.

>[!NOTE]
>
>Adobe Experience Platform Launch est intégré à Adobe Experience Platform comme une suite de technologies destinées à la collecte de données. Plusieurs modifications terminologiques ont été apportées à l’interface que vous devez connaître lors de l’utilisation de ce contenu :
>
> * Le platform launch (côté client) est désormais **[[!DNL tags]](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html?lang=fr)**
> * Le platform launch côté serveur est désormais **[[!DNL event forwarding]](https://experienceleague.adobe.com/docs/experience-platform/tags/event-forwarding/overview.html)**
> * Les configurations Edge sont désormais **[[!DNL datastreams]](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/datastreams.html?lang=fr)**


Ce tutoriel explique comment mettre en oeuvre et activer les données de consentement obtenues à partir d’une plateforme de gestion du consentement (CMP) à l’aide de l’extension SDK Web Platform dans Data Collection. Pour ce faire, nous utiliserons à la fois les normes Adobe et les normes de consentement du TCF 2.0 de l’IAB, avec OneTrust ou Sourcepoint comme exemples de CMP.

Ce tutoriel utilise l’extension SDK Web Platform pour envoyer des données de consentement à Platform. Pour une présentation du SDK Web, voir [cette page](https://experienceleague.adobe.com/docs/experience-platform/edge/home.html?lang=fr).

## Conditions préalables

Les conditions préalables à l’utilisation du SDK Web sont répertoriées. [here](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/prerequisite.html?lang=en#fundamentals).

Sur cette page, un &quot;jeu de données d’événement&quot; est requis et, comme il semble, il s’agit d’un jeu de données destiné à contenir les données d’événement d’expérience. Pour envoyer des informations de consentement avec des événements, la variable [Groupe de champs Détails de confidentialité](https://github.com/adobe/xdm/blob/master/docs/reference/field groups/experience-event/experienceevent-privacy.schema.md) doit être ajouté à votre schéma d’événement d’expérience :

![](./images/event-schema.png)

Pour la norme de consentement de Platform v2.0, nous aurons également besoin d’un accès à Adobe Experience Profile pour créer un schéma et un jeu de données XDM Individual Profile. Pour consulter un tutoriel sur la création de schémas, voir [Création d’un schéma à l’aide de l’éditeur de schémas](https://experienceleague.adobe.com/docs/experience-platform/xdm/tutorials/create-schema-ui.html?lang=en#tutorials) et pour le groupe de champs de profil Détails de la préférence requis, voir [Documentation XDM](https://experienceleague.adobe.com/docs/experience-platform/landing/governance-privacy-security/overview.html?lang=en).

Ce tutoriel suppose que vous avez accès à la collecte de données et que vous avez créé une propriété de balise côté client avec l’extension SDK Web installée et une bibliothèque de travail créée et créée pour le développement. Ces rubriques sont détaillées et affichées dans ces documents :

* [Création ou configuration d’une propriété](https://experienceleague.adobe.com/docs/experience-platform/tags/admin/companies-and-properties.html?lang=en#create-or-configure-a-property)
* [Présentation des bibliothèques](https://experienceleague.adobe.com/docs/experience-platform/tags/publish/libraries.html)
* [Présentation de la publication](https://experienceleague.adobe.com/docs/experience-platform/tags/publish/overview.html)

Nous utiliserons également la variable [Débogueur Platform](https://chrome.google.com/webstore/detail/adobe-experience-platform/bfnnokhpnncpkdmbokanobigaccjkpob) Extension Chrome pour inspecter et valider notre mise en oeuvre.

Pour mettre en oeuvre l’exemple du TCF de l’IAB avec une CMP sur votre propre site, vous devez accéder à une CMP telle que OneTrust ou Sourcepoint pour générer les données qu’ils fournissent. Vous pouvez également suivre cet exemple et consulter les résultats ci-dessous.

## Utilisation du SDK Web avec Adobe Consent Standard (v1.0 ou v2.0)

>[!NOTE]
>
>La norme 1.0 est progressivement abandonnée au profit de la version 2.0. La norme 2.0 vous permet d’ajouter des données de consentement supplémentaires qui peuvent être utilisées pour appliquer manuellement les préférences de consentement. Les captures d’écran ci-dessous de l’extension SDK Web Platform proviennent de la version [2.4.0](https://experienceleague.adobe.com/docs/experience-platform/edge/release-notes.html?lang=en#version-2.4.0) de l’extension compatible avec la version 1.0 ou v2.0 de la norme de consentement de l’Adobe.

Pour plus d’informations sur ces normes, voir [Prise en charge des préférences de consentement du client](https://experienceleague.adobe.com/docs/experience-platform/edge/consent/supporting-consent.html).

### Étape 1 : Configuration du consentement dans l’extension SDK Web

Après avoir installé l’extension SDK Web Platform dans une propriété de balise, nous pouvons configurer les options permettant d’adresser les données de consentement sur l’écran de configuration de l’extension :

![](./images/pending.png)

La section &quot;Confidentialité&quot; définit le niveau de consentement du SDK si l’utilisateur n’a pas fourni de préférences de consentement auparavant. Cela définit l’état par défaut pour la collecte des données de consentement et d’événement dans le SDK. Le paramètre choisi répond à la question &quot;Que doit faire le SDK si l’utilisateur n’a pas encore fourni de préférences de consentement explicite ?&quot;.

* Dans - Collectez les événements qui se produisent avant que l’utilisateur ne fournisse ses préférences de consentement.
* Sortie - Déposez les événements qui se produisent avant que l’utilisateur ne fournisse les préférences de consentement.
* En attente : événements de file d’attente qui se produisent avant que l’utilisateur ne fournisse ses préférences de consentement.
* Fourni par l’élément de données

Si le paramètre de consentement par défaut est &quot;Dans&quot;, cela indique au SDK qu’il ne doit pas attendre le consentement explicite et qu’il doit collecter les événements qui se produisent avant que l’utilisateur ne fournisse les préférences de consentement. Ces préférences sont généralement gérées et stockées dans une CMP.

Si le paramètre de consentement par défaut est &quot;Out&quot;, cela indique au SDK qu’il ne doit collecter aucun événement qui se produit avant que les préférences de consentement de l’utilisateur ne soient définies. L’activité du visiteur qui se produit avant de définir la préférence de consentement ne sera incluse dans aucune donnée envoyée par le SDK une fois le consentement défini. Par exemple, si vous faites défiler et affichez une page web avant de sélectionner la bannière de consentement, et que ce paramètre &quot;Out&quot; est utilisé, l’activité de défilement et l’heure d’affichage ne seront pas envoyées si l’utilisateur fournit ultérieurement un consentement explicite pour la collecte de données.

Si le paramètre de consentement par défaut est &quot;En attente&quot;, le SDK met en file d’attente tous les événements qui se produisent avant que l’utilisateur ne fournisse ses préférences de consentement. Les événements peuvent donc être envoyés une fois les préférences de consentement définies et une fois que le SDK a été initialement configuré au cours d’une visite.

Avec ce paramètre &quot;En attente&quot;, toute tentative d’exécution de commandes nécessitant des préférences de consentement de l’utilisateur (par exemple, la commande d’événement) entraîne la mise en file d’attente de la commande dans le SDK. Ces commandes ne sont pas traitées tant que vous n’avez pas communiqué les préférences de consentement de l’utilisateur au SDK.

Une fois qu’une CMP a collecté les préférences de l’utilisateur, nous pouvons communiquer ces préférences au SDK. Dans une section ultérieure ci-dessous, nous allons voir comment obtenir ces données d’inclusion et les utiliser avec l’extension SDK Web.

&quot;Fourni par l’élément de données&quot; nous permet d’accéder à un élément de données contenant toutes les données de préférences de consentement capturées par un code personnalisé ou une CMP sur votre site ou dans votre couche de données. Un élément de données utilisé à cet effet doit être défini sur &quot;in&quot;, &quot;out&quot; ou &quot;pending&quot;.

Remarque : ce paramètre de configuration du SDK n’est pas conservé pour les profils des utilisateurs. Il est spécifique à la définition du comportement du SDK avant que les préférences de consentement explicite ne soient fournies par le visiteur.

Pour en savoir plus sur la configuration de l’extension SDK Web, voir [Présentation de l’extension SDK Web Platform](https://experienceleague.adobe.com/docs/experience-platform/edge/extension/web-sdk-extension-configuration.html?lang=en#configure-the-extension) et [Prise en charge des préférences de consentement du client](https://experienceleague.adobe.com/docs/experience-platform/edge/consent/supporting-consent.html).

Dans cet exemple, choisissez l’option &quot;En attente&quot; et sélectionnez **Enregistrer** pour enregistrer nos paramètres de configuration.

### Étape 2 : Communication des préférences de consentement

Maintenant que nous avons défini le comportement par défaut du SDK, nous pouvons utiliser des balises pour envoyer les préférences de consentement explicite d’un visiteur à Platform. L’envoi de données de consentement à l’aide de la norme Adobe 1.0 ou 2.0 est facilement mis en oeuvre à l’aide de l’action setConsent du SDK Web dans vos règles de balises.

#### Définition du consentement avec Platform Consent Standard 1.0

Créons une règle pour démontrer cela. Dans la propriété de balise Platform, sélectionnez Règles, puis sur le bouton bleu Ajouter des règles . Nommons la règle &quot;setAdobeConsent&quot; et sélectionnez pour ajouter un événement. Pour le type d’événement, sélectionnez &quot;Fenêtre chargée&quot; qui déclenchera cette règle chaque fois qu’une page sera chargée sur notre site web. Ensuite, sous &quot;Actions&quot;, sélectionnez &quot;Ajouter&quot; pour ouvrir l’écran de configuration des actions. C’est là que nous allons définir les données de consentement. Sélectionnez la liste déroulante &quot;Extension&quot; et sélectionnez &quot;Platform Web SDK&quot;, puis sélectionnez &quot;Action Type&quot; et &quot;Set Consent&quot;.

Sous &quot;Informations de consentement&quot;, sélectionnez &quot;Remplir un formulaire&quot;. Dans cette action de règle, nous utiliserons le SDK Web pour définir le consentement pour la norme de consentement d’Adobe 1.0 en remplissant le formulaire affiché :

![](./images/1-0-form.png)

Nous pouvons choisir de transmettre &quot;Entrée&quot;, &quot;Sortie&quot; ou &quot;Fourni par l’élément de données&quot; avec cette action Définir le consentement . Un élément de données ici doit se résoudre par &quot;in&quot; ou &quot;out&quot;.

Dans cet exemple, nous sélectionnerons &quot;Entrée&quot; pour indiquer que le visiteur a consenti à autoriser le SDK Web à envoyer des données à Platform. Sélectionnez le bouton bleu &quot;Conserver les modifications&quot; pour enregistrer cette action, puis &quot;Enregistrer&quot; pour enregistrer cette règle.

Remarque : Une fois qu’un visiteur du site web s’est désinscrit, le SDK ne vous permet pas de définir le consentement des utilisateurs sur dans .

Les règles de balises peuvent être déclenchées par diverses [events](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/core/overview.html?lang=en) qui peut être utilisé pour transmettre ces données de consentement au moment approprié au cours d’une session de visiteur. Dans l’exemple ci-dessus, nous avons utilisé l’événement window loaded pour déclencher la règle. Dans une section ultérieure, nous utiliserons un événement de préférence de consentement d’une CMP pour déclencher une action Définir le consentement . Vous pouvez utiliser une action Définir le consentement dans une règle déclenchée par tout événement que vous préférez qui indique un paramètre de préférence d’inclusion.

#### Définition du consentement avec Platform Consent Standard 2.0

La version 2.0 de la norme de consentement de Platform fonctionne avec [XDM](https://experienceleague.adobe.com/docs/platform-learn/tutorials/schemas/schemas-and-experience-data-model.html?lang=fr) data. Elle nécessite également l’ajout d’un groupe de champs Détails de confidentialité à votre schéma de profil dans Platform. Voir [Traitement du consentement dans Platform](https://experienceleague.adobe.com/docs/experience-platform/landing/governance-privacy-security/consent/adobe/overview.html) pour plus d’informations sur la version standard d’Adobe 2.0 et ce groupe de champs.

Nous allons créer un élément de données de code personnalisé pour transmettre des données aux propriétés de collecte et de métadonnées de l’objet de consentement affiché dans le schéma ci-dessous :

![](./images/collect-metadata.png)

Ce groupe de champs Détails des préférences contient les champs pour la variable [Type de données XDM Consentements et Préférences](https://experienceleague.adobe.com/docs/experience-platform/xdm/data-types/consents.html?lang=en#prerequisites) qui contiendra les données de préférences de consentement que nous envoyons à Platform avec l’extension SDK Web Platform dans notre action de règle. Actuellement, les seules propriétés requises pour mettre en oeuvre Platform Consent Standard 2.0 sont la valeur de collecte (val) et la valeur de temps des métadonnées, surlignée en rouge ci-dessus.

Créons un élément de données pour ces données. Sélectionnez Data Elements (Éléments de données) et le bouton bleu Add Data Element (Ajouter un élément de données). Appelons cela &quot;xdm-consent 2.0&quot; et, à l’aide de l’extension Core, nous sélectionnerons un type de code personnalisé. Vous pouvez saisir ou copier et coller les données suivantes dans la fenêtre de l’éditeur de code personnalisé :

```js
var dateString = new Date().toISOString();

return {
  collect: {
    val: "y"
  },
  metadata: {
    time: dateString
  }
}
```

Le champ d’heure doit indiquer le moment où l’utilisateur a mis à jour pour la dernière fois ses préférences de consentement. Nous créons ici un horodatage comme exemple à l’aide d’une méthode standard sur l’objet Date JavaScript. Sélectionnez Enregistrer pour enregistrer le code personnalisé et cliquez à nouveau sur Enregistrer pour enregistrer l’élément de données.

Sélectionnez ensuite Règles, puis le bouton bleu Ajouter une règle et saisissez le nom &quot;setConsent onLoad - Consent 2.0&quot;. Sélectionnez l’événement Window Loaded (Fenêtre chargée) comme déclencheur de règle, puis cliquez sur Add (Ajouter) sous Actions. Sélectionnez l’extension SDK Web Platform et, pour le type d’action, choisissez Définir le consentement. La norme doit être Adobe et la version doit être 2.0. Pour la valeur, nous utiliserons l’élément de données que nous venons de créer qui contient les valeurs de collecte et d’heure que nous devons envoyer à Platform :

![](./images/2-0-form.png)

Pour passer en revue cet exemple d’action, nous allons appeler Set Consent from the Platform Web SDK extension et transmettre la norme et la version à partir du formulaire, tout en transmettant les valeurs pour la collecte et l’heure à partir de l’élément de données que nous avons créé précédemment.

Cliquez sur le bouton bleu Enregistrer , puis de nouveau pour enregistrer la règle.

Nous avons maintenant deux règles, une pour chacune des normes de consentement de la plateforme. En pratique, vous choisirez probablement une norme sur l’ensemble de vos sites. Nous allons ensuite créer un exemple en utilisant le standard de consentement IAB TCF 2.0.

## Utilisation du SDK Web avec la norme de consentement du TCF 2.0 de l’IAB

Pour en savoir plus sur la version 2.0 du Transparency and Consent Framework de l’IAB, voir [Site de l’IAB Europe](https://iabeurope.eu/transparency-consent-framework/).

Pour définir les données de préférences de consentement à l’aide de cette norme, nous devons ajouter le groupe de champs Détails de confidentialité à notre schéma Experience Event dans Platform :

![](./images/consentStrings.png)

Ce groupe de champs contient les champs de préférences de consentement requis par la norme IAB TCF 2.0. Pour plus d’informations sur les schémas et les groupes de champs, voir la section [Présentation du système XDM](https://experienceleague.adobe.com/docs/experience-platform/xdm/home.html?lang=fr).

### Étape 1 : Création d’un élément de données de consentement

Pour envoyer des données d’événement de consentement à partir de balises en utilisant la norme de consentement du TCF 2.0 de l’IAB, nous avons d’abord configuré un élément de données xdm avec les champs de consentement requis :

![](./images/data-element.png)

Dans la propriété côté client de vos balises, sélectionnez Éléments de données et le bouton bleu &quot;Ajouter un élément de données&quot;. Nous nommerons cet élément de données &quot;xdm-consentStrings&quot; pour cet exemple. Ces champs xdm contiendront les données de consentement de l’utilisateur requises pour la norme IAB TCF 2.0.

Dans le menu déroulant Extension, sélectionnez &quot;SDK Web Platform&quot;, puis, pour le type d’élément de données, choisissez &quot;Objet XDM&quot;. Le mappeur xdm doit s’afficher, ce qui vous permet de sélectionner et de développer l’élément &quot;consentStrings&quot; comme illustré dans la capture d’écran ci-dessus.

Nous définirons chaque paramètre consentStrings comme suit :

* **`consentStandard`**:  `IAB TCF`
* **`consentStandardVersion`**:  `2.0`
* **`consentStringValue`**:  `%IAB TCF Consent String%`
* **`containsPersonalData`**:  `False` (à partir du bouton Sélectionner la valeur )
* **`gdprApplies`**:  `%IAB TCF Consent GDPR%`

Les variables consentStandard et consentStandardVersion ne sont que des chaînes de texte pour la norme que nous utilisons, qui est la version 2.0 du TCF de l’IAB. La variable consentStringValue fait référence à un élément de données nommé &quot;Chaîne de consentement du TCF de l’IAB&quot;. Les signes de pourcentage autour du texte indiquent le nom d&#39;un élément de données, et nous allons y regarder dans un instant. La propriété containsPersonalData indique si la chaîne de consentement du TCF 2.0 de l’IAB contient des données personnelles avec &quot;True&quot; ou &quot;False&quot;. Le champ gdprApplies indique soit &quot;true&quot; pour l’application du RGPD, soit &quot;false&quot; pour l’application du RGPD, soit &quot;undefined&quot; pour l’application éventuelle du RGPD. Actuellement, le SDK Web traite &quot;non défini&quot; comme &quot;true&quot;. Les données de consentement envoyées avec &quot;gdprApplies&quot; sont donc traitées comme &quot;true&quot; : &quot;non défini&quot; est traité comme si le visiteur se trouve dans une zone où le RGPD s’applique.

Voir [documentation sur le consentement](https://experienceleague.adobe.com/docs/experience-platform/edge/consent/iab-tcf/with-launch.html?lang=en#getting-started) pour plus d’informations sur ces propriétés et sur IAB TCF 2.0 dans les balises .

### Étape 2 : Création d’une règle pour définir le consentement avec IAB TCF 2.0 Standard

Ensuite, nous créons une règle pour définir le consentement avec le SDK Web lorsque les données de consentement pour cette norme sont définies ou modifiées par un visiteur du site Web. Dans cette règle, nous allons également voir comment capturer ces signaux de modification du consentement d’une CMP telle que [OneTrust](https://www.onetrust.com/products/cookie-consent/) ou [Sourcepoint](https://www.sourcepoint.com/cmp/).

#### Ajout d’un événement de règle

Sélectionnez la section Règles dans votre propriété de balise Platform, puis sur le bouton bleu Ajouter une règle . Nommons la règle setConsent - IAB et sélectionnez Ajouter sous Événements. Nommons cet événement addEventListener et sélectionnez Open Editor pour ouvrir l’éditeur de code personnalisé.

Copiez et collez le code suivant dans la fenêtre de votre éditeur :

```js
// Wait for window.__tcfapi to be defined, then trigger when the customer has completed their consent and preferences.
function addEventListener() {
  if (window.__tcfapi) {
    window.__tcfapi("addEventListener", 2, function (tcData, success) {
      if (success && (tcData.eventStatus === "useractioncomplete" || tcData.eventStatus === "tcloaded")) {
        // save the tcData.tcString properties in data elements
        _satellite.setVar("IAB TCF Consent String", tcData.tcString);
        _satellite.setVar("IAB TCF Consent GDPR", tcData.gdprApplies);
        trigger();
      }
    });
  } else {
    // window.__tcfapi wasn't defined. Check again in 100 milliseconds
    setTimeout(addEventListener, 100);
  }
}
addEventListener();
```

Ce code crée et exécute simplement une fonction appelée addEventListener. La fonction vérifie si la fenêtre s’affiche.L’objet __tcfapi existe et, s’il existe, il ajoute un écouteur d’événement en fonction des spécifications de l’API. Vous pouvez en savoir plus sur ces spécifications dans la section [Référentiel IAB](https://github.com/InteractiveAdvertisingBureau/GDPR-Transparency-and-Consent-Framework) sur GitHub. Si cet écouteur d’événement est ajouté avec succès et que le visiteur du site web a terminé ses choix de consentement et de préférences, le code définit des balises pour les variables personnalisées pour tcData tcString et l’indicateur pour les régions RGPD. Pour en savoir plus sur le TCF de l’IAB, voir l’IAB [site web](https://iabeurope.eu/transparency-consent-framework/) et [Référentiel GitHub](https://github.com/InteractiveAdvertisingBureau/GDPR-Transparency-and-Consent-Framework) pour plus de détails techniques. Après avoir défini ces valeurs, le code exécute la fonction de déclenchement qui déclenche l’exécution de cette règle.

Si la fenêtre.__l’objet tcfapi n’existait pas la première fois que cette fonction a été exécutée, la fonction la recherche à nouveau toutes les 100 millisecondes, afin que l’écouteur d’événement puisse être ajouté. La dernière ligne de code exécute simplement la fonction addEventListener définie dans les lignes de code ci-dessus.

Pour résumer, nous avons créé une fonction pour vérifier l’état du consentement défini par un visiteur de site web à l’aide d’une bannière de consentement personnalisée (ou CMP). Lorsque cette préférence de consentement est définie, ce code crée deux variables personnalisées (éléments de données de code personnalisé) que nous pouvons utiliser dans notre action de règle. Après avoir collé le code ci-dessus dans la fenêtre de l’éditeur de code personnalisé de notre événement, sélectionnez le bouton bleu Enregistrer pour enregistrer l’événement de règle.

Configurez maintenant l’action Définir la règle de consentement pour utiliser ces valeurs et les envoyer à Platform.

#### Ajouter une action de règle

Sélectionnez Ajouter dans la section Actions . Sous Extension, sélectionnez SDK Web Platform dans la liste déroulante. Sous Type d’action, sélectionnez Définir le consentement. Nommons cette action setConsent.

Dans la configuration de l’action sous Informations sur le consentement, sélectionnez Remplir un formulaire. Pour Standard, sélectionnez IAB TCF et pour Version saisissez 2.0. Pour la Valeur, nous utiliserons la variable personnalisée de notre événement et saisirons %IAB TCF Consent String% qui provient de la variable [tcData](https://github.com/InteractiveAdvertisingBureau/GDPR-Transparency-and-Consent-Framework/blob/master/TCFv2/IAB%20Tech%20Lab%20-%20CMP%20API%20v2.md#tcdata) nous avons capturé dans notre fonction personnalisée d’événement de règle ci-dessus.

Sous Application RGPD , nous utiliserons l’autre variable personnalisée de notre événement et entrerons %IAB TCF Consent RGPD% qui provient également de tcData que nous avons capturé dans notre fonction personnalisée d’événement de règle ci-dessus. Si vous savez que le RGPD s’appliquera ou non aux visiteurs de ce site Web, vous pouvez sélectionner Oui ou Non, selon le cas, au lieu d’utiliser le choix de variable personnalisée (élément de données). Vous pouvez également utiliser une logique conditionnelle dans un élément de données pour vérifier si le RGPD s’applique et renvoie la valeur appropriée.

Sous le RGPD contient des données personnelles, sélectionnez l’option permettant d’indiquer si les données de cet utilisateur contiennent des données personnelles. Un élément de données ici doit se résoudre sur true ou false.

![](./images/data-element-2-0.png)

Sélectionnez le bouton bleu Enregistrer pour enregistrer l’action et le bouton bleu Enregistrer (ou Enregistrer dans la bibliothèque) pour enregistrer la règle. À ce stade, vous avez implémenté avec succès l’élément de données et la règle dans les balises pour définir le consentement à l’aide de l’extension SDK Web avec la norme de consentement du TCF 2.0 de l’IAB.

### Étape 3 : Enregistrer dans la bibliothèque et créer

Si vous utilisez la variable [bibliothèque de travail](https://experienceleague.adobe.com/docs/platform-learn/implement-in-websites/configure-tags/add-data-elements-rules.html?lang=en#use-the-working-library-feature) prérequis, vous avez déjà enregistré ces modifications et créé votre bibliothèque de développement :

![](./images/save-library.png)

### Étape 4 : Inspect et validation de la collecte de données

Sur notre site, nous actualisons la page et confirmons la version de bibliothèque dans la variable [Debugger](https://chrome.google.com/webstore/detail/adobe-experience-cloud-de/ocdmogmohccmeicdhlhhgepeaijenapj) Extension Chrome, dans la section du menu de balises :

![](./images/build-date.png)

Nous pouvons également examiner l’appel setConsent pour les normes Adobe 1.0 ou 2.0 dans la section du SDK Web de Platform Debugger, en sélectionnant sur la ligne Corps du POST dans la requête réseau où vous voyez `{"consent":[{"value":{"general":"in"},"version…`:

![](./images/inspect-consent-call.png)

Pour valider l’appel setConsent et notre règle pour la norme IAB TCF 2.0, nous utiliserons la bannière de consentement OneTrust sur notre site de test pour définir nos préférences de consentement et créer les données tcData décrites précédemment :

![](./images/banner.png)

Après avoir sélectionné &quot;J’accepte&quot;, nous pouvons examiner l’appel setConsent pour la norme IAB TCF 2.0 dans la section SDK Web de la plateforme du débogueur, en sélectionnant sur la ligne Corps du POST dans la requête réseau où vous voyez `{"consent":[{"value":"someAlphaNumericCharacters…`.

![](./images/inspect-2-0.png)

Nous voyons ici les données que nous avons configurées précédemment dans nos éléments de données et notre règle de balise. La propriété value contient les données tcString codées que nous avons vues précédemment.

OneTrust, Sourcepoint et d’autres CMP qui mettent en oeuvre la norme IAB TCF 2.0 génèrent toutes des données similaires dans nos pages. Nous pouvons capturer ces données et les utiliser avec l’extension SDK Web dans des balises à l’aide de l’événement de code personnalisé dans la règle que nous avons créée ci-dessus. Le code personnalisé sera le même quelle que soit la CMP utilisée pour générer les données IAB TCF 2.0. Le code personnalisé peut également être utilisé avec les normes de consentement de la plateforme (1.0 ou 2.0).

## Envoi de données de consentement avec des événements d’expérience

Vous avez peut-être remarqué que nous ne faisions pas référence à l’élément de données &quot;xdm-consentStrings&quot; que nous avons créé précédemment dans un champ d’élément de données dans l’une de nos règles. Cet élément de données est à utiliser lorsque vous devez envoyer des données de consentement avec un événement d’expérience.

![](./images/consentStrings-data-element.png)

Puisque cet élément de données contient tous les champs requis pour la norme IAB TCF 2.0, vous pouvez simplement référencer l’élément de données lors de l’envoi de ces données xdm avec vos événements d’expérience :

![](./images/consentStrings-reference.png)

## Conclusion

Maintenant que nous avons inspecté et validé les données, vous devriez voir comment mettre en oeuvre et activer les données de consentement obtenues à partir d’une CMP à l’aide de l’extension SDK Web Platform pour Platform.
