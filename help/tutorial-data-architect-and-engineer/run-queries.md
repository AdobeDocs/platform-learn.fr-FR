---
title: Exécution de requêtes
seo-title: Run queries | Getting Started with Adobe Experience Platform for Data Architects and Data Engineers
breadcrumb-title: Exécution de requêtes
description: Dans cette leçon, vous apprendrez à configurer, écrire et exécuter des requêtes pour valider les données que vous avez ingérées.
role: Data Architect, Data Engineer
feature: Queries
jira: KT-4348
thumbnail: 4348-run-queries.jpg
exl-id: a37531cb-96ad-4547-86af-84f7ed65f019
source-git-commit: 00ef0f40fb3d82f0c06428a35c0e402f46ab6774
workflow-type: tm+mt
source-wordcount: '314'
ht-degree: 1%

---

# Exécution de requêtes

<!-- 15 min-->
Dans cette leçon, vous apprendrez à configurer, écrire et exécuter des requêtes pour valider les données que vous avez ingérées.

Adobe Experience Platform Query Service vous aide à comprendre vos données en vous permettant d’utiliser le langage SQL standard pour interroger des données dans Platform. Grâce à Query Service, vous pouvez joindre n’importe quel jeu de données dans le lac de données et capturer les résultats de la requête sous la forme d’un nouveau jeu de données à utiliser dans les rapports, l’apprentissage automatique ou pour ingestion dans Real-Time Customer Profile.

**Les architectes de données** et les **ingénieurs de données** devront utiliser le service de requête en dehors de ce tutoriel.

Avant de commencer les exercices, regardez cette courte vidéo pour en savoir plus sur Query Service :
>[!VIDEO](https://video.tv.adobe.com/v/29795?learn=on)

## Autorisations requises

Dans la leçon [Configurer les autorisations](configure-permissions.md) , vous configurez tous les contrôles d’accès requis pour terminer cette leçon.

<!-- Settings > **[!UICONTROL Services]** > **[!UICONTROL Query Service]**
* Permission items Data Management > **[!UICONTROL View Datasets]** and  **[!UICONTROL Manage Datasets]**
* Permission item Sandboxes > `Luma Tutorial`
* User-role access to the `Luma Tutorial Platform` product profile
-->

## Requêtes simples

Commençons par quelques requêtes simples :

1. Dans l’interface utilisateur de Platform, accédez à **Requêtes** dans le volet de navigation de gauche.
1. Sélectionnez le bouton **Créer une requête** en haut à droite pour ouvrir une zone de texte afin d’exécuter et d’exécuter des requêtes.
1. Saisissez la requête suivante dans l’éditeur, puis appuyez sur Maj+Entrée ou Maj+Retour pour exécuter la requête.

   ```
   SHOW TABLES
   ```

1. La liste des tableaux disponibles s’affiche.

   ![requête SHOW TABLE](assets/queries-showTables.png)


1. Essayez maintenant cette requête, en remplaçant `_techmarketingdemos` par votre propre espace de noms du client, qui, si vous vous souvenez, est visible dans vos schémas.

   ```
   SELECT person.name.lastName,loyalty.tier
   FROM luma_loyalty_dataset
   WHERE loyalty.tier ='gold'
   ```

   ![SELECT data from the loyalty dataset](assets/queries-loyaltySelect.png)

1. En cas d’erreur, des messages détaillés s’affichent dans l’onglet **[!UICONTROL Console]**, comme illustré ci-dessous.
   ![Erreur dans la requête](assets/queries-error.png)

1. Avec votre requête réussie, **[!UICONTROL Name]** it `Luma Gold Level Customers`
1. Sélectionnez le bouton **[!UICONTROL Enregistrer]**
   ![Enregistrement de la requête](assets/queries-loyaltySelect-save.png)


<!--SELECT COUNT(DISTINCT (_techmarketingdemos.systemIdentifier.loyaltyId)) FROM luma_loyalty_dataset 


SELECT _techmarketingdemos.systemIdentifier.loyaltyId, COUNT(_techmarketingdemos.systemIdentifier.loyaltyId)
FROM luma_loyalty_dataset 
GROUP BY _techmarketingdemos.systemIdentifier.loyaltyId
HAVING COUNT(_techmarketingdemos.systemIdentifier.loyaltyId) > 1;-->

## Exercices supplémentaires

D’autres exercices Query Service seront ajoutés au tutoriel ultérieurement.
<!--
## Join Datasets

In this exercise, we will join two datasets `Luma Loyalty Dataset` and `Luma Offline Purchase` to get list of gold customers who have spend over $500 dollars in one purchase.

1. Create a new query
1. Copy and paste following query in query editor and execute, again replacing `_techmarketingdemos` with your own tenant namespace
    
    ```
    SELECT DISTINCT lopd.commerce.order.purchaseID as PurchaseId ,
        lld.person.name.firstName as LastName ,
        lld.person.name.lastName as LastName ,
        lopd.personalEmail.address as email,
        lopd.commerce.order.priceTotal as Total

    FROM luma_loyalty_dataset lld
    JOIN luma_offline_purchase_event_dataset lopd
    ON lopd._techmarketingdemos.systemIdentifier.loyaltyId = lld._techmarketingdemos.systemIdentifier.loyaltyId

    WHERE lld._techmarketingdemos.loyalty.level ='gold' AND lopd.commerce.order.priceTotal >500;
    ```

1. You should get list of Gold Customers who have spend over $500 in single purchase.

## Output datasets

1. Select on Output Dataset button
1. Provide name and description to the dataset
1. Save.
1. Go to **Datasets** under **Data Management** to find new dataset created.

-->
<!--Add content for Adobe Defined Functions-->

## Ressources supplémentaires

* [Documentation de Query Service](https://experienceleague.adobe.com/docs/experience-platform/query/home.html?lang=fr)
* [Référence de l’API Query Service](https://www.adobe.io/experience-platform-apis/references/query-service/)

Et maintenant, pour la dernière leçon pratique, [création de segments](build-segments.md) !
