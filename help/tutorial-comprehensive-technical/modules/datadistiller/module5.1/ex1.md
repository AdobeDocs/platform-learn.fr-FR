---
title: Query Service - Prise en main
description: Query Service - Prise en main
kt: 5342
doc-type: tutorial
exl-id: b8a404d1-7796-46e3-b245-553acdc753ae
source-git-commit: acb941e4ee668248ae0767bb9f4f42e067c181ba
workflow-type: tm+mt
source-wordcount: '645'
ht-degree: 0%

---

# 5.1.1 Prise en main

## 5.1.1.1 Prise en main de l’interface utilisateur de Adobe Experience Platform

Accédez à [Adobe Experience Platform](https://experience.adobe.com/platform). Une fois connecté, vous accédez à la page d’accueil de Adobe Experience Platform.

![Ingestion des données](./../../../modules/datacollection/module1.2/images/home.png)

Avant de continuer, vous devez sélectionner un **sandbox**. L’environnement de test à sélectionner est nommé ``--aepSandboxName--``. Après avoir sélectionné l’[!UICONTROL sandbox] approprié, vous verrez le changement d’écran et vous êtes désormais dans votre [!UICONTROL sandbox] dédié.

![Ingestion des données](./../../../modules/datacollection/module1.2/images/sb1.png)


## 5.1.1.2 Explorer les données sur la plateforme

L’import de données à partir de différents canaux est une tâche difficile pour toute marque. Et dans cet exercice, les clients Citi Signal interagissent avec Citi Signal sur son site web, sur son application mobile, les données d&#39;achat sont collectées par le système de points de vente de Citi Signal, et ils ont des données de gestion de la relation client et de fidélité. Citi Signal utilise Adobe Analytics et Adobe Launch pour capturer des données sur son site web, son application mobile et son système POS. Ces données circulent donc déjà dans Adobe Experience Platform. Commençons par explorer toutes les données de Citi Signal qui existent déjà dans Adobe Experience Platform.

Dans le menu de gauche, accédez à **Jeux de données**.

![emea-website-interaction-dataset.png](./images/emea-website-interaction-dataset.png)

Citi Signal diffuse des données dans Adobe Experience Platform et ces données sont disponibles dans le jeu de données `Demo System - Event Dataset for Website (Global v1.1)`. Recherchez `Demo System - Event Dataset for Website`.

![emea-callcenter-interaction-dataset.png](./images/emea-website-interaction-dataset1.png)

Les données Callcenter Interaction de Citi Signal sont capturées dans le jeu de données `Demo System - Event Dataset for Call Center (Global v1.1)`. Recherchez des données `Demo System - Event Dataset for Call Center` dans la zone de recherche. Cliquez sur le nom du jeu de données pour l’ouvrir.

![emea-callcenter-interaction-dataset.png](./images/emea-callcenter-interaction-dataset.png)

Après avoir cliqué sur le jeu de données, vous obtenez un aperçu de l’activité du jeu de données, comme les lots ingérés et en échec.

![preview-interaction-dataset.png](./images/preview-interaction-dataset.png)

Cliquez sur **Prévisualiser le jeu de données** pour afficher un échantillon des données stockées dans le jeu de données `Demo System - Event Dataset for Call Center (Global v1.1)`. Le panneau de gauche affiche la structure du schéma pour ce jeu de données.

![explorer-interaction-dataset.png](./images/explore-interaction-dataset.png)

Cliquez sur le bouton **Fermer** pour fermer la fenêtre **Prévisualiser le jeu de données** .

## 5.1.1.3 Présentation de Query Service

Pour accéder à Adobe Experience Platform Query Service, cliquez sur **Requêtes** dans le menu de gauche.

![select-query.png](./images/select-queries.png)

En accédant à **Journal**, la page Liste des requêtes s’affiche. Elle contient la liste de toutes les requêtes qui ont été exécutées dans cette organisation, avec les dernières requêtes en date dans la partie supérieure.

![query-list.png](./images/query-list.png)

Cliquez sur une requête SQL de la liste et observez les détails fournis dans le rail de droite.

![click-sql-query.png](./images/click-sql-query.png)

Vous pouvez faire défiler la fenêtre pour afficher l’intégralité de la requête ou cliquer sur l’icône mise en surbrillance ci-dessous pour copier l’intégralité de la requête dans votre bloc-notes. Vous n’avez pas à copier la requête pour l’instant.

![click-copy-query.png](./images/click-copy-query.png)

Vous ne pouvez pas simplement voir les requêtes qui ont été exécutées. Cette interface utilisateur vous permet de créer de nouveaux jeux de données à partir de requêtes. Ces jeux de données peuvent être liés à Real-time Customer Profile Adobe Experience Platform ou utilisés comme entrée pour Adobe Experience Platform Data Science Workspace.

## 5.1.1.4 Connexion du client PSQL à Query Service

Query Service prend en charge les clients avec un pilote pour PostgreSQL. Dans ce cas, nous utiliserons PSQL, une interface de ligne de commande et Power BI ou Tableau. Connectons-nous à PSQL.

Cliquez sur **Credentials** (Informations d’identification).

![query-select-configuration.png](./images/queries-select-configuration.png)

L’écran ci-dessous s’affiche. L’écran Configuration fournit des informations et des informations d’identification du serveur pour l’authentification à Query Service. Pour l’instant, nous allons nous concentrer sur le côté droit de l’écran qui contient une commande de connexion pour PSQL. Cliquez sur le bouton Copier pour copier la commande dans le presse-papiers.

![copy-psql-connection.png](./images/copy-psql-connection.png)

Pour Windows : ouvrez la ligne de commande en appuyant sur la touche Windows et en saisissant cmd, puis en cliquant sur le résultat de l’invite de commande.

![open-command-prompt.png](./images/open-command-prompt.png)

Pour macOS : ouvrez le fichier terminal.app par le biais de la recherche de l’aperçu :

![open-terminal-osx.png](./images/open-terminal-osx.png)

Collez la commande de connexion que vous avez copiée à partir de l’interface utilisateur de Query Service et appuyez sur Entrée dans la fenêtre de l’invite de commande :

Windows :

![command-prompt-connect.png](./images/command-prompt-connected.png)

MACOS :

![command-prompt-paste-osx.png](./images/command-prompt-paste-osx.png)

Vous êtes désormais connecté à Query Service à l’aide de PSQL.

Dans les exercices suivants, il y aura une certaine interaction avec cette fenêtre. Nous l’appellerons votre **interface de ligne de commande PSQL**.

Vous êtes maintenant prêt à envoyer des requêtes.

Étape suivante : [5.1.2 Utilisation de Query Service](./ex2.md)

[Revenir au module 5.1](./query-service.md)

[Revenir à tous les modules](../../../overview.md)
