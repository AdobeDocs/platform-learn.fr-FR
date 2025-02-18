---
title: Query Service - Explorer le jeu de données avec Tableau
description: Query Service - Explorer le jeu de données avec Tableau
kt: 5342
doc-type: tutorial
exl-id: 33ab854d-fad7-497c-affa-f58e4299c0b3
source-git-commit: 1e3a8d585503eddad4c642a3b13d2b5f7ddc9943
workflow-type: tm+mt
source-wordcount: '404'
ht-degree: 0%

---

# 2.1.7 Query Service et Tableau

Ouvrez Tableau.

![start-tableau.png](./images/starttableau.png)

Dans **Se connecter à un serveur**, cliquez sur **Plus** puis sur **PostgreSQL**.

![tableau-connect-postprogress.png](./images/tableauconnectpostgress.png)

Si vous n&#39;avez pas encore utilisé PostgreSQL avec Tableau, ceci peut s&#39;afficher. Cliquez sur **Télécharger le pilote**.

![tableau-connect-postprogress.png](./images/tableauconnectpostgress1.png)

Suivez les instructions pour télécharger et installer le pilote PostgreSQL.

![tableau-connect-postprogress.png](./images/tableauconnectpostgress2.png)

Une fois l&#39;installation du pilote terminée, quittez et redémarrez Tableau Desktop. Ensuite, après le redémarrage, accédez à **Se connecter à un serveur** puis cliquez de nouveau sur **Plus** et sur **PostgreSQL**.

![tableau-connect-postprogress.png](./images/tableauconnectpostgress.png)

Tu verras ça.

![tableau-connect-postprogress.png](./images/tableauconnectpostgress3.png)

Accédez à Adobe Experience Platform, à **Requêtes** et à **Informations d’identification**.

![query-service-credentials.png](./images/queryservicecredentials.png)

À partir de la page **Informations d&#39;identification** de Adobe Experience Platform, copiez le **Hôte** et collez-le dans le champ **Serveur**, copiez le **Base de données** et collez-le dans le champ **Base de données** de Tableau, copiez le **Port** et collez-le dans le champ **Port** dans Tableau, faites de même pour **NomUtilisateur** et **MotDePasse**. Cliquez ensuite sur **Se connecter**.

![tableau-connection-dialog.png](./images/tableauconnectiondialog.png)

Dans la liste des tableaux disponibles, localisez le tableau que vous avez créé dans l’exercice précédent, qui s’appelle `--aepUserLdap--_callcenter_interaction_analysis`. Faites-le glisser sur la zone de travail.

![tableau-drag-table.png](./images/tableaudragtable.png)

Tu verras ça. Cliquez sur **Mettre à jour maintenant**.

![tableau-drag-table.png](./images/tableaudragtable1.png)

Les données d’AEP seront alors disponibles dans Tableau. Cliquez sur **Feuille 1** pour commencer à utiliser les données.

![tableau-drag-table.png](./images/tableaudragtable2.png)

Pour visualiser vos données sur la carte, vous devez convertir la longitude et la latitude en dimensions. Dans **Mesures**, cliquez avec le bouton droit de la souris **Latitude**, puis sélectionnez **Convertir en Dimension** dans le menu. Faites de même pour la mesure **Longitude**.

![tableau-convert-dimension.png](./images/tableauconvertdimension.png)

Faites glisser la mesure **Longitude** vers **Colonnes** et la mesure **Latitude** vers **Lignes**. Automatiquement la carte de **Belgique** apparaîtra avec de petits points représentant les villes dans notre jeu de données.

![tableau-drag-lon-lat.png](./images/tableaudraglonlat.png)

Sélectionnez **Noms des mesures**, puis cliquez sur **Ajouter à la feuille**.

![tableau-select-measurement-names.png](./images/selectmeasurenames.png)

Vous avez maintenant une carte, avec des points de différentes tailles. La taille indique le nombre d’interactions du centre d’appel pour cette ville spécifique. Pour faire varier la taille des points, accédez au panneau de droite et ouvrez **Valeurs de mesure** (à l’aide de l’icône déroulante). Dans la liste déroulante, sélectionnez **Modifier les tailles**. Jouez avec différentes tailles.

![tableau-vary-size-dots.png](./images/tableauvarysizedots.png)

Pour afficher davantage les données par **rubrique d’appel**, faites glisser la dimension **rubrique d’appel** sur **Pages**. Parcourez les différentes **rubriques d’appel** à l’aide de la **rubrique d’appel** sur le côté droit de l’écran :

![tableau-call-topic-navigation.png](./images/tableaucalltopicnavigation.png)

Vous avez maintenant terminé cet exercice.

## Étapes suivantes

Accédez à l’API [2.1.8 Query Service](./ex8.md){target="_blank"}

Revenez à [Query Service](./query-service.md){target="_blank"}

Revenir à [Tous les modules](./../../../../overview.md){target="_blank"}
