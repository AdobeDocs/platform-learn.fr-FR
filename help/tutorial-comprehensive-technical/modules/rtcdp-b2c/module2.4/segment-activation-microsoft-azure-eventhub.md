---
title: Audience Activation à Microsoft Azure Event Hub
description: Audience Activation à Microsoft Azure Event Hub
kt: 5342
doc-type: tutorial
exl-id: 23713cb4-2055-43e8-9380-0ca8845a75e8
source-git-commit: 216914c9d97827afaef90e21ed7d4f35eaef0cd3
workflow-type: tm+mt
source-wordcount: '549'
ht-degree: 0%

---

# 2.4 Real-Time CDP : Audience Activation à Microsoft Azure Event Hub

Dans ce module, vous allez configurer une destination Microsoft Azure EventHub en tant que destination en temps réel pour la plateforme de données clients en temps réel de Adobe Experience Platform. Vous allez également configurer et déployer une fonction Azure qui sera déclenchée en temps réel chaque fois que Adobe Experience Platform envoie une charge utile d’audience à votre destination Azure EventHub. La fonction Azure que vous allez déclencher affichera le mécanisme des fonctionnalités d’activation de la plateforme de données clients en temps réel de Adobe Experience Platform.

Dans le cadre de ce module, vous comprendrez également ce qui déclenche la diffusion d’une charge utile en temps réel sur une destination spécifiée par la plateforme CDP en temps réel. Nous discuterons également de l’état d’une qualification d’audience et de sa relation avec l’activation.

La plateforme de données clients en temps réel de Adobe Experience Platform prend en charge l’activation des données vers les destinations de stockage dans le cloud en continu, ce qui vous permet d’exporter des données et des événements d’audience en temps réel vers ces destinations au format JSON. Vous pouvez ensuite décrire la logique commerciale en plus de ces événements dans vos destinations

Microsoft Azure Event Hubs est un service d’ingestion de données en temps réel entièrement géré, simple, fiable et évolutif. Diffusez des millions d’événements par seconde depuis n’importe quelle source pour créer des pipelines de données dynamiques et répondre immédiatement aux défis de l’entreprise.

## Objectifs d’apprentissage

- Familiarisez-vous avec les centres d’événements Microsoft Azure
- Configuration d’une destination RTCDP sur votre centre d’événements Microsoft Azure
- Comprendre quand la plateforme CDP en temps réel est activée et à quoi ressemble la payload d’activation
- Configuration du code Visual Studio pour développer, tester et déployer votre projet Azure
- Créer et déployer une fonction Azure qui utilise les qualifications d’audience fournies en temps réel par RTCDP

## Conditions préalables

- Accès à [Adobe Experience Platform](https://experience.adobe.com/platform)
- Comprendre comment définir, utiliser et activer des audiences dans Adobe Experience Platform

>[!NOTE]
>
>N’oubliez pas d’installer, de configurer et d’utiliser l’extension Chrome comme référencé dans [Installation de l’extension Chrome pour la documentation Experience League](../../gettingstarted/gettingstarted/ex1.md)

## Exercices

[2.4.1 Configuration de votre environnement](./ex1.md)

Dans cet exercice, vous allez configurer votre environnement Microsoft Azure.

[2.4.2 Configuration de votre environnement Microsoft Azure EventHub](./ex2.md)

Dans cet exercice, vous allez configurer votre environnement Microsoft Azure EventHub.

[2.4.3 Configuration de votre destination Azure Event Hub dans Adobe Experience Platform](./ex3.md)

Dans cet exercice, vous allez configurer votre connexion de destination de la plateforme de données clients en temps réel qui diffusera des audiences en temps réel vers l’instance Event Hub que vous avez configurée dans l’exercice précédent.

[2.4.4 Création d’une audience](./ex4.md)

Dans cet exercice, vous allez créer une audience dans Adobe Experience Platform

[2.4.5 Activation de l’audience](./ex5.md)

Dans cet exercice, vous activerez votre audience vers votre destination EventHub.

[2.4.6 Création de votre projet Microsoft Azure](./ex6.md)

Dans cet exercice, vous allez créer une fonction Azure qui sera déclenchée en temps réel lorsque la plateforme Adobe Experience fournit des qualifications d’audience à la destination Azure Event Hub correspondante.

[2.4.7 Scénario de bout en bout](./ex7.md)

À ce stade, tout est configuré. Vous pouvez désormais naviguer sur votre site web de démonstration et obtenir les qualifications d’audience fournies à votre fonction de déclenchement Microsoft Azure Event Hub.

[Résumé et avantages](./summary.md)

Résumé de ce module et aperçu des avantages.

>[!NOTE]
>
>Merci d’investir votre temps à apprendre tout ce qu’il y a à savoir sur Adobe Experience Platform et ses applications. Si vous avez des questions, si vous souhaitez partager les commentaires généraux d’avoir des suggestions sur le contenu futur, contactez directement les initiés de technologie, en envoyant un email à **techinsiders@adobe.com**.

[Revenir à tous les modules](../../../overview.md)
