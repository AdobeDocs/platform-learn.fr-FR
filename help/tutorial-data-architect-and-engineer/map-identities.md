---
title: Mapping d’identités
seo-title: Map identities | Getting Started with Adobe Experience Platform for Data Architects and Data Engineers
breadcrumb-title: Mapping d’identités
description: Dans cette leçon, nous allons créer des espaces de noms d’identité et ajouter des champs d’identité à nos schémas.
role: Data Architect
feature: Profiles
kt: 4348
thumbnail: 4348-map-identities.jpg
exl-id: e17ffabc-049c-42ff-bf0a-8cc31d665dfa
source-git-commit: cf0193e3aae4d6536c868f078f4773ee14e90408
workflow-type: tm+mt
source-wordcount: '954'
ht-degree: 4%

---

# Mapping d’identités

<!-- 30 min-->

Dans cette leçon, nous allons créer des espaces de noms d’identité et ajouter des champs d’identité à nos schémas. Après cela, nous pourrons également terminer les relations de schéma de la leçon précédente.

Adobe Experience Platform Identity Service vous permet de mieux connaître vos clients et leurs comportements en rapprochant des identités entre appareils et systèmes, ce qui vous permet de proposer des expériences numériques personnelles et percutantes en temps réel. Les champs d’identité et les espaces de noms sont la colle qui relie différentes sources de données pour créer le profil client en temps réel à 360 degrés.

**Architectes de données** Vous devrez mapper des identités en dehors de ce tutoriel.

