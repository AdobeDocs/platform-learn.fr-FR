---
title: Messagerie push Adobe Journey Optimizer
description: Découvrez comment créer des messages push vers une application mobile à l’aide du SDK Mobile Platform et de Adobe Journey Optimizer.
exl-id: e8e920d5-fd36-48b7-9185-a34231c0d336
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '881'
ht-degree: 6%

---

# Messagerie push Adobe Journey Optimizer

Découvrez comment créer des messages push pour les applications mobiles avec le SDK Mobile Platform et Adobe Journey Optimizer.

Journey Optimizer vous permet de créer vos parcours et d’envoyer des messages à des audiences ciblées. Avant d’envoyer des notifications push avec Journey Optimizer, vous devez vous assurer que les configurations et intégrations appropriées sont en place. Pour comprendre le flux de données des notifications push dans Adobe Journey Optimizer, reportez-vous à la section [la documentation](https://experienceleague.adobe.com/docs/journey-optimizer/using/configuration/configuration-message/push-config/push-gs.html).

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
* Compte de développeur Apple payant disposant d’un accès suffisant pour créer des certificats, des identifiants et des clés.
* Appareil iOS physique à des fins de test.

## Objectifs d&#39;apprentissage

Dans cette leçon, vous allez :

* Enregistrez l’ID d’application avec le service Apple Push Notification (APN).
* Créez un **[!UICONTROL Surface de l’application]** dans AJO.
* Mettez à jour votre **[!UICONTROL schema]** pour inclure des champs de messagerie push.
* Installez et configurez le **[!UICONTROL Adobe Journey Optimizer]** extension de balise.
* Mettez à jour votre application pour inclure l’extension de balise AJO.
* Validez la configuration dans Assurance.
* Envoyez un message de test.


## Enregistrement de l’ID d’application avec APN

Les étapes suivantes ne sont pas spécifiques à Adobe Experience Cloud et sont conçues pour vous guider tout au long de la configuration APN.

### Créez un `.p8` clé privée

1. Sur le portail destiné aux développeurs Apple, accédez à **[!UICONTROL Clés]**.
1. Sélectionnez l’icône + pour créer une clé.
   ![créer une clé](assets/mobile-push-apple-dev-new-key.png)

1. Fournissez une **[!UICONTROL Nom de la clé]**.
1. Sélectionnez la **[!UICONTROL APN]** .
1. Sélectionnez **[!UICONTROL Continuer]**.
   ![configurer la nouvelle clé](assets/mobile-push-apple-dev-config-key.png)
1. Vérifiez la configuration et sélectionnez **[!UICONTROL Enregistrer]**.
1. Téléchargez la `.p8` clé privée. Il est utilisé dans la configuration Surface de l’application.
1. Prenez note de la **[!UICONTROL ID de clé]**. Il est utilisé dans la configuration Surface de l’application.

Une documentation supplémentaire peut être [ici](https://help.apple.com/developer-account/#/devcdfbb56a3).

### Récupération de votre identifiant d’équipe de développement Apple

1. Sur le portail destiné aux développeurs Apple, accédez à **[!UICONTROL Abonnement]**.
1. Votre **[!UICONTROL Identifiant de l’équipe]** est répertorié avec vos autres informations d’adhésion. Il est utilisé dans la configuration Surface de l’application.

## Ajout des informations d’identification push de votre application à la collecte de données

1. Dans la [Interface de collecte de données](https://experience.adobe.com/data-collection/), sélectionnez l’onglet Surfaces de l’application dans le panneau de gauche.
1. Sélectionner **[!UICONTROL Création de surfaces d’application]** pour créer une configuration.
   ![page d’accueil de l’application](assets/mobile-push-app-surface.png)
1. Saisissez un **[!UICONTROL Nom]** pour la configuration, par exemple `Luma App Tutorial`  .
1. Dans Configuration de l’application mobile, sélectionnez **[!UICONTROL Apple iOS]**.
1. Renseignez l&#39;ID de bundle de l&#39;application mobile dans le champ ID de l&#39;application (ID de bundle iOS). Si vous suivez l’application Luma, cette valeur est `com.adobe.luma.tutorial`.
1. Activez l’option **[!UICONTROL Informations d’identification push]** pour ajouter vos informations d’identification.
1. Faites glisser et déposez votre `.p8` **Clé d’authentification des notifications push Apple** fichier .
1. Fournissez l’ID de clé, une chaîne de 10 caractères attribuée lors de la création de la variable `p8` clé auth. Elle se trouve sous l&#39;onglet Clés de la page **Certificats, Identifiants et Profils**.
1. Indiquez l&#39;identifiant d&#39;équipe. Il s’agit d’une valeur string qui se trouve sous la propriété **Abonnement** .
1. Sélectionnez **[!UICONTROL Enregistrer]**.
   ![configuration de la surface de l’application](assets/mobile-push-app-surface-config.png)

## Installation de l’extension de balises Adobe Journey Optimizer

1. Accédez à [!UICONTROL Balises] > [!UICONTROL Extensions] > [!UICONTROL Catalogue], puis recherchez la variable **[!UICONTROL Adobe Journey Optimizer]** extension .
1. Installer l’extension.
   ![installation de l’extension ajo](assets/mobile-push-tags-install.png)
1. Sélectionner `CJM Push Tracking Experience Event Dataset` le jeu de données Adobe Experience Platform.
   ![Paramètres de l’extension AJO](assets/mobile-push-tags-ajo.png)
1. Sélectionner **[!UICONTROL Enregistrer dans la bibliothèque et créer]**.

>[!NOTE]
>Si vous ne voyez pas l’option &quot;Jeu de données d’événement d’expérience de suivi Push CJM&quot; comme option, contactez l’assistance clientèle.

## Mise en oeuvre de Adobe Journey Optimizer dans l’application

Comme indiqué dans les leçons précédentes, l’installation d’une extension de balise mobile fournit uniquement la configuration. Vous devez ensuite installer et enregistrer le SDK de messagerie. Si ces étapes ne sont pas claires, veuillez consulter la section [Installation des SDK](install-sdks.md) .

>[!NOTE]
>
>Si vous avez terminé la [Installation des SDK](install-sdks.md) , le SDK est déjà installé et vous pouvez passer à l’étape #7.

1. Ouvrez votre `Podfile` et ajoutez la ligne suivante et enregistrez le fichier.

   `pod 'AEPMessaging', '~>1'`
1. Ouvrez votre terminal et accédez au dossier contenant votre `Podfile`.
1. Installation du SDK en exécutant la commande `pod install`.
   ![valider le consentement](assets/mobile-push-terminal-install.png)
1. Ouvrez XCode et accédez à `AppDelegate.swift`.
1. Ajoutez ce qui suit à votre liste d&#39;imports.

   `import AEPMessaging`
1. Ajouter `Messaging.self` au tableau des extensions que vous enregistrez.
1. Ajoutez la fonction suivante au fichier.

   ```swift
   func application(_: UIApplication, didRegisterForRemoteNotificationsWithDeviceToken deviceToken: Data) {
       MobileCore.setPushIdentifier(deviceToken)
   }
   ```

   Cette fonction récupère le jeton de l’appareil unique sur lequel l’application est installée et l’envoie à Adobe/Apple pour la diffusion des messages push.

## Validation en envoyant un message push de test

1. Consultez la section [instructions de configuration](assurance.md) .
1. Installez l’application sur votre appareil physique.
1. Lancez l’application à l’aide de l’URL générée par Assurance.
1. Envoyez l’application en arrière-plan.
1. Dans l’interface utilisateur d’assurance, sélectionnez **[!UICONTROL Configurer]**.
   ![configurer le clic](assets/mobile-push-validate-config.png)
1. Sélectionnez la **[!UICONTROL +]** bouton en regard de **[!UICONTROL Débogage Push]**.
1. Sélectionnez **[!UICONTROL Enregistrer]**.
   ![save](assets/mobile-push-validate-save.png)
1. Sélectionner **[!UICONTROL Débogage Push]** dans le volet de navigation de gauche.
1. Sélectionnez votre périphérique dans le **[!UICONTROL Liste cliente]**.
1. Confirmez que vous n’obtenez aucune erreur.
   ![validate](assets/mobile-push-validate-confirm.png)
1. Faites défiler la page vers le bas et sélectionnez **[!UICONTROL Envoi de la notification push de test]**.
1. Vérifiez que vous ne recevez pas d’erreurs et et que vous recevez le message sur votre appareil.
   ![envoyer un test push](assets/mobile-push-validate-send-test.png)

Suivant : **[Conclusion et prochaines étapes](conclusion.md)**

>[!NOTE]
>
>Merci d’avoir consacré votre temps à l’apprentissage du SDK Adobe Experience Platform Mobile. Si vous avez des questions, souhaitez partager des commentaires généraux ou avez des suggestions sur le contenu futur, partagez-les à ce sujet. [Article de discussion de la communauté Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796)