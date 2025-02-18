---
title: Configuration du point d’entrée de l’API HTTP dans Adobe Experience Platform
description: Configuration du point d’entrée de l’API HTTP dans Adobe Experience Platform
kt: 5342
doc-type: tutorial
exl-id: 621a4db7-0aff-42bf-ad42-daec6e924451
source-git-commit: 3d61d91111d8693ab031fbd7b26706c02818108c
workflow-type: tm+mt
source-wordcount: '305'
ht-degree: 7%

---

# 2.6.3 Configuration du point d’entrée de flux continu d’API HTTP dans Adobe Experience Platform

Avant de pouvoir configurer le connecteur de récepteur Adobe Experience Platform dans Kafka, vous devez créer un connecteur Source d’API HTTP dans Adobe Experience Platform. L’URL du point d’entrée de flux continu d’API HTTP est requise pour configurer le connecteur de récepteur Adobe Experience Platform.

Pour créer un connecteur Source d’API HTTP, connectez-vous à Adobe Experience Platform en accédant à cette URL : [https://experience.adobe.com/platform](https://experience.adobe.com/platform).

Une fois connecté, vous accédez à la page d’accueil de Adobe Experience Platform.

![Ingestion des données](./../../../../modules/delivery-activation/datacollection/dc1.2/images/home.png)

Avant de continuer, vous devez sélectionner un **sandbox**. Le sandbox à sélectionner est nommé ``--aepSandboxName--``. Après avoir sélectionné la sandbox appropriée, la modification d’écran s’affiche et vous êtes maintenant dans votre sandbox dédiée.

![Ingestion des données](./../../../../modules/delivery-activation/datacollection/dc1.2/images/sb1.png)

Dans le menu de gauche, accédez à **Sources** et faites défiler l’écran vers le bas dans le **Catalogue des sources** jusqu’à afficher **API HTTP**. Cliquez sur **Configurer**.

![Ingestion des données](./images/kaep1.png)

Cliquez sur **Nouveau compte**. Utilisez `--aepUserLdap-- - Kafka` comme nom de connexion API HTTP, dans ce cas **vangeluw - Kafka**. Cochez la case **Compatible avec XDM**. Cliquez sur **Connexion à la source**.

![Ingestion des données](./images/kaep2.png)

Pour afficher ce message, cliquez sur **Suivant**.

![Ingestion des données](./images/kaep3.png)

Sélectionnez **Jeu de données existant**, puis ouvrez le menu déroulant. Recherchez et sélectionnez le jeu de données **Système de démonstration - Jeu de données d’événement pour le centre d’appels (global v1.1)**.

Cliquez sur **Suivant**.

![Ingestion des données](./images/kaep4.png)

Cliquez sur **Terminer**.

![Ingestion des données](./images/kaep8.png)

Vous verrez ensuite un aperçu du connecteur Source d’API HTTP que vous venez de créer.

Vous devez copier l’URL **Point d’entrée de diffusion en continu**, qui ressemble à celle ci-dessous, car vous en aurez besoin dans l’exercice suivant.

`https://dcs.adobedc.net/collection/63751d0f299eeb7aa48a2f22acb284ed64de575f8640986d8e5a935741be9067`

![Ingestion des données](./images/kaep9.png)

Vous avez terminé cet exercice.

## Étapes suivantes

Accédez à [2.6.4 Installation et configuration de Kafka Connect et du connecteur de récepteur Adobe Experience Platform](./ex4.md){target="_blank"}

Revenez à [Diffuser des données d’Apache Kafka vers Adobe Experience Platform](./aep-apache-kafka.md){target="_blank"}

Revenir à [Tous les modules](./../../../../overview.md){target="_blank"}
