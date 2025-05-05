---
title: Query Service - Explorer le jeu de données avec Tableau
description: Query Service - Explorer le jeu de données avec Tableau
kt: 5342
doc-type: tutorial
exl-id: 29525740-fe1f-4770-bcc9-f2ad499a2cb5
source-git-commit: d9d9a38c1e160950ae755e352a54667c8a7b30f7
workflow-type: tm+mt
source-wordcount: '402'
ht-degree: 0%

---

# 5.1.7 Query Service et Tableau

Ouvrez Tableau.

![start-tableau.png](./images/starttableau.png)

Dans **Se connecter à un serveur**, cliquez sur **Plus**, puis sur **PostgreSQL**.

![tableau-connect-postgress.png](./images/tableauconnectpostgress.png)

Si vous n’avez pas encore utilisé PostgeSQL avec Tableau, vous pouvez le voir. Cliquez sur **Télécharger le pilote**.

![tableau-connect-postgress.png](./images/tableauconnectpostgress1.png)

Suivez les instructions pour télécharger et installer le pilote PostgreSQL.

![tableau-connect-postgress.png](./images/tableauconnectpostgress2.png)

Une fois que vous avez fini d’installer le pilote, quittez et redémarrez Tableau Desktop. Ensuite, après le redémarrage, accédez à nouveau à **Se connecter à un serveur**, cliquez sur **Plus**, puis cliquez de nouveau sur **PostgreSQL**.

![tableau-connect-postgress.png](./images/tableauconnectpostgress.png)

Vous verrez alors ceci.

![tableau-connect-postgress.png](./images/tableauconnectpostgress3.png)

Accédez à Adobe Experience Platform, à **Requêtes** et à **Credentials**.

![query-service-credentials.png](./images/queryservicecredentials.png)

Sur la page **Credentials** dans Adobe Experience Platform, copiez l’ **hôte** et collez-le dans le champ **Serveur**, copiez la **base de données** et collez-la dans le champ **Base de données** de Tableau, copiez le **port** et collez-le dans le champ **port** dans Tableau, faites de même **pour effectuer la même opération  14&rbrace;Nom d’utilisateur** et **Mot de passe**. Cliquez ensuite sur **Se connecter**.

![tableau-connection-dialog.png](./images/tableauconnectiondialog.png)

Dans la liste des tables disponibles, recherchez la table que vous avez créée lors de l’exercice précédent, appelée `--aepUserLdap--_callcenter_interaction_analysis`. Faites-le glisser sur la zone de travail.

![tableau-drag-table.png](./images/tableaudragtable.png)

Vous verrez alors ceci. Cliquez sur **Mettre à jour maintenant**.

![tableau-drag-table.png](./images/tableaudragtable1.png)

Vous verrez alors les données d’AEP devenir disponibles dans Tableau. Cliquez sur **Feuille 1** pour commencer à utiliser les données.

![tableau-drag-table.png](./images/tableaudragtable2.png)

Pour visualiser vos données sur la carte, vous devez convertir la longitude et la latitude en dimensions. Dans **Mesures**, cliquez avec le bouton droit de la souris sur **Latitude**, sélectionnez **Convertir en Dimension** dans le menu. Faites de même pour la mesure **Longitude**.

![tableau-convert-dimension.png](./images/tableauconvertdimension.png)

Faites glisser la mesure **Longitude** vers les **Colonnes** et la **Latitude** vers **Lignes**. La carte de **Belgique** apparaîtra automatiquement avec des petits points représentant les villes dans l&#39;ensemble de données.

![tableau-drag-lon-lat.png](./images/tableaudraglonlat.png)

Sélectionnez **Mesurer les noms**, cliquez sur **Ajouter à la feuille**.

![tableau-select-measure-names.png](./images/selectmeasurenames.png)

Vous disposez désormais d’une carte, avec des points de différentes tailles. La taille indique le nombre d’interactions du centre d’appels pour cette ville spécifique. Pour varier la taille des points, accédez au panneau de droite et ouvrez **Mesure des valeurs** (à l’aide de l’icône déroulante). Dans la liste déroulante, sélectionnez **Modifier les tailles**. Jouez avec des tailles différentes.

![tableau-vary-size-dots.png](./images/tableauvarysizedots.png)

Pour afficher davantage les données par **rubrique d’appel**, faites glisser la dimension **rubrique d’appel** sur **Pages**. Parcourez les différentes **rubriques d’appel** à l’aide de la **rubrique d’appel** sur le côté droit de l’écran :

![tableau-call-topic-navigation.png](./images/tableaucalltopicnavigation.png)

Vous avez maintenant terminé cet exercice.

Étape suivante : [5.1.8 Query Service API](./ex8.md)

[Revenir au module 5.1](./query-service.md)

[Revenir à tous les modules](../../../overview.md)
