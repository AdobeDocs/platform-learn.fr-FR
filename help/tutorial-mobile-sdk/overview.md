---
title: Tutoriel sur l’implémentation de Adobe Experience Cloud dans les applications mobiles
description: Découvrez comment implémenter les applications mobiles Adobe Experience Cloud. Ce tutoriel vous guide tout au long de l'implémentation des applications Experience Cloud dans un exemple d'application Swift ou Android.
recommendations: noDisplay,catalog
last-substantial-update: 2023-11-29T00:00:00Z
exl-id: daff4214-d515-4fad-a224-f7589b685b55
source-git-commit: 342bb7efbe868622c4bc08e02568bce948fed61c
workflow-type: tm+mt
source-wordcount: '1019'
ht-degree: 1%

---

# Tutoriel sur l’implémentation de Adobe Experience Cloud dans les applications mobiles

Découvrez comment implémenter des applications Adobe Experience Cloud dans votre application mobile à l’aide de Adobe Experience Platform Mobile SDK.

Experience Platform Mobile SDK est un SDK côté client qui permet aux clients de Adobe Experience Cloud d’interagir avec les applications Adobe et les services tiers via Adobe Experience Platform Edge Network. Consultez la [documentation Adobe Experience Platform Mobile SDK](https://developer.adobe.com/client-sdks/home/) pour plus d’informations.

![Architecture](assets/architecture.png){zoomable="yes"}


Ce tutoriel vous guide tout au long de l’implémentation de Platform Mobile SDK dans un exemple d’application appelé Luma. L’application Luma dispose d’une fonctionnalité qui vous permet de créer une implémentation réaliste. Une fois que vous avez terminé ce tutoriel, vous devriez être prêt à commencer à mettre en œuvre toutes vos solutions marketing via Experience Platform Mobile SDK dans vos propres applications mobiles.

Les leçons sont conçues pour :

* iOS, en utilisant le langage de programmation Swift et le framework SwiftUI.
* Android, en utilisant le langage de programmation Kotlin et Java et le framework JetPack Compose.

Après avoir terminé ce tutoriel, vous serez en mesure de :

* Créez un schéma à l’aide de groupes de champs standard et personnalisés.
* Configurez un flux de données.
* Configurez une propriété de balise mobile.
* Configurez un jeu de données Experience Platform (facultatif).
* Installer et implémenter des extensions de balises dans une application.
* Transmettez correctement les paramètres Experience Cloud à un [webview](web-views.md).
* Validez la mise en œuvre à l’aide de [Adobe Experience Platform Assurance](assurance.md).
* Ajoutez les applications ou extensions Adobe Experience Cloud suivantes :
   * [Adobe Experience Platform Edge (XDM)](events.md)
   * [Collecte de données relatives au cycle de vie](lifecycle-data.md)
   * [Consentement](consent.md)
   * [Identité](identity.md)
   * [Profile](profile.md)
   * [Places](places.md)
   * [Analytics](analytics.md)
   * [Experience Platform](platform.md)
   * [Messagerie push avec Journey Optimizer](journey-optimizer-push.md)
   * [Messagerie in-app avec Journey Optimizer](journey-optimizer-inapp.md)
   * [Gestion des décisions avec Journey Optimizer](journey-optimizer-offers.md)
   * [Cible](target.md)


>[!NOTE]
>
>Un tutoriel multi-solution similaire est disponible pour [Web SDK](../tutorial-web-sdk/overview.md).

## Autorisations

Dans ces leçons, nous supposons que vous disposez d’un Adobe Id et des autorisations requises au niveau de l’utilisateur pour effectuer les exercices. Dans le cas contraire, contactez votre administrateur Adobe pour demander l’accès.

* Dans la collecte de données, vous devez disposer des éléments suivants :
   * **[!UICONTROL Plateformes]**—élément d&#39;autorisation **[!UICONTROL Mobile]**
   * **[!UICONTROL Droits de propriété]** : éléments d’autorisation pour **[!UICONTROL Développer]**, **[!UICONTROL Approuver]**, **[!UICONTROL Publier]**, **[!UICONTROL Gérer les extensions]** et **[!UICONTROL Gérer les environnements]**.
   * **[!UICONTROL Droits d’entreprise]**—éléments d’autorisation pour **[!UICONTROL Gérer les propriétés]**

     Pour plus d’informations sur les autorisations des balises, voir [ Autorisations d’utilisateur pour les balises ](https://experienceleague.adobe.com/en/docs/experience-platform/tags/admin/user-permissions){target="_blank"} dans la documentation du produit.
* Dans Experience Platform, vous devez disposer des éléments suivants :
   * **[!UICONTROL Modélisation des données]** : éléments d&#39;autorisation pour gérer et afficher les schémas.
   * **[!UICONTROL Identity Management]**—éléments d&#39;autorisation pour gérer et afficher les espaces de noms d&#39;identité.
   * **[!UICONTROL Collecte de données]** : éléments d’autorisation pour gérer et afficher les flux de données.

   * Si vous êtes client d’une application basée sur Platform telle que Real-Time CDP, Journey Optimizer ou Customer Journey Analytics, et prévoyez d’effectuer les leçons associées, vous devriez également :
      * **[!UICONTROL Gestion des données]** : éléments d’autorisation pour gérer et afficher les jeux de données.
      * Un **de développement** que vous pouvez utiliser pour ce tutoriel.

   * Pour les leçons Journey Optimizer, vous avez besoin d’autorisations pour configurer le **service de notification push** et pour créer une **surface d’application**, un **parcours**, un **message** et des **préréglages de message**. En outre, pour la gestion des décisions, vous avez besoin des autorisations appropriées pour **gérer les offres** et **les décisions**, comme décrit dans la section [Niveaux d’autorisation](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/access-control/high-low-permissions).

* Pour Adobe Analytics, vous devez savoir quelles **suites de rapports** vous pouvez utiliser pour suivre ce tutoriel.

* Pour Adobe Target, vous devez disposer des autorisations nécessaires pour créer et activer des activités.


>[!NOTE]
>
>Dans le cadre de ce tutoriel, vous allez créer des schémas, des jeux de données, des identités, etc. Si plusieurs personnes suivent ce tutoriel dans un seul sandbox, pensez à ajouter ou à ajouter une identification comme partie intégrante de vos conventions de nommage lors de la création de ces objets. Par exemple, ajoutez ` - <your name or initials>` au nom de l’objet que vous êtes invité à créer.

## Historique des versions

* 9 septembre 2025 :
   * Version Android de l’application avec instructions associées.
   * Mises à jour pour les modifications apportées à la surface d’application et aux fonctionnalités de campagne dans Journey Optimizer.
* 29 novembre 2023 : refonte majeure avec un nouvel exemple d’application et de nouvelles leçons pour la messagerie in-app, la gestion des décisions et Adobe Target.
* 9 mars 2022 : première publication

## Télécharger l’application Luma

>[!BEGINTABS]

>[!TAB iOS]

Deux versions de l’exemple d’application peuvent être téléchargées. Les deux versions peuvent être téléchargées/clonées à partir de [GitHub](https://github.com/Adobe-Marketing-Cloud/Luma-iOS-Mobile-App). Vous trouvez deux dossiers :

1. [Démarrer](https://github.com/Adobe-Marketing-Cloud/Luma-iOS-Mobile-App){target="_blank"} : projet sans code ou avec un code d’espace réservé pour la plupart du code Experience Platform Mobile SDK que vous devez utiliser pour effectuer les exercices pratiques de ce tutoriel.
1. [Terminer](https://github.com/Adobe-Marketing-Cloud/Luma-iOS-Mobile-App){target="_blank"} : une version avec l’implémentation complète à titre de référence.

Vous utilisez iOS comme plateforme, [!DNL Swift] comme langage de programmation, [!DNL SwiftUI] comme framework d’interface utilisateur et [!DNL Xcode] comme environnement de développement intégré (IDE). Cependant, de nombreux concepts de mise en œuvre expliqués sont similaires pour d’autres plateformes de développement. De nombreuses personnes ont déjà suivi avec succès ce tutoriel avec peu ou pas d’expérience de développement antérieure d’iOS et de Swift (interface utilisateur). Vous n’avez pas besoin d’être un expert pour suivre les leçons, mais vous tirez davantage parti de ces leçons si vous pouvez lire et comprendre facilement le code.

Vous pouvez télécharger la version productive finale de l’application à partir d’App Store.

[![Télécharger](assets/download-app.svg)](https://apps.apple.com/us/app/luma-app/id6466588487)

>[!TAB Android]

Deux versions de l’exemple d’application peuvent être téléchargées. Les deux versions peuvent être téléchargées ou clonées à partir de [GitHub](https://github.com/adobe/Luma-Android). Vous trouvez deux dossiers :

1. [Démarrer](https://github.com/adobe/Luma-Android){target="_blank"} : projet sans code ou avec un code d’espace réservé pour la plupart du code Experience Platform Mobile SDK que vous devez utiliser pour effectuer les exercices pratiques de ce tutoriel.
1. [Terminer](https://github.com/adobe/Luma-Android){target="_blank"} : une version avec l’implémentation complète à titre de référence.

Vous utilisez Android comme plateforme, [!DNL Kotlin]+[!DNL Java] comme langage de programmation, [!DNL JetPack Compose] comme framework d’interface utilisateur et [!DNL Android Studio] comme environnement de développement intégré (IDE). Cependant, de nombreux concepts de mise en œuvre expliqués sont similaires pour d’autres plateformes de développement. Beaucoup ont déjà terminé ce tutoriel avec succès avec peu ou pas d’expérience préalable dans Android / Kotlin+Java / JetPack Compose. Vous n’avez pas besoin d’être un expert pour suivre les leçons, mais vous tirez davantage parti de ces leçons si vous pouvez lire et comprendre facilement le code.

Si vous préférez, vous pouvez [joindre un test pour une version personnalisée](https://play.google.com/apps/internaltest/4700642199234438150) de l’application à partir de Google Play.


>[!ENDTABS]

C’est parti !

>[!SUCCESS]
>
>Merci d’avoir consacré votre temps à découvrir Adobe Experience Platform Mobile SDK. Si vous avez des questions, souhaitez partager des commentaires généraux ou des suggestions sur le contenu futur, partagez-les dans ce [article de discussion de la communauté Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796).

Suivant : **[Création d’un schéma XDM](create-schema.md)**
