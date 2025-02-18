---
title: Présentation - Tutoriel technique complet - One Adobe
description: Tutoriel technique complet - One Adobe
doc-type: multipage-overview
exl-id: 5bc0d621-0662-4d94-80a0-b6c173c0ac9e
source-git-commit: f25c1705ae6813dc744945e8a4ee9858513f7374
workflow-type: tm+mt
source-wordcount: '957'
ht-degree: 2%

---

# Tutoriel technique complet - One Adobe

![Insiders de la technologie ](./assets/images/techinsiders.png){width="50px" align="left"}

## Vue d’ensemble

Ce tutoriel est le point de départ idéal pour

Ce tutoriel est très diversifié et offre des informations claires sur les applications suivantes :

- Services Adobe Firefly
- Adobe Photoshop
- Adobe Workfront et Adobe Workfront Fusion
- Adobe Experience Manager Cloud Service, Sites, Assets et Edge Delivery Services
- Adobe Experience Platform
- Adobe Real-Time CDP
- Adobe Journey Optimizer


Ce tutoriel ne se concentre pas uniquement sur les applications Adobe, mais prend en compte l’écosystème plus large dans lequel les marques opèrent. Pour ce faire, certaines leçons mettent l’accent sur la manière dont les applications non Adobe s’intègrent aux applications Adobe. Ainsi, vous comprendrez mieux comment les applications ci-dessous vont fonctionner avec Adobe Experience Platform :

- Amazon AWS
- Google Cloud Platform
- Microsoft Azure
- Postman
- Snowflake
- …

## Conditions préalables

Si vous souhaitez suivre ce tutoriel à l’aide de votre propre instance de Adobe Experience Cloud, les applications suivantes doivent être configurées dans votre instance et vous devez pouvoir y accéder :

