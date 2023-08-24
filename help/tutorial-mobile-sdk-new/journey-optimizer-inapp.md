---
title: Messagerie in-app Adobe Journey Optimizer
description: Découvrez comment créer des messages in-app vers une application mobile avec le SDK Mobile Platform et Adobe Journey Optimizer.
solution: Data Collection,Journey Optimizer
feature-set: Journey Optimizer
hide: true
source-git-commit: c3c12d63762f439faa9c45d27e66468455774b43
workflow-type: tm+mt
source-wordcount: '994'
ht-degree: 3%

---

# Messagerie in-app Adobe Journey Optimizer

Découvrez comment créer des messages in-app pour les applications mobiles avec le SDK Mobile Platform et Adobe Journey Optimizer.

Journey Optimizer vous permet de créer vos parcours et d’envoyer des messages in-app aux audiences ciblées. Avant d’envoyer des messages in-app avec Journey Optimizer, vous devez vous assurer que les configurations et intégrations appropriées sont en place. Pour comprendre le flux de données de la messagerie in-app dans Adobe Journey Optimizer, reportez-vous à la section [la documentation](https://experienceleague.adobe.com/docs/journey-optimizer/using/in-app/inapp-configuration.html?lang=en).

>[!NOTE]
>
>Cette leçon est facultative et s’applique uniquement aux utilisateurs de Adobe Journey Optimizer qui souhaitent envoyer des messages in-app.


## Conditions préalables

* Création et exécution de l’application avec les SDK installés et configurés.
* Accès à Adobe Journey Optimizer et autorisations suffisantes, comme décrit [here](https://experienceleague.adobe.com/docs/journey-optimizer/using/configuration/configuration-message/push-config/push-configuration.html?lang=en). Vous avez également besoin d’autorisations suffisantes pour les fonctionnalités Adobe Journey Optimizer suivantes.
   * Créer une campagne.
* Compte de développeur Apple payant disposant d’un accès suffisant pour créer des certificats, identifiants et clés.
* Appareil ou simulateur iOS physique à tester.
* [Identifiant d’application enregistré avec APN](journey-optimizer-push.md#register-app-id-with-apn)
* [Ajout des informations d’identification push de votre application dans Data Collection](journey-optimizer-push.md#add-your-app-push-credentials-in-data-collection)
* [Extension des balises Adobe Journey Optimizer installées](journey-optimizer-push.md#install-adobe-journey-optimizer-tags-extension)
* [Mise en oeuvre de Adobe Journey Optimizer dans l’application](journey-optimizer-push.md#implement-adobe-journey-optimizer-in-the-app)


## Validation avec Assurance

1. Consultez la section [instructions de configuration](assurance.md) .
1. Installez l’application sur votre appareil physique ou sur le simulateur.
1. Lancez l’application à l’aide de l’URL générée par Assurance.
1. Dans l’interface utilisateur d’assurance, sélectionnez **[!UICONTROL Configurer]**.
   ![configurer le clic](assets/push-validate-config.png)
1. Sélectionnez la variable ![Plus](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) bouton en regard de **[!UICONTROL Messagerie in-app]**.
1. Sélectionnez **[!UICONTROL Enregistrer]**.
   ![save](assets/assurance-in-app-config.png)
1. Sélectionner **[!UICONTROL Messagerie in-app]** dans le volet de navigation de gauche.
1. Sélectionnez la variable **[!UICONTROL Validation]** .
1. Confirmez que vous n’obtenez aucune erreur.
   ![Validation In-App](assets/assurance-in-app-validate.png)


## Créer votre propre message in-app

Pour créer votre propre message in-app, vous devez définir dans Journey Optimizer une campagne qui déclenche un message in-app en fonction des événements qui se produisent. Ces événements peuvent être :

* données envoyées à Adobe Experience Platform,
* les événements de suivi principaux, tels que l’action, l’état ou la collecte des données de PII, via les API génériques Mobile Core,
* les événements de cycle de vie des applications, tels que le lancement, l’installation, la mise à niveau, la fermeture ou le blocage,
* événements de géolocalisation, comme l’entrée ou la sortie d’un point ciblé.

Dans ce tutoriel, vous allez utiliser les API génériques et indépendantes de l’extension Mobile Core pour faciliter le suivi des événements des écrans utilisateur, des actions et des données de PII. Les événements générés par ces API sont publiés sur le centre d’événements du SDK et peuvent être utilisés par des extensions. Par exemple, lorsque l’extension Analytics est installée, toutes les actions de l’utilisateur et les données d’événement des écrans d’application sont envoyées aux points de terminaison de création de rapports Analytics appropriés.

1. Dans l’interface utilisateur de Journey Optimizer, sélectionnez **[!UICONTROL Campagnes]** dans le rail de gauche.
1. Sélectionner **[!UICONTROL Créer une campagne]**.
1. Dans le **[!UICONTROL Créer une campagne]** écran :
   1. Sélectionner **[!UICONTROL Message in-app]** et sélectionnez **[!UICONTROL Application mobile Luma]** de la **[!UICONTROL Surface de l’application]** liste.
   1. Sélectionnez **[!UICONTROL Créer]**
      ![Propriétés de campagne](assets/ajo-campaign-properties.png)
1. Dans l’écran de définition de campagne, à l’adresse **[!UICONTROL Propriétés]**, saisissez une **[!UICONTROL Nom]** pour la campagne, par exemple `Luma - In-App Messaging Campaign`, et a **[!UICONTROL Description]**, par exemple `In-app messaging campaign for Luma app`.
   ![Nom de la campagne](assets/ajo-campaign-properties-name.png)
1. Faites défiler jusqu’à **[!UICONTROL Action]**, puis sélectionnez **[!UICONTROL Modifier le contenu]**.
1. Dans le **[!UICONTROL Message In-App]** écran :
   1. Sélectionner **[!UICONTROL Modal]** comme la propriété **[!UICONTROL Disposition du message]**.
   2. Entrée `https://luma.enablementadobe.com/content/dam/luma/en/logos/Luma_Logo.png` pour **[!UICONTROL URL du média]**.
   3. Saisissez un **[!UICONTROL En-tête]**, par exemple `Welcome to this Luma In-App Message` et saisissez un **[!UICONTROL Corps]**, par exemple `Triggered by pushing that button in the app...`.
   4. Entrée **[!UICONTROL Ignorer]** comme la propriété **[!UICONTROL Texte #1 bouton (principal)]**.
   5. Notez comment l’aperçu est mis à jour.
   6. Sélectionner **[!UICONTROL Réviser pour activer]**.
      ![Editeur in-app](assets/ajo-in-app-editor.png)
1. Dans le **[!UICONTROL Réviser pour activer (Luma - Campagne de messagerie in-app)]** écran, sélectionnez ![Modifier](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Edit_18_N.svg) dans le **[!UICONTROL Planification]** mosaïque.
   ![Planification de la révision : sélectionnez Planification](assets/ajo-review-select-schedule.png)
1. De retour dans le **[!UICONTROL Luma - Campagne de messagerie in-app]** écran, sélectionnez ![Modifier](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Edit_18_N.svg) **[!UICONTROL Modifier les déclencheurs]**.
1. Dans le **[!UICONTROL Déclencheur de message in-app]** vous pouvez configurer les détails de l’action de suivi qui déclenche le message in-app :
   1. Pour supprimer **[!UICONTROL Événement de lancement d’application]**, sélectionnez ![Fermer](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Close_18_N.svg) .
   1. Utilisation ![Ajouter](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) **[!UICONTROL Ajouter une condition]** pour créer à plusieurs reprises la logique suivante pour **[!UICONTROL Afficher le message si]**.
   1. Cliquez sur **[!UICONTROL Terminé]**.
      ![Logique de déclenchement](assets/ajo-trigger-logic.png)

   Vous avez défini une action de suivi, où la variable **[!UICONTROL Action]** est égal à `in-app` et la variable **[!UICONTROL Données contextuelles]** avec l’action est une paire valeur-clé de `"showMessage" : "true"`.

1. De retour dans le **[!UICONTROL Luma - Campagne de messagerie in-app]** écran, sélectionnez **[!UICONTROL Réviser pour activer]**.
1. Dans le **[!UICONTROL Réviser pour activer (Luma - Campagne de messagerie in-app)]** écran, sélectionnez **[!UICONTROL Activer]**.
1. Vous voyez votre **[!UICONTROL Luma - Campagne de messagerie in-app]** avec état **[!UICONTROL En direct]** dans le **[!UICONTROL Campagnes]** liste.
   ![Liste des campagnes](assets/ajo-campaign-list.png)


## Déclenchement du message in-app

Vous disposez de tous les ingrédients nécessaires pour envoyer un message in-app. Reste à savoir comment déclencher ce message in-app dans votre code.

1. Accédez à Luma > Luma > Utils > MobileSDK dans le navigateur de projet Xcode, recherchez la variable `func sendTrackAction(action: String, data: [String: Any]?)` et ajoutez le code suivant, qui appelle la fonction `MobileCore.track` fonction, en fonction des paramètres `action` et `data`.


   ```swift
   // send trackAction event
   MobileCore.track(action: action, data: data)
   ```

1. Accédez à **[!UICONTROL Luma]** > **[!UICONTROL Luma]** > **[!UICONTROL Vues]** > **[!UICONTROL Général]** > **[!UICONTROL ConfigView]** dans Xcode Project Navigator. Recherchez le code du bouton Message in-app et ajoutez le code suivant :

   ```swift
   Task {
       AEPService.shared.sendTrackAction(action: "in-app", data: ["showMessage": "true"])
   }
   ```

## Validation à l’aide de votre application

1. Ouvrez votre application sur un appareil ou dans le simulateur.

1. Accédez au **[!UICONTROL Paramètres]** .

1. Appuyer **[!UICONTROL Message In-App]**. Le message in-app apparaît dans votre application.
   <img src="assets/ajo-in-app-message.png" width="300" />


## Validation dans Assurance

Vous pouvez valider vos messages in-app dans l’interface utilisateur d’assurance.

1. Sélectionner **[!UICONTROL Messagerie in-app]**.
1. Sélectionner **[!UICONTROL Liste des événements]**.
1. Sélectionnez une **[!UICONTROL Afficher le message]** entrée .
1. Inspect de l’événement brut, en particulier le `html`, qui contient la mise en page et le contenu complets du message in-app.
   ![Assurance : message in-app](assets/assurance-in-app-display-message.png)


## Mise en oeuvre dans votre application

Vous devriez maintenant disposer de tous les outils pour commencer à ajouter des notifications push, le cas échéant et de manière applicable, à l’application Luma. Par exemple, accueillir l’utilisateur lorsqu’il se connecte à l’application ou à l’approche d’une géolocalisation spécifique.

>[!SUCCESS]
>
>Vous avez désormais activé l’application pour la messagerie in-app et ajouté une campagne de messagerie in-app à l’aide de Adobe Journey Optimizer et de l’extension Adobe Journey Optimizer pour le SDK Adobe Experience Platform Mobile.<br/>Merci d’investir votre temps à apprendre sur le SDK Adobe Experience Platform Mobile. Si vous avez des questions, souhaitez partager des commentaires généraux ou avez des suggestions sur le contenu futur, partagez-les à ce sujet. [Article de discussion de la communauté Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796).

Suivant : **[Conclusion et prochaines étapes](conclusion.md)**
