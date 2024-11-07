---
title: Foundation - Ingestion de données
description: Foundation - Ingestion de données
kt: 5342
doc-type: tutorial
source-git-commit: 2cdc145d7f3933ec593db4e6f67b60961a674405
workflow-type: tm+mt
source-wordcount: '402'
ht-degree: 1%

---

# 1.2 Foundation - Ingestion des données

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
- Accès à Postman

>[!NOTE]
>
>N’oubliez pas d’installer, de configurer et d’utiliser l’extension Chrome comme référencé dans [Installation de l’extension Chrome pour la documentation Experience League](../../gettingstarted/gettingstarted/ex1.md)

## Exercices

[1.2.1 Exploration du site web](./ex1.md)

Dans cet exercice, vous allez explorer le site web que vous utiliserez dans le cadre de cette activation.

[1.2.2 Configuration des schémas et définition d’identifiants](./ex2.md)

Dans cet exercice, vous allez configurer les schémas XDM requis pour capturer les informations de profil et le comportement des clients. Dans chaque schéma XDM, vous devrez également configurer un identifiant principal pour lier toutes les informations à .

[1.2.3 Configuration de jeux de données](./ex3.md)

Au cours de cet exercice, vous récupérerez les jeux de données requis pour capturer et stocker les informations de profil et le comportement des clients.

[1.2.4 Ingestion de données à partir de sources hors ligne](./ex4.md)

Dans cet exercice, vous allez accéder au site web et à l’application mobile et vous comporter comme un client, en diffusant des données vers Platform.

[1.2.5 Zone d’entrée des données](./ex5.md)

Configurez votre connecteur Source de zone d’entrée de données avec le stockage Azure Blob.

[Résumé et avantages](./summary.md)

Résumé de ce module et aperçu des avantages.

>[!NOTE]
>
>Merci d’investir votre temps à apprendre tout ce qu’il y a à savoir sur Adobe Experience Platform et ses applications. Si vous avez des questions, si vous souhaitez partager les commentaires généraux d’avoir des suggestions sur le contenu futur, contactez directement les initiés de technologie, en envoyant un email à **techinsiders@adobe.com**.

[Revenir à tous les modules](../../../overview.md)
