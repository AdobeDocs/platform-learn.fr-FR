---
title: Intelligent Services - Préparation des données Customer AI (Ingérer)
description: Customer AI - Préparation de données (ingestion)
kt: 5342
doc-type: tutorial
source-git-commit: 6962a0d37d375e751a05ae99b4f433b0283835d0
workflow-type: tm+mt
source-wordcount: '785'
ht-degree: 4%

---

# 2.2.1 Customer AI - Préparation des données (ingestion)

Pour que les services intelligents découvrent des informations à partir de vos données d’événements marketing, les données doivent être enrichies sémantiquement et conservées dans une structure standard. Pour ce faire, les services intelligents utilisent les schémas XDM (Experience Data Model) d’Adobe.
En particulier, tous les jeux de données utilisés dans Intelligent Services doivent être conformes au schéma XDM **Consumer Experience Event**.

## 2.2.1.1 Création d’un schéma

Au cours de cet exercice, vous allez créer un schéma qui contient le **mixin Événement d’expérience client**, qui est requis par le service intelligent **Customer AI**.

Connectez-vous à Adobe Experience Platform en accédant à cette URL : [https://experience.adobe.com/platform](https://experience.adobe.com/platform).

Une fois connecté, vous accédez à la page d’accueil de Adobe Experience Platform.

![Ingestion des données](../../datacollection/module1.2/images/home.png)

Avant de continuer, vous devez sélectionner un **sandbox**. L’environnement de test à sélectionner est nommé ``--module10sandbox--``. Pour ce faire, cliquez sur le texte **[!UICONTROL Production Prod]** dans la ligne bleue en haut de votre écran. Après avoir sélectionné l’environnement de test approprié, l’écran change et vous êtes désormais dans votre environnement de test dédié.

![Ingestion des données](../../datacollection/module1.2/images/sb1.png)

Dans le menu de gauche, cliquez sur **Schémas** et accédez à **Parcourir**. Cliquez sur **Créer un schéma**.

![Créer un schéma](./images/create-schema-button.png)

Dans la fenêtre contextuelle, sélectionnez **XDM ExperienceEvent**.

![Créer un schéma](./images/xdmee.png)

Vous verrez alors ceci.

![Créer un schéma](./images/xdmee1.png)

Recherchez et sélectionnez les **Mixins** suivants à ajouter à ce schéma :

- Événement d’expérience du consommateur

  ![Nouveau schéma CEE](./images/cee.png)

- Informations sur l’identifiant de l’utilisateur final

  ![Nouveau schéma CEE](./images/identitymap.png)

Cliquez sur **Ajouter des groupes de champs**.

![Définition de la clé d’identité](./images/addmixin.png)

Vous verrez alors ceci. Sélectionnez le mixin **End User ID Details**.

![Créer un schéma](./images/eui1.png)

Accédez au champ **endUserIDs._experience.email.id**.

![Créer un schéma](./images/eui2.png)

Dans le menu de droite pour le champ **endUserIDs._experience.emailid.id**, faites défiler l’écran vers le bas et cochez la case correspondant à **Identité**, cochez la case correspondant à **Identité de Principal** et sélectionnez l’ **espace de noms d’identité** de **Adresse électronique**.

![Créer un schéma](./images/eui3.png)

Accédez au champ **endUserIDs._experience.mcid.id**. Cochez la case correspondant à **Identity** et sélectionnez l’ **espace de noms d’identité** de **ECID**. Cliquez sur **Appliquer**.

![Créer un schéma](./images/eui4.png)

Donnez un nom à votre schéma maintenant.

Pour le nom de notre schéma, vous utiliserez ceci :

- `--aepUserLdap-- - Demo System - Customer Experience Event`

Par exemple, pour ldap **vangeluw**, il doit s’agir du nom du schéma :

- **vangeluw - Système de démonstration - Événement d’expérience client**

Ça devrait vous donner quelque chose comme ça. Cliquez sur le bouton **+ Ajouter** pour ajouter de nouveaux **Mixins**.

![Créer un schéma](./images/xdmee2.png)

Sélectionnez le nom de votre schéma. Vous devez maintenant activer votre schéma pour **Profile** en cliquant sur le bouton d’activation/désactivation **Profile** .

![Créer un schéma](./images/xdmee3.png)

Vous verrez alors ceci. Cliquez sur **Activer**.

![Créer un schéma](./images/xdmee4.png)

Vous devriez maintenant avoir ceci. Cliquez sur **Enregistrer** pour enregistrer votre schéma.

![Créer un schéma](./images/xdmee5.png)

## 2.2.1.2 Création d’un jeu de données

Dans le menu de gauche, cliquez sur **Jeux de données** et accédez à **Parcourir**. Cliquez sur **Créer un jeu de données**.

![Jeu de données](./images/createds.png)

Cliquez sur **Créer un jeu de données à partir du schéma**.

![Jeu de données](./images/createdatasetfromschema.png)

Dans l’écran suivant, sélectionnez le jeu de données que vous avez créé lors de l’exercice précédent, nommé **[!UICONTROL ldap - Demo System - Customer Experience Event]**. Cliquez sur **Suivant**.

![Jeu de données](./images/createds1.png)

Pour nommer votre jeu de données, utilisez `--aepUserLdap-- - Demo System - Customer Experience Event Dataset`. Cliquez sur **Terminer**.

![Jeu de données](./images/createds2.png)

Votre jeu de données est maintenant créé. Activez le bouton bascule **Profile** .

![Jeu de données](./images/createds3.png)

Cliquez sur **Activer**.

![Jeu de données](./images/createds4.png)

Vous devez maintenant disposer des éléments suivants :

![Jeu de données](./images/createds5.png)

Vous êtes maintenant prêt à commencer à ingérer des données d’événement d’expérience client et à utiliser le service Customer AI.

## 2.2.1.3 Téléchargement des données de test de l’événement d’expérience

Une fois que le **schéma** et le **jeu de données** sont configurés, vous êtes prêt à ingérer les données d’événement d’expérience. Comme Customer AI nécessite des données sur **2 trimestres au moins**, vous devrez ingérer des données préparées en externe.

Les données préparées pour les événements d’expérience doivent être conformes aux exigences et au schéma du [mixin XDM de l’événement d’expérience client](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/context/experienceevent-consumer.schema.md).

Téléchargez le fichier contenant des exemples de données à partir de cet emplacement : [https://dashboard.adobedemo.com/data](https://dashboard.adobedemo.com/data). Cliquez sur le bouton **Télécharger** .

![Jeu de données](./images/dsn1.png)

Si vous ne pouvez pas accéder au lien ci-dessus, vous pouvez également télécharger le fichier à partir de cet emplacement : [https://aepmodule10.s3-us-west-2.amazonaws.com/retail-v1-dec2020-xl.json.zip](https://aepmodule10.s3-us-west-2.amazonaws.com/retail-v1-dec2020-xl.json.zip).

Vous avez maintenant téléchargé un fichier nommé **retail-v1-dec2020-xl.json.zip**. Placez le fichier sur le bureau de votre ordinateur et décompressez-le, après quoi vous verrez un fichier nommé **retail-v1.json**. Vous aurez besoin de ce fichier lors de l’exercice suivant.

![Jeu de données](./images/ingest.png)

## 2.2.1.4 Ingestion des données de test d’événement d’expérience

Dans Adobe Experience Platform, accédez à **Jeux de données** et ouvrez votre jeu de données, appelé **[!UICONTROL ldap - Demo System - Customer Experience Event Dataset]**.

![Jeu de données](./images/ingest1.png)

Dans votre jeu de données, cliquez sur **Choisir les fichiers** pour ajouter des données.

![Jeu de données](./images/ingest2.png)

Dans la fenêtre contextuelle, sélectionnez le fichier **retail-v1.json** et cliquez sur **Ouvrir**.

![Jeu de données](./images/ingest3.png)

Vous verrez ensuite les données importées et un nouveau lot est créé à l’état **Chargement**. Ne quittez pas cette page tant que le fichier n’a pas été chargé.

![Jeu de données](./images/ingest4.png)

Une fois le fichier téléchargé, l’état du lot passe de **Chargement** à **Traitement**.

![Jeu de données](./images/ingest5.png)

L’ingestion et le traitement des données peuvent prendre entre 10 et 20 minutes.

Une fois l’ingestion des données réussie, l’état du lot passe à **Success**.

![Jeu de données](./images/ingest7.png)

![Jeu de données](./images/ingest8.png)

Étape suivante : [2.2.2 Customer AI - Créer une instance (configurer)](./ex2.md)

[Revenir au module 2.2](./intelligent-services.md)

[Revenir à tous les modules](./../../../overview.md)
