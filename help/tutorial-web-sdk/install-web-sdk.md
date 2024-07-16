---
title: Installation et configuration de l’extension de balise du SDK Web Adobe Experience Platform
description: Découvrez comment installer et configurer l’extension de balise SDK Web Platform dans l’interface de collecte de données. Cette leçon fait partie du tutoriel Implémentation d’Adobe Experience Cloud avec le SDK web.
feature: Web SDK, Tags
jira: KT-15404
exl-id: f30a44bb-99d7-476e-873a-b7802a0fe6aa
source-git-commit: a8431137e0551d1135763138da3ca262cb4bc4ee
workflow-type: tm+mt
source-wordcount: '607'
ht-degree: 11%

---

# Installation de l’extension de balise du SDK Web Adobe Experience Platform

Découvrez comment installer et configurer l’extension de balise du SDK Web de Adobe Experience Platform. Le moyen le plus simple d’implémenter le SDK Web consiste à utiliser le gestionnaire de balises d’Adobe, les balises (anciennement Launch). L’extension de balise du SDK Web Platform est l’ _seule extension de balise_ requise pour envoyer des données à _toutes les applications Adobe Experience Cloud_, y compris [Analytics](setup-analytics.md), [Target](setup-target.md), [Audience Manager](setup-audience-manager.md), Real-Time Customer Data Platform et [Journey Optimizer](setup-web-channel.md) !

## Objectifs d&#39;apprentissage

À la fin de cette leçon, vous saurez comment :

* Création d’une propriété de balise dans l’interface de collecte de données
* Installation de l’extension de balise SDK Web Platform
* Mappage de votre flux de données créé précédemment à l’extension

## Conditions préalables

Vous devez avoir terminé les leçons précédentes de ce tutoriel :

* [Configurer un trains de données](configure-datastream.md)

### Ajouter une propriété de balise

Tout d’abord, vous devez disposer d’une propriété de balise. Une propriété est un conteneur pour toutes les JavaScript, règles et autres fonctionnalités requises pour collecter des détails à partir d’une page web et les envoyer à différents emplacements.

Créez une propriété de balise pour le tutoriel :

1. Ouvrez l’ [ interface de collecte de données](https://launch.adobe.com/){target="_blank"}
1. Sélectionnez **[!UICONTROL Balises]** dans le volet de navigation de gauche
1. Sélectionnez le bouton **[!UICONTROL New Property]**
   ![Ajouter une nouvelle propriété](assets/websdk-property-addNewProperty.png)
1. En tant que **[!UICONTROL Nom]**, saisissez `Web SDK Course` (ajoutez votre nom à la fin, si plusieurs personnes de votre société suivent ce tutoriel).
1. En tant que **[!UICONTROL domaines]**, saisissez `enablementadobe.com` (expliqué plus loin).
1. Sélectionnez **[!UICONTROL Save]**
   ![Détails de la propriété](assets/websdk-property-propertyDetails.png)

## Ajout de l’extension SDK Web

Avec votre schéma XDM, votre flux de données et votre propriété de balise maintenant créés, vous êtes prêt à installer l’extension SDK Web Platform :

1. Ouvrez la nouvelle propriété de balise .
1. Accédez à **[!UICONTROL Extensions]** > **[!UICONTROL Catalogue]**
1. Rechercher `Adobe Experience Platform Web SDK`
1. Sélectionnez **[!UICONTROL Install]**

   ![Installer l’extension SDK Web](assets/extension-platform-web-sdk.png)


## Lier l’extension à votre flux de données

Conservez la plupart des paramètres par défaut et mettez-les à jour ultérieurement, si nécessaire. La seule chose à faire maintenant est de lier l’extension à votre flux de données :

1. Sous **[!UICONTROL Datastreams]**, sélectionnez la méthode d’entrée **[!UICONTROL Choose from list]**
1. Sélectionnez l’environnement de test dans lequel vous avez créé le schéma, l’espace de noms d’identité et le flux de données.
1. Sélectionnez le flux de données que vous avez créé précédemment, `Luma Web SDK`
1. Sélectionnez **[!UICONTROL Save]**

   >[!NOTE]
   >
   > Si vous ne trouvez pas votre flux de données, accédez à la leçon [Configurer un flux de données](configure-datastream.md) et suivez les étapes pour en créer un.

   ![Sélection de flux de données](assets/extension-luma-web-sdk-datastream-extension.png)

Pour plus d’informations sur chaque section de l’extension, voir [Configuration de l’extension SDK Web Adobe Experience Platform](https://experienceleague.adobe.com/en/docs/experience-platform/tags/extensions/client/web-sdk/web-sdk-extension-configuration).

>[!NOTE]
>
>Bien que vous n’ayez pas configuré de CNAME dans le paramètre [!UICONTROL Domaine Edge] de cette leçon, Adobe vous recommande d’utiliser un CNAME lorsque vous implémentez le SDK Web Platform sur votre propre site web. Bien quʼune implémentation CNAME ne permette pas dʼallonger la durée de vie des cookies, elle offre dʼautres avantages. Ces avantages incluent les bloqueurs d’annonces et les navigateurs moins courants qui empêchent l’envoi de données aux domaines qu’ils classent comme outils de suivi. Dans ce cas, lʼutilisation dʼun CNAME peut éviter que votre collecte de données ne soit interrompue pour les utilisateurs qui se servent de ces outils.

>[!NOTE]
>
>Au cours de ce tutoriel, vous ne configurez qu’une seule banque de données et vous l’associez à tous les environnements de balises (développement, évaluation et production). Lorsque vous implémentez le SDK Web Platform sur votre propre site web, vous devez configurer un flux de données distinct pour chaque environnement et les mapper en conséquence dans la configuration de l’extension.

Maintenant que vous avez installé le SDK Web de Platform et que vous l’avez associé au flux de données, vous êtes prêt à commencer à collecter des données.

[Suivant : ](create-data-elements.md)

>[!NOTE]
>
>Merci d’avoir consacré du temps à l’apprentissage du SDK Web Adobe Experience Platform. Si vous avez des questions, souhaitez partager des commentaires généraux ou avez des suggestions sur le contenu à venir, partagez-les sur cet [post de discussion de la communauté Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996)
