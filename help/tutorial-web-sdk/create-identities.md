---
title: Création d’identités pour le SDK Web Platform
description: Découvrez comment créer des identités dans XDM et utiliser l’élément de données de carte des identités pour capturer les identifiants d’utilisateur. Cette leçon fait partie du tutoriel Implémentation d’Adobe Experience Cloud avec le SDK web.
feature: Web SDK, Tags, Identities
jira: KT-15402
exl-id: 7ca32dc8-dd86-48e0-8931-692bcbb2f446
source-git-commit: a8431137e0551d1135763138da3ca262cb4bc4ee
workflow-type: tm+mt
source-wordcount: '876'
ht-degree: 3%

---

# Création d’identités

Découvrez comment capturer des identités avec le SDK web d’Adobe Experience Platform. Capturez les données d’identité non authentifiées et authentifiées sur le [site de démonstration Luma](https://luma.enablementadobe.com/content/luma/us/en.html). Découvrez comment utiliser les éléments de données que vous avez créés précédemment pour collecter des données authentifiées avec un type d’élément de données SDK Web Platform appelé Identity Map.

Cette leçon porte sur l’élément de données Identity Map disponible avec l’extension de balises SDK Web Adobe Experience Platform. Vous mappez des éléments de données contenant un ID utilisateur authentifié et un état d’authentification à XDM.

## Objectifs d&#39;apprentissage

À la fin de cette leçon, vous pouvez :

* Comprendre la relation entre l’identifiant Experience Cloud (ECID) et l’identifiant de périphérique propriétaire (FPID)
* Comprendre la différence entre les ID non authentifiés et les ID authentifiés
* Création d’un élément de données de mappage d’identité

## Conditions préalables

Vous connaissez la couche de données, vous connaissez le [site de démonstration Luma](https://luma.enablementadobe.com/content/luma/us/en.html){target="_blank"} et vous savez comment référencer des éléments de données dans des balises. Vous devez avoir terminé les leçons précédentes du tutoriel :

* [Configurer un schéma XDM](configure-schemas.md)
* [Configuration d’un espace de noms d’identité](configure-identities.md)
* [Configurer un trains de données](configure-datastream.md)
* [Extension SDK Web installée dans la propriété de balise](install-web-sdk.md)
* [Création d’éléments de données](create-data-elements.md)


## Experience Cloud ID

L’ [ identifiant Experience Cloud (ECID)](https://experienceleague.adobe.com/en/docs/experience-platform/identity/features/ecid) est un espace de noms d’identité partagé utilisé dans les applications Adobe Experience Platform et Adobe Experience Cloud. ECID constitue la base de l’identité du client et l’identité par défaut des propriétés numériques. ECID est l’identifiant idéal pour le suivi du comportement des utilisateurs non authentifiés, car il est toujours présent.

<!-- FYI I commented this out because it was breaking the build - Jack
>[!TIP]
>
> When you use the Experience Platform Web SDK to set up Adobe applications on your digital properties, the ECID is generated at the Adobe Edge server level. As such, ECID is not viewable on the client-side network request payload. You can view the ECID by seeing the Preview tab of the network request, or by using the [Adobe Experience Platform Debugger Edge Trace](set-up-analytics.md#experience-cloud-id-validation).
>![View ECID](assets/validate-dev-console-ecid.png)
-->

Découvrez comment [les ECID sont suivis à l’aide du SDK Web Platform](https://experienceleague.adobe.com/en/docs/experience-platform/edge/identity/overview).

Les ECID sont définis à l’aide d’une combinaison de cookies propriétaires et d’Edge Network Platform. Par défaut, les cookies d’identité propriétaires sont définis côté client par le SDK Web. Pour tenir compte des restrictions du navigateur sur la durée de vie des cookies, vous pouvez choisir de définir vos propres cookies d’identité propriétaires côté serveur. Ces cookies d’identité sont appelés identifiants d’appareil propriétaires (FPID).

>[!IMPORTANT]
>
>L’ [extension du service d’ID Experience Cloud](https://exchange.adobe.com/apps/ec/100160/adobe-experience-cloud-id-launch-extension) n’est pas nécessaire lors de l’implémentation du SDK Web de Adobe Experience Platform, car la fonctionnalité du service d’ID est intégrée au SDK Web de Platform.

## Identifiant de périphérique propriétaire (FPID)

Les FPID sont des cookies propriétaires _que vous définissez à l’aide de vos propres serveurs web_, que l’Adobe utilise ensuite pour créer l’ECID, au lieu d’utiliser le cookie propriétaire défini par le SDK Web. Bien que la prise en charge du navigateur puisse varier, les cookies propriétaires ont tendance à être plus durables lorsqu’ils sont définis par un serveur qui exploite un enregistrement DNS A (pour IPv4) ou AAAA (pour IPv6), contrairement à lorsqu’ils sont définis par un CNAME DNS ou un code JavaScript.

Une fois qu’un cookie FPID est défini, sa valeur peut être récupérée et envoyée à l’Adobe à mesure que les données d’événement sont collectées. Les FPID collectés sont utilisés comme graines pour générer des ECID sur Platform Edge Network, qui restent les identifiants par défaut dans les applications Adobe Experience Cloud.

Bien que les FPID ne soient pas utilisés dans ce tutoriel, nous vous recommandons d’utiliser des FPID dans votre propre mise en oeuvre de SDK Web. En savoir plus sur les [identifiants d’appareils propriétaires dans le SDK Web Platform](https://experienceleague.adobe.com/en/docs/experience-platform/edge/identity/first-party-device-ids)

>[!CAUTION]
>
> FPID est une autre manière de générer l’ECID à l’aide d’un cookie défini par vos serveurs web. Il n’est pas utilisé pour identifier les utilisateurs authentifiés.

## Identifiant authentifié

Comme indiqué ci-dessus, un ECID est attribué par Adobe à tous les visiteurs de vos propriétés numériques lors de l’utilisation du SDK Web Platform. ECID est l’identité par défaut pour le suivi des comportements numériques non authentifiés.

Vous pouvez également envoyer un ID utilisateur authentifié afin que Platform puisse créer des [graphiques d’identités](https://experienceleague.adobe.com/en/docs/platform-learn/tutorials/identities/understanding-identity-and-identity-graphs) et que Target puisse définir son [ID tiers](https://experienceleague.adobe.com/en/docs/target/using/audiences/visitor-profiles/3rd-party-id). La définition de l’ID authentifié est effectuée à l’aide du type d’élément de données [!UICONTROL Carte des identités] .

Pour créer l’élément de données [!UICONTROL Carte des identités] :

1. Accédez à **[!UICONTROL Data Elements]** et sélectionnez **[!UICONTROL Add Data Element]**

1. **[!UICONTROL Nom]** de l’élément de données `identityMap.loginID`

1. En tant que **[!UICONTROL Extension]**, sélectionnez `Adobe Experience Platform Web SDK`

1. En tant que **[!UICONTROL Type d’élément de données]**, sélectionnez `Identity map`

1. Une zone d’écran s’affiche à droite dans l’ **[!UICONTROL interface de collecte de données]** pour vous permettre de configurer l’identité :

   ![Interface de collecte de données](assets/identity-identityMap-setup.png)

1. En tant que **[!UICONTROL Espace de noms]**, sélectionnez l’espace de noms `lumaCrmId` que vous avez précédemment créé dans la leçon [Configurer les identités](configure-identities.md). S’il n’apparaît pas dans la liste déroulante, saisissez-le.

1. Une fois l’espace de noms **[!UICONTROL sélectionné, un identifiant doit être défini.]** Sélectionnez l’élément de données `user.profile.attributes.username` créé précédemment dans la leçon [Créer des éléments de données](create-data-elements.md#create-data-elements-to-capture-the-data-layer), qui capture un ID lorsque les utilisateurs sont connectés au site Luma.

   <!--  >[!TIP]
    >
    >You can verify the **[!UICONTROL Luma CRM ID]** is collected in a data element on the web property by going to the [Luma Demo site](https://luma.enablementadobe.com/content/luma/us/en.html), logging in, [switching the tag environment](validate-with-debugger.md#use-the-experience-platform-debugger-to-map-to-your-tag-property) to your own, and typing `_satellite.getVar("user.profile.attributes.username")` in the web browser developer console.
    >
    >   ![Data Element  ID ](assets/identity-data-element-customer-id.png)
    -->

1. En tant que **[!UICONTROL état authentifié]**, sélectionnez **[!UICONTROL Authentifié]**
1. Sélectionnez **[!UICONTROL Principal]**

1. Sélectionnez **[!UICONTROL Save]**

   ![Interface de collecte de données](assets/identity-id-namespace.png)

>[!TIP]
>
> Adobe recommande d’envoyer des identités qui représentent une personne, telles que `Luma CRM Id`, comme identité [!UICONTROL principale].
>
> Si la carte d’identité contient l’identifiant de personne (par exemple, `Luma CRM Id`), l’identifiant de personne devient l’identité [!UICONTROL principale]. Sinon, `ECID` devient l’identité [!UICONTROL principale].




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

| Éléments de données de l’extension Core | Éléments de données d’extension du SDK Web Platform |
-----------------------------|-------------------------------
| `cart.orderId` | `data.variable` |
| `cart.productInfo` | `identityMap.loginID` |
| `cart.productInfo.purchase` | `xdm.variable.content` |
| `page.pageInfo.hierarchie1` | |
| `page.pageInfo.pageName` | |
| `page.pageInfo.server` | |
| `product.category` | |
| `product.productInfo.sku` | |
| `product.productInfo.title` | |
| `user.profile.attributes.loggedIn` | |
| `user.profile.attributes.username` | |

Une fois ces éléments de données en place, vous êtes prêt à commencer à envoyer des données à l’Edge Network Platform en créant une règle dans les balises .

[Suivant : ](create-tag-rule.md)

>[!NOTE]
>
>Merci d’avoir consacré du temps à l’apprentissage du SDK Web Adobe Experience Platform. Si vous avez des questions, souhaitez partager des commentaires généraux ou avez des suggestions sur le contenu à venir, partagez-les sur cet [post de discussion de la communauté Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996)
