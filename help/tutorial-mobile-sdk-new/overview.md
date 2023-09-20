---
title: Présentation du tutoriel Mise en oeuvre de Adobe Experience Cloud dans les applications mobiles
description: Découvrez comment mettre en oeuvre les applications mobiles Adobe Experience Cloud. Ce tutoriel vous guide tout au long d’une mise en oeuvre d’applications Experience Cloud dans un exemple d’application Swift.
recommendations: noDisplay,catalog
hide: true
source-git-commit: a2788110b1c43d24022672bb5ba0f36af66d962b
workflow-type: tm+mt
source-wordcount: '873'
ht-degree: 9%

---

# Tutoriel sur l’implémentation d’Adobe Experience Cloud dans les applications mobiles

Découvrez comment implémenter des applications Adobe Experience Cloud dans votre application mobile à l’aide du SDK Adobe Experience Platform mobile.

Le SDK Mobile Experience Platform est un SDK côté client qui permet aux clients de Adobe Experience Cloud d’interagir avec les applications Adobe et les services tiers par le biais du réseau Adobe Experience Platform Edge. Voir [Documentation du SDK Mobile Adobe Experience Platform](https://developer.adobe.com/client-sdks/documentation/) pour plus d’informations.

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
   * [Adobe Experience Platform](platform.md)
   * [Messagerie push avec Journey Optimizer](journey-optimizer-push.md)
   * [Messagerie in-app avec Journey Optimizer](journey-optimizer-inapp.md)
   * [Offres avec Journey Optimizer](journey-optimizer-offers.md)
   * [Tests A/B avec Target](target.md)


>[!NOTE]
>
>Un tutoriel multisolution similaire est disponible pour [SDK Web](../tutorial-web-sdk/overview.md).

## Conditions préalables

Dans ces leçons, nous supposons que vous disposez d’un Adobe ID et des autorisations requises pour effectuer les exercices. Dans le cas contraire, contactez votre administrateur d’Adobe pour demander l’accès.

* Dans la collecte de données, vous devez disposer des éléments suivants :
   * **[!UICONTROL Plateformes]**—élément d’autorisation **[!UICONTROL Mobile]**
   * **[!UICONTROL Droits de propriété]**: éléments d’autorisation pour **[!UICONTROL Développer]**, **[!UICONTROL Approuver]**, **[!UICONTROL Publier]**, **[!UICONTROL Gestion des extensions]**, et **[!UICONTROL Gestion des environnements]**.
   * **[!UICONTROL Droits d’entreprise]**: éléments d’autorisation pour **[!UICONTROL Gestion des propriétés]** et, si vous suivez la leçon facultative sur la messagerie push, **[!UICONTROL Gestion des configurations d’application]**

     Pour plus d’informations sur les autorisations de balise, voir [Autorisations utilisateur pour les balises](https://experienceleague.adobe.com/docs/experience-platform/tags/admin/user-permissions.html?lang=fr){target="_blank"} dans la documentation du produit.
* En Experience Platform, vous devez disposer des éléments suivants :
   * **[!UICONTROL Modélisation des données]**: éléments d’autorisation pour gérer et afficher les schémas.
   * **[!UICONTROL Identity Management]**: éléments d’autorisation pour gérer et afficher les espaces de noms d’identité.
   * **[!UICONTROL Collecte de données]**: éléments d’autorisation pour gérer et afficher les flux de données.

   * Si vous êtes le client d’une application basée sur Platform telle que Real-Time CDP, Journey Optimizer ou Customer Journey Analytics, vous devez également disposer des éléments suivants :
      * **[!UICONTROL Data Management]**: éléments d’autorisation pour gérer et afficher les jeux de données pour terminer les _exercices Platform facultatifs_ (nécessite une licence pour une application basée sur Platform ).
      * Un développement **sandbox** à utiliser pour ce tutoriel.

* Pour Adobe Analytics, vous devez savoir lequel **suites de rapports** vous pouvez utiliser pour terminer ce tutoriel.

* Pour Adobe Target, vous devez disposer d’autorisations correctement configurées. **rôles**, **espaces de travail**, et **properties** comme décrit [here](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/enterprise/property-channel.html?lang=fr).

* Pour Adobe Journey Optimizer, vous devez disposer des autorisations suffisantes pour configurer la variable **service de notification push** et pour créer un **surface de l’application**, un **parcours**, un **message** et **paramètres prédéfinis de message**. Pour la gestion de la décision, vous avez besoin des autorisations appropriées pour **gérer les offres** et **décisions** comme décrit [here](https://experienceleague.adobe.com/docs/journey-optimizer/using/access-control/privacy/high-low-permissions.html?lang=en#decisions-permissions).

Tous les clients Experience Cloud doivent avoir accès aux fonctionnalités requises pour déployer le SDK Mobile.


>[!NOTE]
>
>Dans le cadre de ce tutoriel, vous allez créer des schémas, des jeux de données, des identités, etc. Si vous passez par ce tutoriel avec plusieurs personnes sur un seul environnement de test ou que vous utilisez un compte partagé, envisagez d’ajouter ou de préparer une identification dans le cadre de vos conventions de dénomination lors de la création de ces objets. Par exemple, ajoutez ` - <your name or initials>` au nom de l’objet que vous êtes invité à créer.


## Téléchargement de l’application Luma

Deux versions de l’exemple d’application sont disponibles en téléchargement. Les deux versions peuvent être téléchargées/clonées depuis [Github](https://git.corp.adobe.com/rmaur/Luma). Vous trouverez deux dossiers :


1. [Début](https://git.corp.adobe.com/rmaur/Luma){target="_blank"}: un projet sans code ou avec un code d’emplacement pour la plupart du code du SDK Mobile Experience Platform que vous devez utiliser pour terminer les exercices pratiques de ce tutoriel.
1. [Terminer](https://git.corp.adobe.com/Luma){target="_blank"}: version avec mise en oeuvre complète à titre de référence.

>[!NOTE]
>
>Vous utiliserez iOS comme plateforme, [!DNL Swift] comme langage de programmation, [!DNL SwiftUI] comme structure de l’interface utilisateur et [!DNL Xcode] comme environnement de développement intégré (IDE). Cependant, la plupart des concepts de mise en oeuvre expliqués sont similaires pour d’autres plateformes de développement. Nombre d’entre eux ont déjà terminé ce tutoriel avec une expérience iOS/Swift (interface utilisateur) qui n’avait pas encore été créée auparavant. Vous n’avez pas besoin d’être un expert pour terminer les leçons, mais vous en retirez davantage si vous pouvez facilement lire et comprendre le code.


C’est parti !

>[!SUCCESS]
>
>Merci d’investir votre temps à apprendre sur le SDK Adobe Experience Platform Mobile. Si vous avez des questions, souhaitez partager des commentaires généraux ou avez des suggestions sur le contenu futur, partagez-les à ce sujet. [Article de discussion de la communauté Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796).

Suivant : **[Créer un schéma XDM](create-schema.md)**
