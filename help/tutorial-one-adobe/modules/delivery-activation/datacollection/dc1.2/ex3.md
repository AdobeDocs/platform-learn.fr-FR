---
title: Foundation - Ingestion de données - Configuration des jeux de données
description: Foundation - Ingestion de données - Configuration des jeux de données
kt: 5342
doc-type: tutorial
exl-id: 322aaaaa-50f7-4da4-bc4b-1b7edfe17e54
source-git-commit: 3d61d91111d8693ab031fbd7b26706c02818108c
workflow-type: tm+mt
source-wordcount: '554'
ht-degree: 8%

---

# 1.2.3 Configuration De Jeux De Données

Dans cet exercice, vous allez configurer des jeux de données pour capturer et stocker des informations de profil et le comportement des clients. Chaque jeu de données créé dans ce utilise l’un des schémas que vous avez créés à l’étape précédente.

## Contexte

Après avoir défini la réponse aux questions **Qui est ce client ?** et **Que fait ce client ?** devrait ressembler à ceci : vous devez maintenant créer un compartiment qui utilise ces informations pour recevoir et valider les données envoyées à Adobe Experience Platform.

## Créer des jeux de données

Vous devez maintenant créer 2 jeux de données :

- 1 jeu de données pour capturer les informations qui répondent au **Qui est ce client ?** - question.
- 1 jeu de données pour capturer les informations qui répondent au **Que fait ce client ?** - question.

Connectez-vous à Adobe Experience Platform en accédant à cette URL : [https://experience.adobe.com/platform](https://experience.adobe.com/platform).

Une fois connecté, vous accédez à la page d’accueil de Adobe Experience Platform.

![Ingestion des données](./images/home.png)

Avant de continuer, vous devez sélectionner un **[!UICONTROL sandbox]**. Le sandbox à sélectionner est nommé ``--aepSandboxName--``. Après avoir sélectionné la [!UICONTROL sandbox] appropriée, la modification d’écran s’affiche et vous êtes maintenant dans votre [!UICONTROL sandbox] dédié.

![Ingestion des données](./images/sb1.png)

Dans Adobe Experience Platform, cliquez sur **[!UICONTROL Jeux de données]** dans le menu situé dans la partie gauche de l’écran.  Vous verrez alors ceci :

![Ingestion des données](./images/menudatasets.png)

Commençons par créer le jeu de données pour capturer les informations d’enregistrement du site web.

Vous devez créer un jeu de données. Pour créer un jeu de données, cliquez sur le bouton **[!UICONTROL + Créer un jeu de données]**.

![Ingestion des données](./images/createdataset.png)

Vous devez définir un jeu de données à partir du schéma que vous avez défini à l’étape précédente. Cliquez sur l’option **[!UICONTROL Créer un jeu de données à partir d’un schéma]** - .

![Ingestion des données](./images/datasetfromschema.png)

Dans l’écran suivant, vous devez sélectionner le schéma que vous avez créé en 1, `--aepUserLdap-- - Demo System - Profile Schema for Website`.

Cliquez sur **Suivant**.

![Ingestion des données](./images/schemaselection.png)

Donnons un nom à votre jeu de données.

Comme nom de jeu de données, utilisez le suivant :

`--aepUserLdap-- - Demo System - Profile Dataset for Website`

Cliquez sur **Terminer**.

![Ingestion des données](./images/datasetname.png)

Vous verrez maintenant ceci :

![Ingestion des données](./images/dsoverview1.png)

Revenez à la présentation de [!UICONTROL Jeux de données]. Le jeu de données que vous avez créé apparaît maintenant dans la fenêtre contextuelle de la présentation.

![Ingestion des données](./images/dsoverview2.png)

Ensuite, vous allez configurer un deuxième jeu de données pour capturer les interactions du site web.

Cliquez sur **[!UICONTROL + Créer un jeu de données]**.

![Ingestion des données](./images/createdataset.png)


Vous devez définir un jeu de données à partir du schéma que vous avez défini à l’étape précédente. Cliquez sur l’option **[!UICONTROL Créer un jeu de données à partir d’un schéma]** - .

![Ingestion des données](./images/datasetfromschema.png)

Dans l’écran suivant, vous devez sélectionner le schéma que vous avez créé précédemment, `--aepUserLdap-- - Demo System - Event Schema for Website`.

Cliquez sur **Suivant**.

![Ingestion des données](./images/schemaselectionee.png)

Donnons un nom à votre jeu de données.

Comme nom de jeu de données, utilisez le suivant :

`--aepUserLdap-- - Demo System - Event Dataset for Website`

Cliquez sur **Terminer**.

![Ingestion des données](./images/datasetnameee.png)

Vous verrez alors ceci :

![Ingestion des données](./images/finish1ee.png)

Revenez à l’écran d’aperçu [!UICONTROL Jeux de données].

![Ingestion des données](./images/datasetsoverview.png)

Vous devez maintenant activer vos jeux de données pour qu’ils fassent partie du profil client en temps réel de Adobe Experience Platform.

Ouvrez votre `--aepUserLdap-- - Demo System - Profile Dataset for Website` de jeu de données en cliquant dessus.

Recherchez l’icône de basculement [!UICONTROL Profil] sur le côté droit de l’écran.
Cliquez sur le bouton (bascule) [!UICONTROL Profil] pour activer ce jeu de données pour [!UICONTROL Profil].

![Ingestion des données](./images/ds1.png)

Cliquez sur **[!UICONTROL Activer]**.

![Ingestion des données](./images/ds3.png)

Votre jeu de données est maintenant activé pour [!UICONTROL Profil].

Revenez à la présentation des jeux de données et ouvrez votre jeu de données `--aepUserLdap-- - Demo System - Event Dataset` pour le site Web en cliquant dessus.

Recherchez l’icône de basculement [!UICONTROL Profil] sur le côté droit de l’écran. Cliquez sur le bouton (bascule) [!UICONTROL Profil] pour activer [!UICONTROL Profil].

![Ingestion des données](./images/ds4.png)

Cliquez sur **[!UICONTROL Activer]**.

![Ingestion des données](./images/ds5.png)

Votre jeu de données est maintenant activé pour [!UICONTROL Profil].

## Étapes suivantes

Accédez à [1.2.4 Ingestion de données à partir de sources hors ligne](./ex4.md){target="_blank"}

Revenir à [Ingestion des données](./data-ingestion.md){target="_blank"}

Revenir à [Tous les modules](./../../../../overview.md){target="_blank"}
