---
title: Query Service - Power BI/Tableau
description: Query Service - Power BI/Tableau
kt: 5342
audience: Data Engineer, Data Architect, Data Analyst, BI Expert
doc-type: tutorial
activity: develop
exl-id: 11525d05-1c19-4d41-8f47-4feb3e8aed66
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '385'
ht-degree: 1%

---

# 4.4 Génération d’un jeu de données à partir d’une requête

## Objectif

Découvrez comment générer des jeux de données à partir des résultats de la requête Connectez Microsoft Power BI Desktop/Tableau directement au service de requête Création d’un rapport dans Microsoft Power BI Bureau/Tableau Bureau

## Contexte de la leçon

Une interface de ligne de commande pour interroger les données est passionnante, mais elle ne présente pas bien. Dans cette leçon, nous vous guiderons tout au long d’un processus recommandé pour savoir comment utiliser Microsoft Power BI Desktop/Tableau directement dans Query Service afin de créer des rapports visuels pour vos parties prenantes.

## 4.4.1 Création d’un jeu de données à partir d’une requête SQL

La complexité de votre requête aura un impact sur le temps nécessaire à Query Service pour renvoyer les résultats. En outre, lors de l’interrogation directement à partir de la ligne de commande ou d’autres solutions comme Microsoft Power BI/Tableau, Query Service est configuré avec un délai d’attente de 5 minutes (600 secondes). Et dans certains cas, ces solutions seront configurées avec des délais d’expiration plus courts. Pour exécuter des requêtes plus volumineuses et charger le temps nécessaire pour renvoyer les résultats, nous proposons une fonctionnalité de génération d’un jeu de données à partir des résultats de la requête. Cette fonctionnalité utilise la fonctionnalité SQL standard appelée Create Table As Select (CTAS). Il est disponible dans l’interface utilisateur de Platform à partir de la liste de requêtes et peut également être exécuté directement à partir de la ligne de commande avec PSQL.

Dans le précédent, vous avez remplacé **saisissez votre nom** avec votre propre ldap avant de l’exécuter dans PSQL.

```sql
select /* enter your name */
       e.--aepTenantId--.identification.core.ecid as ecid,
       e.placeContext.geo.city as city,
       e.placeContext.geo._schema.latitude latitude,
       e.placeContext.geo._schema.longitude longitude,
       e.placeContext.geo.countryCode as countrycode,
       c.--aepTenantId--.interactionDetails.core.callCenterAgent.callFeeling as callFeeling,
       c.--aepTenantId--.interactionDetails.core.callCenterAgent.callTopic as callTopic,
       c.--aepTenantId--.interactionDetails.core.callCenterAgent.callContractCancelled as contractCancelled,
       l.--aepTenantId--.loyaltyDetails.level as loyaltystatus,
       l.--aepTenantId--.loyaltyDetails.points as loyaltypoints,
       l.--aepTenantId--.identification.core.loyaltyId as crmid
from   demo_system_event_dataset_for_website_global_v1_1 e
      ,demo_system_event_dataset_for_call_center_global_v1_1 c
      ,demo_system_profile_dataset_for_loyalty_global_v1_1 l
where  e.--aepTenantId--.demoEnvironment.brandName IN ('Luma Telco', 'Citi Signal')
and    e.web.webPageDetails.name in ('Cancel Service', 'Call Start')
and    e.--aepTenantId--.identification.core.ecid = c.--aepTenantId--.identification.core.ecid
and    l.--aepTenantId--.identification.core.ecid = e.--aepTenantId--.identification.core.ecid;
```

Accédez à l’interface utilisateur de Adobe Experience Platform - [https://experience.adobe.com/platform](https://experience.adobe.com/platform)

Vous recherchez l’instruction exécutée dans l’interface utilisateur de requête de Adobe Experience Platform en saisissant votre LDAP dans le champ de recherche :

Sélectionner **Requêtes**, accédez à **Journal** et saisissez votre ldap dans le champ de recherche.

![search-query-for-ctas.png](./images/search-query-for-ctas.png)

Sélectionnez votre requête, puis cliquez sur **Jeu de données de sortie**.

![search-query-for-ctas.png](./images/search-query-for-ctasa.png)

Entrée `--demoProfileLdap-- Callcenter Interaction Analysis` comme nom et description du jeu de données, puis appuyez sur la touche **Exécuter la requête** button

![create-ctas-dataset.png](./images/create-ctas-dataset.png)

Par conséquent, une nouvelle requête avec un état s’affiche. **Envoyé**.

![ctas-query-submit.png](./images/ctas-query-submitted.png)

Une fois l’opération terminée, une nouvelle entrée pour **Jeu de données créé** (vous devrez peut-être actualiser la page).

![ctas-dataset-created.png](./images/ctas-dataset-created.png)

Dès que votre jeu de données est créé (ce qui peut prendre entre 5 et 10 minutes), vous pouvez poursuivre l’exercice.

Étape suivante - Option A : [4.5 Query Service et Power BI](./ex5.md)

Étape suivante - Option B : [4.6 Query Service et Tableau](./ex6.md)

[Revenir au module 4](./query-service.md)

[Revenir à tous les modules](../../overview.md)
