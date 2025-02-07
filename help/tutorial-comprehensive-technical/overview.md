---
title: Présentation - Tutoriel technique complet pour AEP et les applications
description: Point de départ pour les ingénieurs de données, les analystes de données, les architectes de données, les spécialistes des données, les ingénieurs d’orchestration et les marketeurs afin de mieux comprendre la valeur commerciale de Adobe Experience Platform et de tous ses services applicatifs.
doc-type: multipage-overview
exl-id: 88c19383-c185-40f0-b118-6cb82db0ce0e
source-git-commit: 3b3c62499bfed86ab13a657a816424879cab4f42
workflow-type: tm+mt
source-wordcount: '1258'
ht-degree: 2%

---

# Tutoriel technique complet d’Adobe Experience Platform

![Insiders de la technologie ](./assets/images/techinsiders.png){width="50px" align="left"}

## Vue d’ensemble

Ce tutoriel constitue le point de départ idéal pour les ingénieurs de données, les analystes de données, les architectes des données, les spécialistes des données, les ingénieurs d’orchestration et les spécialistes du marketing afin de mieux comprendre la valeur commerciale de Adobe Experience Platform et de tous ses services applicatifs. Chaque leçon se concentre sur un véritable défi auquel les entreprises sont confrontées dans l’écosystème complexe de personnalisation d’aujourd’hui et détaille la manière dont l’Experience Platform le résout dans divers exercices pratiques.

Ce tutoriel est très diversifié et offre des informations claires sur les applications suivantes :

- Adobe Experience Platform
- Collecte de données dʼAdobe Experience Platform
- Real-time CDP
- Adobe Journey Optimizer
- Customer Journey Analytics

Ce tutoriel ne se concentre pas uniquement sur les applications d’Adobe, mais prend en compte l’écosystème plus large dans lequel les marques opèrent. Pour ce faire, dans certaines leçons, l’accent est mis sur la manière dont les applications _hors Adobe_ s’intègrent à Adobe Experience Platform. Ainsi, vous comprendrez mieux comment les applications ci-dessous vont fonctionner avec Adobe Experience Platform :

- Amazon : AWS Lambda, AWS S3, AWS Kinesis
- Google : Google Cloud Platform, Google BigQuery, Google Display&amp;Video 360, Google AdWords
- Microsoft : Power BI, Azure EventHub, Stockage Blob Azure
- Salesforce : Tableau
- Apache Kafka
- Postman
- …

Après avoir terminé les exercices de ce tutoriel, vous serez en mesure de :

- Configurer des schémas, des groupes de champs, des jeux de données et des identités
- Configurez une propriété de collecte de données Adobe Experience Platform et configurez la nouvelle extension de SDK Web dans la collecte de données Adobe Experience Platform
- Diffusion de données dans Adobe Experience Platform en temps réel à l’aide de la collecte de données Adobe Experience Platform
- Ingérez des données par lots dans Adobe Experience Platform à l’aide d’un workflow ou d’une application d’extraction, de transformation et de chargement (ETL)
- Visualiser et utiliser le profil client en temps réel dans Adobe Experience Platform
- Créer des audiences
- Utilisation de plusieurs API Adobe Experience Platform
- Utiliser SQL pour interroger vos données dans Adobe Experience Platform
- Configuration et exécution de parcours en temps réel basés sur des déclencheurs
- Utilisez Real-Time CDP pour agir en activant une audience vers différentes destinations
- Utilisez Customer Journey Analytics pour générer des rapports sur les données client omnicanales provenant de diverses sources, y compris Google BigQuery

## Conditions préalables

Si vous souhaitez suivre ce tutoriel à l’aide de votre propre instance Adobe Experience Platform, suivez les instructions [ici](./setup.md) pour préparer votre organisation au tutoriel.

