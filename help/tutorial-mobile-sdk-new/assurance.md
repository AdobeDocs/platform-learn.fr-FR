---
title: Configuration d’Assurance
description: Découvrez comment mettre en oeuvre l’extension Assurance dans une application mobile.
feature: Mobile SDK,Assurance
hide: true
source-git-commit: a2788110b1c43d24022672bb5ba0f36af66d962b
workflow-type: tm+mt
source-wordcount: '776'
ht-degree: 4%

---

# Configuration d’Assurance

Découvrez comment configurer Adobe Experience Platform Assurance dans une application mobile.

L’assurance, officiellement appelée Projet Griffon, est conçue pour vous aider à inspecter, tester, simuler et valider la manière dont vous collectez des données ou diffusez des expériences dans votre application mobile.

Assurance vous aide à inspecter les événements SDK bruts générés par le SDK Mobile Adobe Experience Platform. Tous les événements collectés par le SDK sont disponibles pour inspection. Les événements du SDK sont chargés en mode Liste, triés par heure. Chaque événement dispose d’une vue détaillée qui fournit des détails supplémentaires. Des vues supplémentaires sur la configuration du SDK, les éléments de données, les états partagés et les versions de l’extension du SDK sont également fournies. En savoir plus sur les [Assurance](https://experienceleague.adobe.com/docs/experience-platform/assurance/home.html?lang=fr) dans la documentation du produit.


## Conditions préalables

* Configuration réussie de l’application avec les SDK installés et configurés.

## Objectifs d&#39;apprentissage

Dans cette leçon, vous allez :

* Vérifiez que votre entreprise a accès à (et demandez-le si vous ne le faites pas).
* Configurez votre URL de base.
* Ajoutez le code spécifique à iOS requis.
* Connectez-vous à une session.

## Confirmer l’accès

Vérifiez que votre entreprise a accès à Assurance. En tant qu’utilisateur, vous devez être ajouté au profil pour Adobe Experience Platform. Voir [Accès utilisateur](https://experienceleague.adobe.com/docs/experience-platform/assurance/user-access.html?lang=en) pour plus d’informations.

## Implémenter

En plus du [Installation du SDK](install-sdks.md), que vous avez terminé dans la leçon précédente, iOS requiert également l’ajout suivant pour démarrer la session d’assurance pour votre application.

1. Accédez à **[!DNL Luma]** > **[!DNL Luma]** > **[!UICONTROL SceneDelegate]** dans le navigateur de projet de votre code.

1. Ajoutez le code suivant à `func scene(_ scene: UIScene, openURLContexts URLContexts: Set<UIOpenURLContext>` :

   ```swift
   // Called when the app in background is opened with a deep link.
   if let deepLinkURL = URLContexts.first?.url {
       // Start the Assurance session
       Assurance.startSession(url: deepLinkURL)
   }
   ```

   Ce code lance une session d’assurance lorsque l’application est en arrière-plan et s’ouvre à l’aide d’un lien profond.

Vous trouverez plus d’informations [ici](https://developer.adobe.com/client-sdks/documentation/platform-assurance-sdk/api-reference/){target="_blank"}.

## Signature

Avant d’exécuter l’application pour la première fois dans Xcode, veillez à mettre à jour la signature.

1. Ouvrez le projet  dans Xcode.
1. Sélectionner **[!DNL Luma]** dans le navigateur de projet.
1. Sélectionnez la variable **[!DNL Luma]** cible.
1. Sélectionnez la variable **Signature et fonctionnalités** .
1. Configurer **[!UICONTROL Gestion automatique de la signature]**, **[!UICONTROL Équipe]**, et **[!UICONTROL Identifiant du lot]** ou utilisez les détails de mise en service du développement Apple spécifiques.

   >[!IMPORTANT]
   >
   >Veillez à sélectionner un identifiant de lot unique différent de celui par défaut déjà saisi dans le projet de démarrage, car chaque identifiant de lot doit être unique.


   ![Fonctionnalités de signature Xcode](assets/xcode-signing-capabilities.png){zoomable=&quot;yes&quot;}

## Configuration d’une URL de base

1. Accédez à votre projet dans Xcode.
1. Sélectionner **[!DNL Luma]** dans le navigateur de projet.
1. Sélectionnez la variable **[!DNL Luma]** cible.
1. Sélectionnez la variable **Infos** .
1. Pour ajouter une URL de base, faites défiler l’écran jusqu’à **Types d’URL** et sélectionnez la variable **+** bouton .
1. Définir **Identifiant** à l’identifiant du lot que vous avez configuré dans [Signature](#signing) (par exemple `com.adobe.luma.tutorial.swiftui`) et définissez une **Modèles d’URL**, par exemple `lumatutorialswiftui`.

   ![url d&#39;assurance](assets/assurance-url-type.png)

Pour en savoir plus sur les schémas d’URL dans iOS, consultez [Documentation Apple](https://developer.apple.com/documentation/xcode/defining-a-custom-url-scheme-for-your-app){target="_blank"}.

L’assurance fonctionne en ouvrant une URL, que ce soit par navigateur ou par code QR. Cette URL commence par l’URL de base qui ouvre l’application et contient des paramètres supplémentaires. Ces paramètres uniques sont utilisés pour connecter la session.


## Connexion à une session

1. Exécutez l’application dans le simulateur ou sur un appareil physique connecté.
1. Sélectionner **[!UICONTROL Assurance]** dans le rail de gauche de l’interface utilisateur de la collecte de données.
1. Sélectionner **[!UICONTROL Créer une session]**.
1. Sélectionner **[!UICONTROL Début]**.
1. Fournissez une **[!UICONTROL Nom de session]** par exemple `Luma Mobile App Session` et la variable **[!UICONTROL URL de base]**, qui est un schéma d’URL que vous avez saisi dans Xcode, suivi de `://` Par exemple : `lumatutorialswiftui://`
1. Sélectionnez **[!UICONTROL Suivant]**.
   ![création d’une session d’assurance](assets/assurance-create-session.png)
1. Dans le **[!UICONTROL Créer une session]** boîte de dialogue modale :

   Si vous utilisez un appareil physique :

   * Sélectionner **[!UICONTROL Analyser le code QR]**. Utilisez votre appareil photo sur votre appareil physique pour analyser le code QR et appuyez sur le lien pour ouvrir l’application.

     ![code qa d’assurance](assets/assurance-qr-code.png)

   Si vous utilisez un simulateur :

   1. Sélectionner **[!UICONTROL Copier le lien]**.
   1. Copiez le lien profond à l’aide de ![Copier](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Copy_18_N.svg)  et utilisez le lien profond pour ouvrir l’application avec Safari dans le simulateur.
      ![Lien de copie d’assurance](assets/assurance-copy-link.png)

1. Au chargement de l’application, une boîte de dialogue modale vous demande de saisir le code PIN affiché à l’étape 7.

   <img src="assets/assurance-enter-pin.png" width="300">

   Saisissez le code PIN et sélectionnez **[!UICONTROL Connexion]**.


1. Si la connexion a réussi, vous voyez :
   * Une icône Assurance qui flotte au-dessus de votre application.

     <img src="assets/assurance-modal.png" width="300">

   * Mises à jour Experience Cloud effectuées dans l’interface utilisateur d’Assurance, indiquant :

      1. Événements d’expérience provenant de l’application.
      1. Détails d’un événement sélectionné.
      1. L’appareil et la chronologie.

         ![événements d’assurance](assets/assurance-events.png)

Si vous rencontrez des défis, veuillez consulter la section [technique](https://developer.adobe.com/client-sdks/documentation/platform-assurance-sdk/){target="_blank"} and [general documentation](https://experienceleague.adobe.com/docs/experience-platform/assurance/home.html?lang=fr){target="_blank"}.

>[!SUCCESS]
>
>Vous avez maintenant configuré votre application pour utiliser Assurance pour le reste du tutoriel.<br/>Merci d’investir votre temps à apprendre sur le SDK Adobe Experience Platform Mobile. Si vous avez des questions, souhaitez partager des commentaires généraux ou avez des suggestions sur le contenu futur, partagez-les à ce sujet. [Article de discussion de la communauté Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796)


Suivant : **[Consentement](consent.md)**
