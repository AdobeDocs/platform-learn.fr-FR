---
title: Installation des SDK mobiles Adobe Experience Platform
description: Découvrez comment mettre en œuvre le SDK mobile Adobe Experience Platform dans une application mobile.
jira: KT-14627
exl-id: 98d6f59e-b8a3-4c63-ae7c-8aa11e948f59
source-git-commit: 008d3ee066861ea9101fe9fe99ccd0a088b63f23
workflow-type: tm+mt
source-wordcount: '1768'
ht-degree: 3%

---

# Installation des SDK mobiles Adobe Experience Platform {#tutorial_install_mobile_sdks}

>[!CONTEXTUALHELP]
>
>id="platform_mobile_sdk_tutorial_install"
>title="Installation des SDK mobiles Adobe Experience Platform"
>abstract="Découvrez comment mettre en œuvre le SDK mobile Adobe Experience Platform dans une application mobile."

Découvrez comment mettre en œuvre le SDK mobile Adobe Experience Platform dans une application mobile.

## Conditions préalables

* Bibliothèque de balises créée avec les extensions décrites dans la [leçon précédente](configure-tags.md).
* Identifiant du fichier d’environnement de développement à partir des [instructions d’installation mobile](configure-tags.md#generate-sdk-install-instructions).
* Téléchargé l’[exemple d’application pour iOS](https://github.com/Adobe-Marketing-Cloud/Luma-iOS-Mobile-App) ou l’[exemple d’application pour Android](https://github.com/adobe/Luma-Android).
* Expérience avec [Xcode](https://developer.apple.com/xcode/) (iOS) ou [Android Studio](https://developer.android.com/studio/intro?utm_source=android-studio) (Android)

## Objectifs d’apprentissage

Dans cette leçon, vous allez :

* Ajoutez les SDK requis à votre projet.
* Enregistrez les extensions.

>[!NOTE]
>
>Dans une implémentation d’application mobile, les termes *extensions* et *SDK* sont presque interchangeables.

>[!BEGINTABS]

>[!TAB iOS]

## Gestionnaire de packages Swift

Au lieu d’utiliser des CocoaPods et un fichier Pod (comme indiqué dans [Instructions d’installation de Generate SDK](./configure-tags.md#generate-sdk-install-instructions)), vous pouvez ajouter des packages individuels à l’aide du gestionnaire de packages Swift natif de Xcode. Toutes les dépendances de packages ont déjà été ajoutées pour vous dans le projet Xcode. L’écran Xcode **[!UICONTROL Dépendances de packages]** doit se présenter comme suit :

![Dépendances De Packages Xcode](assets/xcode-package-dependencies.png){zoomable="yes"}


Dans Xcode, vous pouvez utiliser **[!UICONTROL Fichier]** > **[!UICONTROL Ajouter des packages...]** pour ajouter des packages. Le tableau ci-dessous fournit des liens vers les URL que vous pouvez utiliser pour ajouter des packages. Les liens vous redirigent également vers des informations supplémentaires sur chaque package spécifique.

| Package | Description |
|---|---|
| [AEP Core](https://github.com/adobe/aepsdk-core-ios) | Les extensions `AEPCore`, `AEPServices` et `AEPIdentity` représentent la base du SDK Adobe Experience Platform. Chaque application utilisant le SDK doit les inclure. Ces modules contiennent un ensemble commun de fonctionnalités et de services dont toutes les extensions SDK ont besoin.<br/><ul><li>`AEPCore` contient l’implémentation du hub d’événements. Event Hub est le mécanisme utilisé pour diffuser des événements entre l’application et le SDK. Event Hub est également utilisé pour partager des données entre les extensions.</li><li>`AEPServices` fournit plusieurs implémentations réutilisables nécessaires à la prise en charge de Platform, notamment la mise en réseau, l’accès au disque et la gestion des bases de données.</li><li>`AEPIdentity` implémente l’intégration avec les services Adobe Experience Platform Identity.</li><li>`AEPSignal` représente l’extension Signal des SDK Adobe Experience Platform qui permet aux spécialistes marketing d’envoyer un « signal » à leurs applications pour envoyer des données à des destinations externes ou ouvrir des URL.</li><li>`AEPLifecycle` représente l’extension de cycle de vie des SDK Adobe Experience Platform qui permet de collecter des mesures de cycle de vie des applications, telles que des informations d’installation ou de mise à niveau des applications, des informations de lancement et de session des applications, des informations sur les appareils et toute donnée contextuelle supplémentaire fournie par le développeur ou la développeuse de l’application.</li></ul> |
| [AEP Edge](https://github.com/adobe/aepsdk-edge-ios) | L’extension mobile Adobe Experience Platform Edge Network (`AEPEdge`) vous permet d’envoyer des données à Adobe Edge Network à partir d’une application mobile. Cette extension vous permet de mettre en œuvre les fonctionnalités de Adobe Experience Cloud de manière plus robuste, de diffuser plusieurs solutions Adobe par le biais d’un seul appel réseau et de transférer simultanément ces informations au Adobe Experience Platform.<br/>L’extension mobile Edge Network est une extension de Adobe Experience Platform SDK. L’extension nécessite les extensions `AEPCore` et `AEPServices` pour la gestion des événements, ainsi que l’extension `AEPEdgeIdentity` pour récupérer les identités, telles que l’ECID. |
| [Identité AEP Edge](https://github.com/adobe/aepsdk-edgeidentity-ios) | L’extension Adobe Experience Platform Edge Identity mobile extension (`AEPEdgeIdentity`) permet de gérer les données d’identité utilisateur d’une application mobile lors de l’utilisation de Adobe Experience Platform SDK et de l’extension Edge Network. |
| [Consentement AEP Edge](https://github.com/adobe/aepsdk-edgeconsent-ios) | L’extension mobile de collecte de consentement Adobe Experience Platform (`AEPConsent`) permet la collecte de préférences de consentement à partir de l’application mobile lors de l’utilisation du SDK Adobe Experience Platform et de l’extension Edge Network. |
| [Profil utilisateur AEP](https://github.com/adobe/aepsdk-userprofile-ios) | L’extension Adobe Experience Platform User Profile Mobile (`AEPUserProfile`) est une extension permettant de gérer les profils utilisateur pour Adobe Experience Platform SDK. |
| [AEP Places](https://github.com/adobe/aepsdk-places-ios) | L&#39;extension Adobe Experience Platform Places (`AEPPlaces`) vous permet d&#39;effectuer le suivi des événements de géolocalisation tels que définis dans l&#39;interface Adobe Places et dans les règles de balise de collecte de données Adobe. |
| [AEP Messaging](https://github.com/adobe/aepsdk-messaging-ios) | L’extension Adobe Experience Platform Messaging (`AEPMessaging`) vous permet d’envoyer des jetons de notification push et des commentaires sur les clics publicitaires des notifications push au Adobe Experience Platform. |
| [AEP Optimize](https://github.com/adobe/aepsdk-optimize-ios) | L’extension Adobe Experience Platform Optimize (`AEPOptimize`) fournit des API pour activer les workflows de personnalisation en temps réel dans les SDK Adobe Experience Platform Mobile à l’aide d’Adobe Target ou de Adobe Journey Optimizer Offer Decisioning. Elle nécessite des extensions `AEPCore` et `AEPEdge` pour envoyer des événements de requête de personnalisation à Experience Edge Network. |
| [AEP Assurance](https://github.com/adobe/aepsdk-assurance-ios) | Adobe Experience Platform Assurance est un produit de Adobe Experience Cloud qui vous permet d’inspecter, de tester, de simuler et de valider la manière dont vous collectez les données ou dont les expériences sont diffusées dans votre application mobile. |


## Importer des extensions

Ouvrez dans Xcode le projet dans le dossier **[!UICONTROL Start]** de l’exemple d’application.

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

1. Remplacez la valeur `@AppStorage` `YOUR_ENVIRONMENT_ID_GOES_HERE` pour `environmentFileId` par la valeur de l’identifiant du fichier d’environnement que vous avez récupérée à partir des balises dans [Instructions d’installation de Generate SDK](configure-tags.md#generate-sdk-install-instructions).

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
1. Active la journalisation du débogage. Vous trouverez plus d’informations et d’options dans la documentation de Adobe Experience Platform Mobile SDK [&#128279;](https://developer.adobe.com/client-sdks/documentation/getting-started/enable-debug-logging/).
1. Démarre la surveillance du cycle de vie. Voir l’étape [Cycle de vie](lifecycle-data.md) du tutoriel pour plus d’informations.
1. Définit le consentement par défaut sur inconnu. Voir l’étape [Consentement](consent.md) du tutoriel pour plus d’informations.

Veillez à mettre à jour les `MobileCore.configureWith(appId: self.environmentFileId)` avec le `appId` en fonction des `environmentFileId` de l’environnement de balises pour lequel vous créez des ressources (développement, évaluation ou production).

>[!TAB Android]

## Gradle

Utilisez les dépendances des instructions d’installation [Generate SDK](./configure-tags.md#generate-sdk-install-instructions) pour ajouter des packages individuels à l’aide de l’intégration de Gradle à Android Studio. Le projet Android Studio comporte déjà toutes les dépendances de packages ajoutées pour vous.

1. Sélectionnez ![FolderOutline](/help/assets/icons/FolderOutline.svg) comme outil.
1. Sélectionnez la vue **[!UICONTROL Android]**.
1. Sélectionnez **[!UICONTROL Scripts Gradle]** > **[!UICONTROL build.gradle.kts (Module :app)]** dans le volet gauche. Ensuite, dans le volet de droite, faites défiler l’écran jusqu’à ce que `dependencies` s’affiche.

   ![Dépendances de niveau Android](assets/androidstudio-package-dependencies.png){zoomable="yes"}

Dans Android Studio, vous pouvez utiliser **[!UICONTROL Fichier]** > **[!UICONTROL Structure de projet...]** pour ajouter des dépendances de module. Sélectionnez **[!UICONTROL Dépendances]** puis utilisez **[!UICONTROL Modules]** ![Ajouter](/help/assets/icons/Add.svg) pour ajouter des modules. Le tableau ci-dessous fournit des liens vers les URL que vous pouvez utiliser pour ajouter des modules de dépendance. Les liens vous redirigent également vers des informations supplémentaires sur chaque module spécifique.

| Package<br/>com.adobe<br/>marketing.mobile: | Description |
|---|---|
| [core](https://github.com/adobe/aepsdk-core-android) | Les extensions `MobileCore` et `Identity` représentent la base du SDK Adobe Experience Platform. Chaque application utilisant le SDK doit les inclure. Ces modules contiennent un ensemble commun de fonctionnalités et de services dont toutes les extensions SDK ont besoin.<ul><li>`MobileCore` contient l’implémentation du hub d’événements. Event Hub est le mécanisme utilisé pour diffuser des événements entre l’application et le SDK. Event Hub est également utilisé pour partager des données entre les extensions et fournit plusieurs implémentations réutilisables nécessaires à la prise en charge de la plateforme, notamment la mise en réseau, l’accès au disque et la gestion des bases de données.</li><li>`Identity` implémente l’intégration avec les services Adobe Experience Platform Identity.</li><li>`Signal` représente l’extension du signal de SDK de Adobe Experience Platform qui permet aux spécialistes marketing d’envoyer un « signal » à leurs applications pour envoyer des données à des destinations externes ou ouvrir des URL.</li><li>`Lifecycle` représente l’extension de cycle de vie du SDK Adobe Experience Platform qui permet de collecter des mesures de cycle de vie des applications, telles que des informations d’installation ou de mise à niveau des applications, des informations de lancement et de session des applications, des informations sur les appareils et toute donnée contextuelle supplémentaire fournie par le développeur ou la développeuse de l’application.</li></ul> |
| [edge](https://github.com/adobe/aepsdk-edge-android) | L’extension mobile Adobe Experience Platform Edge Network (`AEPEdge`) vous permet d’envoyer des données à Adobe Edge Network à partir d’une application mobile. Cette extension vous permet de mettre en œuvre les fonctionnalités de Adobe Experience Cloud de manière plus robuste, de diffuser plusieurs solutions Adobe par le biais d’un seul appel réseau et de transférer simultanément ces informations au Adobe Experience Platform.<br/>L’extension mobile Edge Network est une extension de Adobe Experience Platform SDK. L’extension nécessite les extensions `Mobile Core` et `Services` pour la gestion des événements. Et l’extension `Identity for Edge Network` pour récupérer les identités, telle que l’ECID. |
| [edgeidentity](https://github.com/adobe/aepsdk-edgeidentity-android) | L’extension Adobe Experience Platform Edge Identity Mobile permet de gérer les données d’identité utilisateur d’une application mobile lors de l’utilisation de Adobe Experience Platform SDK et de l’extension Edge Network. |
| [edgeconsentement](https://github.com/adobe/aepsdk-edgeconsent-android) | L’extension mobile Collection de consentement Adobe Experience Platform permet la collecte de préférences de consentement à partir de l’application mobile lors de l’utilisation de Adobe Experience Platform SDK et de l’extension Edge Network. |
| [userprofile](https://github.com/adobe/aepsdk-userprofile-android) | L’extension Adobe Experience Platform User Profile Mobile est une extension permettant de gérer les profils utilisateur pour Adobe Experience Platform SDK. |
| [aepplaces](https://github.com/adobe/aepsdk-places-android) | Adobe Places Service est un service de géolocalisation qui permet aux applications mobiles de connaître l’emplacement de l’utilisateur. Et pour comprendre le contexte de l’emplacement en utilisant des interfaces SDK riches et faciles à utiliser, accompagnées d’une base de données flexible de points ciblés (POI). Pour plus d’informations, voir la documentation du service Places .<br/>Ce service est l&#39;extension mobile Places pour le SDK Adobe Experience Platform Android 2.x et nécessite l&#39;extension Core pour la gestion des événements. |
| [messagerie](https://github.com/adobe/aepsdk-messaging-android) | L’extension Adobe Experience Platform Messaging alimente les notifications push, les messages in-app et les expériences basées sur du code pour vos applications mobiles. Cette extension vous permet également de collecter des jetons push utilisateur et de gérer la mesure des interactions avec les services Adobe Experience Platform. |
| [optimiser](https://github.com/adobe/aepsdk-optimize-android) | L’extension Adobe Experience Platform Optimize fournit des API pour activer les workflows de personnalisation en temps réel dans les SDK Adobe Experience Platform à l’aide d’Adobe Target ou de Adobe Journey Optimizer Offer Decisioning. Elle dépend de Mobile Core et nécessite l’extension Edge pour envoyer des événements de requête de personnalisation à Experience Edge Network. |
| [assurance](https://github.com/adobe/aepsdk-assurance-android) | Assurance (également appelé projet Griffon) est une extension mobile pour Adobe Experience Platform qui permet de s’intégrer à Adobe Experience Platform Assurance. L’extension permet d’inspecter, de corriger, de simuler et de valider la manière dont vous collectez les données ou dont les expériences sont diffusées dans votre application mobile. Cette extension nécessite MobileCore. |

## Importer des extensions

Dans Android Studio, accédez à **[!UICONTROL app]** > **[!UICONTROL kotlin+java]** > **[!UICONTROL com.adobe.luma.tutorial.android]** > **[!UICONTROL LumaApplication]** et assurez-vous que les imports ci-dessous font partie du fichier source.

```kotlin
import com.adobe.marketing.mobile.Assurance
import com.adobe.marketing.mobile.Edge
import com.adobe.marketing.mobile.Lifecycle
import com.adobe.marketing.mobile.LoggingMode
import com.adobe.marketing.mobile.Messaging
import com.adobe.marketing.mobile.MobileCore
import com.adobe.marketing.mobile.MobilePrivacyStatus
import com.adobe.marketing.mobile.Places
import com.adobe.marketing.mobile.Signal
import com.adobe.marketing.mobile.UserProfile
import com.adobe.marketing.mobile.edge.consent.Consent
import com.adobe.marketing.mobile.edge.identity.Identity
import com.adobe.marketing.mobile.optimize.Optimize
```

Faites de même pour **[!UICONTROL app]** > **[!UICONTROL kotlin+java]** > **[!UICONTROL com.adobe.luma.tutorial.android]** > **[!UICONTROL models]** > **[!UICONTROL MobileSDK]**.


## Mettre à jour l’application Luma

Dans la vue **[!UICONTROL Android]**, accédez à **[!UICONTROL app]** > **[!UICONTROL kotlin+java]** > **[!UICONTROL com.adobe.luma.tutorial.android]** > **[!UICONTROL LumaApplication]** dans Android Studio.

1. Remplacez `"YOUR_ENVIRONMENT_FILE_ID"` dans `private var environmentFileId = "YOUR_ENVIRONMENT_ID_GOES_HERE"` par la valeur de l’identifiant du fichier d’environnement que vous avez récupérée à partir des balises dans [Générer les instructions d’installation de SDK](configure-tags.md#generate-sdk-install-instructions).

   ```kotlin
   private var environmentFileId = "YOUR_ENVIRONMENT_ID_GOES_HERE"
   ```

1. Ajoutez le code suivant à `override fun onCreate()` fonction dans `class LumaApplication : Application()`.

   ```kotlin
   // Define extensions
   val extensions = listOf(
      Identity.EXTENSION,
      Lifecycle.EXTENSION,
      Signal.EXTENSION,
      Edge.EXTENSION,
      Consent.EXTENSION,
      UserProfile.EXTENSION,
      Places.EXTENSION,
      Messaging.EXTENSION,
      Optimize.EXTENSION,
      Assurance.EXTENSION
   )
   
   // Register extensions
   MobileCore.registerExtensions(extensions) {
   // Use the environment file id assigned to this application via Adobe Experience Platform Data Collection
     Log.i("Luma", "Using mobile config: $environmentFileId")
     MobileCore.configureWithAppID(environmentFileId)
   
     // set this to true when testing on your device, default is false.
     //MobileCore.updateConfiguration(mapOf("messaging.useSandbox" to true))
   
     // assume unknown, adapt to your needs.
     MobileCore.setPrivacyStatus(MobilePrivacyStatus.UNKNOWN)
   }
   ```

   Le code ci-dessus effectue les opérations suivantes :

   1. Enregistre les extensions requises.
   1. Configure MobileCore et d’autres extensions pour utiliser la configuration de propriété de balise.
   1. Active la journalisation du débogage. Vous trouverez plus d’informations et d’options dans la documentation de Adobe Experience Platform Mobile SDK [&#128279;](https://developer.adobe.com/client-sdks/documentation/getting-started/enable-debug-logging/).
   1. Démarre la surveillance du cycle de vie. Voir l’étape [Cycle de vie](lifecycle-data.md) du tutoriel pour plus d’informations.
   1. Définit le consentement par défaut sur inconnu. Voir l’étape [Consentement](consent.md) du tutoriel pour plus d’informations.

Veillez à mettre à jour `MobileCore.configureWith(environmentFileId)` avec le `environmentFileId` en fonction de l’identifiant de fichier d’environnement de l’environnement de balises pour lequel vous créez des balises (développement, évaluation ou production).


>[!ENDTABS]

>[!SUCCESS]
>
>Vous avez maintenant installé les packages nécessaires et mis à jour votre projet afin d’enregistrer les extensions Adobe Experience Platform Mobile SDK requises que vous allez utiliser pour la suite du tutoriel.
>
>Merci d’avoir consacré votre temps à découvrir Adobe Experience Platform Mobile SDK. Si vous avez des questions, souhaitez partager des commentaires généraux ou des suggestions sur le contenu futur, partagez-les dans ce [article de discussion de la communauté Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796?profile.language=fr)

Suivant : **[Configuration d’Assurance](assurance.md)**
