---
title: Diffusion en continu de données d’Apache Kafka vers Adobe Experience Platform
description: Dans ce module, vous apprendrez à configurer votre propre grappe Apache Kafka, à définir des rubriques, des producteurs et des consommateurs et à diffuser des données dans Adobe Experience Platform à l’aide de Adobe Experience Platform Sink Connector for Kafka Connect.
kt: 5342
audience: Data Engineer, Data Architect, Data Analyst
doc-type: tutorial
activity: develop
exl-id: e1e283b1-93b7-4d06-b9ed-beac48a99c3f
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '419'
ht-degree: 2%

---

# 15. Diffusez les données d’Apache Kafka vers Adobe Experience Platform.

**Auteurs : [Vivek Tiwari](https://www.linkedin.com/in/vivek-tiwari-25092656/), [Nipun Nair](https://www.linkedin.com/in/nipunnair/), [Wouter Van Geluwe](https://www.linkedin.com/in/woutervangeluwe/)**

Dans ce module, vous allez apprendre à configurer votre propre grappe Apache Kafka, à définir des rubriques, des producteurs et des consommateurs et à diffuser des données dans Adobe Experience Platform à l’aide de Adobe Experience Platform Sink Connector via Kafka Connect.

## Objectifs d’apprentissage

- Exécution d’une configuration de base d’une grappe Kafka locale
- Créez un sujet Kafka, utilisez un producteur Kafka et un consommateur Kafka.
- Configuration de Kafka Connect et du connecteur Adobe Experience Platform Sink
- Générer manuellement des événements et voir ces événements être ingérés dans Adobe Experience Platform
- Utilisation d’une bibliothèque de producteurs Twitter existante de Kafka Connect pour diffuser des données Twitter dans Adobe Experience Platform

## Conditions préalables

- Java JDK11 ou version ultérieure doit être installé sur votre ordinateur. Vous pouvez télécharger ce JDK ici : [https://www.oracle.com/java/technologies/javase-jdk11-downloads.html](https://www.oracle.com/java/technologies/javase-jdk11-downloads.html)
- Un accès à Adobe Experience Platform

## Aperçu de l’architecture

Regardez l’architecture ci-dessous, qui met en évidence les composants qui seront discutés et utilisés dans ce module.

![Aperçu de l’architecture](../../assets/images/architecturem24.png)

## Environnement de test à utiliser

Pour ce module, utilisez cet environnement de test : `--aepSandboxId--`.

>[!NOTE]
>
>N’oubliez pas d’installer, de configurer et d’utiliser l’extension Chrome comme référencé dans [0.1 - Installation de l’extension Chrome pour la documentation Experience League](../module0/ex1.md)

## Exercices

[15.1 Présentation d’Apache Kafka](./ex1.md)

Dans cet exercice, vous découvrirez les principes de base d’Apache Kafka

[15.2 Installation et configuration de votre grappe Kafka](./ex2.md)

Dans cet exercice, vous allez télécharger, installer et configurer votre grappe Apache Kafka de base.

[15.3 Configuration du point de terminaison Diffusion en continu de l’API HTTP dans Adobe Experience Platform](./ex3.md)

Dans cet exercice, vous allez configurer un connecteur source d’API HTTP dans Adobe Experience Platform.

[15.4 Installation et configuration de Kafka Connect et du connecteur Adobe Experience Platform Sink](./ex4.md)

Au cours de cet exercice, vous utiliserez Kafka Connect pour installer et utiliser le connecteur Adobe Experience Platform Sink et vous enverrez les événements manuellement dans Adobe Experience Platform.

[Résumé et avantages](./summary.md)

Résumé de ce module et aperçu des avantages.

>[!NOTE]
>
>Merci d&#39;investir votre temps dans l&#39;apprentissage de Adobe Experience Platform. Si vous avez des questions, souhaitez partager les commentaires généraux d&#39;avoir des suggestions sur le contenu futur, contactez directement Wouter Van Geluwe en envoyant un email à **vangeluw@adobe.com**.

[Revenir à tous les modules](../../overview.md)
