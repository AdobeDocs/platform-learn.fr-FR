---
title: Valider les implémentations de Web SDK avec Experience Platform Debugger
description: Découvrez comment valider votre implémentation de Platform Web SDK avec Adobe Experience Platform Debugger. Cette leçon fait partie du tutoriel Implémentation d’Adobe Experience Cloud avec le SDK web.
feature: Web SDK,Tags,Debugger
jira: KT-15405
exl-id: 150bb1b1-4523-4b44-bd4e-6cabc468fc04
source-git-commit: 7ccbaaf4db43921f07c971c485e1460a1a7f0334
workflow-type: tm+mt
source-wordcount: '1171'
ht-degree: 3%

---

# Valider les implémentations de Web SDK avec Experience Platform Debugger

Découvrez comment valider votre implémentation du SDK web d’Adobe Experience Platform avec Adobe Experience Platform Debugger.

Experience Platform Debugger est une extension disponible pour les navigateurs Chrome et Firefox, qui vous permet de voir la technologie Adobe mise en œuvre dans vos pages web. Téléchargez la version correspondant au navigateur de votre choix :

* [Extension Firefox ](https://addons.mozilla.org/fr/firefox/addon/adobe-experience-platform-dbg/)
* [Extension Chrome](https://chromewebstore.google.com/detail/adobe-experience-platform/bfnnokhpnncpkdmbokanobigaccjkpob)

Si vous n’avez jamais utilisé le débogueur auparavant, vous pouvez regarder cette vidéo de présentation de cinq minutes :

>[!VIDEO](https://video.tv.adobe.com/v/32156?learn=on&enablevpops)

Dans cette leçon, vous allez utiliser l’extension [Adobe Experience Platform Debugger](https://chromewebstore.google.com/detail/adobe-experience-platform/bfnnokhpnncpkdmbokanobigaccjkpob) pour remplacer la propriété de balise codée en dur sur le site de démonstration [Luma](https://luma.enablementadobe.com/content/luma/us/en.html) par votre propre propriété.

Cette technique, appelée commutation d’environnement, s’avérera utile ultérieurement, lorsque vous utiliserez les balises sur votre propre site web. Il vous permet de charger votre site web de production dans votre navigateur, mais avec votre bibliothèque de balises *de développement*. Cette fonctionnalité vous permet d’effectuer et de valider en toute confiance les modifications de balises indépendamment de vos versions de code standard. Après tout, cette séparation entre les versions de balises marketing et les versions de code standard est l’une des principales raisons pour lesquelles les clients utilisent les balises.

## Objectifs d’apprentissage

À la fin de cette leçon, vous pourrez utiliser le débogueur pour :

* Chargement d’une autre bibliothèque de balises
* Vérifiez que l’événement XDM côté client capture et envoie les données comme prévu à Platform Edge Network.
* Activez Edge Trace pour afficher les requêtes côté serveur envoyées par Platform Edge Network.

## Conditions préalables

Vous connaissez les balises de la collecte de données et le site de démonstration [Luma](https://luma.enablementadobe.com/content/luma/us/en.html){target="_blank"} et avez terminé les leçons précédentes du tutoriel :

* [Configuration d’un schéma XDM](configure-schemas.md)
* [Configuration d’un espace de noms d’identité](configure-identities.md)
* [Configurer un trains de données](configure-datastream.md)
* [Extension Web SDK installée dans la propriété de balise](install-web-sdk.md)
* [Création d’éléments de données](create-data-elements.md)
* [Création d’identités](create-identities.md)
* [Création de règles de balises](create-tag-rule.md)

## Chargement d’autres bibliothèques de balises avec Debugger

Experience Platform Debugger dispose d’une fonctionnalité pratique qui vous permet de remplacer une bibliothèque de balises existante par une autre. Cette technique est utile pour la validation et nous permet d’ignorer de nombreuses étapes d’implémentation dans ce tutoriel.

1. Assurez-vous que le site web de démonstration [Luma](https://luma.enablementadobe.com/content/luma/us/en.html){target="_blank"} s’ouvre et sélectionnez l’icône de l’extension Experience Platform Debugger
1. Le débogueur s’ouvre et affiche certains détails de l’implémentation en codage en dur (vous devrez peut-être recharger le site Luma après l’ouverture du débogueur)
1. Vérifiez que le débogueur est « **[!UICONTROL connecté à Luma]** » comme illustré ci-dessous, puis sélectionnez l’icône « **[!UICONTROL verrouiller]** » pour le verrouiller sur le site Luma.
1. Sélectionnez le bouton **[!UICONTROL Se connecter]** et connectez-vous à Adobe Experience Cloud à l’aide de votre Adobe Id.
1. Accédez maintenant à **[!UICONTROL Experience Platform Tags]** dans le volet de navigation de gauche

   ![Écran de balise du débogueur](assets/validate-launch-screen.png)

1. Sélectionnez l’onglet **[!UICONTROL Configuration]**
1. À droite de l’emplacement où s’affiche le **[!UICONTROL Codes incorporés de la page]**, ouvrez le menu déroulant **[!UICONTROL Actions]** et sélectionnez **[!UICONTROL Remplacer]**

   ![Sélectionnez Actions > Remplacer](assets/validate-switch-environment.png)

1. Puisque vous êtes authentifié, le débogueur va extraire vos propriétés et environnements de balises disponibles. Sélectionnez votre propriété
1. Sélectionner votre environnement `Development`
1. Sélectionnez le bouton **[!UICONTROL Appliquer]**

   ![Sélectionnez la propriété de balise alternative](assets/validate-switch-selection.png)

1. Le site web Luma va maintenant se recharger _avec votre propre propriété de balise_.

   ![propriété de balise remplacée](assets/validate-switch-success.png)

Au fur et à mesure que vous poursuivez le tutoriel, vous utilisez cette technique de mappage du site Luma à votre propre propriété de balise pour valider votre implémentation de Platform Web SDK. Lors de l’utilisation de balises sur votre propre site web, vous pouvez utiliser cette même technique pour valider les bibliothèques de balises de développement sur votre site web de production.

## Valider les requêtes réseau côté client avec Experience Platform Debugger

Vous pouvez utiliser Debugger pour valider les balises côté client déclenchées à partir de votre implémentation de Platform Web SDK afin d’afficher les données envoyées à Platform Edge Network :

1. Accédez à **[!UICONTROL Résumé]** dans le volet de navigation de gauche pour afficher les détails de votre propriété de balise

   ![Onglet Résumé](assets/validate-summary.png)

1. Accédez maintenant à **[!UICONTROL Experience Platform Web SDK]** dans le volet de navigation de gauche pour afficher les **[!UICONTROL Demandes réseau]**
1. Ouvrez la ligne **[!UICONTROL events]**

   ![Requête Adobe Experience Platform Web SDK](assets/validate-aep-screen.png)

1. Notez comment vous pouvez voir le type d’événement `web.webpagedetails.pageView` que vous avez spécifié dans votre action [!UICONTROL Mettre à jour la variable] et d’autres variables prêtes à l’emploi appartenant au groupe de champs `AEP Web SDK ExperienceEvent`

   ![Détails de l’événement](assets/validate-event-pageViews.png)

1. Faites défiler l’écran jusqu’à l’objet `web`, sélectionnez-le pour l’ouvrir et inspecter les `webPageDetails.name`, `webPageDetails.server` et `webPageDetails.siteSection`. Ils doivent correspondre aux variables de couche de données `digitalData` correspondantes sur la page d’accueil

>[!TIP]
>
> Pour afficher et comparer la couche de données `digitalData` sur la page d’accueil :
>
> 1. Sur la page d’accueil de Luma, ouvrez les outils de développement du navigateur. Dans le cas de Chrome, sélectionnez le bouton `F12` sur votre clavier
> 1. Sélectionnez l’onglet **[!UICONTROL Console]**
> 1. Saisissez `digitalData` et sélectionnez `Enter` sur le clavier pour afficher les valeurs de la couche de données

![Onglet Réseau](assets/validate-xdm-content.png)

Vous pouvez également valider les détails de la carte des identités :

1. Connectez-vous au site Luma à l’aide des informations d’identification `test@test.com`/`test`

1. Revenez à la [page d’accueil de Luma](https://luma.enablementadobe.com/content/luma/us/en.html).

1. Ouvrez la section **[!UICONTROL Experience Platform Web SDK]** dans le volet de navigation de gauche

   ![Web SDK dans Debugger](assets/identity-debugger-websdk-dark.png)

1. Sélectionnez la ligne **[!UICONTROL événements]** pour ouvrir les détails dans un pop-up

   ![Web SDK dans Debugger](assets/identity-deugger-websdk-event-dark.png)

1. Recherchez le **identityMap** dans le pop-up. Vous devriez voir ici `lumaCrmId` avec trois clés authenticatedState, id et primary :
   ![Web SDK dans Debugger](assets/identity-deugger-websdk-event-lumaCrmId-dark.png)

### Valider les requêtes côté client avec les outils de développement du navigateur

Ces types de détails de requête sont également visibles dans l’onglet Outils de développement web **Réseau** du navigateur (en supposant que le site web charge votre bibliothèque de balises).

1. Ouvrez l’onglet Outils de développement web **Réseau** du navigateur et rechargez la page. Filtrez les appels avec des `/ee` pour localiser l’appel, sélectionnez-le, puis recherchez les onglets **En-têtes** et **Payload**

   ![Onglet Réseau](assets/validate-dev-console.png)

1. Accédez à l’onglet **Réponse** et notez comment la valeur ECID est incluse dans la réponse.

   ![Onglet Réseau](assets/validate-dev-console-ecid.png)

   >[!NOTE]
   >
   > La valeur ECID est visible dans la réponse réseau. Il n’est pas inclus dans la partie `identityMap` de la requête réseau et n’est pas non plus stocké dans ce format dans un cookie.

## Valider les requêtes réseau côté serveur avec Experience Platform Debugger

Comme vous l’avez appris dans la leçon [Configurer un flux de données](configure-datastream.md), Platform Web SDK envoie d’abord les données de votre propriété numérique vers Platform Edge Network. Ensuite, Platform Edge Network effectue des requêtes côté serveur supplémentaires vers les services correspondants activés dans votre flux de données. Vous pouvez valider les requêtes côté serveur effectuées par Platform Edge Network à l’aide d’Edge Trace dans le débogueur.

<!--Furthermore, you can also validate the fully processed payload after it reaches an Adobe application by using [Adobe Experience Platform Assurance](https://experienceleague.adobe.com/fr/docs/experience-platform/assurance/home). -->


### Activer Edge Trace

Pour activer Edge Trace :

1. Dans le volet de navigation de gauche de **[!UICONTROL Experience Platform Debugger]** sélectionnez **[!UICONTROL Journaux]**
1. Sélectionnez l’onglet **[!UICONTROL Edge]**, puis sélectionnez **[!UICONTROL Se connecter]**

   ![Connexion à Edge Trace](assets/analytics-debugger-edgeTrace.png)

1. Il est vide pour l&#39;instant

   ![Edge Trace connectée](assets/analytics-debugger-edge-connected.png)

1. Actualisez la page d’accueil [Luma](https://luma.enablementadobe.com/) et vérifiez à nouveau **[!UICONTROL Experience Platform Debugger]** pour voir les données passer.

   ![Balise Analytics Edge Trace](assets/validate-edge-trace.png)

À ce stade, vous ne pouvez pas afficher de requêtes Platform Edge Network destinées aux applications Adobe, car vous n’en avez activé aucune dans le flux de données. Dans les leçons ultérieures, vous utiliserez Edge Trace pour afficher les requêtes côté serveur sortantes pour les applications Adobe et le transfert d’événement. Mais d’abord, découvrez un autre outil permettant de valider les requêtes côté serveur effectuées par Platform Edge Network : Adobe Experience Platform Assurance !

>[!NOTE]
>
>Merci d’avoir investi votre temps dans votre apprentissage de Adobe Experience Platform Web SDK. Si vous avez des questions, souhaitez partager des commentaires généraux ou avez des suggestions sur le contenu futur, veuillez les partager dans ce [article de discussion de la communauté Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996?profile.language=fr)
