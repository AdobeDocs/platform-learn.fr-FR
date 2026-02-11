---
title: Collecte de données Adobe Experience Platform et transfert côté serveur en temps réel
description: Dans ce module, vous allez utiliser les jeux de données, les schémas et la propriété de serveur de collecte de données Adobe Experience Platform configurés précédemment pour collecter des données, puis transférer ces données côté serveur vers un point d’entrée de votre choix.
kt: 5342
doc-type: tutorial
exl-id: dbf5e995-9c2e-4f72-b336-e942cb22cde5
source-git-commit: 2d5ca888eb24c1f65b4ecd48030ec8d1659b7f84
workflow-type: tm+mt
source-wordcount: '448'
ht-degree: 0%

---

# 2.5 Connexions Real-Time CDP : transfert d’événement

Dans ce module, vous allez utiliser les jeux de données, les schémas et la propriété Client de collecte de données Adobe Experience Platform configurés précédemment pour collecter des données, puis transférer ces données côté serveur vers un point d’entrée de votre choix.

Dans ce module, vous allez :

- Création d’une propriété de serveur de collecte de données Adobe Experience Platform
- Installer et utiliser l’extension Adobe Cloud Connector dans la collecte de données Adobe Experience Platform
- Créez un point d’entrée de fonction Google et diffusez-y des données
- Création d’un point d’entrée AWS et diffusion de données vers celui-ci

## Objectifs d’apprentissage

- Familiarisez-vous avec les propriétés du serveur de collecte de données Adobe Experience Platform et la nouvelle extension Adobe Cloud Connector .
- Découvrez comment réutiliser les données Adobe Experience Platform Web SDK dans des solutions tierces telles que Google et AWS
- Découvrez l’architecture derrière la collecte de données Adobe Experience Platform et le transfert côté serveur.

## Conditions préalables

- Accès à la collecte de données Adobe Experience Platform et Adobe Experience Platform
- Compréhension des jeux de données Adobe Experience Platform et de XDM

>[!NOTE]
>
>N’oubliez pas d’installer, de configurer et d’utiliser l’extension Chrome, comme indiqué dans [Installation de l’extension Chrome pour la documentation Experience League](../../../getting-started/gettingstarted/ex1.md)

## Exercices

[2.5.1 Création d’une propriété de transfert d’événement de collecte de données](./ex1.md)

Dans cet exercice, vous allez créer votre propriété Transfert d’événement de la collecte de données Adobe Experience Platform.

[2.5.2 Mettez à jour votre flux de données pour rendre les données disponibles pour votre propriété Transfert d’événement de collecte de données](./ex2.md)

Dans cet exercice, vous allez mettre à jour votre flux de données existant afin que les données collectées par la propriété Client de collecte de données Adobe Experience Platform soient disponibles pour la propriété Serveur de collecte de données Adobe Experience Platform.

[2.5.3 Création et configuration d’un webhook personnalisé](./ex3.md)

Dans cet exercice, vous allez créer et configurer un webhook personnalisé, puis commencer à transférer les données collectées par Web SDK vers ce webhook personnalisé.

[2.5.4 Transférer les événements au GCP Pub/Sub](./ex4.md)

Dans cet exercice, vous allez créer et configurer une fonction cloud Google et vous allez commencer à transférer les données collectées par Web SDK vers Google.

[2.5.5 Transfert d’événements vers AWS Kinesis et AWS S3](./ex5.md)

Dans cet exercice, vous allez configurer votre environnement AWS à l’aide d’AWS IAM, d’AWS Kinesis, d’AWS Firehouse et d’AWS S3, après quoi vous commencerez à transférer les données d’événement collectées par Web SDK.

![Insiders de la technologie ](./../../../../assets/images/techinsiders.png){width="50px" align="left"}

>[!NOTE]
>
>Merci d’avoir consacré votre temps à apprendre tout ce qu’il y a à savoir sur Adobe Experience Platform et ses applications. Si vous avez des questions, si vous souhaitez partager des commentaires généraux ou si vous avez des suggestions sur le contenu futur, veuillez contacter directement les initiés techniques, en envoyant un e-mail à **techinsiders@adobe.com**.

[Revenir à tous les modules](./../../../../overview.md)
