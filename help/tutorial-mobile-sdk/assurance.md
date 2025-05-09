---
title: Configuration d’Assurance pour les mises en oeuvre du SDK Mobile Platform
description: Découvrez comment mettre en oeuvre l’extension Assurance dans une application mobile.
feature: Mobile SDK,Assurance
jira: KT-14628
exl-id: e15774b2-2f52-400f-9313-bb4338a88918
source-git-commit: 576f85eda6e5888b9eafa15a705a99c3a70fed07
workflow-type: tm+mt
source-wordcount: '1022'
ht-degree: 1%

---

# Configuration d’Assurance

Découvrez comment configurer Adobe Experience Platform Assurance dans une application mobile.

L’assurance, officiellement appelée Projet Griffon, est conçue pour vous aider à inspecter, tester, simuler et valider la manière dont vous collectez des données ou diffusez des expériences dans votre application mobile.

Assurance vous aide à inspecter les événements SDK bruts générés par le SDK Mobile Adobe Experience Platform. Tous les événements collectés par le SDK sont disponibles pour inspection. Les événements du SDK sont chargés en mode Liste, triés par heure. Chaque événement dispose d’une vue détaillée qui fournit des détails supplémentaires. Des vues supplémentaires sur la configuration du SDK, les éléments de données, les états partagés et les versions de l’extension du SDK sont également fournies. Pour en savoir plus sur [Assurance](https://experienceleague.adobe.com/docs/experience-platform/assurance/home.html?lang=fr) dans la documentation du produit.


## Conditions préalables

* Configuration réussie de l’application avec les SDK installés et configurés.

## Objectifs d&#39;apprentissage

Dans cette leçon, vous allez :

* Vérifiez que votre entreprise a accès à (et demandez-le si vous ne le faites pas).
* Configurez votre URL de base.
* Ajoutez le code spécifique à iOS requis.
* Connectez-vous à une session.

## Confirmer l’accès

Vérifiez que votre entreprise a accès à Assurance. En tant qu’utilisateur, vous devez être ajouté au profil pour Adobe Experience Platform. Pour plus d’informations, voir [Accès des utilisateurs](https://experienceleague.adobe.com/docs/experience-platform/assurance/user-access.html?lang=fr) dans le guide d’assurance.

## Implémenter

Outre l’ [ installation générale du SDK](install-sdks.md), que vous avez terminée dans la leçon précédente, iOS requiert également l’ajout suivant pour démarrer la session d’assurance pour votre application.

1. Accédez à **[!DNL Luma]** > **[!DNL Luma]** > **[!UICONTROL SceneDelegate]** dans le navigateur de projet Xcode.

1. Ajoutez le code suivant à `func scene(_ scene: UIScene, openURLContexts URLContexts: Set<UIOpenURLContext>` :

   ```swift
   // Called when the app in background is opened with a deep link.
   if let deepLinkURL = URLContexts.first?.url {
       // Start the Assurance session
       Assurance.startSession(url: deepLinkURL)
   }
   ```

   Ce code lance une session d’assurance lorsque l’application est en arrière-plan et ouverte à l’aide d’un lien profond.

Vous trouverez plus d&#39;informations [ici](https://developer.adobe.com/client-sdks/documentation/platform-assurance-sdk/api-reference/){target="_blank"}.



## Définition de l’identifiant de lot

Vous devez fournir un identifiant de lot unique pour votre application.

1. Ouvrez le projet dans Xcode.
1. Sélectionnez **[!DNL Luma]** dans le navigateur de projet.
1. Sélectionnez la cible **[!DNL Luma]**.
1. Sélectionnez l’onglet **Signing &amp; Capabilities** .
1. Définissez un **[!UICONTROL identifiant de lot]**.

   >[!IMPORTANT]
   >
   >Assurez-vous d’utiliser un identifiant de lot _unique_ et remplacez l’identifiant de lot `com.adobe.luma.tutorial.swiftui`, car chaque identifiant de lot doit être unique. En règle générale, vous utilisez un format DNS inversé pour les chaînes d’ID de lot, comme `com.organization.brand.uniqueidentifier`. La version terminée de ce tutoriel, par exemple, utilise `com.adobe.luma.tutorial.swiftui`.


   ![Fonctionnalités de signature Xcode](assets/xcode-signing-capabilities.png){zoomable="yes"}


## Configuration d’une URL de base

1. Accédez à votre projet dans Xcode.
1. Sélectionnez **[!DNL Luma]** dans le navigateur de projet.
1. Sélectionnez la cible **[!DNL Luma]**.
1. Sélectionnez l’onglet **Info** .
1. Pour ajouter une URL de base, faites défiler l’écran jusqu’à **Types d’URL** et sélectionnez le bouton **+** .
1. Définissez **Identifiant** sur l’identifiant de lot de votre choix et définissez un **schéma d’URL** de votre choix.

   ![url d&#39;assurance](assets/assurance-url-type.png)

   >[!IMPORTANT]
   >
   >Assurez-vous d’utiliser un identifiant de lot _unique_ et remplacez l’identifiant de lot `com.adobe.luma.tutorial.swiftui`, car chaque identifiant de lot doit être unique. En règle générale, vous utilisez un format DNS inversé pour les chaînes d’ID de lot, comme `com.organization.brand.uniqueidentifier`. Vous pouvez utiliser le même identifiant de lot que celui utilisé à l’emplacement [Définissez l’identifiant de lot](#define-bundle-identifier).<br/>De même, utilisez un modèle d’URL unique et remplacez le `lumatutorialswiftui` déjà fourni par votre modèle d’URL unique.

Pour en savoir plus sur les schémas d’URL dans iOS, consultez la [documentation Apple](https://developer.apple.com/documentation/xcode/defining-a-custom-url-scheme-for-your-app){target="_blank"}.

L’assurance fonctionne en ouvrant une URL, que ce soit par navigateur ou par code QR. Cette URL commence par l’URL de base qui ouvre l’application et contient des paramètres supplémentaires. Ces paramètres uniques sont utilisés pour connecter la session.


## Connexion à une session

Dans Xcode :

1. Créez ou recréez et exécutez l’application dans le simulateur ou sur un appareil physique à partir de Xcode, en utilisant ![Play](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Play_18_N.svg).

   >[!TIP]
   >
   >Si vous le souhaitez, vous pouvez &quot;nettoyer&quot; votre version, en particulier lorsque des résultats inattendus s’affichent. Pour ce faire, sélectionnez **[!UICONTROL Nettoyer le dossier de génération...]** dans le menu Xcode **[!UICONTROL Product]** .


1. Dans la boîte de dialogue **[!UICONTROL Autoriser &quot;Luma App&quot; à utiliser votre emplacement]**, sélectionnez **[!UICONTROL Autoriser lors de l’utilisation de l’application]**.

   <img src="assets/geolocation-permissions.png" width="300">

1. Dans la boîte de dialogue **[!UICONTROL &quot;Luma App&quot; Vouloir vous envoyer des notifications]**, sélectionnez **[!UICONTROL Autoriser]**.

   <img src="assets/notification-permissions.png" width="300">

1. Sélectionnez **[!UICONTROL Continuer...]** pour permettre à l’application de suivre votre activité.

   <img src="assets/tracking-continue.png" width="300">

1. Dans la boîte de dialogue **[!UICONTROL Autoriser &quot;l’application Luma&quot; à suivre votre activité sur les applications et sites web d’autres entreprises]**, sélectionnez **[!UICONTROL Autoriser]**.

   <img src="assets/tracking-allow.png" width="300">


Dans votre navigateur :

1. Accédez à l’interface utilisateur de la collecte de données.
1. Sélectionnez **[!UICONTROL Assurance]** dans le rail de gauche.
1. Sélectionnez **[!UICONTROL Créer une session]**.
1. Sélectionnez **[!UICONTROL Démarrer]**.
1. Fournissez un **[!UICONTROL nom de session]** tel que `Luma Mobile App Session` et l’ **[!UICONTROL URL de base]**, qui correspond aux schémas d’URL que vous avez saisis dans Xcode, suivi de `://` Par exemple : `lumatutorialswiftui://`
1. Sélectionnez **[!UICONTROL Suivant]**.
   ![assurance créer une session](assets/assurance-create-session.png)
1. Dans la boîte de dialogue modale **[!UICONTROL Créer une session]** :

   Si vous utilisez un appareil physique :

   * Sélectionnez **[!UICONTROL Analyser le code QR]**. Pour ouvrir l’application, utilisez l’appareil photo de votre appareil physique pour analyser le code QR et appuyez sur le lien.

     ![assurance qa code](assets/assurance-qr-code.png)

   Si vous utilisez un simulateur :

   1. Sélectionnez **[!UICONTROL Copier le lien]**.
   1. Copiez le lien profond à l’aide de ![Copier](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Copy_18_N.svg) et utilisez le lien profond pour ouvrir l’application avec Safari dans le simulateur.

      ![Lien de copie d’assurance](assets/assurance-copy-link.png)

1. Au chargement de l’application, une boîte de dialogue modale vous demande de saisir le code PIN affiché à l’étape 7.

   <img src="assets/assurance-enter-pin.png" width="300">

   Saisissez le code PIN et sélectionnez **[!UICONTROL Se connecter]**.


1. Si la connexion a réussi, vous voyez :
   * Une icône Assurance qui flotte au-dessus de votre application.

     <img src="assets/assurance-modal.png" width="300">

   * Mises à jour Experience Cloud effectuées dans l’interface utilisateur d’Assurance, indiquant :

      1. Événements d’expérience provenant de l’application.
      1. Détails d’un événement sélectionné.
      1. L’appareil et la chronologie.

         ![événements d’assurance](assets/assurance-events.png)

Si vous rencontrez des problèmes, consultez la [documentation technique](https://developer.adobe.com/client-sdks/documentation/platform-assurance-sdk/){target="_blank"} et la [documentation générale](https://experienceleague.adobe.com/docs/experience-platform/assurance/home.html?lang=fr){target="_blank"}.


## Vérifier les extensions

Pour vérifier si votre application utilise les extensions les plus récentes :

1. Sélectionnez **[!UICONTROL Configurer]**.

1. Sélectionnez ![Ajouter](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) pour ![123](https://spectrum.adobe.com/static/icons/workflow_18/Smock_123_18_N.svg) **[!UICONTROL Extension Versions]**.

1. Sélectionnez **[!UICONTROL Enregistrer]**.

   ![Configurer des versions d’extension](assets/assurance-configure-extension-versions.png)

1. Sélectionnez ![123](https://spectrum.adobe.com/static/icons/workflow_18/Smock_123_18_N.svg) **[!UICONTROL Extension Versions]** pour afficher un aperçu des dernières extensions disponibles et des extensions utilisées dans votre version de l’application.

   ![Versions d’extension](assets/assurance-extension-versions.png)

1. Pour mettre à jour vos versions d’extension (par exemple, **[!UICONTROL Messaging]** et **[!UICONTROL Optimize]**), sélectionnez le module (extension) dans **[!UICONTROL Package Dependencies]** (par exemple, **[!UICONTROL AEPMessaging]**) et dans le menu contextuel, sélectionnez **[!UICONTROL Update Package]**. Xcode met à jour les dépendances du package.


>[!NOTE]
>
>Une fois que vous avez mis à jour vos extensions (packages) dans Xcode, fermez et supprimez votre session actuelle, puis répétez toutes les étapes depuis [Connexion à une session](#connecting-to-a-session) et [Vérifier les extensions](#verify-extensions) pour vous assurer qu’Assurance signale correctement les extensions correctes dans une nouvelle session d’assurance.





>[!SUCCESS]
>
>Vous avez maintenant configuré votre application pour utiliser Assurance pour le reste du tutoriel.
>
>Merci d’investir votre temps à apprendre sur le SDK Adobe Experience Platform Mobile. Si vous avez des questions, souhaitez partager des commentaires généraux ou avez des suggestions sur le contenu à venir, partagez-les sur cet [post de discussion de la communauté Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796?profile.language=fr)


Suivant : **[Implémentation du consentement](consent.md)**
