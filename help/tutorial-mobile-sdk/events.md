---
title: Suivre les données d’événement dans les applications mobiles avec Experience Platform Mobile SDK
description: Découvrez comment effectuer le suivi des données d’événement dans une application mobile.
jira: KT-14631
exl-id: 4779cf80-c143-437b-8819-1ebc11a26852
source-git-commit: 4a0fa85c76c00fd505118692ea4b6cbe410f5839
workflow-type: tm+mt
source-wordcount: '1698'
ht-degree: 2%

---

# Suivi des données d’événement

Découvrez comment suivre les événements dans une application mobile.

L’extension Edge Network fournit une API pour envoyer des événements d’expérience à Platform Edge Network. Un événement d’expérience est un objet contenant des données conformes à la définition de schéma XDM ExperienceEvent. Plus simplement, ces événements capturent ce que les gens font dans votre application mobile. Une fois que Platform Edge Network a reçu des données, ces données peuvent être transférées vers les applications et services configurés dans votre flux de données, tels qu’Adobe Analytics et Experience Platform. En savoir plus sur le [Événements d’expérience](https://developer.adobe.com/client-sdks/documentation/getting-started/track-events/) dans la documentation du produit.

## Conditions préalables

* Toutes les dépendances de package sont configurées dans votre projet Xcode.
* Extensions enregistrées dans **[!UICONTROL AppDelegate]**.
* Extension MobileCore configurée pour utiliser votre `appId` de développement.
* SDK importés.
* L’application a été créée et exécutée avec les modifications ci-dessus.

## Objectifs d’apprentissage

Dans cette leçon, vous allez :

* comprendre comment structurer les données XDM en fonction d’un schéma ;
* Envoyez un événement XDM basé sur un groupe de champs standard.
* Envoyer un événement XDM basé sur un groupe de champs personnalisés
* Envoyez un événement d’achat XDM.
* Effectuez la validation avec Assurance.

## Création d’un événement d’expérience

L’extension Adobe Experience Platform Edge peut envoyer à Adobe Experience Platform Edge Network des événements qui suivent un schéma XDM défini précédemment.

Le processus se passe comme suit...

1. Identifiez l’interaction de l’application mobile que vous essayez de suivre.

1. Vérifiez votre schéma et identifiez l’événement approprié.

1. Passez en revue votre schéma et identifiez les champs supplémentaires qui doivent être utilisés pour décrire l’événement.

1. Créez et renseignez l’objet de données.

1. Créer et envoyer un événement.

1. Validez.


### Groupes de champs standard

Pour les groupes de champs standard, le processus se présente comme suit :

* Dans votre schéma, identifiez les événements que vous essayez de collecter. Dans cet exemple, vous effectuez le suivi d’événements d’expérience commerciale, par exemple un événement de consultation de produit (**[!UICONTROL productViews]**).

  ![schéma d’affichage du produit](assets/datacollection-prodView-schema.png){zoomable="yes"}

* Pour construire un objet contenant les données d’événement d’expérience dans votre application, vous devez utiliser un code du type :

>[!BEGINTABS]

>[!TAB iOS]

```swift
var xdmData: [String: Any] = [
    "eventType": "commerce.productViews",
    "commerce": [
        "productViews": [
        "value": 1
        ]
    ]
]
```

Dans ce code :

* `eventType` : décrit l’événement qui s’est produit ; utilisez une [valeur connue](https://github.com/adobe/xdm/blob/master/docs/reference/classes/experienceevent.schema.md#xdmeventtype-known-values) si possible.

* `commerce.productViews.value` : valeur numérique ou booléenne de l’événement. S’il s’agit d’une valeur booléenne (ou « compteur » dans Adobe Analytics), la valeur est toujours définie sur 1. S’il s’agit d’un événement numérique ou monétaire, la valeur peut être > 1.

>[!TAB Android]

```kotlin
val xdmData = mapOf(
    "eventType" to "commerce.productViews",
    "commerce" to mapOf(
        "productViews" to mapOf(
        "value": 1
        )
    )
)
```

Dans ce code :

* `eventType` : décrit l’événement qui s’est produit ; utilisez une [valeur connue](https://github.com/adobe/xdm/blob/master/docs/reference/classes/experienceevent.schema.md#xdmeventtype-known-values) si possible.

* `commerce.productViews.value` : valeur numérique ou booléenne de l’événement. S’il s’agit d’une valeur booléenne (ou « compteur » dans Adobe Analytics), la valeur est toujours définie sur 1. S’il s’agit d’un événement numérique ou monétaire, la valeur peut être > 1.

>[!ENDTABS]


* Dans votre schéma, identifiez toutes les données supplémentaires associées à l’événement d’affichage du produit de commerce. Dans cet exemple, incluez **[!UICONTROL productListItems]** qui est un ensemble standard de champs utilisés avec n’importe quel événement lié au commerce :

  ![schéma des éléments de la liste de produits](assets/datacollection-prodListItems-schema.png){zoomable="yes"}
   * Notez que **[!UICONTROL productListItems]** est un tableau, de sorte que plusieurs produits peuvent être fournis.

* Pour ajouter ces données, développez votre objet `xdmData` afin d’inclure des données supplémentaires :

>[!BEGINTABS]

>[!TAB iOS]

```swift
var xdmData: [String: Any] = [
    "eventType": "commerce.productViews",
    "commerce": [
        "productViews": [
            "value": 1
        ]
    ],
    "productListItems": [
        [
            "name":  productName,
            "SKU": sku,
            "priceTotal": priceString,
            "quantity": 1
        ]
    ]
]
```

>[!TAB Android]

```kotlin
val xdmData = mapOf(
    "eventType" to "commerce.productViews",
    "commerce" to mapOf(
        "productViews" to mapOf(
        "value": 1
        )
    ),
    "productListItems" to mapOf(
        "name": productName,
        "SKU": sku,
        "priceTotal", priceString,
        "quantity", 1
    )
)
```

>[!ENDTABS]

* Vous pouvez désormais utiliser cette structure de données pour créer un `ExperienceEvent` :

>[!BEGINTABS]

>[!TAB iOS]

```swift
let productViewEvent = ExperienceEvent(xdm: xdmData)
```

>[!TAB Android]

```kotlin
val productViewEvent = ExperienceEvent.Builder().setXdmSchema(xdmData).build()
```

>[!ENDTABS]

* Et envoyez l’événement et les données à Platform Edge Network à l’aide de l’API `sendEvent` :

>[!BEGINTABS]

>[!TAB iOS]

```swift
Edge.sendEvent(experienceEvent: productViewEvent)
```

>[!TAB Android]

```kotlin
Edge.sendEvent(productViewEvent, null)
```

>[!ENDTABS]


L’API [`Edge.sendEvent`](https://developer.adobe.com/client-sdks/documentation/edge-network/api-reference/#sendevent) est l’équivalent du SDK Mobile AEP des appels API [`MobileCore.trackAction`](https://developer.adobe.com/client-sdks/documentation/mobile-core/api-reference/#trackaction) et [`MobileCore.trackState`](https://developer.adobe.com/client-sdks/documentation/mobile-core/api-reference/#trackstate). Consultez [ Migration de l’extension mobile Analytics vers Adobe Experience Platform Edge Network ](https://developer.adobe.com/client-sdks/documentation/adobe-analytics/migrate-to-edge-network/) pour plus d’informations.

Vous êtes sur le point d’implémenter ce code dans votre projet.
Votre application comporte différentes actions liées à des produits commerciaux et vous souhaitez envoyer des événements en fonction de ces actions, telles qu’elles sont effectuées par l’utilisateur :

* afficher : se produit lorsqu’un utilisateur ou une utilisatrice consulte un produit spécifique,
* ajouter au panier : lorsqu’un utilisateur appuie sur ![ShoppingCart](/help/assets/icons/ShoppingCart.svg) dans l’écran des détails du produit,
* enregistrer pour plus tard : lorsqu’un utilisateur clique sur ![Cœur](/help/assets/icons/Heart.svg) / ![ThumbUp](/help/assets/icons/ThumbUp.svg) dans l’écran des détails du produit,
* achat : lorsqu’un utilisateur clique sur ![Carte de crédit](/help/assets/icons/CreditCard.svg) dans l’écran des détails du produit.

Pour implémenter l’envoi d’événements d’expérience liés au commerce de manière réutilisable, vous utilisez une fonction dédiée :

>[!BEGINTABS]

>[!TAB iOS]

1. Accédez à **[!DNL Luma]** > **[!DNL Luma]** > **[!DNL Utils]** > **[!UICONTROL MobileSDK]** dans le navigateur de projet Xcode, puis ajoutez les éléments suivants à la fonction `func sendCommerceExperienceEvent(commerceEventType: String, product: Product)`.

   ```swift
   // Set up a data dictionary, create an experience event and send the event.
   let xdmData: [String: Any] = [
       "eventType": "commerce." + commerceEventType,
       "commerce": [
           commerceEventType: [
               "value": 1
           ]
       ],
       "productListItems": [
           [
               "name": product.name,
               "priceTotal": product.price,
               "SKU": product.sku
           ]
       ]
   ]
   
   let commerceExperienceEvent = ExperienceEvent(xdm: xdmData)
   Edge.sendEvent(experienceEvent: commerceExperienceEvent)
   ```

   Cette fonction prend le type d’événement d’expérience commerciale et le produit comme paramètres et

   * configure la payload XDM sous la forme d’un dictionnaire, à l’aide des paramètres de la fonction ,
   * configure un événement d’expérience à l’aide du dictionnaire ;
   * envoie l’événement d’expérience à l’aide de l’API [`Edge.sendEvent`](https://developer.adobe.com/client-sdks/documentation/edge-network/api-reference/#sendevent).

1. Accédez à **[!DNL Luma]** > **[!DNL Luma]** > **[!DNL Views]** > **[!DNL Products]** > **[!UICONTROL ProductView]** dans le navigateur de projet Xcode et ajoutez divers appels à la fonction `sendCommerceExperienceEvent` :

   1. Au niveau du modificateur `.task`, dans la fermeture `ATTrackingManager.trackingAuthorizationStatus`. Ce modificateur de `.task` est appelé lors de l&#39;initialisation et de l&#39;affichage de la vue de produit. Vous souhaitez donc envoyer un événement de vue de produit à ce moment précis.

      ```swift
      // Send productViews commerce experience event
      MobileSDK.shared.sendCommerceExperienceEvent(commerceEventType: "productViews", product: product)
      ```

   1. Pour chacun des boutons (![Cœur](/help/assets/icons/Heart.svg), ![Panier](/help/assets/icons/ShoppingCart.svg) et ![Carte de crédit](/help/assets/icons/CreditCard.svg)) de la barre d’outils, ajoutez l’appel correspondant à la fermeture du `ATTrackingManager.trackingAuthorizationStatus == .authorized` :

      1. Pour ![Cœur](/help/assets/icons/Heart.svg) :

         ```swift
         // Send saveForLater commerce experience event
         MobileSDK.shared.sendCommerceExperienceEvent(commerceEventType: "saveForLaters", product: product)
         ```

      1. Pour ![ShoppingCart](/help/assets/icons/ShoppingCart.svg) :

         ```swift
         // Send productListAdds commerce experience event
         MobileSDK.shared.sendCommerceExperienceEvent(commerceEventType: "productListAdds", product: product)
         ```

      1. Pour ![CreditCard](/help/assets/icons/CreditCard.svg) :

         ```swift
         // Send purchase commerce experience event
         MobileSDK.shared.sendCommerceExperienceEvent(commerceEventType: "purchases", product: product)
         ```

>[!TAB Android]

1. Accédez à **[!UICONTROL Android]** ![ChevronDown](/help/assets/icons/ChevronDown.svg) > **[!UICONTROL app]** > **[!UICONTROL kotlin+java]** > **[!UICONTROL com.adobe.luma.tutorial.android]** > **[!UICONTROL models]** > **[!UICONTROL MobileSDK]** dans le navigateur d’Android Studio, puis ajoutez les éléments suivants à la fonction `func sendCommerceExperienceEvent(commerceEventType: String, product: Product)`.

   ```kotlin
   // Set up a data map, create an experience event and send the event.
   val xdmData = mapOf(
       "eventType" to "commerce.$commerceEventType",
       "commerce" to mapOf(commerceEventType to mapOf("value" to 1)),
       "productListItems" to listOf(
           mapOf(
               "name" to product.name,
               "priceTotal" to product.price,
               "SKU" to product.sku
           )
       )
   )
   val commerceExperienceEvent = ExperienceEvent.Builder().setXdmSchema(xdmData).build()
   Edge.sendEvent(commerceExperienceEvent, null)
   ```

   Cette fonction prend le type d’événement d’expérience commerciale et le produit comme paramètres et

   * configure la payload XDM en tant que mappage à l’aide des paramètres de la fonction ,
   * met en place un événement d’expérience à l’aide de la carte,
   * envoie l’événement d’expérience à l’aide de l’API [`Edge.sendEvent`](https://developer.adobe.com/client-sdks/documentation/edge-network/api-reference/#sendevent).

1. Accédez à **[!UICONTROL app]** > **[!UICONTROL kotlin+java]** > **[!UICONTROL com.adobe.luma.tutorial.android]** > **[!UICONTROL views]** > **[!UICONTROL ProductView.kt]** dans le navigateur d’Android Studio, puis ajoutez divers appels à la fonction `sendCommerceExperienceEvent` :

   1. Au niveau de la fonction composable `LaunchedEffect(Unit)`, vous souhaitez envoyer un événement d’affichage de produit au moment spécifique où un produit est affiché.

      ```kotlin
      // Send productViews commerce experience event
      MobileSDK.shared.sendCommerceExperienceEvent("productViews", product)
      ```

   1. Pour chacun des boutons (![ThumbUp](/help/assets/icons/ThumbUp.svg), ![ShoppingCart](/help/assets/icons/ShoppingCart.svg) et ![CreditCard](/help/assets/icons/CreditCard.svg)) de la barre d’outils, ajoutez l’appel correspondant à l’`scope.launch` du `if (MobileSDK.shared.trackingEnabled == TrackingStatus.AUTHORIZED)  statement` :

      1. Pour ![ThumbUp](/help/assets/icons/ThumbUp.svg) :

         ```kotlin
         // Send saveForLater commerce experience event
         MobileSDK.shared.sendCommerceExperienceEvent("saveForLaters", product)
         ```

      1. Pour ![ShoppingCart](/help/assets/icons/ShoppingCart.svg) :

         ```kotlin
         // Send productListAdds commerce experience event
         MobileSDK.shared.sendCommerceExperienceEvent("productListAdds", product)
         ```

      1. Pour ![CreditCard](/help/assets/icons/CreditCard.svg) :

         ```kotlin
         // Send purchase commerce experience event
         MobileSDK.shared.sendCommerceExperienceEvent("purchases", product)
         ```

>[!ENDTABS]

>[!TIP]
>
>Si vous effectuez un développement pour Android™, utilisez Map (`java.util.Map`) comme interface de base pour créer votre payload XDM.


### Groupes de champs personnalisés

Imaginez que vous souhaitiez effectuer le suivi des vues d’écran et des interactions dans l’application elle-même. N’oubliez pas que vous avez défini un groupe de champs personnalisé pour ce type d’événements.

* Dans votre schéma, identifiez les événements que vous essayez de collecter.
  ![schéma d’interaction de l’application](assets/datacollection-appInteraction-schema.png){zoomable="yes"}

* Commencez à construire votre objet.

  >[!NOTE]
  >
  >* Les groupes de champs standard commencent toujours à la racine de l’objet.
  >
  >* Les groupes de champs personnalisés commencent toujours sous un objet unique à votre organisation Experience Cloud, `_techmarketingdemos` dans cet exemple.

* Pour l’événement d’interaction de l’application, vous devez créer un objet du type :

>[!BEGINTABS]

>[!TAB iOS]

```swift
let xdmData: [String: Any] = [
    "eventType": "application.interaction",
    "_techmarketingdemos": [
    "appInformation": [
        "appInteraction": [
            "name": "login",
            "appAction": [
                "value": 1
                ]
            ]
        ]
    ]
]
```

>[!TAB Android]

```kotlin
val xdmData = mapOf(
    "eventType" to "application.interaction",
    "_techmarketingdemos" to mapOf(
        "appInformation" to mapOf(
            "appInteraction" to mapOf(
                "name" to "login",
                "appAction" to mapOf("value" to 1)
            )
        )
    )
)
```

>[!ENDTABS]

* Pour l’événement de suivi d’écran, vous devez construire un objet tel que :

>[!BEGINTABS]

>[!TAB iOS]

```swift
var xdmData: [String: Any] = [
    "eventType": "application.scene",
    "_techmarketingdemos": [
        "appInformation": [
            "appStateDetails": [
                "screenType": "App",
                "screenName": "luma: content: ios: us: en: login",
                "screenView": [
                    "value": 1
                ]
            ]
        ] 
    ]
]
```

>[!TAB Android]

```kotlin
val xdmData = mapOf(
    "eventType" to "application.scene",
    tenant.value to mapOf(
        "appInformation" to mapOf(
            "appStateDetails" to mapOf(
                "screenType" to "App",
                "screenName" to stateName,
                "screenView" to mapOf("value" to 1)
            )
        )
    )
)
```

>[!ENDTABS]



* Vous pouvez désormais utiliser cette structure de données pour créer un `ExperienceEvent`.

>[!BEGINTABS]

>[!TAB iOS]

```swift
let event = ExperienceEvent(xdm: xdmData)
```

>[!TAB Android]

```kotlin
val event = ExperienceEvent(xdmData)
```

>[!ENDTABS]


* Envoyez l’événement et les données à Platform Edge Network.

>[!BEGINTABS]

>[!TAB iOS]

```swift
Edge.sendEvent(experienceEvent: event)
```

>[!TAB Android]

```kotlin
Edge.sendEvent(event, null)
```

>[!ENDTABS]

Là encore, implémentez ce code dans votre projet.

>[!BEGINTABS]

>[!TAB iOS]

1. Pour des raisons pratiques, définissez deux fonctions dans **[!UICONTROL MobileSDK]**. Accédez à **[!DNL Luma]** > **[!DNL Luma]** > **[!DNL Utils]** > **[!UICONTROL MobileSDK]** dans le navigateur de votre projet Xcode.

   * Une pour les interactions avec l’application. Ajoutez ce code à la fonction `func sendAppInteractionEvent(actionName: String)` :

     ```swift
     // Set up a data dictionary, create an experience event and send the event.
     let xdmData: [String: Any] = [
         "eventType": "application.interaction",
         tenant : [
             "appInformation": [
                 "appInteraction": [
                     "name": actionName,
                     "appAction": [
                         "value": 1
                     ]
                 ]
             ]
         ]
     ]
     let appInteractionEvent = ExperienceEvent(xdm: xdmData)
     Edge.sendEvent(experienceEvent: appInteractionEvent)
     ```

     Cette fonction utilise le nom de l’action comme paramètre et

      * configure la payload XDM en tant que dictionnaire, à l’aide du paramètre de la fonction ;
      * configure un événement d’expérience à l’aide du dictionnaire ;
      * envoie l’événement d’expérience à l’aide de l’API [`Edge.sendEvent`](https://developer.adobe.com/client-sdks/documentation/edge-network/api-reference/#sendevent).


   * Et une pour le suivi d’écran. Ajoutez ce code à la fonction `func sendTrackScreenEvent(stateName: String) ` :

     ```swift
     // Set up a data dictionary, create an experience event and send the event.
     let xdmData: [String: Any] = [
         "eventType": "application.scene",
         tenant : [
             "appInformation": [
                 "appStateDetails": [
                     "screenType": "App",
                     "screenName": stateName,
                     "screenView": [
                         "value": 1
                     ]
                 ]
             ]
         ]
     ]
     let trackScreenEvent = ExperienceEvent(xdm: xdmData)
     Edge.sendEvent(experienceEvent: trackScreenEvent)
     ```

     Cette fonction utilise le nom de l’état comme paramètre et

      * configure la payload XDM en tant que dictionnaire, à l’aide du paramètre de la fonction ;
      * configure un événement d’expérience à l’aide du dictionnaire ;
      * envoie l’événement d’expérience à l’aide de l’API [`Edge.sendEvent`](https://developer.adobe.com/client-sdks/documentation/edge-network/api-reference/#sendevent).

1. Accédez à **[!DNL Luma]** > **[!DNL Luma]** > **[!DNL Views]** > **[!DNL General]** > **[!UICONTROL Feuille de connexion]**.

   1. Ajoutez le code en surbrillance suivant à la fermeture du bouton de connexion :

      ```swift
      // Send app interaction event
      MobileSDK.shared.sendAppInteractionEvent(actionName: "login")
      ```

   1. Ajoutez le code en surbrillance suivant au modificateur `onAppear` :

      ```swift
      // Send track screen event
      MobileSDK.shared.sendTrackScreenEvent(stateName: "luma: content: ios: us: en: login")
      ```

>[!TAB Android]

1. Pour des raisons pratiques, définissez deux fonctions dans **[!UICONTROL MobileSDK]**. Accédez à **[!UICONTROL Android]** ![ChevronDown](/help/assets/icons/ChevronDown.svg) **[!DNL app]** > **[!DNL kotlin+java]** > **[!DNL com.adobe.luma.tutorial.android]** > **[!UICONTROL models]** > **[!UICONTROL MobileSDK]** dans le navigateur d’Android Studio.

   * Une pour les interactions avec l’application. Ajoutez ce code à la fonction `fun sendAppInteractionEvent(actionName: String)` :

     ```kotlin
     // Set up a data map, create an experience event and send the event.
     val xdmData = mapOf(
         "eventType" to "application.interaction",
         tenant.value to mapOf(
             "appInformation" to mapOf(
                 "appInteraction" to mapOf(
                     "name" to actionName,
                     "appAction" to mapOf("value" to 1)
                 )
             )
         )
     )
     val appInteractionEvent = ExperienceEvent.Builder().setXdmSchema(xdmData).build()
     Edge.sendEvent(appInteractionEvent, null)
     ```

     Cette fonction utilise le nom de l’action comme paramètre et

      * configure la payload XDM en tant que mappage, à l’aide du paramètre de la fonction ,
      * met en place un événement d’expérience à l’aide de la carte,
      * envoie l’événement d’expérience à l’aide de l’API [`Edge.sendEvent`](https://developer.adobe.com/client-sdks/documentation/edge-network/api-reference/#sendevent).


   * Et une pour le suivi d’écran. Ajoutez ce code à la fonction `fun sendTrackScreenEvent(stateName: String)` :

     ```kotlin
     // Set up a data map, create an experience event and send the event.
     val xdmData = mapOf(
         "eventType" to "application.scene",
         tenant.value to mapOf(
             "appInformation" to mapOf(
                 "appStateDetails" to mapOf(
                     "screenType" to "App",
                     "screenName" to stateName,
                     "screenView" to mapOf("value" to 1)
                 )
             )
         )
     )
     val trackScreenEvent = ExperienceEvent.Builder().setXdmSchema(xdmData).build()
     Edge.sendEvent(trackScreenEvent, null)
     ```

     Cette fonction utilise le nom de l’état comme paramètre et

      * configure la payload XDM en tant que mappage, à l’aide du paramètre de la fonction ,
      * met en place un événement d’expérience à l’aide de la carte,
      * envoie l’événement d’expérience à l’aide de l’API [`Edge.sendEvent`](https://developer.adobe.com/client-sdks/documentation/edge-network/api-reference/#sendevent).

1. Accédez à **[!UICONTROL Android]** ![ChevronDown ](/help/assets/icons/ChevronDown.svg)**[!DNL app]**>**[!DNL kotlin+java]**>**[!DNL com.adobe.luma.tutorial.android]**>**[!UICONTROL &#x200B; views &#x200B;]**>**[!UICONTROL &#x200B; LoginSheet.kt &#x200B;]**

   1. Ajoutez le code en surbrillance suivant à l’événement **[!UICONTROL Button]** **[!UICONTROL onClick]** :

      ```kotlin
      // Send app interaction event
      MobileSDK.shared.sendAppInteractionEvent("login")
      ```

   1. Ajoutez le code en surbrillance suivant à la fonction composable `LaunchedEffect(Unit)` :

      ```kotlin
      // Send track screen event
      MobileSDK.shared.sendTrackScreenEvent("luma: content: android: us: en: login")
      ```

>[!ENDTABS]



## Validation

1. Consultez la section [instructions de configuration](assurance.md#connecting-to-a-session) pour connecter votre simulateur ou votre appareil à Assurance.

   1. Déplacez l’icône Assurance vers la gauche.
   1. Sélectionnez **[!UICONTROL Accueil]** dans la barre d’onglets et vérifiez que vous voyez un **[!UICONTROL ECID]**, **[!UICONTROL E-mail]** et **[!UICONTROL ID CRM]** sur l’écran d’accueil.
   1. Sélectionnez **[!DNL Products]** dans la barre d’onglets.
   1. Sélectionnez un produit.
   1. Sélectionnez ![Cœur](/help/assets/icons/Heart.svg) (iOS) ou ![ThumbUp](/help/assets/icons/ThumbUp.svg) (Android).
   1. Sélectionnez ![ShoppingCartAdd](/help/assets/icons/ShoppingCart.svg).
   1. Sélectionnez ![ Carte de crédit ](/help/assets/icons/CreditCard.svg).

>[!BEGINTABS]

>[!TAB iOS]

<img src="./assets/mobile-app-events-3.png" width="300">

>[!TAB Android]

<img src="./assets/mobile-app-events-3-android.png" width="278">

>[!ENDTABS]

1. Dans l’interface utilisateur d’Assurance, recherchez les événements **[!UICONTROL hitReceived]** du fournisseur **[!UICONTROL com.adobe.edge.konductor]**.
1. Sélectionnez l’événement et passez en revue les données XDM dans l’objet **[!UICONTROL messages]**. Vous pouvez également utiliser ![Copier](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Copy_18_N.svg) **[!UICONTROL Copier l’événement brut]** et utiliser un éditeur de texte ou de code de votre choix pour coller et inspecter l’événement.

   ![validation de la collecte de données](assets/datacollection-validation.png){zoomable="yes"}


## Étapes suivantes

Vous devriez maintenant disposer de tous les outils nécessaires pour commencer à ajouter la collecte de données à votre application. Vous pouvez ajouter plus d’informations sur la manière dont l’utilisateur interagit avec vos produits dans l’application et vous pouvez ajouter d’autres interactions d’application et appels de suivi d’écran à l’application :

* Mettez en œuvre la commande, le passage en caisse, le panier vide et d’autres fonctionnalités dans l’application et ajoutez des événements d’expérience commerciale pertinents à cette fonctionnalité.
* Répétez l’appel à `sendAppInteractionEvent` avec le paramètre approprié pour suivre d’autres interactions de l’application par l’utilisateur.
* Répétez l’appel à `sendTrackScreenEvent` avec le paramètre approprié pour effectuer le suivi des écrans affichés par l’utilisateur dans l’application.

>[!TIP]
>
>Consultez la [application terminée](https://github.com/Adobe-Marketing-Cloud/Luma-iOS-Mobile-App) pour d’autres exemples.


## Envoi d’événements à Analytics et Platform

Maintenant que vous avez collecté les événements et que vous les avez envoyés à Platform Edge Network, ils sont envoyés aux applications et services configurés dans votre [flux de données](create-datastream.md). Dans les leçons ultérieures, vous mapperez ces données à [Adobe Analytics](analytics.md), [Adobe Experience Platform](platform.md) et à d’autres solutions Adobe Experience Cloud (comme [Adobe Target](target.md) et Adobe Journey Optimizer).

>[!SUCCESS]
>
>Vous avez maintenant configuré votre application pour effectuer le suivi du commerce, des interactions de l’application et des événements de suivi d’écran vers Adobe Experience Platform Edge Network. Et à tous les services que vous avez définis dans votre flux de données.
>
>Merci d’avoir consacré votre temps à découvrir Adobe Experience Platform Mobile SDK. Si vous avez des questions, souhaitez partager des commentaires généraux ou des suggestions sur le contenu futur, partagez-les dans ce [article de discussion de la communauté Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796).

Suivant : **[Gérer les vues web](web-views.md)**
