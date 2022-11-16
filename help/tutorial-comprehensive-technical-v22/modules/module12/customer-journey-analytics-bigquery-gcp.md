---
title: Ingestion et analyse de données Google Analytics dans Adobe Experience Platform à l’aide du connecteur source BigQuery
description: Ingestion et analyse de données Google Analytics dans Adobe Experience Platform à l’aide du connecteur source BigQuery
kt: 5342
audience: Data Engineer, Data Architect, Data Analyst
doc-type: tutorial
activity: develop
exl-id: c9c28b5a-d158-49fa-9533-1a295876f6c4
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '555'
ht-degree: 3%

---

# 12. Ingestion et analyse des données de Google Analytics dans Adobe Experience Platform avec le connecteur source BigQuery

**Auteurs : [Victor de l&#39;Iglesia](https://www.linkedin.com/in/victordelaiglesia/), [Wouter Van Geluwe](https://www.linkedin.com/in/woutervangeluwe/)**

Dans ce module, vous allez configurer votre propre instance de Google Cloud Platform, charger des exemples de données dans Google Cloud Platform et vous utiliserez ensuite le connecteur source BigQuery pour ingérer ces données de Google Cloud Platform dans Adobe Experience Platform. Enfin, vous utiliserez Customer Journey Analytics pour visualiser ces données.

Les connecteurs source de Adobe Experience Platform facilitent la récupération des données dans Adobe Experience Platform. Google BigQuery est l’un des connecteurs déjà disponibles. Grâce à Adobe Experience Platform et à BigQuery Source Connector, nous pouvons désormais importer des données Google Analytics dans Analysis Workspace en Customer Journey Analytics.

En outre, nous pouvons enrichir ces données Google Analytics en les associant à d’autres sources de données telles que les données de gestion de la relation client, de centre d’appels ou de fidélité dans Customer Journey Analytics.

## Objectifs d’apprentissage

- Familiarisez-vous avec Google Cloud Platform et l’interface utilisateur de BigQuery
- Ingestion de données Google Analytics dans Adobe Experience Platform
- Utiliser Customer Journey Analytics pour effectuer une analyse des données de Google Analytics
- Enrichissement des données Google Analytics avec des données hors ligne

## Conditions préalables

- Une certaine familiarité avec Customer Journey Analytics est préférable, mais elle n’est pas requise.
- Accès à Adobe Experience Platform : [https://experience.adobe.com/platform](https://experience.adobe.com/platform)
- Accès au Customer Journey Analytics
- Accès à Google Cloud Platform et Google BigQuery
- **Téléchargement de ces ressources**:
   - [JSON - Exemple de données : Données de fidélité](./../../assets/json/bqLoyalty.json)

>[!IMPORTANT]
>
>Ce tutoriel a été créé pour faciliter un format d’atelier particulier. Il utilise des systèmes et des comptes spécifiques auxquels vous n’avez peut-être pas accès. Même sans accès, nous pensons que vous pouvez encore apprendre beaucoup en lisant à travers ce contenu très détaillé. Si vous participez à l’un des ateliers et que vous avez besoin de vos informations d’identification d’accès, veuillez contacter votre représentant d’Adobe qui vous fournira les informations requises.

## Aperçu de l’architecture

Regardez l’architecture ci-dessous, qui met en évidence les composants qui seront discutés et utilisés dans ce module.

![Aperçu de l’architecture](../../assets/images/architecturem16.png)

## Environnement de test à utiliser

Pour ce module, utilisez cet environnement de test : `--aepSandboxId--`.

>[!NOTE]
>
>N’oubliez pas d’installer, de configurer et d’utiliser l’extension Chrome comme référencé dans [0.1 - Installation de l’extension Chrome pour la documentation Experience League](../module0/ex1.md)

## Exercices

[12.1 Création de votre compte Google Cloud Platform](./ex1.md)

Créez votre compte Google Cloud Platform.

[12.2 Créer votre première requête dans BigQuery](./ex2.md)

Découvrez comment utiliser BigQuery pour préparer les données à charger dans Platform.

[12.3 Connexion de GCP et BigQuery à Adobe Experience Platform](./ex3.md)

Découvrez comment configurer le connecteur source dans Adobe Experience Platform.

[12.4 Chargement de données de BigQuery dans Adobe Experience Platform](./ex4.md)

Découvrez comment configurer le connecteur source BigQuery dans Adobe Experience Platform pour ingérer vos données Google Analytics.

[12.5 Analyse des données de Google Analytics à l’aide de Customer Journey Analytics](./ex5.md)

Découvrez comment analyser les données Google Analytics dans Customer Journey Analytics et les combiner aux données de fidélité.

[Résumé et avantages](./summary.md)

Résumé de ce module et aperçu des avantages.

>[!NOTE]
>
>Merci d&#39;investir votre temps dans l&#39;apprentissage de Adobe Experience Platform. Si vous avez des questions, souhaitez partager les commentaires généraux d&#39;avoir des suggestions sur le contenu futur, contactez directement Wouter Van Geluwe en envoyant un email à **vangeluw@adobe.com**.

[Revenir à tous les modules](../../overview.md)
