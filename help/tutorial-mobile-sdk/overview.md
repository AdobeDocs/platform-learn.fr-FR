---
title: Présentation du tutoriel Mise en oeuvre de Adobe Experience Cloud dans les applications mobiles
description: Découvrez comment mettre en oeuvre les applications mobiles Adobe Experience Cloud. Ce tutoriel vous guide tout au long d’une mise en oeuvre d’applications Experience Cloud dans un exemple d’application Swift.
recommendations: noDisplay,catalog
last-substantial-update: 2023-11-29T00:00:00Z
exl-id: daff4214-d515-4fad-a224-f7589b685b55
source-git-commit: 0d5914ee0e63719c0439f02a5aa2a1e1c1d11a2f
workflow-type: tm+mt
source-wordcount: '826'
ht-degree: 3%

---

# Tutoriel sur la mise en oeuvre de Adobe Experience Cloud dans les applications mobiles

Découvrez comment implémenter des applications Adobe Experience Cloud dans votre application mobile à l’aide du SDK Adobe Experience Platform mobile.

Le SDK Mobile Experience Platform est un SDK côté client qui permet aux clients de Adobe Experience Cloud d’interagir avec les applications Adobe et les services tiers via l’Edge Network Adobe Experience Platform. Pour plus d’informations, consultez la [documentation du SDK Mobile Adobe Experience Platform](https://developer.adobe.com/client-sdks/home/) .

![Architecture](assets/architecture.png)


Ce tutoriel vous guide tout au long de la mise en oeuvre du SDK Mobile Platform dans un exemple d’application de vente au détail appelée Luma. L’ [application Luma](https://github.com/Adobe-Marketing-Cloud/Luma-iOS-Mobile-App) dispose d’une fonctionnalité qui vous permet de créer une mise en oeuvre réaliste. Après avoir terminé ce tutoriel, vous devriez être prêt à commencer à mettre en oeuvre toutes vos solutions marketing par le biais du SDK Mobile Experience Platform dans vos propres applications mobiles.

Les leçons sont conçues pour iOS et écrites dans Swift/SwiftUI, mais de nombreux concepts s’appliquent également à Android™.

Après avoir terminé ce tutoriel, vous serez en mesure de :

* Créez un schéma à l’aide de groupes de champs standard et personnalisés.
* Configurez un flux de données.
* Configurez une propriété de balise mobile.
* Configurez un jeu de données Experience Platform (facultatif).
* Installez et implémentez des extensions de balise dans une application.
* Transmettez correctement les paramètres Experience Cloud à une [vue web](web-views.md).
* Validez la mise en oeuvre à l’aide de [Adobe Experience Platform Assurance](assurance.md).
* Ajoutez les applications/extensions Adobe Experience Cloud suivantes :
   * [Adobe Experience Platform Edge (XDM)](events.md)
   * [Collecte de données du cycle de vie](lifecycle-data.md)
   * [Consentement](consent.md)
   * [Identité](identity.md)
   * [Profile](profile.md)
   * [Places](places.md)
   * [Analytics](analytics.md)
   * [Experience Platform](platform.md)
   * [Messagerie push avec Journey Optimizer](journey-optimizer-push.md)
   * [Messagerie in-app avec Journey Optimizer](journey-optimizer-inapp.md)
   * [Gestion des décisions avec Journey Optimizer](journey-optimizer-offers.md)
   * [Target](target.md)


>[!NOTE]
>
>Un tutoriel multisolution similaire est disponible pour le [SDK Web](../tutorial-web-sdk/overview.md).

## Conditions préalables

Dans ces leçons, on suppose que vous disposez d’un identifiant d’Adobe et des autorisations requises au niveau de l’utilisateur pour terminer les exercices. Dans le cas contraire, contactez votre administrateur d’Adobe pour demander l’accès.

* Dans la collecte de données, vous devez disposer des éléments suivants :
   * **[!UICONTROL Plateformes]**—élément d’autorisation **[!UICONTROL Mobile]**
   * **[!UICONTROL Droits de propriété]** : éléments d’autorisation vers **[!UICONTROL Develop]**, **[!UICONTROL Approve]**, **[!UICONTROL Publish]**, **[!UICONTROL Manage Extensions]** et **[!UICONTROL Manage Environments]** (Gérer les environnements).
   * **[!UICONTROL Droits d’entreprise]** : éléments d’autorisation pour **[!UICONTROL Gérer les propriétés]** et, si vous suivez la leçon facultative sur la messagerie push, **[!UICONTROL Gérer les configurations d’application]**

     Pour plus d’informations sur les autorisations de balises, voir [Autorisations utilisateur pour les balises](https://experienceleague.adobe.com/docs/experience-platform/tags/admin/user-permissions.html?lang=fr){target="_blank"} dans la documentation du produit.
* En Experience Platform, vous devez disposer des éléments suivants :
   * **[!UICONTROL Modélisation des données]** : éléments d’autorisation pour gérer et afficher les schémas.
   * **[!UICONTROL Identity Management]** : éléments d’autorisation pour gérer et afficher les espaces de noms d’identité.
   * **[!UICONTROL Collecte de données]** : éléments d’autorisation pour gérer et afficher les flux de données.

   * Si vous êtes le client d’une application basée sur Platform comme Real-Time CDP, Journey Optimizer ou Customer Journey Analytics, et que vous suivez les leçons connexes, vous devez également disposer des éléments suivants :
      * **[!UICONTROL Data Management]** : éléments d’autorisation pour gérer et afficher les jeux de données.
      * Un **sandbox** de développement que vous pouvez utiliser pour ce tutoriel.

   * Pour les leçons Journey Optimizer, vous avez besoin d’autorisations pour configurer le **service de notification push** et pour créer une **surface d’application**, un **parcours**, un **message** et des **paramètres prédéfinis de message**. Pour la gestion de la décision, vous avez besoin des autorisations appropriées pour **gérer les offres** et **décisions** comme décrit [ici](https://experienceleague.adobe.com/docs/journey-optimizer/using/access-control/privacy/high-low-permissions.html?lang=en#decisions-permissions).

* Pour Adobe Analytics, vous devez connaître les **suites de rapports** que vous pouvez utiliser pour terminer ce tutoriel.

* Pour Adobe Target, vous devez disposer des autorisations nécessaires pour créer et activer des activités.


>[!NOTE]
>
>Dans le cadre de ce tutoriel, vous créez des schémas, des jeux de données, des identités, etc. Si plusieurs personnes suivent ce tutoriel dans un seul environnement de test, envisagez d’ajouter ou de préparer une identification dans le cadre de vos conventions d’appellation lors de la création de ces objets. Par exemple, ajoutez ` - <your name or initials>` au nom de l’objet que vous êtes invité à créer.

## Historique des versions

* 29 novembre 2023 : révision majeure avec un nouvel exemple d’application et nouvelles leçons pour la messagerie in-app, la gestion des décisions et Adobe Target.
* 9 mars 2022 : première publication

## Téléchargement de l’application Luma

Deux versions de l’exemple d’application sont disponibles en téléchargement. Les deux versions peuvent être téléchargées/clonées à partir de [Github](https://github.com/Adobe-Marketing-Cloud/Luma-iOS-Mobile-App). Vous trouverez deux dossiers :


1. [Démarrer](https://github.com/Adobe-Marketing-Cloud/Luma-iOS-Mobile-App){target="_blank"} : un projet sans code ou avec un code d’emplacement pour la plupart du code du SDK Mobile Experience Platform que vous devez utiliser pour terminer les exercices pratiques de ce tutoriel.
1. [Finish](https://github.com/Adobe-Marketing-Cloud/Luma-iOS-Mobile-App){target="_blank"} : version avec mise en oeuvre complète à titre de référence.

>[!NOTE]
>
>Vous utilisez iOS comme plateforme, [!DNL Swift] comme langage de programmation, [!DNL SwiftUI] comme structure d’interface utilisateur et [!DNL Xcode] comme environnement de développement intégré (IDE). Cependant, la plupart des concepts de mise en oeuvre expliqués sont similaires pour d’autres plateformes de développement. Nombre d’entre eux ont déjà terminé ce tutoriel avec une expérience iOS/Swift (interface utilisateur) qui n’avait que peu ou pas d’expérience auparavant. Vous n’avez pas besoin d’être un expert pour terminer les leçons, mais vous en retirez davantage si vous pouvez facilement lire et comprendre le code.


Vous pouvez télécharger la version finale productisée de l’application à partir d’App Store.

[![Télécharger](assets/download-app.svg)](https://apps.apple.com/us/app/luma-app/id6466588487)


C’est parti !

>[!SUCCESS]
>
>Merci d’investir votre temps à apprendre sur le SDK Adobe Experience Platform Mobile. Si vous avez des questions, souhaitez partager des commentaires généraux ou avez des suggestions sur le contenu à venir, partagez-les sur cet [post de discussion de la communauté Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796).

Suivant : **[Création d’un schéma XDM](create-schema.md)**
