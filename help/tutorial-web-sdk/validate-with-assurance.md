---
title: Validation des mises en oeuvre du SDK Web avec Experience Platform Assurance
description: Découvrez comment valider votre implémentation du SDK web de Platform avec Adobe Experience Platform Assurance. Cette leçon fait partie du tutoriel Implémentation d’Adobe Experience Cloud avec le SDK web.
feature: Web SDK,Tags,Assurance
jira: KT-15406
exl-id: 31e381ea-fbaf-495f-a6e9-2ff6c0d36939
source-git-commit: a8431137e0551d1135763138da3ca262cb4bc4ee
workflow-type: tm+mt
source-wordcount: '606'
ht-degree: 7%

---

# Validation des mises en oeuvre du SDK Web avec Experience Platform Assurance

Adobe Experience Platform Assurance est une fonctionnalité qui vous permet d’inspecter, de tester, de simuler et de valider la manière dont vous collectez des données ou diffusez des expériences. En savoir plus sur [Assurance Adobe](https://experienceleague.adobe.com/en/docs/experience-platform/assurance/home).


## Objectifs d&#39;apprentissage

À la fin de cette leçon, vous saurez comment :

* Démarrer une session d’assurance
* Affichage des requêtes envoyées à et depuis l’Edge Network Platform

## Conditions préalables

Vous connaissez bien les balises de collecte de données et la variable [Site de démonstration Luma](https://luma.enablementadobe.com/content/luma/us/en.html){target="_blank"} et avoir terminé les leçons précédentes du tutoriel :

* [Configurer un schéma XDM](configure-schemas.md)
* [Configuration d’un espace de noms d’identité](configure-identities.md)
* [Configurer un trains de données](configure-datastream.md)
* [Extension SDK Web installée dans la propriété de balise](install-web-sdk.md)
* [Création d’éléments de données](create-data-elements.md)
* [Création d’identités](create-identities.md)
* [Création d’une règle de balise](create-tag-rule.md)
* [Validation avec Debugger](validate-with-debugger.md)


## Démarrer et afficher une session d’assurance

Il existe plusieurs façons de démarrer une session d’assurance.

### Démarrage d’une session d’assurance dans Debugger

Chaque fois que vous activez Edge Trace dans Adobe Experience Platform Debugger, une session d’assurance est lancée en arrière-plan.

Revue de la leçon sur Debugger :

1. Accédez au [Site de démonstration Luma](https://luma.enablementadobe.com/content/luma/us/en.html) et utilisez le débogueur pour [basculez la propriété de balise sur le site sur votre propre propriété de développement.](validate-with-debugger.md#use-the-experience-platform-debugger-to-map-to-your-tags-property)
1. Dans le volet de navigation de gauche de **[!UICONTROL Débogueur Experience Platform]** select **[!UICONTROL Journaux]**
1. Sélectionnez la variable **[!UICONTROL Edge]** et sélectionnez **[!UICONTROL Connexion]**

   ![Connexion à Edge Trace](assets/analytics-debugger-edgeTrace.png)
1. Une fois Edge Trace activé, une icône de lien sortant s’affiche en haut de l’écran. Sélectionnez l’icône pour ouvrir Assurance.

   ![Démarrer la session Assurance](assets/validate-debugger-start-assurnance.png)

1. Un nouvel onglet du navigateur s’ouvre avec l’interface Assurance.

### Démarrer une session Assurance à partir de l’interface Assurance

1. Ouvrez le [Interface de collecte de données](https://experience.adobe.com/#/data-collection/home){target="_blank"}
1. Sélectionnez Assurance dans la navigation de gauche.
1. Sélectionner Créer une session
   ![Création d’une session d’assurance](assets/assurance-create-session.png)
1. Sélectionner le début
1. Attribuez un nom à la session, par exemple : `Luma Web SDK validation`
1. Comme la variable **[!UICONTROL URL de base]** enter `https://luma.enablementadobe.com/`
   ![Attribution d’un nom à la session Assurance](assets/assurance-name-session.png)
1. Dans l’écran suivant, sélectionnez **[!UICONTROL Copier le lien]**
1. Sélectionnez l’icône pour copier le lien dans le presse-papiers.
1. Collez l’URL dans votre navigateur, qui ouvre le site web Luma avec un paramètre d’URL spécial. `adb_validation_sessionid` et démarrez la session
1. Dans l’interface Assurance, un message doit s’afficher pour vous indiquer que vous avez réussi à vous connecter à la session et que les événements sont capturés dans l’interface Assurance.
   ![La session d’assurance est connectée.](assets/assurance-success.png)

## Validation de l’état actuel de la mise en oeuvre de votre SDK Web

Les informations à afficher à ce stade de la mise en oeuvre sont limitées. Une valeur que nous pouvons voir est votre identifiant Experience Cloud (ECID) généré sur Platform Edge Network :

1. Sélectionnez la ligne avec l’événement appelé `Alloy Response Handle`.
1. Un menu s’affiche à droite. Sélectionnez la variable `+` signe en regard de `[!UICONTROL ACPExtensionEventData]`
1. Effectuez un zoom avant en sélectionnant `[!UICONTROL payload > 0 > payload > 0 > namespace]`. L’identifiant affiché sous la dernière `0` correspond au `ECID`. Vous le savez par la valeur qui apparaît sous `namespace` match `ECID`

   ![Assurance validate ECID](assets/validate-assurance-ecid.png)

   >[!CAUTION]
   >
   >Vous pouvez voir une valeur ECID tronquée en raison de la largeur de la fenêtre. Il vous suffit de sélectionner la barre de gestion dans l’interface et de faire glisser le curseur vers la gauche pour afficher l’ensemble de l’ECID.

Dans les futures leçons, vous utiliserez Assurance pour valider les payloads entièrement traités atteignant une application d’Adobe activée dans votre flux de données.

Avec un objet XDM qui se déclenche maintenant sur une page et avec les connaissances nécessaires pour valider votre collecte de données, vous êtes prêt à configurer les applications Experience Platform et d’Adobe individuelles à l’aide du SDK Web Platform.

[Suivant : ](setup-experience-platform.md)

>[!NOTE]
>
>Merci d’avoir consacré du temps à l’apprentissage du SDK Web Adobe Experience Platform. Si vous avez des questions, souhaitez partager des commentaires généraux ou avez des suggestions sur le contenu futur, partagez-les à ce sujet. [Article de discussion de la communauté Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996)
