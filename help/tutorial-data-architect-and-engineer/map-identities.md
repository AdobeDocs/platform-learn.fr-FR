---
title: Mapping d’identités
seo-title: Map identities | Getting Started with Adobe Experience Platform for Data Architects and Data Engineers
breadcrumb-title: Mapping d’identités
description: Dans cette leçon, nous allons créer des espaces de noms d’identité et ajouter des champs d’identité à nos schémas.
role: Data Architect
feature: Profiles
jira: KT-4348
thumbnail: 4348-map-identities.jpg
exl-id: e17ffabc-049c-42ff-bf0a-8cc31d665dfa
source-git-commit: 73645b8b088cfdfe6f256c187b3c510dcc2386fc
workflow-type: tm+mt
source-wordcount: '937'
ht-degree: 6%

---

# Mapping d’identités

<!-- 30 min-->

Dans cette leçon, nous allons créer des espaces de noms d’identité et ajouter des champs d’identité à nos schémas. Après cela, nous serons également en mesure d’établir les relations de schéma de la leçon précédente.

Adobe Experience Platform Identity Service vous permet de mieux connaître vos clients et leurs comportements, en établissant un lien entre les identités des différents appareils et systèmes, ce qui vous permet de proposer des expériences digitales personnelles et percutantes en temps réel. Les champs d’identité et les espaces de noms sont le ciment qui relie différentes sources de données pour créer le profil client en temps réel à 360 degrés.

**Architectes de données** devront mapper les identités en dehors de ce tutoriel.

