---
title: Création d’identités
description: Découvrez comment créer des identités dans XDM et utiliser l’élément de données de carte des identités pour capturer les identifiants d’utilisateur. Cette leçon fait partie du tutoriel Mise en oeuvre de Adobe Experience Cloud avec le SDK Web .
feature: Tags
source-git-commit: f08866de1bd6ede50bda1e5f8db6dbd2951aa872
workflow-type: tm+mt
source-wordcount: '871'
ht-degree: 2%

---

# Création d’identités

Découvrez comment capturer des identités avec le SDK Web Experience Platform. Capturez les données d’identité non authentifiées et authentifiées sur le [Site de démonstration Luma](https://luma.enablementadobe.com/content/luma/us/en.html). Découvrez comment utiliser les éléments de données que vous avez créés précédemment pour collecter des données authentifiées avec un type d’élément de données SDK Web Platform appelé Identity Map.

Quatre nouveaux types d’éléments de données sont introduits par l’extension des balises SDK Web Platform :

1. Identifiant de fusion d’événements
1. Mappage d’identités
1. Variable
1. Objet XDM

Cette leçon porte sur l’élément de données de carte des identités. Vous mappez des éléments de données contenant un ID utilisateur authentifié et un état d’authentification à XDM.

## Objectifs d&#39;apprentissage

À la fin de cette leçon, vous pouvez :

* Comprendre la différence entre l’identifiant Experience Cloud (ECID) et l’identifiant de périphérique propriétaire
* Comprendre la différence entre les ID non authentifiés et les ID authentifiés
* Création d’un élément de données de mappage d’identité

## Conditions préalables

Vous comprenez ce qu’est une couche de données, vous connaissez le [Site de démonstration Luma](https://luma.enablementadobe.com/content/luma/us/en.html){target="_blank"} couche de données et savoir comment référencer des éléments de données dans des balises. Vous devez avoir suivi les étapes précédentes suivantes du tutoriel :

* [Configurer un schéma XDM](configure-schemas.md)
* [Configuration d’un espace de noms d’identité](configure-identities.md)
* [Configurer un trains de données](configure-datastream.md)
* [Extension SDK Web installée dans la propriété de balise](install-web-sdk.md)
* [Créer des éléments de données](create-data-elements.md)

>[!IMPORTANT]
>
>La variable [Extension du service d’ID Experience Cloud](https://exchange.adobe.com/experiencecloud.details.100160.adobe-experience-cloud-id-launch-extension.html) n’est pas nécessaire lors de l’implémentation du SDK Web de Adobe Experience Platform, car la fonctionnalité du service d’ID est intégrée au SDK Web de Platform.

## Experience Cloud ID

La variable [Identifiant Experience Cloud (ECID)](https://experienceleague.adobe.com/docs/experience-platform/identity/ecid.html?lang=en) est un espace de noms d’identité partagé utilisé dans les applications Adobe Experience Platform et Adobe Experience Cloud. ECID constitue la base de l’identité du client et l’identité par défaut des propriétés numériques. Cela fait d’ECID l’identifiant idéal pour le suivi du comportement non authentifié de l’utilisateur, car il est toujours présent.


<!-- FYI I commented this out because it was breaking the build - Jack
>[!TIP]
>
> When you use the Experience Platform Web SDK to set up Adobe applications on your digital properties, the ECID is generated at the Adobe Edge server level. As such, ECID is not viewable on the client-side network request payload. You can view the ECID by seeing the Preview tab of the network request, or by using the [Adobe Experience Platform Debugger Edge Trace](set-up-analytics.md#experience-cloud-id-validation).
>![View ECID](assets/validate-dev-console-ecid.png)
-->

En savoir plus sur la manière dont [Le suivi des ECID s’effectue à l’aide du SDK Web Platform](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/overview.html?lang=en).

Les ECID sont définis à l’aide d’une combinaison de cookies propriétaires et de Platform Edge Network. Par défaut, les cookies propriétaires sont définis par le SDK Web. Pour tenir compte des restrictions du navigateur sur la durée de vie des cookies, vous pouvez choisir de définir et de gérer vos propres cookies propriétaires à la place. On parle alors d’identifiants d’appareil propriétaires (FPID).

## Identifiant de périphérique propriétaire (FPID)

Les FPID sont des cookies propriétaires. _vous définissez à l’aide de vos propres serveurs web ;_ l’Adobe qui utilise ensuite pour définir l’ECID, au lieu d’utiliser le cookie propriétaire défini par le SDK Web. Les cookies propriétaires sont plus efficaces lorsqu’ils sont définis à l’aide d’un serveur qui exploite un enregistrement DNS A (pour IPv4) ou AAAA (pour IPv6), par opposition à un CNAME DNS ou à un code JavaScript.

Une fois qu’un cookie FPID est défini, sa valeur peut être récupérée et envoyée à l’Adobe à mesure que les données d’événement sont collectées. Les FPID collectés sont utilisés comme graines pour générer des ECID sur Platform Edge Network, qui restent les identifiants par défaut dans les applications Adobe Experience Cloud.

En savoir plus sur [Identifiants d’appareil propriétaires dans le SDK Web Platform](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/first-party-device-ids.html?lang=fr)

>[!CAUTION]
>
> FPID est une autre manière de générer l’ECID à l’aide d’un cookie défini par vos serveurs web. Il n’est pas utilisé pour identifier les utilisateurs authentifiés.

## Identifiant authentifié

Comme indiqué ci-dessus, un ECID est attribué par Adobe à tous les visiteurs de vos propriétés numériques lors de l’utilisation du SDK Web Platform. Cela fait d’ECID l’identité par défaut pour le suivi des comportements numériques non authentifiés.

Vous pouvez également envoyer un ID utilisateur authentifié afin que Platform puisse créer des [Graphiques d’identités](https://experienceleague.adobe.com/docs/platform-learn/tutorials/identities/understanding-identity-and-identity-graphs.html?lang=fr), Target peut définir sa valeur tierce . Pour ce faire, utilisez la méthode [!UICONTROL Carte des identités] type d’élément de données.

Pour créer la variable [!UICONTROL Carte des identités] élément de données :

1. Accédez à **[!UICONTROL Éléments de données]** et sélectionnez **[!UICONTROL Ajouter un élément de données]**

1. **[!UICONTROL Nom]** l’élément de données `identityMap.loginID`

1. Comme la variable **[!UICONTROL Extension]**, sélectionnez `Adobe Experience Platform Web SDK`

1. Comme la variable **[!UICONTROL Type d’élément de données]**, sélectionnez `Identity map`

1. Une zone d’écran s’affiche à droite dans la balise **[!UICONTROL Interface de collecte de données]** pour configurer l’identité :

   ![Interface de collecte de données](assets/identity-identityMap-setup.png)

1. Comme la variable  **[!UICONTROL Espace de noms]**, sélectionnez la variable `lumaCrmId` espace de noms que vous avez précédemment créé dans [Configuration des identités](configure-identities.md) leçon.

   >[!NOTE]
   >
   >    Si vous ne voyez pas votre `lumaCrmId` , vérifiez que vous l’avez également créé dans votre environnement de test de production par défaut. Seuls les espaces de noms créés dans l’environnement de test de production par défaut s’affichent actuellement dans la liste déroulante des espaces de noms.

1. Après la **[!UICONTROL Espace de noms]** est sélectionnée, un ID doit être défini. Sélectionnez la variable `user.profile.attributes.username` élément de données créé précédemment dans la variable [Création d’éléments de données](create-data-elements.md#create-data-elements-to-capture-the-data-layer) leçon qui capture un identifiant lorsque les utilisateurs sont connectés au site Luma.

   <!--  >[!TIP]
    >
    >You can verify the **[!UICONTROL Luma CRM ID]** is collected in a data element on the web property by going to the [Luma Demo site](https://luma.enablementadobe.com/content/luma/us/en.html), logging in, [switching the tag environment](validate-with-debugger.md#use-the-experience-platform-debugger-to-map-to-your-tag-property) to your own, and typing `_satellite.getVar("user.profile.attributes.username")` in the web browser developer console.
    >
    >   ![Data Element  ID ](assets/identity-data-element-customer-id.png)
    -->

1. Comme la variable **[!UICONTROL État authentifié]**, sélectionnez **[!UICONTROL Authentifié]**
1. Sélectionner **[!UICONTROL Principal]**

1. Sélectionnez **[!UICONTROL Enregistrer]**.

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

A la fin de ces étapes, les éléments de données suivants doivent être créés :

| Éléments de données d’extension CORE | Éléments de données du SDK Web Platform |
-----------------------------|-------------------------------
| `cart.orderId` | `identityMap.loginID` |
| `page.pageInfo.hierarchie1` | `xdm.variable.content` |
| `page.pageInfo.pageName` | |
| `page.pageInfo.server` | |
| `user.profile.attributes.loggedIn` | |
| `user.profile.attributes.username` | |

Une fois ces éléments de données en place, vous êtes prêt à commencer à envoyer des données à Platform Edge Network via l’objet XDM en créant une règle dans les balises .

[Suivant : ](create-tag-rule.md)

>[!NOTE]
>
>Merci d’avoir consacré du temps à l’apprentissage du SDK Web Adobe Experience Platform. Si vous avez des questions, souhaitez partager des commentaires généraux ou avez des suggestions sur le contenu futur, partagez-les à ce sujet. [Article de discussion de la communauté Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996)
