---
title: Customer Journey Analytics - Customer Journey Analytics 101
description: Customer Journey Analytics - Customer Journey Analytics 101
kt: 5342
doc-type: tutorial
exl-id: ea1469a4-cbfd-4633-8678-9467c2146a2a
source-git-commit: 1e3a8d585503eddad4c642a3b13d2b5f7ddc9943
workflow-type: tm+mt
source-wordcount: '856'
ht-degree: 1%

---

# 1.1.1 Customer Journey Analytics 101

## Objectifs

- Comprendre le service d’application CJA
- Découvrez comment positionner CJA
- Comprendre le workflow CJA : de la connexion aux données aux informations

## 1.1.1.1 Qu’est-ce que Customer Journey Analytics ?

Customer Journey Analytics (CJA) fournit une boîte à outils aux équipes de Business Intelligence et de science des données pour l’assemblage et l’analyse des données cross-canal (en ligne et hors ligne). Les fonctionnalités de CJA offrent contexte et clarté au parcours client multicanal complexe. Le contexte fourni permet d’obtenir des informations exploitables sur la suppression des problèmes du processus de conversion des clients et sur la conception et la diffusion d’expériences exceptionnelles pour les moments les plus importants.

CJA ajoute Analysis Workspace à Adobe Experience Platform. Adobe Experience Platform est le cerveau de la communication et de l’orchestration. Avec CJA, les marques peuvent désormais contextualiser et visualiser toutes ces données, afin que les équipes commerciales et d’Insight puissent en tirer des leçons en analysant le parcours client en ligne et hors ligne dans son ensemble.

Les équipes d’entreprise et d’Insight peuvent communiquer avec CJA, poser des questions et obtenir des réponses à la volée grâce à l’interface utilisateur conviviale et conviviale d’Analysis Workspace par glisser-déposer et par pointer-cliquer.

![demo](./images/cja-adv-analysis1.png)

## 1.1.1.2 avantages clés

Les trois principaux avantages pour les clients sont les suivants :

- La possibilité de mettre les informations à la disposition de tous (c’est-à-dire de démocratiser l’accès aux données)
- La possibilité de voir le client dans un parcours contextuel (c’est-à-dire que les données peuvent être visualisées de manière séquentielle, sur plusieurs canaux en ligne et hors ligne)
- Capacité à exploiter la puissance des données sans en avoir besoin (c’est-à-dire qu’elle permet à des êtres humains normaux d’utiliser des données pour obtenir des informations et des analyses approfondies en vue de l’activation marketing)

## 1.1.1.3 Pourquoi choisir Customer Journey Analytics ?

CJA n’est pas destiné à remplacer une application BI actuelle telle que Power BI, Microstrategy, Locker ou Tableau. Ces applications de BI sont destinées à visualiser des données afin de créer des tableaux de bord d’entreprise pour que tous les membres d’une organisation puissent rapidement consulter des mesures importantes.\
L’objectif de CJA est d’apporter la puissance d’analyse aux équipes marketing et commerciales, ce qui en fait un outil d’analyse « incontournable » pour ces personnes.

Traditionnellement, les applications de BI n’étaient pas en mesure d’activer une véritable intelligence client :

- Ils ne peuvent pas faire d’attribution et n’effectuent pas d’analyse du parcours client.
- Les applications de BI doivent connaître la question à l’avance
- Les requêtes interactives sont limitées par la structure de la base de données
- Des compétences SQL sont requises.
- Les applications de BI ne vous permettent pas de demander pourquoi quelque chose s’est produit.
- Les applications BI n’ont aucune connexion directe avec les points de contact client.

Pour cette raison, les utilisateurs professionnels et les analystes se retrouvent presque immédiatement dans une impasse, ce qui rend l’analyse coûteuse, lente, rigide et déconnectée des systèmes d’action.

Avec CJA, vous disposez d’une vue à 360° du parcours client, grâce aux données en ligne et hors ligne, et des outils adéquats pour réduire le temps nécessaire aux informations. Les utilisateurs professionnels peuvent ainsi comprendre de manière indépendante pourquoi un événement s’est produit et comment y répondre.

