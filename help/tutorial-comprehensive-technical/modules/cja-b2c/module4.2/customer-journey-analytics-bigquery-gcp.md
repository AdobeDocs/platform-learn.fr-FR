---
title: Ingestion et analyse de données Google Analytics dans Adobe Experience Platform avec le connecteur Source BigQuery
description: Ingestion et analyse de données Google Analytics dans Adobe Experience Platform avec le connecteur Source BigQuery
kt: 5342
doc-type: tutorial
exl-id: b078d003-da25-44c5-b000-77e3b3188fb6
source-git-commit: 0dbcda0cfc9f199a44c845c1b5caf00a8d740251
workflow-type: tm+mt
source-wordcount: '456'
ht-degree: 0%

---

# 4.2 Ingestion et analyse des données de Google Analytics dans Adobe Experience Platform avec le connecteur Source BigQuery

**Auteurs : [Victor de la Iglesia](https://www.linkedin.com/in/victordelaiglesia/), [Wouter Van Geluwe](https://www.linkedin.com/in/woutervangeluwe/)**

Dans ce module, vous allez configurer votre propre instance de Google Cloud Platform, charger des exemples de données dans Google Cloud Platform et vous utiliserez ensuite le connecteur BigQuery Source pour ingérer ces données de Google Cloud Platform dans Adobe Experience Platform. Enfin, vous utiliserez Customer Journey Analytics pour visualiser ces données.

Les connecteurs Source de Adobe Experience Platform facilitent la récupération des données dans Adobe Experience Platform. Google BigQuery est l’un des connecteurs déjà disponibles. Grâce à Adobe Experience Platform et à BigQuery Source Connector, nous pouvons désormais importer des données Google Analytics dans Analysis Workspace en Customer Journey Analytics.

En outre, nous pouvons enrichir ces données Google Analytics en les associant à d’autres sources de données telles que les données de gestion de la relation client, de centre d’appels ou de fidélité dans Customer Journey Analytics.

## Objectifs d’apprentissage

- Familiarisez-vous avec Google Cloud Platform et l’interface utilisateur de BigQuery
- Ingestion de données Google Analytics dans Adobe Experience Platform
- Utiliser Customer Journey Analytics pour effectuer une analyse des données de Google Analytics
- Enrichissement des données Google Analytics avec des données hors ligne

## Conditions préalables

- Une certaine familiarité avec Customer Journey Analytics est préférable, mais elle n’est pas requise.
- Accès à Adobe Experience Platform : [https://experience.adobe.com/platform](https://experience.adobe.com/platform)
- Accès au Customer Journey Analytics
- Accès à Google Cloud Platform et Google BigQuery
- **Téléchargez ces ressources** :
   - [JSON - Exemple de données : données de fidélité](./../../../assets/json/bqLoyalty.json)

>[!NOTE]
>
>N’oubliez pas d’installer, de configurer et d’utiliser l’extension Chrome comme référencé dans [Installation de l’extension Chrome pour la documentation Experience League](../../gettingstarted/gettingstarted/ex1.md)

## Exercices

[4.2.1 Création de votre compte Google Cloud Platform](./ex1.md)

Créez votre compte Google Cloud Platform.

[4.2.2 Création de votre première requête dans BigQuery](./ex2.md)

Découvrez comment utiliser BigQuery pour préparer les données à charger dans Platform.

[4.2.3 Connexion de GCP et BigQuery à Adobe Experience Platform](./ex3.md)

Découvrez comment configurer le connecteur source dans Adobe Experience Platform.

[4.2.4 Chargement de données de BigQuery dans Adobe Experience Platform](./ex4.md)

Découvrez comment configurer le connecteur source BigQuery dans Adobe Experience Platform pour ingérer vos données Google Analytics.

[4.2.5 Analyse des données des Google Analytics à l’aide de Customer Journey Analytics](./ex5.md)

Découvrez comment analyser les données Google Analytics dans Customer Journey Analytics et les combiner aux données de fidélité.

[Résumé et avantages](./summary.md)

Résumé de ce module et aperçu des avantages.

>[!NOTE]
>
>Merci d’investir votre temps à apprendre tout ce qu’il y a à savoir sur Adobe Experience Platform et ses applications. Si vous avez des questions, si vous souhaitez partager les commentaires généraux d’avoir des suggestions sur le contenu futur, contactez directement les initiés de technologie, en envoyant un email à **techinsiders@adobe.com**.

[Revenir à tous les modules](../../../overview.md)
