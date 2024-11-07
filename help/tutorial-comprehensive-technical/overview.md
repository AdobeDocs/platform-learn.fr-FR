---
title: Vue d’ensemble
description: Point de départ des ingénieurs de données, des analystes de données, des architectes de données, des spécialistes des données, des ingénieurs d’orchestration et des spécialistes du marketing pour une compréhension complète de la valeur commerciale de Adobe Experience Platform et de tous ses services d’application.
doc-type: multipage-overview
hide: false
exl-id: 88c19383-c185-40f0-b118-6cb82db0ce0e
source-git-commit: 7d2f5f842559b2d6d9f115f3993268a4b36a0fe0
workflow-type: tm+mt
source-wordcount: '1524'
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
- Créer des segments
- Utilisation de plusieurs API Adobe Experience Platform
- Utiliser SQL pour interroger vos données dans Adobe Experience Platform
- Configuration et exécution de parcours en temps réel basés sur un déclencheur
- Utiliser la plateforme de données clients en temps réel pour agir en activant un segment vers différentes destinations
- Utilisez Customer Journey Analytics pour créer des rapports sur les données clients omnicanal provenant de diverses sources, y compris Google BigQuery

## Conditions préalables

- Accès à Adobe Experience Platform : [https://experience.adobe.com/platform](https://experience.adobe.com/platform)
- Accès à la collecte de données Adobe Experience Platform : [https://experience.adobe.com/#/data-collection/](https://experience.adobe.com/#/data-collection/)
- Accès au système de démonstration : [https://dashboard.adobedemo.com/](https://dashboard.adobedemo.com/)

## Vidéos

Vous trouverez de nombreuses vidéos intéressantes de nos événements de l’académie des technologies, de Bootcamps et plus encore sur notre [ canal YouTube de la communauté Experience Makers](https://www.youtube.com/channel/UCUKG2dkZ9pYuZUPebQ21jUw).

## Contenu

[0. Prise en main](./modules/gettingstarted/gettingstarted/getting-started.md)

- **Audience :** Tous les participants du tutoriel technique complet pour Adobe Experience Platform
- **Conditions préalables :** accès au système de démonstration Suivant, à la collecte de données Adobe Experience Platform et Adobe Experience Platform.
- **Description :** Dans ce module de base, vous allez tout configurer pour pouvoir accéder à l’environnement de démonstration et l’utiliser.
- **Investissement dans le temps :** 30 minutes

### 1. Collecte de données

[1.1 Foundation - Configuration de la collecte de données Adobe Experience Platform et du SDK web](./modules/datacollection/module1.1/data-ingestion-launch-web-sdk.md)

- **Audience :** Ingénieur de données, architecte de données
- **Conditions préalables :** accès à la collecte de données Adobe Experience Platform et Adobe Experience Platform.
- **Description :** Dans ce module de base, vous découvrirez la collecte de données Adobe Experience Platform et la nouvelle extension du SDK Web.
- **Investissement dans le temps :** 30 minutes

[1.2 Foundation - Ingestion des données](./modules/datacollection/module1.2/data-ingestion.md)

- **Audience :** Ingénieur de données, architecte de données
- **Conditions préalables :** accès à la collecte de données Adobe Experience Platform et Adobe Experience Platform.
- **Description :** Dans ce module de base, vous allez ingérer des données du site web dans Platform.
- **Investissement dans le temps :** 120 minutes

[1.3 Federated Audience Composition](./modules/datacollection/module1.3/fac.md)

- **Audience :** Analyste de données, ingénieur de données, architecte de données
- **Conditions préalables :** accès à Adobe Experience Platform
- **Description :** Dans ce module, vous apprendrez à configurer votre propre grappe Apache Kafka, à définir des rubriques, des producteurs et des consommateurs et à diffuser des données dans Adobe Experience Platform à l’aide du connecteur Adobe Experience Platform Sink pour Kafka Connect.
- **Investissement dans le temps :** 90 minutes

### 2. Real-Time CDP B2C

[2.1 Foundation - Profil client en temps réel](./modules/rtcdp-b2c/module2.1/real-time-customer-profile.md)

- **Audience :** ingénieur de données, architecte de données, marketeur
- **Conditions préalables :** accès à Adobe Experience Platform et Postman
- **Description :** Dans ce module de base, vous allez explorer le profil client en temps réel dans Adobe Experience Platform en utilisant l’interface utilisateur et l’API.
- **Investissement dans le temps :** 90 minutes
- **Téléchargez ces ressources** :
   - [Collections Postman](./assets/postman/postman_profile.zip)

[2.2 Intelligent Services](./modules/rtcdp-b2c/module2.2/intelligent-services.md)

- **Audience :** Ingénieur de données, architecte de données, spécialiste des données
- **Conditions préalables :** accès à Adobe Experience Platform, services intelligents
- **Description :** Dans ce module, vous apprendrez à configurer, configurer et utiliser les services intelligents Adobe Experience Platform.
- **Investissement dans le temps :** 60 minutes

[2.3 Real-Time CDP - Création d’un segment et action](./modules/rtcdp-b2c/module2.3/real-time-cdp-build-a-segment-take-action.md)

- **Audience :** Architecte de données, ingénieur d’orchestration, marketeur
- **Conditions préalables :** accès à Adobe Experience Platform, à la plateforme de données clients en temps réel, à Adobe Audience Manager, à Adobe Target, à AWS S3
- **Description :** Dans ce module, vous allez configurer un segment, l’activer pour la segmentation par flux et activer le segment vers plusieurs destinations, y compris Google DV360, Google AdWords, Adobe Audience Manager, Adobe Target et des destinations S3 telles que Salesforce Marketing Cloud.
- **Investissement dans le temps :** 90 minutes

[2.4 Real-Time CDP : activation de segments vers Microsoft Azure Event Hub](./modules/rtcdp-b2c/module2.4/segment-activation-microsoft-azure-eventhub.md)

- **Audience :** Ingénieur de données, architecte de données, analyste de données
- **Conditions préalables :** accès à Adobe Experience Platform, à la plateforme de données clients en temps réel et à Microsoft Azure
- **Description :** Dans ce module, vous allez configurer une destination Microsoft Azure EventHub en tant que destination en temps réel pour la plateforme de données clients en temps réel de Adobe Experience Platform. Vous allez également configurer et déployer une fonction Azure qui sera déclenchée en temps réel chaque fois que Adobe Experience Platform envoie une charge utile de segment à votre destination Azure EventHub. La fonction Azure que vous allez déclencher affichera le mécanisme des fonctionnalités d’activation de la plateforme de données clients en temps réel de Adobe Experience Platform.
Dans le cadre de ce module, vous comprendrez également ce qui déclenche la diffusion d’une charge utile en temps réel sur une destination spécifiée par la plateforme CDP en temps réel. Nous discuterons également de l’état d’une qualification de segment et de sa relation avec l’activation.
- **Investissement dans le temps :** 90 minutes

[2.5 Connexions Real-Time CDP : Transfert d’événement](./modules/rtcdp-b2c/module2.5/aep-data-collection-ssf.md)

- **Audience :** Ingénieur de données, architecte de données, analyste de données
- **Conditions préalables :** accès aux propriétés de connexion Real-Time CDP, de balises et de transfert d’événements
- **Description :** Dans ce module, vous utiliserez les jeux de données, schémas et propriétés de collecte de données Adobe Experience Platform configurés précédemment pour collecter des données, puis vous transmettrez ces données côté serveur à un point de terminaison de votre choix.
- **Investissement dans le temps :** 90 minutes

[2.6 Diffusion de données en continu d’Apache Kafka vers Real-Time CDP](./modules/rtcdp-b2c/module2.6/aep-apache-kafka.md)

- **Audience :** Analyste de données, ingénieur de données, architecte de données
- **Conditions préalables :** accès à Adobe Experience Platform
- **Description :** Dans ce module, vous apprendrez à configurer votre propre grappe Apache Kafka, à définir des rubriques, des producteurs et des consommateurs et à diffuser des données dans Adobe Experience Platform à l’aide du connecteur Adobe Experience Platform Sink pour Kafka Connect.
- **Investissement dans le temps :** 90 minutes

### 3. Adobe Journey Optimizer B2C

[Adobe Journey Optimizer 3.1 : Orchestration](./modules/ajo-b2c/module3.1/journey-orchestration-create-account.md)

- **Audience :** ingénieur de données, architecte de données, ingénieur d’orchestration
- **Conditions préalables :** accès à Adobe Experience Platform et Adobe Journey Optimizer
- **Description :** Dans ce module, vous utiliserez Adobe Journey Optimizer pour créer un parcours basé sur un déclencheur.
- **Investissement dans le temps :** 60 minutes

[3.2 Adobe Journey Optimizer : sources de données externes et actions personnalisées](./modules/ajo-b2c/module3.2/journey-orchestration-external-weather-api-sms.md)

- **Audience :** ingénieur de données, architecte de données, ingénieur d’orchestration, marketeur
- **Conditions préalables :** accès à Adobe Experience Platform, Adobe Journey Optimizer, API Open Weather, Twilio
- **Description :** Dans ce module, vous utiliserez Adobe Journey Optimizer pour écouter le comportement des clients, en ligne et hors ligne, et y répondre de manière intelligente, contextuelle et en temps réel sur divers canaux.
- **Investissement dans le temps :** 90 minutes

[3.3 Adobe Journey Optimizer : Offer decisioning](./modules/ajo-b2c/module3.3/offer-decisioning.md)

- **Audience :** ingénieur de données, architecte de données, ingénieur d’orchestration, marketeur
- **Conditions préalables :** accès à Adobe Experience Platform et à l’Offer decisioning
- **Description :** Dans ce module, vous utiliserez le service d’application Adobe Experience Platform - Offres/prise de décision de manière pratique pour configurer les offres personnalisées et votre propre activité d’offre.
- **Investissement dans le temps :** 120 minutes

[3.4 Adobe Journey Optimizer : Parcours basés sur un événement](./modules/ajo-b2c/module3.4/journeyoptimizer.md)

- **Audience :** spécialiste du marketing par e-mail, spécialiste d’orchestration, ingénieur de données, architecte de données, analyste de données
- **Conditions préalables :** accès à Adobe Experience Platform et Journey Optimizer
- **Description :** Dans ce module, vous découvrirez tout ce que vous devez savoir sur Journey Optimizer, qui aide les entreprises à concevoir et à offrir à leurs clients des expériences connectées, contextuelles et personnalisées.
- **Investissement dans le temps :** 120 minutes

### 4. Adobe Customer Journey Analytics

[Customer Journey Analytics 4.1 : création d’un tableau de bord à l’aide d’Analysis Workspace sur Adobe Experience Platform](./modules/cja-b2c/module4.1/customer-journey-analytics-build-a-dashboard.md)

- **Audience :** Ingénieur de données, architecte de données, analyste de données
- **Conditions préalables :** accès à Adobe Experience Platform et Customer Journey Analytics
- **Description :** Dans ce module, vous accédez aux informations hors ligne en configurant un tableau de bord contenant des données omnicanal telles que Interactions de site Web, Interactions d’applications mobiles, Interactions de centre d’appels, Interactions en magasin, etc.
- **Investissement dans le temps :** 120 minutes

[4.2 Customer Journey Analytics : ingestion et analyse de données de Google Analytics dans Adobe Experience Platform avec le connecteur Source BigQuery](./modules/cja-b2c/module4.2/customer-journey-analytics-bigquery-gcp.md)

- **Audience :** Ingénieur de données, architecte de données, analyste de données
- **Conditions préalables :** accès à Adobe Experience Platform, Customer Journey Analytics, Google Cloud Platform, Google BigQuery
- **Description :** Dans ce module, vous allez configurer votre propre instance de Google Cloud Platform, charger des données de démonstration dans Google Cloud Platform et vous utiliserez ensuite le connecteur BigQuery Source pour ingérer ces données de Google Cloud Platform dans Adobe Experience Platform. Enfin, vous utiliserez Customer Journey Analytics pour visualiser ces données.
- **Investissement dans le temps :** 120 minutes
- **Téléchargez ces ressources** :
   - [JSON - Exemple de données : Demo - Loyalty Data](./assets/json/bqLoyalty.json)

### 5. Distiller de données

[5.1 Query Service](./modules/datadistiller/module5.1/query-service.md)

- **Audience :** ingénieur de données, architecte de données, analyste de données, expert de BI
- **Conditions préalables :** accès à Adobe Experience Platform, Query Service, Power BI ou Tableau
- **Description :** Dans ce module, vous apprendrez à utiliser Adobe Experience Platform Query Service.
- **Investissement dans le temps :** 90 minutes
- **Téléchargez ces ressources** :
   - [JSON - Exemple de données : système de démonstration - jeu de données d’événement pour le site web](./assets/json/ee.json)
   - [JSON - Exemple de données : système de démonstration - jeu de données d’événement pour le centre d’appels](./assets/json/callcenter.json)
   - [JSON - Exemple de données : système de démonstration - jeu de données de profil pour la fidélité](./assets/json/loyalty.json)





