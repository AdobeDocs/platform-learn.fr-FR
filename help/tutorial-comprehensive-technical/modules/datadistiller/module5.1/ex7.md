---
title: Query Service - Explorer le jeu de données avec Tableau
description: Query Service - Explorer le jeu de données avec Tableau
kt: 5342
doc-type: tutorial
exl-id: 29525740-fe1f-4770-bcc9-f2ad499a2cb5
source-git-commit: b53ee64ae8438b8f48f842ed1f44ee7ef3e813fc
workflow-type: tm+mt
source-wordcount: '336'
ht-degree: 0%

---

# 5.1.7 Query Service et Tableau

Ouvrez Tableau.

![start-tableau.png](./images/start-tableau.png)

Dans **Se connecter à un serveur**, sélectionnez **PostgreSQL** :

![tableau-connect-postgress.png](./images/tableau-connect-postgress.png)

Accédez à Adobe Experience Platform, à **Requêtes** et à **Credentials**.

![query-service-credentials.png](./images/query-service-credentials.png)

Sur la page **Credentials** dans Adobe Experience Platform, copiez l’ **hôte** et collez-le dans le champ **Serveur**, copiez la **base de données** et collez-la dans le champ **Base de données** de Tableau, copiez le **port** et collez-le dans le champ **port** dans Tableau, faites de même **pour effectuer la même opération  14}Nom d’utilisateur** et **Mot de passe**. Cliquez ensuite sur **Se connecter**.

Connexion :

![tableau-connection-dialog.png](./images/tableau-connection-dialog.png)

Cliquez sur Rechercher (1) et entrez votre **ldap** dans le champ de recherche, identifiez votre tableau à partir du jeu de résultats et faites-le glisser (3) sur l’emplacement nommé **Faire glisser les tables ici**. Lorsque vous avez terminé, cliquez sur **Feuille 1** (3).

![tableau-drag-table.png](./images/tableau-drag-table.png)

Pour visualiser nos données sur la carte, nous devons convertir la longitude et la latitude en dimensions. Dans **Mesures**, sélectionnez **Latitude** (1), ouvrez la liste déroulante du champ et sélectionnez **Convertir en Dimension** (2). Faites de même pour la mesure **Longitude**.

![tableau-convert-dimension.png](./images/tableau-convert-dimension.png)

Faites glisser la mesure **Longitude** vers les **Colonnes** et la **Latitude** vers **Lignes**. La carte de **Belgique** apparaîtra automatiquement avec des petits points représentant les villes dans l&#39;ensemble de données.

![tableau-drag-lon-lat.png](./images/tableau-drag-lon-lat.png)

Sélectionnez **Mesurer les noms** (1), ouvrez la liste déroulante et sélectionnez **Ajouter à la feuille** (2) :

![tableau-select-measure-names.png](./images/tableau-select-measure-names.png)

Vous disposez désormais d’une carte, avec des points de différentes tailles. La taille indique le nombre d’interactions du centre d’appels pour cette ville spécifique. Pour varier la taille des points, accédez au panneau de droite et ouvrez **Mesure des valeurs** (à l’aide de l’icône déroulante). Dans la liste déroulante, sélectionnez **Modifier les tailles**. Jouez avec des tailles différentes.

![tableau-vary-size-dots.png](./images/tableau-vary-size-dots.png)

Pour afficher davantage les données par **rubrique d’appel**, faites glisser (1) la dimension **rubrique d’appel** sur **Pages**. Parcourez les différentes **rubriques d’appel** à l’aide de la **rubrique d’appel** (2) sur le côté droit de l’écran :

![tableau-call-topic-navigation.png](./images/tableau-call-topic-navigation.png)

Vous avez maintenant terminé cet exercice.

Étape suivante : [5.1.8 Query Service API](./ex8.md)

[Revenir au module 5.1](./query-service.md)

[Revenir à tous les modules](../../../overview.md)
