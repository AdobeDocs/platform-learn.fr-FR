---
title: Création de jeux de données
seo-title: Create datasets | Getting Started with Adobe Experience Platform for Data Architects and Data Engineers
breadcrumb-title: Création de jeux de données
description: Dans cette leçon, vous allez créer des jeux de données pour recevoir vos données.
role: Data Architect, Data Engineer
feature: Data Management
jira: KT-4348
thumbnail: 4348-create-datasets.jpg
exl-id: 80227af7-4976-4fd2-b1d4-b26bc4626fa0
source-git-commit: 00ef0f40fb3d82f0c06428a35c0e402f46ab6774
workflow-type: tm+mt
source-wordcount: '547'
ht-degree: 9%

---

# Création de jeux de données

<!--15min-->

Dans cette leçon, vous allez créer des jeux de données pour recevoir vos données. Vous serez heureux de savoir qu’il s’agit de la leçon la plus courte du tutoriel !

Toutes les données correctement ingérées dans Adobe Experience Platform sont conservées en tant que jeux de données dans le lac de données. Un jeu de données est une structure de stockage et de gestion pour la collecte de données, généralement sous la forme d’un tableau, qui contient un schéma (des colonnes) et des champs (des lignes). Les jeux de données contiennent également des métadonnées qui décrivent divers aspects des données stockées.

**Les architectes de données** devront créer des jeux de données en dehors de ce tutoriel.

Avant de commencer les exercices, regardez cette courte vidéo pour en savoir plus sur les jeux de données :
>[!VIDEO](https://video.tv.adobe.com/v/27269?learn=on)

## Autorisations requises

Dans la leçon [Configurer les autorisations](configure-permissions.md) , vous configurez tous les contrôles d’accès requis pour terminer cette leçon.

<!--
* Permission items **[!UICONTROL Data Management]** > **[!UICONTROL View Datasets]** and **[!UICONTROL Manage Datasets]**
* Permission item **[!UICONTROL Sandboxes]** > `Luma Tutorial`
* User-role access to the `Luma Tutorial Platform` product profile
* Developer-role access to the `Luma Tutorial Platform` product profile (for API)
-->

## Création de jeux de données dans l’interface utilisateur

Au cours de cet exercice, nous allons créer des jeux de données dans l’interface utilisateur. Commençons par les données de fidélité :

1. Accédez à **[!UICONTROL Jeux de données]** dans la navigation de gauche de l’interface utilisateur de Platform.
1. Sélectionnez le bouton **[!UICONTROL Créer un jeu de données]**
   ![Création d’un jeu de données](assets/datasets-createDataset.png)

1. Sur l’écran suivant, sélectionnez **Créer un jeu de données à partir du schéma**
1. Sur l’écran suivant, sélectionnez votre `Luma Loyalty Schema`, puis cliquez sur le bouton **[!UICONTROL Suivant]**
   ![Sélectionner le jeu de données](assets/datasets-selectSchema.png)

1. Nommez le jeu de données `Luma Loyalty Dataset` et sélectionnez le bouton **[!UICONTROL Terminer]**
   ![ Nommez le jeu de données ](assets/datasets-nameDataset.png)
1. Une fois le jeu de données enregistré, vous accédez à un écran comme celui-ci :
   ![Jeu de données créé](assets/datasets-created.png)

Vous avez terminé. Je vous ai dit que ça allait être rapide. Créez ces autres jeux de données en suivant les mêmes étapes :

1. `Luma Offline Purchase Events Dataset` pour votre `Luma Offline Purchase Events Schema`
1. `Luma Web Events Dataset` pour votre `Luma Web Events Schema`
1. `Luma Product Catalog Dataset` pour votre `Luma Product Catalog Schema`


## Créer un jeu de données à l’aide d’une API

Créez maintenant le `Luma CRM Dataset` à l’aide de l’API.

>[!NOTE]
>
>Si vous souhaitez ignorer l’exercice d’API et créer le `Luma CRM Dataset` dans l’interface utilisateur qui convient. Nommez-le `Luma CRM Dataset` et utilisez le `Luma CRM Schema`.

### Obtention de l’identifiant du schéma à utiliser dans le jeu de données

Tout d&#39;abord, nous devons obtenir le `$id` de `Luma CRM Schema` :

1. Ouvrez [!DNL Postman]
1. Si vous ne disposez pas d’un jeton d’accès, ouvrez la requête **[!DNL OAuth: Request Access Token]** et sélectionnez **Envoyer** pour demander un nouveau jeton d’accès, comme vous l’avez fait dans la leçon [!DNL Postman].
1. Ouvrez la requête **[!DNL Schema Registry API > Schemas > Retrieve a list of schemas within the specified container.]**
1. Sélectionnez le bouton **Send**
1. Vous devriez obtenir une réponse 200
1. Recherchez dans la réponse de l’élément `Luma CRM Schema` et copiez la valeur `$id`.
   ![Copiez le $id](assets/dataset-crm-getSchemaId.png)

### Création du jeu de données

Vous pouvez maintenant créer le jeu de données :

1. Téléchargez [API Catalog Service.postman_collection.json](https://raw.githubusercontent.com/adobe/experience-platform-postman-samples/master/apis/experience-platform/Catalog%20Service%20API.postman_collection.json) dans votre dossier `Luma Tutorial Assets`.
1. Importez la collection dans [!DNL Postman]
1. Sélectionnez la requête **[!DNL Catalog Service API > Datasets > Create a new dataset.]**
1. Collez les éléments suivants en tant que **Body** de la requête, ***en remplaçant la valeur d’identifiant par la vôtre*** :

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

1. Sélectionnez le bouton **Send**
1. Vous devriez obtenir une réponse 201 Créée contenant l’identifiant de votre nouveau jeu de données !
   ![Jeu de données créé avec l’API, votre $id personnalisé utilisé dans le corps](assets/datasets-crm-created.png)

>[!TIP]
>
> Problèmes courants à l’origine de cette demande et correctifs probables :
>
> * `400: There was a problem retrieving xdm schema`. Assurez-vous d&#39;avoir remplacé l&#39;identifiant dans l&#39;exemple ci-dessus par l&#39;identifiant de votre propre `Luma CRM Schema`.
> * Aucun jeton d’authentification : exécutez la requête **OAuth: Request Access Token** pour générer un nouveau jeton
> * `401: Not Authorized to PUT/POST/PATCH/DELETE for this path : /global/schemas/` : Mettez à jour la variable d&#39;environnement **CONTAINER_ID** de `global` vers `tenant`
> * `403: PALM Access Denied. POST access is denied for this resource from access control` : Vérifiez vos autorisations utilisateur dans l’Admin Console


Vous pouvez revenir à l’écran **[!UICONTROL Jeux de données]** dans l’interface utilisateur de Platform. Vous pouvez vérifier la création réussie des cinq jeux de données !
![Cinq jeux de données terminés](assets/datasets-allComplete.png)


## Ressources supplémentaires

* [Documentation sur les jeux de données](https://experienceleague.adobe.com/docs/experience-platform/catalog/datasets/overview.html?lang=fr)
* [Référence de l’API des jeux de données (partie du service de catalogue)](https://www.adobe.io/experience-platform-apis/references/catalog/#tag/Datasets)

Maintenant que tous nos schémas, identités et jeux de données sont en place, nous pouvons [les activer pour Real-time Customer Profile](enable-profiles.md).
