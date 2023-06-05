---
title: Installation des SDK Adobe Experience Platform Mobile
description: Découvrez comment mettre en oeuvre le SDK Mobile Adobe Experience Platform dans une application mobile.
exl-id: 98d6f59e-b8a3-4c63-ae7c-8aa11e948f59
source-git-commit: b2e1bf08d9fb145ba63263dfa078c96258342708
workflow-type: tm+mt
source-wordcount: '573'
ht-degree: 2%

---

# Installation des SDK Adobe Experience Platform Mobile

Découvrez comment mettre en oeuvre le SDK Mobile Adobe Experience Platform dans une application mobile.

## Conditions préalables

* La bibliothèque de balises a été créée avec succès avec les extensions décrites dans la section [leçon précédente](configure-tags.md).
* Identifiant du fichier d’environnement de développement du [Instructions d’installation mobile](configure-tags.md#generate-sdk-install-instructions).
* Téléchargé, vide [exemple d’application](https://github.com/Adobe-Marketing-Cloud/Luma-iOS-Mobile-App){target="_blank"}.
* Expérience avec [XCode](https://developer.apple.com/xcode/){target="_blank"}.
* De base [ligne de commande](https://en.wikipedia.org/wiki/Command-line_interface){target="_blank"} connaissance.

## Objectifs d&#39;apprentissage

Dans cette leçon, vous allez :

* Mettez à jour votre fichier CocoaPod .
* Importez les SDK requis.
* Enregistrez les extensions.

>[!NOTE]
>
>Dans une mise en oeuvre d’applications mobiles, les termes &quot;extensions&quot; et &quot;SDK&quot; sont presque interchangeables.


## Mettre à jour le fichier de capsule

>[!NOTE]
>
> Si vous ne connaissez pas les CocoaPods, veuillez consulter les [guide de prise en main](https://guides.cocoapods.org/using/getting-started.html).

L’installation est généralement une simple commande sudo :

```console
sudo gem install cocoapods
```

Une fois que CocoaPods est installé, ouvrez le fichier de capsule.

![initial podfile](assets/mobile-install-initial-podfile.png)

Mettez à jour le fichier pour inclure les capsules suivantes :

```swift
pod 'AEPCore', '~> 3'
pod 'AEPEdge', '~> 1'
pod 'AEPUserProfile', '~> 3'
pod 'AEPAssurance', '~> 3'
pod 'AEPServices', '~> 3'
pod 'AEPEdgeConsent', '~> 1'
pod 'AEPLifecycle', '~>3'
pod 'AEPMessaging', '~>1'
pod 'AEPEdgeIdentity', '~>1'
pod 'AEPSignal', '~>3'
```

>[!NOTE]
>
> `AEPMessaging` n’est nécessaire que si vous prévoyez de mettre en oeuvre la messagerie push à l’aide de Adobe Journey Optimizer. Veuillez lire le tutoriel sur [implémentation de la messagerie push avec Adobe Journey Optimizer](journey-optimizer-push.md) pour plus d’informations.

Après avoir enregistré les modifications dans votre fichier de capsule, accédez au dossier contenant votre projet et exécutez le `pod install` pour installer vos modifications.

![pod install](assets/mobile-install-podfile-install.png)

>[!NOTE]
>
> Si vous obtenez le fichier &quot;Aucun fichier de capsule trouvé dans le répertoire du projet&quot;. , votre terminal se trouve dans le mauvais dossier. Accédez au dossier contenant le fichier de capsule que vous avez mis à jour, puis réessayez.

Si vous souhaitez effectuer la mise à niveau vers la dernière version, exécutez le `pod update` .

>[!INFO]
>
>Si vous ne pouvez pas utiliser CocoaPods dans vos propres applications, vous pouvez en savoir plus sur d’autres [implémentations prises en charge](https://github.com/adobe/aepsdk-core-ios#binaries) dans le projet GitHub.

## Créer des CocoaPods

Pour créer des CocoaPods, ouvrez `Luma.xcworkspace`, puis sélectionnez **Produit**, suivie de **Dossier de génération propre**.

>[!NOTE]
>
> Vous devrez peut-être définir **Créer une architecture Principale uniquement** to **Non**. Pour ce faire, sélectionnez le projet Pods dans le navigateur de projet, puis sélectionnez **Paramètres de création**, puis définissez la variable **Créer une architecture Principale** to **Non**.

Vous pouvez désormais créer et exécuter le projet.

![paramètres de création](assets/mobile-install-build-settings.png)

>[!NOTE]
>
>Le projet Luma a été créé avec Xcode v12.5 sur un jeu de puces M1 et s’exécute sur le simulateur iOS. Si vous utilisez une autre configuration, vous devrez peut-être modifier vos paramètres de génération pour refléter votre architecture.
>
>Si votre version n’a pas réussi, essayez de rétablir la variable **Créer une architecture Principale** > **Déboguer** de retour à **Oui**.
>
>La configuration du simulateur &quot;iPod touch (7e génération)&quot; a été utilisée lors de la création de ce tutoriel.

## Importation d’extensions

Dans chaque `.swift` ajoutez les imports suivants. Commencez par ajouter à `AppDelegate.swift`.

```swift
import AEPUserProfile
import AEPAssurance
import AEPEdge
import AEPCore
import AEPEdgeIdentity
import AEPEdgeConsent
import AEPLifecycle
import AEPMessaging //Optional, used for AJO push messaging
import AEPSignal
import AEPServices
```

## Mettre à jour AppDelegate

Dans le `AppDelegate.swift` , ajoutez le code suivant à `didFinishLaunchingWithOptions`. Remplacez currentAppId par la valeur ID du fichier d’environnement de développement que vous avez récupérée à partir des balises dans la variable [leçon précédente](configure-tags.md).

```swift
let currentAppId = "b5cbd1a1220e/bae66382cce8/launch-88492c6dcb6e-development"

let extensions = [Edge.self, Assurance.self, Lifecycle.self, UserProfile.self, Consent.self, AEPEdgeIdentity.Identity.self, Messaging.self]

MobileCore.setLogLevel(.trace)

MobileCore.registerExtensions(extensions, {
    MobileCore.configureWith(appId: currentAppId)
})
```

`Messaging.self` n’est requis que si vous prévoyez de mettre en oeuvre la messagerie push via Adobe Journey Optimizer comme décrit [here](journey-optimizer-push.md).

Le code ci-dessus effectue les opérations suivantes :

* Enregistre les extensions requises.
* Configure MobileCore et d’autres extensions pour utiliser la configuration de la propriété de balise.
* Active la journalisation de débogage. Vous trouverez plus de détails et d’options dans la section [Documentation du SDK Mobile](https://developer.adobe.com/client-sdks/documentation/getting-started/enable-debug-logging/).

>[!IMPORTANT]
>Dans une application de production, vous devez changer AppId en fonction de l’environnement actuel (dev/stag/prod).

Suivant : **[Configuration d’Assurance](assurance.md)**

>[!NOTE]
>
>Merci d’avoir consacré votre temps à l’apprentissage du SDK Adobe Experience Platform Mobile. Si vous avez des questions, souhaitez partager des commentaires généraux ou avez des suggestions sur le contenu futur, partagez-les à ce sujet. [Article de discussion de la communauté Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796)