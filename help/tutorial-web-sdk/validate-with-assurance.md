---
title: Validation des implémentations de Web SDK avec Experience Platform Assurance
description: Découvrez comment valider votre implémentation du SDK web de Platform avec Adobe Experience Platform Assurance. Cette leçon fait partie du tutoriel Implémentation d’Adobe Experience Cloud avec le SDK web.
feature: Web SDK,Tags,Assurance
jira: KT-15406
exl-id: 31e381ea-fbaf-495f-a6e9-2ff6c0d36939
source-git-commit: 7ccbaaf4db43921f07c971c485e1460a1a7f0334
workflow-type: tm+mt
source-wordcount: '605'
ht-degree: 7%

---

# Validation des implémentations de Web SDK avec Experience Platform Assurance

Adobe Experience Platform Assurance est une fonctionnalité qui vous permet d’inspecter, de tester, de simuler et de valider la manière dont vous collectez les données ou dont les expériences sont diffusées. En savoir plus sur [Adobe Assurance](https://experienceleague.adobe.com/fr/docs/experience-platform/assurance/home).


## Objectifs d’apprentissage

À la fin de cette leçon, vous saurez comment :

* Démarrer une session Assurance
* Afficher les requêtes envoyées à et depuis Platform Edge Network

## Conditions préalables

Vous connaissez les balises de la collecte de données et le site de démonstration [Luma](https://luma.enablementadobe.com/content/luma/us/en.html){target="_blank"} et avez terminé les leçons précédentes du tutoriel :

* [Configuration d’un schéma XDM](configure-schemas.md)
* [Configuration d’un espace de noms d’identité](configure-identities.md)
* [Configurer un trains de données](configure-datastream.md)
* [Extension Web SDK installée dans la propriété de balise](install-web-sdk.md)
* [Création d’éléments de données](create-data-elements.md)
* [Création d’identités](create-identities.md)
* [Création d’une règle de balise](create-tag-rule.md)
* [Validation avec Debugger](validate-with-debugger.md)


## Démarrer et afficher une session Assurance

Il existe plusieurs façons de démarrer une session Assurance.

### Démarrer une session Assurance dans Debugger

Chaque fois que vous activez Edge Trace dans Adobe Experience Platform Debugger, une session Assurance est lancée en arrière-plan.

En examinant comment nous l’avons fait dans la leçon sur le débogueur :

1. Accédez au [site de démonstration Luma](https://luma.enablementadobe.com/content/luma/us/en.html) et utilisez le débogueur pour [changer la propriété de balise du site en votre propre propriété de développement](validate-with-debugger.md#use-the-experience-platform-debugger-to-map-to-your-tags-property)
1. Dans le volet de navigation de gauche de **[!UICONTROL Experience Platform Debugger]** sélectionnez **[!UICONTROL Journaux]**
1. Sélectionnez l’onglet **[!UICONTROL Edge]**, puis sélectionnez **[!UICONTROL Se connecter]**

   ![Connexion à Edge Trace](assets/analytics-debugger-edgeTrace.png)
1. Lorsque Edge Trace est activé, une icône de lien sortant s’affiche en haut. Sélectionnez l’icône pour ouvrir Assurance.

   ![Démarrer une session Assurance](assets/validate-debugger-start-assurnance.png)

1. Un nouvel onglet du navigateur s’ouvre dans l’interface d’Assurance.

### Démarrer une session Assurance à partir de l’interface Assurance

1. Ouvrez l’interface [Collecte de données](https://experience.adobe.com/#/data-collection/home){target="_blank"}
1. Sélectionnez Assurance dans le volet de navigation de gauche
1. Sélectionner Créer une session
   ![Créer une session Assurance](assets/assurance-create-session.png)
1. Sélectionner le début
1. Attribuez un nom à la session, par exemple `Luma Web SDK validation`
1. Dans le champ **[!UICONTROL URL de base]** saisissez `https://luma.enablementadobe.com/`
   ![Nommez la session Assurance](assets/assurance-name-session.png)
1. Dans l’écran suivant, sélectionnez **[!UICONTROL Copier le lien]**
1. Sélectionnez l’icône pour copier le lien dans le presse-papiers
1. Collez l’URL dans votre navigateur, ce qui ouvrira le site web Luma avec un paramètre d’URL spécial `adb_validation_sessionid` et démarrera la session
1. Un message s’affiche dans l’interface d’Assurance pour indiquer que vous êtes correctement connecté à la session et vous devriez voir les événements capturés dans l’interface d’Assurance.
   ![La session Assurance s’est connectée](assets/assurance-success.png)

## Valider l’état actuel de votre implémentation de Web SDK

Les informations à afficher à ce stade de votre implémentation sont limitées. Une valeur que nous pouvons voir est votre Experience Cloud Id (ECID) qui est généré sur Platform Edge Network :

1. Sélectionnez la ligne contenant l’événement appelé `Alloy Response Handle`.
1. Un menu s’affiche à droite. Sélectionnez le signe `+` en regard de `[!UICONTROL ACPExtensionEventData]`
1. Accédez à une liste déroulante en sélectionnant `[!UICONTROL payload > 0 > payload > 0 > namespace]`. L’identifiant affiché sous la dernière `0` correspond à la `ECID`. Vous le savez par la valeur qui s’affiche sous `namespace` `ECID` correspondant

   ![Assurance validate ECID](assets/validate-assurance-ecid.png)

   >[!CAUTION]
   >
   >Il se peut que vous voyiez une valeur ECID tronquée en raison de la largeur de votre fenêtre. Il vous suffit de sélectionner la barre de poignée dans l’interface et de faire glisser vers la gauche pour afficher l’ECID entier.

Dans les leçons ultérieures, vous utiliserez Assurance pour valider les payloads entièrement traitées atteignant une application Adobe activée dans votre flux de données.

Maintenant qu’un objet XDM se déclenche sur une page et que vous savez comment valider votre collecte de données, vous êtes prêt à configurer Experience Platform et les applications Adobe individuelles à l’aide de Platform Web SDK.

>[!NOTE]
>
>Merci d’avoir investi votre temps dans votre apprentissage de Adobe Experience Platform Web SDK. Si vous avez des questions, souhaitez partager des commentaires généraux ou avez des suggestions sur le contenu futur, veuillez les partager dans ce [article de discussion de la communauté Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996?profile.language=fr)
