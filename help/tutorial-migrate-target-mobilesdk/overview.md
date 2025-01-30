---
title: Migration d’Adobe Target vers Adobe Journey Optimizer - Extension mobile Decisioning
description: Découvrez comment migrer l’implémentation de votre application mobile d’Adobe Target vers l’extension Adobe Journey Optimizer - Decisioning
last-substantial-update: 2023-02-23T00:00:00Z
exl-id: 32363b95-b6ad-44af-a3b0-e1fbbbf5a8f1
source-git-commit: 6e442413c178e76183f88454d97d3896f8efa8bc
workflow-type: tm+mt
source-wordcount: '397'
ht-degree: 3%

---

# Migration d’Adobe Target vers Adobe Journey Optimizer - Extension mobile Decisioning

Ce guide est destiné aux personnes expérimentées en mise en œuvre d’Adobe Target. Elles doivent apprendre à migrer les mises en œuvre de SDK mobiles d’Adobe Experience Platform existantes de l’extension Adobe Target vers l’extension Adobe Journey Optimizer - Prise de décision.

Adobe Experience Platform Mobile SDK optimise l&#39;engagement de bout en bout dans vos applications mobiles. L’extension Target s’appuie sur Mobile SDK pour vous aider à personnaliser les expériences d’application avec Adobe Target. L’extension Decisioning est une approche plus récente de l’implémentation d’Adobe Target dans les applications mobiles qui utilise les fonctionnalités de Adobe Experience Platform Edge Network pour intégrer Target aux applications basées sur Platform telles que Real-Time CDP et Journey Optimizer.

## Avantages clés

Voici quelques-uns des avantages de l’extension Decisioning :

* Partage plus rapide des audiences depuis [Real-Time Customer Data Platform](https://experienceleague.adobe.com/docs/platform-learn/tutorials/experience-cloud/next-hit-personalization.html?lang=fr)
* Intégration de Target à Journey Optimizer pour prendre en charge la diffusion en Offer decisioning [](https://experienceleague.adobe.com/docs/target/using/integrate/ajo/offer-decision.html)
* Une intégration plus étroite à Adobe Analytics qui ne repose pas sur l’assemblage d’informations provenant d’appels réseau distincts
* Flexibilité d’implémentation supplémentaire pour les développeurs

L’avantage le plus important de la migration pour les clients Target est sans doute l’intégration à Real-Time Customer Data Platform. Real-Time CDP offre d’énormes fonctionnalités de création d’audiences basées sur l’ensemble des données ingérées dans Experience Platform et sa fonctionnalité de profil client en temps réel. Un cadre de gouvernance des données intégré automatise l’utilisation responsable de ces données. L’IA dédiée aux clients vous permet d’utiliser facilement des modèles de machine learning pour construire des modèles de propension et d’attrition dont la sortie peut être partagée avec Adobe Target. Enfin, les clients des modules complémentaires facultatifs Healthcare et Privacy &amp; Security Shield peuvent utiliser la fonctionnalité d’application du consentement pour appliquer facilement les préférences de consentement des clients individuels. Platform Mobile SDK et l’extension Decisioning sont nécessaires pour utiliser ces fonctionnalités Real-Time CDP dans votre canal mobile.

## Objectifs d’apprentissage

À la fin de cette leçon, vous serez à même d’effectuer les actions suivantes :

* Puce 1
* Puce 2


## Conditions préalables

Pour suivre ce tutoriel, vous devez d’abord :

* Puce 1
* Puce 2


>[!NOTE]
>
>Nous nous engageons à vous aider à réussir votre migration mobile de Target de l’extension Target vers l’extension Decisioning. Si vous rencontrez des obstacles avec votre migration ou si vous pensez qu&#39;il manque des informations essentielles dans ce guide, veuillez nous le faire savoir en postant dans [cette discussion communautaire](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-target-from-at-js-to-web-sdk/m-p/575587#M463).
