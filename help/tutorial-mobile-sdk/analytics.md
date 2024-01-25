---
title: Mappage des données collectées avec le SDK Mobile Platform à Adobe Analytics
description: Découvrez comment collecter et mapper des données pour Adobe Analytics dans une application mobile.
solution: Data Collection,Experience Platform,Analytics
jira: KT-14636
exl-id: 406dc687-643f-4f7b-a8e7-9aad1d0d481d
source-git-commit: 30dd0142f1f5220f30c45d58665b710a06c827a8
workflow-type: tm+mt
source-wordcount: '923'
ht-degree: 1%

---

# Collecte et mappage des données Analytics

Découvrez comment mapper des données mobiles à Adobe Analytics.

La variable [event](events.md) les données que vous avez collectées et envoyées à Platform Edge Network dans les leçons précédentes sont transférées aux services configurés dans votre flux de données, y compris Adobe Analytics. Vous mappez les données aux variables correctes de votre suite de rapports.

![Architecture](assets/architecture-aa.png)

## Conditions préalables

* Présentation du suivi ExperienceEvent.
* Envoi réussi des données XDM dans votre exemple d’application.
* Suite de rapports Adobe Analytics que vous pouvez utiliser pour cette leçon.

## Objectifs d&#39;apprentissage

Dans cette leçon, vous allez :

* Configurez votre flux de données avec le service Adobe Analytics.
* Comprendre le mappage automatique des variables Analytics.
* Configurez les règles de traitement pour mapper les données XDM aux variables Analytics.

## Ajout du service Adobe Analytics datastream

Pour envoyer vos données XDM du réseau Edge à Adobe Analytics, vous configurez le service Adobe Analytics vers la banque de données que vous configurez dans le cadre de la [Création d’un flux de données](create-datastream.md).

1. Dans l’interface utilisateur de la collecte de données, sélectionnez **[!UICONTROL Datastreams]** et votre flux de données.

1. Sélectionnez ![Ajouter](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) **[!UICONTROL Ajouter un service]**.

1. Ajouter **[!UICONTROL Adobe Analytics]** de la [!UICONTROL Service] list,

1. Entrez le nom de la suite de rapports d’Adobe Analytics que vous souhaitez utiliser dans **[!UICONTROL Identifiant de suite de rapports]**.

1. Activez le service en basculant **[!UICONTROL Activé]** sur .

1. Sélectionnez **[!UICONTROL Enregistrer]**.

   ![Ajout d’Adobe Analytics en tant que service de flux de données](assets/datastream-service-aa.png)


## Mise en correspondance automatique

