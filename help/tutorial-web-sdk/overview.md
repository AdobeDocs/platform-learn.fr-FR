---
title: Tutoriel sur lʼimplémentation dʼAdobe Experience Cloud à lʼaide du SDK web
description: Découvrez comment mettre en oeuvre des applications Experience Cloud à l’aide du SDK Web de Adobe Experience Platform.
recommendations: catalog, noDisplay
exl-id: cf0ff74b-e81e-4f6d-ab7d-6c70e9b52d78
source-git-commit: 8602110d2b2ddc561e45f201e3bcce5e6a6f8261
workflow-type: tm+mt
source-wordcount: '717'
ht-degree: 4%

---

# Tutoriel sur lʼimplémentation dʼAdobe Experience Cloud à lʼaide du SDK web

Découvrez comment mettre en oeuvre des applications Experience Cloud à l’aide du SDK Web de Adobe Experience Platform.

Experience Platform Web SDK est une bibliothèque JavaScript côté client qui permet aux clients de Adobe Experience Cloud d’interagir avec les applications Adobe et les services tiers via Adobe Experience Platform Edge Network. Voir [Présentation du SDK Web Adobe Experience Platform](https://experienceleague.adobe.com/en/docs/experience-platform/edge/home) pour plus d’informations.

![Architecture du SDK Web Experience Platform](assets/dc-websdk.png)

Ce tutoriel vous guide tout au long de l’implémentation du SDK Web de Platform sur un exemple de site web de vente au détail appelé Luma. La variable [Site Luma](https://luma.enablementadobe.com/content/luma/us/en.html) dispose d’une couche de données et de fonctionnalités riches qui vous permettent de créer une mise en oeuvre réaliste. Pour ce tutoriel, vous :

* Créez votre propre propriété de balises, dans votre propre compte, avec une mise en oeuvre SDK Web Platform pour le site web Luma.
* Configurez toutes les fonctionnalités de collecte de données pour les implémentations de SDK Web telles que les jeux de données, les schémas et les espaces de noms d’identité.
* Ajoutez les applications Adobe Experience Cloud suivantes :
   * **[Adobe Experience Platform](setup-experience-platform.md)** (et les applications créées sur Platform telles qu’Adobe Real-time Customer Data Platform, Adobe Journey Optimizer et Adobe Customer Journey Analytics)
   * **[Adobe Analytics](setup-analytics.md)**
   * **[Adobe Audience Manager](setup-audience-manager.md)**
   * **[Adobe Target](setup-target.md)**
* Implémentez le transfert d’événement pour envoyer les données collectées par le SDK Web vers des destinations non Adobes.
* Validez votre propre mise en oeuvre du SDK Web Platform à l’aide du débogueur et de l’assurance Experience Platform.

Après avoir terminé ce tutoriel, vous devriez être prêt à commencer à mettre en oeuvre toutes vos applications marketing par le biais du SDK Web Platform sur votre propre site web.


>[!NOTE]
>
>Un tutoriel multisolution similaire est disponible pour [SDK Mobile](../tutorial-mobile-sdk/overview.md).

## Conditions préalables

Tous les clients Experience Cloud peuvent utiliser le SDK Web de Platform. Il n’est pas nécessaire d’acquérir sous licence une application basée sur Platform comme Real-time Customer Data Platform ou Journey Optimizer pour utiliser le SDK Web.

Dans ces leçons, on suppose que vous disposez d’un compte Adobe et des autorisations requises pour terminer les leçons. Si ce n’est pas le cas, vous devez contacter un administrateur Experience Cloud de votre société pour obtenir l’accès.

* Pour **Collecte de données**, vous devez disposer des éléments suivants :
   * **[!UICONTROL Plateformes]**—permission pour **[!UICONTROL Web]** et, si la licence est concédée, **[!UICONTROL Edge]**
   * **[!UICONTROL Droits de propriété]**—autorisation pour **[!UICONTROL Approuver]**, **[!UICONTROL Développer]**, **[!UICONTROL Modifier la propriété]**, **[!UICONTROL Gestion des environnements]**, **[!UICONTROL Gestion des extensions]**, et **[!UICONTROL Publier]**,
   * **[!UICONTROL Droits d’entreprise]**—autorisation pour **[!UICONTROL Gestion des propriétés]**

     Pour plus d’informations sur les autorisations de balise, voir [la documentation](https://experienceleague.adobe.com/en/docs/experience-platform/tags/admin/user-permissions).

* Pour **Experience Platform**, vous devez disposer des éléments suivants :

   * L’accès au **production par défaut**, **&quot;Prod&quot;** sandbox.
   * Accès à **[!UICONTROL Gestion des schémas]** et **[!UICONTROL Affichage des schémas]** under **[!UICONTROL Modélisation des données]**.
   * Accès à **[!UICONTROL Gestion des espaces de noms d’identité]** et **[!UICONTROL Affichage des espaces de noms d’identité]** under **[!UICONTROL Identity Management]**.
   * Accès à **[!UICONTROL Gestion des flux de données]** et **[!UICONTROL Affichage des flux de données]** under **[!UICONTROL Collecte de données]**.
   * Si vous êtes client d’une application basée sur Platform et que vous allez exécuter la variable [Configuration d’un Experience Platform](setup-experience-platform.md) leçon, vous devez également disposer des éléments suivants :
      * Accès à un **development** sandbox.
      * Tous les éléments d’autorisation sous **[!UICONTROL Data Management]**, et **[!UICONTROL Gestion des profils]**:

     Les fonctionnalités requises doivent être disponibles pour tous les clients Experience Cloud, même si vous n’êtes pas client d’une application basée sur Platform telle que Real-Time CDP.

     Pour plus d’informations sur le contrôle d’accès à Platform, voir [la documentation](https://experienceleague.adobe.com/en/docs/experience-platform/access-control/home).

* Pour le paramètre **Adobe Analytics** leçon, vous devez avoir [Accès de l’administrateur aux paramètres de la suite de rapports, aux règles de traitement et à Analysis Workspace](https://experienceleague.adobe.com/en/docs/analytics/admin/admin-console/home)

* Pour le paramètre **Adobe Target** leçon, vous devez avoir [Éditeur ou approbateur](https://experienceleague.adobe.com/en/docs/target/using/administer/manage-users/enterprise/properties-overview#section_8C425E43E5DD4111BBFC734A2B7ABC80) accès.

* Pour le paramètre **Audience Manager** leçon, vous devez avoir accès à la création, à la lecture et à l’écriture de caractéristiques, de segments et de destinations. Pour plus d’informations, consultez le tutoriel sur [Contrôle d’accès en fonction du rôle de l’Audience Manager](https://experienceleague.adobe.com/en/docs/audience-manager-learn/tutorials/setup-and-admin/user-management/setting-permissions-with-role-based-access-control).


>[!NOTE]
>
>Nous partons du principe que vous connaissez les langages de développement front-end tels que HTML et JavaScript. Vous n’avez pas besoin d’être un expert dans ces langues, mais ce tutoriel vous permet de mieux comprendre et lire le code.

## Mises à jour

* 24 avril 2024 : mises à jour majeures comprenant l’ajout de la variable Set/Update, le fractionnement des requêtes de personnalisation et d’analyse, leçons Journey Optimizer

## Chargement du site web Luma

Chargez la variable [Site web Luma](https://luma.enablementadobe.com/content/luma/us/en.html){target="blank"} dans un onglet de navigateur distinct et mettez-le en signet afin que vous puissiez facilement le charger lorsque cela s’avère nécessaire au cours du tutoriel. Vous n’avez pas besoin d’un accès supplémentaire à Luma, hormis la possibilité de charger notre site de production hébergé.

[![Site web Luma](assets/old-overview-luma.png)](https://luma.enablementadobe.com/content/luma/us/en.html){target="blank"}

C’est parti !

[Suivant : ](configure-schemas.md)

>[!NOTE]
>
>Merci d’avoir consacré du temps à l’apprentissage du SDK Web Adobe Experience Platform. Si vous avez des questions, souhaitez partager des commentaires généraux ou avez des suggestions sur le contenu futur, partagez-les à ce sujet. [Article de discussion de la communauté Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996)
