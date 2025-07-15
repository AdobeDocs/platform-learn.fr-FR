---
title: Remplacez SDK - Migrez l’implémentation d’Adobe Target dans votre application mobile vers l’extension Offer Decisioning et Target.
description: Découvrez comment remplacer SDK lors de la migration d’Adobe Target vers l’extension Offer Decisioning et Target Mobile.
exl-id: f1b77cad-792b-4a80-acff-e1a2f29250e1
source-git-commit: 876e664a213aec954105bf2d5547baab5d8a84ea
workflow-type: tm+mt
source-wordcount: '726'
ht-degree: 2%

---

# Remplacer le SDK cible par le SDK d’optimisation

Découvrez comment remplacer les SDK Adobe Target par les SDK Optimize dans votre implémentation mobile. Un remplacement de base comprend les étapes suivantes :

* Mettre à jour les dépendances dans votre fichier Podfile ou `build.gradle`
* Mettre à jour les imports
* Mettre à jour le code de l’application


>[!INFO]
>
>Dans l’écosystème Adobe Experience Platform Mobile SDK, les extensions sont implémentées par des SDK importés dans vos applications, qui peuvent porter des noms différents :
>
> * **Target SDK** met en œuvre l’extension **Adobe Target**
> * **Optimiser SDK** implémente l’extension **Offer Decisioning et Target**

## Mettre à jour les dépendances

Exemple Android

>[!BEGINTABS]

>[!TAB Optimisation de SDK]

`build.gradle` des dépendances après la migration

```Java
implementation platform('com.adobe.marketing.mobile:sdk-bom:3.+')
implementation 'com.adobe.marketing.mobile:core'
implementation 'com.adobe.marketing.mobile:edgeidentity'
implementation 'com.adobe.marketing.mobile:edge'
implementation 'com.adobe.marketing.mobile:optimize'
```


>[!TAB SDK Target]

`build.gradle` les dépendances avant la migration

```Java
implementation platform('com.adobe.marketing.mobile:sdk-bom:3.+')
implementation 'com.adobe.marketing.mobile:analytics'
implementation 'com.adobe.marketing.mobile:target'
implementation 'com.adobe.marketing.mobile:core'
implementation 'com.adobe.marketing.mobile:identity'
implementation 'com.adobe.marketing.mobile:lifecycle'
implementation 'com.adobe.marketing.mobile:signal'
implementation 'com.adobe.marketing.mobile:userprofile'
```


>[!ENDTABS]

+++

+++ Exemple iOS

>[!BEGINTABS]


>[!TAB Optimisation de SDK]

`Podfile` des dépendances après la migration

```Swift
use_frameworks!
target 'YourAppTarget' do
    pod 'AEPCore', '~> 5.0'
    pod 'AEPEdge', '~> 5.0'
    pod 'AEPEdgeIdentity', '~> 5.0'
    pod 'AEPOptimize', '~> 5.0'
end
```

>[!TAB SDK Target]

`Podfile` les dépendances avant la migration

```Swift
use_frameworks!
pod 'AEPAnalytics', '~> 5.0'
pod 'AEPTarget', '~> 5.0'
pod 'AEPCore', '~> 5.0'
pod 'AEPIdentity', '~> 5.0'
pod 'AEPSignal', '~>5.0'
pod 'AEPLifecycle', '~>5.0'
pod 'AEPUserProfile', '~> 5.0'
```

>[!ENDTABS]

+++

## Mise à jour des imports et du code

+++ Exemple Android

>[!BEGINTABS]

>[!TAB Optimisation de SDK]

Code d’initialisation Java après la migration

