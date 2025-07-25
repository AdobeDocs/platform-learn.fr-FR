---
title: Experience Decisioning - Experience Decisioning 101
description: Experience Decisioning - Experience Decisioning 101
kt: 5342
audience: Data Engineer, Data Architect, Orchestration Engineer, Marketer
doc-type: tutorial
source-git-commit: 13d790855601fa6f36c1afa0f2d5faad5fc07eb0
workflow-type: tm+mt
source-wordcount: '365'
ht-degree: 1%

---

# 3.7.1 Experience Decisioning 101

## Terminologie 3.7.1.1

Pour une meilleure compréhension d’Experience Decisioning, nous vous recommandons vivement de lire la [présentation](https://experienceleague.adobe.com/docs/journey-optimizer/using/offer-decisioniong/get-started-decision/starting-offer-decisioning.html?lang=fr) sur le fonctionnement du service applicatif Offer Decisioning avec Adobe Experience Platform.

Dans l&#39;utilisation d&#39;Offer Decisioning, il est nécessaire de comprendre les concepts suivants :

| Terme | Explication |
| ------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Offre** | Une offre est un message marketing auquel des règles peuvent être associées et qui spécifie qui est éligible pour voir l’offre. Une offre a un statut : brouillon, approuvée ou archivée. |
| **Placement** | Combinaison de l’emplacement (ou type de canal) et du contexte (ou type de contenu) dans lequel apparaît une offre pour un utilisateur final. Il s’agit en fait de la combinaison de textes, d’HTML, d’images, de fichiers JSON sur les canaux mobiles, web, sociaux, de messagerie instantanée et non numériques. |
| **Règle** | Logique qui définit et contrôle l’éligibilité des utilisateurs finaux pour une offre. |
| **Offre Personnalisée** | Message marketing personnalisable basé sur des règles et des contraintes d’éligibilité. |
| **Offre De Secours** | Offre par défaut affichée lorsqu&#39;un utilisateur final n&#39;est éligible à aucune des offres de la collection utilisée. |
| **Limitation** | Utilisé dans une définition d’offre pour définir le nombre total de fois où une offre peut être présentée au total et à un utilisateur spécifique. |
| **Priorité** | Niveau permettant de déterminer le rang de priorité à partir d’un jeu d’offres de résultats. |
| **Collection** | Utilisé pour filtrer un sous-ensemble d’offres de la liste des offres personnalisées afin d’accélérer le processus d’Offer Decisioning. |
| **Décision** | Une combinaison d’un ensemble d’offres, d’emplacements et de profils pour laquelle le marketeur souhaite que le moteur de décision fournisse la meilleure offre. |
| **AEM Assets Essentials** | Une expérience universelle et centralisée pour le stockage, la recherche et la sélection de ressources dans les solutions Adobe Experience Cloud et Adobe Experience Platform. |

{style="table-layout:auto"}

## 3.7.1.2 Experience Decisioning

Connectez-vous à Adobe Journey Optimizer en allant sur [Adobe Experience Cloud](https://experience.adobe.com?lang=fr). Cliquez sur **Journey Optimizer**.

![ExD](./../../../../modules/delivery-activation/ajo-b2c/ajob2c-1/images/acophome.png)

Vous serez redirigé vers la vue **Accueil** dans Journey Optimizer. Tout d’abord, assurez-vous d’utiliser le bon sandbox. Le sandbox à utiliser est appelé `--aepSandboxName--`. Vous serez alors dans la vue **Accueil** de votre `--aepSandboxName--` sandbox.

![ExD](./../../../../modules/delivery-activation/ajo-b2c/ajob2c-1/images/acoptriglp.png)

Dans l’exercice suivant, vous allez configurer vos propres offres et décisions.

## Étapes suivantes

Accédez à [3.7.2 Configuration des offres et décision](./ex2.md){target="_blank"}

Revenez à [ Experience Decisioning ](ajo-decisioning.md){target="_blank"}

Revenir à [Tous les modules](./../../../../overview.md){target="_blank"}
