---
title: Configuration du point d’entrée de l’API HTTP dans Adobe Experience Platform
description: Configuration du point d’entrée de l’API HTTP dans Adobe Experience Platform
kt: 5342
audience: Data Engineer, Data Architect, Data Analyst
doc-type: tutorial
activity: develop
exl-id: 3346c57b-3a78-40b1-a891-053fc8781659
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '321'
ht-degree: 9%

---

# 15.3 Configuration du point de terminaison Diffusion en continu de l’API HTTP dans Adobe Experience Platform

Avant de pouvoir configurer Adobe Experience Platform Sink Connector dans Kafka, vous devez créer un connecteur source API HTTP dans Adobe Experience Platform. L’URL du point de terminaison HTTP API Streaming est requise pour configurer Adobe Experience Platform Sink Connector.

Pour créer un connecteur source d’API HTTP, connectez-vous à Adobe Experience Platform en accédant à cette URL : [https://experience.adobe.com/platform](https://experience.adobe.com/platform).

Une fois connecté, vous accédez à la page d’accueil de Adobe Experience Platform.

![Ingestion des données](../module2/images/home.png)

Avant de continuer, vous devez sélectionner une **sandbox**. L’environnement de test à sélectionner est nommé ``--aepSandboxId--``. Pour ce faire, cliquez sur le texte **[!UICONTROL Production Prod]** dans la ligne bleue en haut de votre écran. Après avoir sélectionné l’environnement de test approprié, l’écran change et vous êtes désormais dans votre environnement de test dédié.

![Ingestion des données](../module2/images/sb1.png)

Dans le menu de gauche, accédez à **Sources** et faites défiler l’écran vers le bas **Catalogue de sources** jusqu’à ce que vous voyiez **API HTTP**. Cliquez sur **Ajouter des données**.

![Ingestion des données](./images/kaep1.png)

Cliquez sur **Nouveau compte**. Utilisation `--demoProfileLdap-- - Kafka` comme nom de votre connexion API HTTP, dans ce cas **vangeluw - Kafka**. Activez la case à cocher pour **Compatible XDM**. Cliquez sur **Connexion à la source**.

![Ingestion des données](./images/kaep2.png)

Vous verrez alors ceci, cliquez sur **Suivant**.

![Ingestion des données](./images/kaep3.png)

Sélectionner **Jeu de données existant**, ouvrez le menu déroulant. Recherche et sélection du jeu de données **Système de démonstration - Jeu de données d’événement pour le centre d’appels (Global v1.1)**.

![Ingestion des données](./images/kaep4.png)

Cliquez sur **Suivant**.

![Ingestion des données](./images/kaep6.png)

Cliquez sur **Suivant**.

![Ingestion des données](./images/kaep7.png)

Cliquez sur **Terminer**.

![Ingestion des données](./images/kaep8.png)

Vous verrez ensuite un aperçu du connecteur source de l’API HTTP que vous venez de créer.

![Ingestion des données](./images/kaep9.png)

Vous devez copier la variable **Point de terminaison de diffusion** URL, qui ressemble à celle ci-dessous, comme vous en aurez besoin lors de l’exercice suivant.

`https://dcs.adobedc.net/collection/d282bbfc8a540321341576275a8d052e9dc4ea80625dd9a5fe5b02397cfd80dc`

Vous avez terminé cet exercice.

Étape suivante : [15.4 Installation et configuration de Kafka Connect et du connecteur Adobe Experience Platform Sink](./ex4.md)

[Revenir au module 15](./aep-apache-kafka.md)

[Revenir à tous les modules](../../overview.md)
