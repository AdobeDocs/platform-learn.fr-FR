---
title: Collecte de données Adobe Experience Platform et transfert côté serveur en temps réel
description: Dans ce module, vous utiliserez les jeux de données, les schémas et la propriété du serveur de collecte de données Adobe Experience Platform configurés précédemment pour collecter des données, puis vous les transférerez côté serveur de données vers un point de terminaison de votre choix.
kt: 5342
audience: Data Engineer, Data Architect, Data Analyst
doc-type: tutorial
activity: develop
exl-id: c157ca52-c84f-4398-a658-2b6067e41707
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '574'
ht-degree: 1%

---

# 14. Connexions Real-Time CDP : Transfert d’événement

**Auteur : [Wouter Van Geluwe](https://www.linkedin.com/in/woutervangeluwe/), [Clément Delalande](https://www.linkedin.com/in/clement-delalande/)**

Dans ce module, vous utiliserez les jeux de données, schémas et propriété client de collecte de données Adobe Experience Platform configurés précédemment pour collecter des données, puis vous transmettrez ces données côté serveur à un point de terminaison de votre choix.

Dans ce module, vous allez :

- Création d’une propriété de serveur de collecte de données Adobe Experience Platform
- Installation et utilisation de l’extension Adobe Cloud Connector dans la collecte de données Adobe Experience Platform
- Création d’un point d’entrée de fonction Google et diffusion de données vers ce point
- Création d’un point de terminaison AWS et diffusion de données vers ce point

Regardez cette vidéo pour comprendre la valeur, le parcours client et le processus de configuration :

>[!VIDEO](https://video.tv.adobe.com/v/331987?quality=12&learn=on)

## Objectifs d’apprentissage

- Familiarisez-vous avec les propriétés du serveur de collecte de données Adobe Experience Platform et avec la nouvelle extension Adobe Cloud Connector
- Découvrez comment réutiliser les données du SDK Web Adobe Experience Platform dans des solutions tierces telles que Google et AWS
- Découvrez l’architecture derrière la collecte de données Adobe Experience Platform et le transfert côté serveur.

## Conditions préalables

- Accès à la collecte de données Adobe Experience Platform et Adobe Experience Platform
- Compréhension des jeux de données Adobe Experience Platform et XDM

>[!IMPORTANT]
>
>Ce tutoriel a été créé pour faciliter un format d’atelier particulier. Il utilise des systèmes et des comptes spécifiques auxquels vous n’avez peut-être pas accès. Même sans accès, nous pensons que vous pouvez encore apprendre beaucoup en lisant à travers ce contenu très détaillé. Si vous participez à l’un des ateliers et que vous avez besoin de vos informations d’identification d’accès, veuillez contacter votre représentant d’Adobe qui vous fournira les informations requises.

## Aperçu de l’architecture

Regardez l’architecture ci-dessous, qui met en évidence les composants qui seront discutés et utilisés dans ce module.

![Aperçu de l’architecture](../../assets/images/architecturem21.png)

## Environnement de test à utiliser

Pour ce module, utilisez cet environnement de test : `--aepSandboxId--`.

>[!NOTE]
>
>N’oubliez pas d’installer, de configurer et d’utiliser l’extension Chrome comme référencé dans [0.1 - Installation de l’extension Chrome pour la documentation Experience League](../module0/ex1.md)

## Exercices

[14.1 Création d’une propriété Transfert d’événement de collecte de données](./ex1.md)

Dans cet exercice, vous allez créer la propriété Transfert d’événement de collecte de données Adobe Experience Platform.

[14.2 Mettez à jour votre flux de données pour rendre les données disponibles pour la propriété Transfert d’événement de collecte de données](./ex2.md)

Au cours de cet exercice, vous allez mettre à jour votre flux de données existant pour que les données collectées par votre propriété client de collecte de données Adobe Experience Platform soient disponibles pour votre propriété serveur de collecte de données Adobe Experience Platform.

[14.3 Création et configuration d’un webhook personnalisé](./ex3.md)

Dans cet exercice, vous allez créer et configurer un webhook personnalisé. Vous allez commencer à transférer les données collectées par le SDK Web vers ce webhook personnalisé.

[14.4 Création et configuration d’une fonction cloud Google](./ex4.md)

Au cours de cet exercice, vous allez créer et configurer une fonction cloud Google et vous allez commencer à transférer les données collectées par le SDK Web vers Google.

[14.5 Événements de transfert vers l’écosystème AWS](./ex5.md)

Dans cet exercice, vous allez configurer votre environnement AWS à l’aide de la passerelle API AWS, d’AWS Kinesis, d’AWS Firehose et d’AWS S3, après quoi vous allez commencer à transférer les données d’événement collectées par le SDK Web.

[Résumé et avantages](./summary.md)

Résumé de ce module et aperçu des avantages.

>[!NOTE]
>
>Merci d&#39;investir votre temps dans l&#39;apprentissage de Adobe Experience Platform. Si vous avez des questions, souhaitez partager les commentaires généraux d&#39;avoir des suggestions sur le contenu futur, contactez directement Wouter Van Geluwe en envoyant un email à **vangeluw@adobe.com**.

[Revenir à tous les modules](../../overview.md)
