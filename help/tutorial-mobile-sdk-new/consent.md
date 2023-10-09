---
title: Mise en oeuvre du consentement
description: Découvrez comment mettre en oeuvre le consentement dans une application mobile.
feature: Mobile SDK,Consent
hide: true
exl-id: 83f240ea-ea18-4986-9e89-5110a56167ce
source-git-commit: d7410a19e142d233a6c6597de92f112b961f5ad6
workflow-type: tm+mt
source-wordcount: '558'
ht-degree: 1%

---

# Mise en oeuvre du consentement

Découvrez comment mettre en oeuvre le consentement dans une application mobile.

L’extension mobile de consentement Adobe Experience Platform permet la collecte des préférences de consentement de votre application mobile lors de l’utilisation du SDK Mobile Adobe Experience Platform et de l’extension Edge Network. En savoir plus sur les [Extension de consentement](https://developer.adobe.com/client-sdks/documentation/consent-for-edge-network/), dans la documentation.

## Conditions préalables

* Création et exécution de l’application avec les SDK installés et configurés.

## Objectifs d&#39;apprentissage

Dans cette leçon, vous allez :

* Demandez à l’utilisateur son consentement.
* Mettez à jour l’extension selon la réponse de l’utilisateur.
* Découvrez comment obtenir l’état actuel du consentement.

## Demander le consentement

Si vous avez suivi le tutoriel depuis le début, vous vous souvenez peut-être que vous avez défini le consentement par défaut dans l’extension Consentement sur **[!UICONTROL En attente : événements de file d’attente qui se produisent avant que l’utilisateur ne fournisse ses préférences de consentement.]**

Pour commencer à collecter des données, vous devez obtenir le consentement de l’utilisateur. Dans une application réelle, vous souhaiteriez consulter les bonnes pratiques en matière de consentement pour votre région. Dans ce tutoriel, vous obtenez le consentement de l’utilisateur en le demandant simplement avec une alerte :

1. Vous ne souhaitez demander le consentement de l’utilisateur qu’une seule fois. Vous souhaitez donc combiner le consentement du SDK Mobile avec les autorisations requises pour le suivi à l’aide d’Apple [Structure de transparence du suivi des applications](https://developer.apple.com/documentation/apptrackingtransparency). Dans cette application, supposons que lorsque l’utilisateur autorise le suivi, il consent également à la collecte des événements.

1. Accédez à **[!DNL Luma]** > **[!DNL Luma]** > **[!DNL Utils]** > **[!UICONTROL MobileSDK]** dans le navigateur de projet Xcode.

   Ajoutez ce code à la variable `updateConsent` de la fonction

   ```swift
   // Update consent
   let collectConsent = ["collect": ["val": value]]
   let currentConsents = ["consents": collectConsent]
   Consent.update(with: currentConsents)
   MobileCore.updateConfigurationWith(configDict: currentConsents)
   ```

1. Accédez à **[!DNL Luma]** > **[!DNL Luma]** > **[!DNL Views]** > **[!DNL General]** > **[!UICONTROL DisresponsabilitéView]** dans le navigateur de projet de Xcode, qui est la vue affichée après l’installation ou la réinstallation de l’application et le démarrage initial de l’application. L’utilisateur est invité à autoriser le suivi par Apple. [Structure de transparence du suivi des applications](https://developer.apple.com/documentation/apptrackingtransparency). Si l’utilisateur l’autorise, vous mettez également à jour le consentement.

   Ajoutez le code suivant au `ATTrackingManager.requestTrackingAuthorization { status in` fermeture.

   ```swift
   // Add consent based on authorization
   if status == .authorized {
      // Set consent to yes
      MobileSDK.shared.updateConsent(value: "y")
   }
   else {
      // Set consent to yes
      MobileSDK.shared.updateConsent(value: "n")
   }
   ```

## Obtention de l’état du consentement actuel

L’extension mobile Consent supprime/met en attente/permet le suivi en fonction de la valeur de consentement actuelle. Vous pouvez également accéder vous-même à l’état actuel du consentement :

1. Accédez à **[!DNL Luma]** > **[!DNL Luma]** > **[!DNL Utils]** > **[!UICONTROL MobileSDK]** dans le navigateur de projet de Xcode.

   Ajoutez le code suivant au `getConsents` function:

   ```swift
   // Get consents
   Consent.getConsents { consents, error in
      guard error == nil, let consents = consents else { return }
      guard let jsonData = try? JSONSerialization.data(withJSONObject: consents, options: .prettyPrinted) else { return }
      guard let jsonStr = String(data: jsonData, encoding: .utf8) else { return }
      Logger.aepMobileSDK.info("Consent getConsents: \(jsonStr)")
   }
   ```

2. Accédez à **[!DNL Luma]** > **[!DNL Luma]** > **[!DNL Views]** > **[!DNL General]** > **[!UICONTROL HomeView]** dans le navigateur de projet de Xcode.

   Ajoutez le code suivant au `.task` modifier :

   ```swift
   // Ask status of consents
   MobileSDK.shared.getConsents()   
   ```

Dans l’exemple ci-dessus, vous enregistrez simplement l’état du consentement sur la console dans Xcode. Dans un scénario réel, vous pouvez l’utiliser pour modifier les menus ou options affichés à l’utilisateur.

## Validation avec Assurance

1. Consultez la section [instructions de configuration](assurance.md#connecting-to-a-session) pour connecter le simulateur ou l’appareil à Assurance.
1. Si vous avez correctement ajouté le code ci-dessus, vous êtes invité à fournir votre consentement.

   Sélectionner **[!UICONTROL Continuer...]** puis sélectionnez **[!UICONTROL Autoriser]**.

   <img src="./assets/consent-update-1.png" width="300" /> 
   <img src="./assets/consent-update-2.png" width="300" />

1. Vous devriez voir une **[!UICONTROL Obtenir une réponse de consentement]** dans l’interface utilisateur d’Assurance.
   ![valider le consentement](assets/consent-update.png)


## Réinitialiser le consentement

Si vous souhaitez réinitialiser le consentement :

1. Accédez à **[!UICONTROL Paramètres]** dans l’application.

1. Sélectionner **[!UICONTROL Paramètres de l’application...]** Les paramètres de l’application Luma s’affichent alors dans l’application Paramètres d’iOS.

1. Basculer **[!UICONTROL Autoriser le suivi]** off.



>[!SUCCESS]
>
>Vous avez maintenant activé votre application pour inviter l’utilisateur à son démarrage initial après l’installation (ou la réinstallation) à consentir à l’aide du SDK Adobe Experience Platform Mobile.<br/>Merci d’investir votre temps à apprendre sur le SDK Adobe Experience Platform Mobile. Si vous avez des questions, souhaitez partager des commentaires généraux ou avez des suggestions sur le contenu futur, partagez-les à ce sujet. [Article de discussion de la communauté Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796)

Suivant : **[Collecter les données du cycle de vie](lifecycle-data.md)**
