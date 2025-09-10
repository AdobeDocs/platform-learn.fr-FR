---
title: Mapper les données collectées avec Platform Mobile SDK vers Adobe Analytics
description: Découvrez comment collecter et mapper des données pour Adobe Analytics dans une application mobile.
solution: Data Collection,Experience Platform,Analytics
jira: KT-14636
exl-id: 406dc687-643f-4f7b-a8e7-9aad1d0d481d
source-git-commit: 008d3ee066861ea9101fe9fe99ccd0a088b63f23
workflow-type: tm+mt
source-wordcount: '1033'
ht-degree: 0%

---

# Collecter et mapper des données Analytics

Découvrez comment mapper les données mobiles à Adobe Analytics.

Les données [événement](events.md) que vous avez collectées et envoyées à Platform Edge Network dans des leçons précédentes sont transférées aux services configurés dans votre flux de données, y compris Adobe Analytics. Vous mappez les données aux variables correctes dans votre suite de rapports.

![Architecture](assets/architecture-aa.png){zoomable="yes"}

## Conditions préalables

* Compréhension du suivi des événements d’expérience.
* Envoi réussi de données XDM dans votre exemple d’application.
* Une suite de rapports Adobe Analytics que vous pouvez utiliser pour cette leçon.

## Objectifs d’apprentissage

Dans cette leçon, vous allez :

* Configurez votre flux de données avec le service Adobe Analytics.
* comprendre le mappage automatique des variables Analytics ;
* Configurez les règles de traitement pour mapper les données XDM aux variables Analytics.

## Ajouter un service de flux de données Adobe Analytics

Pour envoyer vos données XDM d’Edge Network vers Adobe Analytics, vous devez configurer le service Adobe Analytics sur le flux de données que vous avez configuré dans le cadre de l’[Création d’un flux de données](create-datastream.md).

1. Dans l’interface utilisateur de collecte de données, sélectionnez **[!UICONTROL Flux de données]** et votre flux de données.

1. Sélectionnez ensuite ![ Ajouter ](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) **[!UICONTROL Ajouter un service]**.

1. Ajouter **[!UICONTROL Adobe Analytics]** à partir de la liste [!UICONTROL Service],

1. Saisissez le nom de la suite de rapports d’Adobe Analytics à utiliser dans **[!UICONTROL Identifiant de suite de rapports]**.

1. Activez le service en activant **[!UICONTROL Activé]**.

1. Sélectionnez **[!UICONTROL Enregistrer]**.

   ![Ajouter Adobe Analytics en tant que service de flux de données](assets/datastream-service-aa.png){zoomable="yes"}


## Mappage automatique

