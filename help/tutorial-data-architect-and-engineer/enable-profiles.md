---
title: Activation des profils client en temps réel
seo-title: Enable Real-Time Customer Profiles | Getting Started with Adobe Experience Platform for Data Architects and Data Engineers
breadcrumb-title: Activation des profils client en temps réel
description: Dans cette leçon, vous allez activer vos schémas et jeux de données pour Real-time Customer Profile.
role: Data Architect
feature: Profiles
jira: KT-4348
thumbnail: 4348-enable-profiles.jpg
exl-id: b05f1af1-a599-42f2-8546-77453a578b92
source-git-commit: 00ef0f40fb3d82f0c06428a35c0e402f46ab6774
workflow-type: tm+mt
source-wordcount: '1089'
ht-degree: 2%

---

# Activation des profils client en temps réel

<!-- 15min-->
Dans cette leçon, vous allez activer vos schémas et jeux de données pour Real-time Customer Profile.

Bon, j&#39;ai menti en disant que la leçon sur les jeux de données était la plus courte de ce tutoriel - celle-ci devrait prendre encore moins de temps ! Littéralement tout ce que vous allez faire c&#39;est retourner un tas de baskets. Mais ce qui se passe lorsque vous retournez ces bascules est _vraiment_ important, je voulais donc y consacrer une page entière.

Real-Time Customer Profile offre une vue d’ensemble de chaque client qui combine des données issues de plusieurs canaux, notamment des données en ligne, hors ligne, CRM et tierces. Le profil vous permet de consolider vos diverses données client en une vue unifiée offrant un compte horodaté et exploitable de chaque interaction client.

Aussi incroyable que cela paraisse, vous n&#39;avez pas besoin d&#39;activer *toutes vos données* pour le profil. En fait, vous ne devez activer que les données dont vous avez besoin pour les cas d’utilisation de l’activation. Activez les données que vous souhaitez utiliser pour les cas d’utilisation marketing, les intégrations du centre d’appels, etc., où vous avez besoin d’un accès rapide à un profil client robuste. Si vous chargez des données uniquement à des fins d’analyse, elles ne doivent probablement pas être activées pour le profil.

