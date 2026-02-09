---
title: Création d’identités pour Platform Web SDK
description: Découvrez comment créer des identités dans XDM et utiliser l’élément de données Identity Map pour capturer des identifiants d’utilisateur. Cette leçon fait partie du tutoriel Implémentation d’Adobe Experience Cloud avec le SDK web.
feature: Web SDK, Tags, Identities
jira: KT-15402
exl-id: 7ca32dc8-dd86-48e0-8931-692bcbb2f446
source-git-commit: 1fc027db2232c8c56de99d12b719ec10275b590a
workflow-type: tm+mt
source-wordcount: '907'
ht-degree: 3%

---

# Création d’identités

Découvrez comment capturer des identités avec le SDK web d’Adobe Experience Platform. Capturez les données d’identité authentifiées et non authentifiées sur le [site de démonstration Luma](https://luma.enablementadobe.com/content/luma/us/en.html). Découvrez comment utiliser les éléments de données que vous avez créés précédemment pour collecter des données authentifiées avec un type d’élément de données Platform Web SDK appelé Mappage d’identité.

Cette leçon se concentre sur l’élément de données Mappage d’identités disponible avec l’extension de balises Adobe Experience Platform Web SDK. Vous mappez les éléments de données contenant un identifiant utilisateur authentifié et un statut d’authentification à XDM.


>[!WARNING]
>
> Le site web Luma utilisé dans ce tutoriel devrait être remplacé au cours de la semaine du 16 février 2026. Le travail effectué dans le cadre de ce tutoriel peut ne pas s’appliquer au nouveau site web.

## Objectifs d’apprentissage

À la fin de cette leçon, vous êtes capable de :

* Comprendre la relation entre l’Experience Cloud ID (ECID) et l’identifiant interne de l’appareil (FPID)
* Comprendre la différence entre les identifiants non authentifiés et authentifiés
* Créer un élément de données de mappage d’identités

## Conditions préalables

Vous comprenez ce qu’est une couche de données, vous vous êtes familiarisé avec le [site de démonstration Luma](https://luma.enablementadobe.com/content/luma/us/en.html){target="_blank"} la couche de données et vous savez comment référencer des éléments de données dans les balises. Vous devez avoir terminé les leçons précédentes du tutoriel :

* [Configuration d’un schéma XDM](configure-schemas.md)
* [Configuration d’un espace de noms d’identité](configure-identities.md)
* [Configurer un trains de données](configure-datastream.md)
* [Extension Web SDK installée dans la propriété de balise](install-web-sdk.md)
* [Création d’éléments de données](create-data-elements.md)


## Experience Cloud ID

L’[Experience Cloud ID (ECID)](https://experienceleague.adobe.com/fr/docs/experience-platform/identity/features/ecid) est un espace de noms d’identité partagé utilisé dans les applications Adobe Experience Platform et Adobe Experience Cloud. L’ECID fournit la base de l’identité du client et est l’identité par défaut pour les propriétés numériques. L’ECID est l’identifiant idéal pour suivre le comportement des utilisateurs non authentifiés, car il est toujours présent.

<!-- FYI I commented this out because it was breaking the build - Jack
>[!TIP]
>
> When you use the Experience Platform Web SDK to set up Adobe applications on your digital properties, the ECID is generated at the Adobe Edge server level. As such, ECID is not viewable on the client-side network request payload. You can view the ECID by seeing the Preview tab of the network request, or by using the [Adobe Experience Platform Debugger Edge Trace](set-up-analytics.md#experience-cloud-id-validation).
>![View ECID](assets/validate-dev-console-ecid.png)
-->

En savoir plus sur la manière dont les [ECID sont suivis à l’aide de Platform Web SDK](https://experienceleague.adobe.com/fr/docs/experience-platform/edge/identity/overview).

Les ECID sont définis à l’aide d’une combinaison de cookies propriétaires et de Platform Edge Network. Par défaut, les cookies d’identité propriétaires sont définis côté client par le SDK Web. Pour tenir compte des restrictions du navigateur sur la durée de vie des cookies, vous pouvez choisir de définir vos propres cookies d’identité propriétaires côté serveur. Ces cookies d’identité sont appelés identifiants d’appareil propriétaires (FPID).

>[!IMPORTANT]
>
>L’extension du service Experience Cloud ID [&#128279;](https://exchange.adobe.com/apps/ec/100160/adobe-experience-cloud-id-launch-extension) n’est pas nécessaire lors de l’implémentation de Adobe Experience Platform Web SDK, car la fonctionnalité du service d’ID est intégrée à Platform Web SDK.

## Identifiant d’appareil interne (FPID)

Les FPID sont des cookies propriétaires _que vous définissez à l’aide de vos propres serveurs web_ qu’Adobe utilise ensuite pour créer l’ECID, au lieu d’utiliser le cookie propriétaire défini par le SDK Web. Bien que la prise en charge des navigateurs puisse varier, les cookies propriétaires ont tendance à être plus durables lorsqu’ils sont définis par un serveur qui utilise un enregistrement DNS A (pour IPv4) ou AAAA (pour IPv6), contrairement aux cookies définis par un code CNAME ou JavaScript DNS.

Une fois qu’un cookie FPID est défini, sa valeur peut être récupérée et envoyée à Adobe lors de la collecte des données d’événement. Les FPID collectés sont utilisés comme adresses de contrôle pour générer des ECID sur Platform Edge Network, qui continuent à être les identifiants par défaut dans les applications Adobe Experience Cloud.

Bien que les FPID ne soient pas utilisés dans ce tutoriel, nous vous recommandons de les utiliser dans votre propre mise en œuvre de Web SDK. En savoir plus sur [les identifiants d’appareils propriétaires dans la SDK web de Platform](https://experienceleague.adobe.com/fr/docs/experience-platform/edge/identity/first-party-device-ids)

>[!CAUTION]
>
> Le FPID est une autre manière de générer l’ECID à l’aide d’un cookie défini par vos serveurs web. Il n’est pas utilisé pour identifier les utilisateurs authentifiés.

## Id Authentifié

Comme indiqué ci-dessus, tous les visiteurs de vos propriétés numériques se voient attribuer un ECID par Adobe lors de l’utilisation de Platform Web SDK. ECID est l’identité par défaut pour le suivi des comportements numériques non authentifiés.

Vous pouvez également envoyer un ID utilisateur authentifié afin que Platform puisse créer des [graphiques d’identités](https://experienceleague.adobe.com/fr/docs/platform-learn/tutorials/identities/understanding-identity-and-identity-graphs) et que Target puisse définir son [ID tiers](https://experienceleague.adobe.com/fr/docs/target/using/audiences/visitor-profiles/3rd-party-id). La définition de l’identifiant authentifié est effectuée à l’aide du type d’élément de données [!UICONTROL Identity Map].

Pour créer l’élément de données [!UICONTROL Identity Map] :

1. Accédez à **[!UICONTROL Data Elements]** et sélectionnez **[!UICONTROL Add Data Element]**

1. **[!UICONTROL Nom]** l’élément de données `identityMap.loginID`

1. Sélectionnez **[!UICONTROL Extension]**, puis `Adobe Experience Platform Web SDK`

1. Sélectionnez **[!UICONTROL comme]** Type d’élément de données`Identity map`

1. Une zone d’écran située à droite dans l’interface **[!UICONTROL Collecte de données]** s’affiche pour vous permettre de configurer l’identité :

   ![Interface de collecte de données](assets/identity-identityMap-setup.png)

1. En tant qu’**[!UICONTROL Espace de noms]**, sélectionnez l’espace de noms `lumaCrmId` que vous avez précédemment créé dans la leçon [Configurer les identités](configure-identities.md). S’il n’apparaît pas dans la liste déroulante, saisissez-le.

1. Une fois le **[!UICONTROL Espace de noms]** sélectionné, un identifiant doit être défini. Sélectionnez l’élément de données `user.profile.attributes.username` créé précédemment dans la leçon [Créer des éléments de données](create-data-elements.md#create-data-elements-to-capture-the-data-layer) qui capture un identifiant lorsque les utilisateurs sont connectés au site Luma.

   <!--  >[!TIP]
    >
    >You can verify the **[!UICONTROL Luma CRM ID]** is collected in a data element on the web property by going to the [Luma Demo site](https://luma.enablementadobe.com/content/luma/us/en.html), logging in, [switching the tag environment](validate-with-debugger.md#use-the-experience-platform-debugger-to-map-to-your-tag-property) to your own, and typing `_satellite.getVar("user.profile.attributes.username")` in the web browser developer console.
    >
    >   ![Data Element  ID ](assets/identity-data-element-customer-id.png)
    -->

1. Dans le champ **[!UICONTROL État authentifié]**, sélectionnez **[!UICONTROL Authentifié]**
1. Sélectionner **[!UICONTROL Principal]**

1. Sélectionnez **[!UICONTROL Enregistrer]**

   ![Interface de collecte de données](assets/identity-id-namespace.png)

>[!TIP]
>
> Adobe recommande d’envoyer les identités qui représentent une personne, telles que `Luma CRM Id`, comme identité [!UICONTROL &#x200B; principale].
>
> Si la carte des identités contient l’identifiant de personne (par exemple, `Luma CRM Id`), l’identifiant de personne devient l’identité [!UICONTROL principale]. Dans le cas contraire, `ECID` devient l’identité [!UICONTROL &#x200B; principale &#x200B;].




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

À la fin de ces étapes, les éléments de données suivants doivent être créés :

| Éléments de données d’extension principaux | Éléments De Données De L’Extension Platform Web SDK |
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

Une fois ces éléments de données en place, vous êtes prêt à commencer à envoyer des données à Platform Edge Network en créant une règle dans les balises.

>[!NOTE]
>
>Merci d’avoir investi votre temps dans votre apprentissage de Adobe Experience Platform Web SDK. Si vous avez des questions, souhaitez partager des commentaires généraux ou avez des suggestions sur le contenu futur, veuillez les partager dans ce [article de discussion de la communauté Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996?profile.language=fr)
