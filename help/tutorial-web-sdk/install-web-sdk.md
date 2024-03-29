---
title: Installation et configuration de l’extension de balise du SDK Web Adobe Experience Platform
description: Découvrez comment installer et configurer l’extension de balise SDK Web Platform dans l’interface de collecte de données. Cette leçon fait partie du tutoriel Mise en oeuvre de Adobe Experience Cloud avec le SDK Web .
feature: Web SDK
exl-id: f30a44bb-99d7-476e-873a-b7802a0fe6aa
source-git-commit: 9f75ef042342e1ff9db6039e722159ad96ce5e5b
workflow-type: tm+mt
source-wordcount: '644'
ht-degree: 13%

---

# Installation de l’extension de balise du SDK Web Adobe Experience Platform


>[!CAUTION]
>
>Nous prévoyons de publier les modifications majeures de ce tutoriel le vendredi 15 mars 2024. Après ce point, de nombreux exercices changeront et vous devrez peut-être redémarrer le tutoriel dès le début pour terminer toutes les leçons.

Découvrez comment installer et configurer l’extension de balise SDK Web Platform dans l’interface de collecte de données. Cette extension de balise est _extension de balise uniquement_ requis pour envoyer des données à _toutes les applications Adobe Experience Cloud_, y compris [Analytics](setup-analytics.md), [Cible](setup-target.md), [Audience Manager](setup-audience-manager.md), Real-time Customer Data Platform et Journey Optimizer !

## Objectifs d&#39;apprentissage

À la fin de cette leçon, vous saurez comment :

* Création d’une propriété de balise dans l’interface de collecte de données
* Installation de l’extension de balise SDK Web Platform
* Mappage de votre flux de données créé précédemment à l’extension

## Conditions préalables

Vous devez avoir terminé les leçons précédentes de ce tutoriel :

* [Configuration des autorisations](configure-permissions.md)
* [Configurer un schéma XDM](configure-schemas.md)
* [Configuration d’un espace de noms d’identité](configure-identities.md)
* [Configurer un trains de données](configure-datastream.md)

## Installation de l’extension SDK Web Experience Platform

### Ajout d’une propriété

Tout d’abord, vous devez disposer d’une propriété de balise. Une propriété est un conteneur pour l’ensemble du code JavaScript, des règles et d’autres fonctionnalités nécessaires pour collecter des détails à partir d’une page web et les envoyer à différents emplacements.

Créez une propriété de balise pour le tutoriel :

1. Ouvrez le [Interface de collecte de données](https://launch.adobe.com/){target="_blank"}
1. Sélectionner **[!UICONTROL Balises]** dans la navigation de gauche
1. Sélectionnez la variable **[!UICONTROL Nouvelle propriété]** button
   ![Ajouter une nouvelle propriété](assets/websdk-property-addNewProperty.png)
1. Comme la variable **[!UICONTROL Nom]**, saisissez `Web SDK Course` (ajoutez votre nom à la fin, si plusieurs personnes de votre société suivent ce tutoriel)
1. Comme la variable **[!UICONTROL Domaines]**, saisissez `enablementadobe.com` (expliqué ultérieurement)
1. Sélectionnez **[!UICONTROL Enregistrer]**.
   ![Détails de la propriété](assets/websdk-property-propertyDetails.png)

## Ajout de l’extension SDK Web

Avec votre schéma XDM, votre flux de données et votre propriété de balise maintenant créés, vous êtes prêt à installer l’extension SDK Web Platform :

1. Ouvrez la nouvelle propriété de balise .
1. Accédez à **[!UICONTROL Extensions]** > **[!UICONTROL Catalogue]**.
1. Recherchez `Adobe Experience Platform Web SDK`.
1. Sélectionner **[!UICONTROL Installer]**

   ![Installation de l’extension SDK Web](assets/extension-platform-web-sdk.jpg)


## Lier le SDK Web Platform à votre flux de données

Conservez la plupart des paramètres par défaut et mettez-les à jour ultérieurement, si nécessaire. La seule chose à faire maintenant est de lier l’extension à votre flux de données :

1. Sous **[!UICONTROL Datastreams]**, sélectionnez la variable **[!UICONTROL Choisir parmi les listes]** méthode d&#39;entrée
1. Sélectionnez le flux de données que vous avez créé précédemment, `Luma Web SDK`
1. Sélectionnez **[!UICONTROL Enregistrer]**.
   >[!NOTE]
   >
   > Si vous ne trouvez pas votre flux de données, accédez au [Configuration d’un flux de données](configure-datastream.md) leçon et suivez les étapes pour en créer une

   ![Sélection des flux de données](assets/extension-luma-web-sdk-datastream-extension.png)

Maintenant que vous avez installé le SDK Web de Platform et que vous l’avez associé au flux de données, vous êtes prêt à commencer à mapper les éléments de données à un objet XDM avec le schéma que vous avez créé.

>[!NOTE]
>
>Au cours de ce tutoriel, vous ne configurez qu’une seule banque de données et vous l’associez à tous les environnements de balises (développement, évaluation et production). Lorsque vous implémentez le SDK Web Platform sur votre propre site web, vous devez configurer un flux de données distinct pour chaque environnement et les mapper à vos environnements de balises à l’aide de la fonction **[!UICONTROL Méthode d’entrée]** > **[!UICONTROL Saisir des valeurs]**
>
>![Sélection des flux de données](assets/extension-luma-web-sdk-datastream-extension-enterValues.png)

>[!NOTE]
>
>Bien que vous n’ayez pas configuré un CNAME dans la variable [!UICONTROL Domaine Edge] dans cette leçon, Adobe vous recommande d’utiliser un CNAME lorsque vous implémentez le SDK Web Platform sur votre propre site web. Bien quʼune implémentation CNAME ne permette pas dʼallonger la durée de vie des cookies, elle offre dʼautres avantages. Parmi ceux-ci, citons les bloqueurs de publicités et les navigateurs moins utilisés qui empêchent lʼenvoi des données aux domaines quʼils considèrent être des dispositifs de suivi. Dans ce cas, lʼutilisation dʼun CNAME peut éviter que votre collecte de données ne soit interrompue pour les utilisateurs qui se servent de ces outils.

Pour plus d’informations sur chaque section de l’extension, voir [Configuration de l’extension du SDK Web Adobe Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/edge/extension/web-sdk-extension-configuration.html?lang=fr)



[Suivant : ](create-data-elements.md)

>[!NOTE]
>
>Merci d’avoir consacré du temps à l’apprentissage du SDK Web Adobe Experience Platform. Si vous avez des questions, souhaitez partager des commentaires généraux ou avez des suggestions sur le contenu futur, partagez-les à ce sujet. [Article de discussion de la communauté Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996)
