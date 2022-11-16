---
title: Foundation - Ingestion de données
description: Foundation - Ingestion de données
kt: 5342
audience: Data Engineer, Data Architect
doc-type: tutorial
activity: develop
exl-id: dbbc0539-ae1b-488d-b312-76a74d4d361f
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '508'
ht-degree: 2%

---

# 2. Foundation - Ingestion des données

**Auteur : [Wouter Van Geluwe](https://www.linkedin.com/in/woutervangeluwe/)**

Dans ce module, l’objectif est d’en savoir plus sur l’ingestion de données. Vous en apprendrez plus sur l’ingestion de données en flux continu et par lots. Vous allez mettre en oeuvre l’ingestion de données par flux à l’aide de Launch, de sorte que le comportement des clients sur le site web de l’atelier de gestion des actifs numériques soit diffusé en temps réel sur Adobe Experience Platform. Pour en savoir plus sur l’ingestion de données par lots, utilisez un workflow Adobe Experience Platform pour prendre un fichier CSV, le mapper à un schéma XDM et l’ingérer dans Adobe Experience Platform.

## Objectifs d’apprentissage

- Découvrez comment créer un schéma XDM dans Adobe Experience Platform
- Découvrez comment créer des jeux de données dans Adobe Experience Platform
- Découvrez comment créer un point de terminaison de diffusion en continu et configurer l’extension Adobe Experience Platform dans Launch
- Découvrez comment créer des règles dans Launch pour diffuser des données vers Adobe Experience Platform
- Découvrez comment intégrer Adobe Experience Platform Launch à une page web
- Découvrez comment utiliser un workflow Adobe Experience Platform pour ingérer un fichier CSV dans Adobe Experience Platform

## Conditions préalables

- Accès à Adobe Experience Platform : [https://experience.adobe.com/platform](https://experience.adobe.com/platform)
- Accès à Adobe Experience Platform Launch : [https://experience.adobe.com/#/data-collection/](https://experience.adobe.com/#/data-collection/)
- Accès à [https://public.aepdemo.net](https://public.aepdemo.net)
- Accès à Postman

>[!IMPORTANT]
>
>Ce tutoriel a été créé pour faciliter un format d’atelier particulier. Il utilise des systèmes et des comptes spécifiques auxquels vous n’avez peut-être pas accès. Même sans accès, nous pensons que vous pouvez encore apprendre beaucoup en lisant à travers ce contenu très détaillé. Si vous participez à l’un des ateliers et que vous avez besoin de vos informations d’identification d’accès, veuillez contacter votre représentant d’Adobe qui vous fournira les informations requises.

## Aperçu de l’architecture

Regardez l’architecture ci-dessous, qui met en évidence les composants qui seront discutés et utilisés dans ce module.

![Aperçu de l’architecture](../../assets/images/architecturem2.png)

## Environnement de test à utiliser

Pour ce module, utilisez cet environnement de test : `--module2sandbox--`.

>[!NOTE]
>
>N’oubliez pas d’installer, de configurer et d’utiliser l’extension Chrome comme référencé dans [0.1 - Installation de l’extension Chrome pour la documentation Experience League](../module0/ex1.md)

## Exercices

[2.1 Exploration du site web](./ex1.md)

Dans cet exercice, vous allez explorer le site web que vous utiliserez dans le cadre de cette activation.

[2.2 Configuration de schémas et définition d’identifiants](./ex2.md)

Dans cet exercice, vous allez configurer les schémas XDM requis pour capturer les informations de profil et le comportement des clients. Dans chaque schéma XDM, vous devrez également configurer un identifiant Principal pour lier toutes les informations.

[2.3 Configuration de jeux de données](./ex3.md)

Au cours de cet exercice, vous récupérerez les jeux de données requis pour capturer et stocker les informations de profil et le comportement des clients.

[2.4 Ingestion de données à partir de sources hors ligne](./ex4.md)

Dans cet exercice, vous allez accéder au site web et à l’application mobile et vous comporter comme un client, en diffusant des données vers Platform.

[2.5 Zone d’entrée des données](./ex5.md)

Configurez votre connecteur source de zone d’entrée de données avec le stockage Azure Blob.

[Résumé et avantages](./summary.md)

Résumé de ce module et aperçu des avantages.

>[!NOTE]
>
>Merci d&#39;investir votre temps dans l&#39;apprentissage de Adobe Experience Platform. Si vous avez des questions, souhaitez partager les commentaires généraux d&#39;avoir des suggestions sur le contenu futur, contactez directement Wouter Van Geluwe en envoyant un email à **vangeluw@adobe.com**.

[Revenir à tous les modules](../../overview.md)