- Accès à Adobe Experience Platform : [https://experience.adobe.com/platform](https://experience.adobe.com/platform)
- Accès à la collecte de données Adobe Experience Platform : [https://experience.adobe.com/#/data-collection/](https://experience.adobe.com/#/data-collection/)
- Accès au système de démonstration : [https://dsn.adobe.com/](https://dsn.adobe.com/)

## Vidéos

Vous trouverez de nombreuses vidéos intéressantes de nos webinaires de la Tech Academy, de nos camps d’amorçage et plus encore sur notre chaîne [Experience Makers Community YouTube](https://www.youtube.com/channel/UCUKG2dkZ9pYuZUPebQ21jUw).

## Accomplissement et certification

Ce tutoriel fait partie d’un cours de certification Adobe. Vous pouvez vous inscrire au cours en même temps que ce tutoriel en accédant à [https://certification.adobe.com/courses/1258](https://certification.adobe.com/courses/1258).

Pour chaque module que vous suivez à l’aide du tutoriel ci-dessous, vous devez soumettre un justificatif d’accomplissement comme indiqué [ici](./completion.md).

## Contenu

Pour vérifier le statut du contenu ci-dessous, accédez à la page [statut](./status.md).

[0. Prise en main](./modules/gettingstarted/gettingstarted/getting-started.md)

Dans ce module de base, vous allez tout configurer pour pouvoir accéder à l’environnement de démonstration et l’utiliser.

**Time Investment :** 30 minutes

### 1. Collecte de données

[1.1 Foundation - Configuration de la collecte de données Adobe Experience Platform et de Web SDK](./modules/datacollection/module1.1/data-ingestion-launch-web-sdk.md)

Dans ce module fondamental, vous découvrirez la collecte de données Adobe Experience Platform et la nouvelle extension de SDK web.

**Time Investment :** 30 minutes

[1.2 Foundation - Ingestion de données](./modules/datacollection/module1.2/data-ingestion.md)

Dans ce module de base, vous allez ingérer des données provenant de diverses sources dans Adobe Experience Platform

**Time Investment :** 120 minutes

[1.3 Composition De L’Audience Fédérée](./modules/datacollection/module1.3/fac.md)

Dans ce module, vous apprendrez à configurer un modèle d’audiences fédérées et à générer des audiences à l’aide de données fédérées.

**Time Investment :** 90 minutes

### 2. Real-Time CDP B2C

[2.1 Foundation - Profil client en temps réel](./modules/rtcdp-b2c/module2.1/real-time-customer-profile.md)

Dans ce module de base, vous allez explorer le profil client en temps réel dans Adobe Experience Platform à l’aide de l’interface utilisateur et de l’API.

**Time Investment :** 90 minutes

[2.2 Services intelligents](./modules/rtcdp-b2c/module2.2/intelligent-services.md)

Dans ce module, vous apprendrez à configurer et à utiliser les services intelligents de Adobe Experience Platform.

**Time Investment :** 60 minutes

[2.3 Real-Time CDP - Créez une audience et prenez des mesures](./modules/rtcdp-b2c/module2.3/real-time-cdp-build-a-segment-take-action.md)

Dans ce module, vous allez configurer une audience et l’activer vers plusieurs destinations, notamment Google DV360, Adobe Target et AWS S3.

**Time Investment :** 90 minutes

[2.4 Real-Time CDP : Audience Activation vers Microsoft Azure Event Hub](./modules/rtcdp-b2c/module2.4/segment-activation-microsoft-azure-eventhub.md)

Dans ce module, vous allez configurer une destination Microsoft Azure EventHub en tant que destination en temps réel pour Adobe Experience Platform Real-time CDP. Vous devez également configurer et déployer une fonction Azure qui sera déclenchée en temps réel chaque fois que Adobe Experience Platform diffuse une payload d’audience vers votre destination Azure EventHub. La fonction Azure que vous déclencherez affichera le mécanisme des fonctionnalités d’activation de Adobe Experience Platform Real-time CDP.
Dans le cadre de ce module, vous comprendrez également ce qui déclenche la plateforme de données clients en temps réel pour diffuser une payload vers une destination spécifiée. Nous discuterons également du statut d’une qualification d’audience et de sa relation avec l’activation.

**Time Investment :** 90 minutes

[2.5 Connexions Real-Time CDP : transfert d’événement](./modules/rtcdp-b2c/module2.5/aep-data-collection-ssf.md)

Dans ce module, vous utiliserez les jeux de données, les schémas et la propriété de collecte de données Adobe Experience Platform configurés précédemment pour collecter des données, puis vous transmettrez ces données côté serveur à plusieurs points d’entrée, tels que Google Cloud Platform Pub/Sub et AWS Kinesis.

**Time Investment :** 90 minutes

[2.6 Diffuser des données d’Apache Kafka vers Real-Time CDP](./modules/rtcdp-b2c/module2.6/aep-apache-kafka.md)

Dans ce module, vous apprendrez à configurer votre propre cluster Apache Kafka, à définir des rubriques, des producteurs et des consommateurs et à diffuser des données dans Adobe Experience Platform à l’aide du connecteur de récepteur Adobe Experience Platform pour Kafka Connect.

**Time Investment :** 90 minutes

### 3. Adobe Journey Optimizer B2C

[3.1 Adobe Journey Optimizer : Orchestration](./modules/ajo-b2c/module3.1/journey-orchestration-create-account.md)

Dans ce module, vous utiliserez Adobe Journey Optimizer pour créer un parcours basé sur un déclencheur.

**Time Investment :** 60 minutes

[3.2 Adobe Journey Optimizer : sources de données externes et actions personnalisées](./modules/ajo-b2c/module3.2/journey-orchestration-external-weather-api-sms.md)

Dans ce module, vous utiliserez Adobe Journey Optimizer pour écouter le comportement des clients, en ligne et hors ligne, et y répondre de manière intelligente, contextuelle et en temps réel sur divers canaux.

**Time Investment :** 90 minutes

[3.3 Adobe Journey Optimizer : Offer decisioning](./modules/ajo-b2c/module3.3/offer-decisioning.md)

Dans ce module, vous allez utiliser le service applicatif Adobe Experience Platform - Offres/Prise de décision de manière pratique pour configurer des offres personnalisées et votre propre activité d’offre.

**Time Investment :** 120 minutes

[3.4 Adobe Journey Optimizer : Parcours basés sur un événement](./modules/ajo-b2c/module3.4/journeyoptimizer.md)

Dans ce module, vous apprendrez tout ce qu’il y a à savoir sur Journey Optimizer, qui aide les entreprises à concevoir et à proposer des expériences connectées, contextuelles et personnalisées à leurs clients.

**Time Investment :** 120 minutes

### 4. Adobe Customer Journey Analytics

[Customer Journey Analytics 4.1 : création d’un tableau de bord à l’aide d’Analysis Workspace sur Adobe Experience Platform](./modules/cja-b2c/module4.1/customer-journey-analytics-build-a-dashboard.md)

Dans ce module, vous obtiendrez des informations en ligne et hors ligne en configurant un tableau de bord contenant des données omnicanales telles que les interactions de site web, les interactions d’application mobile, les interactions de centre d’appels, les interactions en magasin, etc.

**Time Investment :** 120 minutes

[4.2 Customer Journey Analytics : ingestion et analyse de données de Google Analytics dans Adobe Experience Platform avec le connecteur Source BigQuery](./modules/cja-b2c/module4.2/customer-journey-analytics-bigquery-gcp.md)

Dans ce module, vous allez configurer votre propre instance de Google Cloud Platform, charger des données de démonstration dans Google Cloud Platform, puis utiliser le connecteur Source BigQuery pour ingérer ces données de Google Cloud Platform dans Adobe Experience Platform. Enfin, vous utiliserez Customer Journey Analytics pour visualiser ces données.

**Time Investment :** 120 minutes

### 5. Distiller de données

[5.1 Query Service](./modules/datadistiller/module5.1/query-service.md)

Dans ce module, vous apprendrez à utiliser Adobe Experience Platform Query Service.

**Time Investment :** 90 minutes

![Insiders de la technologie ](./assets/images/techinsiders.png){width="50px" align="left"}

>[!NOTE]
>
>Si vous avez des questions, si vous souhaitez partager des commentaires généraux ou si vous avez des suggestions sur le contenu futur, veuillez contacter directement les initiés techniques, en envoyant un e-mail à **techinsiders@adobe.com**.