```Java
import com.adobe.marketing.mobile.MobileCore;
import com.adobe.marketing.mobile.Edge;
import com.adobe.marketing.mobile.edge.identity.Identity;
import com.adobe.marketing.mobile.optimize.Optimize;
import com.adobe.marketing.mobile.AdobeCallback;
 
public class MainApp extends Application {
 
  private final String ENVIRONMENT_FILE_ID = "YOUR_APP_ENVIRONMENT_ID";
 
    @Override
    public void onCreate() {
        super.onCreate();
 
        MobileCore.setApplication(this);
        MobileCore.configureWithAppID(ENVIRONMENT_FILE_ID);
 
        MobileCore.registerExtensions(
            Arrays.asList(Edge.EXTENSION, Identity.EXTENSION, Optimize.EXTENSION),
            o -> Log.d("MainApp", "Offer Decisioning and Target Mobile SDK was initialized.")
        );
    }
}
```

>[!TAB SDK Target]

Code d’initialisation Java avant la migration

```Java
import com.adobe.marketing.mobile.AdobeCallback;
import com.adobe.marketing.mobile.Analytics;
import com.adobe.marketing.mobile.Extension;
import com.adobe.marketing.mobile.Identity;
import com.adobe.marketing.mobile.Lifecycle;
import com.adobe.marketing.mobile.LoggingMode;
import com.adobe.marketing.mobile.MobileCore;
import com.adobe.marketing.mobile.Signal;
import com.adobe.marketing.mobile.Target;
import com.adobe.marketing.mobile.UserProfile;
import java.util.Arrays;
import java.util.List;
...
import android.app.Application;
...
public class MainApp extends Application {
...
    @Override
    public void onCreate() {
        super.onCreate();
        MobileCore.setApplication(this);
        MobileCore.setLogLevel(LoggingMode.DEBUG);
        ...
        List<Class<? extends Extension>> extensions = Arrays.asList(
            Analytics.EXTENSION,
            Target.EXTENSION,
            Identity.EXTENSION,
            Lifecycle.EXTENSION,
            Signal.EXTENSION,
            UserProfile.EXTENSION
        );
 
 
        MobileCore.registerExtensions(extensions, new AdobeCallback () {
            @Override
            public void call(Object o) {
                MobileCore.configureWithAppID(<Environment File ID>);
            }
        });
    }
}
```

>[!ENDTABS]

+++

+++ iOS

>[!BEGINTABS]

>[!TAB Optimisation de SDK]

Code d’initialisation rapide après la migration

```Swift
import AEPCore
import AEPEdge
import AEPEdgeIdentity
import AEPOptimize
 
@UIApplicationMain
final class AppDelegate: UIResponder, UIApplicationDelegate {
  var window: UIWindow?
 
  func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplication.LaunchOptionsKey: Any]? = nil) -> Bool {
 
      // register the extensions
      MobileCore.registerExtensions([Edge.self, AEPEdgeIdentity.Identity.self, Optimize.self]) {
        MobileCore.configureWith(appId: <YOUR_ENVIRONMENT_FILE_ID>) // Replace <YOUR_ENVIRONMENT_FILE_ID> with a String containing your own ID.
      }
 
      return true
  }
}
```

>[!TAB SDK Target]

Code d’initialisation rapide avant la migration

```Swift
import AEPCore
import AEPAnalytics
import AEPTarget
import AEPIdentity
import AEPLifecycle
import AEPSignal
import AEPServices
import AEPUserProfile
...
@UIApplicationMain
class AppDelegate: UIResponder, UIApplicationDelegate {
    func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplication.LaunchOptionsKey: Any]?) -> Bool {
        MobileCore.setLogLevel(.debug)
        let appState = application.applicationState
        ...
        let extensions = [
            Analytics.self,
            Target.self,
            Identity.self,
            Lifecycle.self,
            Signal.self,
            UserProfile.self
        ]
        MobileCore.registerExtensions(extensions, {
        MobileCore.configureWith(<Environment File ID>)
        if appState != .background {
            MobileCore.lifecycleStart(additionalContextData: ["contextDataKey": "contextDataVal"])
            }
        })
        ...
        return true
    }
}
```

>[!ENDTABS]

+++

## Comparaison des API

