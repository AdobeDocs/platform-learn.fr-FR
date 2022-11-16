---
title: Création d’un jeu de données
description: Création d’un jeu de données
exl-id: 19a60087-2f78-4510-b127-b1007a6b7a56
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '308'
ht-degree: 2%

---

# Création d’un jeu de données

Outre la description des données que vous envoyez dans Adobe Experience Platform, vous avez besoin d’un emplacement pour conserver les données. Dans Adobe Experience Platform, ces compartiments dans lesquels vous pouvez placer des données sont appelés jeux de données.

>[!NOTE]
>
>Les jeux de données ne sont pas requis si vous utilisez uniquement le SDK Web de Platform pour envoyer des données à Adobe Analytics, Adobe Target et Adobe Audience Manager ou si vous utilisez le transfert d’événements. Si vous utilisez uniquement le SDK Web à ces fins, vous pouvez ignorer cette page du tutoriel.

1. Sélectionner **[!UICONTROL Jeux de données]** under [!UICONTROL Data Management] dans le menu de gauche de Adobe Experience Platform.
1. Sélectionnez ensuite le **[!UICONTROL Création d’un jeu de données]** dans le coin supérieur droit.
   ![Vue Jeux de données](../assets/datasets-view.png)

## Création d’un jeu de données à partir d’un schéma

1. Dans la [!UICONTROL Workflow] , sélectionnez la première mosaïque, **[!UICONTROL Création d’un jeu de données à partir d’un schéma]**.
1. Recherchez le [le schéma que vous avez créé précédemment ;](create-a-schema.md) et sélectionnez-le.
   ![Sélection de schéma](../assets/schema-selection.png)
1. Sélectionner **[!UICONTROL Suivant]** et indiquez un nom et une description.
   ![Nom et description du jeu de données](../assets/dataset-name-description.png)
1. Sélectionner **[!UICONTROL Terminer]**. Votre jeu de données a été créé et est prêt à recevoir des données.

Lorsque vous commencez à envoyer des données dans un jeu de données, Adobe Experience Platform valide la conformité des données que vous tentez de placer dans le jeu de données au schéma appliqué. Si les données ne sont pas conformes au schéma, elles sont rejetées et ne sont pas placées dans le jeu de données. Grâce à cette étape de validation, les consommateurs du jeu de données (produits d’Adobe, tiers ou votre propre société) peuvent avoir un certain niveau de certitude quant à la structure et la propreté des données du jeu de données.

Pour plus d’informations sur la création de jeux de données, voir [Création de jeux de données et ingestion de données](/help/platform/data-ingestion/create-datasets-and-ingest-data.md).

[Suivant : ](create-a-datastream.md)

>[!NOTE]
>
>Merci d’avoir consacré votre temps à l’apprentissage de la collecte de données. Si vous avez des questions, souhaitez partager des commentaires généraux ou avez des suggestions sur le contenu futur, partagez-les à ce sujet. [Article de discussion de la communauté Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-use-adobe-experience-platform-data/m-p/543877)

