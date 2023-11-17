---
title: Créer des éléments de données
description: Découvrez comment créer un objet XDM et y mapper des éléments de données dans des balises. Cette leçon fait partie du tutoriel Mise en oeuvre de Adobe Experience Cloud avec le SDK Web .
feature: Tags
exl-id: d662ec46-de9b-44ba-974a-f81dfc842e68
source-git-commit: 4a12f8261cf1fb071bc70b6a04c34f6c16bcce64
workflow-type: tm+mt
source-wordcount: '1201'
ht-degree: 7%

---

# Créer des éléments de données

Découvrez comment créer les éléments de données essentiels nécessaires pour capturer des données avec le SDK Web Experience Platform. Capturez à la fois les données de contenu et d’identité sur le [Site de démonstration Luma](https://luma.enablementadobe.com/content/luma/us/en.html). Découvrez comment utiliser le schéma XDM que vous avez créé précédemment pour collecter des données à l’aide du SDK Web Platform par le biais d’un nouveau type d’élément de données appelé Objet XDM.

>[!NOTE]
>
> À des fins de démonstration, les exercices de cette leçon s’appuient sur l’exemple utilisé pendant [Configuration d’un schéma](configure-schemas.md) création d’exemples d’objets XDM qui capturent le contenu affiché et les identités des utilisateurs sur la page [Site de démonstration Luma](https://luma.enablementadobe.com/content/luma/us/en.html).

>[!IMPORTANT]
>
>Les données de cette leçon proviennent de la `[!UICONTROL digitalData]` couche de données sur le site Luma. Pour afficher la couche de données, ouvrez votre console de développement et saisissez `[!UICONTROL digitalData]` pour afficher la couche de données complète disponible.![couche de données digitalData](assets/data-element-data-layer.png)


Quel que soit le SDK Web Platform, vous devez continuer à créer des éléments de données dans votre propriété de balise qui mappent les variables de collecte de données de votre site web, tels qu’une couche de données, un attribut de HTML ou d’autres. Une fois que vous avez créé ces éléments de données, vous devez les mapper au schéma XDM que vous avez créé lors de la [configuration des schémas](configure-schemas.md) leçon. Pour ce faire, l’extension SDK Web Platform met à disposition un nouveau type d’élément de données appelé objet XDM. Par conséquent, la création d’éléments de données se compose de deux actions :

1. Mappage des variables de site web aux éléments de données et
1. Mappage de ces éléments de données à un objet XDM

Pour l’étape 1, vous continuez à mapper votre couche de données aux éléments de données comme vous le faites actuellement, à l’aide de l’un des types d’éléments de données de l’extension de balise Core. Pour l’étape 2, l’extension Platform Web SDK crée un ensemble de nouveaux types d’éléments de données qui n’étaient pas disponibles auparavant :

* Identifiant de fusion d’événements
* Mappage d’identités
* Objet XDM

Cette leçon se concentre sur les types d’éléments de données d’objet XDM et de mappage d’identité. Vous allez créer des objets XDM pour capturer l’activité et l’état d’authentification des visiteurs Luma.

## Objectifs d&#39;apprentissage

À la fin de cette leçon, vous pouvez :

* Création d’éléments de données pour capturer du contenu et des données d’ID de connexion utilisateur
* Création d’un élément de données de mappage d’identité
* Mise en correspondance des éléments de données avec un élément de données d’objet XDM


## Conditions préalables

Vous comprenez ce qu’est une couche de données, vous connaissez le [Site de démonstration Luma](https://luma.enablementadobe.com/content/luma/us/en.html){target="_blank"} couche de données et savoir comment référencer des éléments de données dans des balises. Vous devez avoir suivi les étapes précédentes suivantes du tutoriel.

* [Configurer les autorisations](configure-permissions.md)
* [Configurer un schéma XDM](configure-schemas.md)
* [Configuration d’un espace de noms d’identité](configure-identities.md)
* [Configurer un trains de données](configure-datastream.md)
* [Extension SDK Web installée dans la propriété de balise](install-web-sdk.md)

>[!IMPORTANT]
>
>La variable [Extension du service d’ID Experience Cloud](https://exchange.adobe.com/experiencecloud.details.100160.adobe-experience-cloud-id-launch-extension.html) n’est pas nécessaire lors de l’implémentation du SDK Web de Adobe Experience Platform, car la fonctionnalité du service d’ID est intégrée au SDK Web de Platform.

## Créer des éléments de données pour capturer la couche de données

Avant de commencer la création de l’objet XDM, créez l’ensemble suivant d’éléments de données mappés à l’objet [Site de démonstration Luma](https://luma.enablementadobe.com/content/luma/us/en.html){target="_blank"} couche de données :

1. Accédez à **[!UICONTROL Éléments de données]** et sélectionnez **[!UICONTROL Ajouter un élément de données]** (ou **[!UICONTROL Créer un élément de données]** s’il n’existe aucun élément de données existant dans la propriété de balise)

   ![Créer un élément de données](assets/data-element-create.jpg)

1. Nommez l’élément de données `page.pageInfo.pageName`.
1. Utilisez la variable **[!UICONTROL Variable JavaScript]** **[!UICONTROL Type d’élément de données]** pour pointer vers une valeur dans la couche de données de Luma : `digitalData.page.pageInfo.pageName`

1. Cochez les cases pour **[!UICONTROL Forcer la valeur minuscule]** et **[!UICONTROL Nettoyer le texte]** pour normaliser la casse et supprimer les espaces superflus.

1. Laisser `None` comme la propriété **[!UICONTROL Durée de stockage]** car cette valeur est différente sur chaque page

1. Sélectionnez **[!UICONTROL Enregistrer]**

   ![Élément de données Nom de page](assets/data-element-pageName.jpg)

Suivez les mêmes étapes pour créer ces quatre éléments de données supplémentaires :

* **`page.pageInfo.server`** mappé à .
  `digitalData.page.pageInfo.server`

* **`page.pageInfo.hierarchie1`** mappé à .
  `digitalData.page.pageInfo.hierarchie1`

* **`user.profile.attributes.username`** mappé à .
  `digitalData.user.0.profile.0.attributes.username`

* **`user.profile.attributes.loggedIn`** mappé à .
  `digitalData.user.0.profile.0.attributes.loggedIn`

* **`cart.orderId`** mappé à `digitalData.cart.orderId` (vous utiliserez cette méthode lors de la [Configuration d’Analytics](setup-analytics.md) leçon)


>[!CAUTION]
>
>La variable [!UICONTROL Variable JavaScript] Le type d’élément de données traite les références aux tableaux comme des points plutôt que des crochets. Par conséquent, le fait de référencer l’élément de données username comme `digitalData.user[0].profile[0].attributes.username` **ne fonctionnera pas**.

## Créer un élément de données de carte des identités

Vous pouvez ensuite créer l’élément de données de carte des identités :

1. Accédez à **[!UICONTROL Éléments de données]** et sélectionnez **[!UICONTROL Ajouter un élément de données]**

1. **[!UICONTROL Nom]** l’élément de données `identityMap.loginID`

1. Comme la variable **[!UICONTROL Extension]**, sélectionnez `Adobe Experience Platform Web SDK`

1. Comme la variable **[!UICONTROL Type d’élément de données]**, sélectionnez `Identity map`

1. Une zone d’écran s’affiche à droite dans la balise **[!UICONTROL Interface de collecte de données]** pour configurer l’identité :

   ![Interface de collecte de données](assets/identity-identityMap-setup.png)

1. Comme la variable  **[!UICONTROL Espace de noms]**, sélectionnez la variable `Luma CRM Id` espace de noms que vous avez précédemment créé dans [Configuration des identités](configure-identities.md) leçon.

   >[!NOTE]
   >
   >    Si vous ne voyez pas votre `Luma CRM Id` , vérifiez que vous l’avez également créé dans votre environnement de test de production par défaut. Seuls les espaces de noms créés dans l’environnement de test de production par défaut s’affichent actuellement dans la liste déroulante des espaces de noms.

1. Après la **[!UICONTROL Espace de noms]** est sélectionnée, un ID doit être défini. Sélectionnez la variable `user.profile.attributes.username` élément de données créé plus tôt dans cette leçon, qui capture un identifiant lorsque les utilisateurs sont connectés au site Luma.

<!--  >[!TIP]
   >
   >You can verify the **[!UICONTROL Luma CRM ID]** is collected in a data element on the web property by going to the [Luma Demo site](https://luma.enablementadobe.com/content/luma/us/en.html), logging in, [switching the tag environment](validate-with-debugger.md#use-the-experience-platform-debugger-to-map-to-your-tag-property) to your own, and typing `_satellite.getVar("user.profile.attributes.username")` in the web browser developer console.
   >
   >   ![Data Element  ID ](assets/identity-data-element-customer-id.png)
-->

1. Comme la variable **[!UICONTROL État authentifié]**, sélectionnez **[!UICONTROL Authentifié]**
1. Sélectionner **[!UICONTROL Principal]**

1. Sélectionnez **[!UICONTROL Enregistrer]**

   ![Interface de collecte de données](assets/identity-id-namespace.png)

>[!TIP]
>
> Adobe recommande d’envoyer des identités représentant une personne, telles que `Luma CRM Id`, en tant que [!UICONTROL primary] identité.
>
> Si la carte d’identité contient l’identifiant de personne (par exemple, `Luma CRM Id`), l’identifiant de personne deviendra la variable [!UICONTROL primary] identité. Sinon, `ECID` se transforme en [!UICONTROL primary] identité.





<!--
1. Once the data element is configured in **[!UICONTROL Data Collection interface]**, it can be tested on the Luma web property like any other Data Element. Enter the following script in the browser developer console
   
   
   ```
   _satellite.getVar('identityMap.loginID')
   ```  

   ![Data Collection interface](assets/identity-consoleIdentityDataElement.png)
   
   >[!NOTE]
   >
   >ECID identifier will NOT populate in the Data Element, as this is configured already with Platform Web SDK.   
-->

## Mise en correspondance des éléments de données avec les objets XDM

Tous les éléments de données que vous créez doivent être mappés à un objet XDM. Cet objet doit être conforme au schéma XDM que vous avez créé lors de la [Configuration d’un schéma](configure-schemas.md) leçon.

Il existe différentes manières de mapper des éléments de données à des champs d’objet XDM. Vous pouvez mapper des éléments de données individuels à des champs XDM individuels ou mapper des éléments de données à des objets XDM entiers tant que votre élément de données correspond au schéma de paire clé-valeur exact présent dans l’objet XDM. Dans cette leçon, vous allez capturer des données de contenu en les mappant à des champs individuels. Vous apprendrez à [mappage d’un élément de données à un objet XDM entier](setup-analytics.md#Map-an-entire-array-to-an-XDM-Object) dans le [Configuration d’Analytics](setup-analytics.md) leçon.

Créez un objet XDM pour capturer des données de contenu :

1. Dans le volet de navigation de gauche, sélectionnez **[!UICONTROL Éléments de données]**
1. Sélectionnez **[!UICONTROL Ajouter un élément de données]**
1. **** Nommez l’élément de données . **`xdm.content`**
1. Comme la variable **[!UICONTROL Extension]** select `Adobe Experience Platform Web SDK`
1. Comme la variable **[!UICONTROL Type d’élément de données]** select `XDM object`
1. Sélectionner la plateforme **[!UICONTROL Sandbox]** dans lequel vous avez créé le schéma XDM au cours de la [Configurer un schéma XDM](configure-schemas.md) leçon, dans cet exemple `DEVELOPMENT Mobile and Web SDK Courses`
1. Comme la variable **[!UICONTROL Schéma]**, sélectionnez `Luma Web Event Data` schema :

   ![Objet XDM](assets/data-element-xdm.content-fields.png)

   >[!NOTE]
   >
   >L’environnement de test correspond à l’environnement de test Experience Platform dans lequel vous avez créé le schéma. Plusieurs environnements de test peuvent être disponibles dans votre instance d’Experience Platform. Veillez donc à sélectionner le bon environnement de test. Travaillez toujours en développement d’abord, puis en production.

1. Faites défiler l’écran vers le bas jusqu’à ce que vous atteigniez le **`web`** objet
1. Sélectionner pour l’ouvrir

   ![Objet Web](assets/data-element-pageviews-xdm-object.png)


1. Mappage des variables XDM web suivantes aux éléments de données

   * **`web.webPageDetials.name`** vers `%page.pageInfo.pageName%`
   * **`web.webPageDetials.server`** vers `%page.pageInfo.server%`
   * **`web.webPageDetials.siteSection`** vers `%page.pageInfo.hierarchie1%`

   ![Objet XDM](assets/data-element-xdm.content.png)

1. Recherchez ensuite le `identityMap` dans le schéma et sélectionnez-le.

1. Associer à la variable `identityMap.loginID` élément de données

1. Sélectionnez **[!UICONTROL Enregistrer]**

   ![Interface de collecte de données](assets/identity-dataElements-xdmContent-LumaSchema-identityMapSelect3.png)




A la fin de ces étapes, les éléments de données suivants doivent être créés :

| Éléments de données d’extension CORE | Éléments de données du SDK Web Platform |
-----------------------------|-------------------------------
| `cart.orderId` | `identityMap.loginID` |
| `page.pageInfo.hierarchie1` | `xdm.content` |
| `page.pageInfo.pageName` | |
| `page.pageInfo.server` | |
| `user.profile.attributes.loggedIn` | |
| `user.profile.attributes.username` | |

Une fois ces éléments de données en place, vous êtes prêt à commencer à envoyer des données à Platform Edge Network via l’objet XDM en créant une règle dans les balises .

[Suivant : ](create-tag-rule.md)

>[!NOTE]
>
>Merci d’avoir consacré du temps à l’apprentissage du SDK Web Adobe Experience Platform. Si vous avez des questions, souhaitez partager des commentaires généraux ou avez des suggestions sur le contenu futur, partagez-les à ce sujet. [Article de discussion de la communauté Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996)