- Adobe Firefly [https://firefly.adobe.com/](https://firefly.adobe.com/){target="_blank"}
- Adobe Photoshop
- Adobe Workfront
- Adobe Workfront Fusion [https://fusion.adobe.com/](https://fusion.adobe.com/){target="_blank"}
- Adobe Experience Platform : [https://experience.adobe.com/platform](https://experience.adobe.com/platform){target="_blank"}
- Collecte De Données Adobe Experience Platform : [https://experience.adobe.com/#/data-collection/](https://experience.adobe.com/#/data-collection/){target="_blank"}
- Accès au système de démonstration : [https://dsn.adobe.com/](https://dsn.adobe.com/){target="_blank"}

## Prétravail

Vérifiez les applications requises qui doivent être installées sur votre ordinateur [ici](./prework.md){target="_blank"}.

## Accomplissement et certification

Ce tutoriel fait partie d’un cours de certification Adobe. Vous pouvez vous inscrire au cours en même temps que ce tutoriel en accédant à [https://certification.adobe.com](https://certification.adobe.com).

Pour chaque module que vous suivez à l’aide du tutoriel ci-dessous, vous devez soumettre un justificatif d’accomplissement comme indiqué [ici](./completion.md).

## Contenu

Pour vérifier le statut du contenu ci-dessous, accédez à la page [statut](./status.md){target="_blank"}.

### Commencer

[Prise en main](./modules/getting-started/gettingstarted/getting-started.md){target="_blank"}

Dans ce module de base, vous allez tout configurer pour pouvoir accéder à l’environnement de démonstration et l’utiliser.

### 1. Workflow et planification

### 2. Création et production

[1.1 Services Adobe Firefly](./modules/creation-production/module1.1/firefly-services.md){target="_blank"}

Dans ce module, vous utiliserez les API Adobe Firefly Services, les API Photoshop et les services de stockage Azure Microsoft pour générer des images et les stocker par programmation.

[1.2 Automatisation des workflows créatifs avec Workfront Fusion](./modules/creation-production/module1.2/automation.md){target="_blank"}

Dans ce module de base, vous utiliserez Adobe Workfront Fusion pour automatiser et mettre à l’échelle vos workflows de création de contenu.

### 3. Gestion des actifs

[1.1 Adobe Experience Manager Cloud Service et Edge Delivery Services](./modules/asset-mgmt/module2.1/aemcs.md){target="_blank"}

Dans ce module de base, vous allez configurer votre programme Adobe Experience Manager Cloud Service, votre site et votre référentiel Assets.

[1.2 Gestion des workflows avec Adobe Workfront](./modules/asset-mgmt/module2.2/workfront.md){target="_blank"}

Dans ce module de base, vous allez configurer et utiliser Adobe Workfront pour gérer les flux de validation et vous utiliserez les intégrations à Adobe Experience Manager Assets, l’éditeur universel, Photoshop, etc.

### 4. Diffusion et activation

#### Collecte de données

[1.1 Foundation - Configuration de la collecte de données Adobe Experience Platform et de Web SDK](./modules/delivery-activation/datacollection/dc1.1/data-ingestion-launch-web-sdk.md)

Dans ce module fondamental, vous découvrirez la collecte de données Adobe Experience Platform et la nouvelle extension de SDK web.

[1.2 Foundation - Ingestion de données](./modules/delivery-activation/datacollection/dc1.2/data-ingestion.md)

Dans ce module de base, vous allez ingérer des données provenant de diverses sources dans Adobe Experience Platform

[1.3 Composition De L’Audience Fédérée](./modules/delivery-activation/datacollection/dc1.3/fac.md)

Dans ce module, vous apprendrez à configurer un modèle d’audiences fédérées et à générer des audiences à l’aide de données fédérées.

#### Real-Time CDP B2C

[2.1 Foundation - Profil client en temps réel](./modules/delivery-activation/rtcdp-b2c/rtcdpb2c-1/real-time-customer-profile.md)

Dans ce module de base, vous allez explorer le profil client en temps réel dans Adobe Experience Platform à l’aide de l’interface utilisateur et de l’API.

[2.2 Services intelligents](./modules/delivery-activation/rtcdp-b2c/rtcdpb2c-2/intelligent-services.md)

Dans ce module, vous apprendrez à configurer et à utiliser les services intelligents de Adobe Experience Platform.

[2.3 Real-Time CDP - Créez une audience et prenez des mesures](./modules/delivery-activation/rtcdp-b2c/rtcdpb2c-3/real-time-cdp-build-a-segment-take-action.md)

Dans ce module, vous allez configurer une audience et l’activer vers plusieurs destinations, notamment Google DV360, Adobe Target et AWS S3.

[2.4 Real-Time CDP : Audience Activation vers Microsoft Azure Event Hub](./modules/delivery-activation/rtcdp-b2c/rtcdpb2c-4/segment-activation-microsoft-azure-eventhub.md)

Dans ce module, vous allez configurer une destination Microsoft Azure EventHub en tant que destination en temps réel pour Adobe Experience Platform Real-time CDP.

[2.5 Connexions Real-Time CDP : transfert d’événement](./modules/delivery-activation/rtcdp-b2c/rtcdpb2c-5/aep-data-collection-ssf.md)

Dans ce module, vous allez transférer des données côté serveur vers plusieurs points d’entrée, tels que Google Cloud Platform Pub/Sub et AWS Kinesis.

[2.6 Diffuser des données d’Apache Kafka vers Real-Time CDP](./modules/delivery-activation/rtcdp-b2c/rtcdpb2c-6/aep-apache-kafka.md)

Dans ce module, vous apprendrez à configurer votre propre cluster Apache Kafka et à diffuser des données dans Adobe Experience Platform.

#### Adobe Journey Optimizer B2C

[3.1 Adobe Journey Optimizer : Orchestration](./modules/delivery-activation/ajo-b2c/ajob2c-1/journey-orchestration-create-account.md)

Dans ce module, vous utiliserez Adobe Journey Optimizer pour créer un parcours basé sur un déclencheur.

[3.2 Adobe Journey Optimizer : sources de données externes et actions personnalisées](./modules/delivery-activation/ajo-b2c/ajob2c-2/journey-orchestration-external-weather-api-sms.md)

Dans ce module, vous utiliserez Adobe Journey Optimizer pour écouter le comportement des clients, en ligne et hors ligne, et y répondre de manière intelligente, contextuelle et en temps réel sur divers canaux.

[3.3 Adobe Journey Optimizer : Offer Decisioning](./modules/delivery-activation/ajo-b2c/ajob2c-3/offer-decisioning.md)

Dans ce module, vous utiliserez Adobe Journey Optimizer pour configurer des offres personnalisées et votre propre décision d’offre.

[3.4 Adobe Journey Optimizer : Parcours basés sur un événement](./modules/delivery-activation/ajo-b2c/ajob2c-4/journeyoptimizer.md)

Dans ce module, vous apprendrez tout ce qu’il y a à savoir sur Journey Optimizer, qui aide les entreprises à concevoir et à proposer des expériences connectées, contextuelles et personnalisées à leurs clients.

[3.5 Adobe Journey Optimizer : services de traduction](./modules/delivery-activation/ajo-b2c/ajob2c-5/ajotranslationsvcs.md)

Dans ce module, vous apprendrez à configurer et à utiliser les services de traduction dans Adobe Journey Optimizer pour localiser vos messages à l’intention de vos clients.

### 5. Rapports et informations

#### Adobe Customer Journey Analytics

[1.1 Customer Journey Analytics : création d’un tableau de bord à l’aide d’Analysis Workspace sur Adobe Experience Platform](./modules/reporting-insights/cja-b2c/cjab2c-1/customer-journey-analytics-build-a-dashboard.md)

Dans ce module, vous obtiendrez des informations en ligne et hors ligne en configurant un tableau de bord contenant des données omnicanales.

[1.2 Customer Journey Analytics : ingestion et analyse de données Google Analytics dans Adobe Experience Platform avec le connecteur Source BigQuery](./modules/reporting-insights/cja-b2c/cjab2c-2/customer-journey-analytics-bigquery-gcp.md)

Dans ce module, vous allez configurer votre propre instance de Google Cloud Platform, charger des données de démonstration dans Google Cloud Platform, puis utiliser le connecteur Source BigQuery pour ingérer ces données de Google Cloud Platform dans Adobe Experience Platform.

#### Data Distiller

[2.1 Query Service](./modules/reporting-insights/datadistiller/dd-1/query-service.md)

Dans ce module, vous apprendrez à utiliser Adobe Experience Platform Query Service.

![Insiders de la technologie ](./assets/images/techinsiders.png){width="50px" align="left"}

>[!NOTE]
>
>Si vous avez des questions, si vous souhaitez partager des commentaires généraux ou si vous avez des suggestions sur le contenu futur, veuillez contacter directement les initiés techniques, en envoyant un e-mail à **techinsiders@adobe.com**.
