---
title: Diffusion de données d’Apache Kafka vers Adobe Experience Platform
description: Dans ce module, vous apprendrez à configurer votre propre cluster Apache Kafka, à définir des rubriques, des producteurs et des consommateurs et à diffuser des données dans Adobe Experience Platform à l’aide du connecteur de récepteur Adobe Experience Platform pour Kafka Connect.
kt: 5342
doc-type: tutorial
exl-id: 2b7010f3-ab31-4099-aecd-fd4e73b7e96e
source-git-commit: bd46be455f88007174f7e6be9a1ce5f508edc09b
workflow-type: tm+mt
source-wordcount: '368'
ht-degree: 1%

---

# 2.6 Diffuser des données d’Apache Kafka vers Adobe Experience Platform

Dans ce module, vous apprendrez à configurer votre propre cluster Apache Kafka, à définir des rubriques, des producteurs et des consommateurs et à diffuser des données dans Adobe Experience Platform à l’aide du connecteur de récepteur Adobe Experience Platform via Kafka Connect.

## Objectifs d’apprentissage

- Effectuer une configuration de base d’un cluster Kafka local
- Créez une rubrique Kafka, utilisez un producteur Kafka et un consommateur Kafka
- Configuration de Kafka Connect et du connecteur de récepteur Adobe Experience Platform
- Générez manuellement des événements et vérifiez qu’ils sont ingérés dans Adobe Experience Platform.
- Utilisez une bibliothèque de producteurs de Twitter existante de Kafka Connect pour diffuser des données de Twitter dans Adobe Experience Platform

## Conditions préalables

- Java JDK23 ou version ultérieure doit être installé sur votre ordinateur. Vous pouvez télécharger ce JDK ici : [https://www.oracle.com/java/technologies/javase-jdk11-downloads.html](https://www.oracle.com/java/technologies/javase-jdk11-downloads.html)
- Accès à Adobe Experience Platform

>[!NOTE]
>
>N’oubliez pas d’installer, de configurer et d’utiliser l’extension Chrome, comme indiqué dans [Installation de l’extension Chrome pour la documentation de l’Experience League &#x200B;](../../gettingstarted/gettingstarted/ex1.md)

## Exercices

[2.6.1 Présentation d’Apache Kafka](./ex1.md)

Dans cet exercice, vous découvrirez les principes de base d’Apache Kafka

[2.6.2 Installation et configuration de votre cluster Kafka](./ex2.md)

Dans cet exercice, vous allez télécharger, installer et configurer votre cluster Apache Kafka de base.

[2.6.3 Configuration du point d’entrée de flux continu d’API HTTP dans Adobe Experience Platform](./ex3.md)

Dans cet exercice, vous allez configurer un connecteur Source d’API HTTP dans Adobe Experience Platform.

[2.6.4 Installation et configuration de Kafka Connect et du connecteur de récepteur Adobe Experience Platform](./ex4.md)

Dans cet exercice, vous utiliserez Kafka Connect pour installer et utiliser le connecteur de récepteur Adobe Experience Platform et vous enverrez manuellement des événements dans Adobe Experience Platform.

[Résumé et avantages](./summary.md)

Résumé de ce module et aperçu des avantages.

![Insiders de la technologie &#x200B;](./../../../assets/images/techinsiders.png){width="50px" align="left"}

>[!NOTE]
>
>Merci d’avoir consacré votre temps à apprendre tout ce qu’il y a à savoir sur Adobe Experience Platform et ses applications. Si vous avez des questions, si vous souhaitez partager des commentaires généraux ou si vous avez des suggestions sur le contenu futur, veuillez contacter directement les initiés techniques, en envoyant un e-mail à **techinsiders@adobe.com**.

[Revenir à tous les modules](../../../overview.md)
