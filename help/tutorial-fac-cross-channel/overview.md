---
title: Déverrouiller les informations cross-canal avec la composition d’audiences fédérées
description: La composition de l’audience fédérée est une puissante fonctionnalité qui permet aux architectes et aux ingénieurs de données de créer et d’enrichir des audiences directement à partir d’entrepôts de données tiers.
breadcrumb-title: Aperçu
role: Data Architect, Data Engineer
jira: KT-18743
thumbnail: 18743-overview.jpg
recommendations: catalog, noDisplay
last-substantial-update: 2025-08-11T00:00:00Z
source-git-commit: a5ae2695763bc3d6dce786861dcbc15f3422c035
workflow-type: tm+mt
source-wordcount: '558'
ht-degree: 0%

---


# Aperçu

La composition de l’audience fédérée est une puissante fonctionnalité disponible pour les environnements Adobe Real-Time Customer Data Platform (Real-Time CDP) et Adobe Journey Optimizer. Il permet aux architectes de données et aux ingénieurs de données de créer et d’enrichir des audiences directement à partir d’entrepôts de données tiers [pris en charge](https://experienceleague.adobe.com/en/docs/federated-audience-composition/using/start/access-prerequisites){target="_blank"} sans répliquer les données dans Adobe Experience Platform. Ce tutoriel fournit des conseils pratiques aux utilisateurs et utilisatrices techniques pour connecter des entrepôts de données d’entreprise, créer et enrichir des audiences, et les activer pour offrir des expériences marketing personnalisées.

## Objectifs d’apprentissage

En suivant ce tutoriel, vous pourrez :

- Découvrez comment connecter Adobe Experience Platform à un entrepôt de données d’entreprise.
- Découvrez comment créer et gérer des audiences à l’aide de la composition d’audiences fédérées.
- Découvrez comment enrichir les audiences existantes avec des données d’entrepôt de données.
- Mappez les audiences fédérées à des destinations externes telles qu’Amazon S3.
- Créez des parcours client à l’aide des données d’audience fédérées.
- Validez les données et les processus par le biais d’exercices pratiques et de démonstrations.

Ce tutoriel est conçu pour les architectes et ingénieurs de données qui travaillent avec Real-Time CDP ou Journey Optimizer. Il suppose une connaissance des concepts de base de Adobe Experience Platform et de Data Warehouse.

## Contexte commercial

SecurFinancial est une société de services financiers de premier plan. Il tire parti de sa richesse de données client sur différentes sources pour personnaliser les offres et les campagnes pour un grand nombre de segments. Ils prévoient d’utiliser la fonctionnalité de composition d’audience fédérée d’Adobe Real-Time CDP qui permet aux entreprises d’utiliser leur entrepôt de données existant tout en utilisant les applications Adobe Experience Platform pour offrir des expériences client personnalisées. Les principaux avantages sont les suivants :

- **Accès aux données de l’entrepôt de données** : créez des audiences à forte valeur ajoutée à partir de jeux de données dans des entrepôts de données pris en charge sans réplication des données.
- **Mouvement des données réduit** : interrogez les données directement dans l’entrepôt de données, ce qui réduit la duplication et maintient la gouvernance des données.
- **Workflows d’expérience unifiée** : traitez et activez des audiences dans Adobe Experience Platform pour des cas d’utilisation cross-canal.
- **Personnalisation améliorée** : enrichissez les profils et les audiences avec des attributs d’entrepôt de données pour alimenter des expériences déclenchées en temps réel.

## Scénario d’entreprise

SecurFinancial souhaite lancer une campagne par e-mail pour recibler ses clients qui sont préqualifiés pour un prêt basé sur un bon crédit et n&#39;ont pas de prêt actif dans leur portefeuille SecurFinancial. Bien qu’ils ingèrent des données comportementales en ligne en temps réel, ils rencontrent des difficultés pour identifier la préqualification des clients, car ils ne peuvent pas ingérer d’informations de crédit dans AEP. Pour qualifier les clients préqualifiés sans déplacer les données restreintes, ils utiliseront la composition d’audience fédérée afin d’enrichir leur audience comportementale AEP.



## Conditions préalables

Pour suivre ce tutoriel, vérifiez que vous disposez des éléments suivants :

- Accès à un compte Adobe Experience Platform configuré avec Real-Time CDP ou Journey Optimizer.
- Autorisations d’administrateur système ou possibilité de configurer des autorisations.
- Connaissance des concepts Adobe Experience Platform tels que les schémas, les jeux de données et les audiences (recommandé : suivez la [Présentation de la liste de lecture Adobe Experience Platform](https://experienceleague.adobe.com/en/playlists/experience-platform-introduction?lang=en){target="_blank"} sur Experience League).
- Accès à un entrepôt de données d’entreprise pris en charge (par exemple, Amazon Redshift, Azure Synapse Analytics, Snowflake ou Google BigQuery).
- Connaissances de base de SQL pour interroger les entrepôts de données.

## Utilisation De Ce Tutoriel

Ce tutoriel est structuré pour les utilisateurs et utilisatrices techniques. Les leçons s’appuient les unes sur les autres, donc complétez-les dans l’ordre, sauf indication contraire.

## Notes techniques

- **Environnements Sandbox** : créez un sandbox dans l’instance Real-Time CDP de votre organisation pour effectuer des tests en toute sécurité sans affecter les données de production.
- **Connexion Data Warehouse** : ce tutoriel utilise une connexion Snowflake, mais vous pouvez utiliser n’importe quel [entrepôt de données cloud pris en charge](https://experienceleague.adobe.com/en/docs/federated-audience-composition/using/start/access-prerequisites).

Commencez par la leçon [Connexion à Data Warehouse](data-warehouse-connection.md) pour commencer à configurer votre environnement.
