---
title: Installation et configuration de l’extension de balise Adobe Experience Platform Web SDK
description: Découvrez comment installer et configurer l’extension de balise Platform Web SDK dans l’interface de collecte de données. Cette leçon fait partie du tutoriel Implémentation d’Adobe Experience Cloud avec le SDK web.
feature: Web SDK, Tags
jira: KT-15404
exl-id: f30a44bb-99d7-476e-873a-b7802a0fe6aa
source-git-commit: 1fc027db2232c8c56de99d12b719ec10275b590a
workflow-type: tm+mt
source-wordcount: '638'
ht-degree: 10%

---

# Installation de l’extension de balise Adobe Experience Platform Web SDK

Découvrez comment installer et configurer l’extension de balise Adobe Experience Platform Web SDK. Le moyen le plus simple de mettre en œuvre Web SDK consiste à utiliser le gestionnaire de balises d’Adobe, les balises (anciennement appelé Launch). L’extension de balise SDK Web Platform est la _seule extension de balise_ requise pour envoyer des données à _toutes les applications Adobe Experience Cloud_, y compris [Analytics](setup-analytics.md), [Target](setup-target.md), [Audience Manager](setup-audience-manager.md), Real-Time Customer Data Platform et [Journey Optimizer](setup-web-channel.md) !


>[!WARNING]
>
> Le site web Luma utilisé dans ce tutoriel devrait être remplacé au cours de la semaine du 16 février 2026. Le travail effectué dans le cadre de ce tutoriel peut ne pas s’appliquer au nouveau site web.

## Objectifs d’apprentissage

À la fin de cette leçon, vous saurez comment :

* Créer une propriété de balise dans l’interface de collecte de données
* Installation de l’extension de balises de Platform Web SDK
* Mappez le flux de données créé précédemment à l’extension

## Conditions préalables

Vous devez avoir terminé les leçons précédentes de ce tutoriel :

* [Configurer un trains de données](configure-datastream.md)

### Ajout d’une propriété de balise

Vous devez d’abord disposer d’une propriété de balise. Une propriété est un conteneur de toutes les fonctionnalités, JavaScript, règles et autres, nécessaires pour collecter des détails dans une page web et l’envoyer à différents emplacements.

Créez une propriété de balise pour le tutoriel :

1. Ouvrez l’interface [Collecte de données](https://experience.adobe.com/data-collection/){target="_blank"}
1. Sélectionnez **[!UICONTROL Balises]** dans le volet de navigation de gauche
1. Sélectionnez le bouton **[!UICONTROL Nouvelle propriété]**
   ![Ajouter une nouvelle propriété](assets/websdk-property-addNewProperty.png)
1. Dans le champ **[!UICONTROL Nom]**, saisissez `Web SDK Course` (ajoutez votre nom à la fin, si plusieurs personnes de votre entreprise suivent ce tutoriel)
1. Pour le **[!UICONTROL Domaines]**, saisissez `enablementadobe.com` (expliqué plus loin)
1. Sélectionnez **[!UICONTROL Enregistrer]**
   ![Détails de la propriété](assets/websdk-property-propertyDetails.png)

## Ajouter l’extension Web SDK

Maintenant que votre schéma XDM, votre flux de données et votre propriété de balise sont créés, vous êtes prêt à installer l’extension SDK web Platform :

1. Ouvrez votre nouvelle propriété de balise.
1. Accédez à **[!UICONTROL Extensions]** > **[!UICONTROL Catalogue]**
1. Rechercher des `Adobe Experience Platform Web SDK`
1. Sélectionnez **[!UICONTROL Installer]**

   ![Installer l’extension Web SDK](assets/extension-platform-web-sdk.png)


## Lier l’extension à votre flux de données

Conservez la plupart des paramètres par défaut et mettez-les à jour ultérieurement, si nécessaire. La seule chose que vous devez faire maintenant est de lier l’extension à votre flux de données :

1. Sous **[!UICONTROL Flux de données]**, sélectionnez la méthode d’entrée **[!UICONTROL Choisir parmi]**
1. Sélectionnez le sandbox dans lequel vous avez créé le schéma, l’espace de noms d’identité et le flux de données
1. Sélectionnez le flux de données que vous avez créé précédemment, `Luma Web SDK`
1. Sélectionnez **[!UICONTROL Enregistrer]**

   >[!NOTE]
   >
   > Si vous ne trouvez pas votre flux de données, suivez la leçon [Configurer un flux de données](configure-datastream.md) et suivez les étapes pour en créer un

   ![Sélection du flux de données](assets/extension-luma-web-sdk-datastream-extension.png)

Pour plus d’informations sur chaque section de l’extension, consultez [Configuration de l’extension Adobe Experience Platform Web SDK](https://experienceleague.adobe.com/fr/docs/experience-platform/tags/extensions/client/web-sdk/web-sdk-extension-configuration).

>[!NOTE]
>
>Bien que vous n’ayez pas configuré de CNAME dans le domaine [!UICONTROL Edge] dans cette leçon, Adobe vous recommande d’utiliser un CNAME lorsque vous implémentez Platform Web SDK sur votre propre site web. Bien quʼune implémentation CNAME ne permette pas dʼallonger la durée de vie des cookies, elle offre dʼautres avantages. Ces avantages incluent des bloqueurs de publicités et des navigateurs moins courants qui empêchent l’envoi de données vers des domaines qu’ils considèrent comme des dispositifs de suivi (ou traceurs). Dans ce cas, lʼutilisation dʼun CNAME peut éviter que votre collecte de données ne soit interrompue pour les utilisateurs qui se servent de ces outils.

>[!NOTE]
>
>Au cours de ce tutoriel, vous ne configurez qu’un seul flux de données et l’associez à tous les environnements de balises (développement, évaluation et production). Lorsque vous implémentez Platform Web SDK sur votre propre site Web, vous devez configurer un flux de données distinct pour chaque environnement et le mapper en conséquence dans la configuration de l’extension.

Maintenant que vous avez installé Platform Web SDK et que vous l’avez associé au flux de données, vous êtes prêt à commencer à collecter des données.

>[!NOTE]
>
>Merci d’avoir investi votre temps dans votre apprentissage de Adobe Experience Platform Web SDK. Si vous avez des questions, souhaitez partager des commentaires généraux ou avez des suggestions sur le contenu futur, veuillez les partager dans ce [article de discussion de la communauté Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996?profile.language=fr)
