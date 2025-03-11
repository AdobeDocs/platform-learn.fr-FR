---
title: Migrez l’implémentation Adobe Target dans votre application mobile vers l’extension Adobe Journey Optimizer - Decisioning
description: Découvrez comment migrer l’implémentation de votre application mobile d’Adobe Target vers l’extension Adobe Journey Optimizer - Decisioning
last-substantial-update: 2023-02-23T00:00:00Z
exl-id: 32363b95-b6ad-44af-a3b0-e1fbbbf5a8f1
source-git-commit: b8baa6d48b9a99d2d32fad2221413b7c10937191
workflow-type: tm+mt
source-wordcount: '656'
ht-degree: 0%

---

# Migrez l’implémentation Adobe Target dans votre application mobile vers l’extension Adobe Journey Optimizer - Decisioning

Ce guide est destiné aux personnes expérimentées en mise en œuvre d’Adobe Target. Elles doivent apprendre à migrer les mises en œuvre de SDK mobiles d’Adobe Experience Platform existantes de l’extension Adobe Target vers l’extension Adobe Journey Optimizer - Prise de décision.

Adobe Experience Platform Mobile SDK optimise l&#39;engagement de bout en bout dans vos applications mobiles. L’extension Target s’appuie sur Mobile SDK pour vous aider à personnaliser les expériences d’application avec Adobe Target. L’extension Decisioning est une approche plus récente de l’implémentation d’Adobe Target dans les applications mobiles qui utilise les fonctionnalités de Adobe Experience Platform Edge Network pour intégrer Target aux applications basées sur Platform telles que Real-Time CDP et Journey Optimizer.

![Diagramme montrant la connexion de Mobile SDK à Target par le biais d’Edge Network avec l’extension Decisioning](assets/datacollection.png)

>[!INFO]
>
>Dans l’écosystème Adobe Experience Platform Mobile SDK, les extensions sont implémentées par des SDK importés dans vos applications, qui peuvent porter des noms différents :
>
> * **Target SDK** met en œuvre l’extension **Adobe Target**
> * **Optimiser SDK** implémente l’extension **Adobe Journey Optimizer - Decisioning**


## Avantages clés

Voici quelques-uns des avantages de l’extension Adobe Journey Optimizer Decisioning par rapport à l’extension Target :

* Partage plus rapide des audiences depuis [Real-Time Customer Data Platform](https://experienceleague.adobe.com/docs/platform-learn/tutorials/experience-cloud/next-hit-personalization.html?lang=fr)
* Intégration de Target à Journey Optimizer pour prendre en charge la diffusion [Offer Decisioning](https://experienceleague.adobe.com/docs/target/using/integrate/ajo/offer-decision.html)
* Une intégration plus étroite à Adobe Analytics qui ne repose pas sur l’assemblage d’informations provenant d’appels réseau distincts
* Flexibilité d’implémentation supplémentaire pour les développeurs

L’avantage le plus important de la migration pour les clients Target est sans doute l’intégration à Real-Time Customer Data Platform. Real-Time CDP offre d’incroyables fonctionnalités de création d’audiences basées sur l’ensemble des données ingérées dans Experience Platform et sa fonctionnalité de profil client en temps réel. Un cadre de gouvernance des données intégré automatise l’utilisation responsable de ces données. L’IA dédiée aux clients vous permet d’utiliser facilement des modèles de machine learning pour construire des modèles de propension et d’attrition dont la sortie peut être partagée avec Adobe Target. Enfin, les clients des modules complémentaires facultatifs Healthcare et Privacy &amp; Security Shield peuvent utiliser la fonctionnalité d’application du consentement pour appliquer les préférences de consentement des clients individuels. Platform Mobile SDK et l’extension Decisioning sont nécessaires pour utiliser ces fonctionnalités Real-Time CDP dans votre canal mobile.

## Étapes de migration

Le niveau d’effort à fournir pour migrer de l’extension Target à l’extension Decisioning dépend de la complexité de votre implémentation actuelle et des fonctionnalités Target utilisées.

Quelle que soit la simplicité ou la complexité de votre implémentation, il est important de bien comprendre votre état actuel avant la migration. Ce guide vous aide à ventiler les composants de votre implémentation actuelle et à développer un plan gérable pour migrer chaque élément.

Le processus de migration implique les étapes clés suivantes :

1. Évaluation de votre implémentation actuelle
1. Configurer les composants initiaux pour la connexion à Adobe Experience Platform Edge Network
1. Mettez à jour la mise en œuvre de base pour remplacer l’extension Target par l’extension Decisioning
1. Améliorez l’implémentation de SDK pour vos cas d’utilisation spécifiques. Cela peut impliquer la transmission de paramètres supplémentaires, l’utilisation de jetons de réponse, etc.
1. Mettre à jour des objets dans l’interface Target, tels que des scripts de profil, des activités et des définitions d’audience
1. Validez la mise en œuvre finale avant d’effectuer le changement dans votre application de production.

>[!INFO]
>
>Dans l’écosystème Adobe Experience Platform Mobile SDK, les extensions sont implémentées par des SDK importés dans vos applications, qui peuvent porter des noms différents :
>
> * **Target SDK** met en œuvre l’extension **Adobe Target**
> * **Optimiser SDK** implémente l’extension **Adobe Journey Optimizer - Decisioning**

Ensuite, passez en revue la comparaison détaillée [de l’extension Target et de l’extension Decisioning](comparison.md) pour mieux comprendre les différences techniques et identifier les domaines nécessitant une attention supplémentaire.

>[!NOTE]
>
>Nous nous engageons à vous aider à réussir votre migration mobile de Target de l’extension Target vers l’extension Decisioning. Si vous rencontrez des obstacles avec votre migration ou si vous pensez qu&#39;il manque des informations essentielles dans ce guide, veuillez nous le faire savoir en postant dans [cette discussion communautaire](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-target-from-at-js-to-web-sdk/m-p/575587#M463).
