---
title: Query Service - Power BI/Tableau
description: Query Service - Power BI/Tableau
kt: 5342
doc-type: tutorial
exl-id: c4e4f5f9-3962-4c8f-978d-059f764eee1c
source-git-commit: d9d9a38c1e160950ae755e352a54667c8a7b30f7
workflow-type: tm+mt
source-wordcount: '391'
ht-degree: 0%

---

# 5.1.5 Génération d’un jeu de données à partir d’une requête

## Objectif

Découvrez comment générer des jeux de données à partir de résultats de requête
Connecter directement Microsoft Power BI Desktop/Tableau à Query Service
Création d’un rapport dans Microsoft Power BI Desktop/Tableau Desktop

## Contexte

Une interface de ligne de commande pour interroger les données est passionnante, mais elle ne présente pas bien. Dans cette leçon, nous vous guiderons tout au long d’un processus recommandé pour savoir comment utiliser Microsoft Power BI Desktop/Tableau directement dans Query Service afin de créer des rapports visuels pour vos parties prenantes.

## Création d’un jeu de données à partir d’une requête SQL

La complexité de votre requête aura un impact sur le temps nécessaire à Query Service pour renvoyer les résultats. En outre, lors de l’interrogation directement à partir de la ligne de commande ou d’autres solutions telles que Microsoft Power BI/Tableau, Query Service est configuré avec un délai d’attente de 5 minutes (600 secondes). Et dans certains cas, ces solutions seront configurées avec des délais d’expiration plus courts. Pour exécuter des requêtes plus volumineuses et charger le temps nécessaire pour renvoyer les résultats, nous proposons une fonctionnalité de génération d’un jeu de données à partir des résultats de la requête. Cette fonctionnalité utilise la fonctionnalité SQL standard appelée Create Table As Select (CTAS). Il est disponible dans l’interface utilisateur de Platform à partir de la liste de requêtes et peut également être exécuté directement à partir de la ligne de commande avec PSQL.

Dans la précédente, vous avez remplacé **par votre propre ldap avant de l’exécuter dans PSQL.**

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

Vous recherchez l’instruction exécutée dans l’interface utilisateur de requête de Adobe Experience Platform en saisissant votre LDAP dans le champ de recherche :

Sélectionnez **Requêtes**, accédez à **Journal** et saisissez votre LDAP dans le champ de recherche.

![search-query-for-ctas.png](./images/searchqueryforctas.png)

Sélectionnez votre requête et cliquez sur **Exécuter en tant que CTAS**.

![search-query-for-ctas.png](./images/searchqueryforctasa.png)

Saisissez `--aepUserLdap-- Callcenter Interaction Analysis` comme nom et description du jeu de données, puis cliquez sur **Exécuter en tant que CTAS**.

![create-ctas-dataset.png](./images/createctasdataset.png)

Par conséquent, une nouvelle requête avec le statut **Envoyé** s’affiche.

![ctas-query-submit.png](./images/ctasquerysubmitted.png)

Une fois l’opération terminée, vous verrez une nouvelle entrée pour **Jeu de données créé** (vous devrez peut-être actualiser la page).

![ctas-dataset-created.png](./images/ctasdatasetcreated.png)

Dès que votre jeu de données est créé (ce qui peut prendre entre 5 et 10 minutes), vous pouvez poursuivre l’exercice.

Étape suivante - Option A : [5.1.6 Query Service et Power BI](./ex6.md)

Étape suivante - Option B : [5.1.7 Query Service et Tableau](./ex7.md)

[Revenir au module 5.1](./query-service.md)

[Revenir à tous les modules](../../../overview.md)
