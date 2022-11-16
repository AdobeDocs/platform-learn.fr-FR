---
title: Création de jeux de données
seo-title: Create datasets | Getting Started with Adobe Experience Platform for Data Architects and Data Engineers
breadcrumb-title: Création de jeux de données
description: Dans cette leçon, vous allez créer des jeux de données pour recevoir vos données.
role: Data Architect, Data Engineer
feature: Data Management
kt: 4348
thumbnail: 4348-create-datasets.jpg
exl-id: 80227af7-4976-4fd2-b1d4-b26bc4626fa0
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '581'
ht-degree: 9%

---

# Création de jeux de données

<!--15min-->

Dans cette leçon, vous allez créer des jeux de données pour recevoir vos données. Vous serez heureux de savoir qu’il s’agit de la leçon la plus courte du tutoriel !

Toutes les données correctement ingérées dans Adobe Experience Platform sont conservées en tant que jeux de données dans le lac de données. Un jeu de données est une structure de stockage et de gestion pour la collecte de données, généralement sous la forme d’un tableau, qui contient un schéma (des colonnes) et des champs (des lignes). Les jeux de données contiennent également des métadonnées qui décrivent divers aspects des données stockées.

**Architectes de données** Vous devrez créer des jeux de données en dehors de ce tutoriel.

