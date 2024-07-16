---
title: Validation des mises en oeuvre du SDK Web avec le débogueur Experience Platform
description: Découvrez comment valider votre mise en oeuvre du SDK Web Platform avec Adobe Experience Platform Debugger. Cette leçon fait partie du tutoriel Implémentation d’Adobe Experience Cloud avec le SDK web.
feature: Web SDK,Tags,Debugger
jira: KT-15405
exl-id: 150bb1b1-4523-4b44-bd4e-6cabc468fc04
source-git-commit: a8431137e0551d1135763138da3ca262cb4bc4ee
workflow-type: tm+mt
source-wordcount: '1172'
ht-degree: 3%

---

# Validation des mises en oeuvre du SDK Web avec le débogueur Experience Platform

Découvrez comment valider votre implémentation du SDK web d’Adobe Experience Platform avec Adobe Experience Platform Debugger.

Le débogueur Experience Platform est une extension disponible pour les navigateurs Chrome et Firefox, qui vous permet de voir la technologie d’Adobe mise en oeuvre dans vos pages web. Téléchargez la version de votre navigateur préféré :

* [Extension Firefox](https://addons.mozilla.org/fr/firefox/addon/adobe-experience-platform-dbg/)
* [Extension Chrome](https://chromewebstore.google.com/detail/adobe-experience-platform/bfnnokhpnncpkdmbokanobigaccjkpob)

Si vous n’avez jamais utilisé le débogueur auparavant, vous pouvez regarder cette vidéo de présentation de cinq minutes :

>[!VIDEO](https://video.tv.adobe.com/v/32156?learn=on)

Dans cette leçon, vous utilisez l’ [extension d’Adobe Experience Platform Debugger](https://chromewebstore.google.com/detail/adobe-experience-platform/bfnnokhpnncpkdmbokanobigaccjkpob) pour remplacer la propriété de balise codée en dur sur le [site de démonstration Luma](https://luma.enablementadobe.com/content/luma/us/en.html) par votre propre propriété.

Cette technique, appelée changement d’environnement, vous sera utile ultérieurement lorsque vous utiliserez des balises sur votre propre site web. Il vous permet de charger votre site web de production dans votre navigateur, mais avec votre bibliothèque de balises *development*. Cette fonctionnalité vous permet d’effectuer et de valider des modifications de balises en toute confiance, indépendamment de vos mises à jour de code standard. Après tout, cette séparation entre les mises à jour de balises marketing et les mises à jour de code standard est l’une des principales raisons pour lesquelles les clients utilisent des balises en premier lieu !

## Objectifs d&#39;apprentissage

À la fin de cette leçon, vous pourrez utiliser le débogueur pour :

* Chargement d’une autre bibliothèque de balises
* Validez que l’événement XDM côté client capture et envoie des données comme prévu à Platform Edge Network.
* Activer Edge Trace pour afficher les requêtes côté serveur envoyées par Platform Edge Network

## Conditions préalables

Vous connaissez les balises de collecte de données et le [site de démonstration Luma](https://luma.enablementadobe.com/content/luma/us/en.html){target="_blank"} et avez terminé les leçons précédentes du tutoriel :

* [Configurer un schéma XDM](configure-schemas.md)
* [Configuration d’un espace de noms d’identité](configure-identities.md)
* [Configurer un trains de données](configure-datastream.md)
* [Extension SDK Web installée dans la propriété de balise](install-web-sdk.md)
* [Création d’éléments de données](create-data-elements.md)
* [Création d’identités](create-identities.md)
* [Création de règles de balise](create-tag-rule.md)

## Chargement de bibliothèques de balises alternatives avec Debugger

Le débogueur Experience Platform dispose d’une fonctionnalité intéressante qui vous permet de remplacer une bibliothèque de balises existante par une autre. Cette technique est utile pour la validation et nous permet d’ignorer de nombreuses étapes d’implémentation dans ce tutoriel.

1. Assurez-vous que le [site web de démonstration Luma](https://luma.enablementadobe.com/content/luma/us/en.html){target="_blank"} est ouvert et sélectionnez l’icône de l’extension Debugger Experience Platform.
1. Le débogueur s’ouvre et affiche des détails sur l’implémentation codée en dur (vous devrez peut-être recharger le site Luma après avoir ouvert le débogueur).
1. Vérifiez que le débogueur est &quot;**[!UICONTROL Connecté à Luma]**&quot; comme illustré ci-dessous, puis sélectionnez l’icône &quot;**[!UICONTROL lock]**&quot; pour verrouiller le débogueur sur le site Luma.
1. Sélectionnez le bouton **[!UICONTROL Se connecter]** et connectez-vous à Adobe Experience Cloud à l’aide de votre identifiant d’Adobe.
1. Maintenant, accédez à **[!UICONTROL Balises Experience Platform]** dans le volet de navigation de gauche.

   ![Écran de balise Debugger ](assets/validate-launch-screen.png)

1. Sélectionnez l’onglet **[!UICONTROL Configuration]**
1. À droite de l’emplacement où vous voyez les **[!UICONTROL codes incorporés de page]**, ouvrez la liste déroulante **[!UICONTROL Actions]** et sélectionnez **[!UICONTROL Remplacer]**.

   ![ Sélectionner Actions > Remplacer](assets/validate-switch-environment.png)

1. Puisque vous êtes authentifié, le débogueur va extraire vos propriétés et environnements de balise disponibles. Sélectionner votre propriété
1. Sélectionner votre environnement `Development`
1. Sélectionnez le bouton **[!UICONTROL Appliquer]**

   ![Sélectionnez la propriété alternative de balise](assets/validate-switch-selection.png)

1. Le site web Luma va maintenant recharger _avec votre propre propriété de balise_.

   ![propriété de balise remplacée](assets/validate-switch-success.png)

Au fur et à mesure que vous continuez le tutoriel, vous utilisez cette technique pour mapper le site Luma sur votre propre propriété de balise afin de valider votre mise en oeuvre du SDK Web Platform. Lorsque vous utilisez des balises sur votre propre site web, vous pouvez utiliser cette même technique pour valider les bibliothèques de balises de développement sur votre site web de production.

## Validation des requêtes réseau côté client avec le débogueur Experience Platform

Vous pouvez utiliser le débogueur pour valider les balises côté client déclenchées à partir de votre mise en oeuvre du SDK Web Platform pour afficher les données envoyées à l’Edge Network Platform :

1. Accédez à **[!UICONTROL Summary]** dans le volet de navigation de gauche pour afficher les détails de votre propriété de balise.

   ![Onglet Résumé](assets/validate-summary.png)

1. Maintenant, accédez à **[!UICONTROL SDK Web Experience Platform]** dans le volet de navigation de gauche pour afficher les **[!UICONTROL requêtes réseau]**
1. Ouvrez la ligne **[!UICONTROL events]** .

   ![Demande de SDK Web Adobe Experience Platform](assets/validate-aep-screen.png)

1. Notez comment vous pouvez voir le type d’événement `web.webpagedetails.pageView` que vous avez spécifié dans votre action [!UICONTROL Mettre à jour la variable], ainsi que d’autres variables prêtes à l’emploi conformes au groupe de champs `AEP Web SDK ExperienceEvent`.

   ![Détails de l’événement](assets/validate-event-pageViews.png)

1. Faites défiler l’écran jusqu’à l’objet `web`, sélectionnez-le pour l’ouvrir et inspectez les `webPageDetails.name`, `webPageDetails.server` et `webPageDetails.siteSection`. Ils doivent correspondre aux variables de couche de données `digitalData` correspondantes sur la page d’accueil.

>[!TIP]
>
> Pour afficher et comparer la couche de données `digitalData` sur la page d’accueil :
>
> 1. Sur la page d’accueil de Luma, ouvrez les outils de développement du navigateur. Dans le cas de Chrome, sélectionnez le bouton `F12` sur votre clavier.
> 1. Sélectionnez l’onglet **[!UICONTROL Console]**
> 1. Saisissez `digitalData` et sélectionnez `Enter` sur votre clavier pour afficher les valeurs de couche de données.

![Onglet Réseau](assets/validate-xdm-content.png)

Vous pouvez également valider les détails de la carte des identités :

1. Connectez-vous au site Luma à l’aide des identifiants `test@adobe.com`/`test`

1. Revenez à la [page d’accueil de Luma](https://luma.enablementadobe.com/content/luma/us/en.html).

1. Ouvrez la section **[!UICONTROL SDK Web Experience Platform]** dans le volet de navigation de gauche.

   ![SDK Web dans Debugger](assets/identity-debugger-websdk-dark.png)

1. Sélectionnez la ligne **[!UICONTROL events]** pour ouvrir les détails dans une fenêtre contextuelle.

   ![SDK Web dans Debugger](assets/identity-deugger-websdk-event-dark.png)

1. Recherchez **identityMap** dans la fenêtre contextuelle. Ici, vous devriez voir `lumaCrmId` avec trois clés de authenticatedState, id et primary :
   ![SDK Web dans Debugger](assets/identity-deugger-websdk-event-lumaCrmId-dark.png)

### Validation des requêtes côté client à l’aide des outils de développement de navigateur

Ces types de détails de requête sont également visibles dans l’onglet des outils de développement web **Réseau** du navigateur (en supposant que le site web charge votre bibliothèque de balises).

1. Ouvrez l’onglet **Réseau** des outils de développement web du navigateur et rechargez la page. Filtrez les appels avec `/ee` pour localiser l’appel, sélectionnez-le, puis recherchez dans l’onglet **En-têtes** et l’onglet **Payload**.

   ![Onglet Réseau](assets/validate-dev-console.png)

1. Accédez à l’onglet **Réponse** et notez comment la valeur ECID est incluse dans la réponse.

   ![Onglet Réseau](assets/validate-dev-console-ecid.png)

   >[!NOTE]
   >
   > La valeur ECID est visible dans la réponse réseau. Il n’est pas inclus dans la partie `identityMap` de la requête réseau et il n’est pas stocké dans ce format dans un cookie.

## Validation des requêtes réseau côté serveur avec le débogueur Experience Platform

Comme vous l’avez appris dans la leçon [Configuration d’un flux de données](configure-datastream.md), le SDK Web Platform envoie d’abord des données de votre propriété numérique à l’Edge Network Platform. Ensuite, Platform Edge Network envoie des requêtes supplémentaires côté serveur aux services correspondants activés dans votre flux de données. Vous pouvez valider les requêtes côté serveur effectuées par l’Edge Network Platform à l’aide d’Edge Trace dans le débogueur.

<!--Furthermore, you can also validate the fully processed payload after it reaches an Adobe application by using [Adobe Experience Platform Assurance](https://experienceleague.adobe.com/en/docs/experience-platform/assurance/home). -->


### Activation d’Edge Trace

Pour activer Edge Trace :

1. Dans le volet de navigation de gauche de **[!UICONTROL Experience Platform Debugger]**, sélectionnez **[!UICONTROL Logs]**
1. Sélectionnez l’onglet **[!UICONTROL Edge]** et sélectionnez **[!UICONTROL Connect]**

   ![Connecter Edge Trace](assets/analytics-debugger-edgeTrace.png)

1. Il est vide pour l’instant.

   ![Edge Trace connectée](assets/analytics-debugger-edge-connected.png)

1. Actualisez la [page d’accueil Luma](https://luma.enablementadobe.com/) et vérifiez à nouveau **[!UICONTROL Débogueur Experience Platform]** pour voir les données passer.

   ![Balise Analytics Edge Trace](assets/validate-edge-trace.png)

À ce stade, vous ne pouvez pas afficher les requêtes de l’Edge Network Platform qui vont vers les applications Adobe, car vous n’en avez activé aucune dans le flux de données. Dans les leçons à venir, vous utiliserez Edge Trace pour afficher les requêtes sortantes côté serveur pour Adobe des applications et du transfert d’événement. Mais tout d’abord, découvrez un autre outil pour valider les requêtes côté serveur effectuées par l’Edge Network Platform—Adobe Experience Platform Assurance !

[Suivant : ](validate-with-assurance.md)

>[!NOTE]
>
>Merci d’avoir consacré du temps à l’apprentissage du SDK Web Adobe Experience Platform. Si vous avez des questions, souhaitez partager des commentaires généraux ou avez des suggestions sur le contenu à venir, partagez-les sur cet [post de discussion de la communauté Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996)
