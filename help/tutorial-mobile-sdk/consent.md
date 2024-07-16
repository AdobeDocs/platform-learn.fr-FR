---
title: Implémentation du consentement pour les implémentations du SDK Platform Mobile
description: Découvrez comment mettre en oeuvre le consentement dans une application mobile.
feature: Mobile SDK,Consent
jira: KT-14629
exl-id: 08042569-e16e-4ed9-9b5a-864d8b7f0216
source-git-commit: 25f0df2ea09bb7383f45a698e75bd31be7541754
workflow-type: tm+mt
source-wordcount: '529'
ht-degree: 1%

---

# Mise en oeuvre du consentement

Découvrez comment mettre en oeuvre le consentement dans une application mobile.

L’extension mobile de consentement Adobe Experience Platform permet la collecte des préférences de consentement à partir de votre application mobile lors de l’utilisation du SDK Adobe Experience Platform Mobile et de l’extension Edge Network. Pour en savoir plus sur l’ [extension de consentement](https://developer.adobe.com/client-sdks/documentation/consent-for-edge-network/) dans la documentation.

## Conditions préalables

* Création et exécution de l’application avec les SDK installés et configurés.

## Objectifs d&#39;apprentissage

Dans cette leçon, vous allez :

* Demandez à l’utilisateur son consentement.
* Mettez à jour l’extension selon la réponse de l’utilisateur.
* Découvrez comment obtenir l’état actuel du consentement.

## Demander le consentement

Si vous avez suivi le tutoriel depuis le début, vous vous souvenez peut-être que vous avez défini le consentement par défaut dans l’extension Consentement sur **[!UICONTROL En attente - Événements de file d’attente qui se produisent avant que l’utilisateur ne fournisse les préférences de consentement.]**

Pour commencer à collecter des données, vous devez obtenir le consentement de l’utilisateur. Dans une application réelle, vous souhaiteriez consulter les bonnes pratiques en matière de consentement pour votre région. Dans ce tutoriel, vous obtenez le consentement de l’utilisateur en le demandant simplement avec une alerte :

1. Vous ne souhaitez demander le consentement de l’utilisateur qu’une seule fois. Pour ce faire, vous pouvez combiner le consentement du SDK Mobile avec l’autorisation requise pour le suivi à l’aide de la [structure de transparence du suivi des applications](https://developer.apple.com/documentation/apptrackingtransparency) d’Apple. Dans cette application, vous supposez que lorsque l’utilisateur autorise le suivi, il autorise la collecte d’événements.

1. Accédez à **[!DNL Luma]** > **[!DNL Luma]** > **[!DNL Utils]** > **[!UICONTROL MobileSDK]** dans le navigateur de projet Xcode.

   Ajoutez ce code à la fonction `updateConsent`.

   ```swift
   // Update consent
   let collectConsent = ["collect": ["val": value]]
   let currentConsents = ["consents": collectConsent]
   Consent.update(with: currentConsents)
   MobileCore.updateConfigurationWith(configDict: currentConsents)
   ```

1. Accédez à **[!DNL Luma]** > **[!DNL Luma]** > **[!DNL Views]** > **[!DNL General]** > **[!UICONTROL DisresponsabilitéView]** dans le navigateur de projet de Xcode, qui est la vue affichée après l’installation ou la réinstallation de l’application et le démarrage initial de l’application. L’utilisateur est invité à autoriser le suivi par l’Apple [Structure de transparence du suivi des applications](https://developer.apple.com/documentation/apptrackingtransparency). Si l’utilisateur l’autorise, vous mettez également à jour le consentement.

   Ajoutez le code suivant à la fermeture `ATTrackingManager.requestTrackingAuthorization { status in`.

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

   Ajoutez le code suivant à la fonction `getConsents` :

   ```swift
   // Get consents
   Consent.getConsents { consents, error in
      guard error == nil, let consents = consents else { return }
      guard let jsonData = try? JSONSerialization.data(withJSONObject: consents, options: .prettyPrinted) else { return }
      guard let jsonStr = String(data: jsonData, encoding: .utf8) else { return }
      Logger.aepMobileSDK.info("Consent getConsents: \(jsonStr)")
   }
   ```

2. Accédez à **[!DNL Luma]** > **[!DNL Luma]** > **[!DNL Views]** > **[!DNL General]** > **[!UICONTROL HomeView]** dans le navigateur de projet Xcode.

   Ajoutez le code suivant au modificateur `.task` :

   ```swift
   // Ask status of consents
   MobileSDK.shared.getConsents()   
   ```

Dans l’exemple ci-dessus, vous enregistrez simplement l’état du consentement sur la console dans Xcode. Dans un scénario réel, vous pouvez l’utiliser pour modifier les menus ou options affichés à l’utilisateur.

## Valider avec Assurance

1. Supprimez l’application de votre appareil ou de votre simulateur pour réinitialiser correctement et initialiser le suivi et le consentement.
1. Pour connecter votre simulateur ou votre appareil à Assurance, consultez la section [Instructions de configuration](assurance.md#connecting-to-a-session) .
1. Lorsque vous passez de l’écran **[!UICONTROL Home]** à l’écran **[!UICONTROL Products]** et revenez à l’écran **[!UICONTROL Home]**, un événement **[!UICONTROL Get Conents Response]** doit s’afficher dans l’interface utilisateur d’assurance.
   ![valider le consentement](assets/consent-update.png)


>[!SUCCESS]
>
>Vous avez maintenant activé votre application pour inviter l’utilisateur à son démarrage initial après l’installation (ou la réinstallation) à consentir à l’aide du SDK Adobe Experience Platform Mobile.
>
>Merci d’investir votre temps à apprendre sur le SDK Adobe Experience Platform Mobile. Si vous avez des questions, souhaitez partager des commentaires généraux ou avez des suggestions sur le contenu à venir, partagez-les sur cet [post de discussion de la communauté Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796)

Suivant : **[Collecter les données du cycle de vie](lifecycle-data.md)**
