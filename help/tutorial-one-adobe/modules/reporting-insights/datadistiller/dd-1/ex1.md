---
title: Query Service - Conditions préalables
description: Query Service - Conditions préalables
kt: 5342
doc-type: tutorial
exl-id: e9e4d478-cb8d-42a9-87a3-319e5a8b8522
source-git-commit: 1e3a8d585503eddad4c642a3b13d2b5f7ddc9943
workflow-type: tm+mt
source-wordcount: '169'
ht-degree: 1%

---

# 2.1.1 Conditions préalables

## Installation de l’utilitaire de ligne de commande PSQL

Suivez les instructions décrites dans la documentation de Adobe Experience Platform pour installer le client psql :
[&#x200B; Guide d’installation de PSQL &#x200B;](https://experienceleague.adobe.com/docs/experience-platform/query/clients/psql.html?lang=fr)

Une fois que vous avez installé PSQL, vous devrez peut-être mettre à jour votre **PATH** en exécutant la commande ci-dessous dans une fenêtre de terminal :

Pour macOS (remplacez XX dans la commande ci-dessous par le numéro de version de PSQL que vous avez installé) :

`export PATH=/Library/PostgreSQL/XX/bin:$PATH`

## Installation de Power BI

Uniquement pour les utilisateurs de Windows

[Installation de Microsoft Power BI](https://experienceleague.adobe.com/docs/experience-platform/query/clients/power-bi.html?lang=fr)

Assurez-vous d’installer la version exacte de **npgsql** comme indiqué sur le document, sinon vous ne pourrez pas connecter Power BI à Adobe Experience Platform Query Service.

## Installer Tableau

Pour les utilisateurs de Windows ou Mac

[Installez Tableau Desktop](https://experienceleague.adobe.com/docs/experience-platform/query/clients/tableau.html?lang=fr) conformément à la documentation.

Tableau vous donne automatiquement une période d&#39;essai de 14 jours.

Si vous souhaitez utiliser Tableau au-delà de ces 14 jours, vous aurez besoin d&#39;une clé de licence.

## Étapes suivantes

Accédez à [2.1.2 Prise en main](./ex2.md){target="_blank"}

Revenez à [Query Service](./query-service.md){target="_blank"}

Revenir à [Tous les modules](./../../../../overview.md){target="_blank"}
