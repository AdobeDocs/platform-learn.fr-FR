---
title: Interagissez avec les audiences directement depuis votre entrepôt de données à l’aide de la présentation de la composition des audiences fédérées
description: La composition de l’audience fédérée est une puissante fonctionnalité qui permet aux architectes et aux ingénieurs de données de traiter et d’activer des audiences à forte valeur ajoutée directement à partir des entrepôts de données pris en charge.
breadcrumb-title: Vue d’ensemble
role: Data Architect, Data Engineer
jira: KT-18743
thumbnail: 18743-overview.jpg
recommendations: catalog, noDisplay
last-substantial-update: 2025-08-11T00:00:00Z
exl-id: 9d5a2e40-6cda-4164-87db-1bfffe3438e3
source-git-commit: ab9563d1ac4a0b97f45de0fd18186b34c98e2a36
workflow-type: tm+mt
source-wordcount: '575'
ht-degree: 0%

---

# Interagissez avec les audiences directement depuis votre entrepôt de données à l’aide de la présentation de la composition des audiences fédérées

Federated Audience Composition (FAC) est un module pour Adobe Real-Time Customer Data Platform (Real-Time CDP) et Adobe Journey Optimizer. Elle est également disponible avec les audiences composables Adobe Real-Time CDP (une solution sur mesure pour les clients sous la forme d’une plateforme de données clients composables). Il permet aux architectes et aux ingénieurs de données de traiter et d’activer des audiences à forte valeur ajoutée directement à partir d’[entrepôts de données d’entreprise pris en charge](https://experienceleague.adobe.com/fr/docs/federated-audience-composition/using/start/access-prerequisites){target="_blank"}, sans copier ni déplacer les données client dans Adobe Experience Platform (AEP). Cette approche CDP composable (une solution sur mesure pour les clients) s’aligne sur les tendances du secteur, ce qui permet aux entreprises d’exploiter leur infrastructure de données pour des expériences digitales personnalisées tout en maintenant la gouvernance des données.

## Contexte commercial

SecurFinancial est une société de services financiers de premier plan. Il tire parti de sa richesse de données client sur différentes sources pour personnaliser les offres et les campagnes pour un grand nombre de segments. Ils prévoient d’utiliser le module de composition d’audiences fédérées d’Adobe Real-Time CDP qui permet aux entreprises d’utiliser leur entrepôt de données à des fins de gestion des données tout en utilisant Adobe Experience Platform pour offrir des expériences client personnalisées. Les principaux avantages sont les suivants :

- **Accès aux données de l’entrepôt de données** : créez des audiences à forte valeur ajoutée à partir de jeux de données dans des entrepôts de données pris en charge sans réplication des données.
- **Mouvement de données réduit** : interrogez les données directement dans l’entrepôt de données, sans duplication et en maintenant la gouvernance des données.
- **Workflows d’expérience unifiée** : traitez et activez des audiences dans Adobe Experience Platform pour des cas d’utilisation cross-canal.
- **Personnalisation améliorée** : enrichissez les profils et les audiences avec des attributs d’entrepôt de données pour alimenter des expériences déclenchées en temps réel.

## Scénario d’entreprise

SecurFinancial souhaite lancer une campagne par e-mail pour recibler ses clients qui sont préqualifiés pour un prêt basé sur un bon crédit et n&#39;ont pas de prêt actif dans leur portefeuille SecurFinancial. Bien qu’ils ingèrent des données comportementales en ligne en temps réel, ils rencontrent des difficultés pour identifier la préqualification des clients, car ils ne peuvent pas ingérer d’informations de crédit dans AEP. Pour qualifier les clients préqualifiés sans déplacer les données restreintes, ils utiliseront la composition d’audience fédérée afin d’enrichir leur audience comportementale AEP.

## Guide

Ce guide explique comment nous prenons en charge le scénario SecureFinancial Business. Plus précisément, il couvre la manière dont nous exposons les audiences aux systèmes qui ont besoin de ces audiences, notamment un compte de stockage S3, un parcours dans Journey Optimizer pour générer une campagne par e-mail et un reciblage sur site pour les clients qui ont été préapprouvés pour un prêt.

Les étapes incluent :

1. Connectez Adobe Experience Platform à un entrepôt de données d’entreprise.
2. Créez une audience à l’aide de la composition d’audience fédérée.
3. Mappez une audience fédérée à une destination Amazon S3 externe.
4. Créez un parcours client à l’aide des données d’audience fédérée.
5. Enrichir une audience avec des données fédérées.
6. Pilotez la personnalisation « à la volée » sur Edge.

## Conditions préalables

Pour effectuer des activités similaires dans votre environnement, vérifiez que vous disposez des éléments suivants :

- Accès à un compte Adobe Experience Platform configuré avec Real-Time CDP ou Journey Optimizer.
- Autorisations d’administrateur système ou possibilité de configurer des autorisations.
- Connaissance des concepts Adobe Experience Platform tels que les schémas, les jeux de données et les audiences (recommandé : suivez la [Présentation de la liste de lecture Adobe Experience Platform](https://experienceleague.adobe.com/fr/playlists/experience-platform-introduction?lang=en){target="_blank"} sur Experience League).
- Accès à un [entrepôt de données d’entreprise](https://experienceleague.adobe.com/fr/docs/federated-audience-composition/using/start/access-prerequisites){target="_blank"} pris en charge.
- Connaissances de base de SQL pour interroger les entrepôts de données.
- **Environnements Sandbox** : créez un sandbox dans l’instance de votre organisation pour effectuer des tests en toute sécurité sans affecter les données de production.
- **Connexion Data Warehouse** : ce tutoriel utilise une connexion Snowflake, mais vous pouvez utiliser n’importe quel [entrepôt de données pris en charge](https://experienceleague.adobe.com/fr/docs/federated-audience-composition/using/start/access-prerequisites).

Tout d’abord, examinons la [Architecture de haut niveau et flux pour la composition d’audiences fédérées](fac-architecture-and-flow.md).
