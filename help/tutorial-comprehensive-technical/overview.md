---
title: Vue d’ensemble
description: Point de départ des ingénieurs de données, des analystes de données, des architectes de données, des spécialistes des données, des ingénieurs d’orchestration et des spécialistes du marketing pour une compréhension complète de la valeur commerciale de Adobe Experience Platform et de tous ses services d’application.
doc-type: multipage-overview
source-git-commit: 8270f69dd04714e217ddbb4d125157799cba2940
workflow-type: tm+mt
source-wordcount: '1207'
ht-degree: 2%

---

# Tutoriel technique complet d’Adobe Experience Platform

## Vue d’ensemble

Ce tutoriel est le point de départ idéal pour les ingénieurs de données, les analystes de données, les architectes de données, les spécialistes des données, les ingénieurs d’orchestration et les spécialistes du marketing afin de mieux comprendre la valeur commerciale de Adobe Experience Platform et de tous ses services d’application. Chaque leçon se concentre sur un véritable défi auquel les entreprises sont confrontées dans l&#39;écosystème complexe de personnalisation d&#39;aujourd&#39;hui, et révèle comment les Experience Platform résolvent ce défi dans le cadre de divers exercices pratiques.

Ce tutoriel est très varié et offre des informations claires dans les applications suivantes :

- Adobe Experience Platform
- Collecte de données dʼAdobe Experience Platform
- Real-time CDP
- Adobe Journey Optimizer
- Customer Journey Analytics

Ce tutoriel ne se concentre pas seulement sur les applications d’Adobe, mais tient compte de l’écosystème élargi dans lequel les marques opèrent. Pour ce faire, dans certaines leçons, il est possible de se concentrer sur la façon dont les applications _non-Adobe_ s’intègrent à Adobe Experience Platform. Vous aurez ainsi une bonne compréhension de la manière dont les applications suivantes fonctionneront avec Adobe Experience Platform :

- Amazon : AWS Lambda, AWS S3, AWS Kinesis
- Google : Google Cloud Platform, Google BigQuery, Google Display&amp;Video 360, Google AdWords
- Microsoft : Power BI, Azure EventHub, Azure Blob Storage
- Salesforce : Tableau
- Apache Kafka
- Postman
- …

Après avoir terminé les exercices de ce tutoriel, vous serez en mesure de :

- Configuration de schémas, de groupes de champs, de jeux de données et d’identités
- Configurez une propriété de collecte de données Adobe Experience Platform et configurez la nouvelle extension du SDK Web dans la collecte de données Adobe Experience Platform.
- Diffusion de données en continu dans Adobe Experience Platform en temps réel à l’aide de la collecte de données Adobe Experience Platform
- Ingestion par lots de données dans Adobe Experience Platform à l’aide d’un workflow ou d’une application d’extraction, de transformation et de chargement (ETL)
- Visualisation et utilisation du profil client en temps réel dans Adobe Experience Platform
- Créer des audiences
- Utilisation de plusieurs API Adobe Experience Platform
- Utiliser SQL pour interroger vos données dans Adobe Experience Platform
- Configuration et exécution de parcours en temps réel basés sur un déclencheur
- Utiliser la plateforme de données clients en temps réel pour agir en activant une audience vers différentes destinations
- Utilisez Customer Journey Analytics pour créer des rapports sur les données clients omnicanal provenant de diverses sources, y compris Google BigQuery

## Conditions préalables

Si vous souhaitez suivre ce tutoriel à l’aide de votre propre instance Adobe Experience Platform, suivez les instructions [ici](./setup.md) pour préparer votre organisation au tutoriel.