La plupart des champs XDM standard sont automatiquement mappés aux variables Analytics. Voir la liste complète [ici](https://experienceleague.adobe.com/docs/analytics/implementation/aep-edge/variable-mapping.html?lang=en).

### Exemple #1 - s.products

Un bon exemple est le suivant : [variable products](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/products.html?lang=en) qui ne peuvent pas être renseignées à l’aide de règles de traitement. Avec une implémentation XDM, vous transmettez toutes les données nécessaires dans `productListItems` et `s.products` sont automatiquement renseignées via le mappage Analytics.

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

a pour résultat :

```
s.products = ";5829;1;49.99,9841;3;30.00"
```

>[!NOTE]
>
>If `productListItems[].SKU` et `productListItems[].name` contiennent tous deux des données, la valeur de `productListItems[].SKU` est utilisée. Voir [Mappage des variables Analytics dans Adobe Experience Edge](https://experienceleague.adobe.com/docs/analytics/implementation/aep-edge/variable-mapping.html?lang=en) pour plus d’informations.


### Exemple #2 - scAdd

Si vous observez attentivement, tous les événements comportent deux champs. `value` (obligatoire) et `id` (facultatif). La variable `value` sert à incrémenter le nombre d’événements. La variable `id` est utilisé pour la sérialisation.

Cet objet :

```swift
"commerce" : {
  "productListAdds" : {
    "value" : 1
  }
}
```

a pour résultat :

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

a pour résultat :

```
s.events = "scAdd:321435"
```

## Validation avec Assurance

En utilisant la variable [Assurance](assurance.md) vous pouvez confirmer que vous envoyez un événement d’expérience, que les données XDM sont correctes et que le mappage Analytics se produit comme prévu.

1. Consultez la section [instructions de configuration](assurance.md#connecting-to-a-session) pour connecter le simulateur ou l’appareil à Assurance.

1. Envoyer un **[!UICONTROL productListAdds]** (ajoutez un produit à votre panier).

1. Affichez l’accès ExperienceEvent.

   ![accès xdm analytics](assets/analytics-assurance-experiencevent.png)

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

1. Consultez la section **[!UICONTROL analytics.mapping]** .

   ![accès xdm analytics](assets/analytics-assurance-mapping.png)

Notez ce qui suit dans le mappage Analytics :

* **[!UICONTROL events]** sont renseignées par `scAdd` basé sur `commerce.productListAdds`.
* **[!UICONTROL pl]** (variable products) sont renseignées par une valeur concaténée basée sur `productListItems`.
* Il y a d’autres informations intéressantes dans cet événement, y compris toutes les données contextuelles.


## Mappage avec les données contextuelles

Les données XDM transférées à Analytics sont converties en [données contextuelles](https://experienceleague.adobe.com/docs/mobile-services/ios/getting-started-ios/proc-rules.html?lang=en) comprenant des champs standard et personnalisés.

La clé de données contextuelles est construite selon la syntaxe suivante :

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
>Les champs personnalisés sont placés sous l’identifiant de votre organisation Experience Cloud.
>
>`_techmarketingdemos` est remplacé par la valeur unique de votre organisation.



Pour mapper ces données contextuelles XDM à vos données Analytics dans votre suite de rapports, vous pouvez :

### Utilisation d’un groupe de champs

* Ajoutez la variable **[!UICONTROL Extension complète Adobe Analytics ExperienceEvent]** groupe de champs à votre schéma.

  ![Groupe de champs Extension complète Analytics ExperienceEvent](assets/schema-analytics-extension.png)

* Créez des payloads XDM dans votre application, conformes au groupe de champs Extension complète Adobe Analytics ExperienceEvent , comme vous l’avez fait dans la section [Suivi des données d’événement](events.md) leçon ou
* Créez des règles dans la propriété Balises qui utilisent des actions de règle pour joindre ou modifier des données au groupe de champs Extension complète Adobe Analytics ExperienceEvent . Voir pour plus d’informations [Association de données aux événements du SDK](https://developer.adobe.com/client-sdks/documentation/user-guides/attach-data/) ou [Modification des données dans les événements du SDK](https://developer.adobe.com/client-sdks/documentation/user-guides/attach-data/).


### eVars de marchandisage

Si vous utilisez [eVars de marchandisage](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/conversion-variables/merchandising-evars.html?lang=en) dans votre configuration Analytics, par exemple pour capturer la couleur des produits, comme `&&products = ...;evar1=red;event10=50,...;evar1=blue;event10=60`, vous devez étendre la charge utile XDM que vous avez définie dans [Suivi des données d’événement](events.md) pour capturer ces informations de marchandisage.

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

Voici à quoi peut ressembler une règle de traitement utilisant ces données :

* You **[!UICONTROL Remplacer la valeur de]** (1) **[!UICONTROL Nom de l’écran de l’application (eVar2)]** (2) avec la valeur de **[!UICONTROL a.x._techmarketingdemo.appinformation.appstatedetails.screename]** (3) si **[!UICONTROL a.x._techmarketingdemo.appinformation.appstatedetails.screename]** (4) **[!UICONTROL est défini]** (5).

* You **[!UICONTROL Définir un événement]** (6) **[!UICONTROL Ajouter à la liste blanche (événement 3)]** (7) à **[!UICONTROL a.x.commerce.saveForLaters.value(Context)]** (8) si **[!UICONTROL a.x.commerce.saveForLaters.value(Context)]** (9) **[!UICONTROL est défini]** (10)

![règles de traitement analytics](assets/analytics-processing-rules.png)

>[!IMPORTANT]
>
>
>Certaines des variables mappées automatiquement ne peuvent pas être utilisées dans les règles de traitement.
>
>
>La première fois que vous mappez à une règle de traitement, l’interface ne vous affiche pas les variables de données contextuelles de l’objet XDM. Pour corriger les éléments qui sélectionnent une valeur, cliquez sur Enregistrer pour revenir à la modification. Toutes les variables XDM doivent maintenant apparaître.


Vous trouverez des informations supplémentaires sur les règles de traitement et les données contextuelles. [here](https://experienceleague.adobe.com/docs/analytics-learn/tutorials/implementation/implementation-basics/map-contextdata-variables-into-props-and-evars-with-processing-rules.html?lang=en).

>[!TIP]
>
>Contrairement aux mises en oeuvre précédentes d’applications mobiles, il n’existe aucune distinction entre les pages vues/écrans et d’autres événements. Vous pouvez à la place incrémenter la variable **[!UICONTROL Page vue]** en définissant la mesure **[!UICONTROL Nom de la page]** dans une règle de traitement. Puisque vous collectez le `screenName` dans le tutoriel, il est vivement recommandé de mapper le nom de l’écran à **[!UICONTROL Nom de la page]** dans une règle de traitement.


>[!SUCCESS]
>
>Vous avez configuré votre application pour mapper vos objets XDM Experience Edge aux variables Adobe Analytics en activant le service Adobe Analytics dans votre flux de données et en utilisant des règles de traitement le cas échéant.<br/> Merci d’investir votre temps à apprendre sur le SDK Adobe Experience Platform Mobile. Si vous avez des questions, souhaitez partager des commentaires généraux ou avez des suggestions sur le contenu futur, partagez-les à ce sujet. [Article de discussion de la communauté Experience League](https://experienceleaguecommunities.adobe.com:443/t5/adobe-experience-platform-data/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796).

Suivant : **[Envoi de données à l’Experience Platform](platform.md)**
