---
title: Offer decisioning - Test de votre décision à l’aide de l’API
description: Test de votre décision à l’aide de l’API
kt: 5342
doc-type: tutorial
source-git-commit: 7d2f5f842559b2d6d9f115f3993268a4b36a0fe0
workflow-type: tm+mt
source-wordcount: '651'
ht-degree: 1%

---

# 3.3.6 Test de votre décision à l’aide de l’API

## 3.3.6.1 Utilisation de l’API Offer Decisioning à l’aide de Postman

Téléchargez [ cette collection Postman pour Offer Decisioning](./../../../assets/postman/postman_offer-decisioning.zip) sur votre bureau et décompressez-la. Vous obtiendrez alors ce qui suit :

![API OD](./images/unzip.png)

Vous disposez maintenant de ce fichier sur votre bureau :

- [!UICONTROL _Module 14- Service de prise de décision.postman_collection.json]

Dans [Exercice 2.1.3 - Authentification Postman vers Adobe I/O](./../../../modules/rtcdp-b2c/module2.1/ex3.md), vous avez installé Postman. Vous devrez réutiliser Postman pour cet exercice.

Ouvrez Postman. Cliquez sur **[!UICONTROL Importer]**.

![Adobe I/O d’une nouvelle intégration](./images/postmanui.png)

Cliquez sur **[!UICONTROL Télécharger des fichiers]**.

![Adobe I/O d’une nouvelle intégration](./images/pm1.png)

Sélectionnez le fichier **[!UICONTROL _Module 14- Decisioning Service.postman_collection.json]** et cliquez sur **[!UICONTROL Ouvrir]**.

![Adobe I/O d’une nouvelle intégration](./images/pm2.png)

Cette collection sera alors disponible dans Postman.

![Adobe I/O d’une nouvelle intégration](./images/pm3.png)

Vous avez désormais tout ce dont vous avez besoin dans Postman pour commencer à interagir avec Adobe Experience Platform par le biais des API.

### 3.3.6.1.1 Conteneurs de liste

Cliquez pour ouvrir la requête **[!UICONTROL GET - Conteneurs de liste]**.

Sous **[!UICONTROL Params]**, vous verrez ceci :

- property: `_instance.parentName==aepenablementfy22`

Dans ce paramètre, **[!UICONTROL aepenablementfy22]** est le nom de l’environnement de test utilisé dans Adobe Experience Platform. L’environnement de test que vous devez utiliser est `--aepSandboxId--`. Remplacez le texte **[!UICONTROL aepenablementfy22]** par `--aepSandboxId--`.

Après avoir remplacé le nom de l’environnement de test, cliquez sur **[!UICONTROL Envoyer]**.

![API OD](./images/api2.png)

Il s’agit de la réponse, qui affiche le conteneur d’offres pour l’environnement de test que vous avez spécifié. Copiez le **[!UICONTROL container instanceId]** comme indiqué ci-dessous et écrivez-le dans un fichier texte sur votre ordinateur. Vous devrez utiliser cet **[!UICONTROL instanceId]** de conteneur pour l’exercice suivant !

![API OD](./images/api3.png)

### 3.3.6.1.2 Placements de liste

Cliquez pour ouvrir la requête **[!UICONTROL GET - Répertorier les emplacements]**. Cliquez sur **[!UICONTROL Envoyer]**.

![API OD](./images/api4.png)

Vous voyez maintenant tous les emplacements disponibles dans votre conteneur d’offres. Les emplacements que vous voyez ont été définis dans l’interface utilisateur de Adobe Experience Platform, comme vous pouvez le voir dans l’ [exercice 3.3.1.3](./ex1.md).

![API OD](./images/api5.png)

### 3.3.6.1.3 Règles de décision de liste

Cliquez pour ouvrir la requête **[!UICONTROL GET - Lister des règles de décision]**. Cliquez sur **[!UICONTROL Envoyer]**.

![API OD](./images/api6.png)

Dans la réponse, vous verrez les règles de décision que vous avez définies dans l’interface utilisateur de Adobe Experience Platform, comme vous pouvez le voir dans l’ [exercice 3.3.1.4](./ex1.md).

![API OD](./images/api7.png)

### 3.3.6.1.4 Liste des offres personnalisées

Cliquez pour ouvrir la requête **[!UICONTROL GET - Liste des offres personnalisées]**. Cliquez sur **[!UICONTROL Envoyer]**.

![API OD](./images/api8.png)

Dans la réponse, vous verrez les offres personnalisées que vous avez définies dans l’interface utilisateur de Adobe Experience Platform dans l’ [exercice 3.3.2.1](./ex2.md).

![API OD](./images/api9.png)

### 3.3.6.1.5 Liste des offres de secours

Cliquez pour ouvrir la requête **[!UICONTROL GET - Liste des offres de secours]**. Cliquez sur **[!UICONTROL Envoyer]**.

![API OD](./images/api10.png)

Dans la réponse, vous verrez l’offre de secours que vous avez définie dans l’interface utilisateur de Adobe Experience Platform dans l’ [exercice 3.3.2.2](./ex2.md).

![API OD](./images/api11.png)

### 3.3.6.1.6 Collections de liste

Cliquez pour ouvrir la requête **[!UICONTROL GET - Liste des collections]**.

![API OD](./images/api12.png)

Dans la réponse, vous verrez la collection que vous avez définie dans l’interface utilisateur de Adobe Experience Platform dans l’ [exercice 3.3.2.3](./ex2.md).

![API OD](./images/api13.png)

### 3.3.6.1.7 Obtention d’offres détaillées pour le profil client

Cliquez pour ouvrir la requête **[!UICONTROL POST - Obtenir des offres détaillées pour le profil client]**. Cette requête est similaire à la précédente, mais renvoie en fait des détails tels que des URL d’image, du texte, etc.

![API OD](./images/api23.png)

Pour cette requête, comme pour l’exercice précédent qui présente des exigences similaires, vous devez fournir les valeurs de **[!UICONTROL xdm:placementId]** et **[!UICONTROL xdm:activityId]** pour récupérer les détails spécifiques de l’offre pour un client.

Le champ **[!UICONTROL xdm:activityId]** doit être renseigné. Vous pouvez récupérer cela dans l’interface utilisateur de Adobe Experience Platform, comme indiqué ci-dessous.

![API OD](./images/activityid.png)

Le champ **[!UICONTROL xdm:placementId]** doit être renseigné. Vous pouvez récupérer cela dans l’interface utilisateur de Adobe Experience Platform, comme indiqué ci-dessous. Dans l’exemple ci-dessous, vous pouvez voir le placementId pour l’emplacement **[!UICONTROL Web - Image]**.

![API OD](./images/placementid.png)

Accédez à **[!UICONTROL Body]** et saisissez l’adresse électronique du client pour lequel vous souhaitez demander une offre. Cliquez sur **[!UICONTROL Envoyer]**.

![API OD](./images/api24.png)

Enfin, vous verrez le résultat de quel type d’offre personnalisée et quelles ressources doivent être affichées pour ce client.

![API OD](./images/api25.png)

Vous avez maintenant terminé cet exercice.

Étape suivante : [Résumé et avantages](./summary.md)

[Revenir au module 3.3](./offer-decisioning.md)

[Revenir à tous les modules](./../../../overview.md)