- Accès à Adobe Experience Platform : [https://experience.adobe.com/platform](https://experience.adobe.com/platform)
- Accès à la collecte de données Adobe Experience Platform : [https://experience.adobe.com/#/data-collection/](https://experience.adobe.com/#/data-collection/)
- Accès au système de démonstration : [https://dsn.adobe.com/](https://dsn.adobe.com/)

## Vidéos

Vous trouverez de nombreuses vidéos intéressantes de nos webinaires de l’académie de technologie, de bootcamps et plus encore sur notre [ canal YouTube de la communauté Experience Makers](https://www.youtube.com/channel/UCUKG2dkZ9pYuZUPebQ21jUw).

## Achèvement et certification

Ce tutoriel fait partie d’un cours de certification d’Adobe. Vous pouvez vous inscrire au cours en même temps que ce tutoriel en accédant à [https://certification.adobe.com](https://certification.adobe.com).

Pour chaque module que vous exécutez à l’aide du tutoriel ci-dessous, vous devez envoyer un bon à tirer comme indiqué [ici](./completion.md).

## Contenu

[0. Prise en main](./modules/gettingstarted/gettingstarted/getting-started.md)

Dans ce module de base, vous allez tout configurer pour pouvoir accéder à l’environnement de démonstration et l’utiliser.

**Investissement dans le temps :** 30 minutes

### 1. Collecte de données

[1.1 Foundation - Configuration de la collecte de données Adobe Experience Platform et du SDK web](./modules/datacollection/module1.1/data-ingestion-launch-web-sdk.md)

Dans ce module de base, vous découvrirez la collecte de données Adobe Experience Platform et la nouvelle extension du SDK Web.

**Investissement dans le temps :** 30 minutes

[1.2 Foundation - Ingestion des données](./modules/datacollection/module1.2/data-ingestion.md)

Dans ce module fondamental, vous ingérerez des données provenant de diverses sources dans Adobe Experience Platform.

**Investissement dans le temps :** 120 minutes

[1.3 Composition du public fédéré](./modules/datacollection/module1.3/fac.md)

Dans ce module, vous apprendrez à configurer un modèle d’audiences fédérées et à générer des audiences à l’aide de données fédérées.

**Investissement dans le temps :** 90 minutes

### 2. Real-Time CDP B2C

[2.1 Foundation - Profil client en temps réel](./modules/rtcdp-b2c/module2.1/real-time-customer-profile.md)

Dans ce module de base, vous allez explorer Real-time Customer Profile dans Adobe Experience Platform en utilisant l’interface utilisateur et l’API.

**Investissement dans le temps :** 90 minutes

[2.2 Intelligent Services](./modules/rtcdp-b2c/module2.2/intelligent-services.md)

Dans ce module, vous apprendrez à configurer et à utiliser les services intelligents Adobe Experience Platform.

**Investissement dans le temps :** 60 minutes

[2.3 Real-Time CDP - Création d’une audience et action](./modules/rtcdp-b2c/module2.3/real-time-cdp-build-a-segment-take-action.md)

Dans ce module, vous allez configurer une audience et activer l’audience vers plusieurs destinations, y compris Google DV360, Adobe Target et AWS S3.

**Investissement dans le temps :** 90 minutes

[2.4 Real-Time CDP : Audience Activation à Microsoft Azure Event Hub](./modules/rtcdp-b2c/module2.4/segment-activation-microsoft-azure-eventhub.md)

Dans ce module, vous allez configurer une destination Microsoft Azure EventHub en tant que destination en temps réel pour la plateforme de données clients en temps réel de Adobe Experience Platform. Vous allez également configurer et déployer une fonction Azure qui sera déclenchée en temps réel chaque fois que Adobe Experience Platform envoie une charge utile d’audience à votre destination Azure EventHub. La fonction Azure que vous allez déclencher affichera le mécanisme des fonctionnalités d’activation de la plateforme de données clients en temps réel de Adobe Experience Platform.
Dans le cadre de ce module, vous comprendrez également ce qui déclenche la diffusion d’une charge utile en temps réel sur une destination spécifiée par la plateforme CDP en temps réel. Nous discuterons également de l’état d’une qualification d’audience et de sa relation avec l’activation.

**Investissement dans le temps :** 90 minutes

[2.5 Connexions Real-Time CDP : Transfert d’événement](./modules/rtcdp-b2c/module2.5/aep-data-collection-ssf.md)

Dans ce module, vous utiliserez les jeux de données, schémas et propriétés de collecte de données Adobe Experience Platform configurés précédemment pour collecter des données, puis vous transférerez ces données côté serveur à plusieurs points de terminaison, tels que Google Cloud Platform Pub/Sub et AWS Kinesis.

**Investissement dans le temps :** 90 minutes

[2.6 Diffusion de données en continu d’Apache Kafka vers Real-Time CDP](./modules/rtcdp-b2c/module2.6/aep-apache-kafka.md)

Dans ce module, vous apprendrez à configurer votre propre grappe Apache Kafka, à définir des rubriques, des producteurs et des consommateurs et à diffuser des données dans Adobe Experience Platform à l’aide de Adobe Experience Platform Sink Connector for Kafka Connect.

**Investissement dans le temps :** 90 minutes

### 3. Adobe Journey Optimizer B2C

[Adobe Journey Optimizer 3.1 : Orchestration](./modules/ajo-b2c/module3.1/journey-orchestration-create-account.md)

Dans ce module, vous allez utiliser Adobe Journey Optimizer pour créer un parcours basé sur un déclencheur.

**Investissement dans le temps :** 60 minutes

[3.2 Adobe Journey Optimizer : sources de données externes et actions personnalisées](./modules/ajo-b2c/module3.2/journey-orchestration-external-weather-api-sms.md)

Dans ce module, vous utiliserez Adobe Journey Optimizer pour écouter le comportement des clients, en ligne et hors ligne, et y répondre de manière intelligente, contextuelle et en temps réel sur divers canaux.

**Investissement dans le temps :** 90 minutes

[3.3 Adobe Journey Optimizer : Offer decisioning](./modules/ajo-b2c/module3.3/offer-decisioning.md)

Dans ce module, vous utiliserez le service d’application Adobe Experience Platform - Offres/prise de décision de manière pratique pour configurer les offres personnalisées et votre propre activité d’offre.

**Investissement dans le temps :** 120 minutes

[3.4 Adobe Journey Optimizer : Parcours basés sur un événement](./modules/ajo-b2c/module3.4/journeyoptimizer.md)

Dans ce module, vous découvrirez tout ce que vous devez savoir sur Journey Optimizer, qui permet aux entreprises de concevoir et de proposer à leurs clients des expériences connectées, contextuelles et personnalisées.

**Investissement dans le temps :** 120 minutes

### 4. Adobe Customer Journey Analytics

[Customer Journey Analytics 4.1 : création d’un tableau de bord à l’aide d’Analysis Workspace sur Adobe Experience Platform](./modules/cja-b2c/module4.1/customer-journey-analytics-build-a-dashboard.md)

Dans ce module, vous obtiendrez des informations en ligne vers les informations hors ligne en configurant un tableau de bord contenant des données omnicanal telles que Interactions de site web, Interactions d’applications mobiles, Interactions du centre d’appels, Interactions en magasin, etc.

**Investissement dans le temps :** 120 minutes

[4.2 Customer Journey Analytics : ingestion et analyse de données de Google Analytics dans Adobe Experience Platform avec le connecteur Source BigQuery](./modules/cja-b2c/module4.2/customer-journey-analytics-bigquery-gcp.md)

Dans ce module, vous allez configurer votre propre instance de Google Cloud Platform, charger les données de démonstration dans Google Cloud Platform et vous utiliserez ensuite le connecteur BigQuery Source pour ingérer ces données de Google Cloud Platform dans Adobe Experience Platform. Enfin, vous utiliserez Customer Journey Analytics pour visualiser ces données.

**Investissement dans le temps :** 120 minutes

### 5. Distiller de données

[5.1 Query Service](./modules/datadistiller/module5.1/query-service.md)

Dans ce module, vous apprendrez à utiliser Adobe Experience Platform Query Service.

**Investissement dans le temps :** 90 minutes