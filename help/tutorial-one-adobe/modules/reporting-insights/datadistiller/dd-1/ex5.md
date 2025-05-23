---
title: Query Service - Power BI/Tableau
description: Query Service - Power BI/Tableau
kt: 5342
doc-type: tutorial
exl-id: 4c89fa24-44a5-4a9a-bb24-39ad4650c503
source-git-commit: 1e3a8d585503eddad4c642a3b13d2b5f7ddc9943
workflow-type: tm+mt
source-wordcount: '393'
ht-degree: 1%

---

# 2.1.5 Générer un jeu de données à partir d’une requête

## Objectif

Découvrez comment générer des jeux de données à partir des résultats de requête.
Connexion directe de Microsoft Power BI Desktop/Tableau à Query Service
Création d&#39;un rapport dans Microsoft Power BI Desktop/Tableau Desktop

## Contexte

Une interface de ligne de commande pour interroger les données est passionnante, mais elle ne se présente pas bien. Dans cette leçon, nous vous guiderons à travers un workflow recommandé pour savoir comment utiliser Microsoft Power BI Desktop/Tableau directement dans Query Service afin de créer des rapports visuels pour vos parties prenantes.

## Créer un jeu de données à partir d’une requête SQL

La complexité de votre requête aura une incidence sur le temps nécessaire au service de requête pour renvoyer les résultats. De plus, lors de l’interrogation directe à partir de la ligne de commande ou d’autres solutions telles que Microsoft Power BI/Tableau , Query Service est configuré avec un délai d’expiration de 5 minutes (600 secondes). Et dans certains cas, ces solutions seront configurées avec des délais plus courts. Pour exécuter des requêtes plus volumineuses et précharger le temps nécessaire au renvoi des résultats, nous proposons une fonctionnalité permettant de générer un jeu de données à partir des résultats de la requête. Cette fonction utilise la fonction SQL standard appelée Create Table As Select (CTAS). Il est disponible dans l’interface utilisateur de Platform à partir de la liste des requêtes et peut également être exécuté directement à partir de la ligne de commande avec PSQL.

Dans l&#39;exemple précédent, vous avez remplacé **saisissez votre nom** par votre propre ldap avant de l&#39;exécuter dans PSQL.

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
       l.--aepTenantId--.identification.core.crmId as crmid
from   demo_system_event_dataset_for_website_global_v1_1 e
      ,demo_system_event_dataset_for_call_center_global_v1_1 c
      ,demo_system_profile_dataset_for_crm_global_v1_1 l
where  e.--aepTenantId--.demoEnvironment.brandName IN ('Citi Signal')
and    e.web.webPageDetails.name in ('Cancel Service', 'Call Start')
and    e.--aepTenantId--.identification.core.ecid = c.--aepTenantId--.identification.core.ecid
and    l.--aepTenantId--.identification.core.ecid = e.--aepTenantId--.identification.core.ecid;
```

Accédez à l’interface utilisateur de Adobe Experience Platform - [https://experience.adobe.com/platform](https://experience.adobe.com/platform)

Vous rechercherez votre instruction exécutée dans l’interface utilisateur de requête de Adobe Experience Platform en saisissant votre ldap dans le champ de recherche :

Sélectionnez **Requêtes**, accédez à **Journal** et saisissez votre ldap dans le champ de recherche.

![search-query-for-ctas.png](./images/searchqueryforctas.png)

Sélectionnez votre requête et cliquez sur **Exécuter en tant que CTAS**.

![search-query-for-ctas.png](./images/searchqueryforctasa.png)

Saisissez `--aepUserLdap-- Callcenter Interaction Analysis` comme nom et description pour le jeu de données, puis cliquez sur **Exécuter en tant que CTAS**.

![create-ctas-dataset.png](./images/createctasdataset.png)

Par conséquent, une nouvelle requête avec un statut **Envoyée** s’affiche.

![ctas-query-submit.png](./images/ctasquerysubmitted.png)

Une fois l’opération terminée, une nouvelle entrée s’affiche pour **Jeu de données créé** (vous devrez peut-être actualiser la page).

![ctas-dataset-created.png](./images/ctasdatasetcreated.png)

Dès que votre jeu de données est créé (ce qui peut prendre entre 5 et 10 minutes), vous pouvez continuer l’exercice.

## Étapes suivantes

Accédez à l’option A : [2.1.6 Query Service et Power BI](./ex6.md){target="_blank"}

Accédez à l’option B : [2.1.7 Query Service et Tableau](./ex7.md){target="_blank"}

Revenez à [Query Service](./query-service.md){target="_blank"}

Revenir à [Tous les modules](./../../../../overview.md){target="_blank"}
