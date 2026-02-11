---
title: Collecte de données - Composition de l’audience fédérée
description: Collecte de données - Composition de l’audience fédérée
kt: 5342
doc-type: tutorial
exl-id: a2449e72-794a-4ff0-a208-28303fd574d1
source-git-commit: 23816907de778cbe3b9708f4a7273bdcb8e86d5c
workflow-type: tm+mt
source-wordcount: '613'
ht-degree: 0%

---

# 1.3 Composition De L’Audience Fédérée

Dans ce module, l’objectif est de tout savoir sur la création d’audiences à l’aide de la composition d’audiences fédérées.

La composition de l’audience fédérée (FAC) dans Experience Platform vous permet d’accéder aux audiences et d’en créer avec les attributs à forte valeur correspondants des entrepôts de données d’entreprise, ce qui enrichit et complète le profil client en temps réel et les audiences dans Experience Platform pour améliorer la segmentation, le ciblage, l’activation et la diffusion d’expériences client percutantes. Grâce à la composition d’audiences fédérées, une base de données virtuelle est créée en liant les bases de données distantes par le biais de métadonnées. Cette approche simplifie l’accès, réduit la duplication et améliore l’expérience de l’utilisateur final. Les équipes ont la possibilité d’ingérer directement des jeux de données dans Experience Platform ou d’accéder à des jeux de données résidant dans des entrepôts de données lors de l’assemblage des audiences pour les workflows d’engagement. Cette approche tire parti des investissements et des ressources dans l’entrepôt de données pour compléter Real-Time CDP et Journey Optimizer. La composition de l’audience fédérée permet aux clients d’utiliser et de combiner des fonctionnalités par lots et en temps réel selon de nouveaux modèles de cas d’utilisation critiques :

- Segmentation des audiences fédérées : une équipe peut créer une audience à l’aide de l’interface utilisateur de composition d’audiences par glisser-déposer conviviale pour les spécialistes du marketing dans Real-Time CDP et Journey Optimizer, mais avec une requête transmise à l’entrepôt de données, ce qui laisse les données sous-jacentes sensibles dans l’entrepôt sans duplication et offre un accès flexible aux jeux de données essentiels.
- Enrichissement de l’audience : les audiences créées dans Real-Time CDP et Journey Optimizer peuvent être enrichies avec des données d’entreprise supplémentaires afin d’améliorer le ciblage et la personnalisation avec des jeux de données supplémentaires, basés ou non sur les profils, qui ne seront pas conservés dans Adobe Experience Platform. Par exemple, une marque de vente au détail peut compléter une audience d’acheteurs en ligne récents avec une liste des principaux emplacements physiques pour créer une audience pour une promotion cross-canal en ligne et en magasin.
- Enrichissement du profil : les équipes peuvent sélectionner des attributs de profil à partir de l’entrepôt de données qui sont essentiels pour que les expériences du moment soient conservées dans les profils clients exploitables résidant dans Real-Time CDP et accessibles via Journey Optimizer. Ces points de données supplémentaires sont ensuite disponibles pour la segmentation et la personnalisation en aval déclenchées par des comportements d’événement en fonction de l’action de l’utilisateur et du cas d’utilisation du client. Cela permet aux attributs apportés avec les audiences fédérées d’être disponibles pour la segmentation et la personnalisation instantanées, ainsi que d’autres attributs et signaux comportementaux conservés dans un profil client.

La composition de l’audience fédérée offre aux clients de Real-Time CDP et de Journey Optimizer la possibilité de décider quelles données ils souhaitent utiliser à quel moment. Elle permet également d’éviter la duplication inutile de jeux de données ou de modèles d’intégration. Il s’agit d’une combinaison unique d’une approche fédérée de l’utilisation des données d’entreprise pour traiter les audiences et les attributs à forte valeur ajoutée, combinée à un système optimisé pour l’engagement cross-canal en temps réel. Cela permet de réduire le déplacement des données, mais aussi d’utiliser de nouvelles audiences et de nouveaux attributs à forte valeur ajoutée pour une activation cohérente à faible latence sur l’ensemble des canaux.

## Objectifs d’apprentissage

- Découvrez comment connecter Snowflake à Adobe Experience Platform
- Découvrez comment créer un modèle de données pour vos données fédérées dans Adobe Experience Platform
- Découvrez comment créer des compositions d’audiences fédérées dans Adobe Experience Platform

## Conditions préalables

- Accès à Adobe Experience Platform : [https://experience.adobe.com/platform](https://experience.adobe.com/platform)
- Accès à un entrepôt de données Snowflake

## Exercices

[1.3.1 Configuration de votre environnement Snowflake](./ex1.md)

Dans cet exercice, vous allez configurer votre compte d’évaluation Snowflake et le connecter à Adobe Experience Platform

[1.3.2 Création de schémas, de modèles de données et de liens](./ex2.md)

Dans cet exercice, vous allez configurer votre modèle de données dans AEP pour les données fédérées.

[1.3.3 Créer une composition fédérée](./ex3.md)

Dans cet exercice, vous allez configurer votre modèle de données dans AEP pour les données fédérées.

![Insiders de la technologie ](./../../../../assets/images/techinsiders.png){width="50px" align="left"}

>[!NOTE]
>
>Merci d’avoir consacré votre temps à apprendre tout ce qu’il y a à savoir sur Adobe Experience Platform et ses applications. Si vous avez des questions, si vous souhaitez partager des commentaires généraux ou si vous avez des suggestions sur le contenu futur, veuillez contacter directement les initiés techniques, en envoyant un e-mail à **techinsiders@adobe.com**.

[Revenir à tous les modules](./../../../../overview.md)
