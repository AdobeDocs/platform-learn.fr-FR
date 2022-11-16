---
title: Présentation
description: Point de départ pour les ingénieurs de données, les analystes de données, les architectes de données, les spécialistes des données, les ingénieurs d’orchestration et les spécialistes du marketing afin de mieux comprendre la valeur commerciale de Adobe Experience Platform et de tous ses services d’application.
doc-type: multipage-overview
hide: false
exl-id: 88c19383-c185-40f0-b118-6cb82db0ce0e
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '1869'
ht-degree: 2%

---

# Tutoriel technique complet d’Adobe Experience Platform

## Présentation

Ce tutoriel est le point de départ idéal pour les ingénieurs de données, les analystes de données, les architectes de données, les spécialistes des données, les ingénieurs d’orchestration et les spécialistes du marketing afin de mieux comprendre la valeur commerciale de Adobe Experience Platform et de tous ses services d’application. Chaque leçon se concentre sur un véritable défi auquel les entreprises sont confrontées dans l&#39;écosystème complexe de personnalisation d&#39;aujourd&#39;hui, et révèle comment les Experience Platform résolvent ce défi dans le cadre de divers exercices pratiques. Regardez cette vidéo pour comprendre les problèmes que Adobe Experience Platform vous aidera à résoudre.

