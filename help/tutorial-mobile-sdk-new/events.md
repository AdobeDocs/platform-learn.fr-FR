---
title: Événements
description: Découvrez comment collecter des données d’événement dans une application mobile.
hide: true
hidefromtoc: true
source-git-commit: ca83bbb571dc10804adcac446e2dba4fda5a2f1d
workflow-type: tm+mt
source-wordcount: '1121'
ht-degree: 0%

---

# Événements

Découvrez comment effectuer le suivi des événements dans une application mobile.

L’extension Edge Network fournit une API pour envoyer des événements d’expérience à Platform Edge Network. Un événement d’expérience est un objet qui contient des données conformes à la définition de schéma XDM ExperienceEvent. Plus simplement, ils capturent ce que les gens font dans votre application mobile. Une fois les données reçues par Platform Edge Network, elles peuvent être transférées vers les applications et services configurés dans votre flux de données, tels qu’Adobe Analytics et Experience Platform. En savoir plus sur les [Événements d’expérience](https://developer.adobe.com/client-sdks/documentation/getting-started/track-events/) dans la documentation du produit.

## Conditions préalables

* Toutes les dépendances de package en place dans le projet Xcode.
* Extensions enregistrées dans AppDelegate.
* Configuré MobileCore pour utiliser votre appId de développement.
* SDK importés.
* Création et exécution de l’application réussie avec les modifications ci-dessus.

## Objectifs d&#39;apprentissage

Dans cette leçon, vous allez :

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

  ```swift {highlight="2-8"}
  var xdmData: [String: Any] = [
      "eventType": "commerce.productViews",
      "commerce": [
          "productViews": [
            "id": sku,
            "value": 1
          ]
      ]
  ]
  ```

   * `eventType`: décrit l’événement qui s’est produit, utilisez une [valeur connue](https://github.com/adobe/xdm/blob/master/docs/reference/classes/experienceevent.schema.md#xdmeventtype-known-values) si possible.
   * `commerce.productViews.id`: une valeur string représentant le SKU du produit
   * `commerce.productViews.value`: indiquez la valeur numérique de l’événement. S’il s’agit d’une valeur booléenne (ou &quot;Compteur&quot; dans Adobe Analytics), la valeur est toujours définie sur 1. S’il s’agit d’un événement numérique ou monétaire, la valeur peut être supérieure à 1.

* Dans votre schéma, identifiez toutes les données supplémentaires associées à l’événement d’affichage de produit commercial. Dans cet exemple, incluez `productListItems` qui est un ensemble standard de champs utilisé avec tous les événements liés au commerce :

  ![schéma d’éléments de liste de produits](assets/datacollection-prodListItems-schema.png)
   * Notez que `productListItems` est un tableau qui permet de fournir plusieurs produits.

* Pour ajouter ces données, développez `xdmData` afin d’inclure des données supplémentaires :

```swift {highlight="9-16"}
var xdmData: [String: Any] = [
    "eventType": "commerce.productViews",
        "commerce": [
        "productViews": [
            "id": sku,
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

* Vous pouvez ensuite utiliser la structure de données pour créer une `ExperienceEvent`:

  ```swift
  let productViewEvent = ExperienceEvent(xdm: xdmData)
  ```

* Et envoyez l’événement et les données à Platform Edge Network à l’aide de l’API sendEvent :

  ```swift
  Edge.sendEvent(experienceEvent: productViewEvent)
  ```

Alors maintenant, implémentons ce code dans votre projet Xcode.
Vous avez différentes actions commerciales liées aux produits (affichage, ajout au panier, enregistrement pour plus tard, achat) dans votre application et vous souhaitez envoyer des événements en fonction de ces actions, comme l’a fait l’utilisateur.

1. Pour structurer l’envoi des événements d’expérience, accédez à `MobileSDK`, puis ajoutez le code suivant au `sendCommerceExperienceEvent` de la fonction Cette fonction utilise l’événement et le produit de l’expérience de commerce comme paramètres :

   ```swift {highlight="2-22"}
   func sendCommerceExperienceEvent(commerceEventType: String, product: Product) {
     let xdmData: [String: Any] = [
         "eventType": "commerce." + commerceEventType,
         "commerce": [
             commerceEventType: [
                 "id": product.sku,
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
   
     Logger.viewCycle.info("About to send commerce experience event of type  \(commerceEventType)..."
     let commerceExperienceEvent = ExperienceEvent(xdm: xdmData)
     Edge.sendEvent(experienceEvent: commerceExperienceEvent)
   }
   ```

1. Dans `ProductView` ajouter divers appels à la fonction `sendCommerceExperienceEvent` function:

   1. À l’emplacement `.task` dans le `ATTrackingManager.trackingAuthorizationStatus` fermeture. La variable `.task` est appelé lorsque la consultation de produit est initialisée et affichée. vous souhaitez donc envoyer un événement de consultation de produit à ce moment spécifique.

      ```swift {highlight="4-5"}
      .task {
          if ATTrackingManager.trackingAuthorizationStatus == .authorized {
               // Send commerce experience event
              MobileSDK.shared.sendCommerceExperienceEvent(commerceEventType: "productView", product: product)
          }
      }
      ```

   1. Pour chacun des boutons (Enregistré pour plus tard, Ajouter au panier et Achat) de la barre d’outils, disponible dans la vue Produit, ajoutez l’appel approprié.

      * Pour Enregistrer pour plus tard / Ajouter à la liste des souhaits :

        ```swift {highlight="5-6"}
        Button {
            Task {
                if ATTrackingManager.trackingAuthorizationStatus == .authorized {
                // Send saveForLater commerce experience event
                    MobileSDK.shared.sendCommerceExperienceEvent(commerceEventType: "saveForLaters", product: product)
                }
            }
            showSaveForLaterDialog.toggle()
        } label: {
            Label("", systemImage: "heart")
        }
        .alert(isPresented: $showSaveForLaterDialog, content: {
            Alert(title: Text( "Saved for later"), message: Text("The selected item is saved to your wishlist…"))
        })
        ```

      * Pour Ajouter au panier :

        ```swift {highlight="5-6"}
        Button {
            Task {
                if ATTrackingManager.trackingAuthorizationStatus == .authorized {
                    // Send productListAdds commerce experience event
                    MobileSDK.shared.sendCommerceExperienceEvent(commerceEventType: "productListAdds", product: product)
                }
            }
            showAddToCartDialog.toggle()
        } label: {
                Label("", systemImage: "cart.badge.plus")
        }
        alert(isPresented: $showAddToCartDialog, content: {
            Alert(title: Text( "Added to basket"), message: Text("The selected item is added to your basket…"))
        })
        ```

      * Pour l’achat :

        ```swift {highlight="5-6"}
        Button {
            Task {
                if ATTrackingManager.trackingAuthorizationStatus == .authorized {
                    // Send purchase commerce experience event
                    MobileSDK.shared.sendCommerceExperienceEvent(commerceEventType: "purchases", product: product)
                }
            }
            showPurchaseDialog.toggle()
        } label: {
            Label("", systemImage: "creditcard")
        }
        .alert(isPresented: $showPurchaseDialog, content: {
            Alert(title: Text( "Purchases"), message: Text("The selected item is purchased…"))
        })
        ```

### Groupes de champs personnalisés

Imaginez que vous souhaitiez effectuer le suivi des affichages d’écran et des interactions dans l’application elle-même. Souvenez-vous que vous avez défini un groupe de champs personnalisé pour ce type d’événements.

* Dans votre schéma, identifiez les événements que vous essayez de collecter.
  ![schéma d’interaction de l’application](assets/datacollection-appInteraction-schema.png)

* Commencez à construire votre objet.

  >[!NOTE]
  >
  >  Les groupes de champs standard commencent toujours à la racine de l’objet.
  >
  >  Les groupes de champs personnalisés commencent toujours sous un objet unique à votre organisation Experience Cloud, `_techmarketingdemos` dans cet exemple.

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


* Ensuite, la structure de données pour créer une `ExperienceEvent`.

  ```swift
  let event = ExperienceEvent(xdm: xdmData)
  ```

* Envoyez l’événement et les données à Platform Edge Network.

  ```swift
  Edge.sendEvent(experienceEvent: event)
  ```


Encore une fois, permet de mettre en oeuvre ce code dans votre projet Xcode.

1. Pour des raisons pratiques, vous définissez deux fonctions dans `MobileSDK`.

   Une pour les interactions avec l’application. Ajoutez le code mis en surbrillance au `sendAppInteractionEvent(actionName)` fonction dans **[!UICONTROL MobileSDK]**:

   ```swift {highlight="2-16"}
   func sendAppInteractionEvent(actionName: String) {
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
   }
   ```

   Et un pour le suivi d&#39;écran. Ajoutez le code mis en surbrillance à la fonction `sendTrackScreenEvent(stateName)` fonction dans **[!UICONTROL MobileSDK]**:

   ```swift {highlight="2-17"}
   func sendTrackScreenEvent(stateName: String) {
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
   }
   ```

1. Accédez à **[!UICONTROL LoginSheet]**.

   * Ajoutez le code en surbrillance suivant à la fermeture du bouton Connexion :

     ```swift {highlight="3"}
     Button("Login") {                               
        // Send app interaction event
        MobileSDK.shared.sendAppInteractionEvent(actionName: "login")
        dismiss()
     }
     .disabled(currentEmailId.isValidEmail == false)
     .buttonStyle(.bordered)
     ```

   * Ajoutez le code mis en surbrillance suivant à `onAppear` modifier :

     ```swift {highlight="13"}
     .onAppear {
        Task {
            if currentEmailId == "testUser@gmail.com" || currentEmailId.isValidEmail == false {
                // still allow to log in
                disableLogin = false
            }
            else {
                disableLogin = true
            }
        }
        // Send track screen event
        MobileSDK.shared.sendTrackScreenEvent(stateName: "luma: content: ios: us: en: login")
     }
     ```

### Validation

1. Consultez la section [instructions de configuration](assurance.md) et connectez votre simulateur ou votre appareil à Assurance.
1. Exécutez l’application pour vous connecter et interagir avec un produit.

   1. Déplacez l’icône Assurance vers la gauche.
   1. Sélectionner **[!UICONTROL Accueil]** dans la barre d’onglets.
   1. Sélectionnez la variable **[!UICONTROL Connexion]** pour ouvrir la feuille de connexion.
   1. Sélectionnez la variable **[!UICONTROL A|]** pour insérer un email aléatoire et un ID de client.
   1. Sélectionner **[!UICONTROL Connexion]**.
   1. Sélectionner **[!UICONTROL Produits]** dans la barre d’onglets.
   1. Sélectionnez un produit.
   1. Sélectionner **[!UICONTROL Enregistrer ultérieurement]**.
   1. Sélectionner **[!UICONTROL Ajouter au panier]**.
   1. Sélectionner **[!UICONTROL Achat]**.

      <img src="./assets/mobile-app-events-1.png" width="200"> <img src="./assets/mobile-app-events-2.png" width="200"> <img src="./assets/mobile-app-events-3.png" width="200">


1. Recherchez le **[!UICONTROL hitReceived]** des événements **[!UICONTROL com.adobe.edge.konductor]** fournisseur.
1. Sélectionnez l’événement et passez en revue les données XDM dans le **[!UICONTROL messages]** .
   ![validation de la collecte de données](assets/datacollection-validation.png)


### Mise en oeuvre dans l’application Luma

Vous devriez maintenant disposer de tous les outils pour commencer à ajouter la collecte de données à l’application Luma. Vous pouvez ajouter plus d’informations sur la manière dont votre utilisateur interagit avec vos produits et vous pouvez ajouter plus d’appels d’interaction d’application et de suivi d’écran à votre application :

* Mettez en oeuvre la commande, le passage en caisse, le panier vide et d’autres fonctionnalités dans l’application et ajoutez un événement d’expérience commerciale approprié à cette fonctionnalité.
* Répétez l’appel à `sendAppInteractionEvent` avec le paramètre approprié pour effectuer le suivi des autres interactions de l’application dans l’application par l’utilisateur.
* Répétez l’appel à `sendTrackScreenEvent` avec le paramètre approprié pour suivre chaque écran affiché par l’utilisateur dans l’application.

>[!TIP]
>
>Consultez la section [application entièrement implémentée](https://github.com/Adobe-Marketing-Cloud/Luma-iOS-Mobile-App) pour plus d’exemples.


## Envoi d’événements à Analytics et Platform

Maintenant que vous avez collecté les événements et que vous les avez envoyés à Platform Edge Network, ils sont envoyés aux applications et services configurés dans votre [datastream](create-datastream.md). Dans les leçons ultérieures, vous mappez ces données avec [Adobe Analytics](analytics.md) et [Adobe Experience Platform](platform.md).

>[!SUCCESS]
>
>Vous avez maintenant configuré votre application pour effectuer le suivi des événements de commerce, d’interaction d’application et de suivi d’écran sur le réseau Adobe Experience Platform Edge et tous les services que vous avez définis dans votre flux de données.<br/>Merci d’investir votre temps à apprendre sur le SDK Adobe Experience Platform Mobile. Si vous avez des questions, souhaitez partager des commentaires généraux ou avez des suggestions sur le contenu futur, partagez-les à ce sujet. [Article de discussion de la communauté Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796).

Suivant : **[WebViews](web-views.md)**
