---
title: Ingestion et analyse de données Google Analytics dans Adobe Experience Platform avec le connecteur Source BigQuery
description: Ingestion et analyse de données Google Analytics dans Adobe Experience Platform avec le connecteur Source BigQuery
kt: 5342
doc-type: tutorial
exl-id: 19266ac3-7c93-4cdb-8b65-75ce5c38649c
source-git-commit: 1e3a8d585503eddad4c642a3b13d2b5f7ddc9943
workflow-type: tm+mt
source-wordcount: '448'
ht-degree: 0%

---

# 1.2 Ingestion et analyse de données Google Analytics dans Adobe Experience Platform avec le connecteur Source BigQuery

Dans ce module, vous allez configurer votre propre instance de Google Cloud Platform, charger des données d’exemple dans Google Cloud Platform, puis utiliser le connecteur Source BigQuery pour ingérer ces données de Google Cloud Platform dans Adobe Experience Platform. Enfin, vous utiliserez Customer Journey Analytics pour visualiser ces données.

Les connecteurs Source de Adobe Experience Platform facilitent le processus de transfert des données dans Adobe Experience Platform. BigQuery Google est l’un des connecteurs déjà disponibles. Grâce à Adobe Experience Platform et au connecteur Source BigQuery, nous pouvons désormais importer des données Google Analytics dans Analysis Workspace en Customer Journey Analytics.

En outre, nous pouvons enrichir ces données Google Analytics en les joignant à d’autres sources de données telles que les données de gestion de la relation client (CRM), de centre d’appels ou de fidélité dans Customer Journey Analytics.

## Objectifs d’apprentissage

- Familiarisez-vous avec la plateforme cloud Google et l’interface utilisateur de BigQuery
- Ingestion de données Google Analytics dans Adobe Experience Platform
- Utilisation de Customer Journey Analytics pour effectuer une analyse des données Google Analytics
- Enrichissement des données Google Analytics avec des données hors ligne

## Conditions préalables

- Une certaine familiarité avec Customer Journey Analytics est préférable, mais non requise
- Accès à Adobe Experience Platform : [https://experience.adobe.com/platform](https://experience.adobe.com/platform)
- Accès à Customer Journey Analytics
- Accès à Google Cloud Platform et à Google BigQuery
- **Téléchargez ces ressources** :
   - [JSON - Exemples de données : données de fidélité](./../../../../assets/json/bqLoyalty.json)

>[!NOTE]
>
>N’oubliez pas d’installer, de configurer et d’utiliser l’extension Chrome, comme indiqué dans [Installation de l’extension Chrome pour la documentation Experience League](../../../getting-started/gettingstarted/ex1.md)

## Exercices

[1.2.1 Commencer à utiliser Google Cloud Platform](./ex1.md)

Commencez à utiliser votre environnement Google Cloud Platform.

[1.2.2 Création de votre première requête dans BigQuery](./ex2.md)

Découvrez comment utiliser BigQuery pour préparer les données à charger dans Platform.

[1.2.3 Connexion de GCP et BigQuery à Adobe Experience Platform](./ex3.md)

Découvrez comment configurer le connecteur source dans Adobe Experience Platform.

[1.2.4 Chargement de données BigQuery dans Adobe Experience Platform](./ex4.md)

Découvrez comment configurer le connecteur source BigQuery dans Adobe Experience Platform pour ingérer vos données Google Analytics.

[1.2.5 Analyse des données Google Analytics à l’aide de Customer Journey Analytics](./ex5.md)

Découvrez comment analyser les données Google Analytics dans Customer Journey Analytics et les combiner avec les données de fidélité.

[Résumé et avantages](./summary.md)

Résumé de ce module et aperçu des avantages.

![Insiders de la technologie ](./../../../../assets/images/techinsiders.png){width="50px" align="left"}

>[!NOTE]
>
>Merci d’avoir consacré votre temps à apprendre tout ce qu’il y a à savoir sur Adobe Experience Platform et ses applications. Si vous avez des questions, si vous souhaitez partager des commentaires généraux ou si vous avez des suggestions sur le contenu futur, veuillez contacter directement les initiés techniques, en envoyant un e-mail à **techinsiders@adobe.com**.

[Revenir à tous les modules](./../../../../overview.md)