Avant de commencer les exercices, regardez cette courte vidéo pour en savoir plus sur les jeux de données :
>[!VIDEO](https://video.tv.adobe.com/v/27269?quality=12&learn=on)

## Autorisations requises

Dans le [Configuration des autorisations](configure-permissions.md) leçon, vous configurez tous les contrôles d’accès requis pour terminer cette leçon.

<!--
* Permission items **[!UICONTROL Data Management]** > **[!UICONTROL View Datasets]** and **[!UICONTROL Manage Datasets]**
* Permission item **[!UICONTROL Sandboxes]** > `Luma Tutorial`
* User-role access to the `Luma Tutorial Platform` product profile
* Developer-role access to the `Luma Tutorial Platform` product profile (for API)
-->

## Création de jeux de données dans l’interface utilisateur

Au cours de cet exercice, nous allons créer des jeux de données dans l’interface utilisateur. Commençons par les données de fidélité :

1. Accédez à **[!UICONTROL Jeux de données]** dans la navigation de gauche de l’interface utilisateur de Platform
1. Sélectionnez la **[!UICONTROL Création d’un jeu de données]** button
   ![Création d’un jeu de données](assets/datasets-createDataset.png)

1. Dans l’écran suivant, sélectionnez **Création d’un jeu de données à partir d’un schéma**
1. Dans l’écran suivant, sélectionnez votre `Luma Loyalty Schema` puis sélectionnez l’option **[!UICONTROL Suivant]** button
   ![Sélectionner le jeu de données](assets/datasets-selectSchema.png)

1. Nommer le jeu de données `Luma Loyalty Dataset` et sélectionnez la variable **[!UICONTROL Terminer]** button
   ![Nommer le jeu de données](assets/datasets-nameDataset.png)
1. Une fois le jeu de données enregistré, vous accédez à un écran comme celui-ci :
   ![Jeu de données créé](assets/datasets-created.png)

Vous avez terminé. Je vous ai dit que ça allait être rapide. Créez ces autres jeux de données en suivant les mêmes étapes :

1. `Luma Offline Purchase Events Dataset` pour votre `Luma Offline Purchase Events Schema`
1. `Luma Web Events Dataset` pour votre `Luma Web Events Schema`
1. `Luma Product Catalog Dataset` pour votre `Luma Product Catalog Schema`


## Création d’un jeu de données à l’aide d’une API

Créez maintenant le `Luma CRM Dataset` à l’aide de l’API.

>[!NOTE]
>
>Si vous souhaitez ignorer l’exercice d’API et créer la variable `Luma CRM Dataset` dans l’interface utilisateur. Nommez-le `Luma CRM Dataset` et utilisez la fonction `Luma CRM Schema`.

### Obtention de l’identifiant du schéma à utiliser dans le jeu de données

Tout d’abord, nous devons obtenir le `$id` de `Luma CRM Schema`:

1. Ouvrir [!DNL Postman]
1. Si vous n’avez pas fait de demande au cours des dernières 24 heures, vos jetons d’autorisation ont probablement expiré. Ouvrir la requête **[!DNL Adobe I/O Access Token Generation > Local Signing (Non-production use-only) > IMS: JWT Generate + Auth via User Token]** et sélectionnez **Envoyer** pour demander de nouveaux jetons JWT et d’accès, comme vous l’avez fait dans la variable [!DNL Postman] leçon.
1. Ouvrir la requête **[!DNL Schema Registry API > Schemas > Retrieve a list of schemas within the specified container.]**
1. Sélectionnez la **Envoyer** button
1. Vous devriez obtenir une réponse 200
1. Recherchez dans la réponse pour la variable `Luma CRM Schema` et copiez l’élément `$id` value
   ![Copiez le $id](assets/dataset-crm-getSchemaId.png)

### Création du jeu de données

Vous pouvez maintenant créer le jeu de données :

1. Télécharger [API.postman_collection.json du service de catalogue](https://raw.githubusercontent.com/adobe/experience-platform-postman-samples/master/apis/experience-platform/Catalog%20Service%20API.postman_collection.json) à `Luma Tutorial Assets` dossier.
1. Importez la collection dans [!DNL Postman]
1. Sélectionner la requête **[!DNL Catalog Service API > Datasets > Create a new dataset.]**
1. Collez les éléments suivants en tant que **Corps** de la requête, ***en remplaçant la valeur id par la vôtre***:

   ```json
   {
       "name": "Luma CRM Dataset",
   
       "schemaRef": {
           "id": "REPLACE_WITH_YOUR_OWN_ID",
           "contentType": "application/vnd.adobe.xed-full+json;version=1"
       },
       "fileDescription": {
           "persisted": true,
           "containerFormat": "parquet",
           "format": "parquet"
       }
   }
   ```

1. Sélectionnez la **Envoyer** button
1. Vous devriez obtenir une réponse 201 Créée contenant l’identifiant de votre nouveau jeu de données !
   ![Jeu de données créé avec l’API, votre $id personnalisé utilisé dans le corps](assets/datasets-crm-created.png)

>[!TIP]
>
> Problèmes courants à l’origine de cette demande et correctifs probables :
>
> * `400: There was a problem retrieving xdm schema`. Assurez-vous d’avoir remplacé l’identifiant dans l’exemple ci-dessus par l’identifiant de votre propre compte. `Luma CRM Schema`
> * Aucun jeton d’authentification : Exécutez la variable **IMS : JWT Generate + Auth via User Token** appel pour générer de nouveaux jetons
> * `401: Not Authorized to PUT/POST/PATCH/DELETE for this path : /global/schemas/`: Mettez à jour le **CONTAINER_ID** Variable d’environnement de `global` to `tenant`
> * `403: PALM Access Denied. POST access is denied for this resource from access control`: Vérification des autorisations utilisateur dans le Admin Console



Vous pouvez revenir au **[!UICONTROL Jeux de données]** dans l’interface utilisateur de Platform, vous pouvez vérifier la création réussie des cinq jeux de données.
![Cinq jeux de données terminés](assets/datasets-allComplete.png)


## Ressources supplémentaires

* [Documentation sur les jeux de données](https://experienceleague.adobe.com/docs/experience-platform/catalog/datasets/overview.html?lang=fr)
* [Référence de l’API des jeux de données (faisant partie du service de catalogue)](https://www.adobe.io/experience-platform-apis/references/catalog/#tag/Datasets)

Maintenant que tous nos schémas, identités et jeux de données sont en place, nous pouvons [les activer pour Real-time Customer Profile ;](enable-profiles.md).
