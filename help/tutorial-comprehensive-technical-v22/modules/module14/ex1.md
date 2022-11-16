---
title: Collecte de données Adobe Experience Platform et transfert côté événement en temps réel - Création d’une propriété Transfert d’événement de collecte de données Adobe Experience Platform
description: Création d’une propriété Transfert d’événement de collecte de données Adobe Experience Platform
kt: 5342
audience: Data Engineer, Data Architect, Data Analyst
doc-type: tutorial
activity: develop
exl-id: 2ca908a3-28b9-48d4-b96e-00951de530ba
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '747'
ht-degree: 2%

---

# 14.1 Création d’une propriété Transfert d’événement de collecte de données Adobe Experience Platform

>[!NOTE]
>
>L’extension mobile Adobe Experience Platform Edge est actuellement en version bêta. L’utilisation de cette extension est réalisée sur invitation uniquement. Veuillez contacter votre responsable du succès client Adobe pour en savoir plus et accéder aux ressources de ce tutoriel.

## 14.1.1 Qu’est-ce qu’une propriété Transfert d’événement de collecte de données Adobe Experience Platform ?

En règle générale, lorsque des données sont collectées à l’aide de la collecte de données Adobe Experience Platform, elles sont collectées sur la variable **Côté client**. Le **Côté client** est un environnement tel qu’un site web ou une application mobile. Dans les modules 0 et 1, la configuration d’une propriété du client de collecte de données Adobe Experience Platform a fait l’objet de discussions approfondies et vous avez implémenté cette propriété du client de collecte de données Adobe Experience Platform sur votre site web et votre application mobile, de sorte que les données puissent y être collectées lorsqu’un client interagissait avec le site web et l’application mobile.

Lorsque ces données d’interaction sont collectées par la propriété Client de collecte de données Adobe Experience Platform, une demande est envoyée par le site web ou l’application mobile à l’Adobe Edge. L’Edge est l’environnement de collecte de données de l’Adobe et est le point d’entrée des données de parcours de navigation dans l’écosystème de l’Adobe. Depuis Edge, les données collectées sont ensuite envoyées aux applications telles que Adobe Experience Platform, Adobe Analytics, Adobe Audience Manager ou Adobe Target.

Avec l’ajout d’une propriété Transfert d’événement de collecte de données Adobe Experience Platform, il est désormais possible de configurer une propriété Collecte de données Adobe Experience Platform qui écoute les données entrantes sur le Edge. Lorsque la propriété Transfert d’événement de collecte de données Adobe Experience Platform en cours d’exécution sur Edge voit les données entrantes, elle peut les utiliser et les transférer ailleurs. Cet autre emplacement peut désormais être un webhook externe non Adobe, ce qui permet d’envoyer ces données à par exemple, votre lac de données de votre choix, une application de prise de décision ou toute autre application ayant la capacité d’ouvrir un webhook.

La configuration d’une propriété Transfert d’événement de collecte de données Adobe Experience Platform semble familière à une propriété client, avec la possibilité de configurer des éléments de données et des règles comme par le passé avec les propriétés du client de collecte de données Adobe Experience Platform. Toutefois, la manière dont les données seront accessibles et utilisées sera légèrement différente, selon votre cas d’utilisation.

Commençons par créer la propriété Transfert d’événement de collecte de données Adobe Experience Platform.

## 14.1.2 Création d’une propriété Transfert d’événement de collecte de données Adobe Experience Platform

Accédez à [https://experience.adobe.com/#/data-collection/](https://experience.adobe.com/#/data-collection/). Dans le menu de gauche, cliquez sur **Transfert d’événement**. Vous verrez ensuite un aperçu de toutes les propriétés de transfert d’événement de collecte de données Adobe Experience Platform disponibles. Cliquez sur le bouton **Nouvelle propriété** bouton .

![Transfert côté serveur de la collecte de données Adobe Experience Platform](./images/launchhome.png)

Vous devez maintenant saisir un nom pour la propriété Transfert d’événement de collecte de données Adobe Experience Platform. Pour définir une convention d’affectation des noms, utilisez `--demoProfileLdap-- - Demo System (DD/MM/YYYY) (Edge)`. Par exemple, dans cet exemple, le nom est **vangeluw - Système de démonstration (22/02/2022) (Edge)**. Cliquez sur **Enregistrer**.

![Transfert côté serveur de la collecte de données Adobe Experience Platform](./images/ssf1.png)

Vous revenez alors dans la liste des propriétés de transfert d’événement de collecte de données Adobe Experience Platform. Cliquez sur pour ouvrir la propriété que vous venez de créer.

![Transfert côté serveur de la collecte de données Adobe Experience Platform](./images/ssf2.png)

## 14.1.2 Configuration de l’extension Adobe Cloud Connector

Dans le menu de gauche, accédez à **Extensions**. Vous verrez que la variable **Core** est déjà configurée.

![Transfert côté serveur de la collecte de données Adobe Experience Platform](./images/ssf3.png)

Accédez à **Catalogue**. Vous verrez le **Connecteur Adobe Cloud** extension . Cliquez sur **Installer** pour l’installer.

![Transfert côté serveur de la collecte de données Adobe Experience Platform](./images/ssf4.png)

L’extension sera alors ajoutée. Il n’y a aucune configuration à faire à cette étape. Vous serez renvoyé à la présentation des extensions installées.

![Transfert côté serveur de la collecte de données Adobe Experience Platform](./images/ssf5.png)

## 14.1.3 Déploiement de la propriété Transfert d’événement de collecte de données Adobe Experience Platform

Dans le menu de gauche, accédez à **Flux de publication**. Cliquez sur **Ajouter une bibliothèque**.

![Transfert côté serveur de la collecte de données Adobe Experience Platform](./images/ssf6.png)

Saisissez le nom **Principal**, sélectionnez l’environnement. **Développement (développement)** et cliquez sur **+ Ajouter toutes les ressources modifiées**.

![Transfert côté serveur de la collecte de données Adobe Experience Platform](./images/ssf7.png)

Vous verrez alors ceci. Cliquez sur **Enregistrer et générer pour le développement**.

![Transfert côté serveur de la collecte de données Adobe Experience Platform](./images/ssf8.png)

Votre bibliothèque sera alors créée, ce qui peut prendre entre 1 et 2 minutes.

![Transfert côté serveur de la collecte de données Adobe Experience Platform](./images/ssf9.png)

Enfin, votre bibliothèque sera créée et prête.

![Transfert côté serveur de la collecte de données Adobe Experience Platform](./images/ssf10.png)

Étape suivante : [14.2 Mettez à jour votre flux de données pour rendre les données disponibles pour la propriété Transfert d’événement de collecte de données](./ex2.md)

[Revenir au module 14](./aep-data-collection-ssf.md)

[Revenir à tous les modules](./../../overview.md)
