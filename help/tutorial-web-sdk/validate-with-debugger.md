---
title: Valider les implémentations de Web SDK avec Experience Platform Debugger
description: Découvrez comment valider votre implémentation de Platform Web SDK avec Adobe Experience Platform Debugger. Cette leçon fait partie du tutoriel Implémentation d’Adobe Experience Cloud avec le SDK web.
feature: Web SDK,Tags,Debugger
jira: KT-15405
exl-id: 150bb1b1-4523-4b44-bd4e-6cabc468fc04
source-git-commit: 4e5fe50c1ec7a867fed57700b35851b859680fef
workflow-type: tm+mt
source-wordcount: '1471'
ht-degree: 2%

---

# Valider les implémentations de Web SDK avec Experience Platform Debugger

Découvrez comment valider votre implémentation du SDK web d’Adobe Experience Platform avec Adobe Experience Platform Debugger.


Experience Platform Debugger est une extension Chrome [&#128279;](https://chromewebstore.google.com/detail/adobe-experience-platform/bfnnokhpnncpkdmbokanobigaccjkpob) qui vous aide à voir la technologie Adobe mise en œuvre dans vos pages web. Experience Platform Debugger et la console de développement de votre navigateur sont les meilleurs moyens de valider et de déboguer les aspects côté navigateur de votre implémentation de Web SDK. Adobe Experience Platform Assurance, dont il sera question dans la leçon suivante, offre la meilleure vue des données lorsqu’elles entrent dans Platform Edge Network et en sortent.

![Diagramme de validation de Web SDK et Adobe Experience Platform](assets/dc-websdk-validation.png)


Si vous n’avez jamais utilisé Debugger auparavant, vous pouvez regarder cette vidéo de présentation de cinq minutes :

>[!VIDEO](https://video.tv.adobe.com/v/32156?learn=on&enablevpops)

Dans cette leçon, vous allez utiliser l’extension [Adobe Experience Platform Debugger](https://chromewebstore.google.com/detail/adobe-experience-platform/bfnnokhpnncpkdmbokanobigaccjkpob) pour remplacer la propriété de balise codée en dur sur le site de démonstration [Luma](https://luma.enablementadobe.com) par votre propre propriété.

Cette technique, appelée commutation d’environnement, s’avérera utile ultérieurement, lorsque vous utiliserez les balises sur votre propre site web. Il vous permet de charger votre site web de production dans votre navigateur, mais avec votre bibliothèque de balises *de développement*. Cette fonctionnalité vous permet d’effectuer et de valider en toute confiance les modifications de balises indépendamment de vos versions de code standard. Après tout, cette séparation entre les versions de balises marketing et les versions de code standard est l’une des principales raisons pour lesquelles les clients utilisent les balises.

## Objectifs d’apprentissage

À la fin de cette leçon, vous pourrez utiliser le débogueur pour :

* Chargement d’une autre bibliothèque de balises
* Vérifiez que l’événement XDM côté client capture et envoie les données comme prévu à Platform Edge Network.
* Activez Edge Trace pour afficher les requêtes côté serveur envoyées par Platform Edge Network.

## Conditions préalables

Vous connaissez les balises de la collecte de données et le site de démonstration [Luma](https://luma.enablementadobe.com/){target="_blank"} et avez terminé les leçons précédentes du tutoriel :

* [Configuration d’un schéma XDM](configure-schemas.md)
* [Configuration d’un espace de noms d’identité](configure-identities.md)
* [Configurer un trains de données](configure-datastream.md)
* [Extension Web SDK installée dans la propriété de balise](install-web-sdk.md)
* [Création d’éléments de données](create-data-elements.md)
* [Capturer des identités](create-identities.md)
* [Création de règles de balises](create-tag-rule.md)

## Chargement d’autres bibliothèques de balises avec Debugger

Experience Platform Debugger dispose d’une fonctionnalité pratique qui vous permet de remplacer une bibliothèque de balises existante par une autre. Cette technique est utile pour la validation et nous permet d’ignorer de nombreuses étapes d’implémentation dans ce tutoriel.

1. Assurez-vous que le site web de démonstration [Luma](https://luma.enablementadobe.com){target="_blank"} s’ouvre et sélectionnez l’icône de l’extension Experience Platform Debugger
1. Le débogueur s’ouvre et affiche certains détails de l’implémentation en codage en dur (vous devrez peut-être recharger le site Luma après l’ouverture du débogueur)
1. Vérifiez que le débogueur est « **[!UICONTROL connecté à Luma]** » comme illustré ci-dessous, puis sélectionnez l’icône « **[!UICONTROL verrouiller]** » pour le verrouiller sur le site Luma.
1. Sélectionnez le bouton **[!UICONTROL Se connecter]**, connectez-vous à Adobe Experience Cloud à l’aide de votre Adobe ID, puis sélectionnez votre organisation.

   >[!TIP]
   >
   > Si le débogueur affiche votre nom d’utilisateur au lieu de votre nom d’organisation après s’être connecté, déconnectez-vous et réessayez.


   ![Écran de balise du débogueur](assets/validate-launch-screen.png)

1. Accédez maintenant à **[!UICONTROL Experience Platform Tags]** dans le volet de navigation de gauche
1. Sélectionnez l’onglet **[!UICONTROL Configuration]**
1. À droite de l’emplacement où s’affiche le **[!UICONTROL Codes incorporés de la page]**, ouvrez le menu déroulant **[!UICONTROL Actions]** et sélectionnez **[!UICONTROL Remplacer]**

   ![Sélectionnez Actions > Remplacer](assets/validate-switch-environment.png)

1. Puisque vous êtes authentifié, le débogueur va extraire vos propriétés et environnements de balises disponibles. Sélectionnez votre propriété
1. Sélectionner votre environnement `Development`
   ![Sélectionnez la propriété de balise alternative](assets/validate-switch-selection.png)

   >[!TIP]
   >
   > Si vous ne parvenez pas à sélectionner votre propriété et votre environnement à l’aide des listes déroulantes, accédez plutôt à [!UICONTROL Balises] > [!UICONTROL Environnements] > [!UICONTROL Développement] > [!UICONTROL Installer] et sélectionnez l’icône pour copier le code incorporé et le coller dans le débogueur :
   > ![Sélectionnez la propriété de balise alternative](assets/validate-copy-embed-code.png)

1. Sélectionnez le bouton **[!UICONTROL Appliquer]**

1. Le site web Luma va maintenant se recharger _avec votre propre propriété de balise_.

   ![propriété de balise remplacée](assets/validate-switch-success.png)

Au fur et à mesure que vous poursuivez le tutoriel, vous utilisez cette technique de mappage du site Luma à votre propre propriété de balise pour valider votre implémentation de Platform Web SDK. Lors de l’utilisation de balises sur votre propre site web, vous pouvez utiliser cette même technique pour valider les bibliothèques de balises de développement sur votre site web de production.



## Validation avec Debugger

### Valider les requêtes réseau et XDM

Vous pouvez utiliser Debugger pour valider les balises côté client déclenchées à partir de votre implémentation de Platform Web SDK afin d’afficher les données envoyées à Platform Edge Network :

1. Accédez à **[!UICONTROL Résumé]** dans le volet de navigation de gauche pour afficher les détails de votre propriété de balise

   ![Onglet Résumé](assets/validate-summary.png)

1. Accédez maintenant à **[!UICONTROL Experience Platform Web SDK]** dans le volet de navigation de gauche pour afficher les **[!UICONTROL Demandes réseau]**
1. Ouvrez la ligne **[!UICONTROL events]**

   ![Requête Adobe Experience Platform Web SDK](assets/validate-aep-screen.png)

1. Notez comment vous pouvez voir le type d’événement `web.webPageDetails.pageView` que vous avez spécifié dans votre action [!UICONTROL Mettre à jour la variable] et d’autres variables prêtes à l’emploi appartenant au groupe de champs `AEP Web SDK ExperienceEvent`

   ![Détails de l’événement](assets/validate-event-pageViews.png)

1. Faites défiler l’écran jusqu’à l’objet `web`, sélectionnez pour l’ouvrir et inspecter le `webPageDetails.name`. Ils doivent correspondre aux variables de couche de données `adobeDataLayer` correspondantes sur la page d’accueil

>[!TIP]
>
> Pour afficher et comparer la couche de données `adobeDataLayer` sur la page d’accueil :
>
> 1. Sur la page d’accueil de Luma, ouvrez les outils de développement du navigateur. Dans le cas de Chrome, sélectionnez le bouton `F12` sur votre clavier
> 1. Sélectionnez l’onglet **[!UICONTROL Console]**
> 1. Saisissez `adobeDataLayer` et sélectionnez `Enter` sur le clavier pour afficher les valeurs de la couche de données

![Onglet Réseau](assets/validate-xdm-content.png)

Validez les événements et les variables définis sur les pages de produits, la page de panier et la page de confirmation de commande.

### Validation du mappage d’identités

Vous pouvez également valider les détails de la carte des identités :

1. Sélectionnez **[!DNL Sign In]** sur le site web [Luma](https://luma.enablementadobe.com/){target=_blank}. Sélectionnez **[!DNL Create Account]** et créez un compte à l’aide des informations d’identification `test@test.com`/`test`

1. Utilisez le raccourci **[!UICONTROL Aller au plus récent]** dans le débogueur pour accéder rapidement à l’événement Web SDK le plus récent (c’est la dernière colonne). Sélectionnez la ligne **[!UICONTROL événements]** pour ouvrir la boîte de dialogue modale des détails.

1. Recherchez le **identityMap** dans la boîte de dialogue modale. Vous devriez voir ici `lumaCrmId` avec trois clés d’authenticatedState, d’id et de désignation principale :
   ![Web SDK dans Debugger](assets/identity-deugger-websdk-event-lumaCrmId-dark.png)

## Validation à l’aide des outils de développement du navigateur

De nombreux développeurs web peuvent préférer afficher l’implémentation dans les outils de développement de leur navigateur. Ceci est particulièrement important, car tous les navigateurs ne prennent pas en charge l’extension Debugger. En outre, en raison du cadre flexible, vous pouvez examiner d’autres détails d’implémentation, tels que les cookies et les détails de réponse.

### Valider les requêtes réseau

Les détails de la requête Web SDK sont également visibles dans l’onglet **Réseau** des outils de développement web du navigateur (en supposant que le site web charge votre bibliothèque de balises).

1. Ouvrez l’onglet Outils de développement web **Réseau** du navigateur et rechargez la page. Filtrez les appels avec des `/ee` pour localiser l’appel, sélectionnez-le, puis recherchez les onglets **En-têtes** et **Payload**

   ![Onglet Réseau](assets/validate-dev-console.png)

1. Accédez à l’onglet **Aperçu** et notez comment la valeur ECID est incluse dans la réponse réseau.

   ![Onglet Réseau](assets/validate-dev-console-ecid.png)

   >[!NOTE]
   >
   > La valeur ECID est visible dans la réponse réseau. Il n’est pas inclus dans la partie `identityMap` de la requête réseau et n’est pas non plus stocké dans ce format dans un cookie.

### Cookies du SDK web

Pendant que nous sommes dans les outils de développement, jetons un coup d’œil à certains des ensembles de cookies de SDK web dans le navigateur. Ouvrez Application > Cookies > https://luma.enablementadobe.com .

Vous devriez voir plusieurs cookies définis par Web SDK :

* kndctr_[IMS_ORGID]_AdobeOrg_identity : stocke les données liées à l’ECID.
* kndctr_[IMS_ORGID]_AdobeOrg_cluster : stocke l’emplacement du centre de données utilisé pour que les appels réseau suivants soient acheminés vers les mêmes serveurs Edge
* AMCV_[IMS_ORGID]%40AdobeOrg : il s’agit de l’ancien cookie AMCV utilisé par les bibliothèques Experience Cloud SDK antérieures au Web. Il est défini, car nous avons laissé le paramètre par défaut **[!UICONTROL Migrer l’ECID vers l’API Visiteur vers le SDK Web]** sélectionné dans l’extension Balises de Adobe Experience Platform Web SDK. Il est important d’activer ce paramètre lorsque vous migrez vos pages depuis d’anciennes bibliothèques vers Web SDK, mais il peut être désactivé une fois toutes vos pages migrées pendant un certain temps.

![Onglet Cookies](assets/debugger-cookies.png)

Si vous effacez ces cookies et rechargez la page, vous remarquerez peut-être d’autres cookies tiers définis sur le domaine `.demdex.net`. Ces paramètres sont définis, car nous avons laissé le paramètre par défaut **[!UICONTROL Utiliser des cookies tiers]** : **[!UICONTROL Activé]** dans l’extension de balises Adobe Experience Platform Web SDK. Si votre navigateur n’autorise pas les cookies tiers, ils seront supprimés lorsque vous rechargez la page.

![Cookies Demdex](assets/debugger-demdex-cookies.png)


### Stockage local Luma

Le site web de démonstration Luma utilise uniquement des technologies côté client telles qu’HTML, CSS et JavaScript. Il n’existe aucun mécanisme de stockage principal, à l’exception de l’implémentation d’Experience Cloud utilisée par l’état par défaut du site web. Des informations telles que les détails du nom d’utilisateur sont simplement stockées localement dans votre navigateur à l’aide de localStorage. Ainsi, si vous supprimez ces informations ou utilisez une fenêtre d’analyseur, vous remarquerez que vous devrez peut-être recréer un compte utilisateur de test que vous avez créé précédemment.

![Stockage local](assets/debugger-local-storage.png)


Ensuite, découvrez comment valider ces requêtes réseau lorsqu’elles sont reçues et transmises à partir de Platform Edge Network à l’aide d’Adobe Experience Platform Assurance.

>[!NOTE]
>
>Merci d’avoir investi votre temps dans votre apprentissage de Adobe Experience Platform Web SDK. Si vous avez des questions, souhaitez partager des commentaires généraux ou avez des suggestions sur le contenu futur, veuillez les partager dans ce [article de discussion de la communauté Experience League](https://experienceleaguecommunities.adobe.com/adobe-experience-platform-18/tutorial-discussion-implement-adobe-experience-cloud-with-web-sdk-tutorial-248848?profile.language=fr)
