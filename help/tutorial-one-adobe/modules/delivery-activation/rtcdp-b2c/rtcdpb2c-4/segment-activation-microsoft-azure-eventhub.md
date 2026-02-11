---
title: Hub d’événements Azure d’Audience Activation vers Microsoft
description: Hub d’événements Azure d’Audience Activation vers Microsoft
kt: 5342
doc-type: tutorial
exl-id: c1f5566d-0f57-4554-95ee-950d66373716
source-git-commit: 2d5ca888eb24c1f65b4ecd48030ec8d1659b7f84
workflow-type: tm+mt
source-wordcount: '539'
ht-degree: 0%

---

# 2.4 Real-Time CDP : Audience Activation vers Microsoft Azure Event Hub

Dans ce module, vous allez configurer une destination Microsoft Azure EventHub en tant que destination en temps réel pour Adobe Experience Platform Real-time CDP. Vous allez également configurer et déployer une fonction Azure qui sera déclenchée en temps réel chaque fois que Adobe Experience Platform diffuse une payload d’audience vers votre destination Azure EventHub. La fonction Azure que vous déclencherez affichera le mécanisme des fonctionnalités d’activation de Adobe Experience Platform Real-time CDP.

Dans le cadre de ce module, vous comprendrez également ce qui déclenche la plateforme de données clients en temps réel pour diffuser une payload vers une destination spécifiée. Nous discuterons également du statut d’une qualification d’audience et de sa relation avec l’activation.

La plateforme de données clients en temps réel de Adobe Experience Platform prend en charge l’activation des données vers des destinations d’espace de stockage en flux continu, ce qui vous permet d’exporter des données et des événements d’audience en temps réel vers ces destinations au format JSON. Vous pouvez ensuite décrire la logique commerciale en plus de ces événements dans vos destinations

Microsoft Azure Event Hubs est un service d’ingestion de données en temps réel, entièrement géré, simple, fiable et évolutif. Diffusez des millions d’événements par seconde à partir de n’importe quelle source pour créer des pipelines de données dynamiques et répondre immédiatement aux défis commerciaux.

## Objectifs d’apprentissage

- Familiarisez-vous avec les Microsoft Azure Event Hubs
- Configurer une destination RTCDP vers votre hub d’événements Microsoft Azure
- Découvrez quand Real-time CDP s’active et à quoi ressemble la payload d’activation
- Configurez Visual Studio Code pour développer, tester et déployer votre projet Azure
- Créez et déployez une fonction Azure qui utilise les qualifications d’audience diffusées en temps réel par RTCDP

## Conditions préalables

- Accès à [Adobe Experience Platform](https://experience.adobe.com/platform)
- Découvrez comment définir, utiliser et activer des audiences dans Adobe Experience Platform

>[!NOTE]
>
>N’oubliez pas d’installer, de configurer et d’utiliser l’extension Chrome, comme indiqué dans [Installation de l’extension Chrome pour la documentation Experience League](../../../getting-started/gettingstarted/ex1.md)

## Exercices

[2.4.1 Configuration de votre environnement](./ex1.md)

Dans cet exercice, vous allez configurer votre environnement Microsoft Azure.

[2.4.2 Configuration de votre environnement Microsoft Azure EventHub](./ex2.md)

Dans cet exercice, vous allez configurer votre environnement Microsoft Azure EventHub.

[2.4.3 Configuration de la destination Azure Event Hub dans Adobe Experience Platform](./ex3.md)

Dans cet exercice, vous allez configurer votre connexion de destination Real-time CDP qui diffusera des audiences en temps réel vers l’instance Event Hub que vous avez configurée dans l’exercice précédent.

[2.4.4 Création d’une audience](./ex4.md)

Dans cet exercice, vous allez créer une audience dans Adobe Experience Platform

[2.4.5 Activer votre audience](./ex5.md)

Dans cet exercice, vous allez activer votre audience vers votre destination EventHub.

[2.4.6 Création de votre projet Microsoft Azure](./ex6.md)

Dans cet exercice, vous allez créer une fonction Azure qui sera déclenchée en temps réel lorsqu’Adobe Experience Platform délivrera les qualifications d’audience à la destination correspondante du hub d’événements Azure.

[2.4.7 Scénario de bout en bout](./ex7.md)

À ce stade, tout est configuré. Vous pouvez désormais effectuer une navigation sur votre site web de démonstration et obtenir les qualifications d’audience diffusées à votre fonction de déclencheur de hub d’événement d’Azure de Microsoft.

![Insiders de la technologie &#x200B;](./../../../../assets/images/techinsiders.png){width="50px" align="left"}

>[!NOTE]
>
>Merci d’avoir consacré votre temps à apprendre tout ce qu’il y a à savoir sur Adobe Experience Platform et ses applications. Si vous avez des questions, si vous souhaitez partager des commentaires généraux ou si vous avez des suggestions sur le contenu futur, veuillez contacter directement les initiés techniques, en envoyant un e-mail à **techinsiders@adobe.com**.

[Revenir à tous les modules](./../../../../overview.md)
