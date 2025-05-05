---
title: Rechargez vos données client pour offrir des expériences électrisantes
description: Découvrez comment atténuer l’impact des données de faible qualité, réduire le délai de rentabilisation et multiplier le retour sur investissement en utilisant les mêmes données pour une multitude de cas d’utilisation.
feature: Queries
role: Data Engineer, Data Architect, Developer
level: Beginner
jira: KT-10323
thumbnail: 342533.jpeg
exl-id: 30574cc5-66fa-4ab8-83ed-7af710294dbf
source-git-commit: 286c85aa88d44574f00ded67f0de8e0c945a153e
workflow-type: tm+mt
source-wordcount: '163'
ht-degree: 0%

---

# Rechargez vos données client pour offrir des expériences électrisantes

Les données omnicanales sont un ingrédient essentiel pour alimenter les profils clients exploitables utilisés par les spécialistes marketing pour orchestrer l’activation et mesurer les parcours client qui en résultent. Toutefois, les entreprises sont confrontées à des défis pour gérer la qualité, l’échelle et la variété de ces données. Elles nécessitent des solutions rationalisées pour atténuer l’impact des données de faible qualité, réduire le délai de rentabilisation et multiplier le retour sur investissement en utilisant les mêmes données pour une multitude de cas d’utilisation.
Pour plus d’informations, consultez la [documentation de Query Service](https://experienceleague.adobe.com/docs/experience-platform/query/home.html?lang=fr).

Cette vidéo explore les points suivants :

* Fonctionnalités de préparation des données de Adobe Experience Platform que vous pouvez exploiter
* Augmentation du retour sur investissement depuis Adobe Real-Time CDP, Adobe Journey Optimizer et Customer Journey Analytics

>[!VIDEO](https://video.tv.adobe.com/v/3454937?learn=on&enablevpops&captions=fre_fr)

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

>[!NOTE]
>
>Cette vidéo est un extrait de la session Adobe Summit 2020 *[Rechargement des données omnicanales pour des expériences électrisantes](https://business.adobe.com/summit/2022/sessions/recharging-omnichannel-data-for-electrifying-exper-s409.html)*.
