---
title: Mise en correspondance des données avec les données Analytics
description: Découvrez comment collecter et mapper des données pour Adobe Analytics dans une application mobile.
solution: Data Collection,Experience Platform,Analytics
hide: true
source-git-commit: 5f178f4bd30f78dff3243b3f5bd2f9d11c308045
workflow-type: tm+mt
source-wordcount: '632'
ht-degree: 2%

---

# Collecte et mappage des données Analytics

Découvrez comment mapper des données mobiles à Adobe Analytics.

La variable [event](events.md) les données que vous avez collectées et envoyées à Platform Edge Network dans les leçons précédentes sont transférées aux services configurés dans votre flux de données, y compris Adobe Analytics. Vous mappez les données aux variables correctes de votre suite de rapports.

![Architecture](assets/architecture-aa.png)

## Conditions préalables

* Présentation du suivi ExperienceEvent.
* Envoi réussi des données XDM dans votre exemple d’application.
* Flux de données configuré sur Adobe Analytics

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

La plupart des champs XDM standard sont automatiquement mappés aux variables Analytics. Voir la liste complète [ici](https://experienceleague.adobe.com/docs/experience-platform/edge/data-collection/adobe-analytics/automatically-mapped-vars.html?lang=en).

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

En utilisant la variable [Assurance](assurance.md) vous pouvez confirmer que vous envoyez un événement d’expérience, que les données XDM sont correctes et que le mappage Analytics se produit comme prévu. Par exemple :

1. Envoyez un événement productListAdds .

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
       "id" : "LLWS05.1-XS",
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

* Ajoutez la variable **[!UICONTROL Extension complète Adobe Analytics ExperienceEvent]** groupe de champs à votre schéma.

  ![Groupe de champs Extension complète Analytics ExperienceEvent](assets/schema-analytics-extension.png)
* Créez des règles dans la propriété Tags pour mapper les données contextuelles aux champs du groupe de champs Extension complète Adobe Analytics ExperienceEvent . Par exemple, map `_techmarketingdemo.appinformation.appstatedetails.screenname` to `_experience.analytics.customDimensions.eVars.eVar2`.

<!-- Old processing rules section
Here is what a processing rule using this data might look like:

* You **[!UICONTROL Overwrite value of]** (1) **[!UICONTROL App Screen Name (eVar2)]** (2) with the value of **[!UICONTROL a.x._techmarketingdemo.appinformation.appstatedetails.screenname]** (3) if **[!UICONTROL a.x._techmarketingdemo.appinformation.appstatedetails.screenname]** (4) **[!UICONTROL is set]** (5).

* You **[!UICONTROL Set event]** (6) **[!UICONTROL Add to Wishlist (Event 3)]** (7) to **[!UICONTROL a.x.commerce.saveForLaters.value(Context)]** (8) if **[!UICONTROL a.x.commerce.saveForLaters.value(Context)]** (9) **[!UICONTROL is set]** (10).

![analytics processing rules](assets/analytics-processing-rules.png)

>[!IMPORTANT]
>
>
>Some of the automatically mapped variables may not be available for use in processing rules.
>
>
>The first time you map to a processing rule, the interface does not show you the context data variables from the XDM object. To fix that select any value, Save, and come back to edit. All XDM variables should now appear.


Additional information about processing rules and context data can be found [here](https://experienceleague.adobe.com/docs/analytics-learn/tutorials/implementation/implementation-basics/map-contextdata-variables-into-props-and-evars-with-processing-rules.html?lang=en).

>[!TIP]
>
>Unlike previous mobile app implementations, there is no distinction between a page / screen views and other events. Instead you can increment the **[!UICONTROL Page View]** metric by setting the **[!UICONTROL Page Name]** dimension in a processing rule. Since you are collecting the custom `screenName` field in the tutorial, it is highly recommended to map screen name to **[!UICONTROL Page Name]** in a processing rule.

-->

>[!SUCCESS]
>
>Vous avez configuré votre application pour mapper vos objets XDM Experience Edge aux variables Adobe Analytics en activant le service Adobe Analytics dans votre flux de données et en utilisant des règles de traitement le cas échéant.<br/> Merci d’investir votre temps à apprendre sur le SDK Adobe Experience Platform Mobile. Si vous avez des questions, souhaitez partager des commentaires généraux ou avez des suggestions sur le contenu futur, partagez-les à ce sujet. [Article de discussion de la communauté Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796).

Suivant : **[Envoi de données à l’Experience Platform](platform.md)**
