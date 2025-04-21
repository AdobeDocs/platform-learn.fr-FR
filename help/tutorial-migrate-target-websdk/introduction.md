---
title: Migration de Target d’at.js 2.x vers Web SDK
description: Découvrez comment migrer une implémentation Adobe Target d’at.js 2.x vers Adobe Experience Platform Web SDK. Les rubriques incluent le chargement de la bibliothèque JavaScript, les paramètres d’envoi, les activités de rendu et d’autres légendes importantes.
last-substantial-update: 2023-02-23T00:00:00Z
exl-id: c8920fde-ad6b-4f2d-a35f-ce865b35bba0
source-git-commit: e0359d1bade01f79d0f7aff6a6e69f3e4d0c3b62
workflow-type: tm+mt
source-wordcount: '611'
ht-degree: 5%

---

# Migration de Target d’at.js 2.x vers Platform Web SDK

Ce guide est destiné aux personnes expérimentées dans la mise en œuvre d’Adobe Target. Elles doivent apprendre à migrer une mise en œuvre at.js vers Adobe Experience Platform Web SDK.

Adobe Experience Platform Web SDK est une bibliothèque JavaScript côté client qui permet aux clients Adobe Experience Cloud d’interagir avec les services Experience Cloud via Adobe Experience Platform Edge Network. Cette nouvelle bibliothèque regroupe les fonctionnalités des différentes bibliothèques d’applications Adobe dans un package léger unique qui peut tirer pleinement parti des nouvelles fonctionnalités de Adobe Experience Platform.


>[!NOTE]
>
>Des tutoriels de migration similaires sont disponibles pour :
>
> * [Adobe Analytics](../tutorial-migrate-analytics-websdk/migration-to-websdk-overview.md)
> * [Adobe Audience Manager](https://experienceleague.adobe.com/en/docs/audience-manager/user-guide/migrate-to-web-sdk/appmeasurement-to-web-sdk)

>[!CAUTION]
>
> Étant donné que Platform Web SDK prend en charge plusieurs applications Adobe, toutes les bibliothèques Adobe d’une page donnée doivent être migrées en même temps. Par exemple, une implémentation mixte de Web SDK for Target et d’AppMeasurement for Analytics sur une seule page _n’est pas prise en charge_. Cependant, une implémentation mixte est prise en charge sur différentes pages, par exemple Web SDK sur la page A et at.js avec AppMeasurement sur la page B.



## Avantages clés

Voici quelques-uns des avantages de Platform Web SDK par rapport à la bibliothèque at.js autonome :

* Partage plus rapide des audiences depuis [Real-Time Customer Data Platform](https://experienceleague.adobe.com/en/docs/platform-learn/tutorials/destinations/target/next-hit-personalization)
* Intégration de Target à Journey Optimizer pour prendre en charge la diffusion [Offer Decisioning](https://experienceleague.adobe.com/en/docs/target/using/integrate/ajo/offer-decision)
* Possibilité d’utiliser des [identifiants propriétaires](https://experienceleague.adobe.com/en/docs/platform-learn/data-collection/edge-network/generate-first-party-device-ids) pour générer l’ECID en vue d’une identification des visiteurs de plus longue durée
* Un encombrement réduit pour des mesures de vitesse de page améliorées
* Flexibilité d’implémentation supplémentaire pour les développeurs

L’avantage le plus important de la migration pour les clients Target est sans doute l’intégration à Real-Time Customer Data Platform. Real-Time CDP offre d’incroyables fonctionnalités de création d’audiences basées sur l’ensemble des données ingérées dans Experience Platform et sa fonctionnalité de profil client en temps réel. Un cadre de gouvernance des données intégré automatise l’utilisation responsable de ces données. L’IA dédiée aux clients vous permet d’utiliser facilement des modèles de machine learning pour construire des modèles de propension et d’attrition dont la sortie peut être partagée avec Adobe Target. Enfin, les clients des modules complémentaires facultatifs Healthcare et Privacy &amp; Security Shield peuvent utiliser la fonctionnalité d’application du consentement pour appliquer facilement les préférences de consentement des clients individuels. Platform Web SDK est obligatoire pour utiliser ces fonctionnalités Real-Time CDP dans votre canal web.

## Objectifs d’apprentissage

À la fin de cette leçon, vous serez à même d’effectuer les actions suivantes :

* Comprendre les différences d’implémentation de Target entre at.js et Platform Web SDK
* Configurer la configuration initiale de la fonctionnalité Target
* Mettre à niveau la bibliothèque at.js vers Platform Web SDK
* Rendu des activités basées sur les formulaires et du compositeur d’expérience visuelle
* Transmission de paramètres à Target
* Suivi des événements de conversion
* Activer la prise en charge inter-domaines
* Mise à jour des audiences et des scripts de profil
* Valider la mise en œuvre
* Déboguer la diffusion de l’expérience Target


## Conditions préalables

Pour suivre ce tutoriel, vous devez d’abord :

* Posséder une compréhension technique de votre implémentation actuelle de Target at.js ;
* Assurez-vous de disposer d’un [rôle Éditeur ou Éditeur](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/enterprise/properties-overview.html#section_8C425E43E5DD4111BBFC734A2B7ABC80) pour votre instance Target afin de pouvoir tenter d’obtenir des exemples par vous-même
* Savoir comment configurer des activités dans Adobe Target. Si vous avez besoin d’un rappel, les tutoriels et guides suivants sont utiles pour cette leçon :
   * [Utilisation du Compositeur d’expérience visuelle](https://experienceleague.adobe.com/docs/target-learn/tutorials/experiences/use-the-visual-experience-composer.html)
   * [Utilisation du compositeur d’expérience d’après les formulaires](https://experienceleague.adobe.com/docs/target-learn/tutorials/experiences/use-the-form-based-experience-composer.html)
   * [Créer des activités de ciblage d’expérience](https://experienceleague.adobe.com/docs/target-learn/tutorials/activities/create-experience-targeting-activities.html)

Une fois que vous êtes prêt(e), la première étape d’une migration réussie consiste à [en savoir plus sur le processus de migration](migration-overview.md) et sur les différences entre at.js et Platform Web SDK.

>[!NOTE]
>
>Nous nous engageons à vous aider à réussir la migration de Target d’at.js vers Web SDK. Si vous rencontrez des obstacles avec votre migration ou si vous pensez qu&#39;il manque des informations essentielles dans ce guide, veuillez nous le faire savoir en postant dans [cette discussion communautaire](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-target-from-at-js-to-web-sdk/m-p/575587#M463).
