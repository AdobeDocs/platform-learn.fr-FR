---
title: Diffusion en continu de données d’Apache Kafka vers Adobe Experience Platform
description: Dans ce module, vous apprendrez à configurer votre propre grappe Apache Kafka, à définir des rubriques, des producteurs et des consommateurs et à diffuser des données dans Adobe Experience Platform à l’aide de Adobe Experience Platform Sink Connector for Kafka Connect.
kt: 5342
doc-type: tutorial
exl-id: 2b7010f3-ab31-4099-aecd-fd4e73b7e96e
source-git-commit: 0dbcda0cfc9f199a44c845c1b5caf00a8d740251
workflow-type: tm+mt
source-wordcount: '377'
ht-degree: 1%

---

# 2.6 Diffusion de données en continu d’Apache Kafka vers Adobe Experience Platform

**Auteurs : [Vivek Tiwari](https://www.linkedin.com/in/vivek-tiwari-25092656/), [Nipun Nair](https://www.linkedin.com/in/nipunnair/), [Wouter Van Geluwe](https://www.linkedin.com/in/woutervangeluwe/)**

Dans ce module, vous apprendrez à configurer votre propre grappe Apache Kafka, à définir des rubriques, des producteurs et des consommateurs et à diffuser des données dans Adobe Experience Platform à l’aide de Adobe Experience Platform Sink Connector via Kafka Connect.

## Objectifs d’apprentissage

- Exécution d’une configuration de base d’une grappe Kafka locale
- Créez un sujet Kafka, utilisez un producteur Kafka et un consommateur Kafka.
- Configuration de Kafka Connect et du connecteur Adobe Experience Platform Sink
- Générer manuellement des événements et voir ces événements être ingérés dans Adobe Experience Platform
- Utilisation d’une bibliothèque de producteurs de Twitter existante de Kafka Connect pour diffuser des données de Twitter dans Adobe Experience Platform

## Conditions préalables

- Java JDK11 ou version ultérieure doit être installé sur votre ordinateur. Vous pouvez télécharger ce JDK ici : [https://www.oracle.com/java/technologies/javase-jdk11-downloads.html](https://www.oracle.com/java/technologies/javase-jdk11-downloads.html)
- Accès à Adobe Experience Platform

>[!NOTE]
>
>N’oubliez pas d’installer, de configurer et d’utiliser l’extension Chrome comme référencé dans [Installation de l’extension Chrome pour la documentation Experience League](../../gettingstarted/gettingstarted/ex1.md)

## Exercices

[2.6.1 Présentation d’Apache Kafka](./ex1.md)

Dans cet exercice, vous découvrirez les principes de base d’Apache Kafka

[2.6.2 Installation et configuration de votre grappe Kafka](./ex2.md)

Dans cet exercice, vous allez télécharger, installer et configurer votre grappe Apache Kafka de base.

[2.6.3 Configuration du point de terminaison de la diffusion en continu des API HTTP dans Adobe Experience Platform](./ex3.md)

Dans cet exercice, vous allez configurer un connecteur Source d’API HTTP dans Adobe Experience Platform.

[2.6.4 Installation et configuration de Kafka Connect et Adobe Experience Platform Sink Connector](./ex4.md)

Au cours de cet exercice, vous utiliserez Kafka Connect pour installer et utiliser le connecteur Adobe Experience Platform Sink et vous enverrez les événements manuellement dans Adobe Experience Platform.

[Résumé et avantages](./summary.md)

Résumé de ce module et aperçu des avantages.

>[!NOTE]
>
>Merci d’investir votre temps à apprendre tout ce qu’il y a à savoir sur Adobe Experience Platform et ses applications. Si vous avez des questions, si vous souhaitez partager les commentaires généraux d’avoir des suggestions sur le contenu futur, contactez directement les initiés de technologie, en envoyant un email à **techinsiders@adobe.com**.

[Revenir à tous les modules](../../../overview.md)