Avant de commencer les exercices, regardez cette courte vidéo pour en savoir plus sur l’identité dans Adobe Experience Platform :
>[!VIDEO](https://video.tv.adobe.com/v/27841?quality=12&learn=on)

>[!NOTE]
>
>Les champs d’identité ne sont requis que si vous créez des profils clients en temps réel. Elles ne sont pas requises si vous ingérez uniquement des données dans le lac de données.

<!--explain identity maps-->
<!--explain the strategy behind the identity selection, how these identities will join all the data together-->

## Autorisations requises

Dans le [Configuration des autorisations](configure-permissions.md) leçon, vous configurez tous les contrôles d’accès requis pour terminer cette leçon.

<!--
* Permission items **[!UICONTROL Identity Management]** > **[!UICONTROL View Identity Namespaces]** and **[!UICONTROL Manage Identity Namespaces]**
* Permission item **[!UICONTROL Data Modeling]** > **[!UICONTROL View Schemas]** and **[!UICONTROL Manage Schemas]**
* Permission item **[!UICONTROL Sandboxes]** > `Luma Tutorial`
* User-role access to the `Luma Tutorial Platform` product profile
* Developer-role access to the `Luma Tutorial Platform` product profile (for API)
-->

## Créer un espace de noms d’identité

Dans cet exercice, nous allons créer des espaces de noms d’identité pour les champs d’identité personnalisés de Luma, `loyaltyId`, `crmId`, et `productSku`. Les espaces de noms d’identité jouent un rôle essentiel dans la création de profils clients en temps réel, car deux valeurs correspondantes dans le même espace de noms permettent à deux sources de données de former un graphique d’identités.


### Création d’espaces de noms dans l’interface utilisateur

Commençons par créer un espace de noms pour le schéma de fidélité Luma :

1. Dans l’interface utilisateur de Platform, accédez à **[!UICONTROL Identités]** dans le volet de navigation de gauche
1. Vous remarquerez que plusieurs espaces de noms d’identité d’usine sont disponibles. Sélectionnez la **[!UICONTROL Créer un espace de noms d’identité]** button
1. Fournissez les détails suivants :

   | Champ | Valeur |
   |---------------|-----------|
   | Nom d’affichage | Identifiant De Fidélité Luma |
   | Symbole d’identité | lumaLoyaltyId |
   | Type | Multi-appareils |

1. Sélectionnez **[!UICONTROL Créer]**

   ![Créer des espaces de noms](assets/identity-createNamespace.png)

Configurez maintenant un autre espace de noms pour le schéma du catalogue de produits Luma avec les détails suivants :

| Champ | Valeur |
|---------------|-----------|
| Nom d’affichage | SKU du produit Luma |
| Symbole d’identité | lumaProductSKU |
| Type | Identifiant de non-personne |



## Création d’un espace de noms d’identité à l’aide de l’API

Nous allons créer notre espace de noms CRM via l&#39;API.

>[!NOTE]
>
>Si vous préférez ignorer les exercices d’API, n’hésitez pas à créer l’espace de noms CRM via la méthode d’interface utilisateur que vous avez utilisée avec les détails suivants :
>
> 1. Comme la variable **[!UICONTROL Nom d’affichage]**, utilisez `Luma CRM Id`
> 1. Comme la variable **[!UICONTROL Symbole d’identité]**, utilisez `lumaCrmId`
> 1. Comme la variable **[!UICONTROL Type]**, utilisez le mode multi-appareils


Créons l’espace de noms d’identité `Luma CRM Id`:

1. Télécharger [Identity Service.postman_collection.json](https://raw.githubusercontent.com/adobe/experience-platform-postman-samples/master/apis/experience-platform/Identity%20Service.postman_collection.json) à `Luma Tutorial Assets` folder
1. Importez la collection dans [!DNL Postman]
1. Si vous n’avez pas fait de demande au cours des dernières 24 heures, vos jetons d’autorisation ont probablement expiré. Ouvrir la requête **[!DNL Adobe I/O Access Token Generation > Local Signing (Non-production use-only) > IMS: JWT Generate + Auth via User Token]**, puis sélectionnez **Envoyer** pour demander de nouveaux jetons JWT et d’accès.
1. Sélectionner la requête **[!UICONTROL Identity Service] > [!UICONTROL Espace de noms d’identité] > [!UICONTROL Création d’un espace de noms d’identité].**
1. Collez les éléments suivants en tant que [!DNL Body] de la requête :

   ```json
   {
       "name": "Luma CRM Id",
       "code": "lumaCrmId",
       "idType": "Cross_device"
   }
   ```

1. Appuyez sur la touche **Envoyer** et vous devriez obtenir un **200 OK** response :

   ![Espace de noms d’identité](assets/identity-createUsingApi.png)

Si vous revenez à l’interface utilisateur, vos trois nouveaux espaces de noms personnalisés s’affichent désormais :
![Espace de noms d’identité ](assets/identity-newIdentities.png)


## Étiquetage des champs d’identité dans les schémas

Maintenant que nous disposons de nos espaces de noms, l’étape suivante consiste à mettre à jour nos schémas pour étiqueter nos champs d’identité.


### Étiquetage Des Champs XDM Pour L’Identité Principal

Chaque schéma utilisé avec Real-time Customer Profile doit disposer d’une identité Principale spécifiée. Et chaque enregistrement ingéré doit avoir une valeur pour ce champ.

Ajoutons une identité Principale à la variable `Luma Loyalty Schema`:

1. Ouvrez le `Luma Loyalty Schema`
1. Sélectionnez l’événement `Luma Identity profile field group`.
1. Sélectionnez la `loyaltyId` field
1. Vérifiez les **[!UICONTROL Identité]** box
1. Vérifiez les **[!UICONTROL Identité Principal]** box, également
1. Sélectionnez la `Luma Loyalty Id` namespace de **[!UICONTROL Espaces de noms d’identité]** menu déroulant
1. Sélectionner **[!UICONTROL Appliquer]**
1. Sélectionnez **[!UICONTROL Enregistrer]**

   ![Identité Principal ](assets/identity-loyalty-primary.png)

Répétez le processus pour certains de vos autres schémas :

1. Dans le `Luma CRM Schema`, étiquetez la variable `crmId` comme identité Principale à l’aide de la variable `Luma CRM Id` namespace
1. Dans le `Luma Offline Purchase Events Schema`, étiquetez la variable `loyaltyId` comme identité Principale à l’aide de la variable `Luma Loyalty Id` namespace
1. Dans le `Luma Product Catalog Schema`, étiquetez la variable `productSku` comme identité Principale à l’aide de la variable `Luma Product SKU` namespace

>[!NOTE]
>
>Les données collectées avec le SDK Web constituent une exception à la pratique habituelle de l’étiquetage des champs d’identité dans le schéma. Le SDK Web utilise la carte des identités pour étiqueter les identités *côté implémentation* et ainsi, nous déterminerons les identités pour la variable `Luma Web Events Schema` lorsque nous implémentons le SDK Web sur le site web de Luma. Dans cette leçon ultérieure, nous allons collecter l’identifiant visiteur Experience Cloud (ECID) en tant qu’identifiant Principal et l’identifiant crmId en tant qu’identifiant secondaire.

Avec notre sélection d&#39;identités Principales, il est clair de voir comment `Luma CRM Schema` peut se connecter au `Luma Offline Purchase Events Schema` car ils utilisent tous deux `loyaltyId` comme identifiant. Mais comment pouvons-nous connecter nos achats hors ligne au comportement en ligne ? Comment classer les produits achetés avec notre catalogue de produits ? Nous utiliserons d’autres champs d’identité et relations de schémas.

<!--use a visual-->

### Étiquetage Des Champs XDM Pour L’Identité Secondaire

Plusieurs champs d’identité peuvent être ajoutés à un schéma. Les identités non Principales sont souvent appelées identités secondaires. Pour connecter les achats hors ligne au comportement en ligne, nous allons ajouter crmId en tant qu’identifiant secondaire à notre `Luma Loyalty Schema` et plus tard dans nos données d’événements web. Mettons à jour le `Luma Loyalty Schema`:

1. Ouvrez le `Luma Loyalty Schema`
1. Sélectionner `Luma Identity Profile Field group`
1. Sélectionner `crmId` field
1. Vérifiez les **[!UICONTROL Identité]** box
1. Sélectionnez la `Luma CRM Id` namespace de **[!UICONTROL Espaces de noms d’identité]** menu déroulant
1. Sélectionner **[!UICONTROL Appliquer]** puis sélectionnez l’option **[!UICONTROL Enregistrer]** pour enregistrer vos modifications.

   ![Identité Secondaire](assets/identity-loyalty-secondaryId.png)

## Compléter les relations de schéma

Maintenant que nos champs d’identité sont libellés, nous pouvons terminer la configuration des relations de schéma entre le catalogue de produits de Luma et les schémas d’événement :

1. Ouvrez le `Luma Offline Purchase Events Schema`
1. Sélectionner **[!UICONTROL Détails du commerce]** groupe de champs
1. Sélectionner **[!UICONTROL productListItems]** > **[!UICONTROL SKU]** field
1. Vérifiez les **[!UICONTROL Relation]** box
1. Sélectionner `Luma Product Catalog Schema` comme la propriété **[!UICONTROL Schéma de référence]**
1. `Luma Product SKU` doit être automatiquement renseigné en tant que **[!UICONTROL Espace de noms d’identité de référence]**
1. Sélectionner **[!UICONTROL Appliquer]**
1. Sélectionnez **[!UICONTROL Enregistrer]**

   ![Champ de référence](assets/identity-offlinePurchase-relationship.png)

Répétez ce processus pour créer une relation entre la variable `Luma Web Events Schema` et le `Luma Product Catalog Schema`.

Notez qu’après avoir défini la relation, elle est indiquée dans la variable **[!UICONTROL Composition]** et **[!UICONTROL Structure]** de l’éditeur de schéma.

![Visualisation des relations dans l’éditeur de schémas](assets/identity-webEvents-relationship.png)

<!--need to verify that the relationship schema works-->

## Ressources supplémentaires

* [Documentation d’Identity Service](https://experienceleague.adobe.com/docs/experience-platform/identity/home.html?lang=fr)
* [API Identity Service](https://www.adobe.io/experience-platform-apis/references/identity-service/)

Maintenant que nos identités sont en place, nous pouvons [création de nos jeux de données](create-datasets.md)!
