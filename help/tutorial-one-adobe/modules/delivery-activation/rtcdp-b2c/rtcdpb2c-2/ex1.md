---
title: Intelligent Services - Préparation des données de l’IA dédiée aux clients (Ingest)
description: IA dédiée aux clients - Préparation des données (ingestion)
kt: 5342
doc-type: tutorial
exl-id: 2b49d86a-af75-4ecd-ab3f-0182f3b8da2f
source-git-commit: 15adbf950115f0b6bb6613e69a60b310f25de058
workflow-type: tm+mt
source-wordcount: '694'
ht-degree: 5%

---

# 2.2.1 IA dédiée aux clients - Préparation des données (ingestion)

Pour qu’Intelligent Services puisse découvrir des informations à partir de vos données d’événements marketing, les données doivent être enrichies sémantiquement et conservées dans une structure standard. Pour ce faire, les services intelligents exploitent les schémas de modèle de données d’expérience (XDM) d’Adobe.
Plus précisément, tous les jeux de données utilisés dans les services intelligents doivent être conformes au schéma XDM **Événement d’expérience client**.

## Créer un schéma

Dans cet exercice, vous allez créer un schéma contenant le mixin **Événement d’expérience client**, requis par le service intelligent **IA dédiée aux clients**.

Connectez-vous à Adobe Experience Platform en accédant à cette URL : [https://experience.adobe.com/platform](https://experience.adobe.com/platform).

Une fois connecté, vous accédez à la page d’accueil de Adobe Experience Platform.

![Ingestion des données](../../datacollection/dc1.2/images/home.png)

Avant de continuer, vous devez sélectionner un **sandbox**. Le sandbox à sélectionner est nommé ``--aepSandboxName--``. Après avoir sélectionné la sandbox appropriée, la modification d’écran s’affiche et vous êtes maintenant dans votre sandbox dédiée.

![Ingestion des données](../../datacollection/dc1.2/images/sb1.png)

Dans le menu de gauche, cliquez sur **Schémas** et accédez à **Parcourir**. Cliquez sur **Créer un schéma**.

![Créer un schéma](./images/createschemabutton.png)

Dans la fenêtre contextuelle, sélectionnez **Manuel** et cliquez sur **Sélectionner**.

![Créer un schéma](./images/schmanual.png)

Ensuite, sélectionnez **Événement d’expérience** et cliquez sur **Suivant**.

![Créer un schéma](./images/xdmee.png)

Vous devez maintenant fournir un nom pour votre schéma. Comme nom de notre schéma, utilisez ceci : `--aepUserLdap-- - Demo System - Customer Experience Event` et cliquez sur **Terminer**.

![Créer un schéma](./images/schname.png)

Tu verras ça. Cliquez sur **+ Ajouter** sous Groupes de champs .

![Créer un schéma](./images/xdmee1.png)

Recherchez et sélectionnez les **groupes de champs** suivants à ajouter à ce schéma :

- Événement d’expérience du consommateur

![Nouveau schéma CEE](./images/cee1.png)

- IdentityMap

Cliquez sur **Ajouter des groupes de champs**.

![Nouveau schéma CEE](./images/cee2.png)

Tu verras ça. Sélectionnez ensuite le nom de votre schéma. Vous devez maintenant activer votre schéma pour **Profil** en cliquant sur le bouton (bascule) **Profil**.

![Créer un schéma](./images/xdmee3.png)

Tu verras ça. Cochez la case correspondant à **Les données de ce schéma contiendront une identité principale dans le champ identityMap .**. Cliquez sur **Activer**.

![Créer un schéma](./images/xdmee4.png)

Vous devriez maintenant avoir ceci. Cliquez sur **Enregistrer** pour enregistrer le schéma.

![Créer un schéma](./images/xdmee5.png)

## Créer un jeu de données

Dans le menu de gauche, cliquez sur **Jeux de données** et accédez à **Parcourir**. Cliquez sur **Créer un jeu de données**.

![Jeu de données](./images/createds.png)

Cliquez sur **Créer un jeu de données à partir d’un schéma**.

![Jeu de données](./images/createdatasetfromschema.png)

Dans l’écran suivant, sélectionnez le jeu de données que vous avez créé dans l’exercice précédent, qui est nommé `--aepUserLdap-- - Demo System - Customer Experience Event`. Cliquez sur **Suivant**.

![Jeu de données](./images/createds1.png)

Utilisez `--aepUserLdap-- - Demo System - Customer Experience Event Dataset` comme nom de jeu de données. Cliquez sur **Terminer**.

![Jeu de données](./images/createds2.png)

Votre jeu de données est maintenant créé. Activez le bouton (bascule) **Profil**.

![Jeu de données](./images/createds3.png)

Cliquez sur **Activer**.

![Jeu de données](./images/createds4.png)

Voici ce que vous devriez maintenant avoir :

![Jeu de données](./images/createds5.png)

Vous êtes maintenant prêt à ingérer des données d’événement d’expérience client et à commencer à utiliser le service d’IA dédiée aux clients.

## Télécharger des données de test d’événement d’expérience

Une fois les **Schéma** et **Jeu de données** configurés, vous êtes prêt à ingérer les données d’événement d’expérience. Comme l’IA dédiée aux clients a des exigences spécifiques en matière de données, vous devez ingérer des données préparées en externe.

Les données préparées pour les événements d’expérience de cet exercice doivent être conformes aux exigences et au schéma du [groupe de champs XDM Événement d’expérience client](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/context/experienceevent-consumer.schema.md).

Téléchargez le fichier zip avec les données de démonstration à partir de cet emplacement : [https://one-adobe-tech-insiders.s3.us-west-2.amazonaws.com/CUSTOM-CAI-EVENTS-WEB.zip](https://one-adobe-tech-insiders.s3.us-west-2.amazonaws.com/CUSTOM-CAI-EVENTS-WEB.zip).

Vous avez téléchargé un fichier nommé **CUSTOM-CAI-EVENTS-WEB.zip**. Placez le fichier sur le bureau de votre ordinateur et décompressez-le, après quoi vous verrez un dossier nommé **CUSTOM-CAI-EVENTS-WEB**.

![Jeu de données](./images/ingest.png)

Dans ce dossier, vous trouverez plusieurs fichiers json séquencés, qui doivent tous être ingérés dans l’exercice suivant.

![Jeu de données](./images/ingest1a.png)

## Ingérer des données de test d’événement d’expérience

Dans Adobe Experience Platform, accédez à **Jeux de données** et ouvrez votre jeu de données nommé **[!UICONTROL ldap - Système de démonstration - Jeu de données d’événement d’expérience client]**.

![Jeu de données](./images/ingest1.png)

Dans votre jeu de données, cliquez sur **Choisir les fichiers** pour ajouter des données.

![Jeu de données](./images/ingest2.png)

Dans la fenêtre contextuelle, sélectionnez les fichiers **WEBSITE-EE-1.json** jusqu’à **WEBSITE-EE-5.json** et cliquez sur **Ouvrir**.

![Jeu de données](./images/ingest3.png)

Répétez ce processus d’ingestion pour les fichiers **WEBSITE-EE-6.json** et **WEBSITE-EE-7.json**.

Les données importées apparaissent alors et un nouveau lot est créé à l’état **Chargement**. Ne quittez pas cette page que lorsque le fichier est chargé.

![Jeu de données](./images/ingest4.png)

Une fois le fichier chargé, le statut du lot passe de **Chargement** à **Traitement**.

![Jeu de données](./images/ingest5.png)

L’ingestion et le traitement des données peuvent prendre entre 10 et 20 minutes.

Une fois l’ingestion des données réussie, le statut du lot des différents chargements passe à **Succès**.

![Jeu de données](./images/ingest7.png)

## Étapes suivantes

Accédez à [2.2.2 Customer AI - Créer une instance (Configurer)](./ex2.md){target="_blank"}

Revenir à [Services intelligents](./intelligent-services.md){target="_blank"}

Revenir à [Tous les modules](./../../../../overview.md){target="_blank"}
