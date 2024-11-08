---
title: Foundation - Ingestion de données - Configuration des jeux de données
description: Foundation - Ingestion de données - Configuration des jeux de données
kt: 5342
doc-type: tutorial
source-git-commit: 6962a0d37d375e751a05ae99b4f433b0283835d0
workflow-type: tm+mt
source-wordcount: '713'
ht-degree: 7%

---

# 1.2.3 Configuration de jeux de données

Au cours de cet exercice, vous allez configurer les jeux de données requis pour capturer et stocker les informations de profil et le comportement des clients. Chaque jeu de données que vous créez dans utilise l’un des schémas que vous avez créés à l’étape précédente.

## Histoire

Après avoir défini la réponse aux questions **Qui est ce client ?** et **Que fait ce client ?** doit ressembler à , vous devez maintenant créer un compartiment qui utilise ces informations, pour recevoir et valider les données envoyées à Adobe Experience Platform.

## 1.2.3.1 - Création de jeux de données

Vous devez maintenant créer 2 jeux de données :

- 1 jeu de données pour capturer les informations qui répondent au **Qui est ce client ?** - question.
- 1 jeu de données pour capturer les informations qui répondent au **Que fait ce client ?** - question.

Connectez-vous à Adobe Experience Platform en accédant à cette URL : [https://experience.adobe.com/platform](https://experience.adobe.com/platform).

Une fois connecté, vous accédez à la page d’accueil de Adobe Experience Platform.

![Ingestion des données](./images/home.png)

Avant de continuer, vous devez sélectionner un **[!UICONTROL sandbox]**. L’environnement de test à sélectionner est nommé ``--module2sandbox--``. Pour ce faire, cliquez sur le texte **[!UICONTROL Production Prod]** dans la ligne bleue en haut de votre écran. Après avoir sélectionné l’[!UICONTROL sandbox] approprié, vous verrez le changement d’écran et vous êtes désormais dans votre [!UICONTROL sandbox] dédié.

![Ingestion des données](./images/sb1.png)

Dans Adobe Experience Platform, cliquez sur **[!UICONTROL Jeux de données]** dans le menu sur le côté gauche de votre écran.  Vous verrez alors :

![Ingestion des données](./images/menudatasets.png)

Commençons par créer le jeu de données pour capturer les informations d’enregistrement du site web.

Vous devez créer un nouveau jeu de données. Pour créer un nouveau jeu de données, cliquez sur le bouton **[!UICONTROL + Créer un jeu de données]**.

![Ingestion des données](./images/createdataset.png)

Après avoir cliqué sur le bouton **[!UICONTROL + Créer un jeu de données]** , l’écran suivant s’affiche.

![Ingestion des données](./images/datasetsetup.png)

Vous devez définir un jeu de données à partir du schéma que vous avez défini à l’étape précédente. Cliquez sur l’option **[!UICONTROL Créer un jeu de données à partir du schéma]** - .

![Ingestion des données](./images/datasetfromschema.png)

Dans l’écran suivant, vous devez sélectionner le schéma que vous avez créé dans 1, `--aepUserLdap-- - Demo System - Profile Schema for Website`.

![Ingestion des données](./images/schemaselection.png)

Après avoir sélectionné le schéma, cliquez sur **[!UICONTROL Suivant]** pour continuer.

![Ingestion des données](./images/next.png)

Attribuons un nom à votre jeu de données.

Pour nommer notre jeu de données, utilisez ceci :

`--aepUserLdap-- - Demo System - Profile Dataset for Website`

Par exemple, pour ldap **[!UICONTROL vangeluw]**, il doit s’agir du nom du schéma :

**[!UICONTROL vangeluw - Système de démonstration - Jeu de données de profil pour le site web]**

Cela devrait vous donner quelque chose comme ceci :

![Ingestion des données](./images/datasetname.png)

Cliquez sur **[!UICONTROL Terminer]** pour terminer la configuration de votre jeu de données.

![Ingestion des données](./images/finish.png)

Vous verrez maintenant ceci :

![Ingestion des données](./images/dsoverview1.png)

Revenez à la présentation des [!UICONTROL jeux de données] . Le jeu de données que vous avez créé s’affiche désormais dans l’aperçu.

![Ingestion des données](./images/dsoverview2.png)

Vous allez ensuite configurer un deuxième jeu de données pour capturer les interactions avec le site web.

Vous devez créer un nouveau jeu de données. Pour créer un nouveau jeu de données, cliquez sur le bouton **[!UICONTROL + Créer un jeu de données]**.

![Ingestion des données](./images/createdataset.png)

Après avoir cliqué sur le bouton **[!UICONTROL + Créer un jeu de données]** , l’écran suivant s’affiche.

![Ingestion des données](./images/datasetsetup.png)

Vous devez définir un jeu de données à partir du schéma que vous avez défini à l’étape précédente. Cliquez sur l’option **[!UICONTROL Créer un jeu de données à partir du schéma]** - .

![Ingestion des données](./images/datasetfromschema.png)

Dans l’écran suivant, vous devez sélectionner le schéma que vous avez créé dans 2.2, `--aepUserLdap-- - Demo System - Event Schema for Website`.

![Ingestion des données](./images/schemaselectionee.png)

Après avoir sélectionné le schéma, cliquez sur **[!UICONTROL Suivant]** pour continuer.

![Ingestion des données](./images/next.png)

Attribuons un nom à votre jeu de données.

Comme nom de notre jeu de données, nous utiliserons ceci :

`--aepUserLdap-- - Demo System - Event Dataset for Website`

Par exemple, pour ldap **[!UICONTROL vangeluw]**, il doit s’agir du nom du schéma :

**[!UICONTROL vangeluw - Système de démonstration - Jeu de données d’événement pour le site web]**

Cela devrait vous donner quelque chose comme ceci :

![Ingestion des données](./images/datasetnameee.png)

Cliquez sur **[!UICONTROL Terminer]** pour terminer la configuration de votre jeu de données.

![Ingestion des données](./images/finish.png)

Vous verrez alors :

![Ingestion des données](./images/finish1.png)

Revenez à l’écran d’aperçu [!UICONTROL Jeux de données] .

![Ingestion des données](./images/datasetsoverview.png)

Vous devez maintenant activer vos jeux de données pour faire partie de Adobe Experience Platform Real-time Customer Profile.

Ouvrez votre jeu de données `--aepUserLdap--` - Système de démonstration - Jeu de données de profil pour le site web en cliquant dessus.

Recherchez l’icône de basculement [!UICONTROL Profile] sur le côté droit de l’écran.

![Ingestion des données](./images/ds1.png)

Cliquez sur le bouton d’activation/désactivation [!UICONTROL Profile] pour activer ce jeu de données pour [!UICONTROL Profile].

![Ingestion des données](./images/ds2.png)

Cliquez sur le **[!UICONTROL Activer]**.

![Ingestion des données](./images/ds3.png)

Votre jeu de données est maintenant activé pour [!UICONTROL Profile].

Revenez à la présentation des jeux de données et ouvrez votre jeu de données `--aepUserLdap-- - Demo System - Event Dataset` pour le site web en cliquant dessus.

Recherchez l’icône de basculement [!UICONTROL Profile] sur le côté droit de l’écran.

![Ingestion des données](./images/ds4.png)

Cliquez sur la bascule [!UICONTROL Profile] pour activer [!UICONTROL Profile].

![Ingestion des données](./images/ds2.png)

Cliquez sur **[!UICONTROL Activer]**.

![Ingestion des données](./images/ds5.png)

Votre jeu de données est maintenant activé pour [!UICONTROL Profile].

Étape suivante : [1.2.4 Data Ingestion à partir de sources hors ligne](./ex4.md)

[Revenir au module 1.2](./data-ingestion.md)

[Revenir à tous les modules](../../../overview.md)
