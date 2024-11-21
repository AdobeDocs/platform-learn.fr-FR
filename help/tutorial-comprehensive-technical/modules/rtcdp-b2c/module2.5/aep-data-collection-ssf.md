---
title: Collecte de données Adobe Experience Platform et transfert côté serveur en temps réel
description: Dans ce module, vous utiliserez les jeux de données, les schémas et la propriété du serveur de collecte de données Adobe Experience Platform configurés précédemment pour collecter des données, puis vous les transférerez côté serveur de données vers un point de terminaison de votre choix.
kt: 5342
doc-type: tutorial
exl-id: aa3ab1eb-6fee-4ea9-9a0d-0d8ca803d7c2
source-git-commit: 7779e249b4ca03c243cf522811cd81370002d51a
workflow-type: tm+mt
source-wordcount: '458'
ht-degree: 0%

---

# 2.5 Connexions Real-Time CDP : Transfert d’événement

Dans ce module, vous utiliserez les jeux de données, schémas et propriété client de collecte de données Adobe Experience Platform configurés précédemment pour collecter des données, puis vous transmettrez ces données côté serveur à un point de terminaison de votre choix.

Dans ce module, vous allez :

- Création d’une propriété de serveur de collecte de données Adobe Experience Platform
- Installation et utilisation de l’extension Adobe Cloud Connector dans la collecte de données Adobe Experience Platform
- Création d’un point d’entrée de fonction Google et diffusion de données vers ce point
- Création d’un point de terminaison AWS et diffusion de données vers ce point

## Objectifs d’apprentissage

- Familiarisez-vous avec les propriétés du serveur de collecte de données Adobe Experience Platform et avec la nouvelle extension Adobe Cloud Connector
- Découvrez comment réutiliser les données du SDK Web Adobe Experience Platform dans des solutions tierces telles que Google et AWS
- Découvrez l’architecture derrière la collecte de données Adobe Experience Platform et le transfert côté serveur.

## Conditions préalables

- Accès à la collecte de données Adobe Experience Platform et Adobe Experience Platform
- Compréhension des jeux de données Adobe Experience Platform et XDM

>[!NOTE]
>
>N’oubliez pas d’installer, de configurer et d’utiliser l’extension Chrome comme référencé dans [Installation de l’extension Chrome pour la documentation Experience League](../../gettingstarted/gettingstarted/ex1.md)

## Exercices

[2.5.1 Création d’une propriété Transfert d’événement de collecte de données](./ex1.md)

Dans cet exercice, vous allez créer la propriété Transfert d’événement de collecte de données Adobe Experience Platform.

[2.5.2 Mise à jour de votre flux de données pour rendre les données disponibles pour la propriété Transfert d’événement de collecte de données](./ex2.md)

Au cours de cet exercice, vous allez mettre à jour votre flux de données existant pour que les données collectées par votre propriété client de collecte de données Adobe Experience Platform soient disponibles pour votre propriété serveur de collecte de données Adobe Experience Platform.

[2.5.3 Création et configuration d’un webhook personnalisé](./ex3.md)

Dans cet exercice, vous allez créer et configurer un webhook personnalisé. Vous allez commencer à transférer les données collectées par le SDK Web vers ce webhook personnalisé.

[2.5.4 Transfert d’événements vers le sous-site/public GCP](./ex4.md)

Au cours de cet exercice, vous allez créer et configurer une fonction cloud Google et vous allez commencer à transférer les données collectées par le SDK Web vers Google.

[2.5.5 Transfert d’événements vers AWS Kinesis et AWS S3](./ex5.md)

Dans cet exercice, vous allez configurer votre environnement AWS à l’aide d’AWS IAM, d’AWS Kinesis, d’AWS Firehose et d’AWS S3, après quoi vous allez commencer à transférer les données d’événement collectées par le SDK Web.

[Résumé et avantages](./summary.md)

Résumé de ce module et aperçu des avantages.

>[!NOTE]
>
>Merci d’investir votre temps à apprendre tout ce qu’il y a à savoir sur Adobe Experience Platform et ses applications. Si vous avez des questions, si vous souhaitez partager les commentaires généraux d’avoir des suggestions sur le contenu futur, contactez directement les initiés de technologie, en envoyant un email à **techinsiders@adobe.com**.

[Revenir à tous les modules](../../../overview.md)
