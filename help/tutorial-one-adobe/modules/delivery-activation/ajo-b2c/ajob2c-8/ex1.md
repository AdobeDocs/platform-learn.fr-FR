---
title: Configurer votre base de données relationnelle
description: Configurer votre base de données relationnelle
kt: 5342
doc-type: tutorial
exl-id: 532e5f2c-971f-488f-bef4-3a8141408cc8
source-git-commit: bf3bebfa3bd79829da5352e950aed3f4ef5bf6d1
workflow-type: tm+mt
source-wordcount: '250'
ht-degree: 21%

---

# 3.8.1 Configurer votre base de données relationnelle

Connectez-vous à Adobe Journey Optimizer en allant sur [https://experience.adobe.com](https://experience.adobe.com?lang=fr). Cliquez sur **Journey Optimizer**.

![AJO OC](./images/aechome.png)

Vous serez redirigé vers la vue **Accueil** dans Journey Optimizer. Tout d’abord, assurez-vous d’utiliser le bon sandbox. Le sandbox à utiliser est appelé `--aepSandboxName--`.

![AJO OC](./images/ajohome.png)

## Configuration 3.8.1.1 schéma basé sur relationnel

Un schéma relationnel est la définition formelle du modèle de données basé sur un modèle.

Il précise :

- L’ensemble de tables
- Les colonnes de chaque table
- Les contraintes
- Les relations entre les tables

L’organisation des schémas ou des tables dans un modèle de données basé sur un modèle consiste à structurer vos données en plusieurs tables. Assurez-vous que chaque table stocke un type d’entité/de schéma.

Lors de l’ingestion de données dans en vue de les utiliser avec des campagnes orchestrées par Adobe Journey Optimizer, les sources suivantes sont disponibles :

- Amazon S3
- Google Cloud Storage
- SFTP
- Snowflake
- Google BigQuery
- Data Landing Zone
- Azure Databricks
- Chargement de fichiers locaux

La première étape de cet exercice consiste à configurer vos schémas XDM basés sur des relations. Dans le menu de gauche, faites défiler l’écran jusqu’à **Gestion des données** et sélectionnez **Schémas**. Cliquez sur **+ Créer un schéma**.

![AJO OC](./images/ajoocdata1.png)

Sélectionnez **Relationnel**.

![AJO OC](./images/ajoocdata2.png)

Sélectionnez **Charger le fichier DDL** puis cliquez sur **Choisir les fichiers**.

![AJO OC](./images/ajoocdata3.png)

Maintenant que vos schémas XDM relationnels sont configurés et que les données sont ingérées, vous pouvez commencer à utiliser ces données pour créer votre campagne orchestrée dans l’exercice suivant.

## Ingestion des données 3.8.1.2


## Étapes suivantes

Accédez à [Créer votre campagne orchestrée](./ex2.md){target="_blank"}

Revenez à [Adobe Journey Optimizer : Campagnes](./ajocampaigns.md){target="_blank"}

Revenir à [Tous les modules](./../../../../overview.md){target="_blank"}
