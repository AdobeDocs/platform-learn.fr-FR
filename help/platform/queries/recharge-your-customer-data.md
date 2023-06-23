---
title: Rechargez vos données client pour offrir des expériences d’électrification
description: Découvrez comment atténuer l’impact de données de mauvaise qualité, réduire le temps à évaluer et multiplier le retour sur investissement en utilisant les mêmes données pour une multitude de cas d’utilisation.
role: Data Engineer, Data Architect, Developer
feature: Queries
jira: KT-10323
thumbnail: 342533.jpeg
exl-id: 30574cc5-66fa-4ab8-83ed-7af710294dbf
source-git-commit: 90f7621536573f60ac6585404b1ac0e49cb08496
workflow-type: tm+mt
source-wordcount: '172'
ht-degree: 3%

---

# Rechargez vos données client pour offrir des expériences d’électrification

Les données omnicanal sont un ingrédient essentiel pour alimenter les profils clients exploitables utilisés par les marketeurs pour orchestrer l’activation et mesurer les parcours client qui en résultent. Toutefois, les entreprises doivent relever des défis pour gérer la qualité, l’échelle et la variété de ces données. Elles nécessitent des solutions rationalisées pour atténuer l’impact de données de mauvaise qualité, réduire le temps à évaluer et multiplier le retour sur investissement en utilisant les mêmes données pour une multitude de cas d’utilisation.

Cette vidéo explore :

* Fonctionnalités de préparation des données Adobe Experience Platform que vous pouvez exploiter
* Augmentation du retour sur investissement d’Adobe Real-Time CDP, Adobe Journey Optimizer et Customer Journey Analytics

>[!VIDEO](https://video.tv.adobe.com/v/342533?quality=12&learn=on)

## Exemple SQL

```sql
INSERT INTO summit_adv_data_prep_dataset
SELECT STRUCT(
customerId AS crmCustomerId, struct(sku AS sku, price AS sku_price, abandonTS AS abandonTS) AS abandonBrowse) AS _pfreportingonprod
FROM
(SELECT
B.personKey.sourceID AS customerId,
A.productListItems[0].SKU AS sku,
max(A.timestamp) AS abandonTS,
max(C._pfreportingonprod.price) AS price
FROM summit_adobe_analytics_dataset A,profile_attribute_14adf268_2a20_4dee_bee6_a6b0e34616a9 B,summit_product_dataset C
WHERE A._experience.analytics.customDimensions.eVars.eVar1 = B.personKey.sourceID
AND A.productListItems[0].sku = C._pfreportingonprod.sku
AND A.web.webpagedetails.URL NOT LIKE '%orderconfirmation%'
AND timestamp > current_date - interval '4 day'
GROUP BY customerId,sku
order by price desc)D;
```

Pour plus d’informations, consultez la [Documentation de Query Service](https://experienceleague.adobe.com/docs/experience-platform/query/home.html?lang=fr).

>[!NOTE]
>
>Cette vidéo est un extrait de la session Adobe Summit 2020. *[Rechargement des données omnicanales pour l’électrification des expériences](https://business.adobe.com/summit/2022/sessions/recharging-omnichannel-data-for-electrifying-exper-s409.html)*.
