---
title: Consentement
description: Découvrez comment mettre en oeuvre le consentement dans une application mobile.
feature: Mobile SDK,Consent
hide: true
source-git-commit: 4101425bd97e271fa6cc15157a7be435c034e764
workflow-type: tm+mt
source-wordcount: '535'
ht-degree: 2%

---

# Consentement

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

Pour commencer à collecter des données, vous devez obtenir le consentement de l’utilisateur. Dans ce tutoriel, vous obtenez le consentement de l’utilisateur en le demandant simplement avec une alerte. Dans une application réelle, vous souhaitez consulter les bonnes pratiques en matière de consentement pour votre région.

1. Vous ne souhaitez demander à l’utilisateur qu’une seule fois. Vous souhaitez donc combiner le consentement du SDK Mobile avec les autorisations requises pour le suivi à l’aide d’Apple [Structure de transparence du suivi des applications](https://developer.apple.com/documentation/apptrackingtransparency). Dans cette application, supposons que lorsque l’utilisateur autorise le suivi, il consent également à la collecte des événements.

1. Accédez à **[!UICONTROL Luma]** > **[!UICONTROL Luma]** > **[!UICONTROL Utils]** > **[!UICONTROL MobileSDK]** dans le navigateur de projet Xcode.

   Ajoutez ce code à la variable `updateConsent` de la fonction

   ```swift
   let collectConsent = ["collect": ["val": value]]
   let currentConsents = ["consents": collectConsent]
   Consent.update(with: currentConsents)
   MobileCore.updateConfigurationWith(configDict: currentConsents)
   ```

1. Accédez à **[!UICONTROL Luma]** > **[!UICONTROL Luma]** > **[!UICONTROL Vues]** > **[!UICONTROL Général]** > **[!UICONTROL DisresponsabilitéView]** dans le navigateur de projet de Xcode, qui est la vue affichée après l’installation ou la réinstallation de l’application et le démarrage initial de l’application. L’utilisateur est invité à autoriser le suivi par Apple. [Structure de transparence du suivi des applications](https://developer.apple.com/documentation/apptrackingtransparency). Si l’utilisateur l’autorise, vous mettez également à jour le consentement.

   Ajoutez le code suivant au `ATTrackingManager.requestTrackingAuthorization { status in` fermeture.

   ```swift
   if status == .authorized {
         // Set consent to yes
         MobileSDK.shared.updateConsent(value: "y")
   }
   else {
         MobileSDK.shared.updateConsent(value: "n")
   }
   ```

## Obtention de l’état du consentement actuel

L’extension mobile Consent supprime/met en attente/permet le suivi en fonction de la valeur de consentement actuelle. Vous pouvez également accéder vous-même à l’état actuel du consentement :

1. Accédez à **[!UICONTROL Luma]** > **[!UICONTROL Luma]** > **[!UICONTROL Utils]** > **[!UICONTROL MobileSDK]** dans le navigateur de projet de Xcode.

   Ajoutez le code suivant au `getConsents` function:

   ```swift
   Consent.getConsents { consents, error in
      guard error == nil, let consents = consents else { return }
      guard let jsonData = try? JSONSerialization.data(withJSONObject: consents, options: .prettyPrinted) else { return }
      guard let jsonStr = String(data: jsonData, encoding: .utf8) else { return }
      Logger.aepMobileSDK.info("Consent getConsents: \(jsonStr)")
   }
   ```

2. Accédez à **[!UICONTROL Luma]** > **[!UICONTROL Luma]** > **[!UICONTROL Vues]** > **[!UICONTROL Général]** > **[!UICONTROL HomeView]** dans le navigateur de projet de Xcode.

   Ajoutez le code suivant au `.task` modifier :

   ```swift
   // Ask status of consents
   MobileSDK.shared.getConsents()   
   ```

Dans l’exemple ci-dessus, vous enregistrez simplement l’état du consentement sur la console dans Xcode. Dans un scénario réel, vous pouvez l’utiliser pour modifier les menus ou options affichés à l’utilisateur.

## Validation avec Assurance

1. Consultez la section [Assurance](assurance.md) leçon.
1. Installez l’application.
1. Lancez l’application à l’aide de l’URL générée par Assurance.
1. Si vous avez correctement ajouté le code ci-dessus, vous êtes invité à fournir votre consentement.

   Sélectionner **[!UICONTROL Continuer...]** puis sélectionnez **[!UICONTROL Autoriser]**.

   <img src="./assets/consent-update-1.png" width="300" /> 
   <img src="./assets/consent-update-2.png" width="300" />

1. Vous devriez voir une **[!UICONTROL Obtenir une réponse de consentement]** dans l’interface utilisateur d’Assurance.
   ![valider le consentement](assets/consent-update.png)



>[!SUCCESS]
>
>Vous avez maintenant activé votre application pour inviter l’utilisateur à son démarrage initial après l’installation (ou la réinstallation) à consentir à l’aide du SDK Adobe Experience Platform Mobile.<br/>Merci d’investir votre temps à apprendre sur le SDK Adobe Experience Platform Mobile. Si vous avez des questions, souhaitez partager des commentaires généraux ou avez des suggestions sur le contenu futur, partagez-les à ce sujet. [Article de discussion de la communauté Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796)

Suivant : **[Collecter les données du cycle de vie](lifecycle-data.md)**