Il existe d’importantes [barrières de sécurité pour les données de profil client en temps réel](https://experienceleague.adobe.com/docs/experience-platform/profile/guardrails.html?lang=en) que vous devez examiner lors du choix de vos propres données à activer pour le profil.

<!--is this accurate. Are there other considerations to point out? -->

**Les architectes de données** devront activer Real-time Customer Profile en dehors de ce tutoriel.

Avant de commencer les exercices, regardez cette courte vidéo pour en savoir plus sur Real-time Customer Profile :
>[!VIDEO](https://video.tv.adobe.com/v/27251?learn=on)

## Autorisations requises

Dans la leçon [Configurer les autorisations](configure-permissions.md) , vous configurez tous les contrôles d’accès requis pour terminer cette leçon.


<!--* Permission items **[!UICONTROL Data Modeling]** > **[!UICONTROL View Schemas]** and **[!UICONTROL Manage Schemas]**
* Permission items **[!UICONTROL Data Management]** > **[!UICONTROL View Datasets]** and **[!UICONTROL Manage Datasets]**
* Permission item **[!UICONTROL Sandboxes]** > `Luma Tutorial`
* User-role access to the `Luma Tutorial Platform` product profile
* Developer-role access to the `Luma Tutorial Platform` product profile (for API)
-->

## Activation des schémas pour Real-time Customer Profile à l’aide de l’interface utilisateur de Platform

Commençons par la tâche simple d’activation d’un schéma :

1. Dans l’interface utilisateur de Platform, ouvrez le **schéma de fidélité Luma**
1. Dans **[!UICONTROL Propriétés du schéma]**, basculez le commutateur **Profile**
1. Dans le modal de confirmation, appuyez sur le bouton **[!UICONTROL Activer]** pour confirmer.
1. Sélectionnez le bouton **[!UICONTROL Enregistrer]** pour enregistrer vos modifications.

   >[!IMPORTANT]
   >
   >Une fois qu’un schéma est activé pour Profile, il ne peut pas être désactivé ni supprimé. De plus, les champs ne peuvent plus être supprimés du schéma après ce point. Il est important de tenir compte de ces implications ultérieurement lorsque vous travaillez avec vos propres données dans votre environnement de production. Vous devriez utiliser un environnement de test de développement dans ce tutoriel, qui peut être supprimé à tout moment.
   >
   >Dans l’environnement contrôlé de ce tutoriel, vous activerez vos schémas et jeux de données pour profile, _avant d’ingérer des données_. Lorsque vous utilisez vos propres données, nous vous recommandons de procéder dans l’ordre suivant :
   >
   > 1. Tout d’abord, ingérez des données dans vos jeux de données.
   > 1. Résolvez tous les problèmes qui se produisent pendant le processus d’ingestion des données (par exemple, les problèmes de validation des données ou de mappage).
   > 1. Activation des jeux de données et des schémas pour Profile
   > 1. Réingérer les données


   ![Basculement du profil](assets/profile-loyalty-enableSchema.png)

Facile, n&#39;est-ce pas ? Répétez les étapes ci-dessus pour ces autres schémas :

1. Schéma du catalogue de produits Luma
1. Schéma d’événements d’achat hors ligne Luma
1. Schéma des événements web Luma (dans le modal de confirmation, cochez la case &quot;Les données de ce schéma contiendront une identité principale dans le champ identityMap&quot;.

## Activation des schémas pour Real-time Customer Profile à l’aide de l’API Platform

Il est maintenant temps d’activer le `Luma CRM Schema` avec l’API. Si vous souhaitez ignorer cet exercice et l’activer simplement dans l’interface utilisateur, allez-y.

### Obtention du meta:altId du schéma

Commençons par obtenir le `meta:altId` de `Luma CRM Schema` :

1. Ouvrez [!DNL Postman]
1. Si vous ne disposez pas d’un jeton d’accès, ouvrez la requête **[!DNL OAuth: Request Access Token]** et sélectionnez **Envoyer** pour demander un nouveau jeton d’accès, comme vous l’avez fait dans la leçon [!DNL Postman].
1. Ouvrez la requête **[!DNL Schema Registry API > Schemas > Retrieve a list of schemas within the specified container.]**
1. Sélectionnez le bouton **Send**
1. Vous devriez obtenir une réponse 200
1. Recherchez dans la réponse de l’élément `Luma CRM Schema` et copiez la valeur `meta:altId`.
   ![Copiez le meta:altIid](assets/profile-crm-getMetaAltId.png)

### Activation du schéma

Maintenant que nous avons le meta:altId du schéma, nous pouvons l&#39;activer pour le profil :

1. Ouvrez la requête **[!DNL Schema Registry API > Schemas > Update one or more attributes of a custom schema specified by ID.]**
1. Dans **Params**, collez votre valeur `meta:altId` comme valeur de paramètre `SCHEMA_ID`
1. Dans l’onglet **Body** , collez le code suivant :

   ```json
   [{
       "op": "add",
       "path": "/meta:immutableTags",
       "value": ["union"]
   }]
   ```

1. Sélectionnez le bouton **Send**
1. Vous devriez obtenir une réponse 200

   ![Activez le schéma CRM pour le profil avec votre méta:altIid personnalisé utilisé comme paramètre SCHEMA_ID](assets/profile-crm-enableProfile.png)

Vous devriez être en mesure de voir dans l’interface utilisateur que les cinq schémas sont activés pour Profile (vous devrez peut-être MAJ-Recharger pour voir que `Luma CRM Schema` est activé) :
![ Tous les schémas activés](assets/profile-allSchemasEnabled.png)


## Activation des jeux de données pour Real-time Customer Profile à l’aide de l’interface utilisateur de Platform

Les jeux de données doivent également être activés pour Profile, et le processus est encore plus simple :

1. Dans l’interface utilisateur de Platform, ouvrez le `Luma Loyalty Dataset`
1. Basculer le commutateur **[!UICONTROL Profile]**
1. Dans le modal de confirmation, appuyez sur le bouton **[!UICONTROL Activer]** pour confirmer.

   ![ Basculement des profils](assets/profile-loyalty-enableDataset.png)

Répétez les étapes ci-dessus pour ces autres jeux de données :

1. Jeu de données du catalogue de produits Luma
1. Jeu de données des événements d’achat hors ligne Luma
1. Jeu de données des événements web Luma

>[!NOTE]
>
>Contrairement aux schémas, vous pouvez désactiver les jeux de données de Profile, mais toutes les données précédemment ingérées resteront dans Profile.

## Activation des jeux de données pour Real-time Customer Profile à l’aide de l’API Platform

Vous allez maintenant activer un jeu de données pour Profile à l’aide de l’API. Encore une fois, si vous souhaitez l’activer via l’interface utilisateur à l’aide de la méthode ci-dessus, c’est également très bien.

### Obtention de l’identifiant du jeu de données

Tout d&#39;abord, nous devons obtenir le `id` de `Luma CRM Dataset` :

1. Ouvrez [!DNL Postman]
1. Si vous ne disposez pas d’un jeton d’accès, ouvrez la requête **[!DNL OAuth: Request Access Token]** et sélectionnez **Envoyer** pour demander un nouveau jeton d’accès, comme vous l’avez fait dans la leçon [!DNL Postman].
1. Ouvrez la requête **[!DNL Catalog Service API > Datasets > Retrieve a list of datasets.]**
1. Sélectionnez le bouton **Send**
1. Vous devriez obtenir une réponse 200
1. Recherchez dans la réponse de l’élément `Luma CRM Dataset` et copiez l’identifiant :
   ![Copiez l’id](assets/profile-crm-copyDatasetId.png)

### Activer le jeu de données

Maintenant que nous disposons de l’identifiant du jeu de données, nous pouvons l’activer pour le profil :

1. Ouvrez la requête **[!DNL Catalog Service API > Datasets > Update one or more attributes of a dataset specified by ID.]**
1. Dans **Params**, mettez à jour la valeur `DATASET_ID` en fonction de vos besoins.
1. Dans l’onglet **Body**, collez le code suivant. Notez que les deux premières valeurs sont des balises préexistantes qui sont visibles dans la réponse précédente. Ils doivent être inclus dans le corps, en plus des deux nouvelles balises que nous ajoutons :

   ```json
   {
       "tags":{
           "adobe/pqs/table":["luma_crm_dataset"],
           "adobe/siphon/table/format":["parquet"],
           "unifiedProfile":["enabled:true"],
           "unifiedIdentity":["enabled:true"]
           }
   }
   ```

1. Sélectionnez le bouton **Send**
1. Vous devriez obtenir une réponse 200

   ![Activez le jeu de données CRM pour le profil, en veillant à utiliser votre identifiant de jeu de données personnalisé comme paramètre DATASET_ID](assets/profile-crm-enableDataset.png)

Vous pouvez également confirmer que l’interface utilisateur affiche le jeu de données activé :
![Confirmer](assets/profile-crm-confirmEnabled.png)

>[!IMPORTANT]
>
> Si vous ingérez des données avant d’activer le schéma et le jeu de données pour le profil, vous devrez réingérer ces données par la suite.

## Ressources supplémentaires

* [ Documentation sur Real-Time Customer Profile ](https://experienceleague.adobe.com/docs/experience-platform/profile/home.html?lang=fr)
* [Référence de l’API Real-Time Customer Profile](https://www.adobe.io/experience-platform-apis/references/profile/)


**Les ingénieurs de données** doivent continuer la leçon [Abonner aux événements d’ingestion de données](subscribe-to-data-ingestion-events.md) .
**Les architectes de données** _peuvent passer à l’étape_ et accéder à la [leçon sur l’ingestion par lots](ingest-batch-data.md).
