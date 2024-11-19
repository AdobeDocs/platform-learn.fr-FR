---
title: Collection de données - Composition de l’audience fédérée
description: Collection de données - Composition de l’audience fédérée
kt: 5342
doc-type: tutorial
exl-id: 44660f3e-0594-4578-9531-1c918992aa9d
source-git-commit: 3a19e88e820c63294eff38bb8f699a9f690afcb9
workflow-type: tm+mt
source-wordcount: '631'
ht-degree: 0%

---

# 1.3 Composition du public fédéré

**Auteur : [Ludovic Latapie](https://www.linkedin.com/in/ludoviclatapie/), [Wouter Van Geluwe](https://www.linkedin.com/in/woutervangeluwe/)**

Dans ce module, l’objectif est d’en savoir plus sur la création d’audiences à l’aide de la composition d’audiences fédérées.

La composition d’audiences fédérées (FAC) en Experience Platform vous permet d’accéder et de créer des audiences avec les attributs à forte valeur ajoutée correspondants à partir des entrepôts de données d’entreprise, ce qui enrichit et complète le profil client en temps réel et les audiences dans Experience Platform pour améliorer la segmentation, le ciblage, l’activation et la diffusion d’expériences client percutantes. Avec Federated Audience Composition, une base de données virtuelle est créée en liant des bases de données distantes par le biais de métadonnées. Cette approche simplifie l’accès, réduit la duplication et améliore l’expérience de l’utilisateur final. Les équipes ont la possibilité d’ingérer des jeux de données directement dans un Experience Platform ou d’accéder à des jeux de données résidant dans des entrepôts de données lors de l’assemblage d’audiences pour les workflows d’engagement. Cette méthode tire parti des investissements et des ressources de l’entrepôt de données pour compléter Real-Time CDP et Journey Optimizer. La composition d’audiences fédérées permet aux clients d’utiliser et de combiner des fonctionnalités en temps réel et par lots à travers de nouveaux modèles de cas d’utilisation critiques :

- Segmentation d’audience fédérée : une équipe peut créer une audience à l’aide de l’interface utilisateur de composition d’audience par glisser-déposer conviviale pour les marketeurs dans Real-Time CDP et Journey Optimizer, mais avec une requête envoyée à l’entrepôt de données, en conservant les données sous-jacentes sensibles dans l’entrepôt sans duplication et en fournissant un accès flexible aux jeux de données essentiels.
- Enrichissement de l’audience : les audiences créées dans Real-Time CDP et Journey Optimizer peuvent être enrichies de données d’entreprise supplémentaires afin d’améliorer le ciblage et la personnalisation grâce à des jeux de données basés sur des profils et non basés sur des profils supplémentaires qui ne persisteront pas dans Adobe Experience Platform. Par exemple, une marque de vente au détail peut compléter une audience de clients en ligne récents avec une liste d’emplacements standard pour créer une audience pour une promotion cross-canal en ligne et en magasin.
- Enrichissement de profil : les équipes peuvent sélectionner, à partir de l’entrepôt de données, des attributs de profil essentiels pour que les expériences en cours soient conservées dans des profils clients exploitables résidant dans Real-Time CDP et accessibles via Journey Optimizer. Ces points de données supplémentaires sont ensuite disponibles pour la segmentation et la personnalisation en aval déclenchées par les comportements d’événement selon l’action de l’utilisateur et le cas d’utilisation client. Cela permet aux attributs apportés avec les audiences fédérées d’être disponibles pour la segmentation et la personnalisation instantanées, avec d’autres attributs et signaux comportementaux conservés dans un profil client.

La composition d’audiences fédérées offre aux clients Real-Time CDP et Journey Optimizer la possibilité de décider quelles données ils souhaitent utiliser lorsqu’ils le souhaitent et permet d’éviter les jeux de données ou les modèles d’intégration inutilement dupliqués. Il s’agit d’une combinaison unique d’une approche fédérée de l’utilisation des données d’entreprise pour traiter les audiences et les attributs à forte valeur ajoutée, combinée à un système optimisé pour l’engagement cross-canal en temps réel. Cela se traduit par moins de mouvements de données, mais offre également de nouvelles opportunités d’utiliser des audiences et des attributs à forte valeur ajoutée pour une activation cohérente à faible latence sur tous les canaux.

## Objectifs d’apprentissage

- Découvrez comment connecter Snowflake à Adobe Experience Platform
- Découvrez comment créer un modèle de données pour vos données fédérées dans Adobe Experience Platform
- Découvrez comment créer des compositions d’audience fédérées dans Adobe Experience Platform

## Conditions préalables

- Accès à Adobe Experience Platform : [https://experience.adobe.com/platform](https://experience.adobe.com/platform)
- Accès à un entrepôt de données de Snowflake

## Exercices

[1.3.1 Configuration de votre compte de Snowflake](./ex1.md)

Dans cet exercice, vous allez configurer votre compte d’évaluation de Snowflake et le connecter à Adobe Experience Platform

[1.3.2 Création de schémas, de modèles de données et de liens](./ex2.md)

Dans cet exercice, vous allez configurer votre modèle de données dans AEP pour les données fédérées.

[1.3.3 Création d’une composition fédérée](./ex3.md)

Dans cet exercice, vous allez configurer votre modèle de données dans AEP pour les données fédérées.

[Résumé et avantages](./summary.md)

Résumé de ce module et aperçu des avantages.

>[!NOTE]
>
>Merci d’investir votre temps à apprendre tout ce qu’il y a à savoir sur Adobe Experience Platform et ses applications. Si vous avez des questions, si vous souhaitez partager les commentaires généraux d’avoir des suggestions sur le contenu futur, contactez directement les initiés de technologie, en envoyant un email à **techinsiders@adobe.com**.

[Revenir à tous les modules](../../../overview.md)
