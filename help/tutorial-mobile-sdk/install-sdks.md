---
title: Installation des SDK mobiles Adobe Experience Platform
description: Découvrez comment mettre en œuvre Adobe Experience Platform Mobile SDK dans une application mobile.
jira: KT-14627
exl-id: 98d6f59e-b8a3-4c63-ae7c-8aa11e948f59
source-git-commit: 463a5d54e99ddf6587fe19081c07025f7caf648e
workflow-type: tm+mt
source-wordcount: '916'
ht-degree: 0%

---

# Installation des SDK mobiles Adobe Experience Platform

>[!CONTEXTUALHELP]
>id="platform_mobile_sdk_tutorial_install"
>title="Installation des SDK mobiles Adobe Experience Platform"
>abstract="Découvrez comment mettre en œuvre Adobe Experience Platform Mobile SDK dans une application mobile."

Découvrez comment mettre en œuvre Adobe Experience Platform Mobile SDK dans une application mobile.

## Conditions préalables

* Bibliothèque de balises créée avec les extensions décrites dans la [leçon précédente](configure-tags.md).
* Identifiant du fichier d’environnement de développement à partir des [instructions d’installation mobile](configure-tags.md#generate-sdk-install-instructions).
* Téléchargé l’exemple d’application [vide](https://github.com/Adobe-Marketing-Cloud/Luma-iOS-Mobile-App){target="_blank"}.
* Expérience avec [Xcode](https://developer.apple.com/xcode/){target="_blank"}.

## Objectifs d’apprentissage

Dans cette leçon, vous allez :

* Ajoutez les SDK requis à votre projet à l’aide du gestionnaire de packages Swift.
* Enregistrez les extensions.

>[!NOTE]
>
>Dans une implémentation d’application mobile, les termes « extensions » et « SDK » sont presque interchangeables.

## Gestionnaire de packages Swift

Au lieu d’utiliser des CocoaPods et un fichier Pod (comme indiqué dans [Instructions d’installation de Generate SDK](./configure-tags.md#generate-sdk-install-instructions)), vous pouvez ajouter des packages individuels à l’aide du gestionnaire de packages Swift natif de Xcode. Toutes les dépendances de packages ont déjà été ajoutées pour vous dans le projet Xcode. L’écran Xcode **[!UICONTROL Dépendances de packages]** doit se présenter comme suit :

![Dépendances De Packages Xcode](assets/xcode-package-dependencies.png){zoomable="yes"}


Dans Xcode, vous pouvez utiliser **[!UICONTROL Fichier]** > **[!UICONTROL Ajouter des packages...]** pour ajouter des packages. Le tableau ci-dessous fournit des liens vers les URL que vous pouvez utiliser pour ajouter des packages. Les liens vous redirigent également vers des informations supplémentaires sur chaque package spécifique.

| Package | Description |
|---|---|
| [AEP Core](https://github.com/adobe/aepsdk-core-ios) | Les extensions `AEPCore`, `AEPServices` et `AEPIdentity` représentent la base du SDK Adobe Experience Platform. Chaque application utilisant le SDK doit les inclure. Ces modules contiennent un ensemble commun de fonctionnalités et de services requis par toutes les extensions de SDK.<br/><ul><li>`AEPCore` contient l’implémentation du hub d’événements. Event Hub est le mécanisme utilisé pour diffuser des événements entre l’application et le SDK. Event Hub est également utilisé pour partager des données entre les extensions.</li><li>`AEPServices` fournit plusieurs implémentations réutilisables nécessaires à la prise en charge de Platform, notamment la mise en réseau, l’accès au disque et la gestion des bases de données.</li><li>`AEPIdentity` implémente l’intégration avec les services Adobe Experience Platform Identity.</li><li>`AEPSignal` représente l’extension Signal des SDK Adobe Experience Platform qui permet aux spécialistes marketing d’envoyer un « signal » à leurs applications pour envoyer des données à des destinations externes ou ouvrir des URL.</li><li>`AEPLifecycle` représente l’extension de cycle de vie des SDK Adobe Experience Platform qui permet de collecter des mesures de cycle de vie des applications, telles que des informations d’installation ou de mise à niveau des applications, des informations de lancement et de session des applications, des informations sur les appareils et toute donnée contextuelle supplémentaire fournie par le développeur ou la développeuse de l’application.</li></ul> |
| [AEP EDGE](https://github.com/adobe/aepsdk-edge-ios) | L’extension mobile Adobe Experience Platform Edge Network (`AEPEdge`) vous permet d’envoyer des données au réseau Adobe Edge à partir d’une application mobile. Cette extension vous permet d’implémenter les fonctionnalités de Adobe Experience Cloud de manière plus robuste, de diffuser plusieurs solutions d’Adobe par le biais d’un appel réseau et de transférer simultanément ces informations au Adobe Experience Platform.<br/>L’extension mobile Edge Network est une extension de Adobe Experience Platform SDK qui nécessite les extensions `AEPCore` et `AEPServices` pour la gestion des événements, ainsi que l’extension `AEPEdgeIdentity` pour la récupération des identités, telles que l’ECID. |
| [Identité Edge AEP](https://github.com/adobe/aepsdk-edgeidentity-ios) | L’extension AEP Edge Identity Mobile (`AEPEdgeIdentity`) permet de gérer les données d’identité utilisateur d’une application mobile lors de l’utilisation de Adobe Experience Platform SDK et de l’extension Edge Network. |
| [Consentement AEP Edge](https://github.com/adobe/aepsdk-edgeconsent-ios) | L’extension mobile de collecte de consentement AEP (`AEPConsent`) permet la collecte de préférences de consentement à partir de l’application mobile lors de l’utilisation du SDK Adobe Experience Platform et de l’extension de l’Edge Network. |
| [ Profil utilisateur AEP ](https://github.com/adobe/aepsdk-userprofile-ios) | L’extension Adobe Experience Platform User Profile Mobile (`AEPUserProfile`) est une extension permettant de gérer les profils utilisateur pour Adobe Experience Platform SDK. |
| [AEP Places](https://github.com/adobe/aepsdk-places-ios) | L’extension AEP Places (`AEPPlaces`) vous permet d’effectuer le suivi des événements de géolocalisation tels que définis dans l’interface d’Adobe Places et dans les règles de balise de collecte de données d’Adobe. |
| [Messagerie AEP](https://github.com/adobe/aepsdk-messaging-ios) | L’extension de messagerie AEP (`AEPMessaging`) vous permet d’envoyer des jetons de notification push et des commentaires relatifs aux clics publicitaires de notification push au Adobe Experience Platform. |
| [AEP Optimize](https://github.com/adobe/aepsdk-optimize-ios) | L’extension AEP Optimize (`AEPOptimize`) fournit des API pour activer les workflows de personnalisation en temps réel dans les SDK mobiles Adobe Experience Platform à l’aide d’Adobe Target ou de l’Offer decisioning Adobe Journey Optimizer. Elle nécessite des extensions `AEPCore` et `AEPEdge` pour envoyer des événements de requête de personnalisation au réseau Experience Edge. |
| [AEP ASSURANCE](https://github.com/adobe/aepsdk-assurance-ios) | Assurance (également appelé projet Griffon) est une nouvelle extension innovante (`AEPAssurance`) qui vous permet d’inspecter, de tester, de simuler et de valider la manière dont vous collectez les données ou dont les expériences sont diffusées dans votre application mobile. Cette extension active votre application pour Assurance. |


## Importer des extensions

Dans Xcode, accédez à **[!DNL Luma]** > **[!DNL Luma]** > **[!UICONTROL AppDelegate]** et assurez-vous que les importations suivantes font partie de ce fichier source.

```swift
// import AEP MobileSDK libraries
import AEPCore
import AEPServices
import AEPIdentity
import AEPSignal
import AEPLifecycle
import AEPEdge
import AEPEdgeIdentity
import AEPEdgeConsent
import AEPUserProfile
import AEPPlaces
import AEPMessaging
import AEPOptimize
import AEPAssurance
```

Faites de même pour **[!DNL Luma]** > **[!DNL Luma]** > **[!DNL Utils]** > **[!UICONTROL MobileSDK]**.

## Mettre à jour AppDelegate

Accédez à **[!DNL Luma]** > **[!DNL Luma]** > **AppDelegate** dans le navigateur de projet Xcode.

1. Remplacez la valeur `@AppStorage` `YOUR_ENVIRONMENT_ID_GOES_HERE` pour `environmentFileId` à la valeur de l’identifiant du fichier d’environnement de développement que vous avez récupérée à partir des balises dans [Générer les instructions d’installation de SDK](configure-tags.md#generate-sdk-install-instructions).

   ```swift
   @AppStorage("environmentFileId") private var environmentFileId = "YOUR_ENVIRONMENT_ID_GOES_HERE"
   ```

1. Ajoutez le code suivant à la fonction `application(_, didFinishLaunchingWithOptions)`.

   ```swift
   // Define extensions
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
   
   // Register extensions
   MobileCore.registerExtensions(extensions, {
       // Use the environment file id assigned to this application via Adobe Experience Platform Data Collection
       Logger.aepMobileSDK.info("Luma - using mobile config: \(self.environmentFileId)")
       MobileCore.configureWith(appId: self.environmentFileId)
   
       // set this to false or comment it when deploying to TestFlight (default is false),
       // set this to true when testing on your device.
       MobileCore.updateConfigurationWith(configDict: ["messaging.useSandbox": true])
       if appState != .background {
           // only start lifecycle if the application is not in the background
           MobileCore.lifecycleStart(additionalContextData: nil)
       }
   
       // assume unknown, adapt to your needs.
       MobileCore.setPrivacyStatus(.unknown)
   })
   ```

Le code ci-dessus effectue les opérations suivantes :

1. Enregistre les extensions requises.
1. Configure MobileCore et d’autres extensions pour utiliser la configuration de propriété de balise.
1. Active la journalisation du débogage. Vous trouverez plus d’informations et d’options dans la documentation de Adobe Experience Platform Mobile SDK [](https://developer.adobe.com/client-sdks/documentation/getting-started/enable-debug-logging/).
1. Démarre la surveillance du cycle de vie. Voir l’étape [Cycle de vie](lifecycle-data.md) du tutoriel pour plus d’informations.
1. Définit le consentement par défaut sur inconnu. Voir l’étape [Consentement](consent.md) du tutoriel pour plus d’informations.

>[!IMPORTANT]
>
>Veillez à mettre à jour les `MobileCore.configureWith(appId: self.environmentFileId)` avec le `appId` en fonction des `environmentFileId` de l’environnement de balises pour lequel vous créez des ressources (développement, évaluation ou production).
>

>[!SUCCESS]
>
>Vous avez maintenant installé les packages nécessaires et mis à jour votre projet afin d’enregistrer correctement les extensions Adobe Experience Platform Mobile SDK requises que vous allez utiliser pour la suite du tutoriel.
>
>Merci d’avoir consacré votre temps à découvrir Adobe Experience Platform Mobile SDK. Si vous avez des questions, si vous souhaitez partager des commentaires généraux ou si vous avez des suggestions sur le contenu futur, partagez-les sur ce [article de discussion de la communauté des Experience League ](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796)

Suivant : **[Configuration d’Assurance](assurance.md)**
