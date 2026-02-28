---
title: Créer et envoyer des messages in-app avec Platform Mobile SDK
description: Découvrez comment créer et envoyer des messages in-app à une application mobile avec Platform Mobile SDK et Adobe Journey Optimizer.
solution: Data Collection,Journey Optimizer
feature-set: Journey Optimizer
feature: In App
jira: KT-14639
exl-id: 6cb4d031-6172-4a84-b717-e3a1f5dc7d5d
source-git-commit: 97fba09ddba62cffe4428592ce25e4f26c3a5850
workflow-type: tm+mt
source-wordcount: '1786'
ht-degree: 4%

---

# Créer et envoyer des messages in-app

Découvrez comment créer des messages in-app pour les applications mobiles avec Experience Platform Mobile SDK et Journey Optimizer.

Journey Optimizer vous permet de créer des campagnes pour envoyer des messages in-app à des audiences ciblées. Les campagnes dans Journey Optimizer sont utilisées pour diffuser du contenu unique à une audience spécifique à l’aide de divers canaux. Avec les campagnes, les actions sont exécutées simultanément, immédiatement ou selon un planning spécifié. Lors de l’utilisation de parcours (voir la leçon [Notifications push Journey Optimizer](journey-optimizer-push.md)), les actions sont exécutées en séquence.

![Architecture](assets/architecture-ajo.png){zoomable="yes"}

Avant d’envoyer des messages in-app avec Journey Optimizer, vous devez vous assurer que les configurations et intégrations appropriées sont en place. Pour comprendre le flux de données de la messagerie in-app dans Journey Optimizer, consultez [documentation](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/in-app/inapp-configuration).

>[!NOTE]
>
>Cette leçon est facultative et s’applique uniquement aux utilisateurs de Journey Optimizer qui cherchent à envoyer des messages in-app.


## Conditions préalables

* Application créée et exécutée avec succès avec les SDK installés et configurés.
* Configurez l’application pour Adobe Experience Platform.
* Accès à Journey Optimizer et [autorisations suffisantes pour les notifications push](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/push/push-config/push-configuration). Vous devez également disposer des autorisations suffisantes pour accéder aux fonctionnalités de Journey Optimizer ci-après.
   * Gérer des campagnes.
* Périphérique ou simulateur iOS physique à des fins de test.


## Objectifs d’apprentissage

Dans cette leçon, vous allez :

* Créez une configuration de canal dans Journey Optimizer.
* Installez et configurez l’extension de balise Journey Optimizer.
* Mettez à jour votre application pour enregistrer l’extension de balise Journey Optimizer.
* Validez la configuration dans Assurance.
* Définissez votre propre expérience de campagne et de message in-app dans Journey Optimizer.
* Envoyez votre propre message in-app depuis l’application.

## Configuration

>[!TIP]
>
>Si vous avez déjà configuré votre environnement dans le cadre de la leçon [Messagerie push Journey Optimizer](journey-optimizer-push.md), il se peut que vous ayez déjà effectué certaines des étapes de cette section de configuration.


### Créer une configuration des canaux

Pour commencer, vous devez créer une configuration de canal afin de pouvoir envoyer des notifications de messages d’application depuis Journey Optimizer.

1. Dans l’interface de Journey Optimizer, ouvrez le menu **[!UICONTROL Canaux]** > **[!UICONTROL Paramètres généraux]** > **[!UICONTROL Configurations de canal]** puis sélectionnez **[!UICONTROL Créer une configuration de canal]**.

1. Saisissez un nom et une description (facultatif) pour la configuration. Par exemple, `LumaInAppMessaging` et `Channel for in-app messaging`.

   >[!NOTE]
   >
   > Les noms doivent commencer par une lettre (A-Z). Ils ne peuvent contenir que des caractères alphanumériques. Vous pouvez également utiliser le trait de soulignement `_`, le point`.` et le trait d&#39;union `-`.