![demo](./images/cja-use-case.png)

## 1.1.1.4 Présentation du workflow Customer Journey Analytics

Avant de commencer les exercices suivants, il est essentiel de comprendre les étapes nécessaires pour importer des données de Adobe Experience Platform dans CJA afin de les visualiser et d’obtenir des informations détaillées. Il s’agit de ce que nous appelons un workflow CJA. Jetons un coup d&#39;œil :

![demo](./images/cja-work-flow.jpg)

Avant de commencer les étapes ci-dessus, n’oubliez pas l’étape 0, qui consiste à comprendre les données disponibles dans Adobe Experience Platform.

**Enfouir, jeter.** Vous Souvenez ? Vous devez avoir une idée claire des données disponibles et de la manière dont les schémas sont configurés dans Adobe Experience Platform. Comprendre les données qui se trouvent dans Adobe Experience Platform facilitera les choses, non seulement au niveau de la connexion aux données, mais également lors de la création de visualisations et de l’analyse.

## 1.1.1.5 Étape 0 : comprendre les schémas et les jeux de données Adobe Experience Platform

Connectez-vous à Adobe Experience Platform en accédant à cette URL : [https://experience.adobe.com/platform](https://experience.adobe.com/platform).

Une fois connecté, vous accédez à la page d’accueil de Adobe Experience Platform.

![Ingestion des données](./../../../../modules/delivery-activation/datacollection/dc1.2/images/home.png)

Avant de continuer, vous devez sélectionner un **sandbox**. Le sandbox à sélectionner est nommé ``--aepSandboxName--``. Après avoir sélectionné la sandbox appropriée, la modification d’écran s’affiche et vous êtes maintenant dans votre sandbox dédiée.

![Ingestion des données](./../../../../modules/delivery-activation/datacollection/dc1.2/images/sb1.png)

Veuillez consulter ces schémas et jeux de données dans Adobe Experience Platform.

| Jeu de données | Schéma |
| ----------------- |-------------| 
| Système de démonstration - Jeu de données d’événement pour le site web (Global v1.1) | Système de démonstration - Schéma d’événement pour le site web (version globale v1.1) |
| Système de démonstration - Jeu de données d’événement pour le centre d’appels (version globale v1.1) | Système de démonstration - Schéma d’événement pour le centre d’appels (version globale v1.1) |
| Système de démonstration - Jeu de données d’événement pour les assistants vocaux (version globale v1.1) | Système de démonstration - Schéma d’événement pour les assistants vocaux (version globale v1.1) |

Veillez à avoir au moins vérifié des éléments tels que :

- Identités : CRMID, phoneNumber, ECID, e-mail. Quelles sont les identités principales, lesquelles sont les identifiants secondaires ?
Vous pouvez trouver les identifiants en ouvrant un schéma et en examinant la `--aepTenantId--.identification.core` de l’objet . Consultez le schéma [Système de démonstration - Schéma d’événement pour le site web (global v1.1)](https://experience.adobe.com/platform/schema).

![demo](./images/identity.png)

- Explorez l’objet Commerce dans le schéma [Système de démonstration - Schéma d’événement pour le site web (version globale v1.1)](https://experience.adobe.com/platform/schema).

![demo](./images/commerce.png)

- Prévisualisez tous les [jeux de données](https://experience.adobe.com/platform/dataset/browse?limit=50&amp;page=1&amp;sortDescending=1&amp;sortField=created) et examinez les données

Vous êtes maintenant prêt à utiliser l’interface utilisateur de Customer Journey Analytics.

## Étapes suivantes

Accédez à [1.1.2 Connexion des jeux de données Adobe Experience Platform dans Customer Journey Analytics](./ex2.md){target="_blank"}

Revenir à [Customer Journey Analytics](./customer-journey-analytics-build-a-dashboard.md){target="_blank"}

Revenir à [Tous les modules](./../../../../overview.md){target="_blank"}