De nombreuses API d’extension Target ont une approche équivalente utilisant l’extension Offer Decisioning et Target décrite dans le tableau ci-dessous. Pour plus d’informations sur les [fonctions](https://developer.adobe.com/client-sdks/edge/adobe-journey-optimizer-decisioning/api-reference/), consultez la référence de l’API .

| Extension Target | Extension Offer Decisioning and Target | Notes |
| --- | --- | --- | 
| [prefetchContent](https://developer.adobe.com/client-sdks/solution/adobe-target/api-reference/#prefetchcontent){target=_blank} | [updatePropositions](https://developer.adobe.com/client-sdks/edge/adobe-journey-optimizer-decisioning/api-reference/#updatepropositionswithcompletionhandlerandtimeout){target=_blank} |  |
| [retrieveLocationContent](https://developer.adobe.com/client-sdks/solution/adobe-target/api-reference/#retrievelocationcontent){target=_blank} | [getPropositions](https://developer.adobe.com/client-sdks/edge/adobe-journey-optimizer-decisioning/api-reference/#getpropositionswithtimeout){target=_blank} | Lors de l’utilisation de l’API `getPropositions`, aucun appel à distance n’est effectué pour récupérer des portées non mises en cache dans le SDK. |
| [displayLocations](https://developer.adobe.com/client-sdks/solution/adobe-target/api-reference/#retrievelocationcontent){target=_blank} | [Offre -> display()](https://developer.adobe.com/client-sdks/edge/adobe-journey-optimizer-decisioning/#proposition-tracking-using-direct-offer-class-methods){target=_blank} | En outre, `generateDisplayInteractionXdm` méthode Offre peut être utilisée pour générer le XDM pour l’affichage des articles. Par la suite, l’API sendEvent du SDK réseau Edge peut être utilisée pour joindre des données XDM à structure libre supplémentaires et envoyer un événement d’expérience à l’instance distante. |
| [clickedLocation](https://developer.adobe.com/client-sdks/solution/adobe-target/api-reference/#clickedlocation){target=_blank} | [Offre -> appuyé()](https://developer.adobe.com/client-sdks/edge/adobe-journey-optimizer-decisioning/#proposition-tracking-using-direct-offer-class-methods){target=_blank} | En outre, `generateTapInteractionXdm` méthode Offre peut être utilisée pour générer le fichier XDM pour l’appui sur l’élément. Par la suite, l’API sendEvent du SDK réseau Edge peut être utilisée pour joindre des données XDM à structure libre supplémentaires et envoyer un événement d’expérience à l’instance distante. |
| [clearPrefetchCache](https://developer.adobe.com/client-sdks/solution/adobe-target/api-reference/#clickedlocation){target=_blank} | [clearCachedPropositions](https://developer.adobe.com/client-sdks/edge/adobe-journey-optimizer-decisioning/#proposition-tracking-using-direct-offer-class-methods){target=_blank} |  |
| [resetExperience](https://developer.adobe.com/client-sdks/solution/adobe-target/api-reference/#resetexperience){target=_blank} | S.O. | Utilisez l’API [removeIdentity](https://developer.adobe.com/client-sdks/edge/identity-for-edge-network/api-reference/#removeidentity){target=_blank} de l’extension Identity for Edge Network pour SDK afin de cesser d’envoyer l’identifiant visiteur au réseau Edge. Pour plus d’informations, voir [documentation de l’API removeIdentity](https://developer.adobe.com/client-sdks/edge/identity-for-edge-network/api-reference/#removeidentity). <br><br>Remarque : l’API `resetIdentities` de Mobile Core efface toutes les identités stockées dans le SDK, y compris l’Experience Cloud ID (ECID), et elle doit être utilisée avec parcimonie ! |
| [getSessionId](https://developer.adobe.com/client-sdks/solution/adobe-target/api-reference/#getsessionid){target=_blank} | S.O. | `state:store` handle de réponse transfère les informations relatives à la session. L’extension de réseau Edge permet de le gérer en joignant des éléments de magasin d’état non expirés aux requêtes suivantes. |
| [setSessionId](https://developer.adobe.com/client-sdks/solution/adobe-target/api-reference/#setsessionid){target=_blank} | S.O. | `state:store` handle de réponse transfère les informations relatives à la session. L’extension de réseau Edge permet de le gérer en joignant des éléments de magasin d’état non expirés aux requêtes suivantes. |
| [getThirdPartyId](https://developer.adobe.com/client-sdks/solution/adobe-target/api-reference/#getthirdpartyid){target=_blank} | S.O. | Utilisez l’API updateIdentities de l’extension Identity for Edge Network pour fournir la valeur de l’ID tiers. Configurez ensuite l’espace de noms d’ID tiers dans le flux de données. Pour plus d’informations, voir [documentation mobile ID tiers de Target](https://developer.adobe.com/client-sdks/edge/adobe-journey-optimizer-decisioning/#target-third-party-id). |
| [setThirdPartyId](https://developer.adobe.com/client-sdks/solution/adobe-target/api-reference/#setthirdpartyid){target=_blank} | S.O. | Utilisez l’API updateIdentities de l’extension Identity for Edge Network pour fournir la valeur de l’ID tiers. Configurez ensuite l’espace de noms d’ID tiers dans le flux de données. Pour plus d’informations, voir [documentation mobile ID tiers de Target](https://developer.adobe.com/client-sdks/edge/adobe-journey-optimizer-decisioning/#target-third-party-id). |
| [getTntId](https://developer.adobe.com/client-sdks/solution/adobe-target/api-reference/#gettntid){target=_blank} | S.O. | `locationHint:result` descripteur de réponse contient les informations relatives à l’indicateur d’emplacement cible. On suppose que Target Edge sera co-implanté avec Experience Edge. <br> <br>L’extension de réseau Edge utilise l’indicateur d’emplacement EdgeNetwork pour déterminer le cluster réseau Edge auquel envoyer des requêtes. Pour partager l’indicateur d’emplacement réseau Edge sur plusieurs SDK (applications hybrides), utilisez les API `getLocationHint` et `setLocationHint` de l’extension Edge Network. Pour plus d’informations, voir [documentation de l’API `getLocationHint`](https://developer.adobe.com/client-sdks/edge/edge-network/api-reference/#getlocationhint). |
| [setTntId](https://developer.adobe.com/client-sdks/solution/adobe-target/api-reference/#gettntid){target=_blank} | S.O. | Le handle de réponse [locationHint:result](https://developer.adobe.com/client-sdks/edge/edge-network/api-reference/#setlocationhint){target=_blank} transfère les informations sur l’indicateur d’emplacement de Target. On suppose que Target Edge sera co-implanté avec Experience Edge. <br> <br>L’extension de réseau Edge utilise l’indicateur d’emplacement EdgeNetwork pour déterminer le cluster réseau Edge auquel envoyer des requêtes. Pour partager l’indicateur d’emplacement réseau Edge sur plusieurs SDK (applications hybrides), utilisez les API `getLocationHint` et `setLocationHint` de l’extension Edge Network. Pour plus d’informations, voir [documentation de l’API `getLocationHint`](https://developer.adobe.com/client-sdks/edge/edge-network/api-reference/#getlocationhint). |


Ensuite, découvrez comment [demander et effectuer le rendu des activités](retrieve-activities.md) sur la page.

>[!NOTE]
>
>Nous nous engageons à vous aider à réussir votre migration mobile de Target vers l’extension Offer Decisioning et Target. Si vous rencontrez des obstacles avec votre migration ou si vous pensez qu&#39;il manque des informations essentielles dans ce guide, veuillez nous le faire savoir en postant dans [cette discussion communautaire](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-adobe-target-to-mobile-sdk-on-edge/m-p/747484#M625).
