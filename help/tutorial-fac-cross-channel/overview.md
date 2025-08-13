---
title: Déverrouiller les informations cross-canal avec la composition d’audiences fédérées
description: La composition de l’audience fédérée est une puissante fonctionnalité qui permet aux architectes et aux ingénieurs de données de créer et d’enrichir des audiences directement à partir d’entrepôts de données tiers.
breadcrumb-title: Aperçu
role: Data Architect, Data Engineer
jira: KT-18743
thumbnail: 18743-overview.jpg
recommendations: catalog, noDisplay
last-substantial-update: 2025-08-11T00:00:00Z
exl-id: 9d5a2e40-6cda-4164-87db-1bfffe3438e3
source-git-commit: a3c8d8b03472d01f491bf787ed647a696d3a5524
workflow-type: tm+mt
source-wordcount: '551'
ht-degree: 0%

---

# Aperçu

La composition de l’audience fédérée est une puissante fonctionnalité disponible pour les environnements Adobe Real-Time Customer Data Platform (Real-Time CDP) et Adobe Journey Optimizer. Il permet aux architectes de données et aux ingénieurs de données de créer et d’enrichir des audiences directement à partir d’entrepôts de données tiers [pris en charge](https://experienceleague.adobe.com/en/docs/federated-audience-composition/using/start/access-prerequisites){target="_blank"} sans répliquer les données dans Adobe Experience Platform. Ce tutoriel fournit des conseils pratiques aux utilisateurs et utilisatrices techniques pour connecter des entrepôts de données d’entreprise, créer et enrichir des audiences, et les activer pour offrir des expériences marketing personnalisées.

## Guide visuel

Ce guide visuel vous présente les étapes de chacune des activités entreprises pour prendre en charge divers aspects du scénario d’entreprise. L’objectif est de vous proposer des activités que vous pouvez exploiter dans votre environnement, notamment :

- Connectez Adobe Experience Platform à un entrepôt de données d’entreprise.
- Créez et gérez des audiences à l’aide de la composition d’audiences fédérées.
- Mappez les audiences fédérées à des destinations externes telles qu’Amazon S3.
- Enrichir les audiences existantes avec des données fédérées.
- Créez des audiences pour piloter la personnalisation « à l’instant ».
- Créez des parcours client à l’aide des données d’audience fédérées.

Ce guide est conçu pour les architectes et ingénieurs de données qui travaillent avec Real-Time CDP ou Journey Optimizer. Il suppose une connaissance des concepts de base de Adobe Experience Platform et de Data Warehouse.

## Contexte commercial

SecurFinancial est une société de services financiers de premier plan. Il tire parti de sa richesse de données client sur différentes sources pour personnaliser les offres et les campagnes pour un grand nombre de segments. Ils prévoient d’utiliser la fonctionnalité de composition d’audience fédérée d’Adobe Real-Time CDP qui permet aux entreprises d’utiliser leur entrepôt de données existant tout en utilisant les applications Adobe Experience Platform pour offrir des expériences client personnalisées. Les principaux avantages sont les suivants :

- **Accès aux données de l’entrepôt de données** : créez des audiences à forte valeur ajoutée à partir de jeux de données dans des entrepôts de données pris en charge sans réplication des données.
- **Mouvement des données réduit** : interrogez les données directement dans l’entrepôt de données, ce qui réduit la duplication et maintient la gouvernance des données.
- **Workflows d’expérience unifiée** : traitez et activez des audiences dans Adobe Experience Platform pour des cas d’utilisation cross-canal.
- **Personnalisation améliorée** : enrichissez les profils et les audiences avec des attributs d’entrepôt de données pour alimenter des expériences déclenchées en temps réel.

## Scénario d’entreprise

SecurFinancial souhaite lancer une campagne par e-mail pour recibler ses clients qui sont préqualifiés pour un prêt basé sur un bon crédit et n&#39;ont pas de prêt actif dans leur portefeuille SecurFinancial. Bien qu’ils ingèrent des données comportementales en ligne en temps réel, ils rencontrent des difficultés pour identifier la préqualification des clients, car ils ne peuvent pas ingérer d’informations de crédit dans AEP. Pour qualifier les clients préqualifiés sans déplacer les données restreintes, ils utiliseront la composition d’audience fédérée afin d’enrichir leur audience comportementale AEP.

## Conditions préalables

Pour effectuer des activités similaires dans votre environnement, vérifiez que vous disposez des éléments suivants :

- Accès à un compte Adobe Experience Platform configuré avec Real-Time CDP ou Journey Optimizer.
- Autorisations d’administrateur système ou possibilité de configurer des autorisations.
- Connaissance des concepts Adobe Experience Platform tels que les schémas, les jeux de données et les audiences (recommandé : suivez la [Présentation de la liste de lecture Adobe Experience Platform](https://experienceleague.adobe.com/en/playlists/experience-platform-introduction?lang=en){target="_blank"} sur Experience League).
- Accès à un entrepôt de données d’entreprise pris en charge (par exemple, Amazon Redshift, Azure Synapse Analytics, Snowflake ou Google BigQuery).
- Connaissances de base de SQL pour interroger les entrepôts de données.
- **Environnements Sandbox** : créez un sandbox dans l’instance Real-Time CDP de votre organisation pour effectuer des tests en toute sécurité sans affecter les données de production.
- **Connexion Data Warehouse** : ce tutoriel utilise une connexion Snowflake, mais vous pouvez utiliser n’importe quel [entrepôt de données cloud pris en charge](https://experienceleague.adobe.com/en/docs/federated-audience-composition/using/start/access-prerequisites).

Commençons par la [Connexion Data Warehouse](data-warehouse-connection.md).
