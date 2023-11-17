---
title: Mappage Analytics
description: Découvrez comment collecter des données pour Adobe Analytics dans une application mobile.
solution: Data Collection,Experience Platform,Analytics
exl-id: 406dc687-643f-4f7b-a8e7-9aad1d0d481d
source-git-commit: bc53cb5926f708408a42aa98a1d364c5125cb36d
workflow-type: tm+mt
source-wordcount: '608'
ht-degree: 1%

---

# Mappage Analytics

Découvrez comment mapper des données mobiles à Adobe Analytics.

>[!INFO]
>
> Ce tutoriel sera remplacé par un nouveau tutoriel utilisant un nouvel exemple d’application mobile à la fin novembre 2023.


La variable [event](events.md) les données que vous avez collectées et envoyées à Platform Edge Network dans les leçons précédentes sont transférées aux services configurés dans votre flux de données, y compris Adobe Analytics. Il vous suffit de mettre en correspondance les données avec les variables correctes de votre suite de rapports.

## Conditions préalables

* Présentation du suivi ExperienceEvent.
* Envoi réussi des données XDM dans votre exemple d’application.
* Flux de données configuré sur Adobe Analytics

## Objectifs d&#39;apprentissage

Dans cette leçon, vous allez :

* Comprendre le mappage automatique des variables Analytics.
* Configurez les règles de traitement pour mapper les données XDM aux variables Analytics.

## Mise en correspondance automatique

La plupart des champs XDM standard sont automatiquement mappés aux variables Analytics. Voir la liste complète [ici](https://experienceleague.adobe.com/docs/experience-platform/edge/data-collection/adobe-analytics/automatically-mapped-vars.html?lang=en).

### Exemple #1 - s.products

Un bon exemple est le suivant : [variable products](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/products.html?lang=en) qui ne peuvent pas être renseignées à l’aide de règles de traitement. Avec une implémentation XDM, vous transmettez toutes les données nécessaires dans productListItems et s.products est automatiquement renseigné via le mappage Analytics.

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

Cela se traduirait par ce qui suit :

```
s.products = ";Yoga Mat;1;49.99,;Water Bottle,3,30.00"
```

>[!NOTE]
>
>Actuellement `productListItems[N].SKU` est ignorée par le mappage automatique.

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

Cela se traduirait par ce qui suit :

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

Cela se traduirait par ce qui suit :

```
s.events = "scAdd:321435"
```

## Validation avec Assurance

En utilisant la variable [Outil Assurance qualité](assurance.md) vous pouvez confirmer que vous envoyez un événement ExperienceEvent, que les données XDM sont correctes et que le mappage Analytics se produit comme prévu. Par exemple :

1. Envoyez un événement productListAdds .

   ```swift
   var xdmData: [String: Any] = [
     "eventType": "commerce.productListAdds",
     "commerce": [
       "productListAdds": [
         "value": 1
       ]
     ],
     "productListItems": [
       [
         "name": "neve studio dance jacket - (blue)",
         "SKU": "test-sku",
         "priceTotal": 69
       ]
     ]
   ]
   let addToCartEvent = ExperienceEvent(xdm: xdmData)
   Edge.sendEvent(experienceEvent: addToCartEvent)
   ```

1. Affichez l’accès ExperienceEvent.

   ![accès xdm analytics](assets/mobile-analytics-assurance-xdm.png)

1. Examinez la partie XDM du fichier JSON.

   ```json
     "xdm" : {
       "productListItems" : [ {
         "priceTotal" : 69,
         "SKU" : "test-sku",
         "name" : "neve studio dance jacket - (blue)"
       } ],
       "timestamp" : "2021-10-22T22:03:37Z",
       "commerce" : {
         "productListAdds" : {
           "value" : 1
         }
       },
       "eventType" : "commerce.productListAdds",
       //...
     }
   ```

1. Consultez la section `analytics.mapping` .

   ![accès xdm analytics](assets/mobile-analytics-assurance-mapping.png)

Notez ce qui suit dans le mappage Analytics :

* &quot;events&quot; a été renseigné avec &quot;scAdd&quot; sur la base de `commerce.productListAdds`.
* &quot;pl&quot; (variable products) a été renseigné avec une valeur concaténée basée sur `productListItems`.
* Il y a d’autres informations intéressantes dans cet événement, y compris toutes les données contextuelles.


## Mappage avec les données contextuelles

Les données XDM transférées à Analytics sont converties en [données contextuelles](https://experienceleague.adobe.com/docs/mobile-services/ios/getting-started-ios/proc-rules.html?lang=en) comprenant des champs standard et personnalisés.

La clé de données contextuelles est construite selon la syntaxe suivante :

```
a.x.[xdm path]
```

Par exemple :

```
//Standard Field
a.x.commerce.saveforlaters.value

//Custom Field
a.x._techmarketingdemos.appinformationa.appstatedetails.screenname
```

>[!NOTE]
>
>Les champs personnalisés sont placés sous l’identifiant de votre organisation Experience Cloud.
>
>&quot;_techmarketingdemos&quot; est remplacé par la valeur unique de votre organisation.

Voici à quoi peut ressembler une règle de traitement utilisant ces données :

![règles de traitement analytics](assets/mobile-analytics-processing-rules.png)

>[!IMPORTANT]
>
>
>Certaines des variables mappées automatiquement ne peuvent pas être utilisées dans les règles de traitement.
>
>
>La première fois que vous mappez à une règle de traitement, l’interface utilisateur ne vous affiche pas les variables de données contextuelles de l’objet XDM. Pour corriger les éléments qui sélectionnent une valeur, cliquez sur Enregistrer pour revenir à la modification. Toutes les variables XDM doivent maintenant apparaître.


Vous trouverez des informations supplémentaires sur les règles de traitement et les données contextuelles. [here](https://experienceleague.adobe.com/docs/analytics-learn/tutorials/implementation/implementation-basics/map-contextdata-variables-into-props-and-evars-with-processing-rules.html?lang=en).

>[!TIP]
>
>Contrairement aux mises en oeuvre précédentes d’applications mobiles, il n’existe aucune distinction entre les pages vues/écrans et les autres événements. Vous pouvez à la place incrémenter la variable **[!UICONTROL Page vue]** en définissant la mesure **[!UICONTROL Nom de la page]** dans une règle de traitement. Puisque vous collectez le `screenName` dans le tutoriel, il est vivement recommandé de mapper ceci à **[!UICONTROL Nom de la page]** dans une règle de traitement.


Suivant : **[Experience Platform](platform.md)**

>[!NOTE]
>
>Merci d’investir votre temps à apprendre sur le SDK Adobe Experience Platform Mobile. Si vous avez des questions, souhaitez partager des commentaires généraux ou avez des suggestions sur le contenu futur, partagez-les à ce sujet. [Article de discussion de la communauté Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796)