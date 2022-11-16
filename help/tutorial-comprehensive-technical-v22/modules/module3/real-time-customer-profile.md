---
title: Foundation - Profil client en temps réel
description: Foundation - Profil client en temps réel
kt: 5342
audience: Data Engineer, Data Architect, Marketer
doc-type: tutorial
activity: develop
exl-id: 050e5d99-544d-4a86-a7f6-9f103381dca5
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '517'
ht-degree: 1%

---

# 3. Foundation - Profil client en temps réel

**Auteur : [Wouter Van Geluwe](https://www.linkedin.com/in/woutervangeluwe/)**

Dans ce module, nous allons approfondir nos connaissances des fonctionnalités Real-time Customer Profile et Identity Service de Adobe Experience Platform. Vous découvrirez comment les audiences peuvent être définies, le rôle du service d’identité et de l’ID Experience Cloud, ainsi que comment définir des requêtes du créateur de segments pour définir vos propres segments.

## Objectifs d’apprentissage

- Découvrez comment visualiser le profil client en temps réel d’un client via l’interface utilisateur de Adobe Experience Platform
- Découvrez comment créer un segment à l’aide du créateur de segments Adobe Experience Platform
- Découvrez comment créer un segment et stocker les résultats du segment dans un jeu de données à l’aide des API Adobe Experience Platform
- Découvrez l’impact d’un accès à un profil client complet, y compris le comportement en temps réel, dans les environnements hors ligne.

## Conditions préalables

- Accès à [Adobe Experience Platform](https://experience.adobe.com/platform)
- Accès à [https://public.aepdemo.net](https://public.aepdemo.net)
- **Téléchargement de ces ressources**:
   - [Collections Postman](./../../assets/postman/postman_profile.zip)

>[!IMPORTANT]
>
>Ce tutoriel a été créé pour faciliter un format d’atelier particulier. Il utilise des systèmes et des comptes spécifiques auxquels vous n’avez peut-être pas accès. Même sans accès, nous pensons que vous pouvez encore apprendre beaucoup en lisant à travers ce contenu très détaillé. Si vous participez à l’un des ateliers et que vous avez besoin de vos informations d’identification d’accès, veuillez contacter votre représentant d’Adobe qui vous fournira les informations requises.

## Aperçu de l’architecture

Regardez l’architecture ci-dessous, qui met en évidence les composants qui seront discutés et utilisés dans ce module.

![Aperçu de l’architecture](../../assets/images/architecturem3.png)

## Environnement de test à utiliser

Pour ce module, utilisez cet environnement de test : `--aepSandboxId--`.

>[!NOTE]
>
>N’oubliez pas d’installer, de configurer et d’utiliser l’extension Chrome comme référencé dans [0.1 - Installation de l’extension Chrome pour la documentation Experience League](../module0/ex1.md)

## Exercices

[3.1 Visite du site web](./ex1.md)

Dans cet exercice, vous allez suivre un script et parcourir le site web.

[3.2 Visualiser votre propre profil client en temps réel - interface utilisateur](./ex2.md)

Au cours de cet exercice, vous vous connecterez à Adobe Experience Platform et vous verrez votre propre profil client en temps réel dans l’interface utilisateur.

[3.3 Visualiser votre propre profil client en temps réel - API](./ex3.md)

Au cours de cet exercice, vous utiliserez Postman et Adobe I/O pour afficher votre propre profil client en temps réel, en utilisant les API Adobe Experience Platform.

[3.4 Création d’un segment - IU](./ex4.md)

Dans cet exercice, vous allez créer un segment à l’aide du créateur de segments de Adobe Experience Platform.

[3.5 Création d’un segment - API](./ex5.md)

Au cours de cet exercice, vous utiliserez Postman et Adobe I/O pour créer un segment et stocker les résultats de ce segment sous la forme d’un jeu de données, à l’aide des API Adobe Experience Platform.

[3.6 Voir votre profil client en temps réel en action dans le centre d’appels](./ex6.md)

Dans cet exercice, vous emprunterez l’identité d’un employé du centre d’appels qui reçoit un appel d’un client. Pour réellement avoir un impact sur l’expérience de ce client, vous aurez besoin d’accéder à toutes les informations disponibles en temps réel.

[Résumé et avantages](./summary.md)

Résumé de ce module et aperçu des avantages.

>[!NOTE]
>
>Merci d&#39;investir votre temps dans l&#39;apprentissage de Adobe Experience Platform. Si vous avez des questions, souhaitez partager les commentaires généraux d&#39;avoir des suggestions sur le contenu futur, contactez directement Wouter Van Geluwe en envoyant un email à **vangeluw@adobe.com**.

[Revenir à tous les modules](../../overview.md)