La plupart des champs XDM standard sont automatiquement mappés à des variables Analytics. Voir la [liste complète](https://experienceleague.adobe.com/en/docs/analytics/implementation/aep-edge/xdm-var-mapping).

### Exemple #1 - s.products

Un bon exemple est la variable [products](https://experienceleague.adobe.com/en/docs/analytics/implementation/vars/page-vars/products) qui ne peut pas être renseignée à l’aide de règles de traitement. Avec une implémentation XDM, vous transmettez toutes les données nécessaires dans `productListItems` et `s.products` sont automatiquement renseignées via le mappage Analytics.

Cet objet :

```swift
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
```

permet d’obtenir :

```
s.products = ";5829;1;49.99,9841;3;30.00"
```

>[!NOTE]
>
>Si `productListItems[].SKU` et `productListItems[].name` contiennent tous deux des données, la valeur de `productListItems[].SKU` est utilisée. Pour plus d’informations, voir [Mappage des variables Analytics dans Adobe Experience Edge](https://experienceleague.adobe.com/en/docs/analytics/implementation/aep-edge/xdm-var-mapping).


### Exemple de #2 - scAdd

Si vous y regardez de plus près, tous les événements comportent deux champs : `value` (obligatoire) et `id` (facultatif). Le champ `value` est utilisé pour incrémenter le nombre d’événements. Le champ `id` est utilisé pour la sérialisation.

Cet objet :

```swift
"commerce" : {
  "productListAdds" : {
    "value" : 1
  }
}
```

permet d’obtenir :

```
s.events = "scAdd"
```

Cet objet :

```swift
"commerce" : {
  "productListAdds" : {
    "value" : 1,
    "id": "321435"
  }
}
```

permet d’obtenir :

```
s.events = "scAdd:321435"
```

## Valider avec Assurance

À l’aide de l’[Assurance](assurance.md) vous pouvez confirmer que vous envoyez un événement d’expérience, que les données XDM sont correctes et que le mappage Analytics se produit comme prévu.

1. Consultez la section [instructions de configuration](assurance.md#connecting-to-a-session) pour connecter votre simulateur ou votre appareil à Assurance.

1. Envoyer un événement **[!UICONTROL productListAdds]** (ajouter un produit à votre panier)

1. Affichez l’accès ExperienceEvent.

   ![accès à analytics xdm](assets/analytics-assurance-experiencevent.png){zoomable="yes"}

1. Examinez la partie XDM du fichier JSON.

   ```json
   "xdm" : {
     "productListItems" : [ {
       "SKU" : "LLWS05.1-XS",
       "name" : "Desiree Fitness Tee",
       "priceTotal" : 24
     } ],
   "timestamp" : "2023-08-04T12:53:37.662Z",
   "eventType" : "commerce.productListAdds",
   "commerce" : {
     "productListAdds" : {
       "value" : 1
     }
   }
   // ...
   ```

1. Examinez l’événement **[!UICONTROL analytics.mapping]**.

   ![accès à analytics xdm](assets/analytics-assurance-mapping.png){zoomable="yes"}

Notez ce qui suit dans le mappage Analytics :

* Les **[!UICONTROL événements]** sont renseignés avec des `scAdd` basées sur `commerce.productListAdds`.
* **[!UICONTROL pl]** (variable products) est renseignée avec une valeur concaténée basée sur `productListItems`.
* Il y a d’autres informations intéressantes dans cet événement, y compris toutes les données contextuelles.


## Mappage avec des données contextuelles

Les données XDM transférées vers Analytics sont converties en [données contextuelles](https://github.com/Adobe-Marketing-Cloud/mobile-services/blob/master/docs/ios/getting-started/proc-rules.md?lang=en) y compris les champs standard et personnalisés.

La clé des données contextuelles est construite selon cette syntaxe :

```
a.x.[xdm path]
```

Par exemple :

```
// Standard Field
a.x.commerce.saveforlaters.value

// Custom Field
a.x._techmarketingdemos.appinformation.appstatedetails.screenname
```

>[!NOTE]
>
>Les champs personnalisés sont placés sous votre identifiant d’organisation Experience Cloud.
>
Le nom du client `_techmarketingdemos` est remplacé par la valeur unique de votre organisation.



Pour mapper ces données contextuelles XDM à vos données Analytics dans votre suite de rapports, vous pouvez :

### Utiliser un groupe de champs

* Ajoutez le groupe de champs Extension complète **[!UICONTROL Adobe Analytics ExperienceEvent]** à votre schéma.

  ![Groupe de champs FullExtension Analytics ExperienceEvent](assets/schema-analytics-extension.png){zoomable="yes"}

* Créez des payloads XDM dans votre application, en respectant le groupe de champs Extension complète Adobe Analytics ExperienceEvent, comme vous l’avez fait dans la leçon [Suivi des données d’événement](events.md) ou
* Créez dans votre propriété Balises des règles qui utilisent des actions de règle pour joindre ou modifier des données au groupe de champs de l’extension complète Adobe Analytics ExperienceEvent . Voir pour plus d’informations [Joindre des données aux événements SDK](https://developer.adobe.com/client-sdks/documentation/user-guides/attach-data/) ou [Modifier des données dans les événements SDK](https://developer.adobe.com/client-sdks/documentation/user-guides/attach-data/).


### eVars de marchandisage

Si vous utilisez des [eVars de marchandisage](https://experienceleague.adobe.com/en/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/conversion-variables/merchandising-evars) dans votre configuration Analytics, vous devez étendre la payload XDM que vous avez définie dans [Suivi des données d’événement](events.md) pour capturer ces informations de marchandisage. Un exemple de var de marchandisage est `evar1` lorsque vous souhaitez capturer la couleur de produits, comme `&&products = ...;evar1=red;event10=50,...;evar1=blue;event10=60`

* Dans JSON :

  ```json
  {
    "productListItems": [
        {
            "SKU": "LLWS05.1-XS",
            "name": "Desiree Fitness Tee",
            "priceTotal": 24,
            "_experience": {
                "analytics": {
                    "events1to100": {
                        "event10": {
                            "value": 50
                        }
                    },
                    "customDimensions": {
                        "eVars": {
                            "eVar1": "red",
                        }
                    }
                }
            }
        }
    ],
    "eventType": "commerce.productListAdds",
    "commerce": {
        "productListAdds": {
            "value": 1
        }
    }
  }
  ```

* Dans le code :

  ```swift
  var xdmData: [String: Any] = [
    "productListItems": [
      [
        "name":  productName,
        "SKU": sku,
        "priceTotal": priceString,
        "_experience" : [
          "analytics": [
            "events1to100": [
              "event10": [
                "value:": value
              ]
            ],
            "customDimensions": [
              "eVars": [
                "eVar1": color
              ]
            ]
          ]
        ]
      ]
    ],
    "eventType": "commerce.productViews",
    "commerce": [
      "productViews": [
        "value": 1
      ]
    ]
  ]
  ```


### Utilisation des règles de traitement

Voici à quoi pourrait ressembler une règle de traitement utilisant ces données :

* Vous **[!UICONTROL Remplacez la valeur de]** (1) **[!UICONTROL Nom d’écran de l’application (eVar2)]** (2) par la valeur de **[!UICONTROL a.x._techmarketingdemo.appinformation.appstatedetails.screenname]** (3) si **[!UICONTROL a.x._techmarketingdemo.appinformation.appstatedetails]** (4) **[!UICONTROL est défini]** (5).

* Vous **[!UICONTROL Définir l’événement]** (6) **[!UICONTROL Ajouter à la liste de souhaits (Événement 3)]** (7) à **[!UICONTROL a.x.commerce.saveForLaters.value(Context)]** (8) si **[!UICONTROL a.x.commerce.saveForLaters.value(Context)]** (9) **[!UICONTROL est défini]** (10).

![règles de traitement analytics](assets/analytics-processing-rules.png){zoomable="yes"}

>[!IMPORTANT]
>
>
>Certaines des variables mappées automatiquement peuvent ne pas être disponibles pour une utilisation dans les règles de traitement.
>
>
>La première fois que vous mappez à une règle de traitement, l’interface ne vous affiche pas les variables de données contextuelles de l’objet XDM. Pour corriger ce problème, sélectionnez n’importe quelle valeur, enregistrez, puis revenez pour modifier. Toutes les variables XDM doivent maintenant apparaître.


Voir [Mappage des variables contextData en props et eVars avec des règles de traitement](https://experienceleague.adobe.com/en/docs/analytics-learn/tutorials/implementation/implementation-basics/map-contextdata-variables-into-props-and-evars-with-processing-rules).

>[!TIP]
>
>Contrairement aux implémentations d’applications mobiles précédentes, il n’existe aucune distinction entre une page ou un affichage d’écran et d’autres événements. Au lieu de cela, vous pouvez incrémenter la mesure **[!UICONTROL Page vue]** en définissant la dimension **[!UICONTROL Nom de page]** dans une règle de traitement. Puisque vous collectez le champ de `screenName` personnalisé dans le tutoriel, il est vivement recommandé de mapper le nom d’écran au **[!UICONTROL nom de page]** dans une règle de traitement.

## Migration depuis l’extension mobile Analytics

Si vous avez développé votre application mobile à l’aide de l’extension mobile [Adobe Analytics](https://developer.adobe.com/client-sdks/solution/adobe-analytics/#add-analytics-to-your-application), vous avez probablement utilisé des appels d’API [`MobileCore.trackAction`](https://developer.adobe.com/client-sdks/home/base/mobile-core/api-reference/#trackaction) et [`MobileCore.trackState`](https://developer.adobe.com/client-sdks/home/base/mobile-core/api-reference/#trackstate).

Si vous décidez de migrer pour utiliser Edge Network recommandé, vous disposez des options suivantes :

* Mettez en œuvre l’extension [Edge Network et utilisez ](configure-tags.md#extension-configuration) API [`Edge.sendEvent`](https://developer.adobe.com/client-sdks/edge/edge-network/api-reference/#sendevent), comme illustré dans la leçon sur la façon de [suivre les données d’événement](events.md). Ce tutoriel se concentre sur cette implémentation.
* Mettez en œuvre l’extension Edge Bridge [](https://developer.adobe.com/client-sdks/solution/adobe-analytics/migrate-to-edge-network/#implement-the-edge-bridge-extension) et continuez à utiliser vos appels d’API [`MobileCore.trackAction`](https://developer.adobe.com/client-sdks/home/base/mobile-core/api-reference/#trackaction) et [`MobileCore.trackState`](https://developer.adobe.com/client-sdks/home/base/mobile-core/api-reference/#trackstate). Voir [Implémentation de l’extension Edge Bridge](https://developer.adobe.com/client-sdks/solution/adobe-analytics/migrate-to-edge-network/#implement-the-edge-bridge-extension) pour plus d’informations et pour un tutoriel séparé.




>[!SUCCESS]
>
>Vous avez configuré votre application pour mapper vos objets XDM Experience Edge aux variables Adobe Analytics en activant le service Adobe Analytics dans votre flux de données. Et en utilisant les règles de traitement le cas échéant.<br/> Merci d’avoir investi votre temps pour en savoir plus sur Adobe Experience Platform Mobile SDK. Si vous avez des questions, souhaitez partager des commentaires généraux ou des suggestions sur le contenu futur, partagez-les dans ce [article de discussion de la communauté Experience League](https://experienceleaguecommunities.adobe.com:443/t5/adobe-experience-platform-data/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796).

Suivant : **[Envoi de données à Experience Platform](platform.md)**
