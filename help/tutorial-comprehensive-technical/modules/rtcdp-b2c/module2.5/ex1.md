---
title: Collecte de données Adobe Experience Platform et transfert côté événement en temps réel - Création d’une propriété Transfert d’événement de collecte de données Adobe Experience Platform
description: Création d’une propriété Transfert d’événement de collecte de données Adobe Experience Platform
kt: 5342
doc-type: tutorial
exl-id: 9c64e57d-c91c-4d4c-923f-91a02edeb2ac
source-git-commit: 6485bfa1c75c43bb569f77c478a273ace24a61d4
workflow-type: tm+mt
source-wordcount: '736'
ht-degree: 1%

---

# 2.5.1 Création d’une propriété Transfert d’événement de collecte de données Adobe Experience Platform

## Qu’est-ce qu’une propriété Transfert d’événement de collecte de données Adobe Experience Platform ?

En règle générale, lorsque des données sont collectées à l’aide de la collecte de données Adobe Experience Platform, elles sont collectées sur le **côté client**. **côté client** est un environnement tel qu’un site web ou une application mobile. Dans Prise en main et collecte de données, la configuration d’une propriété du client de collecte de données Adobe Experience Platform a été abordée en détail. Vous avez mis en oeuvre cette propriété du client de collecte de données Adobe Experience Platform sur votre site web et votre application mobile, de sorte que les données puissent y être collectées lorsqu’un client interagissait avec le site web et l’application mobile.

Lorsque ces données d’interaction sont collectées par la propriété Client de collecte de données Adobe Experience Platform, une demande est envoyée par le site web ou l’application mobile à Edge de l’Adobe. Edge est l’environnement de collecte de données d’Adobe et le point d’entrée des données de parcours de navigation dans l’écosystème d’Adobe. À partir d’Edge, les données collectées sont ensuite envoyées aux applications telles que Adobe Experience Platform, Adobe Analytics, Adobe Audience Manager ou Adobe Target.

Avec l’ajout d’une propriété Transfert d’événement de collecte de données Adobe Experience Platform, il est désormais possible de configurer une propriété Collecte de données Adobe Experience Platform qui écoute les données entrantes sur Edge. Lorsque la propriété Transfert d’événement de collecte de données Adobe Experience Platform qui s’exécute sur Edge voit les données entrantes, elle peut les utiliser et les transférer ailleurs. Cet autre emplacement peut désormais être un webhook externe non Adobe, ce qui permet d’envoyer ces données à par exemple, votre lac de données de votre choix, une application de prise de décision ou toute autre application ayant la capacité d’ouvrir un webhook.

La configuration d’une propriété Transfert d’événement de collecte de données Adobe Experience Platform semble familière à une propriété côté client, avec la possibilité de configurer des éléments de données et des règles comme par le passé avec les propriétés du client de collecte de données Adobe Experience Platform. Toutefois, la manière dont les données seront accessibles et utilisées sera légèrement différente, selon votre cas d’utilisation.

Commençons par créer la propriété Transfert d’événement de collecte de données Adobe Experience Platform.

## Création d’une propriété Transfert d’événement de collecte de données Adobe Experience Platform

Accédez à [https://experience.adobe.com/#/data-collection/](https://experience.adobe.com/#/data-collection/). Dans le menu de gauche, cliquez sur **Transfert d’événement**. Vous verrez ensuite un aperçu de toutes les propriétés de transfert d’événement de collecte de données Adobe Experience Platform disponibles. Cliquez sur le bouton **Créer une propriété** .

![Adobe Experience Platform Data Collection SSF](./images/launchhome.png)

Si d’autres propriétés de transfert d’événement ont déjà été créées, l’interface utilisateur se présente différemment. Dans ce cas, cliquez sur **Nouvelle propriété**.

![Adobe Experience Platform Data Collection SSF](./images/launchhomea.png)

Vous devez maintenant saisir un nom pour la propriété Transfert d’événement de collecte de données Adobe Experience Platform. Pour la convention d’affectation des noms, utilisez `--aepUserLdap-- - Demo System (DD/MM/YYYY) (Edge)`. Par exemple, dans cet exemple, le nom est **vangeluw - Demo System (22/02/2022) (Edge)**. Cliquez sur **Enregistrer**.

![Adobe Experience Platform Data Collection SSF](./images/ssf1.png)

Vous revenez alors dans la liste des propriétés de transfert d’événement de collecte de données Adobe Experience Platform. Cliquez sur pour ouvrir la propriété que vous venez de créer.

![Adobe Experience Platform Data Collection SSF](./images/ssf2.png)

## Configuration de l’extension Adobe Cloud Connector

Dans le menu de gauche, accédez à **Extensions**. Vous verrez que l’extension **Core** est déjà configurée.

![Adobe Experience Platform Data Collection SSF](./images/ssf3.png)

Accédez à **Catalog**. Vous verrez l’extension **Adobe Cloud Connector**, ainsi que de nombreuses autres. Cliquez sur **Installer** pour l’installer.

![Adobe Experience Platform Data Collection SSF](./images/ssf4.png)

L’extension sera alors ajoutée. Il n’y a aucune configuration à faire à cette étape. Vous serez renvoyé à la présentation des extensions installées.

![Adobe Experience Platform Data Collection SSF](./images/ssf5.png)

## Déployer la propriété Transfert d’événement de collecte de données Adobe Experience Platform

Dans le menu de gauche, accédez à **Flux de publication**. Cliquez sur **Ajouter une bibliothèque**.

![Adobe Experience Platform Data Collection SSF](./images/ssf6.png)

Saisissez le nom **Main**, sélectionnez l’environnement **Développement (développement)** et cliquez sur **+ Ajouter toutes les ressources modifiées**.

![Adobe Experience Platform Data Collection SSF](./images/ssf7.png)

Vous verrez alors ceci. Cliquez sur **Enregistrer et générer pour le développement**.

![Adobe Experience Platform Data Collection SSF](./images/ssf8.png)

Votre bibliothèque sera alors créée, ce qui peut prendre entre 1 et 2 minutes.

![Adobe Experience Platform Data Collection SSF](./images/ssf10.png)

Étape suivante : [2.5.2 Mettre à jour votre flux de données pour rendre les données disponibles pour la propriété de transfert des événements de collecte de données](./ex2.md)

[Revenir au module 2.5](./aep-data-collection-ssf.md)

[Revenir à tous les modules](./../../../overview.md)
