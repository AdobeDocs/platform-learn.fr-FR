---
title: Création d’un jeu de données
description: Création d’un jeu de données
role: Developer
level: Intermediate
recommendations: noDisplay,noCatalog
jira: KT-10447
hide: true
hidefromtoc: true
exl-id: 7705d292-a29c-4977-bcc6-f088a51713ea
source-git-commit: 90f7621536573f60ac6585404b1ac0e49cb08496
workflow-type: tm+mt
source-wordcount: '211'
ht-degree: 8%

---

# Création d’un jeu de données

Outre la description des données que vous enverrez dans Adobe Experience Platform, vous avez besoin d’un emplacement pour conserver les données. Dans Adobe Experience Platform, ces compartiments dans lesquels vous pouvez placer des données sont appelés jeux de données.

Pour créer un jeu de données, accédez au [!UICONTROL Jeux de données] dans Adobe Experience Platform.

![Vue Jeux de données](../../../assets/implementation-strategy/datasets-view.png)

Cliquez sur [!UICONTROL Création d’un jeu de données] dans le coin supérieur droit.

Pendant le processus de création du jeu de données, sélectionnez [!UICONTROL Création d’un jeu de données à partir d’un schéma] et sélectionnez [le schéma que vous avez créé précédemment ;](create-a-schema.md).

![Sélection de schéma](../../../assets/implementation-strategy/schema-selection.png)

Cliquez sur [!UICONTROL Suivant] et indiquez un nom et une description.

![Nom et description du jeu de données](../../../assets/implementation-strategy/dataset-name-description.png)

Cliquez sur [!UICONTROL Terminer]. Votre jeu de données a été créé et est prêt à recevoir des données.

Lorsque vous commencez à envoyer des données dans un jeu de données, Adobe Experience Platform vérifie que les données que vous essayez de placer dans le jeu de données sont conformes au schéma appliqué. Si les données ne sont pas conformes au schéma, elles sont rejetées et ne sont pas placées dans le jeu de données. Grâce à cette étape de validation, les consommateurs du jeu de données (produits d’Adobe, tiers ou votre propre société) peuvent avoir un certain niveau de certitude quant à la structure et la propreté des données du jeu de données.

Pour plus d’informations sur la création de jeux de données, voir [Guide de l’interface utilisateur des jeux de données](https://experienceleague.adobe.com/docs/experience-platform/catalog/datasets/user-guide.html?lang=fr).
