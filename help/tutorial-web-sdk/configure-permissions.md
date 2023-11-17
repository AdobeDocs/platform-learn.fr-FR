---
title: Configuration des autorisations pour le tutoriel
description: Découvrez comment demander l’accès au SDK Web Experience Platform et configurer l’autorisation requise pour terminer le tutoriel Mise en oeuvre de Adobe Experience Cloud avec le SDK Web .
feature: Web SDK,Tags,Access Control
exl-id: d7c4f2c3-cf3c-4587-88f8-82113d250084
source-git-commit: 4a12f8261cf1fb071bc70b6a04c34f6c16bcce64
workflow-type: tm+mt
source-wordcount: '414'
ht-degree: 7%

---

# Configuration des autorisations pour le tutoriel

Découvrez comment demander l’accès au SDK Web Experience Platform et configurer l’autorisation requise pour suivre ce tutoriel. Pour mettre en oeuvre le SDK Web Platform à l’aide de balises dans l’interface de collecte de données, vous devez disposer des autorisations utilisateur appropriées configurées dans [Admin Console](https://adminconsole.adobe.com).

## Collecte de données

* Ont la permission de **[!UICONTROL Développer]**, **[!UICONTROL Modifier]**, **[!UICONTROL Approuver]**, **[!UICONTROL Publier]**, **[!UICONTROL Gestion des extensions]**, **[!UICONTROL Gestion des environnements]**, et **[!UICONTROL Gestion des propriétés]**. Pour plus d’informations sur les autorisations de balises, voir [la documentation](https://experienceleague.adobe.com/docs/experience-platform/tags/admin/user-permissions.html?lang=fr).
* Si vous suivez la leçon facultative sur le transfert d’événement, disposez d’une licence de produit qui inclut le transfert de périphérie et l’élément d’autorisation. **[!UICONTROL Plateformes]** > **[!UICONTROL Edge]**

## Experience Platform

Ces fonctionnalités doivent être disponibles pour tous les clients Experience Cloud, même si vous n’êtes pas client d’une application basée sur Platform comme Real-Time CDP.

* L’accès au **production par défaut**, **&quot;Prod&quot;** sandbox.
* Accès à **[!UICONTROL Gestion des schémas]** et **[!UICONTROL Affichage des schémas]** under **[!UICONTROL Modélisation des données]**
* Accès à **[!UICONTROL Gestion des espaces de noms d’identité]** et **[!UICONTROL Affichage des espaces de noms d’identité]** under **[!UICONTROL Identity Management]**
* Accès à **[!UICONTROL Gestion des flux de données]** et **[!UICONTROL Affichage des flux de données]** under **[!UICONTROL Collecte de données]**
* Si vous êtes client d’une application basée sur Platform et que vous allez exécuter la variable [Configuration d’un Experience Platform](setup-experience-platform.md) leçon, vous devez également disposer des éléments suivants :
   * Accès à un **development** sandbox.
   * Tous les éléments d’autorisation sous **[!UICONTROL Data Management]**, et **[!UICONTROL Gestion des profils]**:


Pour plus d’informations sur le contrôle d’accès à Platform, voir [la documentation](https://experienceleague.adobe.com/docs/experience-platform/access-control/home.html?lang=fr).

## Adobe Analytics

Pour la leçon facultative Adobe Analytics, vous devez disposer des [Accès de l’administrateur aux paramètres de la suite de rapports, aux règles de traitement et à Analysis Workspace](https://experienceleague.adobe.com/docs/analytics/admin/admin-console/home.html?lang=fr)

## Adobe Target

Pour la leçon facultative Adobe Target, vous devez disposer des [Éditeur ou approbateur](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/enterprise/properties-overview.html#section_8C425E43E5DD4111BBFC734A2B7ABC80) accès.

## Adobe Audience Manager

* Pour la leçon d’Audience Manager facultative, vous devez avoir accès à la création, à la lecture et à l’écriture de caractéristiques, de segments et de destinations. Pour plus d’informations, consultez le tutoriel sur [Contrôle d’accès en fonction du rôle de l’Audience Manager](https://experienceleague.adobe.com/docs/audience-manager-learn/tutorials/setup-and-admin/user-management/setting-permissions-with-role-based-access-control.html?lang=en).

Vous êtes maintenant prêt à démarrer les étapes de configuration initiales.

[Suivant : ](configure-schemas.md)

>[!NOTE]
>
>Merci d’avoir consacré du temps à l’apprentissage du SDK Web Adobe Experience Platform. Si vous avez des questions, souhaitez partager des commentaires généraux ou avez des suggestions sur le contenu futur, partagez-les à ce sujet. [Article de discussion de la communauté Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996)
