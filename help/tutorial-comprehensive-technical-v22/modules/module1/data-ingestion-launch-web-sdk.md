---
title: 1. Configuration de la collecte de données Adobe Experience Platform et de l’extension du SDK Web
description: Foundation - Configuration de la collecte de données Adobe Experience Platform et de l’extension du SDK Web
kt: 5342
audience: Data Engineer, Data Architect
doc-type: tutorial
activity: develop
exl-id: 86da7132-cb06-4be3-b6b8-ea3ab937e6dc
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '692'
ht-degree: 1%

---

# 1. Foundation - Configuration de la collecte de données Adobe Experience Platform et de l’extension du SDK Web

**Auteur : [Matthew Joseph Woolley](https://www.linkedin.com/in/matthewjwoolley/), [Wouter Van Geluwe](https://www.linkedin.com/in/woutervangeluwe/)**

Ce module de base vous présente la vision de collecte de données d’Adobe et explique comment obtenir des données d’un site web et d’une application mobile dans Adobe Experience Platform et d’autres applications via la collecte de données Adobe Experience Platform, les SDK Adobe Experience Platform et Adobe Experience Platform Edge Network. Ce module présente certains concepts et technologies qui ont un impact au-delà de la portée d’un tutoriel technique Adobe Experience Platform. Il doit être clair quelles parties de ces exercices sont essentielles pour le reste du tutoriel complet, qui vous en apprend davantage sur Experience Edge et ses fonctionnalités, et où aller pour obtenir des informations supplémentaires et des tutoriels.

## Objectifs d’apprentissage

- Découvrez comment une marque utilise la collecte de données Adobe Experience Platform comme son système Tag Management (TMS).
- Découvrez les flux de données utilisés par une marque pour ingérer des données vers ses produits d’Adobe.
- Découvrez comment envoyer des données à Adobe Experience Platform et à d’autres produits par le biais du réseau Adobe Experience Platform Edge.
- Découvrez comment créer des éléments de données et des règles qui collectent des données sur le Web et sur mobile.
- Découvrez les événements de suivi du SDK Web et comment déboguer leur contenu.
- Découvrez ce qu’est une couche de données et ce qu’Adobe recommande lors de l’implémentation d’une couche de données.
- Découvrez les étapes à suivre pour mettre en oeuvre le SDK Web de A à Z.
- Découvrez la différence entre une mise en oeuvre web et mobile.

## Conditions préalables

- Accès à Adobe Experience Platform : [https://experience.adobe.com/platform](https://experience.adobe.com/platform)
- Accès à la collecte de données Adobe Experience Platform : [https://experience.adobe.com/#/data-collection/](https://experience.adobe.com/#/data-collection/)
- Accès au site web de démonstration

>[!IMPORTANT]
>
>Ce tutoriel a été créé pour faciliter un format d’atelier particulier. Il utilise des systèmes et des comptes spécifiques auxquels vous n’avez peut-être pas accès. Même sans accès, nous pensons que vous pouvez encore apprendre beaucoup en lisant à travers ce contenu très détaillé. Si vous participez à l’un des ateliers et que vous avez besoin de vos informations d’identification d’accès, veuillez contacter votre représentant d’Adobe qui vous fournira les informations requises.

## Aperçu de l’architecture

Regardez l’architecture ci-dessous, qui met en évidence les composants qui seront discutés et utilisés dans ce module.

![Aperçu de l’architecture](../../assets/images/architecturem1.png)

## Environnement de test à utiliser

Pour ce module, utilisez cet environnement de test : `--aepSandboxId--`.

>[!NOTE]
>
>N’oubliez pas d’installer, de configurer et d’utiliser l’extension Chrome comme référencé dans [0.1 - Installation de l’extension Chrome pour la documentation Experience League](../module0/ex1.md)

## Exercices

[1.1 Présentation de la collecte de données Adobe Experience Platform](./ex1.md)

Au cours de cet exercice, explorez l’interface utilisateur de collecte de données Adobe Experience Platform et découvrez ses fonctionnalités.

[1.2 Collecte de données côté serveur, flux de données et réseau Edge](./ex2.md)

Au cours de cet exercice, vous apprendrez à transférer des données vers des produits Adobe dans l’interface de collecte de données Adobe Experience Platform et à étudier les flux de données utilisés par le site web de démonstration.

[1.3 Présentation de la collecte de données Adobe Experience Platform](./ex3.md)

Au cours de cet exercice, vous apprendrez à configurer une extension, à créer des éléments de données et des règles et à les publier sur le web.

[1.4 Collecte de données web côté client](./ex4.md)

Dans cet exercice, déboguez le SDK Web qui a été installé pour comprendre son fonctionnement et les données qui seront utilisées dans les exercices futurs.

[1.5 Mise en oeuvre d’Adobe Analytics et de Adobe Audience Manager](./ex5.md)

Dans cet exercice, consultez et utilisez les données web collectées avec le SDK web dans Adobe Analytics et Adobe Audience Manager.

[1.6 Mise en oeuvre d’Adobe Target](./ex6.md)

Dans cet exercice, configurez une activité dans Adobe Target, implémentée via le SDK Web.

[Exigences de schéma XDM 1.7 dans Adobe Experience Platform](./ex7.md)

Pour que le SDK Web et alloy.js puissent ingérer des données dans Adobe Experience Platform, un mixin XDM spécifique doit faire partie du schéma XDM dans Adobe Experience Platform.

[Résumé et avantages](./summary.md)

Résumé de ce module et aperçu des avantages.

>[!NOTE]
>
>Merci d&#39;investir votre temps dans l&#39;apprentissage de Adobe Experience Platform. Si vous avez des questions, souhaitez partager les commentaires généraux d&#39;avoir des suggestions sur le contenu futur, contactez directement Wouter Van Geluwe en envoyant un email à **vangeluw@adobe.com**.

[Revenir à tous les modules](../../overview.md)
