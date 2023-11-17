---
title: Présentation du tutoriel Mise en oeuvre de Adobe Experience Cloud dans les applications mobiles
description: Découvrez comment mettre en oeuvre les applications mobiles Adobe Experience Cloud. Ce tutoriel vous guide tout au long d’une mise en oeuvre d’applications Experience Cloud dans un exemple d’application Swift.
recommendations: noDisplay,catalog
hide: true
exl-id: 378bdf5d-c3ce-4a4c-b188-ab9e8265627f
source-git-commit: bc53cb5926f708408a42aa98a1d364c5125cb36d
workflow-type: tm+mt
source-wordcount: '821'
ht-degree: 6%

---

# Tutoriel sur l’implémentation d’Adobe Experience Cloud dans les applications mobiles

Découvrez comment implémenter des applications Adobe Experience Cloud dans votre application mobile à l’aide du SDK Adobe Experience Platform mobile.

Le SDK Mobile Experience Platform est un SDK côté client qui permet aux clients de Adobe Experience Cloud d’interagir avec les applications Adobe et les services tiers par le biais du réseau Adobe Experience Platform Edge. Voir [Documentation du SDK Mobile Adobe Experience Platform](https://developer.adobe.com/client-sdks/home/) pour plus d’informations.

![Architecture](assets/architecture.png)


Ce tutoriel vous guide tout au long de la mise en oeuvre du SDK Mobile Platform dans un exemple d’application de vente au détail appelée Luma. La variable [Application Luma](https://github.com/Adobe-Marketing-Cloud/Luma-iOS-Mobile-App) dispose d’une fonctionnalité qui vous permet de créer une mise en oeuvre réaliste. Après avoir terminé ce tutoriel, vous devriez être prêt à commencer à mettre en oeuvre toutes vos solutions marketing par le biais du SDK Mobile Experience Platform dans vos propres applications mobiles.

Les leçons sont conçues pour iOS et écrites dans Swift/SwiftUI, mais de nombreux concepts s’appliquent également à Android™.

Après avoir terminé ce tutoriel, vous serez en mesure de :

* Créez un schéma à l’aide de groupes de champs standard et personnalisés.
* Configurer un flux de données.
* Configurez une propriété de balise mobile.
* Configurez un jeu de données Experience Platform (facultatif).
* Installez et implémentez des extensions de balise dans une application.
* Transmettez correctement les paramètres Experience Cloud à un [webview](web-views.md).
* Validation de la mise en oeuvre à l’aide de [Adobe Experience Platform Assurance](assurance.md).
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
>Un tutoriel multisolution similaire est disponible pour [SDK Web](../tutorial-web-sdk/overview.md).

## Conditions préalables

Dans ces leçons, on suppose que vous disposez d’un identifiant d’Adobe et des autorisations requises au niveau de l’utilisateur pour terminer les exercices. Dans le cas contraire, contactez votre administrateur d’Adobe pour demander l’accès.

* Dans la collecte de données, vous devez disposer des éléments suivants :
   * **[!UICONTROL Plateformes]**—élément d’autorisation **[!UICONTROL Mobile]**
   * **[!UICONTROL Droits de propriété]**: éléments d’autorisation pour **[!UICONTROL Développer]**, **[!UICONTROL Approuver]**, **[!UICONTROL Publier]**, **[!UICONTROL Gestion des extensions]**, et **[!UICONTROL Gestion des environnements]**.
   * **[!UICONTROL Droits d’entreprise]**: éléments d’autorisation pour **[!UICONTROL Gestion des propriétés]** et, si vous suivez la leçon facultative sur la messagerie push, **[!UICONTROL Gestion des configurations d’application]**

     Pour plus d’informations sur les autorisations de balise, voir [Autorisations utilisateur pour les balises](https://experienceleague.adobe.com/docs/experience-platform/tags/admin/user-permissions.html?lang=fr){target="_blank"} dans la documentation du produit.
* En Experience Platform, vous devez disposer des éléments suivants :
   * **[!UICONTROL Modélisation des données]**: éléments d’autorisation pour gérer et afficher les schémas.
   * **[!UICONTROL Identity Management]**: éléments d’autorisation pour gérer et afficher les espaces de noms d’identité.
   * **[!UICONTROL Collecte de données]**: éléments d’autorisation pour gérer et afficher les flux de données.

   * Si vous êtes le client d’une application basée sur Platform comme Real-Time CDP, Journey Optimizer ou Customer Journey Analytics, et que vous suivez les leçons connexes, vous devez également disposer des éléments suivants :
      * **[!UICONTROL Data Management]**: éléments d’autorisation pour gérer et afficher les jeux de données.
      * Un développement **sandbox** à utiliser pour ce tutoriel.

   * Pour les leçons Journey Optimizer, vous avez besoin d’autorisations pour configurer la variable **service de notification push** et pour créer un **surface de l’application**, un **parcours**, un **message**, et **paramètres prédéfinis de message**. Pour la gestion de la décision, vous avez besoin des autorisations appropriées pour **gérer les offres** et **décisions** comme décrit [here](https://experienceleague.adobe.com/docs/journey-optimizer/using/access-control/privacy/high-low-permissions.html?lang=en#decisions-permissions).

* Pour Adobe Analytics, vous devez savoir lequel **suites de rapports** vous pouvez utiliser pour terminer ce tutoriel.

* Pour Adobe Target, vous devez disposer des autorisations nécessaires pour créer et activer des activités.


>[!NOTE]
>
>Dans le cadre de ce tutoriel, vous créez des schémas, des jeux de données, des identités, etc. Si plusieurs personnes suivent ce tutoriel dans un seul environnement de test, envisagez d’ajouter ou de préparer une identification dans le cadre de vos conventions d’appellation lors de la création de ces objets. Par exemple, ajoutez ` - <your name or initials>` au nom de l’objet que vous êtes invité à créer.


## Téléchargement de l’application Luma

Deux versions de l’exemple d’application sont disponibles en téléchargement. Les deux versions peuvent être téléchargées/clonées depuis [Github](https://github.com/Adobe-Marketing-Cloud/Luma-iOS-Mobile-App). Vous trouverez deux dossiers :


1. [Début](https://github.com/Adobe-Marketing-Cloud/Luma-iOS-Mobile-App){target="_blank"}: un projet sans code ou avec un code d’emplacement pour la plupart du code du SDK Mobile Experience Platform que vous devez utiliser pour terminer les exercices pratiques de ce tutoriel.
1. [Terminer](https://github.com/Adobe-Marketing-Cloud/Luma-iOS-Mobile-App){target="_blank"}: version avec mise en oeuvre complète à titre de référence.


>[!NOTE]
>
>Vous utilisez iOS comme plateforme, [!DNL Swift] comme langage de programmation, [!DNL SwiftUI] comme structure de l’interface utilisateur et [!DNL Xcode] comme environnement de développement intégré (IDE). Cependant, la plupart des concepts de mise en oeuvre expliqués sont similaires pour d’autres plateformes de développement. Nombre d’entre eux ont déjà terminé ce tutoriel avec une expérience iOS/Swift (interface utilisateur) qui n’avait que peu ou pas d’expérience auparavant. Vous n’avez pas besoin d’être un expert pour terminer les leçons, mais vous en retirez davantage si vous pouvez facilement lire et comprendre le code.


C’est parti !

>[!SUCCESS]
>
>Merci d’investir votre temps à apprendre sur le SDK Adobe Experience Platform Mobile. Si vous avez des questions, souhaitez partager des commentaires généraux ou avez des suggestions sur le contenu futur, partagez-les à ce sujet. [Article de discussion de la communauté Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796).

Suivant : **[Créer un schéma XDM](create-schema.md)**
