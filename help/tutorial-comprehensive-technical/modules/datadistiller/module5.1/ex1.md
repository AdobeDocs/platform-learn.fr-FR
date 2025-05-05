---
title: Query Service - Conditions préalables
description: Query Service - Conditions préalables
kt: 5342
doc-type: tutorial
exl-id: b8a404d1-7796-46e3-b245-553acdc753ae
source-git-commit: d9d9a38c1e160950ae755e352a54667c8a7b30f7
workflow-type: tm+mt
source-wordcount: '167'
ht-degree: 0%

---

# 5.1.1 Conditions préalables

## Installation de l’utilitaire de ligne de commande PSQL

Suivez les instructions décrites dans la documentation Adobe Experience Platform pour installer le client psql :
[Guide d’installation PSQL](https://experienceleague.adobe.com/docs/experience-platform/query/clients/psql.html?lang=fr)

Une fois que vous avez installé PSQL, vous devrez peut-être mettre à jour votre **PATH** en exécutant la commande ci-dessous dans une fenêtre de terminal :

Pour macOS (remplacez XX dans la commande ci-dessous par le numéro de version de PSQL que vous avez installé) :

`export PATH=/Library/PostgreSQL/XX/bin:$PATH`

## Installer Power BI

Uniquement pour les utilisateurs Windows

[Installer Microsoft Power BI](https://experienceleague.adobe.com/docs/experience-platform/query/clients/power-bi.html?lang=fr)

Assurez-vous d’installer la version exacte de **npgsql** comme indiqué dans le document, sinon vous ne pourrez pas connecter Power BI à Adobe Experience Platform Query Service.

## Installation de Tableau

Pour les utilisateurs de Windows ou Mac

[Installez Tableau Desktop](https://experienceleague.adobe.com/docs/experience-platform/query/clients/tableau.html?lang=fr) conformément à la documentation.

Tableau vous donne automatiquement une période d’évaluation de 14 jours.

Si vous souhaitez utiliser Tableau au-delà de ces 14 jours, vous aurez besoin d’une clé de licence.

Étape suivante : [5.1.2 Prise en main](./ex2.md)

[Revenir au module 5.1](./query-service.md)

[Revenir à tous les modules](../../../overview.md)