1. Pour attribuer des libellés d’utilisation des données personnalisés ou de base à la configuration, vous pouvez sélectionner **[!UICONTROL Gérer l’accès]**. [En savoir plus sur le contrôle d’accès au niveau de l’objet (OLAC)](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/access-control/object-based-access)

1. Sélectionnez le canal **Messagerie in-app**.

1. Sélectionnez **[!UICONTROL Action(s) marketing]** pour associer des politiques de consentement aux messages à l’aide de cette configuration. Toutes les politiques de consentement associées à l’action marketing sont utilisées pour respecter les préférences de vos clients. [En savoir plus sur les actions marketing](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/privacy/consent/consent#surface-marketing-actions). Par exemple : ciblage push.

1. Sélectionnez la Plateforme pour laquelle vous souhaitez définir les paramètres. Ce paramètre vous permet de spécifier l’application cible pour chaque plateforme et d’assurer la cohérence de la diffusion du contenu sur plusieurs plateformes.

   >[!NOTE]
   >
   >Pour les plateformes iOS et Android, la diffusion se base uniquement sur l’ID d’application. Si les deux applications partagent le même ID d’application, le contenu est diffusé aux deux, quelle que soit la plateforme sélectionnée dans la **[!UICONTROL configuration du canal]**.

1. Saisissez les ID d’application de la plateforme que vous souhaitez prendre en charge.

   ![Créer une configuration de canal](assets/in-app-messaging-config.png){zoomable="yes"}

1. Sélectionnez **[!UICONTROL Envoyer]** pour enregistrer vos modifications.

### Mettre à jour la configuration du flux de données

Pour vous assurer que les données envoyées de votre application mobile à Edge Network sont transférées vers Journey Optimizer, mettez à jour votre configuration Experience Edge.



1. Dans l’interface utilisateur de collecte de données, sélectionnez **[!UICONTROL Flux de données]**, puis sélectionnez votre flux de données, par exemple **[!DNL Luma Mobile App]**.
1. Sélectionnez ![Plus](https://spectrum.adobe.com/static/icons/workflow_18/Smock_MoreSmallList_18_N.svg) pour **[!UICONTROL Experience Platform]** et sélectionnez ![Modifier](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Edit_18_N.svg) **[!UICONTROL Modifier]** dans le menu contextuel.
1. Dans l’écran **[!UICONTROL Flux de données]** > ![Dossier](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Folder_18_N.svg) > **[!UICONTROL Adobe Experience Platform]**, assurez-vous que **[!UICONTROL Adobe Journey Optimizer]** est sélectionné. Voir [Paramètres Adobe Experience Platform](https://experienceleague.adobe.com/fr/docs/experience-platform/datastreams/configure) pour plus d&#39;informations.
1. Pour enregistrer la configuration de votre flux de données, sélectionnez **[!UICONTROL Enregistrer]**.


   ![configuration du train de données AEP](assets/datastream-ajo-inapp-configuration.png){zoomable="yes"}


### Installation de l’extension de balises Journey Optimizer

Pour que votre application fonctionne avec Journey Optimizer, vous devez mettre à jour votre propriété de balise.

1. Accédez à **[!UICONTROL Balises]** > **[!UICONTROL Extensions]** > **[!UICONTROL Catalogue]**.
1. Ouvrez votre propriété, par exemple **[!DNL Luma Mobile App Tutorial]**.
1. Sélectionnez **[!UICONTROL Catalogue]**.
1. Recherchez l’extension **[!UICONTROL Adobe Journey Optimizer]**.
1. Installez l’extension .

Lorsque vous *uniquement* utilisez des messages in-app dans votre application, dans **[!UICONTROL Installer l’extension]** ou **[!UICONTROL Configurer l’extension]**, vous n’avez rien à configurer. Si vous avez déjà suivi la leçon [Notifications push](journey-optimizer-push.md) dans le tutoriel, vous constatez que pour l’environnement **[!UICONTROL Développement]**, le jeu de données **[!UICONTROL Jeu de données d’événement d’expérience de suivi push AJO]** est sélectionné dans la liste **[!UICONTROL Jeu de données d’événement]**.


### Implémentation de Journey Optimizer dans l’application

Comme nous l’avons vu dans les leçons précédentes, l’installation d’une extension de balise mobile fournit uniquement la configuration . Vous devez ensuite installer et enregistrer le SDK de messagerie. Si ces étapes ne sont pas claires, consultez la section [Installation des SDK](install-sdks.md).

>[!NOTE]
>
>Si vous avez terminé la section [Installation des SDK](install-sdks.md), le SDK est déjà installé et vous pouvez ignorer cette étape.
>

>[!BEGINTABS]

>[!TAB iOS]

1. Dans Xcode, assurez-vous que [AEP Messaging](https://github.com/adobe/aepsdk-messaging-ios) est ajouté à la liste des packages dans Dépendances de packages. Voir [Gestionnaire de packages Swift](install-sdks.md#swift-package-manager).
1. Accédez à **[!DNL Luma]** > **[!DNL Luma]** > **[!UICONTROL AppDelegate]** dans le navigateur de projet Xcode.
1. Assurez-vous que `AEPMessaging` fait partie de votre liste d’importations.

   `import AEPMessaging`

1. Assurez-vous que `Messaging.self` fait partie du tableau d’extensions que vous enregistrez.

   ```swift
   let extensions = [
       AEPIdentity.Identity.self,
       Lifecycle.self,
       Signal.self,
       Edge.self,
       AEPEdgeIdentity.Identity.self,
       Consent.self,
       UserProfile.self,
       Places.self,
       Messaging.self,
       Optimize.self,
       Assurance.self
   ]
   ```

>[!TAB Android]

1. Dans Android Studio, assurez-vous que [aepsdk-messaging-android](https://github.com/adobe/aepsdk-messaging-android) fait partie des dépendances dans **[!UICONTROL build.gradle.kts]** dans **[!UICONTROL Android]** ![ChevronDown](/help/assets/icons/ChevronDown.svg) > **[!UICONTROL Scripts Gradle]**. Voir [Gradle](install-sdks.md#gradle).
1. Accédez à **[!UICONTROL Android]** ![ChevronDown](/help/assets/icons/ChevronDown.svg) **[!DNL app]** > **[!DNL kotlin+java]** > **[!UICONTROL com.adobe.luma.tutorial.android]** > **[!UICONTROL LumaApplication]** dans le navigateur de projet Android Studio.
1. Assurez-vous que `com.adobe.marketing.mobile.Messaging` fait partie de votre liste d’importations.

   `import import com.adobe.marketing.mobile.Messaging`

1. Assurez-vous que `Messaging.EXTENSION` fait partie du tableau d’extensions que vous enregistrez.

   ```kotlin
   val extensions = listOf(
       Identity.EXTENSION,
       Lifecycle.EXTENSION,
       Signal.EXTENSION,
       Edge.EXTENSION,
       Consent.EXTENSION,
       UserProfile.EXTENSION,
       Places.EXTENSION,
       Messaging.EXTENSION,
       Optimize.EXTENSION,
       Assurance.EXTENSION
   )
   ```

>[!ENDTABS]

## Validation de la configuration avec Assurance

1. Consultez la section [instructions de configuration](assurance.md#connecting-to-a-session) pour connecter votre simulateur ou votre appareil à Assurance.
1. Dans l’interface utilisateur d’Assurance, sélectionnez **[!UICONTROL Configurer]**.
   ![configurer le clic](assets/push-validate-config.png){zoomable="yes"}
1. Sélectionnez le bouton ![Plus](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) en regard de **[!UICONTROL Messagerie In-App]**.
1. Sélectionnez **[!UICONTROL Enregistrer]**.
   ![enregistrer](assets/assurance-in-app-config.png){zoomable="yes"}
1. Sélectionnez **[!UICONTROL Messagerie In-App]** dans le volet de navigation de gauche.
1. Sélectionnez l’onglet **[!UICONTROL Validation]**. Vérifiez que vous n’obtenez aucune erreur.

   ![ Validation In-App ](assets/assurance-in-app-validate.png){zoomable="yes"}


## Créer votre propre message in-app

Pour créer votre propre message in-app, vous devez définir une campagne dans Journey Optimizer qui déclenche un message in-app en fonction des événements qui se produisent. Ces événements peuvent être les suivants :

* les données envoyées à Adobe Experience Platform,
* les événements de suivi principaux, tels que l’action, l’état ou la collecte de données PII, par le biais des API génériques Mobile Core,
* événements du cycle de vie de l’application, tels que lancement, installation, mise à niveau, fermeture ou blocage
* les événements de géolocalisation, tels que l’entrée ou la sortie d’un point ciblé.

Dans ce tutoriel, vous allez utiliser les API génériques Mobile Core et indépendantes de l&#39;extension (voir [API génériques Mobile Core](https://developer.adobe.com/client-sdks/documentation/mobile-core/#mobile-core-generic-apis)) pour faciliter le suivi des événements des écrans utilisateur, des actions et des données PII. Les événements générés par ces API sont publiés sur le hub d’événements SDK et peuvent être utilisés par les extensions. Le hub d’événements SDK fournit la structure de données de base liée à toutes les extensions de Mobile Platform SDK. Le hub d’événements conserve une liste des extensions enregistrées et des modules internes, une liste des écouteurs d’événements enregistrés et une base de données d’état partagée.

Le hub d’événements SDK publie et reçoit des données d’événement provenant d’extensions enregistrées afin de simplifier les intégrations aux solutions Adobe et tierces. Par exemple, lorsque l’extension Optimize est installée, le hub d’événements gère toutes les requêtes et interactions avec le moteur d’offres Journey Optimizer - Gestion des décisions .

1. Dans l’interface utilisateur de Journey Optimizer, sélectionnez **[!UICONTROL Campagnes]** dans le rail de gauche.
1. Sélectionnez **[!UICONTROL Créer une campagne]**.
1. Dans la boîte de dialogue **[!UICONTROL Créer votre campagne]**, sélectionnez ![Horloge](/help/assets/icons/Clock.svg) **[!UICONTROL Planifié - Marketing]** et sélectionnez **[!UICONTROL Confirmer]**.
1. Sur l’écran **[!UICONTROL Campaign - *AAAA-MM-JJ HH:MM:SS UTC+XX:XX*]**:

   1. Dans l’onglet **[!UICONTROL Propriétés]** :

      1. Saisissez un nom pour la campagne. Par exemple, `Luma Mobile In-App Campaign`.
      1. Vous pouvez éventuellement ajouter une description.


   1. Sélectionnez l’onglet **[!UICONTROL Action]**.

      1. Sous **[!UICONTROL Afficher le message si]**, sélectionnez ![Ajouter](/help/assets/icons/Add.svg) **[!UICONTROL Ajouter une action]**. Dans le menu déroulant, sélectionnez **[!UICONTROL Message in-app]**.
      1. Dans le menu déroulant **[!UICONTROL Configuration du message in-app]**, sélectionnez votre configuration. Par exemple, **[!UICONTROL LumaInAppMessaging]**.
      1. Sélectionnez ![Modifier](/help/assets/icons/Edit.svg) **[!UICONTROL Modifier les déclencheurs]**.
      1. Dans la boîte de dialogue **[!UICONTROL Déclencheur de message in-app]** :

         1. Sélectionnez **[!UICONTROL Lancement de l’application]** et sélectionnez **[!UICONTROL Action de suivi]** dans le menu déroulant.
         1. Sélectionnez ![AjouterCercle](/help/assets/icons/AddCircle.svg) **[!UICONTROL Ajouter une condition]**.
         1. Sélectionnez **[!UICONTROL Action]** et **[!UICONTROL égal]** dans les menus déroulants.
         1. Saisissez `in-app`.
         1. Sélectionnez ![AjouterCercle](/help/assets/icons/AddCircle.svg) **[!UICONTROL Ajouter une condition]**.
         1. Sélectionnez **[!UICONTROL Données contextuelles]** dans le menu déroulant, puis saisissez `showMessage`.
         1. Sélectionnez **[!UICONTROL égal]** dans le menu déroulant, puis saisissez `true`.

            ![Modifier les déclencheurs](assets/edit-triggers.png){zoomable="yes"}
         1. Sélectionnez **[!UICONTROL Terminé]**.

   1. De retour dans l’écran principal de définition de la campagne, sélectionnez l’onglet **[!UICONTROL Contenu]**.

      1. Activez **[!UICONTROL Formatage avancé]**.
      1. Sélectionnez **[!UICONTROL Modal]** comme **[!UICONTROL Disposition des messages]**. Dans la boîte de dialogue **[!UICONTROL Changer de disposition]**, sélectionnez **[!UICONTROL Modifier la disposition]**.
      1. Dans l’onglet **[!UICONTROL Contenu]**.
         1. Saisissez `https://newluma.enablementadobe.com/images/logo.png` pour l’URL **[!UICONTROL Media]**.
         1. Saisissez un **[!UICONTROL En-tête]**, par exemple `Welcome to this Luma In-App Message` et saisissez un **[!UICONTROL Corps]**, par exemple `Triggered by pushing that button in the app...`.

         ![ Contenu du message in-app ](assets/in-app-message-content.png){zoomable="yes"}

      1. Sélectionnez l’onglet **[!UICONTROL Paramètres]**.
         1. Sélectionnez **[!UICONTROL Personnaliser la taille]** dans **[!UICONTROL Message]**.
         1. Désactivez **[!UICONTROL Ajuster au contenu]**.
         1. Définissez **[!UICONTROL Hauteur]** sur **[!UICONTROL 75 %]**.

         ![Paramètres des messages in-app](assets/in-app-message-settings.png){zoomable="yes"}

1. Sélectionnez **[!UICONTROL Vérifier pour activer]**. Pour modifier éventuellement l’une des configurations pour **[!UICONTROL Contenu]**, **[!UICONTROL Propriétés]**, **[!UICONTROL Actions]** ou plus, sélectionnez ![Modifier](/help/assets/icons/Edit.svg).
1. Dans l’écran **[!UICONTROL Vérifier pour activer (*nom de la campagne*)]** sélectionnez **[!UICONTROL Activer]**.
1. Au bout d’un certain temps, votre **_nom de la campagne_** avec le statut **[!UICONTROL Actif]** s’affiche dans la liste **[!UICONTROL Campagnes]**.
   ![Liste des campagnes.](assets/ajo-campaign-list.png){zoomable="yes"}


## Déclencher le message in-app

Tous les ingrédients sont en place pour envoyer un message in-app. Il reste à savoir comment déclencher ce message in-app dans votre application.

>[!BEGINTABS]

>[!TAB iOS]

1. Accédez à **[!DNL Luma]** > **[!DNL Luma]** > **[!DNL Utils]** > **[!UICONTROL MobileSDK]** dans le navigateur de projet Xcode. Recherchez la fonction `func sendTrackAction(action: String, data: [String: Any]?)` et ajoutez le code suivant, qui appelle la fonction [`MobileCore.track`](https://developer.adobe.com/client-sdks/documentation/mobile-core/api-reference/#trackaction), en fonction des paramètres `action` et `data`.


   ```swift
   // Send trackAction event
   MobileCore.track(action: action, data: data)
   ```

1. Accédez à **[!DNL Luma]** > **[!DNL Luma]** > **[!DNL Views]** > **[!DNL General]** > **[!UICONTROL ConfigView]** dans le navigateur de projet Xcode. Recherchez le code du bouton Message In-App et ajoutez le code suivant :

   ```swift
   // Setting parameters and calling function to send in-app message
   Task {
       MobileSDK.shared.sendTrackAction(action: "in-app", data: ["showMessage": "true"])
   }
   ```

>[!TAB Android]

1. Accédez à **[!UICONTROL Android]** ![ChevronDown](/help/assets/icons/ChevronDown.svg) > **[!DNL app]** > **[!DNL kotlin+java]** > **[!DNL com.adobe.luma.tutorial.android]** > **[!DNL models]** > **[!UICONTROL MobileSDK]** dans le navigateur d’Android Studio. Recherchez la fonction `fun sendTrackAction(action: String, data: Map<String, String>?)` et ajoutez le code suivant, qui appelle la fonction [`MobileCore.track`](https://developer.adobe.com/client-sdks/documentation/mobile-core/api-reference/#trackaction), en fonction des paramètres `action` et `data`.


   ```kotlin
   // Send trackAction event
   MobileCore.track(action, data)
   ```

1. Accédez à **[!UICONTROL Android]** ![ChevronDown](/help/assets/icons/ChevronDown.svg) > **[!DNL app]** > **[!DNL kotlin+java]** > **[!DNL com.adobe.luma.tutorial.androi]** > **[!DNL views]** > **[!UICONTROL ConfigView.kt]** dans le navigateur d’Android Studio. Recherchez le code du bouton du gestionnaire de `onInAppMessageClick` et ajoutez le code suivant :

   ```kotlin
   // Setting parameters and calling function to send in-app message
   MobileSDK.shared.sendTrackAction(
       "in-app",
       mapOf("showMessage" to "true")
   )
   ```

>[!ENDTABS]

## Validation à l’aide de l’application

Vous pouvez valider les messages in-app depuis l’application elle-même.

>[!BEGINTABS]

>[!TAB iOS]

1. Recréez et exécutez l’application dans le simulateur ou sur un appareil physique à partir de Xcode, à l’aide de ![Play](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Play_18_N.svg).

1. Accédez à l’onglet **[!UICONTROL Paramètres]**.

1. Appuyez Sur **[!UICONTROL Message In-App]**. Le message in-app apparaît dans votre application.

   <img src="assets/ajo-in-app-message.png" width="300">


>[!TAB Android]

1. Recréez et exécutez l’application dans le simulateur ou sur un appareil physique à partir d’Android Studio, à l’aide de ![Play](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Play_18_N.svg).

1. Accédez à l’onglet **[!UICONTROL Paramètres]**.

1. Appuyez Sur **[!UICONTROL Message In-App]**. Le message in-app apparaît dans votre application.

   <img src="assets/ajo-in-app-message-android.png" width="300">


>[!ENDTABS]


## Validation de la mise en œuvre dans Assurance

Vous pouvez valider vos messages in-app dans l’interface utilisateur d’Assurance.

1. Consultez la section [instructions de configuration](assurance.md#connecting-to-a-session) pour connecter votre simulateur ou votre appareil à Assurance.
1. Sélectionnez **[!UICONTROL Messagerie In-App]**.
1. Sélectionnez **[!UICONTROL Liste des événements]**.
1. Sélectionnez une entrée **[!UICONTROL Afficher le message]**.
1. Inspectez l’événement brut, en particulier le `html`, qui contient la disposition et le contenu complets du message in-app.
   ![Message In-App Assurance](assets/assurance-in-app-display-message.png){zoomable="yes"}


## Étapes suivantes

Vous devriez maintenant disposer de tous les outils nécessaires pour commencer à ajouter des messages in-app, le cas échéant. Par exemple, la promotion de produits en fonction d’interactions spécifiques que vous suivez dans votre application .

>[!SUCCESS]
>
>Vous avez activé l’application pour la messagerie in-app et ajouté une campagne de messagerie in-app à l’aide de Journey Optimizer et de l’extension Journey Optimizer pour Experience Platform Mobile SDK.
>
>Merci d’avoir consacré votre temps à découvrir Adobe Experience Platform Mobile SDK. Si vous avez des questions, souhaitez partager des commentaires généraux ou des suggestions sur le contenu futur, partagez-les dans ce [article de discussion de la communauté Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796).

Suivant : **[Création et affichage d&#39;offres](journey-optimizer-offers.md)**
