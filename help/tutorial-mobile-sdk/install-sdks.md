---
title: Installation des SDK Adobe Experience Platform Mobile
description: Découvrez comment mettre en oeuvre le SDK Mobile Adobe Experience Platform dans une application mobile.
jira: KT-14627
exl-id: 98d6f59e-b8a3-4c63-ae7c-8aa11e948f59
source-git-commit: 25f0df2ea09bb7383f45a698e75bd31be7541754
workflow-type: tm+mt
source-wordcount: '896'
ht-degree: 0%

---

# Installation des SDK Adobe Experience Platform Mobile

Découvrez comment mettre en oeuvre le SDK Mobile Adobe Experience Platform dans une application mobile.

## Conditions préalables

* Création réussie d’une bibliothèque de balises avec les extensions décrites dans la [leçon précédente](configure-tags.md).
* Identifiant du fichier d’environnement de développement à partir des [instructions d’installation mobile](configure-tags.md#generate-sdk-install-instructions).
* Téléchargez l’ [exemple d’application](https://github.com/Adobe-Marketing-Cloud/Luma-iOS-Mobile-App){target="_blank"} vide.
* Expérience avec [Xcode](https://developer.apple.com/xcode/){target="_blank"}.

## Objectifs d&#39;apprentissage

Dans cette leçon, vous allez :

* Ajoutez les SDK requis à votre projet à l’aide du gestionnaire de modules Swift.
* Enregistrez les extensions.

>[!NOTE]
>
>Dans une mise en oeuvre d’applications mobiles, les termes &quot;extensions&quot; et &quot;SDK&quot; sont presque interchangeables.

## Swift Package Manager

Au lieu d’utiliser CocoaPods et un fichier Pod (comme indiqué dans la section [Générer les instructions d’installation du SDK](./configure-tags.md#generate-sdk-install-instructions)), vous ajoutez des modules individuels à l’aide du gestionnaire de modules Swift natif de Xcode. Toutes les dépendances de packages sont déjà ajoutées pour le projet Xcode. L&#39;écran Xcode **[!UICONTROL Dépendances de module]** doit se présenter comme suit :

![Dépendances de modules Xcode](assets/xcode-package-dependencies.png){zoomable="yes"}


Dans Xcode, vous pouvez utiliser **[!UICONTROL File]** > **[!UICONTROL Add Packages...]** pour ajouter des packages. Le tableau ci-dessous fournit des liens vers les URL que vous utiliseriez pour ajouter des packages. Les liens vous dirigent également vers des informations supplémentaires sur chaque package spécifique.

| Package | Description |
|---|---|
| [AEP Core](https://github.com/adobe/aepsdk-core-ios) | Les extensions `AEPCore`, `AEPServices` et `AEPIdentity` représentent la base du SDK Adobe Experience Platform ; chaque application utilisant le SDK doit les inclure. Ces modules contiennent un ensemble commun de fonctionnalités et de services requis par toutes les extensions SDK.<br/><ul><li>`AEPCore` contient l’implémentation de Event Hub. Event Hub est le mécanisme utilisé pour diffuser des événements entre l’application et le SDK. Event Hub est également utilisé pour le partage de données entre les extensions.</li><li>`AEPServices` fournit plusieurs implémentations réutilisables nécessaires à la prise en charge de la plateforme, notamment la mise en réseau, l’accès au disque et la gestion de base de données.</li><li>`AEPIdentity` met en oeuvre l’intégration avec les services Adobe Experience Platform Identity.</li><li>`AEPSignal` représente l’extension Signal des SDK Adobe Experience Platform qui permet aux marketeurs d’envoyer un &quot;signal&quot; à leurs applications pour envoyer des données à des destinations externes ou ouvrir des URL.</li><li>`AEPLifecycle` représente l’extension du cycle de vie des SDK Adobe Experience Platform qui permet de collecter des mesures de cycle de vie des applications, telles que les informations d’installation ou de mise à niveau de l’application, les informations de lancement et de session de l’application, les informations sur l’appareil et toute donnée contextuelle supplémentaire fournie par le développeur de l’application.</li></ul> |
| [AEP Edge](https://github.com/adobe/aepsdk-edge-ios) | L’extension mobile Adobe Experience Platform Edge Network (`AEPEdge`) vous permet d’envoyer des données au réseau Adobe Edge à partir d’une application mobile. Cette extension vous permet d’implémenter les fonctionnalités de Adobe Experience Cloud de manière plus robuste, de servir plusieurs solutions d’Adobe par le biais d’un seul appel réseau et de transférer simultanément ces informations à Adobe Experience Platform.<br/>L’extension mobile Edge Network est une extension du SDK Adobe Experience Platform et requiert les extensions `AEPCore` et `AEPServices` pour la gestion des événements, ainsi que l’extension `AEPEdgeIdentity` pour la récupération des identités, comme ECID. |
| [AEP Edge Identity](https://github.com/adobe/aepsdk-edgeidentity-ios) | L’extension mobile AEP Edge Identity (`AEPEdgeIdentity`) permet la gestion des données d’identité utilisateur d’une application mobile lors de l’utilisation du SDK Adobe Experience Platform et de l’extension Edge Network. |
| [Consentement AEP Edge](https://github.com/adobe/aepsdk-edgeconsent-ios) | L’extension mobile AEP Consent Collection (`AEPConsent`) permet la collecte des préférences de consentement à partir de l’application mobile lors de l’utilisation du SDK Adobe Experience Platform et de l’extension Edge Network. |
| [Profil utilisateur AEP](https://github.com/adobe/aepsdk-userprofile-ios) | L’extension Mobile Profil utilisateur Adobe Experience Platform (`AEPUserProfile`) est une extension permettant de gérer les profils utilisateur pour le SDK Adobe Experience Platform. |
| [Places AEP](https://github.com/adobe/aepsdk-places-ios) | L’extension AEP Places (`AEPPlaces`) vous permet de suivre les événements de géolocalisation tels que définis dans l’interface Adobe Places et dans les règles Adobe Data Collection Tag. |
| [Messagerie AEP](https://github.com/adobe/aepsdk-messaging-ios) | L’extension de messagerie AEP (`AEPMessaging`) vous permet d’envoyer des jetons de notification push et des commentaires de clic publicitaire de notification push à Adobe Experience Platform. |
| [AEP Optimize](https://github.com/adobe/aepsdk-optimize-ios) | L’extension AEP Optimize (`AEPOptimize`) fournit des API pour activer les workflows de personnalisation en temps réel dans les SDK mobiles Adobe Experience Platform à l’aide d’Adobe Target ou de l’Offer decisioning Adobe Journey Optimizer. Il nécessite des extensions `AEPCore` et `AEPEdge` pour envoyer des événements de requête de personnalisation au réseau Experience Edge. |
| [Assurance AEP](https://github.com/adobe/aepsdk-assurance-ios) | Assurance (alias projet Griffon) est une nouvelle extension innovante (`AEPAssurance`) qui vous permet d’inspecter, de tester, de simuler et de valider la manière dont vous collectez des données ou diffusez des expériences dans votre application mobile. Cette extension active votre application pour l’assurance. |


## Importation d’extensions

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

1. Remplacez la valeur `@AppStorage` `YOUR_ENVIRONMENT_ID_GOES_HERE` de `environmentFileId` par la valeur d’identifiant de fichier d’environnement de développement que vous avez récupérée à partir des balises dans les [instructions d’installation du SDK Generate](configure-tags.md#generate-sdk-install-instructions).

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
1. Configure MobileCore et d’autres extensions pour utiliser la configuration de la propriété de balise.
1. Active la journalisation de débogage. Vous trouverez plus de détails et d’options dans la [documentation du SDK Mobile Adobe Experience Platform](https://developer.adobe.com/client-sdks/documentation/getting-started/enable-debug-logging/).
1. Commence la surveillance du cycle de vie. Pour plus d’informations, voir l’étape [Cycle de vie](lifecycle-data.md) du tutoriel.
1. Définit le consentement par défaut sur inconnu. Pour plus d’informations, voir l’étape [Consentement](consent.md) du tutoriel.

>[!IMPORTANT]
>
>Assurez-vous de mettre à jour `MobileCore.configureWith(appId: self.environmentFileId)` avec le `appId` en fonction de l’ `environmentFileId` de l’environnement de balises pour lequel vous créez (développement, évaluation ou production).
>

>[!SUCCESS]
>
>Vous avez maintenant installé les packages nécessaires et mis à jour votre projet afin d’enregistrer correctement les extensions de SDK Mobile Adobe Experience Platform requises que vous allez utiliser pour le reste du tutoriel.
>
>Merci d’investir votre temps à apprendre sur le SDK Adobe Experience Platform Mobile. Si vous avez des questions, souhaitez partager des commentaires généraux ou avez des suggestions sur le contenu à venir, partagez-les sur cet [post de discussion de la communauté Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796)

Suivant : **[Configuration de l’assurance](assurance.md)**
