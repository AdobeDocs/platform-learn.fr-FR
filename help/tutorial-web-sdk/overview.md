---
title: Tutoriel sur lʼimplémentation dʼAdobe Experience Cloud à lʼaide du SDK web
description: Découvrez comment implémenter des applications Experience Cloud à l’aide du SDK web d’Adobe Experience Platform.
recommendations: catalog, noDisplay
exl-id: cf0ff74b-e81e-4f6d-ab7d-6c70e9b52d78
source-git-commit: 8602110d2b2ddc561e45f201e3bcce5e6a6f8261
workflow-type: tm+mt
source-wordcount: '717'
ht-degree: 7%

---

# Tutoriel sur lʼimplémentation dʼAdobe Experience Cloud à lʼaide du SDK web

Découvrez comment implémenter des applications Experience Cloud à l’aide du SDK web d’Adobe Experience Platform.

Experience Platform Web SDK est une bibliothèque JavaScript côté client qui permet aux clients de Adobe Experience Cloud d’interagir avec les applications d’Adobe et les services tiers via l’Edge Network Adobe Experience Platform. Pour plus d’informations, voir [Présentation du SDK Web Adobe Experience Platform](https://experienceleague.adobe.com/fr/docs/experience-platform/edge/home) .

![Architecture du SDK Web Experience Platform](assets/dc-websdk.png)

Ce tutoriel vous guide tout au long de l’implémentation du SDK Web de Platform sur un exemple de site web de vente au détail appelé Luma. Le [site Luma](https://luma.enablementadobe.com/content/luma/us/en.html) dispose d’une couche de données et de fonctionnalités riches qui vous permettent de créer une mise en oeuvre réaliste. Pour ce tutoriel, vous :

* Créez votre propre propriété de balises, dans votre propre compte, avec une mise en oeuvre SDK Web Platform pour le site web Luma.
* Configurez toutes les fonctionnalités de collecte de données pour les implémentations de SDK Web telles que les jeux de données, les schémas et les espaces de noms d’identité.
* Ajoutez les applications Adobe Experience Cloud suivantes :
   * **[Adobe Experience Platform](setup-experience-platform.md)** (et applications créées sur Platform telles qu’Adobe Real-Time Customer Data Platform, Adobe Journey Optimizer et Adobe Customer Journey Analytics)
   * **[Adobe Analytics](setup-analytics.md)**
   * **[Adobe Audience Manager](setup-audience-manager.md)**
   * **[Adobe Target](setup-target.md)**
* Implémentez le transfert d’événement pour envoyer les données collectées par le SDK Web vers des destinations non Adobes.
* Validez votre propre mise en oeuvre du SDK Web Platform à l’aide du débogueur et de l’assurance Experience Platform.

Après avoir terminé ce tutoriel, vous devriez être prêt à commencer à mettre en oeuvre toutes vos applications marketing par le biais du SDK Web Platform sur votre propre site web.


>[!NOTE]
>
>Un tutoriel multisolution similaire est disponible pour le [SDK mobile](../tutorial-mobile-sdk/overview.md).

## Conditions préalables

Tous les clients Experience Cloud peuvent utiliser le SDK Web de Platform. Il n’est pas nécessaire d’acquérir sous licence une application basée sur Platform comme Real-Time Customer Data Platform ou Journey Optimizer pour utiliser le SDK Web.

Dans ces leçons, on suppose que vous disposez d’un compte Adobe et des autorisations requises pour terminer les leçons. Si ce n’est pas le cas, vous devez contacter un administrateur Experience Cloud de votre société pour obtenir l’accès.

* Pour **Data Collection**, vous devez disposer des éléments suivants :
   * **[!UICONTROL Plateformes]**—permission pour **[!UICONTROL Web]** et, si une licence est accordée, **[!UICONTROL Edge]**
   * **[!UICONTROL Droits de propriété]**—autorisation de **[!UICONTROL Approve]**, **[!UICONTROL Develop]**, **[!UICONTROL Edit Property]**, **[!UICONTROL Manage Environments]**, **[!UICONTROL Manage Extensions]** et **[!UICONTROL Publish]**,
   * **[!UICONTROL Droits d’entreprise]**—autorisation de **[!UICONTROL Gérer les propriétés]**

     Pour plus d&#39;informations sur les autorisations de balise, consultez [la documentation](https://experienceleague.adobe.com/fr/docs/experience-platform/tags/admin/user-permissions).

* Pour **Experience Platform**, vous devez disposer des éléments suivants :

   * Accès à l’environnement de test **production par défaut**, **&quot;Prod&quot;**.
   * Accédez à **[!UICONTROL Gérer les schémas]** et **[!UICONTROL Afficher les schémas]** sous **[!UICONTROL Modélisation de données]**.
   * Accédez à **[!UICONTROL Gérer les espaces de noms d’identité]** et **[!UICONTROL Afficher les espaces de noms d’identité]** sous **[!UICONTROL Identity Management]**.
   * Accès à **[!UICONTROL Gérer les données]** et **[!UICONTROL Afficher les données]** sous **[!UICONTROL Collecte de données]**.
   * Si vous êtes client d’une application basée sur Platform et que vous allez terminer la leçon [Configurer un Experience Platform](setup-experience-platform.md), vous devez également disposer des éléments suivants :
      * Accès à un environnement de test **development**.
      * Tous les éléments d’autorisation sous **[!UICONTROL Data Management]** et **[!UICONTROL Profile Management]** :

     Les fonctionnalités requises doivent être disponibles pour tous les clients Experience Cloud, même si vous n’êtes pas client d’une application basée sur Platform telle que Real-Time CDP.

     Pour plus d’informations sur le contrôle d’accès à Platform, voir [la documentation](https://experienceleague.adobe.com/fr/docs/experience-platform/access-control/home).

* Pour la leçon facultative **Adobe Analytics**, vous devez disposer d’[ accès administrateur aux paramètres de suite de rapports, aux règles de traitement et à Analysis Workspace](https://experienceleague.adobe.com/fr/docs/analytics/admin/admin-console/home).

* Pour la leçon facultative **Adobe Target**, vous devez disposer de l’accès [Éditeur ou approbateur](https://experienceleague.adobe.com/fr/docs/target/using/administer/manage-users/enterprise/properties-overview#section_8C425E43E5DD4111BBFC734A2B7ABC80).

* Pour la leçon facultative **Audience Manager**, vous devez avoir accès à la création, à la lecture et à l’écriture de caractéristiques, de segments et de destinations. Pour plus d’informations, reportez-vous au tutoriel sur le [contrôle d’accès en fonction du rôle](https://experienceleague.adobe.com/fr/docs/audience-manager-learn/tutorials/setup-and-admin/user-management/setting-permissions-with-role-based-access-control) de l’Audience Manager.


>[!NOTE]
>
>Nous partons du principe que vous connaissez les langages de développement front-end tels qu’HTML et JavaScript. Vous n’avez pas besoin d’être un expert dans ces langues, mais ce tutoriel vous permet de mieux comprendre et lire le code.

## Mises à jour

* 24 avril 2024 : mises à jour majeures comprenant l’ajout de la variable Set/Update, le fractionnement des requêtes de personnalisation et d’analyse, leçons Journey Optimizer

## Chargement du site web Luma

Chargez le [site web Luma](https://luma.enablementadobe.com/content/luma/us/en.html){target="blank"} dans un onglet de navigateur distinct et mettez-le en signet afin que vous puissiez facilement le charger si nécessaire pendant le tutoriel. Vous n’avez pas besoin d’un accès supplémentaire à Luma, hormis la possibilité de charger notre site de production hébergé.

[![Site web Luma](assets/old-overview-luma.png)](https://luma.enablementadobe.com/content/luma/us/en.html){target="blank"}

C’est parti !

[Suivant : ](configure-schemas.md)

>[!NOTE]
>
>Merci d’avoir consacré du temps à l’apprentissage du SDK Web Adobe Experience Platform. Si vous avez des questions, souhaitez partager des commentaires généraux ou avez des suggestions sur le contenu à venir, partagez-les sur cet [post de discussion de la communauté Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996?profile.language=fr)
