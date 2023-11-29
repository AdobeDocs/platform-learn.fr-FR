---
title: Suivi des données d’événement dans les applications mobiles avec le SDK Mobile Platform
description: Découvrez comment effectuer le suivi des données d’événement dans une application mobile.
exl-id: 4779cf80-c143-437b-8819-1ebc11a26852
source-git-commit: d353de71d8ad26d2f4d9bdb4582a62d0047fd6b1
workflow-type: tm+mt
source-wordcount: '1397'
ht-degree: 3%

---

# Suivi des données d’événement

Découvrez comment effectuer le suivi des événements dans une application mobile.

L’extension Edge Network fournit une API pour envoyer des événements d’expérience à Platform Edge Network. Un événement d’expérience est un objet qui contient des données conformes à la définition de schéma XDM ExperienceEvent. Plus simplement, ils capturent ce que les gens font dans votre application mobile. Une fois les données reçues par Platform Edge Network, elles peuvent être transférées vers les applications et services configurés dans votre flux de données, tels qu’Adobe Analytics et Experience Platform. En savoir plus sur les [Événements d’expérience](https://developer.adobe.com/client-sdks/documentation/getting-started/track-events/) dans la documentation du produit.

## Conditions préalables

* Toutes les dépendances de package sont en place dans votre projet Xcode.
* Extensions enregistrées dans **[!UICONTROL AppDelegate]**.
* Extension MobileCore configurée pour utiliser votre développement `appId`.
* SDK importés.
* Création et exécution de l’application réussie avec les modifications ci-dessus.

## Objectifs d&#39;apprentissage

Dans cette leçon, vous allez

* Découvrez comment structurer les données XDM en fonction d’un schéma.
* Envoyez un événement XDM en fonction d’un groupe de champs standard.
* Envoyez un événement XDM en fonction d’un groupe de champs personnalisé.
* Envoyez un événement d’achat XDM.
* Validez avec assurance.

## Création d’un événement d’expérience

L’extension Adobe Experience Platform Edge peut envoyer à Adobe Experience Platform Edge Network des événements qui suivent un schéma XDM défini précédemment.

Le processus est le suivant...

1. Identifiez l’interaction de l’application mobile dont vous essayez d’effectuer le suivi.

1. Vérifiez votre schéma et identifiez l’événement approprié.

1. Vérifiez votre schéma et identifiez tous les champs supplémentaires qui doivent être utilisés pour décrire l’événement.

1. Créez et remplissez l’objet de données.

1. Créer et envoyer un événement.

1. Valider.


### Groupes de champs standard

Pour les groupes de champs standard, le processus ressemble à :

* Dans votre schéma, identifiez les événements que vous essayez de collecter. Dans cet exemple, vous effectuez le suivi des événements d’expérience commerciale, par exemple une consultation de produit (**[!UICONTROL productViews]**).

  ![schéma de consultation de produit](assets/datacollection-prodView-schema.png)

* Pour créer un objet contenant les données d’événement d’expérience dans votre application, vous devez utiliser le code suivant :

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

   * `eventType`: décrit l’événement qui s’est produit, utilisez une [valeur connue](https://github.com/adobe/xdm/blob/master/docs/reference/classes/experienceevent.schema.md#xdmeventtype-known-values) si possible.
   * `commerce.productViews.value`: valeur numérique ou booléenne de l’événement. S’il s’agit d’une valeur booléenne (ou &quot;Compteur&quot; dans Adobe Analytics), la valeur est toujours définie sur 1. S’il s’agit d’un événement numérique ou monétaire, la valeur peut être supérieure à 1.

* Dans votre schéma, identifiez toutes les données supplémentaires associées à l’événement d’affichage de produit commercial. Dans cet exemple, incluez **[!UICONTROL productListItems]** qui est un ensemble standard de champs utilisé avec tout événement commercial :

  ![schéma d’éléments de liste de produits](assets/datacollection-prodListItems-schema.png)
   * Notez que **[!UICONTROL productListItems]** est un tableau qui permet de fournir plusieurs produits.

* Pour ajouter ces données, développez `xdmData` afin d’inclure des données supplémentaires :

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

* Vous pouvez désormais utiliser cette structure de données pour créer une `ExperienceEvent`:

  ```swift
  let productViewEvent = ExperienceEvent(xdm: xdmData)
  ```

* Et envoyez l’événement et les données à Platform Edge Network à l’aide du `sendEvent` API :

  ```swift
  Edge.sendEvent(experienceEvent: productViewEvent)
  ```

La variable [`Edge.sendEvent`](https://developer.adobe.com/client-sdks/documentation/edge-network/api-reference/#sendevent) L’API est le SDK AEP Mobile équivalent à [`MobileCore.trackAction`](https://developer.adobe.com/client-sdks/documentation/mobile-core/api-reference/#trackaction) et [`MobileCore.trackState`](https://developer.adobe.com/client-sdks/documentation/mobile-core/api-reference/#trackstate) Appels API. Voir [Migration de l’extension mobile Analytics vers Adobe Experience Platform Edge Network](https://developer.adobe.com/client-sdks/documentation/adobe-analytics/migrate-to-edge-network/) pour plus d’informations.

Vous allez maintenant mettre en oeuvre ce code dans votre projet Xcode.
Vous avez différentes actions commerciales liées aux produits dans votre application et vous souhaitez envoyer des événements, en fonction des actions suivantes, telles qu’elles sont exécutées par l’utilisateur :

* view : survient lorsqu’un utilisateur consulte un produit spécifique,
* ajouter au panier : lorsqu’un utilisateur appuie sur <img src="assets/addtocart.png" width="20" /> dans un écran de détail de produit,
* Enregistrer pour plus tard : lorsqu’un utilisateur appuie sur <img src="assets/saveforlater.png" width="15" /> dans un écran de détail de produit,
* achat : lorsqu’un utilisateur appuie sur <img src="assets/purchase.png" width="20" /> dans un écran de détails de produit.

Pour mettre en oeuvre l’envoi d’événements d’expérience liés au commerce de manière réutilisable, vous utilisez une fonction dédiée :

1. Accédez à **[!DNL Luma]** > **[!DNL Luma]** > **[!DNL Utils]** > **[!UICONTROL MobileSDK]** dans le navigateur de projet Xcode, puis ajoutez ce qui suit au `func sendCommerceExperienceEvent(commerceEventType: String, product: Product)` de la fonction

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

   Cette fonction utilise le type d’événement et le produit de l’expérience de commerce comme paramètres et

   * configure la charge utile XDM en tant que dictionnaire à l’aide des paramètres de la fonction ,
   * configure un événement d’expérience à l’aide du dictionnaire,
   * envoie l’événement d’expérience à l’aide de la fonction [`Edge.sendEvent`](https://developer.adobe.com/client-sdks/documentation/edge-network/api-reference/#sendevent) API.

1. Accédez à **[!DNL Luma]** > **[!DNL Luma]** > **[!DNL Views]** > **[!DNL Products]** > **[!UICONTROL ProductView]** dans le navigateur de projet Xcode et ajoutez divers appels à la fonction `sendCommerceExperienceEvent` function:

   1. À l’emplacement `.task` , dans la propriété `ATTrackingManager.trackingAuthorizationStatus` fermeture. Ceci `.task` est appelé lorsque la consultation de produit est initialisée et affichée. vous souhaitez donc envoyer un événement de consultation de produit à ce moment spécifique.

      ```swift
      // Send productViews commerce experience event
      MobileSDK.shared.sendCommerceExperienceEvent(commerceEventType: "productViews", product: product)
      ```

   1. Pour chacun des boutons (<img src="assets/saveforlater.png" width="15" />, <img src="assets/addtocart.png" width="20" /> et <img src="assets/purchase.png" width="20" />) dans la barre d’outils, ajoutez l’appel correspondant dans la fonction `ATTrackingManager.trackingAuthorizationStatus == .authorized` fermeture :

      1. Pour <img src="assets/saveforlater.png" width="15" /> :

         ```swift
         // Send saveForLater commerce experience event
         MobileSDK.shared.sendCommerceExperienceEvent(commerceEventType: "saveForLaters", product: product)
         ```

      1. Pour <img src="assets/addtocart.png" width="20" /> :

         ```swift
         // Send productListAdds commerce experience event
         MobileSDK.shared.sendCommerceExperienceEvent(commerceEventType: "productListAdds", product: product)
         ```

      1. Pour <img src="assets/purchase.png" width="20" /> :

         ```swift
         // Send purchase commerce experience event
         MobileSDK.shared.sendCommerceExperienceEvent(commerceEventType: "purchases", product: product)
         ```

>[!TIP]
>
>Si vous développez pour Android™, utilisez Map (`java.util.Map`) comme interface de base pour construire votre charge utile XDM.


### Groupes de champs personnalisés

Imaginez que vous souhaitiez effectuer le suivi des affichages d’écran et des interactions dans l’application elle-même. Souvenez-vous que vous avez défini un groupe de champs personnalisé pour ce type d’événements.

* Dans votre schéma, identifiez les événements que vous essayez de collecter.
  ![schéma d’interaction de l’application](assets/datacollection-appInteraction-schema.png)

* Commencez à construire votre objet.

  >[!NOTE]
  >
  * Les groupes de champs standard commencent toujours à la racine de l’objet.
  >
  * Les groupes de champs personnalisés commencent toujours sous un objet unique à votre organisation Experience Cloud, `_techmarketingdemos` dans cet exemple.

  Pour l’événement d’interaction de l’application, vous devez créer un objet du type :

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

  Pour l’événement de suivi d’écran, vous créez un objet du type :

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


* Vous pouvez désormais utiliser cette structure de données pour créer une `ExperienceEvent`.

  ```swift
  let event = ExperienceEvent(xdm: xdmData)
  ```

* Envoyez l’événement et les données à Platform Edge Network.

  ```swift
  Edge.sendEvent(experienceEvent: event)
  ```


Encore une fois, permet de mettre en oeuvre ce code dans votre projet Xcode.

1. Pour des raisons pratiques, vous définissez deux fonctions dans **[!UICONTROL MobileSDK]**. Accédez à **[!DNL Luma]** > **[!DNL Luma]** > **[!DNL Utils]** > **[!UICONTROL MobileSDK]** dans votre navigateur de projet Xcode.

   1. Une pour les interactions avec l’application. Ajoutez ce code à la variable `func sendAppInteractionEvent(actionName: String)` function:

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

      * configure la charge utile XDM en tant que dictionnaire à l’aide du paramètre de la fonction ,
      * configure un événement d’expérience à l’aide du dictionnaire,
      * envoie l’événement d’expérience à l’aide de la fonction [`Edge.sendEvent`](https://developer.adobe.com/client-sdks/documentation/edge-network/api-reference/#sendevent) API.


   1. Et un pour le suivi d&#39;écran. Ajoutez ce code à la variable `func sendTrackScreenEvent(stateName: String) ` function:

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

      * configure la charge utile XDM en tant que dictionnaire à l’aide du paramètre de la fonction ,
      * configure un événement d’expérience à l’aide du dictionnaire,
      * envoie l’événement d’expérience à l’aide de la fonction [`Edge.sendEvent`](https://developer.adobe.com/client-sdks/documentation/edge-network/api-reference/#sendevent) API.

1. Accédez à **[!DNL Luma]** > **[!DNL Luma]** > **[!DNL Views]** > **[!DNL General]** > **[!UICONTROL LoginSheet]**.

   1. Ajoutez le code en surbrillance suivant à la fermeture du bouton Connexion :

      ```swift
      // Send app interaction event
      MobileSDK.shared.sendAppInteractionEvent(actionName: "login")
      ```

   1. Ajoutez le code mis en surbrillance suivant à `onAppear` modifier :

      ```swift
      // Send track screen event
      MobileSDK.shared.sendTrackScreenEvent(stateName: "luma: content: ios: us: en: login")
      ```

## Validation

1. Consultez la section [instructions de configuration](assurance.md#connecting-to-a-session) pour connecter votre simulateur ou votre périphérique à l’aide d’Assurance.

   1. Déplacez l’icône Assurance vers la gauche.
   1. Sélectionner **[!UICONTROL Accueil]** dans la barre d’onglets et vérifiez que vous voyez une **[!UICONTROL ECID]**, **[!UICONTROL Email]**, et **[!UICONTROL Identifiant CRM]** dans l’écran Accueil .
   1. Sélectionner **[!DNL Products]** dans la barre d’onglets.
   1. Sélectionnez un produit.
   1. Sélectionner <img src="assets/saveforlater.png" width="15" />.
   1. Sélectionner <img src="assets/addtocart.png" width="20" />.
   1. Sélectionner <img src="assets/purchase.png" width="15" />.

      <img src="./assets/mobile-app-events-3.png" width="300">


1. Dans l’interface utilisateur d’Assurance, recherchez le **[!UICONTROL hitReceived]** des événements **[!UICONTROL com.adobe.edge.konductor]** fournisseur.
1. Sélectionnez l’événement et passez en revue les données XDM dans le **[!UICONTROL messages]** . Vous pouvez également utiliser ![Copier](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Copy_18_N.svg) **[!UICONTROL Copier l’événement brut]** et utilisez un éditeur de texte ou de code de votre préférence pour coller et inspecter l’événement.

   ![validation de la collecte de données](assets/datacollection-validation.png)


## Étapes suivantes

Vous devez maintenant disposer de tous les outils pour commencer à ajouter la collecte de données à votre application. Vous pouvez ajouter plus d’informations sur la manière dont l’utilisateur interagit avec vos produits dans l’application et ajouter d’autres appels d’interaction et de suivi d’écran à l’application :

* Mettez en oeuvre la commande, le passage en caisse, le panier vide et d’autres fonctionnalités dans l’application et ajoutez des événements d’expérience commerciale pertinents à cette fonctionnalité.
* Répétez l’appel à `sendAppInteractionEvent` avec le paramètre approprié pour suivre les autres interactions de l’application par l’utilisateur.
* Répétez l’appel à `sendTrackScreenEvent` avec le paramètre approprié pour effectuer le suivi des écrans consultés par l’utilisateur dans l’application.

>[!TIP]
>
Consultez la section [application terminée](https://github.com/Adobe-Marketing-Cloud/Luma-iOS-Mobile-App) pour plus d’exemples.


## Envoi d’événements à Analytics et Platform

Maintenant que vous avez collecté les événements et que vous les avez envoyés à Platform Edge Network, ils sont envoyés aux applications et services configurés dans votre [datastream](create-datastream.md). Dans les leçons ultérieures, vous mappez ces données avec [Adobe Analytics](analytics.md), [Adobe Experience Platform](platform.md)et d’autres solutions Adobe Experience Cloud telles que [Adobe Target](target.md) et Adobe Journey Optimizer.

>[!SUCCESS]
>
Vous avez maintenant configuré votre application pour effectuer le suivi des événements de commerce, d’interaction d’application et de suivi d’écran sur le réseau Adobe Experience Platform Edge et tous les services que vous avez définis dans votre flux de données.
>
Merci d’investir votre temps à apprendre sur le SDK Adobe Experience Platform Mobile. Si vous avez des questions, souhaitez partager des commentaires généraux ou avez des suggestions sur le contenu futur, partagez-les à ce sujet. [Article de discussion de la communauté Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796).

Suivant : **[Gestion des WebViews](web-views.md)**
