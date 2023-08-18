---
title: Messagerie push Adobe Journey Optimizer
description: Découvrez comment créer des messages push vers une application mobile à l’aide du SDK Mobile Platform et de Adobe Journey Optimizer.
solution: Data Collection,Journey Optimizer
feature-set: Journey Optimizer
feature: Push
hide: true
hidefromtoc: true
source-git-commit: ca83bbb571dc10804adcac446e2dba4fda5a2f1d
workflow-type: tm+mt
source-wordcount: '942'
ht-degree: 4%

---

# Messagerie push Adobe Journey Optimizer

Découvrez comment créer des messages push pour les applications mobiles avec le SDK Mobile Platform et Adobe Journey Optimizer.

Journey Optimizer vous permet de créer vos parcours et d’envoyer des messages à des audiences ciblées. Avant d’envoyer des notifications push avec Journey Optimizer, vous devez vous assurer que les configurations et intégrations appropriées sont en place. Pour comprendre le flux de données des notifications push dans Adobe Journey Optimizer, voir [la documentation](https://experienceleague.adobe.com/docs/journey-optimizer/using/configuration/configuration-message/push-config/push-gs.html).

>[!NOTE]
>
>Cette leçon est facultative et s’applique uniquement aux utilisateurs de Adobe Journey Optimizer qui souhaitent envoyer des messages push.


## Conditions préalables

* Création et exécution de l’application avec les SDK installés et configurés.
* Accès à Adobe Journey Optimizer et autorisations suffisantes, comme décrit [here](https://experienceleague.adobe.com/docs/journey-optimizer/using/configuration/configuration-message/push-config/push-configuration.html?lang=en). Vous avez également besoin d’autorisations suffisantes pour les fonctionnalités Adobe Journey Optimizer suivantes.
   * Créez une surface d’application.
   * Créer un parcours
   * Créez un message.
   * Création de préréglages de message.
* Compte de développeur Apple payant disposant d’un accès suffisant pour créer des certificats, identifiants et clés.
* Appareil iOS physique à tester.

## Objectifs d&#39;apprentissage

Dans cette leçon, vous allez :

* Enregistrez l’ID d’application avec le service Apple Push Notification (APN).
* Créez un **[!UICONTROL Surface de l’application]** dans AJO.
* Mettez à jour votre **[!UICONTROL schema]** pour inclure des champs de messagerie push.
* Installez et configurez la variable **[!UICONTROL Adobe Journey Optimizer]** extension de balise.
* Mettez à jour votre application pour inclure l’extension de balise AJO.
* Validez la configuration dans Assurance.
* Envoyez un message de test.


## Enregistrement de l’ID d’application avec l’APN

Les étapes suivantes ne sont pas spécifiques à Adobe Experience Cloud et sont conçues pour vous guider tout au long de la configuration de l’APN.

### Création d’une clé privée

1. Sur le portail destiné aux développeurs Apple, accédez à **[!UICONTROL Clés]**.
1. Pour créer une clé, sélectionnez **[!UICONTROL +]**.
   ![créer une clé](assets/mobile-push-apple-dev-new-key.png)

1. Fournissez une **[!UICONTROL Nom de la clé]**.
1. Sélectionnez la variable **[!UICONTROL APN]** .
1. Sélectionnez **[!UICONTROL Continuer]**.
   ![configurer la nouvelle clé](assets/mobile-push-apple-dev-config-key.png)
1. Vérifiez la configuration et sélectionnez **[!UICONTROL Enregistrer]**.
1. Téléchargez la `.p8` clé privée. Il est utilisé dans la configuration Surface de l’application.
1. Prenez note de la [!UICONTROL ID de clé]. Il est utilisé dans la configuration Surface de l’application.
1. Prenez note de la [!UICONTROL Identifiant de l’équipe]. Il est utilisé dans la configuration Surface de l’application.
   ![Détails clés](assets/push-apple-dev-key-details.png)

Une documentation supplémentaire peut être [se trouve ici](https://help.apple.com/developer-account/#/devcdfbb56a3).

## Ajout des informations d’identification push de votre application à la collecte de données

1. Dans la [Interface de collecte de données](https://experience.adobe.com/data-collection/), sélectionnez **[!UICONTROL Surfaces de l’application]** dans le panneau de gauche.
1. Pour créer une configuration, sélectionnez **[!UICONTROL Création de surfaces d’application]**.
   ![page d’accueil de l’application](assets/push-app-surface.png)
1. Saisissez un **[!UICONTROL Nom]** pour la configuration, par exemple `Luma App Tutorial`  .
1. Dans Configuration de l’application mobile, sélectionnez **[!UICONTROL Apple iOS]**.
1. Renseignez l&#39;ID de bundle de l&#39;application mobile dans le champ ID de l&#39;application (ID de bundle iOS). Si vous suivez l’application Luma, cette valeur est `com.adobe.luma.tutorial.swiftui`.
1. Activez l’option **[!UICONTROL Informations d’identification push]** pour ajouter vos informations d’identification.
1. Faites glisser et déposez votre `.p8` **Clé d’authentification des notifications push Apple** fichier .
1. Fournissez les **[!UICONTROL ID de clé]**, chaîne de 10 caractères attribuée lors de la création de la variable `p8` clé auth. Il se trouve sous **[!UICONTROL Clés]** dans **Certificats, identifiants et profils** page des pages du portail des développeurs Apple.
1. Indiquez l&#39;**[!UICONTROL identifiant d&#39;équipe]**. L’ ID d’équipe est une valeur qui se trouve sous la variable **Abonnement** ou dans la partie supérieure des pages du portail des développeurs Apple.
1. Sélectionnez **[!UICONTROL Enregistrer]**.

   ![configuration de la surface de l’application](assets/push-app-surface-config.png)

## Installation de l’extension de balises Adobe Journey Optimizer

1. Accédez à **[!UICONTROL Balises]** > **[!UICONTROL Extensions]** > **[!UICONTROL Catalogue]**,
1. Ouvrez votre propriété, par exemple **[!UICONTROL Tutoriel sur l’application mobile Luma]**.
1. Sélectionner **[!UICONTROL Catalogue]**.
1. Recherchez le **[!UICONTROL Adobe Journey Optimizer]** extension .
1. Installation l’extension.
1. Dans le **[!UICONTROL Installer l’extension]** dialog
   1. Sélectionnez un environnement, par exemple **[!UICONTROL Développement]**.
   1. Sélectionnez la variable **[!UICONTROL Jeu de données d’événement de suivi push AJO]** jeu de données à partir du **[!UICONTROL Jeu de données d’événement]** liste déroulante
      ![Paramètres de l’extension AJO](assets/push-tags-ajo.png)
   1. Sélectionner **[!UICONTROL Enregistrer dans la bibliothèque et créer]**.

>[!NOTE]
>
>Si vous ne voyez pas `AJO Push Tracking Experience Event Dataset` contactez l’assistance clientèle.
>

## Mise en oeuvre de Adobe Journey Optimizer dans l’application

Comme indiqué dans les leçons précédentes, l’installation d’une extension de balise mobile fournit uniquement la configuration. Vous devez ensuite installer et enregistrer le SDK de messagerie. Si ces étapes ne sont pas claires, passez en revue la [Installation des SDK](install-sdks.md) .

>[!NOTE]
>
>Si vous avez terminé la [Installation des SDK](install-sdks.md) , le SDK est déjà installé et vous pouvez passer à l’étape #7.
>

1. Dans Xcode, assurez-vous que [Messagerie AEP](https://github.com/adobe/aepsdk-messaging-ios.git) est ajouté à la liste des modules dans les dépendances de modules. Voir [Swift Package Manager](install-sdks.md#swift-package-manager).
1. Ouvrez Xcode et accédez à **[!UICONTROL AppDelegate]**.
1. Assurez-vous que `AEPMessaging` fait partie de votre liste d’importations.

   `import AEPMessaging`

1. Assurez-vous que `Messaging.self` fait partie du tableau des extensions que vous enregistrez.

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

1. Ajoutez la variable `MobileCore.setPushIdentifier` à la fonction `application(_, didRegisterForRemoteNotificationsWithDeviceToken)` de la fonction

   ```swift {highlight="7"}
   func application(_ application: UIApplication, didRegisterForRemoteNotificationsWithDeviceToken deviceToken: Data) {
       // Required to log the token
       let tokenParts = deviceToken.map { data in String(format: "%02.2hhx", data) }
       let token = tokenParts.joined()
       Logger.notifications.info("didRegisterForRemoteNotificationsWithDeviceToken - device token: \(token)")
   
       // Send push token to Experience Platform
       MobileCore.setPushIdentifier(deviceToken)
       currentDeviceToken = token
   }
   ```

   Cette fonction récupère le jeton de l’appareil unique sur lequel l’application est installée et envoie le jeton à Adobe Apple pour la diffusion des messages push.

## Validation en envoyant un message push de test

1. Consultez la section [instructions de configuration](assurance.md) .
1. Installez l’application sur votre appareil physique ou sur le simulateur.
1. Lancez l’application à l’aide de l’URL générée par Assurance.
1. Dans l’interface utilisateur d’assurance, sélectionnez **[!UICONTROL Configurer]**.
   ![configurer le clic](assets/push-validate-config.png)
1. Sélectionnez la variable ![Plus](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) bouton en regard de **[!UICONTROL Débogage Push]**.
1. Sélectionnez **[!UICONTROL Enregistrer]**.
   ![save](assets/push-validate-save.png)
1. Sélectionner **[!UICONTROL Débogage Push]** dans le volet de navigation de gauche.
1. Sélectionnez la variable **[!UICONTROL Validation de la configuration]** .
1. Sélectionnez votre périphérique dans le **[!UICONTROL Client]** liste.
1. Confirmez que vous n’obtenez aucune erreur.
   ![validate](assets/push-validate-confirm.png)
1. Sélectionnez la variable **[!UICONTROL Envoyer le test push]** .
1. (Facultatif) Modifiez les détails par défaut de la variable **[!UICONTROL Titre]** et **[!UICONTROL Corps]**
1. Sélectionner ![Bogue](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Bug_18_N.svg) **[!UICONTROL Envoi de la notification push de test]**.
1. Vérifiez les **[!UICONTROL Résultats du test]**.
1. La notification push devrait apparaître dans votre application.

   <img src="assets/luma-app-push.png" width="300" />


>[!SUCCESS]
>
>Vous avez maintenant activé l’application pour la notification push à l’aide de l’extension Adobe Journey Optimizer pour le SDK Adobe Experience Platform Mobile.<br/>Merci d’investir votre temps à apprendre sur le SDK Adobe Experience Platform Mobile. Si vous avez des questions, souhaitez partager des commentaires généraux ou avez des suggestions sur le contenu futur, partagez-les à ce sujet. [Article de discussion de la communauté Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796).

Suivant : **[Conclusion et prochaines étapes](conclusion.md)**
