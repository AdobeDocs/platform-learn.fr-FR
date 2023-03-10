---
title: Présentation du tutoriel Mise en oeuvre de Adobe Experience Cloud dans les applications mobiles
description: Découvrez comment mettre en oeuvre les applications mobiles Adobe Experience Cloud. Ce tutoriel vous guide tout au long d’une mise en oeuvre d’applications Experience Cloud dans un exemple d’application Swift.
recommendation: noDisplay,catalog
exl-id: daff4214-d515-4fad-a224-f7589b685b55
source-git-commit: cf0193e3aae4d6536c868f078f4773ee14e90408
workflow-type: tm+mt
source-wordcount: '648'
ht-degree: 10%

---

# Tutoriel sur l’implémentation d’Adobe Experience Cloud dans les applications mobiles

Découvrez comment implémenter des applications Adobe Experience Cloud dans votre application mobile à l’aide du SDK Adobe Experience Platform mobile.

Le SDK Mobile Experience Platform est un SDK côté client qui permet aux clients de Adobe Experience Cloud d’interagir avec les applications Adobe et les services tiers par le biais du réseau Adobe Experience Platform Edge. Voir [Documentation du SDK Mobile Adobe Experience Platform](https://aep-sdks.gitbook.io/docs/) pour plus d’informations.

![paramètres de création](assets/data-collection-mobile-sdk.png)


Ce tutoriel vous guide tout au long de la mise en oeuvre du SDK Mobile Platform dans un exemple d’application de vente au détail appelée Luma. Le [Application Luma](https://github.com/Adobe-Marketing-Cloud/Luma-iOS-Mobile-App) dispose d’une fonctionnalité qui vous permet de créer une mise en oeuvre réaliste. Après avoir terminé ce tutoriel, vous devriez être prêt à commencer à mettre en oeuvre toutes vos solutions marketing par le biais du SDK Mobile Platform dans vos propres applications mobiles.

Les leçons sont conçues pour iOS et écrites dans Swift, mais de nombreux concepts s’appliquent également à Android™.

Après avoir terminé ce tutoriel, vous serez en mesure de :

* Créez un schéma à l’aide de groupes de champs standard et personnalisés.
* Configurez un flux de données.
* Configurez une propriété de balise mobile.
* Configurez un jeu de données Experience Platform (facultatif).
* Installez et implémentez des extensions de balise dans une application.
* Ajoutez les applications/extensions Adobe Experience Cloud suivantes :
   * [Adobe Experience Platform Edge (XDM)](events.md)
   * [Collecte de données du cycle de vie](lifecycle-data.md)
   * [Adobe Analytics via XDM](analytics.md)
   * [Consentement](consent.md)
   * [Identité](identity.md)
   * [Profile](profile.md)
   * [Adobe Experience Platform](platform.md)
   * [Messagerie push avec Journey Optimizer](journey-optimizer-push.md)
* Transmettez correctement les paramètres Experience Cloud à un [webview](web-views.md).
* Validation de la mise en oeuvre à l’aide de [Adobe Experience Platform Assurance](assurance.md).

>[!NOTE]
>
>Un tutoriel multisolution similaire est disponible pour [SDK Web](../tutorial-web-sdk/overview.md).

## Conditions préalables

Dans ces leçons, nous supposons que vous disposez d’un Adobe ID et des autorisations requises pour effectuer les exercices. Dans le cas contraire, contactez votre administrateur d’Adobe pour demander l’accès.

* Dans la collecte de données, vous devez disposer des éléments suivants :
   * **[!UICONTROL Plateformes]**—élément d’autorisation **[!UICONTROL Mobile]**
   * **[!UICONTROL Droits de propriété]**: éléments d’autorisation pour **[!UICONTROL Développer]**, **[!UICONTROL Approuver]**, **[!UICONTROL Publier]**, **[!UICONTROL Gestion des extensions]**, et **[!UICONTROL Gestion des environnements]**.
   * **[!UICONTROL Droits d’entreprise]**: éléments d’autorisation pour **[!UICONTROL Gestion des propriétés]** et, si vous suivez la leçon facultative sur la messagerie push, **[!UICONTROL Gestion des configurations d’application]**

      Pour plus d’informations sur les autorisations de balise, voir [Autorisations utilisateur pour les balises](https://experienceleague.adobe.com/docs/experience-platform/tags/admin/user-permissions.html?lang=fr){target=&quot;_blank&quot;} dans la documentation du produit.
* En Experience Platform, vous devez disposer des éléments suivants :
   * **[!UICONTROL Modélisation des données]**: éléments d’autorisation pour gérer et afficher les schémas.
   * **[!UICONTROL Identity Management]**: éléments d’autorisation pour gérer et afficher les espaces de noms d’identité.
   * **[!UICONTROL Collecte de données]**: éléments d’autorisation pour gérer et afficher les flux de données.

   * Si vous êtes le client d’une application basée sur Platform telle que Real-Time CDP, Journey Optimizer ou Customer Journey Analytics, vous devez également disposer des éléments suivants :
      * **[!UICONTROL Data Management]**: éléments d’autorisation pour gérer et afficher les jeux de données pour terminer les _exercices Platform facultatifs_ (nécessite une licence pour une application basée sur Platform ).
      * Un développement **sandbox** que vous pouvez utiliser pour ce tutoriel.
* Pour Adobe Analytics, vous devez savoir lequel **suites de rapports** vous pouvez utiliser pour terminer ce tutoriel.

Tous les clients Experience Cloud doivent avoir accès aux fonctionnalités requises pour déployer le SDK Mobile.

En outre, il est supposé que vous connaissez les [!DNL Swift]. Vous n’avez pas besoin d’être un expert pour terminer les leçons, mais vous en tirerez plus d’informations si vous pouvez facilement lire et comprendre le code.

## Téléchargement de l’application Luma

Deux versions de l’exemple d’application sont disponibles en téléchargement.

1. [Vide](https://github.com/Adobe-Marketing-Cloud/Luma-iOS-Mobile-App){target=&quot;_blank&quot;} - version sans code Experience Cloud pour terminer les exercices pratiques dans ce tutoriel
1. [Intégralement implémenté](https://github.com/Adobe-Marketing-Cloud/Luma-iOS-Mobile-App){target=&quot;_blank&quot;} : version avec mise en oeuvre Experience Cloud complète à titre de référence.

C’est parti !


Suivant : **[Création d’un schéma XDM](create-schema.md)**

>[!NOTE]
>
>Merci d’avoir consacré votre temps à l’apprentissage du SDK Adobe Experience Platform Mobile. Si vous avez des questions, souhaitez partager des commentaires généraux ou avez des suggestions sur le contenu futur, partagez-les à ce sujet. [Article de discussion de la communauté Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796)