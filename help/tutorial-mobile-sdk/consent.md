---
title: Implémentation du consentement pour les implémentations de Platform Mobile SDK
description: Découvrez comment implémenter le consentement dans une application mobile.
feature: Mobile SDK,Consent
jira: KT-14629
exl-id: 08042569-e16e-4ed9-9b5a-864d8b7f0216
source-git-commit: 008d3ee066861ea9101fe9fe99ccd0a088b63f23
workflow-type: tm+mt
source-wordcount: '673'
ht-degree: 1%

---

# Implémenter le consentement

Découvrez comment implémenter le consentement dans une application mobile.

L’extension mobile de consentement Adobe Experience Platform permet la collecte de préférences de consentement à partir de votre application mobile lors de l’utilisation de la SDK mobile Adobe Experience Platform et de l’extension Edge Network. En savoir plus sur l’[extension de consentement](https://developer.adobe.com/client-sdks/documentation/consent-for-edge-network/) dans la documentation.

## Conditions préalables

* Application créée et exécutée avec succès avec les SDK installés et configurés.

## Objectifs d’apprentissage

Dans cette leçon, vous allez :

* Demander le consentement de l’utilisateur.
* Mettez à jour l’extension en fonction de la réponse de l’utilisateur.
* Découvrez comment obtenir l’état de consentement actuel.

## Demander le consentement

Si vous avez suivi le tutoriel depuis le début, vous vous souvenez peut-être que vous avez défini le consentement par défaut dans l’extension de consentement sur **[!UICONTROL En attente - Événements de file d’attente qui se produisent avant que l’utilisateur ne fournisse des préférences de consentement]**.

Pour commencer à collecter des données, vous devez obtenir le consentement de l’utilisateur. Dans une application réelle, vous pouvez consulter les bonnes pratiques en matière de consentement pour votre région. Dans ce tutoriel, vous obtenez le consentement de l’utilisateur en le demandant simplement avec une alerte :

>[!BEGINTABS]

>[!TAB iOS]

1. Vous ne souhaitez demander le consentement de l’utilisateur qu’une seule fois. Vous devez associer le consentement de Mobile SDK à l’autorisation requise pour le suivi à l’aide d’Apple [Cadre de transparence du suivi des applications](https://developer.apple.com/documentation/apptrackingtransparency). Dans cette application, vous supposez que lorsque l’utilisateur autorise le suivi, il consent à la collecte des événements.

1. Accédez à **[!DNL Luma]** > **[!DNL Luma]** > **[!DNL Utils]** > **[!UICONTROL MobileSDK]** dans le navigateur de projet Xcode.

   Ajoutez ce code à la fonction `updateConsent`.

   ```swift
   // Update consent
   let collectConsent = ["collect": ["val": value]]
   let currentConsents = ["consents": collectConsent]
   Consent.update(with: currentConsents)
   MobileCore.updateConfigurationWith(configDict: currentConsents)
   ```

1. Accédez à **[!DNL Luma]** > **[!DNL Luma]** > **[!DNL Views]** > **[!DNL General]** > **[!UICONTROL DisclaimerView]** dans le navigateur de projet de Xcode. Le navigateur de projet du code est la vue qui s’affiche après l’installation ou la réinstallation de l’application et le premier démarrage de l’application. L’utilisateur est invité à autoriser le suivi selon le [framework de transparence du suivi des applications](https://developer.apple.com/documentation/apptrackingtransparency) d’Apple. Si l’utilisateur ou l’utilisatrice l’autorise, vous mettez également à jour le consentement.

   Ajoutez le code suivant à la fermeture du `ATTrackingManager.requestTrackingAuthorization { status in`.

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

>[!TAB Android]

1. Vous ne souhaitez demander le consentement de l’utilisateur qu’une seule fois. Dans cette application, vous supposez que lorsque l’utilisateur autorise le suivi, il consent à la collecte des événements.

1. Accédez à **[!UICONTROL app]** > **[!UICONTROL kotlin+java]** > **[!UICONTROL com.adobe.luma.tutorial.android]** > **[!UICONTROL models]** > **[!UICONTROL MobileSDK]** dans le navigateur d’Android Studio.

   Ajoutez ce code à la fonction `updateConsent(value: String)`.

   ```kotlin
   // Update consent
   val collectConsent = mapOf("collect" to mapOf("val" to value))
   val currentConsents = mapOf("consents" to collectConsent)
   Consent.update(currentConsents)
   MobileCore.updateConfiguration(currentConsents)
   ```

1. Accédez à **[!UICONTROL app]** > **[!UICONTROL kotlin+java]** > **[!UICONTROL com.adobe.luma.tutorial.android]** > **[!UICONTROL views]** > **[!UICONTROL DisclaimerView.kt]** dans le navigateur d’Android Studio.

   Ajoutez le code suivant à la fonction `DisclaimerView(navController: NavController)` sous `// Set content to yes` et `// Set content to no`.

   ```kotlin
   // Add consent based on authorization
   if (status) {
      showPersonalizationWarning = false
   
      // Set consent to yes
      MobileSDK.shared.updateTrackingStatus(TrackingStatus.AUTHORIZED)
      MobileSDK.shared.updateConsent("y")
   } else {
      Toast.makeText(
            context,
            "You will not receive offers and location tracking will be disabled.",
            Toast.LENGTH_LONG
      ).show()
      showPersonalizationWarning = true
   
      // Set consent to no
      MobileSDK.shared.updateTrackingStatus(TrackingStatus.DENIED)
      MobileSDK.shared.updateConsent("n")
   }
   ```

>[!ENDTABS]

## Obtention de l’état de consentement actuel

L’extension mobile de consentement supprime/met en attente/autorise automatiquement le suivi en fonction de la valeur de consentement actuelle. Vous pouvez également accéder vous-même à l’état de consentement actuel :

>[!BEGINTABS]

>[!TAB iOS]

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

2. Accédez à **[!DNL Luma]** > **[!DNL Luma]** > **[!DNL Views]** > **[!DNL General]** > **[!UICONTROL HomeView]** dans le navigateur de projet de Xcode.

   Ajoutez le code suivant au modificateur `.task` :

   ```swift
   // Ask status of consents
   MobileSDK.shared.getConsents()   
   ```

Dans l’exemple ci-dessus, vous consignez simplement le statut du consentement dans la console dans Xcode. Dans un scénario réel, vous pouvez l’utiliser pour modifier les menus ou les options présentés à l’utilisateur ou l’utilisatrice.

>[!TAB Android]

1. Accédez à **[!UICONTROL app]** > **[!UICONTROL kotlin+java]** > **[!UICONTROL com.adobe.luma.tutorial.android]** > **[!UICONTROL models]** > **[!UICONTROL MobileSDK]** dans le navigateur d’Android Studio.

   Ajoutez le code suivant à la fonction `getConsents()` :

   ```kotlin
   // Get consents
   Consent.getConsents { callback ->
      if (callback != null) {
            val jsonStr = JSONObject(callback).toString(4)
            Log.i("MobileSDK", "Consent getConsents: $jsonStr")
      }
   }
   ```

1. Accédez à **[!UICONTROL app]** > **[!UICONTROL kotlin+java]** > **[!UICONTROL com.adobe.luma.tutorial.android]** > **[!UICONTROL views]** > **[!UICONTROL HomeView.kt]** dans le navigateur d’Android Studio.

   Ajoutez le code suivant à `LaunchedEffect(unit)` :

   ```kotlin
   // Ask status of consents
   MobileSDK.shared.getConsents()   
   ```

Dans l’exemple ci-dessus, vous consignez simplement le statut du consentement dans la console d’Android Studio. Dans un scénario réel, vous pouvez l’utiliser pour modifier les menus ou les options présentés à l’utilisateur ou l’utilisatrice.

>[!ENDTABS]

## Valider avec Assurance

1. Supprimez l’application de votre appareil ou simulateur pour réinitialiser et initialiser correctement le suivi et le consentement.
1. Pour connecter votre simulateur ou appareil à Assurance, consultez la section [instructions de configuration](assurance.md#connecting-to-a-session).
1. Lorsque vous passez de l’écran **[!UICONTROL Accueil]** à l’écran **[!UICONTROL Produits]** et revenez à l’écran **[!UICONTROL Accueil]**, un événement **[!UICONTROL Obtenir une réponse de consentement]** doit s’afficher dans l’interface utilisateur d’Assurance.
   ![valider le consentement](assets/consent-update.png){zoomable="yes"}


>[!SUCCESS]
>
>Vous avez maintenant activé votre application pour inviter l’utilisateur, à son démarrage initial après l’installation (ou la réinstallation), à consentir à l’aide de Adobe Experience Platform Mobile SDK.
>
>Merci d’avoir consacré votre temps à découvrir Adobe Experience Platform Mobile SDK. Si vous avez des questions, souhaitez partager des commentaires généraux ou des suggestions sur le contenu futur, partagez-les dans ce [article de discussion de la communauté Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796?profile.language=fr)

Suivant : **[Collecter des données de cycle de vie](lifecycle-data.md)**