Avant de commencer les exercices, regardez cette courte vidéo pour en savoir plus sur l’identité dans Adobe Experience Platform :
>[!VIDEO](https://video.tv.adobe.com/v/3422771?learn=on&enablevpops&captions=fre_fr)

>[!NOTE]
>
>Les champs d’identité ne sont obligatoires que si vous créez des profils clients en temps réel. Elles ne sont pas requises si vous ingérez uniquement des données dans le lac de données.

<!--explain identity maps-->
<!--explain the strategy behind the identity selection, how these identities will join all the data together-->

## Autorisations requises

Dans la leçon [Configurer les autorisations](configure-permissions.md), vous allez configurer tous les contrôles d’accès requis pour suivre cette leçon.

<!--
* Permission items **[!UICONTROL Identity Management]** > **[!UICONTROL View Identity Namespaces]** and **[!UICONTROL Manage Identity Namespaces]**
* Permission item **[!UICONTROL Data Modeling]** > **[!UICONTROL View Schemas]** and **[!UICONTROL Manage Schemas]**
* Permission item **[!UICONTROL Sandboxes]** > `Luma Tutorial`
* User-role access to the `Luma Tutorial Platform` product profile
* Developer-role access to the `Luma Tutorial Platform` product profile (for API)
-->

## Créer un espace de noms identité

Dans cet exercice, nous allons créer des espaces de noms d’identité pour les champs d’identité personnalisés, `loyaltyId`, `crmId` et `productSku` de Luma. Les espaces de noms d’identité jouent un rôle essentiel dans la création de profils clients en temps réel, car deux valeurs correspondantes dans le même espace de noms permettent à deux sources de données de former un graphique d’identité.


### Création d’espaces de noms dans l’interface utilisateur

Commençons par créer un espace de noms pour le schéma de fidélité Luma :

1. Dans l’interface utilisateur de Platform, accédez à **[!UICONTROL Identités]** dans le volet de navigation de gauche
1. Vous remarquerez qu’il existe plusieurs espaces de noms d’identité d’usine disponibles. Sélectionnez le bouton **[!UICONTROL Créer un espace de noms d’identité]**
1. Fournissez les détails suivants :

   | Champ | Valeur |
   |---------------|-----------|
   | Nom d’affichage | Identifiant de fidélité Luma |
   | Symbole d’identité | lumaLoyaltyId |
   | Type | Multi-appareils |

1. Sélectionnez **[!UICONTROL Créer]**

   ![Création d’espaces de noms.](assets/identity-createNamespace.png)

Configurez maintenant un autre espace de noms pour le schéma de catalogue de produits Luma avec les détails suivants :

| Champ | Valeur |
|---------------|-----------|
| Nom d’affichage | SKU du produit Luma |
| Symbole d’identité | lumaProductSKU |
| Type | Identifiant non personnel |



## Créer un espace de noms d’identité à l’aide de l’API

Nous allons créer notre espace de noms CRM via l&#39;API.

>[!NOTE]
>
>Si vous préférez ignorer les exercices d’API, n’hésitez pas à créer l’espace de noms CRM par le biais de la méthode de l’interface utilisateur que vous avez utilisée avec les détails suivants :
>
> 1. Comme **[!UICONTROL Nom d’affichage]**, utilisez `Luma CRM Id`
> 1. Comme **[!UICONTROL symbole d’identité]**, utilisez `lumaCrmId`
> 1. Comme **[!UICONTROL Type]**, utilisez l’option sur plusieurs appareils

Créons l’espace de noms d’identité `Luma CRM Id` :

1. Téléchargez [Identity Service.postman_collection.json](https://raw.githubusercontent.com/adobe/experience-platform-postman-samples/master/apis/experience-platform/Identity%20Service.postman_collection.json) dans votre dossier `Luma Tutorial Assets`
1. Importer la collection dans [!DNL Postman]
1. Si vous ne disposez pas d’un jeton d’accès, ouvrez le **[!DNL OAuth: Request Access Token]** de requête et sélectionnez **Envoyer** pour demander un nouveau jeton d’accès.
1. Sélectionnez la requête **[!UICONTROL Service d’identités] > [!UICONTROL Espace de noms d’identité] > [!UICONTROL Créer un espace de noms d’identité].**
1. Collez les éléments suivants en tant que [!DNL Body] de la requête :

   ```json
   {
       "name": "Luma CRM Id",
       "code": "lumaCrmId",
       "idType": "Cross_device"
   }
   ```

1. Appuyez sur le bouton **Envoyer** pour obtenir une réponse **200 OK** :

   ![Espace de noms d’identité](assets/identity-createUsingApi.png)

Si vous revenez à l’interface utilisateur, vous devriez maintenant voir vos trois nouveaux espaces de noms personnalisés :
![Espace de noms d’identité ](assets/identity-newIdentities.png)


## Champs d’identité des libellés dans les schémas

Maintenant que nous avons nos espaces de noms, l’étape suivante consiste à mettre à jour nos schémas pour libeller nos champs d’identité.


### Étiqueter les champs XDM pour l’identité du Principal

Chaque schéma utilisé avec le profil client en temps réel est requis pour qu’une identité principale soit spécifiée. Et chaque enregistrement ingéré doit avoir une valeur pour ce champ.

Ajoutons une identité principale au `Luma Loyalty Schema` :

1. Ouvrir le `Luma Loyalty Schema`
1. Sélectionner le `Luma Identity profile field group`
1. Sélectionner le champ `loyaltyId`
1. Cochez la case **[!UICONTROL Identité]**
1. Cochez également la case **[!UICONTROL Identité du Principal]**
1. Sélectionnez l’espace de noms `Luma Loyalty Id` dans le menu déroulant **[!UICONTROL Espaces de noms d’identité]**
1. Sélectionnez **[!UICONTROL Appliquer]**
1. Sélectionnez **[!UICONTROL Enregistrer]**

   ![](assets/identity-loyalty-primary.png) d’identité de Principal

Répétez le processus pour certains de vos autres schémas :

1. Dans la `Luma CRM Schema`, libellez le champ `crmId` comme identité principale à l’aide de l’espace de noms `Luma CRM Id`
1. Dans la `Luma Offline Purchase Events Schema`, libellez le champ `loyaltyId` comme identité principale à l’aide de l’espace de noms `Luma Loyalty Id`
1. Dans la `Luma Product Catalog Schema`, libellez le champ `productSku` comme identité principale à l’aide de l’espace de noms `Luma Product SKU`

>[!NOTE]
>
>Les données collectées avec le SDK Web constituent une exception à la pratique courante consistant à libeller les champs d’identité dans le schéma . Web SDK utilise le mappage d’identités pour libeller les identités *côté implémentation* et ainsi nous déterminerons les identités de l’`Luma Web Events Schema` lorsque nous implémentons Web SDK sur le site Web Luma. Dans cette leçon ultérieure, nous allons collecter l’identifiant visiteur Experience Cloud (ECID) en tant qu’identifiant principal et crmId en tant qu’identifiant secondaire.

Avec notre sélection d’identités principales, il est clair que `Luma Loyalty Schema` pouvez vous connecter à l’`Luma Offline Purchase Events Schema`, car ils utilisent tous deux loyaltyId comme identifiant. Mais comment le CRM peut-il se connecter aux événements d’achat hors ligne ? Comment relier nos achats hors ligne au comportement en ligne ? Et comment classer les produits achetés avec notre catalogue de produits ? Nous utiliserons d’autres champs d’identité et relations de schéma.

<!--use a visual-->

### Étiqueter les champs XDM pour l’identité Secondaire

Plusieurs champs d’identité peuvent être ajoutés à un schéma. Les identités non principales sont souvent appelées identités secondaires. Pour connecter les achats hors ligne au comportement en ligne, nous ajouterons le crmId en tant qu’identifiant secondaire à notre `Luma Loyalty Schema` et ultérieurement dans nos données d’événements web. Mettons à jour le `Luma Loyalty Schema` :

1. Ouvrir le `Luma Loyalty Schema`
1. Sélectionner un `Luma Identity Profile Field group`
1. Sélectionner `crmId` champ
1. Cochez la case **[!UICONTROL Identité]**
1. Sélectionnez l’espace de noms `Luma CRM Id` dans le menu déroulant **[!UICONTROL Espaces de noms d’identité]**
1. Sélectionnez **[!UICONTROL Appliquer]** puis cliquez sur le bouton **[!UICONTROL Enregistrer]** pour enregistrer vos modifications

   ![Identité Secondaire ](assets/identity-loyalty-secondaryId.png)

## Compléter les relations de schéma

Maintenant que nos champs d’identité sont étiquetés, nous pouvons terminer la configuration des relations de schéma entre le catalogue de produits de Luma et les schémas d’événement :

1. Ouvrir le `Luma Offline Purchase Events Schema`
1. Sélectionner le groupe de champs **[!UICONTROL Détails Commerce]**
1. Sélectionnez le champ **[!UICONTROL productListItems]** > **[!UICONTROL SKU]**
1. Cochez la case **[!UICONTROL Relation]**
1. Sélectionnez `Luma Product Catalog Schema` comme **[!UICONTROL Schéma de référence]**
1. `Luma Product SKU` doit automatiquement être renseigné comme espace de noms d’identité de **[!UICONTROL référence]**
1. Sélectionnez **[!UICONTROL Appliquer]**
1. Sélectionnez **[!UICONTROL Enregistrer]**

   ![ Champ de référence ](assets/identity-offlinePurchase-relationship.png)

Répétez ce processus pour créer une relation entre le `Luma Web Events Schema` et le `Luma Product Catalog Schema`.

Notez qu’après avoir défini la relation, elle est indiquée à la fois dans les sections **[!UICONTROL Composition]** et **[!UICONTROL Structure]** de l’éditeur de schéma.

![Visualisation des relations dans l’éditeur de schémas](assets/identity-webEvents-relationship.png)

<!--need to verify that the relationship schema works-->

## Ressources supplémentaires

* [Documentation Identity Service](https://experienceleague.adobe.com/docs/experience-platform/identity/home.html?lang=fr)
* [API Service d’identités](https://www.adobe.io/experience-platform-apis/references/identity-service/)

Maintenant que nos identités sont en place, nous pouvons [créer nos jeux de données](create-datasets.md) !
