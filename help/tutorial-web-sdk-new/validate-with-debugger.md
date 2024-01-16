---
title: Validation des mises en oeuvre du SDK Web avec le débogueur Experience Platform
description: Découvrez comment valider votre mise en oeuvre du SDK Web Platform avec Adobe Experience Platform Debugger. Cette leçon fait partie du tutoriel Mise en oeuvre de Adobe Experience Cloud avec le SDK Web .
feature: Web SDK,Tags,Debugger
source-git-commit: 904581df85df5d8fc4f36a4d47a37b03ef92d76f
workflow-type: tm+mt
source-wordcount: '1465'
ht-degree: 1%

---

# Validation des mises en oeuvre du SDK Web avec le débogueur Experience Platform

Découvrez comment valider votre mise en oeuvre du SDK Web Platform avec Adobe Experience Platform Debugger.

Le débogueur Experience Platform est une extension disponible pour les navigateurs Chrome et Firefox qui vous permet de voir la technologie d’Adobe mise en oeuvre dans vos pages web. Téléchargez la version de votre navigateur préféré :

* [Extension Firefox](https://addons.mozilla.org/fr/firefox/addon/adobe-experience-platform-dbg/)
* [Extension Chrome](https://chrome.google.com/webstore/detail/adobe-experience-platform/bfnnokhpnncpkdmbokanobigaccjkpob)

Si vous n’avez jamais utilisé le débogueur auparavant et que celui-ci est différent de l’ancien débogueur Adobe Experience Cloud, vous pouvez regarder cette vidéo de présentation de cinq minutes :

>[!VIDEO](https://video.tv.adobe.com/v/32156?learn=on)

Dans cette leçon, vous utilisez la méthode [Extension Adobe Experience Cloud Debugger](https://chrome.google.com/webstore/detail/adobe-experience-cloud-de/ocdmogmohccmeicdhlhhgepeaijenapj) pour remplacer la propriété de balise codée en dur sur la propriété [Site de démonstration Luma](https://luma.enablementadobe.com/content/luma/us/en.html) avec votre propre propriété.

Cette technique, appelée changement d’environnement, vous sera utile ultérieurement lorsque vous utiliserez des balises sur votre propre site web. Vous pouvez charger votre site web de production dans votre navigateur, mais avec votre *development* environnement de balises. Cette fonctionnalité vous permet d’effectuer et de valider des modifications de balises en toute confiance, indépendamment de vos mises à jour de code standard. Après tout, cette séparation entre les mises à jour de balises marketing et les mises à jour de code standard est l’une des principales raisons pour lesquelles les clients utilisent des balises en premier lieu !

## Objectifs d&#39;apprentissage

À la fin de cette leçon, vous pourrez utiliser le débogueur pour :

* Chargement d’une autre bibliothèque de balises
* Validez que l’événement XDM côté client capture et envoie des données comme prévu à Platform Edge Network
* Activation d’Edge Trace pour afficher les requêtes côté serveur envoyées par Platform Edge Network
* Démarrez une session Adobe Experience Platform Assurance pour afficher un identifiant Experience Cloud généré par Platform Edge Network.

## Conditions préalables

Vous connaissez bien les balises de collecte de données et la variable [Site de démonstration Luma](https://luma.enablementadobe.com/content/luma/us/en.html){target="_blank"} et avoir suivi les leçons précédentes suivantes dans le tutoriel :

* [Configurer un schéma XDM](configure-schemas.md)
* [Configuration d’un espace de noms d’identité](configure-identities.md)
* [Configurer un trains de données](configure-datastream.md)
* [Extension SDK Web installée dans la propriété de balise](install-web-sdk.md)
* [Créer des éléments de données](create-data-elements.md)
* [Création d’identités](create-identities.md)
* [Création d’une règle de balise](create-tag-rule.md)

## Chargement de bibliothèques de balises alternatives avec Debugger

Ce tutoriel utilise une version hébergée publiquement de [Site web de démonstration Luma](https://luma.enablementadobe.com/content/luma/us/en.html). Ouvrez la page d’accueil et mettez-la en signet.

![Page d’accueil Luma](assets/validate-luma-site.png)

Le débogueur Experience Platform dispose d’une fonctionnalité intéressante qui vous permet de remplacer une bibliothèque de balises existante par une autre. Cette technique est utile pour la validation et nous permet d’ignorer de nombreuses étapes d’implémentation dans ce tutoriel.

1. Assurez-vous que le site Luma est ouvert et sélectionnez l’icône de l’extension Debugger Experience Platform.
1. Le débogueur s’ouvre et affiche quelques détails sur l’implémentation codée en dur, qui n’est pas liée à ce tutoriel (vous devrez peut-être recharger le site Luma après avoir ouvert le débogueur).
1. Vérifiez que le débogueur est &quot;**[!UICONTROL Connexion à Luma]**&quot; comme illustré ci-dessous, puis sélectionnez &quot;**[!UICONTROL lock]**&quot; pour verrouiller le débogueur sur le site Luma.
1. Sélectionnez la variable **[!UICONTROL Se connecter]** et connectez-vous à Adobe Experience Cloud à l’aide de votre identifiant d’Adobe.
1. Accédez à **[!UICONTROL Balises Experience Platform]** dans la navigation de gauche

   ![Écran de balise Debugger](assets/validate-launch-screen.png)

1. Sélectionnez la variable **[!UICONTROL Configuration]** tab
1. À droite de l’emplacement où il vous montre la variable **[!UICONTROL Codes d’intégration de page]**, ouvrez le **[!UICONTROL Actions]** , puis sélectionnez **[!UICONTROL Remplacer]**

   ![Sélectionnez Actions > Remplacer .](assets/validate-switch-environment.png)

1. Puisque vous êtes authentifié, le débogueur va extraire vos propriétés et environnements de balise disponibles. Sélectionnez votre propriété ; dans ce cas, `Web SDK Course 3`
1. Sélectionnez votre `Development` environnement
1. Sélectionnez la variable **[!UICONTROL Appliquer]** button

   ![Sélectionnez la propriété de balise alternative.](assets/validate-switch-selection.png)

1. Le site web Luma est maintenant rechargé. _avec votre propre propriété de balise_.

   ![propriété de balise remplacée](assets/validate-switch-success.png)

Au fur et à mesure que vous continuez le tutoriel, vous utilisez cette technique pour mapper le site Luma sur votre propre propriété de balise afin de valider votre mise en oeuvre du SDK Web Platform. Lorsque vous commencez à utiliser des balises sur votre site web de production, vous pouvez utiliser cette même technique pour valider les modifications.

## Validation des requêtes réseau côté client avec le débogueur Experience Platform

Vous pouvez utiliser le débogueur pour valider les balises côté client déclenchées à partir de votre mise en oeuvre du SDK Web Platform pour afficher les données envoyées à Platform Edge Network :

1. Accédez à **[!UICONTROL Résumé]** dans le volet de navigation de gauche, pour afficher les détails de votre propriété de balise

   ![Onglet Résumé](assets/validate-summary.png)

1. Accédez à **[!UICONTROL SDK Web Experience Platform]** dans le volet de navigation de gauche pour afficher la variable **[!UICONTROL Requêtes réseau]**
1. Ouvrez le **[!UICONTROL events]** row

   ![Requête SDK Web Adobe Experience Platform](assets/validate-aep-screen.png)

1. Notez comment vous pouvez voir la variable `web.webpagedetails.pageView` type d’événement que vous avez spécifié dans votre [!UICONTROL Mettre à jour la variable] , ainsi que d’autres variables prêtes à l’emploi conformes à la `AEP Web SDK ExperienceEvent` groupe de champs

   ![Détails de l’événement](assets/validate-event-pageViews.png)

1. Faites défiler l’écran vers le bas jusqu’à `web` , sélectionnez pour l’ouvrir et examinez l’objet `webPageDetails.name`, `webPageDetails.server`, et `webPageDetails.siteSection`. Ils doivent correspondre au `digitalData` variables de couche de données sur la page d’accueil

>[!TIP]
>
> Pour afficher et comparer le `digitalData` couche de données sur la page d’accueil :
>
> 1. Sur la page d’accueil de Luma, ouvrez les outils de développement du navigateur. Dans le cas de Chrome, cliquez sur le bouton `F12` sur votre clavier
> 1. Sélectionnez la variable **[!UICONTROL Console]** tab
> 1. Entrée `digitalData` et sélectionnez `Enter` sur votre clavier pour afficher les valeurs de couche de données.

![Onglet Réseau](assets/validate-xdm-content.png)

Vous pouvez également valider les détails de la carte des identités :

1. Connectez-vous au site Luma à l’aide des informations d’identification. `test@adobe.com`/`test`

1. Revenez à la [page d’accueil de Luma](https://luma.enablementadobe.com/content/luma/us/en.html).

1. Ouvrez le **[!UICONTROL SDK Web Experience Platform]** dans la navigation de gauche

   ![SDK Web dans Debugger](assets/identity-debugger-websdk-dark.png)

1. Sélectionnez la variable **[!UICONTROL events]** pour ouvrir les détails dans une fenêtre contextuelle

   ![SDK Web dans Debugger](assets/identity-deugger-websdk-event-dark.png)

1. Recherchez le **identityMap** dans la fenêtre contextuelle. Ici, vous devriez voir `lumaCrmId` avec trois clés authenticatedState, id et primary :
   ![SDK Web dans Debugger](assets/identity-deugger-websdk-event-lumaCrmId-dark.png)

### Validation des requêtes côté client à l’aide des outils de développement de navigateur

Ces types de détails de requête sont également visibles dans les outils de développement web du navigateur. **Réseau** (en supposant que le site web charge votre bibliothèque de balises).

1. Ouvrez les outils de développement web du navigateur. **Réseau** et rechargez la page. Filtrer les appels avec `/ee` pour localiser l’appel, sélectionnez-le, puis recherchez dans le **En-têtes** et **Payload** tab

   ![Onglet Réseau](assets/validate-dev-console.png)

1. Accédez au **Réponse** et notez comment la valeur ECID est incluse dans la réponse. Copiez cette valeur, car vous l’utiliserez pour valider les informations de profil lors de l’exercice suivant.

   ![Onglet Réseau](assets/validate-dev-console-ecid.png)


## Validation des requêtes réseau côté serveur avec le débogueur Experience Platform

Comme vous l’avez appris dans la [Configuration d’un flux de données](configure-datastream.md) leçon à retenir, le SDK Web Platform envoie d’abord des données de votre propriété numérique à Platform Edge Network. Ensuite, Platform Edge Network effectue des requêtes supplémentaires côté serveur vers les services correspondants activés dans votre flux de données.

Vous pouvez valider les requêtes côté serveur en activant Edge Trace dans le débogueur. En outre, vous pouvez également valider la charge utile entièrement traitée après qu’elle a atteint une application d’Adobe en utilisant [Adobe Experience Platform Assurance](https://experienceleague.adobe.com/docs/experience-platform/assurance/home.html?lang=en).

Dans les deux exercices suivants, vous activez Edge Trace et affichez l’identifiant Experience Cloud généré à partir de Platform Edge Network à l’aide d’Assurance.

### Activation d’Edge Trace

Pour activer Edge Trace

1. Dans le volet de navigation de gauche de **[!UICONTROL Débogueur Experience Platform]** select **[!UICONTROL Journaux]**
1. Sélectionnez la variable **[!UICONTROL Edge]** et sélectionnez **[!UICONTROL Connexion]**

   ![Connexion à Edge Trace](assets/analytics-debugger-edgeTrace.png)

1. Il est vide pour l’instant.

   ![Trace Edge connectée](assets/analytics-debugger-edge-connected.png)

1. Actualisez la variable [Page d’accueil Luma](https://luma.enablementadobe.com/) et vérifier **[!UICONTROL Débogueur Experience Platform]** encore une fois, pour voir les données passer.

   ![Balise Analytics Edge Trace](assets/validate-edge-trace.png)

À ce stade, vous ne pouvez pas afficher les requêtes Platform Edge Network envoyées à une application Adobe, car vous n’en avez activé aucune dans le flux de données. Dans les leçons futures, vous utiliserez Edge Trace pour afficher les requêtes sortantes côté serveur pour Adobe des applications. Cependant, avec Assurance, vous pouvez toujours afficher l’identifiant Experience Cloud généré par Platform Edge Network.

### Démarrer une session d’assurance

Adobe Experience Platform Assurance est un produit de Adobe Experience Cloud qui vous aide à inspecter, à tester, à simuler et à valider la manière dont vous collectez des données ou diffusez des expériences.

En savoir plus sur [Assurance Adobe](https://experienceleague.adobe.com/docs/experience-platform/assurance/home.html?lang=en).

Chaque fois que vous activez Edge Trace, une session d’assurance est lancée en arrière-plan.

Pour afficher la session Assurance,

1. Une fois Edge Trace activé, une icône de lien sortant s’affiche en haut de l’écran. Sélectionnez l’icône pour ouvrir Assurance. Un nouvel onglet s’ouvre dans votre navigateur.

   ![Démarrer la session Assurance](assets/validate-debugger-start-assurnance.png)

1. Sélectionnez la ligne avec l’événement appelé Adobe Response Handle.
1. Un menu s’affiche à droite. Sélectionnez la variable `+` signe en regard de `[!UICONTROL ACPExtensionEvent]`
1. Effectuez un zoom avant en sélectionnant `[!UICONTROL payload > 0 > payload > 0 > namespace]`. L’identifiant affiché sous la dernière `0` correspond au `ECID`. Vous le savez par la valeur qui apparaît sous `namespace` match `ECID`

   ![Assurance validate ECID](assets/validate-assurance-ecid.png)

   >[!CAUTION]
   >
   >Vous pouvez voir une valeur ECID tronquée en raison de la largeur de la fenêtre. Il vous suffit de sélectionner la barre de gestion dans l’interface et de faire glisser le curseur vers la gauche pour afficher l’ensemble de l’ECID.

Dans les futures leçons, vous utiliserez Assurance pour valider les payloads entièrement traités atteignant une application d’Adobe activée dans votre flux de données.

Avec un objet XDM qui se déclenche maintenant sur une page et avec les connaissances nécessaires pour valider votre collecte de données, vous êtes prêt à configurer les applications Adobe individuelles à l’aide du SDK Web Platform.

[Suivant : ](setup-experience-platform.md)

>[!NOTE]
>
>Merci d’avoir consacré du temps à l’apprentissage du SDK Web Adobe Experience Platform. Si vous avez des questions, souhaitez partager des commentaires généraux ou avez des suggestions sur le contenu futur, partagez-les à ce sujet. [Article de discussion de la communauté Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996)