---
title: Créer et envoyer des notifications push avec le SDK Mobile Platform
description: Découvrez comment créer des notifications push vers une application mobile à l’aide du SDK Mobile Platform et de Adobe Journey Optimizer.
solution: Data Collection,Journey Optimizer
feature-set: Journey Optimizer
feature: Push
jira: KT-14638
exl-id: e8e920d5-fd36-48b7-9185-a34231c0d336
source-git-commit: e316f881372a387b82f8af27f7f0ea032a99be99
workflow-type: tm+mt
source-wordcount: '2582'
ht-degree: 1%

---

# Créer et envoyer des notifications push

Découvrez comment créer des notifications push pour les applications mobiles avec le SDK Mobile Experience Platform et Journey Optimizer.

Journey Optimizer vous permet de créer des parcours et d’envoyer des messages à des audiences ciblées. Avant d’envoyer des notifications push avec Journey Optimizer, vous devez vous assurer que les configurations et intégrations appropriées sont en place. Pour comprendre le flux de données des notifications push dans Journey Optimizer, reportez-vous à la [documentation](https://experienceleague.adobe.com/docs/journey-optimizer/using/push/push-config/push-gs.html).

![Architecture](assets/architecture-ajo.png)

>[!NOTE]
>
>Cette leçon est facultative et s’applique uniquement aux utilisateurs de Journey Optimizer qui souhaitent envoyer des notifications push.


## Conditions préalables

* Création et exécution de l’application avec les SDK installés et configurés.
* Configurez l’application pour Adobe Experience Platform.
* Accès à Journey Optimizer et autorisations suffisantes comme décrit [ici](https://experienceleague.adobe.com/docs/journey-optimizer/using/push/push-config/push-configuration.html?lang=en). Vous avez également besoin d’une autorisation suffisante pour accéder aux fonctionnalités Journey Optimizer suivantes.
   * Créez une surface d’application.
   * Créez un parcours.
   * Créez un message.
   * Créer des paramètres prédéfinis de message.
* **Compte de développeur Apple payant** disposant d’un accès suffisant pour créer des certificats, des identifiants et des clés.
* Appareil ou simulateur iOS physique à tester.

## Objectifs d&#39;apprentissage

Dans cette leçon, vous allez

* Enregistrez l’ID d’application avec le service Apple Push Notification (APNS).
* Créez une surface d’application dans Journey Optimizer.
* Mettez à jour votre schéma pour inclure les champs de messagerie push.
* Installez et configurez l’extension de balise Journey Optimizer.
* Mettez à jour votre application pour enregistrer l’extension de balise Journey Optimizer.
* Validez la configuration dans Assurance.
* Envoi d’un message de test à partir d’Assurance
* Définissez votre propre événement, parcours et expérience de notification push dans Journey Optimizer.
* Envoyez votre propre notification push depuis l’application.


## Configuration

>[!TIP]
>
>Si vous avez déjà configuré votre environnement dans le cadre de la leçon [Messagerie in-app Journey Optimizer](journey-optimizer-inapp.md), vous avez peut-être déjà effectué certaines des étapes de cette section de configuration.

### Enregistrement de l’ID d’application avec des APNS

Les étapes suivantes ne sont pas spécifiques à Adobe Experience Cloud et sont conçues pour vous guider tout au long de la configuration des APNS.

#### Création d’une clé privée

1. Sur le portail destiné aux développeurs Apple, accédez à **[!UICONTROL Clés]**.
1. Pour créer une clé, sélectionnez **[!UICONTROL +]**.
   ![créer une clé](assets/mobile-push-apple-dev-new-key.png)

1. Fournissez un **[!UICONTROL nom de clé]**.
1. Cochez la case **[!UICONTROL Service de notification push Apple] (APNS)** .
1. Sélectionnez **[!UICONTROL Continuer]**.
   ![configurer une nouvelle clé](assets/mobile-push-apple-dev-config-key.png)
1. Vérifiez la configuration et sélectionnez **[!UICONTROL Enregistrer]**.
1. Téléchargez la clé privée `.p8`. Il est utilisé dans la configuration Surface de l’application plus loin dans cette leçon.
1. Prenez note de l&#39;**[!UICONTROL ID de clé]**. Il est utilisé dans la configuration Surface de l’application.
1. Prenez note de l&#39;**[!UICONTROL ID d&#39;équipe]**. Il est utilisé dans la configuration Surface de l’application.
   ![Détails de la clé](assets/push-apple-dev-key-details.png)

Vous trouverez [de la documentation supplémentaire ici](https://help.apple.com/developer-account/#/devcdfbb56a3).

#### Ajout d’une surface d’application dans la collecte de données

1. Dans l’ [ interface de collecte de données ](https://experience.adobe.com/data-collection/), sélectionnez **[!UICONTROL App Surfaces]** dans le panneau de gauche.
1. Pour créer une configuration, sélectionnez **[!UICONTROL Créer une surface d’application]**.
   ![app surface home](assets/push-app-surface.png)
1. Saisissez un **[!UICONTROL Nom]** pour la configuration, par exemple `Luma App Tutorial` .
1. Dans **[!UICONTROL Configuration d&#39;application mobile]**, sélectionnez **[!UICONTROL Apple iOS]**.
1. Saisissez l’ID du lot de l’application mobile dans le champ **[!UICONTROL ID de l’application (ID du lot iOS)]** . Par exemple, `com.adobe.luma.tutorial.swiftui`.
1. Activez la bascule **[!UICONTROL Push Credentials]** (Informations d’identification push) pour ajouter vos informations d’identification.
1. Faites glisser et déposez votre fichier `.p8` **Apple Push Notification Authentication Key** .
1. Fournissez l’ **[!UICONTROL ID de clé]**, une chaîne de 10 caractères attribuée lors de la création de la clé d’authentification `p8`. Elle se trouve sous l’onglet **[!UICONTROL Clés]** de la page **Certificats, identifiants et profils** des pages du portail du développeur Apple. Voir aussi [Création d’une clé privée](#create-a-private-key).
1. Indiquez l&#39;**[!UICONTROL identifiant d&#39;équipe]**. L’ID d’équipe est une valeur qui se trouve sous l’onglet **Adhésion** ou en haut de la page du portail des développeurs Apple. Voir aussi [Création d’une clé privée](#create-a-private-key).
1. Sélectionnez **[!UICONTROL Enregistrer]**.

   ![Configuration de la surface de l’application](assets/push-app-surface-config.png)

### Mise à jour de la configuration des flux de données

Pour vous assurer que les données envoyées de votre application mobile à l’Edge Network sont transférées vers Journey Optimizer, mettez à jour votre configuration Experience Edge .

1. Dans l’interface utilisateur de la collecte de données, sélectionnez **[!UICONTROL Datastreams]**, puis sélectionnez votre flux de données, par exemple **[!DNL Luma Mobile App]**.
1. Sélectionnez ![Plus](https://spectrum.adobe.com/static/icons/workflow_18/Smock_MoreSmallList_18_N.svg) pour **[!UICONTROL Experience Platform]** et ![Modifier](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Edit_18_N.svg) **[!UICONTROL Modifier]** dans le menu contextuel.
1. Dans l’écran **[!UICONTROL Datastreams]** > ![Folder](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Folder_18_N.svg) > **[!UICONTROL Adobe Experience Platform]** :

   1. Si cette option n’est pas déjà sélectionnée, sélectionnez **[!UICONTROL Jeu de données de profil push AJO]** dans le **[!UICONTROL jeu de données de profil]**. Ce jeu de données de profil est requis lors de l’utilisation de l’appel de l’API `MobileCore.setPushIdentifier` (voir [Enregistrer le jeton de l’appareil pour les notifications push](#register-device-token-for-push-notifications)) qui garantit que l’identifiant unique des notifications push (ou l’identifiant push) est stocké dans le profil de l’utilisateur.

   1. **[!UICONTROL Adobe Journey Optimizer]** est sélectionné. Voir [Paramètres Adobe Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/datastreams/configure.html?lang=en#aep) pour plus d’informations.

   1. Pour enregistrer votre configuration de flux de données, sélectionnez **[!UICONTROL Enregistrer]**.

   ![ {configuration de flux de données AEP](assets/datastream-aep-configuration.png)



### Installation de l’extension de balises Journey Optimizer

Pour que votre application fonctionne avec Journey Optimizer, vous devez mettre à jour la propriété de balise.

1. Accédez à **[!UICONTROL Balises]** > **[!UICONTROL Extensions]** > **[!UICONTROL Catalogue]**,
1. Ouvrez votre propriété, par exemple **[!DNL Luma Mobile App Tutorial]**.
1. Sélectionnez **[!UICONTROL Catalog]**.
1. Recherchez l’extension **[!UICONTROL Adobe Journey Optimizer]**.
1. Installez l’extension .
1. Dans la boîte de dialogue **[!UICONTROL Installer l’extension]**
   1. Sélectionnez un environnement, par exemple **[!UICONTROL Développement]**.
   1. Sélectionnez le jeu de données **[!UICONTROL Jeu de données d’événement de suivi d’expérience AJO]** dans la liste **[!UICONTROL Jeu de données d’événement]**.
   1. Sélectionnez **[!UICONTROL Enregistrer dans la bibliothèque et créer]**.
      ![Paramètres de l’extension AJO](assets/push-tags-ajo.png)

>[!NOTE]
>
>Si vous ne voyez pas l’option **[!UICONTROL Jeu de données d’événement d’expérience de suivi push AJO]** comme option, contactez l’assistance clientèle.
>

## Validation de la configuration avec Assurance

1. Consultez la section [instructions de configuration](assurance.md#connecting-to-a-session) pour connecter votre simulateur ou périphérique à Assurance.
1. Dans l’interface utilisateur d’assurance, sélectionnez **[!UICONTROL Configurer]**.
   ![configurer le clic](assets/push-validate-config.png)
1. Sélectionnez ![Plus](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) en regard de **[!UICONTROL Débogage push]**.
1. Sélectionnez **[!UICONTROL Enregistrer]**.
   ![save](assets/push-validate-save.png)
1. Sélectionnez **[!UICONTROL Débogage push]** dans le volet de navigation de gauche.
1. Sélectionnez l’onglet **[!UICONTROL Valider la configuration]** .
1. Sélectionnez votre appareil dans la liste **[!UICONTROL Client]**.
1. Confirmez que vous n’obtenez aucune erreur.
   ![validate](assets/push-validate-confirm.png)
1. Sélectionnez l’onglet **[!UICONTROL Envoyer le test push]** .
1. (Facultatif) Modifiez les détails par défaut pour **[!UICONTROL Title]** et **[!UICONTROL Body]**
1. Sélectionnez ![Bogue](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Bug_18_N.svg) **[!UICONTROL Envoyer la notification push de test]**.
1. Vérifiez les **[!UICONTROL résultats du test]**.
1. La notification push de test devrait apparaître dans votre application.

   <img src="assets/luma-app-push.png" width="300" />


## Signature

La signature de l’application Luma est nécessaire pour envoyer des notifications push et **nécessite un compte développeur Apple payant**.

Pour mettre à jour la signature de votre application :

1. Accédez à votre application dans Xcode.
1. Sélectionnez **[!DNL Luma]** dans le navigateur de projet.
1. Sélectionnez la cible **[!DNL Luma]**.
1. Sélectionnez l’onglet **Signing &amp; Capabilities** .
1. Configurez **[!UICONTROL la gestion automatique de la signature]**, **[!UICONTROL Team]** et **[!UICONTROL Bundle Identifier]**, ou utilisez vos détails de mise en service de développement Apple spécifiques.

   >[!IMPORTANT]
   >
   >Assurez-vous d’utiliser un identifiant de lot _unique_ et remplacez l’identifiant de lot `com.adobe.luma.tutorial.swiftui`, car chaque identifiant de lot doit être unique. En règle générale, vous utilisez un format DNS inversé pour les chaînes d’ID de lot, comme `com.organization.brand.uniqueidentifier`. La version terminée de ce tutoriel, par exemple, utilise `com.adobe.luma.tutorial.swiftui`.


   ![Fonctionnalités de signature Xcode](assets/xcode-signing-capabilities.png){zoomable="yes"}


## Ajout de fonctionnalités de notification push à votre application

>[!IMPORTANT]
>
>Pour mettre en oeuvre et tester la notification push dans une application iOS, vous devez disposer d’un compte de développeur Apple **paid**. Si vous ne disposez pas d’un compte de développeur Apple payant, vous pouvez ignorer le reste de cette leçon.

1. Dans Xcode, sélectionnez **[!DNL Luma]** dans la liste **[!UICONTROL TARGETS]**, sélectionnez l’onglet **[!UICONTROL Signing &amp; Capabilities]**, cliquez sur le bouton **[!UICONTROL + Capability]**, puis sélectionnez **[!UICONTROL Push Notifications]**. Cela permet à votre application de recevoir des notifications push.

1. Vous devez ensuite ajouter une extension de notification à l’application. Revenez à l’onglet **[!DNL General]** et sélectionnez l’icône **[!UICONTROL +]** au bas de la section **[!UICONTROL TARGETS]** .

1. Vous êtes invité à sélectionner le modèle correspondant à votre nouvelle cible. Sélectionnez **[!UICONTROL Extension du service de notification]**, puis **[!UICONTROL Suivant]**.

1. Dans la fenêtre suivante, utilisez `NotificationExtension` comme nom de l&#39;extension et cliquez sur le bouton **[!UICONTROL Terminer]** .

Une extension de notification push doit maintenant être ajoutée à votre application, comme dans l’écran ci-dessous.

![Extension de notifications push](assets/xcode-signing-capabilities-pushnotifications.png)


## Mise en oeuvre de Journey Optimizer dans l’application

Comme indiqué dans les leçons précédentes, l’installation d’une extension de balise mobile fournit uniquement la configuration. Vous devez ensuite installer et enregistrer le SDK de messagerie. Si ces étapes ne sont pas claires, consultez la section [Installer les SDK](install-sdks.md) .

>[!NOTE]
>
>Si vous avez terminé la section [Installer les SDK](install-sdks.md) , le SDK est déjà installé et vous pouvez ignorer cette étape.
>

1. Dans Xcode, assurez-vous que [AEP Messaging](https://github.com/adobe/aepsdk-messaging-ios) est ajouté à la liste des packages dans les dépendances de modules. Voir [Swift Package Manager](install-sdks.md#swift-package-manager).
1. Accédez à **[!DNL Luma]** > **[!DNL Luma]** > **[!UICONTROL AppDelegate]** dans le navigateur de projet Xcode.
1. Assurez-vous que `AEPMessaging` fait partie de votre liste d’importations.

   `import AEPMessaging`

1. Vérifiez que `Messaging.self` fait partie du tableau des extensions que vous enregistrez.

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

## Enregistrement du jeton de périphérique pour les notifications push

1. Ajoutez l’API [`MobileCore.setPushIdentifier`](https://developer.adobe.com/client-sdks/documentation/mobile-core/api-reference/#setpushidentifier) à la fonction `func application(_ application: UIApplication, didRegisterForRemoteNotificationsWithDeviceToken deviceToken: Data)`.

   ```swift
   // Send push token to Mobile SDK
   MobileCore.setPushIdentifier(deviceToken)
   ```

   Cette fonction récupère le jeton de l’appareil unique sur lequel l’application est installée. Définit ensuite le jeton pour la diffusion de la notification push à l’aide de la configuration que vous avez configurée et qui repose sur le service Apple Push Notification (APN).

>[!IMPORTANT]
>
>L’ `MobileCore.updateConfigurationWith(configDict: ["messaging.useSandbox": true])` détermine si les notifications push utilisent un environnement de test APN ou un serveur de production pour envoyer des notifications push. Lors du test de votre application dans le simulateur ou sur un appareil, assurez-vous que `messaging.useSandbox` est défini sur `true` afin de recevoir des notifications push. Lors du déploiement de votre application pour production afin de tester à l’aide d’Apple Testflight, assurez-vous que vous avez défini `messaging.useSandbox` sur `false` sans quoi votre application de production ne pourra pas recevoir de notifications push.


## Créer votre propre notification push

Pour créer votre propre notification push, vous devez définir un événement dans Journey Optimizer qui déclenche un parcours chargé de l&#39;envoi d&#39;une notification push.

### Mettre à jour votre schéma

Vous allez définir un nouveau type d’événement, qui n’est pas encore disponible dans la liste des événements définis dans votre schéma. Vous utiliserez ce type d’événement ultérieurement lors du déclenchement des notifications push.

1. Dans l’interface utilisateur de Journey Optimizer, sélectionnez **[!UICONTROL Schémas]** dans le rail de gauche.
1. Sélectionnez **[!UICONTROL Parcourir]** dans la barre d’onglets.
1. Sélectionnez votre schéma, par exemple **[!DNL Luma Mobile App Event Schema]** pour l’ouvrir.
1. Dans l’éditeur de schémas :
   1. Sélectionnez le champ **[!UICONTROL eventType]** .
   1. Dans le volet **[!UICONTROL Propriétés du champ]**, faites défiler l’écran vers le bas pour afficher la liste des valeurs possibles pour le type d’événement. Sélectionnez **[!UICONTROL Ajouter une ligne]** et ajoutez `application.test` comme **[!UICONTROL VALUE]** et `[!UICONTROL Test event for push notification]` comme `DISPLAY NAME`.
   1. Sélectionnez **[!UICONTROL Appliquer]**.
   1. Sélectionnez **[!UICONTROL Enregistrer]**.
      ![Ajouter une valeur aux types d’événements](assets/ajo-update-schema-eventtype-enum.png)

### Définition d’un événement

Les événements dans Journey Optimizer vous permettent de déclencher vos parcours unitairement pour envoyer des messages, par exemple des notifications push. Voir [À propos des événements](https://experienceleague.adobe.com/docs/journey-optimizer/using/configuration/configure-journeys/events-journeys/about-events.html?lang=en) pour plus d’informations.

1. Dans l’interface utilisateur de Journey Optimizer, sélectionnez **[!UICONTROL Configurations]** dans le rail de gauche.

1. Dans l’écran **[!UICONTROL Tableau de bord]**, sélectionnez le bouton **[!UICONTROL Gérer]** dans la mosaïque **[!UICONTROL Événements]**.

1. Dans l’écran **[!UICONTROL Events]**, sélectionnez **[!UICONTROL Create Event]**.

1. Dans le volet **[!UICONTROL Edit event1]** :

   1. Saisissez `LumaTestEvent` comme **[!UICONTROL Nom]** de l’événement.
   1. Fournissez une **[!UICONTROL description]**, par exemple `Test event to trigger push notifications in Luma app`.

   1. Sélectionnez le schéma d’événement d’expérience d’application mobile que vous avez créé précédemment dans [Création d’un schéma XDM](create-schema.md) dans la liste **[!UICONTROL Schéma]**, par exemple **[!DNL Luma Mobile App Event Schema v.1]**.
   1. Sélectionnez ![Edit](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Edit_18_N.svg) en regard de la liste **[!UICONTROL Fields]**.

      ![Modifier l’étape 1](assets/ajo-edit-event1.png) de l’événement

      Dans la boîte de dialogue **[!UICONTROL Fields]**, assurez-vous que les champs suivants sont sélectionnés (en plus des champs par défaut toujours sélectionnés (**[!UICONTROL _id]**, **[!UICONTROL id]** et **[!UICONTROL timestamp]**). Vous pouvez basculer, à l’aide de la liste déroulante, entre **[!UICONTROL Sélectionné]**, **[!UICONTROL Tous]** et **[!UICONTROL Principal]** ou utiliser le champ ![Recherche](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Search_18_N.svg).

      * **[!UICONTROL Application identifiée (id)]**,
      * **[!UICONTROL Type d’événement (eventType)]**,
      * **[!UICONTROL Principal (principal)]**.

      ![Modifier les champs d’événement](assets/ajo-event-fields.png)

      Sélectionnez ensuite **[!UICONTROL Ok]**.

   1. Sélectionnez ![Edit](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Edit_18_N.svg) en regard du champ **[!UICONTROL Event id condition]**.

      1. Dans la boîte de dialogue **[!UICONTROL Ajouter une condition d’ID d’événement]**, placez **[!UICONTROL Type d’événement (eventType)]** sur **[!UICONTROL Faites glisser un élément ici]**.
      1. Dans la fenêtre contextuelle, faites défiler l’écran vers le bas et sélectionnez **[!UICONTROL application.test]** (qui est le type d’événement que vous avez ajouté précédemment à la liste des types d’événement dans le cadre de la [mise à jour de votre schéma](#update-your-schema)). Faites ensuite défiler l’écran jusqu’en haut et sélectionnez **[!UICONTROL Ok]**.
      1. Sélectionnez **[!UICONTROL Ok]** pour enregistrer la condition.
         ![Modifier la condition d’événement](assets/ajo-edit-condition.png)

   1. Sélectionnez **[!UICONTROL ECID (ECID)]** dans la liste **[!UICONTROL Espace de noms]**. Le champ **[!UICONTROL Identifiant du profil]** est automatiquement renseigné avec **[!UICONTROL l’identifiant du premier élément de l’ECID clé pour la carte identityMap]**.
   1. Sélectionnez **[!UICONTROL Enregistrer]**.
      ![Modifier l’étape 2](assets/ajo-edit-event2.png)

Vous venez de créer une configuration d’événement basée sur le schéma d’événements d’expérience d’application mobile que vous avez créé précédemment dans le cadre de ce tutoriel. Cette configuration d’événement filtrera les événements d’expérience entrants à l’aide de votre type d’événement spécifique (`application.test`). De ce fait, seuls les événements de ce type spécifique, initiés à partir de votre application mobile, déclencheront le parcours que vous créez à l’étape suivante. Dans un scénario réel, vous souhaiterez peut-être envoyer des notifications push depuis un service externe. Toutefois, les mêmes concepts s’appliquent : depuis l’application externe, envoyez un événement d’expérience dans un Experience Platform contenant des champs spécifiques sur lesquels vous pouvez appliquer des conditions avant que ces événements ne déclenchent un parcours.

### Création du parcours

L’étape suivante consiste à créer le parcours qui déclenche l’envoi de la notification push lors de la réception de l’événement approprié.

1. Dans l’interface utilisateur de Journey Optimizer, sélectionnez **[!UICONTROL Parcours]** dans le rail de gauche.
1. Sélectionnez **[!UICONTROL Créer un Parcours]**.
1. Dans le panneau **[!UICONTROL Propriétés du Parcours]** :

   1. Saisissez un **[!UICONTROL Nom]** pour le parcours, par exemple `Luma - Test Push Notification Journey`.
   1. Saisissez une **[!UICONTROL Description]** pour le parcours, par exemple `Journey for test push notifications in Luma mobile app`.
   1. Assurez-vous que l’option **[!UICONTROL Autoriser la rentrée]** est sélectionnée et définissez la **[!UICONTROL Période d’attente de rentrée]** sur **[!UICONTROL 30]** **[!UICONTROL Secondes]**.
   1. Cliquez sur **[!UICONTROL OK]**.
      ![Propriétés du parcours](assets/ajo-journey-properties.png)

1. De retour dans la zone de travail du parcours, à partir de **[!UICONTROL EVENTS]**, effectuez un glisser-déposer de votre ![événement](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Globe_18_N.svg) **[!DNL LumaTestEvent]** sur la zone de travail où se trouve **[!UICONTROL Sélectionner un événement d’entrée ou une activité de lecture d’audience]**.

   * Dans le panneau **[!UICONTROL Events: LumaTestEvent]** , saisissez un **[!UICONTROL libellé]**, par exemple `Luma Test Event`.

1. Dans la liste déroulante **[!UICONTROL ACTIONS]**, effectuez un glisser-déposer de ![Push](https://spectrum.adobe.com/static/icons/workflow_18/Smock_PushNotification_18_N.svg) **[!UICONTROL Push]** sur l’écran ![Ajouter](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) apparaissant à droite de votre activité **[!DNL LumaTestEvent]**. Dans le volet **[!UICONTROL Actions : Push]** :

   1. Fournissez un **[!UICONTROL libellé]**, par exemple `Luma Test Push Notification`, fournissez une **[!UICONTROL description]**, par exemple `Test push notification for Luma mobile app`, sélectionnez **[!UICONTROL Transactional]** dans la liste **[!UICONTROL Category]** et sélectionnez **[!DNL Luma]** dans la **[!UICONTROL surface push]**.
   1. Sélectionnez ![Modifier](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Edit_18_N.svg) **[!UICONTROL Modifier le contenu]** pour commencer à modifier la notification push réelle.
      ![Propriétés push](assets/ajo-push-properties.png)

      Dans l’éditeur **[!UICONTROL Notification push]** :

      1. Saisissez un **[!UICONTROL Titre]**, par exemple `Luma Test Push Notification`, puis un **[!UICONTROL Corps]**, par exemple `Test push notification for Luma mobile app`.
      1. Vous pouvez éventuellement saisir un lien vers une image (.png ou .jpg) dans **[!UICONTROL Ajouter un média]**. Si vous le faites, l’image fera partie de la notification push.
      1. Pour enregistrer et quitter l’éditeur, sélectionnez ![Chevron left](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ChevronLeft_18_N.svg).
         ![Éditeur push](assets/ajo-push-editor.png)

   1. Pour enregistrer et terminer la définition de notification push, sélectionnez **[!UICONTROL Ok]**.

1. Votre parcours devrait ressembler à celui-ci. Sélectionnez **[!UICONTROL Publish]** pour publier et activer votre parcours.
   ![parcours terminé](assets/ajo-journey-finished.png)


## Déclencher la notification push

Vous avez tous les ingrédients en place pour envoyer une notification push. Reste à savoir comment déclencher cette notification push. Essentiellement, c’est la même chose que précédemment : envoyez simplement un événement d’expérience avec la charge utile appropriée (comme dans [Events](events.md)).

Cette fois, l’événement d’expérience que vous êtes sur le point d’envoyer n’est pas créé en créant un dictionnaire XDM simple. Vous allez utiliser un `struct` représentant une payload de notification push. La définition d’un type de données dédié est une autre manière de mettre en oeuvre la création de payloads d’événement d’expérience dans votre application.

1. Accédez à **[!DNL Luma]** > **[!DNL Luma]** > **[!UICONTROL Modèle]** > **[!UICONTROL XDM]** > **[!UICONTROL TestPushPayload]** dans le navigateur de projet Xcode et inspectez le code.

   ```swift
   import Foundation
   
   // MARK: - TestPush
   struct TestPushPayload: Codable {
      let application: Application
      let eventType: String
   }
   
   // MARK: - Application
   struct Application: Codable {
      let id: String
   }
   ```

   Le code est une représentation de la payload simple suivante que vous allez envoyer pour déclencher votre parcours de notification push de test.

   ```json
   {
      "eventType": string,
      "application" : [
          "id": string
      ]
   }
   ```

1. Accédez à **[!DNL Luma]** > **[!DNL Luma]** > **[!DNL Utils]** > **[!UICONTROL MobileSDK]** dans le navigateur de projet Xcode et ajoutez le code suivant à `func sendTestPushEvent(applicationId: String, eventType: String)` :

   ```swift
   // Create payload and send experience event
   Task {
       let testPushPayload = TestPushPayload(
           application: Application(
               id: applicationId
           ),
           eventType: eventType
       )
       // send the final experience event
       await sendExperienceEvent(
           xdm: testPushPayload.asDictionary() ?? [:]
       )
   }
   ```

   Ce code crée une instance `testPushPayload` à l’aide des paramètres fournis à la fonction (`applicationId` et `eventType`), puis appelle `sendExperienceEvent` lors de la conversion de la charge utile en dictionnaire. Cette fois-ci, ce code prend également en compte les aspects asynchrones de l’appel du SDK Adobe Experience Platform en utilisant le modèle d’accès simultané de Swift basé sur `await` et `async`.

1. Accédez à **[!DNL Luma]** > **[!DNL Luma]** > **[!DNL Views]** > **[!DNL General]** > **[!UICONTROL ConfigView]** dans le navigateur de projet Xcode. Dans la définition du bouton de notification push, ajoutez le code suivant pour envoyer la payload de l’événement d’expérience de notification push de test afin de déclencher votre parcours lorsque ce bouton est activé.

   ```swift
   // Setting parameters and calling function to send push notification
   Task {
       let eventType = testPushEventType
       let applicationId = Bundle.main.bundleIdentifier ?? "No bundle id found"
       await MobileSDK.shared.sendTestPushEvent(applicationId: applicationId, eventType: eventType)
   }
   ```


## Validation à l’aide de votre application

1. Recréez et exécutez l’application dans le simulateur ou sur un appareil physique à partir de Xcode, en utilisant ![Play](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Play_18_N.svg).

1. Accédez à l’onglet **[!UICONTROL Paramètres]** .

1. Appuyez sur **[!UICONTROL Notification push]**. La notification push apparaît dans votre application.

   <img src="assets/ajo-test-push.png" width="300" />


## Étapes suivantes

Vous devriez maintenant disposer de tous les outils pour gérer les notifications push dans votre application. Par exemple, vous pouvez créer dans Journey Optimizer un parcours qui envoie une notification push de bienvenue lorsqu’un utilisateur de l’application se connecte. Ou une notification push de confirmation lorsqu’un utilisateur achète un produit dans l’application. Ou entre dans la clôture virtuelle d’un emplacement (comme vous le verrez dans la leçon [Places](places.md)).

>[!SUCCESS]
>
>Vous avez maintenant activé l’application pour la notification push à l’aide de Journey Optimizer et de l’extension Journey Optimizer pour le SDK Mobile Experience Platform.
>
>Merci d’investir votre temps à apprendre sur le SDK Adobe Experience Platform Mobile. Si vous avez des questions, souhaitez partager des commentaires généraux ou avez des suggestions sur le contenu à venir, partagez-les sur cet [post de discussion de la communauté Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796).

Suivant : **[Créer et envoyer des messages in-app](journey-optimizer-inapp.md)**
