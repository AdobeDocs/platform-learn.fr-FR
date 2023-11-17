---
title: Événements
description: Découvrez comment collecter des données d’événement dans une application mobile.
exl-id: 4779cf80-c143-437b-8819-1ebc11a26852
source-git-commit: 94ca4a238c241518219fb2e8d73f775836f86d86
workflow-type: tm+mt
source-wordcount: '955'
ht-degree: 1%

---

# Événements

Découvrez comment effectuer le suivi des événements dans une application mobile.

>[!INFO]
>
> Ce tutoriel sera remplacé par un nouveau tutoriel utilisant un nouvel exemple d’application mobile à la fin novembre 2023.

L’extension Edge Network fournit une API pour envoyer des événements d’expérience à Platform Edge Network. Un événement d’expérience est un objet qui contient des données conformes à la définition de schéma XDM ExperienceEvent. Plus simplement, ils capturent ce que les gens font dans votre application mobile. Une fois les données reçues par Platform Edge Network, elles peuvent être transférées vers les applications et services configurés dans votre flux de données, tels qu’Adobe Analytics et Experience Platform. En savoir plus sur les [Événements d’expérience](https://developer.adobe.com/client-sdks/documentation/getting-started/track-events/) dans la documentation du produit.

## Conditions préalables

* Mise à jour de PodFile avec les SDK requis.
* Extensions enregistrées dans AppDelegate.
* Configuré MobileCore pour utiliser votre AppId de développement.
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

Regardons quelques exemples.

### Exemple #1 - groupes de champs standard

Examinez l’exemple suivant sans essayer de le mettre en oeuvre dans l’exemple d’application :

1. Dans votre schéma, identifiez l’événement que vous tentez de collecter. Dans cet exemple, nous effectuons le suivi d’une consultation de produit.
   ![schéma de consultation de produit](assets/mobile-datacollection-prodView-schema.png)

1. Commencez à créer l’objet :

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

   * eventType : décrit l’événement qui s’est produit, utilisez une variable [valeur connue](https://github.com/adobe/xdm/blob/master/docs/reference/classes/experienceevent.schema.md#xdmeventtype-known-values) si possible.
   * commerce.productViews.value : indiquez la valeur numérique de l’événement. S’il s’agit d’une valeur booléenne (ou &quot;compteur&quot; dans Adobe Analytics), la valeur sera toujours 1. S’il s’agit d’un événement numérique ou monétaire, la valeur peut être supérieure à 1.

1. Dans votre schéma, identifiez toutes les données supplémentaires associées à l’événement. Dans cet exemple, incluez `productListItems` qui est un ensemble standard de champs utilisé avec les événements liés au commerce :
   ![schéma d’éléments de liste de produits](assets/mobile-datacollection-prodListItems-schema.png)
   * Notez que `productListItems` est un tableau qui permet de fournir plusieurs produits.

1. Développez votre objet xdmData pour inclure des données supplémentaires :

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

1. Utilisez la structure de données pour créer une `ExperienceEvent`:

   ```swift
   let productViewEvent = ExperienceEvent(xdm: xdmData)
   ```

1. Envoyez l’événement et les données à Platform Edge Network :

   ```swift
   Edge.sendEvent(experienceEvent: productViewEvent)
   ```

### Exemple #2 - groupes de champs personnalisés

Examinez l’exemple suivant sans essayer de le mettre en oeuvre dans l’exemple d’application :

1. Dans votre schéma, identifiez l’événement que vous essayez de collecter. Dans cet exemple, effectuez le suivi d’une &quot;Interaction de l’application&quot; composée d’un événement et d’un nom d’action de l’application.
   ![schéma d’interaction de l’application](assets/mobile-datacollection-appInteraction-schema.png)

1. Commencez à construire votre objet.

   >[!NOTE]
   >
   >  Les groupes de champs standard commencent toujours à la racine de l’objet.
   >
   >  Les groupes de champs personnalisés commencent toujours sous un objet unique à votre organisation Experience Cloud, &quot;_techmarketingdemos&quot; dans cet exemple.

   ```swift
   var xdmData: [String: Any] = [
   "_techmarketingdemos": [
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
   ```

   Ou bien...

   ```swift
   var xdmData: [String: Any] = [:]
   xdmData["_techmarketingdemos"] = [
       "appInformation": [
           "appInteraction": [
               "name": actionName,
               "appAction": [
                   "value": 1
               ]
           ]
       ]
   ]
   ```

1. Utilisez la structure de données pour créer une `ExperienceEvent`.

   ```swift
   let appInteractionEvent = ExperienceEvent(xdm: xdmData)
   ```

1. Envoyez l’événement et les données à Platform Edge Network.

   ```swift
   Edge.sendEvent(experienceEvent: appInteractionEvent)
   ```

### Ajout du suivi des vues d’écran à l’application Luma

Les exemples ci-dessus expliquent, je l’espère, le processus de réflexion lors de la création d’un objet de données XDM. Nous allons ensuite ajouter le suivi des vues d’écran dans l’application Luma.

1. Accédez à `Home.swift`.
1. Ajoutez le code suivant à `viewDidAppear(...)`.

   ```swift
           let stateName = "luma: content: ios: us: en: home"
           var xdmData: [String: Any] = [:]
           //Page View
           xdmData["_techmarketingdemos"] = [
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
           let experienceEvent = ExperienceEvent(xdm: xdmData)
           Edge.sendEvent(experienceEvent: experienceEvent)
   ```

1. Répétez l’opération pour chaque écran de l’application, en mettant à jour `stateName` au fur et à mesure.



### Validation

1. Consultez la section [instructions de configuration](assurance.md) et connectez votre simulateur ou votre appareil à Assurance.
1. Exécutez l’action et recherchez le `hitReceived` de l’événement `com.adobe.edge.konductor` fournisseur.
1. Sélectionnez l’événement et passez en revue les données XDM dans le `messages` .
   ![validation de la collecte de données](assets/mobile-datacollection-validation.png)

### Exemple #3 - purchase

Dans cet exemple, supposons que l’utilisateur ait effectué avec succès l’achat suivant :

* Produit #1 - Yoga Mat.
   * 49,99 $ x1
   * SKU : 5829
* Produit #2 - Bouteille d&#39;eau.
   * 10,00 $ x3
   * SKU : 9841
* Total de la commande : 79,99 $
* Identifiant de commande unique : 298234720
* Type de paiement : carte de crédit Visa
* Identifiant de transaction de paiement unique : 847361

#### Schéma

Voici les champs de schéma associés à utiliser :

* eventType : &quot;commerce.purchases&quot;
* commerce.purchases
* commerce.order
* productsListItems
* _techmarketingdemos.appStateDetails (personnalisé)

>[!TIP]
>
>Les groupes de champs personnalisés sont toujours placés sous l’identifiant de votre organisation Experience Cloud.
>
>&quot;_techmarketingdemos&quot; est remplacé par la valeur unique de votre organisation.

![schéma d&#39;achat](assets/mobile-datacollection-purchase-schema.png)


#### Code

Voici comment créer et envoyer l’objet XDM dans l’application.

```swift
let stateName = "luma: content: ios: us: en: orderconfirmation"
let currencyCode = "USD"
let orderTotal = "79.99"
let paymentType = "Visa Credit Card"
let orderId = "298234720"
let paymentTransactionId = "847361"
var xdmData: [String: Any] = [
  "eventType": "commerce.purchases",
  "commerce": [
    "purchases": [
      "value": 1
    ],
    "order": [
      "currencyCode": currencyCode,
      "priceTotal": orderTotal,
      "purchaseID": orderId,
      "purchaseOrderNumber": orderId,
      "payments": [ //Assuming only 1 payment type is used
        [
          "currencyCode": currencyCode,
          "paymentAmount": orderTotal,
          "paymentType": paymentType,
          "transactionID": paymentTransactionId
        ]
      ]
    ]
  ],
  "productListItems": [
      [
          "name":  "Yoga Mat",
          "SKU": "5829",
          "priceTotal": "49.99",
          "quantity": 1
      ],
      [
        "name":  "Water Bottle",
        "SKU": "9841",
        "priceTotal": "30.00",
        "quantity": 3
      ]
  ]
]

//Custom field group
xdmData["_techmarketingdemos"] = [
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
let experienceEvent = ExperienceEvent(xdm: xdmData)
Edge.sendEvent(experienceEvent: experienceEvent)
```

>[!NOTE]
>
>Pour plus de clarté, toutes les valeurs sont codées en dur. Dans une situation réelle, les valeurs seraient renseignées dynamiquement.


### Mise en oeuvre dans l’application Luma

Vous devez disposer de tous les outils pour commencer à ajouter la collecte de données à l’exemple d’application Luma. Vous trouverez ci-dessous une liste des exigences de suivi hypothétiques que vous pouvez suivre.

* Effectuez le suivi de chaque affichage d’écran.
   * Champs du schéma : screenType, screenName, screenView
* Suivi des actions autres que commerciales.
   * Champs de schéma : appInteraction.name, appAction
* Actions commerciales :
   * Page de produit : productViews
   * Ajouter au panier : productListAdds
   * Supprimer du panier : productListRemovals
   * Début du passage en caisse : passages en caisse
   * Afficher le panier : productListViews
   * Ajouter à la liste blanche : saveForLaters
   * Achat : achats, commande

>[!TIP]
>
>Consultez la section [application entièrement implémentée](https://github.com/Adobe-Marketing-Cloud/Luma-iOS-Mobile-App) pour plus d’exemples.

### Validation

1. Consultez la section [instructions de configuration](assurance.md) et connectez votre simulateur ou votre appareil à Assurance.

1. Exécutez l’action et recherchez le `hitReceived` de l’événement `com.adobe.edge.konductor` fournisseur.

1. Sélectionnez l’événement et passez en revue les données XDM dans le `messages` .
   ![validation de la collecte de données](assets/mobile-datacollection-validation.png)

## Envoi d’événements à Analytics et Platform

Maintenant que vous avez collecté les événements et que vous les avez envoyés à Platform Edge Network, ils seront envoyés aux applications et services configurés dans votre [datastream](create-datastream.md). Dans les leçons suivantes, vous allez mapper ces données à [Adobe Analytics](analytics.md) et [Adobe Experience Platform](platform.md).

Suivant : **[WebViews](web-views.md)**

>[!NOTE]
>
>Merci d’investir votre temps à apprendre sur le SDK Adobe Experience Platform Mobile. Si vous avez des questions, souhaitez partager des commentaires généraux ou avez des suggestions sur le contenu futur, partagez-les à ce sujet. [Article de discussion de la communauté Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796)