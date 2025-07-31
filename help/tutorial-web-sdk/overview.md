---
title: Tutoriel sur lʼimplémentation dʼAdobe Experience Cloud à lʼaide du SDK web
description: Découvrez comment implémenter des applications Experience Cloud à l’aide du SDK web d’Adobe Experience Platform.
recommendations: catalog, noDisplay
exl-id: cf0ff74b-e81e-4f6d-ab7d-6c70e9b52d78
source-git-commit: 7ccbaaf4db43921f07c971c485e1460a1a7f0334
workflow-type: tm+mt
source-wordcount: '716'
ht-degree: 8%

---

# Tutoriel sur lʼimplémentation dʼAdobe Experience Cloud à lʼaide du SDK web

Découvrez comment implémenter des applications Experience Cloud à l’aide du SDK web d’Adobe Experience Platform.

Experience Platform Web SDK est une bibliothèque JavaScript côté client qui permet aux clients de Adobe Experience Cloud d’interagir avec les applications Adobe et les services tiers via Adobe Experience Platform Edge Network. Voir [Présentation de Adobe Experience Platform Web SDK](https://experienceleague.adobe.com/fr/docs/experience-platform/edge/home) pour plus d’informations.

![Architecture Experience Platform Web SDK](assets/dc-websdk.png)

Ce tutoriel vous guide tout au long de l’implémentation de Platform Web SDK sur un exemple de site web de vente au détail appelé Luma. Le site [Luma](https://luma.enablementadobe.com/content/luma/us/en.html) dispose d’une couche de données et de fonctionnalités riches qui vous permettent de créer une implémentation réaliste. Pour ce tutoriel, vous :

* Créez votre propre propriété de balises, dans votre propre compte, avec une implémentation de SDK web Platform pour le site web Luma.
* Configurez toutes les fonctionnalités de collecte de données pour les implémentations de Web SDK telles que les flux de données, les schémas et les espaces de noms d’identité.
* Ajoutez les applications Adobe Experience Cloud suivantes :
   * **[Adobe Experience Platform](setup-experience-platform.md)** (et les applications reposant sur Platform telles qu’Adobe Real-Time Customer Data Platform, Adobe Journey Optimizer et Adobe Customer Journey Analytics)
   * **[Adobe Analytics](setup-analytics.md)**
   * **[Adobe Audience Manager](setup-audience-manager.md)**
   * **[Adobe Target](setup-target.md)**
* Implémentez le transfert d’événement pour envoyer les données collectées par Web SDK vers des destinations autres qu’Adobe.
* Validez votre propre mise en œuvre de Platform Web SDK à l’aide d’Experience Platform Debugger et d’Assurance.

Après avoir suivi ce tutoriel, vous devriez être prêt à commencer à implémenter toutes vos applications marketing par le biais de Platform Web SDK sur votre propre site web !


>[!NOTE]
>
>Un tutoriel multi-solution similaire est disponible pour [Mobile SDK](../tutorial-mobile-sdk/overview.md).

## Conditions préalables

Tous les clients Experience Cloud peuvent utiliser Platform Web SDK. Il n’est pas nécessaire d’obtenir la licence d’une application basée sur Platform telle que Real-Time Customer Data Platform ou Journey Optimizer pour utiliser Web SDK.

Dans ces leçons, nous supposons que vous disposez d’un compte Adobe et des autorisations requises pour suivre les leçons. Si ce n’est pas le cas, vous devez contacter un administrateur Experience Cloud de votre société pour obtenir l’accès.

* Pour **Collecte de données**, vous devez disposer des éléments suivants :
   * **[!UICONTROL Plateformes]** : autorisation pour **[!UICONTROL Web]** et, si une licence est disponible, **[!UICONTROL Edge]**
   * **[!UICONTROL Droits de propriété]**—autorisation d’**[!UICONTROL approuver]**, **[!UICONTROL développer]**, **[!UICONTROL modifier la propriété]**, **[!UICONTROL gérer les environnements]**, **[!UICONTROL gérer les extensions]** et **[!UICONTROL publier]**,
   * **[!UICONTROL Droits d’entreprise]**—autorisation de **[!UICONTROL Gérer les propriétés]**

     Pour plus d’informations sur les autorisations des balises, consultez [la documentation](https://experienceleague.adobe.com/fr/docs/experience-platform/tags/admin/user-permissions).

* Pour **Experience Platform**, vous devez disposer des éléments suivants :

   * Accès au sandbox **production par défaut** **« Prod »**.
   * Accès à **[!UICONTROL Gérer les schémas]** et **[!UICONTROL Afficher les schémas]** sous **[!UICONTROL Modélisation des données]**.
   * Accès à **[!UICONTROL Gérer les espaces de noms d’identité]** et **[!UICONTROL Afficher les espaces de noms d’identité]** sous **[!UICONTROL Identity Management]**.
   * Accès à **[!UICONTROL Gérer les flux de données]** et **[!UICONTROL Afficher les flux de données]** sous **[!UICONTROL Collecte de données]**.
   * Si vous êtes client d’une application basée sur Platform et que vous allez suivre la leçon [Configuration d’Experience Platform](setup-experience-platform.md), vous devriez également disposer des éléments suivants :
      * Accès à un sandbox **de développement**.
      * Tous les éléments d’autorisation sous **[!UICONTROL Gestion des données]** et **[!UICONTROL Gestion des profils]** :

     Les fonctionnalités requises doivent être disponibles pour tous les clients Experience Cloud, même si vous n’êtes pas client d’une application basée sur Platform comme Real-Time CDP.

     Pour plus d’informations sur le contrôle d’accès de Platform, consultez [la documentation](https://experienceleague.adobe.com/fr/docs/experience-platform/access-control/home).

* Pour la leçon facultative **Adobe Analytics**, vous devez disposer d’un accès administrateur [aux paramètres de la suite de rapports, aux règles de traitement et à Analysis Workspace](https://experienceleague.adobe.com/fr/docs/analytics/admin/admin-console/home)

* Pour la leçon facultative **Adobe Target**, vous devez disposer d’un accès [ Éditeur ou Approbateur](https://experienceleague.adobe.com/fr/docs/target/using/administer/manage-users/enterprise/properties-overview#section_8C425E43E5DD4111BBFC734A2B7ABC80).

* Pour la leçon facultative **Audience Manager**, vous devez avoir accès à la création, à la lecture et à l’écriture de caractéristiques, de segments et de destinations. Pour plus d’informations, consultez le tutoriel sur le contrôle d’accès en fonction du rôle [Audience Manager](https://experienceleague.adobe.com/fr/docs/audience-manager-learn/tutorials/setup-and-admin/user-management/setting-permissions-with-role-based-access-control).


>[!NOTE]
>
>Nous partons du principe que vous connaissez les langages de développement front-end tels qu’HTML et JavaScript. Vous n’avez pas besoin d’être un expert de ces langages, mais vous obtiendrez davantage de ce tutoriel si vous pouvez lire et comprendre le code.

## Mises à jour

* 24 avril 2024 : mises à jour majeures, y compris l’ajout de Définir la variable/Mettre à jour la variable, le partage des demandes de personnalisation et d’analyse, leçons sur Journey Optimizer

## Chargement du site web Luma

Chargez le site web [Luma](https://luma.enablementadobe.com/content/luma/us/en.html){target="blank"} dans un onglet de navigateur distinct et ajoutez-y un signet afin de pouvoir le charger facilement si nécessaire pendant le tutoriel. Vous n’avez pas besoin d’un accès supplémentaire à Luma, hormis la possibilité de charger notre site de production hébergé.

[![Site web de Luma](assets/old-overview-luma.png)](https://luma.enablementadobe.com/content/luma/us/en.html){target="blank"}

C’est parti !

>[!NOTE]
>
>Merci d’avoir investi votre temps dans votre apprentissage de Adobe Experience Platform Web SDK. Si vous avez des questions, souhaitez partager des commentaires généraux ou avez des suggestions sur le contenu futur, veuillez les partager dans ce [article de discussion de la communauté Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996?profile.language=fr)
