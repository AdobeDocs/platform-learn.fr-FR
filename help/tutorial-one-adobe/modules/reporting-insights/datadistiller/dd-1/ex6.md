---
title: Query Service - Explorer le jeu de données avec Power BI
description: Query Service - Explorer le jeu de données avec Power BI
kt: 5342
doc-type: tutorial
exl-id: f1125d91-2fe6-456c-9d4a-802e3f288fc0
source-git-commit: 1e3a8d585503eddad4c642a3b13d2b5f7ddc9943
workflow-type: tm+mt
source-wordcount: '315'
ht-degree: 0%

---

# 2.1.6 Query Service et Power BI

Ouvrez Microsoft Power BI Desktop.

![start-power-bi.png](./images/startpowerbi.png)

Cliquez sur **Obtenir des données**.

![power-bi-get-data.png](./images/powerbigetdata.png)

Recherchez **postgres** (1), sélectionnez **Postgres** (2) dans la liste et **Connect** (3).

![power-bi-connect-progress.png](./images/powerbiconnectprogress.png)

Accédez à Adobe Experience Platform, à **Requêtes** et à **Informations d’identification**.

![query-service-credentials.png](./images/queryservicecredentials.png)

Sur la page **Informations d’identification** de Adobe Experience Platform, copiez le **Hôte** et collez-le dans le champ **Serveur**, copiez le **Base de données** et collez-le dans le champ **Base de données** de PowerBI, puis cliquez sur OK (2).

>[!IMPORTANT]
>
>Veillez à inclure le port **:80** à la fin de la valeur Serveur , car Query Service n’utilise actuellement pas le port PostgreSQL par défaut 5432.

![power-bi-connect-server.png](./images/powerbiconnectserver.png)

Dans la boîte de dialogue suivante, indiquez le nom d’utilisateur et le mot de passe avec vos nom d’utilisateur et mot de passe figurant dans les **Informations d’identification** des requêtes dans Adobe Experience Platform.

![query-service-credentials.png](./images/queryservicecredentials.png)

Dans la boîte de dialogue Navigateur, placez votre **LDAP** dans le champ de recherche (1) pour localiser vos jeux de données CTAS et cochez la case en regard de chacun (2). Cliquez ensuite sur Charger (3).

![power-bi-load-churn-data.png](./images/powerbiloadchurndata.png)

Assurez-vous que l’onglet **Rapport** (1) est sélectionné.

![power-bi-report-tab.png](./images/powerbireporttab.png)

Sélectionnez la carte (1) et, après l’avoir ajoutée à la zone de travail de création de rapports, agrandissez la carte (2).

![power-bi-select-map.png](./images/powerbiselectmap.png)

Vous devez ensuite définir les mesures et les dimensions en faisant glisser les champs de la section **champs** vers les espaces réservés correspondants (situés sous **visualisations**), comme indiqué ci-dessous :

![power-bi-drag-lat-lon.png](./images/powerbidraglatlon.png)

Comme mesure, nous utiliserons un nombre de **customerId**. Faites glisser le champ **crmid** de la section **fields** vers l’espace réservé **Size** :

![power-bi-drag-crmid.png](./images/powerbidragcrmid.png)

Enfin, pour effectuer une analyse **callTopic**, faisons glisser le champ **callTopic** sur l&#39;espace réservé **Filtres au niveau de la page** (vous devrez peut-être faire défiler la section **visualisations**) ;

![power-bi-drag-calltopic.png](./images/powerbidragcalltopic.png)

Sélectionnez/désélectionnez **callTopics** pour examiner les éléments suivants :

![power-bi-report-select-calltopic.png](./images/powerbireportselectcalltopic.png)

Vous avez maintenant terminé cet exercice.

## Étapes suivantes

Accédez à l’API [2.1.8 Query Service](./ex8.md){target="_blank"}

Revenez à [Query Service](./query-service.md){target="_blank"}

Revenir à [Tous les modules](./../../../../overview.md){target="_blank"}
