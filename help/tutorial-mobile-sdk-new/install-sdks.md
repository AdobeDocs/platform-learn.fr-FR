---
title: Installation des SDK Adobe Experience Platform Mobile
description: Découvrez comment mettre en oeuvre le SDK Mobile Adobe Experience Platform dans une application mobile.
hide: true
exl-id: 86348d8b-f428-465d-a79e-ce73d140da79
source-git-commit: f592fc61ad28d04eba3c1c21a0a66bda6e816a5b
workflow-type: tm+mt
source-wordcount: '948'
ht-degree: 1%

---

# Installation des SDK Adobe Experience Platform Mobile

Découvrez comment mettre en oeuvre le SDK Mobile Adobe Experience Platform dans une application mobile.

## Conditions préalables

* Création réussie d’une bibliothèque de balises avec les extensions décrites dans la section [leçon précédente](configure-tags.md).
* Identifiant du fichier d’environnement de développement du [Instructions d’installation mobile](configure-tags.md#generate-sdk-install-instructions).
* Téléchargé le vide [exemple d’application](https://github.com/Adobe-Marketing-Cloud/Luma-iOS-Mobile-App){target="_blank"}.
* Expérience avec [Xcode](https://developer.apple.com/xcode/){target="_blank"}.

## Objectifs d&#39;apprentissage

Dans cette leçon, vous allez :

* Ajoutez les SDK requis à votre projet à l’aide du gestionnaire de modules Swift.
* Enregistrez les extensions.

>[!NOTE]
>
>Dans une mise en oeuvre d’applications mobiles, les termes &quot;extensions&quot; et &quot;SDK&quot; sont presque interchangeables.

## Swift Package Manager

Au lieu d’utiliser CocoaPods et un fichier Pod (comme indiqué dans les instructions d’installation mobile), voir [Instructions d’installation du SDK Generate](./configure-tags.md#generate-sdk-install-instructions)), vous ajoutez des modules individuels à l’aide du gestionnaire de modules Swift natif de Xcode. Toutes les dépendances de packages sont déjà ajoutées pour le projet Xcode. Xcode **[!UICONTROL Dépendances de modules]** L’écran doit se présenter comme suit :

![Dépendances de modules Xcode](assets/xcode-package-dependencies.png){zoomable=&quot;yes&quot;}


Dans Xcode, vous pouvez utiliser **[!UICONTROL Fichier]** > **[!UICONTROL Ajouter des packages...]** pour ajouter des packages. Le tableau ci-dessous fournit des liens vers les URL que vous utiliseriez pour ajouter des packages. Les liens vous dirigent également vers des informations supplémentaires sur chaque package spécifique.

| Package | Description |
|---|---|
| [AEP Core](https://github.com/adobe/aepsdk-core-ios.git) | La variable `AEPCore`, `AEPServices`, et `AEPIdentity` Les extensions représentent la base du SDK Adobe Experience Platform. Chaque application utilisant le SDK doit les inclure. Ces modules contiennent un ensemble commun de fonctionnalités et de services requis par toutes les extensions du SDK.<br/><ul><li>`AEPCore` contient l’implémentation de Event Hub. Event Hub est le mécanisme utilisé pour diffuser des événements entre l’application et le SDK. Event Hub est également utilisé pour le partage de données entre les extensions.</li><li>`AEPServices` fournit plusieurs implémentations réutilisables nécessaires à la prise en charge de la plateforme, notamment la mise en réseau, l’accès au disque et la gestion de base de données.</li><li>`AEPIdentity` met en oeuvre l’intégration avec les services Adobe Experience Platform Identity.</li><li>`AEPSignal` représente l’extension Signal des SDK Adobe Experience Platform qui permet aux marketeurs d’envoyer un &quot;signal&quot; à leurs applications afin d’envoyer des données à des destinations externes ou d’ouvrir des URL.</li><li>`AEPLifecycle` représente l’extension de cycle de vie des SDK Adobe Experience Platform qui permet de collecter des mesures de cycle de vie des applications, telles que les informations d’installation ou de mise à niveau de l’application, les informations de lancement et de session de l’application, les informations sur l’appareil et toute donnée contextuelle supplémentaire fournie par le développeur de l’application.</li></ul> |
| [AEP Edge](https://github.com/adobe/aepsdk-edge-ios.git) | Extension mobile Adobe Experience Platform Edge Network (`AEPEdge`) vous permet d’envoyer des données à Adobe Edge Network à partir d’une application mobile. Cette extension vous permet d’implémenter les fonctionnalités de Adobe Experience Cloud de manière plus robuste, de servir plusieurs solutions d’Adobe par le biais d’un seul appel réseau et de transférer simultanément ces informations à Adobe Experience Platform.<br/>L’extension mobile Edge Network est une extension du SDK Adobe Experience Platform qui requiert le `AEPCore` et `AEPServices` les extensions pour la gestion des événements, ainsi que la variable `AEPEdgeIdentity` pour récupérer les identités, telles qu’ECID. |
| [AEP Edge Identity](https://github.com/adobe/aepsdk-edgeidentity-ios.git) | Extension mobile AEP Edge Identity (`AEPEdgeIdentity`) permet de gérer les données d’identité utilisateur d’une application mobile lors de l’utilisation du SDK Adobe Experience Platform et de l’extension Edge Network. |
| [Consentement AEP Edge](https://github.com/adobe/aepsdk-edgeconsent-ios.git) | Extension mobile de collecte de consentement AEP (`AEPConsent`) active la collecte des préférences de consentement à partir de l’application mobile lors de l’utilisation du SDK Adobe Experience Platform et de l’extension Edge Network. |
| [Profil utilisateur AEP](https://github.com/adobe/aepsdk-userprofile-ios.git) | Extension Mobile du profil utilisateur Adobe Experience Platform (`AEPUserProfile`) est une extension permettant de gérer les profils utilisateur pour le SDK Adobe Experience Platform. |
| [Places AEP](https://github.com/adobe/aepsdk-places-ios) | L’extension AEP Places (`AEPPlaces`) vous permet de suivre les événements de géolocalisation tels que définis dans l’interface Adobe Places et dans les règles Adobe Data Collection Tag. |
| [Messagerie AEP](https://github.com/adobe/aepsdk-messaging-ios.git) | L’extension de messagerie AEP (`AEPMessaging`) vous permet d’envoyer des jetons de notification push et des commentaires de clic publicitaire de notification push à Adobe Experience Platform. |
| [Optimisation AEP](https://github.com/adobe/aepsdk-optimize-ios) | L’extension AEP Optimization (`AEPOptimize`) fournit des API pour activer les workflows de personnalisation en temps réel dans les SDK mobiles Adobe Experience Platform à l’aide d’Adobe Target ou de l’Offer decisioning Adobe Journey Optimizer. Cela nécessite `AEPCore` et `AEPEdge` extensions pour envoyer des événements de requête de personnalisation au réseau Experience Edge. |
| [Assurance AEP](https://github.com/adobe/aepsdk-assurance-ios.git) | Assurance (alias Griffon) est une extension nouvelle et innovante (`AEPAssurance`) pour vous aider à inspecter, tester, simuler et valider la manière dont vous collectez des données ou diffusez des expériences dans votre application mobile. Cette extension active votre application pour l’assurance. |


## Importation d’extensions

Dans Xcode, accédez à **[!DNL Luma]** > **[!DNL Luma]** > **[!UICONTROL AppDelegate]** et assurez-vous que les imports suivants font partie de ce fichier source.

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

1. Remplacez la variable `@AppStorage` value `YOUR_ENVIRONMENT_ID_GOES_HERE` pour `environmentFileId` à la valeur d’identifiant de fichier d’environnement de développement que vous avez récupérée à partir des balises à l’étape 6 de la section [Instructions d’installation du SDK Generate](configure-tags.md#generate-sdk-install-instructions).

   ```swift
   @AppStorage("environmentFileId") private var environmentFileId = "YOUR_ENVIRONMENT_ID_GOES_HERE"
   ```

1. Ajoutez le code suivant au `application(_, didFinishLaunchingWithOptions)` de la fonction

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
1. Configure MobileCore et d’autres extensions pour utiliser la configuration de la propriété de balise.
1. Active la journalisation de débogage. Vous trouverez plus de détails et d’options dans la section [Documentation du SDK Mobile Adobe Experience Platform](https://developer.adobe.com/client-sdks/documentation/getting-started/enable-debug-logging/).
1. Commence la surveillance du cycle de vie. Voir [Cycle de vie](lifecycle-data.md) pour plus d’informations, consultez le tutoriel .
1. Définit le consentement par défaut sur inconnu. Voir [Consentement](consent.md) pour plus d’informations, consultez le tutoriel .

>[!IMPORTANT]
>
>Veillez à mettre à jour `MobileCore.configureWith(appId: self.environmentFileId)` avec la propriété `appId` en fonction de la variable `environmentFileId` à partir de l’environnement de balises pour lequel vous créez (développement, évaluation ou production).
>

>[!SUCCESS]
>
>Vous avez maintenant installé les packages nécessaires et mis à jour votre projet afin d’enregistrer correctement les extensions de SDK Mobile Adobe Experience Platform requises que vous allez utiliser pour le reste du tutoriel.<br/>Merci d’investir votre temps à apprendre sur le SDK Adobe Experience Platform Mobile. Si vous avez des questions, souhaitez partager des commentaires généraux ou avez des suggestions sur le contenu futur, partagez-les à ce sujet. [Article de discussion de la communauté Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796)

Suivant : **[Configuration d’Assurance](assurance.md)**
