---
title: Activation de segment vers Microsoft Azure Event Hub
description: Activation de segment vers Microsoft Azure Event Hub
kt: 5342
doc-type: tutorial
exl-id: 23713cb4-2055-43e8-9380-0ca8845a75e8
source-git-commit: 0dbcda0cfc9f199a44c845c1b5caf00a8d740251
workflow-type: tm+mt
source-wordcount: '566'
ht-degree: 0%

---

# 2.4 Real-Time CDP : activation de segments vers Microsoft Azure Event Hub

**Auteurs : [Marc Meewis](https://www.linkedin.com/in/marcmeewis/), [Wouter Van Geluwe](https://www.linkedin.com/in/woutervangeluwe/)**

Dans ce module, vous allez configurer une destination Microsoft Azure EventHub en tant que destination en temps réel pour la plateforme de données clients en temps réel de Adobe Experience Platform. Vous allez également configurer et déployer une fonction Azure qui sera déclenchée en temps réel chaque fois que Adobe Experience Platform envoie une charge utile de segment à votre destination Azure EventHub. La fonction Azure que vous allez déclencher affichera le mécanisme des fonctionnalités d’activation de la plateforme de données clients en temps réel de Adobe Experience Platform.

Dans le cadre de ce module, vous comprendrez également ce qui déclenche la diffusion d’une charge utile en temps réel sur une destination spécifiée par la plateforme CDP en temps réel. Nous discuterons également de l’état d’une qualification de segment et de sa relation avec l’activation.

La plateforme de données clients en temps réel de Adobe Experience Platform prend en charge l’activation des données vers les destinations de stockage dans le cloud en continu, ce qui vous permet d’exporter des données et des événements d’audience en temps réel vers ces destinations au format JSON. Vous pouvez ensuite décrire la logique commerciale en plus de ces événements dans vos destinations

Microsoft Azure Event Hubs est un service d’ingestion de données en temps réel entièrement géré, simple, fiable et évolutif. Diffusez des millions d’événements par seconde depuis n’importe quelle source pour créer des pipelines de données dynamiques et répondre immédiatement aux défis de l’entreprise.

## Objectifs d’apprentissage

- Familiarisez-vous avec les centres d’événements Microsoft Azure
- Configuration d’une destination RTCDP sur votre centre d’événements Microsoft Azure
- Comprendre quand la plateforme CDP en temps réel est activée et à quoi ressemble la payload d’activation
- Configuration du code Visual Studio pour développer, tester et déployer votre projet Azure
- Créer et déployer une fonction Azure qui utilise les qualifications de segments fournies en temps réel par RTCDP

## Conditions préalables

- Accès à [Adobe Experience Platform](https://experience.adobe.com/platform)
- Familiarité avec l’environnement du site web de démonstration AEP
- Comprendre comment définir, utiliser et activer des segments en flux continu dans Adobe Experience Platform

>[!NOTE]
>
>N’oubliez pas d’installer, de configurer et d’utiliser l’extension Chrome comme référencé dans [Installation de l’extension Chrome pour la documentation Experience League](../../gettingstarted/gettingstarted/ex1.md)

## Exercices

[2.4.0 Configuration de votre environnement](./ex0.md)

Dans cet exercice, vous allez configurer votre environnement Microsoft Azure.

[2.4.1 Configuration de votre environnement Microsoft Azure EventHub](./ex1.md)

Dans cet exercice, vous allez configurer votre environnement Microsoft Azure EventHub.

[2.4.2 Configuration de votre destination Azure Event Hub dans Adobe Experience Platform](./ex2.md)

Au cours de cet exercice, vous allez configurer votre connexion de destination de la plateforme de données clients en temps réel qui diffusera les segments en temps réel vers EventHub que vous avez configuré dans l’exercice précédent.

[2.4.3 Création d’un segment](./ex3.md)

Dans cet exercice, vous allez créer un segment en continu dans Adobe Experience Platform.

[2.4.4 Activation du segment](./ex4.md)

Dans cet exercice, vous activerez votre segment de diffusion en continu vers votre destination EventHub de la plateforme de données clients en temps réel.

[2.4.5 Création de votre projet Microsoft Azure](./ex5.md)

Dans cet exercice, vous allez créer une fonction Azure qui sera déclenchée en temps réel lorsque Adobe Experience Platform active les qualifications de segments vers la destination Azure Event Hub correspondante.

[2.4.6 Scénario de bout en bout](./ex6.md)

À ce stade, tout est configuré. Vous pouvez désormais naviguer sur votre site web de démonstration AEP et obtenir les qualifications de segment fournies à votre fonction de déclenchement Microsoft Azure EventHub.

[Résumé et avantages](./summary.md)

Résumé de ce module et aperçu des avantages.

>[!NOTE]
>
>Merci d’investir votre temps à apprendre tout ce qu’il y a à savoir sur Adobe Experience Platform et ses applications. Si vous avez des questions, si vous souhaitez partager les commentaires généraux d’avoir des suggestions sur le contenu futur, contactez directement les initiés de technologie, en envoyant un email à **techinsiders@adobe.com**.

[Revenir à tous les modules](../../../overview.md)