>[!VIDEO](https://video.tv.adobe.com/v/344237?quality=12&enable=on)

Ce tutoriel est très varié et offre des informations claires dans les applications suivantes :

- Adobe Experience Platform
- Collecte de données dʼAdobe Experience Platform
- Real-time CDP
- Adobe Journey Optimizer
- Customer Journey Analytics
- Offer Decisioning

Ce tutoriel ne se concentre pas seulement sur les applications d’Adobe, mais tient compte de l’écosystème élargi dans lequel les marques opèrent. Pour ce faire, dans certaines leçons, on se concentre sur la façon dont _non-Adobe_ les applications s’intègrent à Adobe Experience Platform. Vous aurez ainsi une bonne compréhension de la manière dont les applications suivantes fonctionneront avec Adobe Experience Platform :

- Amazon : AWS Lambda, AWS S3, AWS Kinesis
- Google : Google Cloud Platform, Google BigQuery, Google Display&amp;Video 360, Google AdWords
- Microsoft : Power BI, Azure EventHub, stockage Azure Blob
- Salesforce : Tableau
- Apache Kafka
- Postman
- ...

Après avoir terminé ce tutoriel, vous serez en mesure de :

- Configuration de schémas, de mixins, de jeux de données et d’identités
- Configurez une propriété de collecte de données Adobe Experience Platform et configurez la nouvelle extension du SDK Web dans la collecte de données Adobe Experience Platform.
- Diffusez des données dans Adobe Experience Platform en temps réel à l’aide de la collecte de données Adobe Experience Platform, du gestionnaire de balises Google ou d’Amazon Alexa.
- Ingestion par lots de données dans Adobe Experience Platform à l’aide d’un workflow ou d’une application d’extraction, de transformation et de chargement (ETL)
- Visualisation et utilisation du profil client en temps réel dans Adobe Experience Platform
- Créer des segments
- Utilisation de plusieurs API Adobe Experience Platform
- Utiliser SQL pour interroger vos données dans Adobe Experience Platform
- Configuration, formation et notation de modèles d’apprentissage automatique dans Adobe Experience Platform
- Utilisation de Journey Orchestration pour configurer des parcours en temps réel basés sur un déclencheur
- Utiliser la plateforme de données clients en temps réel pour agir en activant un segment vers différentes destinations
- Utilisez Customer Journey Analytics pour créer des rapports sur les données clients omnicanal provenant de diverses sources, y compris Google BigQuery

## Conditions préalables

- Accès à Adobe Experience Platform : [https://experience.adobe.com/platform](https://experience.adobe.com/platform)
- Accès à la collecte de données Adobe Experience Platform : [https://experience.adobe.com/#/data-collection/](https://experience.adobe.com/#/data-collection/)
- Accès au système de démonstration : [https://dashboard.adobedemo.com/](https://dashboard.adobedemo.com/)

>[!IMPORTANT]
>
>Ce tutoriel a été créé pour faciliter un format d’atelier particulier. Il utilise des systèmes et des comptes spécifiques auxquels vous n’avez peut-être pas accès. Même sans accès, nous pensons que vous pouvez encore apprendre beaucoup en lisant à travers ce contenu très détaillé. Si vous participez à l’un des ateliers et que vous avez besoin de vos informations d’identification d’accès, veuillez contacter votre représentant d’Adobe qui vous fournira les informations requises.

## À propos de ce tutoriel

Dans ces leçons, vous allez mettre en oeuvre Adobe Experience Platform et Application Services à l’aide d’un site web de démonstration qui prend en charge plusieurs secteurs d’activité. Le site web de démonstration et l’application mobile disposent d’une couche de données et de fonctionnalités riches qui vous permettront de créer une mise en oeuvre réaliste. Il permet d’accéder aux marques de démonstration telles que **Luma**, **Signal Citi**, **EXP News**, **MUTUAL365**, **Carvelo** et plusieurs autres. Vous allez créer votre propre propriété Adobe Experience Platform Data Collection Client, dans votre propre organisation Experience Cloud, et la mapper à votre site web de démonstration. Cela génère ensuite des données envoyées dans votre propre instance Adobe Experience Platform.

## Architecture

Avant de commencer avec les exercices pratiques, consultez l’ architecture derrière ce tutoriel. Comme vous pouvez le constater dans l’aperçu ci-dessus, ce tutoriel abordera en détail un certain nombre de fonctionnalités de Adobe Experience Platform, mais abordera également plusieurs intégrations dans diverses sources et destinations. Pour bien comprendre l’architecture de ce tutoriel et le positionnement global de Adobe Experience Platform dans votre écosystème d’entreprise, commencez par consulter la vidéo et le diagramme d’architecture.

Accédez à [Architecture](./architecture.md).


## Vidéos

Vidéos sur ![](./assets/images/yt.jpeg)

Vous pouvez trouver de nombreuses vidéos intéressantes de nos événements de l&#39;Académie des Technologies, de Bootcamps et plus sur nos [Canal YouTube de la communauté des créateurs d’expérience](https://www.youtube.com/channel/UCUKG2dkZ9pYuZUPebQ21jUw).

Plusieurs vidéos ont été créées, qui présentent des éléments de l’activation et des intégrations puissantes entre Adobe Experience Platform et les applications non Adobes. Cliquez sur le lien ci-dessous pour obtenir un aperçu de ces vidéos.

Accédez à [Vidéos](./videos.md).



## Comment mesure-t-on la fin du tutoriel technique complet de Adobe Experience Platform ?

Si vous participez à ce tutoriel en tant que partenaire d’Adobe ou employé d’Adobe, vous devez soumettre votre progression après avoir terminé chaque module d’activation.

Vous trouverez les conditions requises et le processus pour envoyer la fin de l’opération ici : [Mesurer la fin](./completion.md)

## Contenu

[0. Prise en main](./modules/module0/getting-started.md)

- **Public :** Tous les participants au tutoriel technique complet de Adobe Experience Platform
- **Conditions préalables :** Accès à Demo System Next, Adobe Experience Platform et à la collecte de données Adobe Experience Platform. Accès à l’identifiant de configuration par défaut de votre environnement Adobe Experience Platform.
- **Description :** Dans ce module de base, vous allez tout configurer pour pouvoir accéder à l’environnement de démonstration et l’utiliser.
- **Time Investment :** 30 minutes

[1. Foundation - Configuration de la collecte de données Adobe Experience Platform et du SDK web](./modules/module1/data-ingestion-launch-web-sdk.md)

- **Public :** Ingénieur de données, architecte de données
- **Conditions préalables :** Accès à la collecte de données Adobe Experience Platform et Adobe Experience Platform.
- **Description :** Dans ce module de base, vous découvrirez la collecte de données Adobe Experience Platform et la nouvelle extension du SDK Web.
- **Time Investment :** 30 minutes

[2. Foundation - Ingestion des données](./modules/module2/data-ingestion.md)

- **Public :** Ingénieur de données, architecte de données
- **Conditions préalables :** Accès à la collecte de données Adobe Experience Platform et Adobe Experience Platform.
- **Description :** Dans ce module de base, vous allez ingérer des données du site web dans Platform.
- **Time Investment :** 120 minutes

[3. Foundation - Profil client en temps réel](./modules/module3/real-time-customer-profile.md)

- **Public :** Ingénieur de données, architecte de données, marketeur
- **Conditions préalables :** Accès à Adobe Experience Platform et Postman
- **Description :** Dans ce module de base, vous allez explorer Real-time Customer Profile dans Adobe Experience Platform en utilisant l’interface utilisateur et l’API.
- **Time Investment :** 90 minutes
- **Téléchargement de ces ressources**:
   - [Collections Postman](./assets/postman/postman_profile.zip)

[4. Query Service](./modules/module4/query-service.md)

- **Public :** Ingénieur de données, architecte de données, analyste de données, expert BI
- **Conditions préalables :** Accès à Adobe Experience Platform, Query Service, Power BI ou Tableau
- **Description :** Dans ce module, vous apprendrez à utiliser Adobe Experience Platform Query Service.
- **Time Investment :** 90 minutes
- **Téléchargement de ces ressources**:
   - [JSON - Exemple de données : Système de démonstration - Jeu de données d’événement pour le site web](./assets/json/ee.json)
   - [JSON - Exemple de données : Système de démonstration - Jeu de données d’événement pour le centre d’appels](./assets/json/callcenter.json)
   - [JSON - Exemple de données : Système de démonstration - Jeu de données de profil pour la fidélité](./assets/json/loyalty.json)

[5. Intelligent Services](./modules/module5/intelligent-services.md)

- **Public :** Ingénieur de données, architecte de données, spécialiste des données
- **Conditions préalables :** Accès à Adobe Experience Platform, services intelligents
- **Description :** Dans ce module, vous apprendrez à configurer et à utiliser les services intelligents Adobe Experience Platform.
- **Time Investment :** 60 minutes

[6. Real-Time CDP : créer un segment et agir](./modules/module6/real-time-cdp-build-a-segment-take-action.md)

- **Public :** Architecte de données, ingénieur d’orchestration, marketeur
- **Conditions préalables :** Accès à Adobe Experience Platform, la plateforme de données clients en temps réel, Adobe Audience Manager, Adobe Target, AWS S3
- **Description :** Dans ce module, vous allez configurer un segment, l’activer pour la segmentation par flux et activer le segment vers plusieurs destinations, y compris Google DV360, Google AdWords, Adobe Audience Manager, Adobe Target et S3-destinations comme le Marketing Cloud Salesforce.
- **Time Investment :** 90 minutes

[7. Adobe Journey Optimizer : Orchestration](./modules/module7/journey-orchestration-create-account.md)

- **Public :** Ingénieur de données, architecte de données, ingénieur d’orchestration
- **Conditions préalables :** Accès à Adobe Experience Platform et Adobe Journey Optimizer
- **Description :** Dans ce module, vous utiliserez Adobe Journey Optimizer pour créer un parcours basé sur un déclencheur.
- **Time Investment :** 60 minutes

[8. Adobe Journey Optimizer : Sources de données externes et actions personnalisées](./modules/module8/journey-orchestration-external-weather-api-sms.md)

- **Public :** Ingénieur de données, architecte de données, ingénieur d’orchestration, marketeur
- **Conditions préalables :** Accès à Adobe Experience Platform, Adobe Journey Optimizer, API Open Weather, Twilio
- **Description :** Dans ce module, vous utiliserez Adobe Journey Optimizer pour écouter le comportement des clients, en ligne et hors ligne, et y répondre de manière intelligente, contextuelle et en temps réel sur divers canaux.
- **Time Investment :** 90 minutes

[9. Adobe Journey Optimizer : offer decisioning](./modules/module9/offer-decisioning.md)

- **Public :** Ingénieur de données, architecte de données, ingénieur d’orchestration, marketeur
- **Conditions préalables :** Accès à Adobe Experience Platform et à Offer Decisioning
- **Description :** Dans ce module, vous utiliserez le service d’application Adobe Experience Platform - Offres/prise de décision de manière pratique pour configurer les offres personnalisées et votre propre activité d’offre.
- **Time Investment :** 120 minutes

[10. Adobe Journey Optimizer : Parcours basés sur un événement](./modules/module10/journeyoptimizer.md)

- **Public :** Marketer d’email, spécialiste d’orchestration, ingénieur de données, architecte de données, analyste de données
- **Conditions préalables :** Accès à Adobe Experience Platform et Journey Optimizer
- **Description :** Dans ce module, vous découvrirez tout ce que vous devez savoir sur Journey Optimizer, qui permet aux entreprises de concevoir et de proposer à leurs clients des expériences connectées, contextuelles et personnalisées.
- **Time Investment :** 120 minutes

[11. Customer Journey Analytics : Création d’un tableau de bord à l’aide d’Analysis Workspace sur Adobe Experience Platform](./modules/module11/customer-journey-analytics-build-a-dashboard.md)

- **Public :** Ingénieur de données, architecte de données, analyste de données
- **Conditions préalables :** Accès à Adobe Experience Platform et Customer Journey Analytics
- **Description :** Dans ce module, vous obtiendrez des informations en ligne vers les informations hors ligne en configurant un tableau de bord contenant des données omnicanal telles que Interactions de site web, Interactions d’applications mobiles, Interactions du centre d’appels, Interactions en magasin, etc.
- **Time Investment :** 120 minutes

[12. Customer Journey Analytics : Ingestion et analyse de données Google Analytics dans Adobe Experience Platform à l’aide du connecteur source BigQuery](./modules/module12/customer-journey-analytics-bigquery-gcp.md)

- **Public :** Ingénieur de données, architecte de données, analyste de données
- **Conditions préalables :** Accès à Adobe Experience Platform, Customer Journey Analytics, Google Cloud Platform, Google BigQuery
- **Description :** Dans ce module, vous allez configurer votre propre instance de Google Cloud Platform, charger les données de démonstration dans Google Cloud Platform et vous utiliserez ensuite le connecteur source BigQuery pour ingérer ces données de Google Cloud Platform dans Adobe Experience Platform. Enfin, vous utiliserez Customer Journey Analytics pour visualiser ces données.
- **Time Investment :** 120 minutes
- **Téléchargement de ces ressources**:
   - [JSON - Exemple de données : Démo - Données de fidélité](./assets/json/bqLoyalty.json)

[13. Real-Time CDP : Activation de segment vers Microsoft Azure Event Hub](./modules/module13/segment-activation-microsoft-azure-eventhub.md)

- **Public :** Ingénieur de données, architecte de données, analyste de données
- **Conditions préalables :** Accès à Adobe Experience Platform, à la plateforme de données clients en temps réel et à Microsoft Azure
- **Description :** Dans ce module, vous allez configurer une destination Microsoft Azure EventHub en tant que destination en temps réel pour la plateforme de données clients en temps réel de Adobe Experience Platform. Vous allez également configurer et déployer une fonction Azure qui sera déclenchée en temps réel chaque fois que Adobe Experience Platform envoie une charge utile de segment à votre destination Azure EventHub. La fonction Azure que vous allez déclencher affiche le mécanisme des fonctionnalités d’activation de la plateforme de données clients en temps réel de Adobe Experience Platform.
Dans le cadre de ce module, vous comprendrez également ce qui déclenche la diffusion d’une charge utile en temps réel sur une destination spécifiée par la plateforme CDP en temps réel. Nous discuterons également de l’état d’une qualification de segment et de sa relation avec l’activation.
- **Time Investment :** 90 minutes

[14. Connexions Real-Time CDP : Transfert d’événement](./modules/module14/aep-data-collection-ssf.md)

- **Public :** Ingénieur de données, architecte de données, analyste de données
- **Conditions préalables :** Accès aux propriétés de connexion Real-Time CDP, de balises et de transfert d’événements
- **Description :** Dans ce module, vous utiliserez les jeux de données, schémas et propriétés de collecte de données Adobe Experience Platform configurés précédemment pour collecter des données, puis vous transférerez ces données côté serveur à un point de terminaison de votre choix.
- **Time Investment :** 90 minutes

[15. Diffusez les données d’Apache Kafka vers Real-Time CDP.](./modules/module15/aep-apache-kafka.md)

- **Public :** Analyste de données, ingénieur de données, architecte de données
- **Conditions préalables :** Accès à Adobe Experience Platform
- **Description :** Dans ce module, vous apprendrez à configurer votre propre grappe Apache Kafka, à définir des rubriques, des producteurs et des consommateurs et à diffuser des données dans Adobe Experience Platform à l’aide de Adobe Experience Platform Sink Connector for Kafka Connect.
- **Time Investment :** 90 minutes

>[!NOTE]
>
>Merci d&#39;investir votre temps dans l&#39;apprentissage de Adobe Experience Platform. Si vous avez des questions, souhaitez partager les commentaires généraux d&#39;avoir des suggestions sur le contenu futur, contactez directement Wouter Van Geluwe en envoyant un email à **vangeluw@adobe.com**.
