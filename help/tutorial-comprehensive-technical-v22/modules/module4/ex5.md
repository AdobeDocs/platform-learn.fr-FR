---
title: Query Service - Exploration du jeu de données avec Power BI
description: Query Service - Exploration du jeu de données avec Power BI
kt: 5342
audience: Data Engineer, Data Architect, Data Analyst, BI Expert
doc-type: tutorial
activity: develop
exl-id: 0f9e6719-056b-4858-8c86-04b3beaa950e
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '296'
ht-degree: 0%

---

# 4.5 Query Service et Power BI

Ouvrez Microsoft Power BI Desktop.

![start-power-bi.png](./images/start-power-bi.png)

Cliquez sur **Obtenir des données**.

![power-bi-get-data.png](./images/power-bi-get-data.png)

Rechercher **postgres** (1), sélectionnez **Postgres** (2) de la liste et **Connexion** (3).

![power-bi-connect-progress.png](./images/power-bi-connect-progress.png)

Accédez à Adobe Experience Platform, puis à **Requêtes** et à **Informations d’identification**.

![query-service-credentials.png](./images/query-service-credentials.png)

Dans la **Informations d’identification** dans Adobe Experience Platform, copiez la variable **Hôte** et collez-le dans le **Serveur** et copiez la variable **Base** et collez-le dans le **Base** dans PowerBI, puis cliquez sur OK (2).

>[!IMPORTANT]
>
>Veillez à inclure le port **:80** à la fin de la valeur Server, car Query Service n’utilise actuellement pas le port PostgreSQL par défaut 5432.

![power-bi-connect-server.png](./images/power-bi-connect-server.png)

Dans la boîte de dialogue suivante, indiquez le nom d’utilisateur et le mot de passe avec le nom d’utilisateur et le mot de passe figurant dans le champ **Informations d’identification** de requêtes dans Adobe Experience Platform.

![query-service-credentials.png](./images/query-service-credentials.png)

Dans la boîte de dialogue Navigator, placez votre **LDAP** dans le champ de recherche (1) pour localiser vos jeux de données CTAS et cochez la case en regard de chaque (2). Cliquez ensuite sur Charger (3).

![power-bi-load-churn-data.png](./images/power-bi-load-churn-data.png)

Assurez-vous que la variable **Rapport** (1) est sélectionné.

![power-bi-report-tab.png](./images/power-bi-report-tab.png)

Sélectionnez la carte (1) et une fois qu’elle a été ajoutée à la zone de travail de création de rapports, agrandissez la carte (2).

![power-bi-select-map.png](./images/power-bi-select-map.png)

Ensuite, nous devons définir les mesures et les dimensions. Pour ce faire, faites glisser les champs de la variable **fields** sur les espaces réservés correspondants (situés sous **visualisations**), comme indiqué ci-dessous :

![power-bi-drag-lat-lon.png](./images/power-bi-drag-lat-lon.png)

Comme mesure, nous utiliserons un comptage de **customerId**. Faites glisser le **crmid** du champ **fields** dans la section **Taille** espace réservé :

![power-bi-drag-crmid.png](./images/power-bi-drag-crmid.png)

Pour finir, **callTopic** analysez, faisons glisser la balise **callTopic** sur le champ **Filtres au niveau de la page** espace réservé (vous devrez peut-être faire défiler l’écran **visualisations** );

![power-bi-drag-calltopic.png](./images/power-bi-drag-calltopic.png)

Sélectionner/désélectionner **calltopics** pour enquêter :

![power-bi-report-select-calltopic.png](./images/power-bi-report-select-calltopic.png)

Vous avez maintenant terminé cet exercice.

Étape suivante : [4.7 API Query Service](./ex7.md)

[Revenir au module 4](./query-service.md)

[Revenir à tous les modules](../../overview.md)
