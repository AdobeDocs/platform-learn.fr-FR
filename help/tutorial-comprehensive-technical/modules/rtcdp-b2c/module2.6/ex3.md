---
title: Configuration du point d’entrée de l’API HTTP dans Adobe Experience Platform
description: Configuration du point d’entrée de l’API HTTP dans Adobe Experience Platform
kt: 5342
doc-type: tutorial
exl-id: a29dd01d-4415-45d6-ad52-7f14aef60565
source-git-commit: acb941e4ee668248ae0767bb9f4f42e067c181ba
workflow-type: tm+mt
source-wordcount: '303'
ht-degree: 8%

---

# 2.6.3 Configuration du point de terminaison de la diffusion en continu des API HTTP dans Adobe Experience Platform

Avant de pouvoir configurer Adobe Experience Platform Sink Connector dans Kafka, vous devez créer un connecteur Source API HTTP dans Adobe Experience Platform. L’URL du point de terminaison HTTP API Streaming est requise pour configurer Adobe Experience Platform Sink Connector.

Pour créer un connecteur Source d’API HTTP, connectez-vous à Adobe Experience Platform en accédant à cette URL : [https://experience.adobe.com/platform](https://experience.adobe.com/platform).

Une fois connecté, vous accédez à la page d’accueil de Adobe Experience Platform.

![Ingestion des données](./../../../modules/datacollection/module1.2/images/home.png)

Avant de continuer, vous devez sélectionner un **sandbox**. L’environnement de test à sélectionner est nommé ``--aepSandboxName--``. Après avoir sélectionné l’environnement de test approprié, l’écran change et vous êtes désormais dans votre environnement de test dédié.

![Ingestion des données](./../../../modules/datacollection/module1.2/images/sb1.png)

Dans le menu de gauche, accédez à **Sources** et faites défiler l’écran vers le bas dans le **Catalogue de sources** jusqu’à ce que l’ **API HTTP** s’affiche. Cliquez sur **Ajouter des données**.

![Ingestion des données](./images/kaep1.png)

Cliquez sur **Nouveau compte**. Utilisez `--aepUserLdap-- - Kafka` comme nom pour votre connexion API HTTP, dans ce cas **vangeluw - Kafka**. Activez la case à cocher pour **Compatible XDM**. Cliquez sur **Se connecter à la source**.

![Ingestion des données](./images/kaep2.png)

Vous verrez alors ceci, cliquez sur **Suivant**.

![Ingestion des données](./images/kaep3.png)

Sélectionnez **Jeu de données existant**, ouvrez le menu déroulant. Recherchez et sélectionnez le jeu de données **Demo System - Event Dataset for Call Center (Global v1.1)**.

![Ingestion des données](./images/kaep4.png)

Cliquez sur **Suivant**.

![Ingestion des données](./images/kaep6.png)

Cliquez sur **Suivant**.

![Ingestion des données](./images/kaep7.png)

Cliquez sur **Terminer**.

![Ingestion des données](./images/kaep8.png)

Vous verrez ensuite un aperçu du connecteur Source de l’API HTTP que vous venez de créer.

![Ingestion des données](./images/kaep9.png)

Vous devrez copier l’URL **Point d’entrée de diffusion en continu**, qui ressemble à celle ci-dessous, comme vous en aurez besoin dans l’exercice suivant.

`https://dcs.adobedc.net/collection/d282bbfc8a540321341576275a8d052e9dc4ea80625dd9a5fe5b02397cfd80dc`

Vous avez terminé cet exercice.

Étape suivante : [2.6.4 Installation et configuration de Kafka Connect et Adobe Experience Platform Sink Connector](./ex4.md)

[Revenir au module 2.6](./aep-apache-kafka.md)

[Revenir à tous les modules](../../../overview.md)
