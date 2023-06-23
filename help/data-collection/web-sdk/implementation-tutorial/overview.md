---
title: Aperçu
description: Aperçu
role: Developer
level: Intermediate
recommendations: noDisplay,noCatalog
jira: KT-10447
hide: true
hidefromtoc: true
exl-id: 8ffa258b-6ff7-4413-aead-21b106668c65
source-git-commit: 90f7621536573f60ac6585404b1ac0e49cb08496
workflow-type: tm+mt
source-wordcount: '259'
ht-degree: 1%

---

# Aperçu

La collecte de données sur les événements se produisant dans le navigateur d’un utilisateur est un principe fondamental de la stratégie marketing. Adobe propose plusieurs outils pour vous aider à gérer ces données. Bien que vous puissiez vous familiariser avec chacun de ces outils individuellement, ce tutoriel tente de fournir une vue plus large de ce que chacun de ces outils font et de la manière dont ils travaillent ensemble pour atteindre un objectif commun.

Dans ce tutoriel, nous allons discuter d’une stratégie pour (1) structurer et conserver vos données dans Adobe Experience Platform, (2) gérer vos données dans le navigateur et communiquer que certains événements se sont produits, et (3) réagir à ces événements en envoyant les données appropriées à Adobe Experience Platform.

Bien que ce tutoriel utilise la couche de données client Adobe, le SDK web Adobe Experience Platform et la fonctionnalité de balises pour une mise en oeuvre plus prescriptive et transparente, vous pouvez également mélanger ces outils avec des outils tiers ou internes pour une flexibilité ultime.

## Exemple de scénario

Pour ce tutoriel, nous supposons que vous mettez en oeuvre la collecte de données pour une page de produit simple sur un site de commerce électronique. La page du produit est chargée dans le navigateur. Vous allez ici effectuer le suivi de l’affichage du produit par l’utilisateur. L’utilisateur décide d’acheter le produit, il clique donc sur un bouton pour ajouter le produit à son panier. Ici, vous allez vérifier que l’utilisateur a ouvert un nouveau panier et ajouté le produit au panier en envoyant des événements d’expérience à Adobe Experience Platform. Enfin, l’utilisateur clique sur un _Téléchargement de l’application_ car votre application mobile les intéresse. Vous allez vérifier que l’utilisateur a cliqué sur le lien.
