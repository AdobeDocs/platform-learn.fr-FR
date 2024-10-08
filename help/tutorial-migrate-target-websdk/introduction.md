---
title: Migration de Target depuis at.js 2.x vers le SDK Web
description: Découvrez comment migrer une mise en oeuvre Adobe Target d’at.js 2.x vers le SDK Web Adobe Experience Platform. Les rubriques incluent le chargement de la bibliothèque JavaScript, l’envoi de paramètres, les activités de rendu et d’autres légendes à noter.
last-substantial-update: 2023-02-23T00:00:00Z
exl-id: c8920fde-ad6b-4f2d-a35f-ce865b35bba0
source-git-commit: eebe598e55228d038dfc2adb97df0f8ff03748ac
workflow-type: tm+mt
source-wordcount: '556'
ht-degree: 4%

---

# Migration de Target depuis at.js 2.x vers le SDK Web Platform

Ce guide est destiné aux implémentateurs expérimentés d’Adobe Target pour savoir comment migrer une implémentation d’at.js vers le SDK Web de Adobe Experience Platform.

Le SDK Web de Adobe Experience Platform est une bibliothèque JavaScript côté client qui permet aux clients Adobe Experience Cloud d’interagir avec les services Experience Cloud via l’Edge Network Adobe Experience Platform. Cette nouvelle bibliothèque combine les fonctionnalités des bibliothèques d’applications Adobe distinctes en un seul module léger pouvant tirer pleinement parti des nouvelles fonctionnalités de Adobe Experience Platform.

## Avantages clés

Voici quelques-uns des avantages du SDK Web Platform par rapport à la bibliothèque at.js autonome :

* Partage plus rapide des audiences à partir de [Real-Time Customer Data Platform](https://experienceleague.adobe.com/docs/platform-learn/tutorials/experience-cloud/next-hit-personalization.html?lang=fr)
* Intégration de Target à Journey Optimizer pour la prise en charge de [diffusion d’Offer decisioning](https://experienceleague.adobe.com/docs/target/using/integrate/ajo/offer-decision.html)
* Possibilité d’utiliser des [identifiants propriétaires](https://experienceleague.adobe.com/docs/platform-learn/data-collection/edge-network/generate-first-party-device-ids.html?lang=fr) pour générer l’ECID pour une identification des visiteurs de plus longue durée
* Consolidation des appels réseau entre les applications Adobe
* Plus petit encombrement pour des mesures de vitesse de page améliorées
* Une intégration plus étroite avec Adobe Analytics qui ne repose pas sur l’assemblage d’informations à partir d’appels réseau distincts
* Plus de flexibilité pour la mise en oeuvre pour les développeurs

La migration présente sans doute le plus grand avantage pour les clients Target : son intégration à Real-Time Customer Data Platform. Real-Time CDP offre d’immenses fonctionnalités de création d’audiences en fonction de l’ensemble des données ingérées dans Experience Platform et de ses fonctionnalités de profil client en temps réel. Un cadre de gouvernance des données intégré automatise l’utilisation responsable de ces données. Customer AI vous permet d’utiliser facilement des modèles d’apprentissage automatique pour construire des modèles de propension et d’attrition dont la sortie peut être partagée à nouveau vers Adobe Target. Enfin, les clients des ajouts facultatifs Health care, Privacy &amp; Security Shield peuvent utiliser la fonctionnalité d’application du consentement pour appliquer facilement les préférences de consentement des clients individuels. Le SDK Web Platform est une exigence pour l’utilisation de ces fonctionnalités RTCDP dans votre canal web.

## Objectifs d&#39;apprentissage

À la fin de cette leçon, vous serez à même d’effectuer les actions suivantes :

* Comprendre les différences d’implémentation de Target entre at.js et le SDK Web Platform
* Configuration initiale de la fonctionnalité Target
* Mise à niveau de la bibliothèque at.js vers le SDK Web Platform
* Rendu des activités de compositeur d’expérience visuelle et d’après les formulaires
* Transfert de paramètres à Target
* Suivi des événements de conversion
* Activation de la prise en charge inter-domaines
* Mise à jour des audiences et des scripts de profil
* Valider la mise en œuvre
* Déboguer la diffusion de l’expérience Target


## Conditions préalables

Pour terminer ce tutoriel, vous devez d’abord :

* avoir une compréhension technique de votre implémentation actuelle d’at.js Target ;
* Assurez-vous que vous disposez du [rôle d’éditeur ou d’éditeur](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/enterprise/properties-overview.html#section_8C425E43E5DD4111BBFC734A2B7ABC80) pour votre instance Target afin que vous puissiez essayer des exemples vous-même.
* Découvrez comment configurer des activités dans Adobe Target. Si vous avez besoin d’une actualisation, les tutoriels et guides suivants sont utiles pour cette leçon :
   * [Utilisation du Compositeur d’expérience visuelle](https://experienceleague.adobe.com/docs/target-learn/tutorials/experiences/use-the-visual-experience-composer.html)
   * [Utilisation du compositeur d’expérience d’après les formulaires](https://experienceleague.adobe.com/docs/target-learn/tutorials/experiences/use-the-form-based-experience-composer.html)
   * [Créer des activités de ciblage d’expérience](https://experienceleague.adobe.com/docs/target-learn/tutorials/activities/create-experience-targeting-activities.html)

Une fois que vous êtes prêt, la première étape d’une migration réussie consiste à [ découvrir le processus de migration](migration-overview.md) et les différences entre at.js et le SDK Web Platform.

>[!NOTE]
>
>Nous nous engageons à vous aider à réussir la migration de Target d’at.js vers le SDK Web. Si vous rencontrez des obstacles lors de votre migration ou si vous pensez qu’il manque des informations essentielles dans ce guide, faites-le-nous savoir en publiant sur [cette discussion communautaire](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-target-from-at-js-to-web-sdk/m-p/575587#M463).
