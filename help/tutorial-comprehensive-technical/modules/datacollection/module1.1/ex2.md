---
title: Foundation - Configuration de la collecte de données Adobe Experience Platform et de l’extension du SDK Web - Edge Network, flux de données et collecte de données côté serveur
description: Foundation - Configuration de la collecte de données Adobe Experience Platform et de l’extension du SDK Web - Edge Network, flux de données et collecte de données côté serveur
kt: 5342
doc-type: tutorial
exl-id: e97d40b5-616d-439c-9d6b-eaa4ebf5acb0
source-git-commit: 0dbcda0cfc9f199a44c845c1b5caf00a8d740251
workflow-type: tm+mt
source-wordcount: '597'
ht-degree: 0%

---

# 1.1.2 Edge Network, flux de données et collecte de données côté serveur

## Contexte

Dans cet exercice, vous allez créer un **Datastream**. Un **datastream** indique aux serveurs Adobe Edge où envoyer les données une fois qu’elles ont été collectées par le SDK Web. Par exemple, souhaitez-vous envoyer les données à Adobe Experience Platform ? ADOBE ANALYTICS ? ADOBE AUDIENCE MANAGER ? ADOBE TARGET ?

Les flux de données sont toujours gérés dans l’interface utilisateur de la collecte de données Adobe Experience Platform et sont essentiels à la collecte de données Adobe Experience Platform avec le SDK Web. Même lorsque vous implémentez un SDK Web avec une solution de gestion des balises non-Adobe, vous devrez toujours créer votre flux de données dans l’interface utilisateur de la collecte de données Adobe Experience Platform.

Vous allez mettre en oeuvre le SDK Web sur le navigateur au cours de l’exercice suivant. Il vous sera alors plus clair à quoi ressemblent les données collectées. Pour l’instant, nous disons simplement au Datastream où transférer les données.

## Création d’un flux de données

Dans [Prise en main](./../../../modules/gettingstarted/gettingstarted/ex2.md), vous avez déjà créé un flux de données, mais nous n’avons pas discuté de l’arrière-plan et de la raison d’être du flux de données.

Un flux indique aux serveurs Adobe Edge où envoyer les données une fois qu’elles ont été collectées par le SDK Web. Par exemple, souhaitez-vous envoyer les données à Adobe Experience Platform ? ADOBE ANALYTICS ? ADOBE AUDIENCE MANAGER ? ADOBE TARGET ? Les flux de données sont gérés dans l’interface utilisateur de la collecte de données Adobe Experience Platform et sont essentiels à la collecte de données à l’aide du SDK Web, que vous mettiez ou non en oeuvre le SDK Web via la collecte de données Adobe Experience Platform.

Examinons votre **[!UICONTROL Datastream]** :

Accédez à [https://experience.adobe.com/launch/](https://experience.adobe.com/launch/).

Cliquez sur **[!UICONTROL Datastreams]** dans le menu de gauche.

![Cliquez sur l’icône Datastream dans le volet de navigation de gauche](./images/edgeconfig1.png)

Ouvrez votre flux de données, qui s’appelle `--aepUserLdap-- - Demo System Datastream`.

![Nommez le flux de données et enregistrez](./images/edgeconfig2.png)

Vous verrez ensuite les détails de votre flux de données.

![Nommez le flux de données et enregistrez](./images/edgecfg1.png)

Cliquez sur **...** en regard de **Adobe Experience Platform** et cliquez sur **Modifier**.

![Nommez le flux de données et enregistrez](./images/edgecfg1a.png)

Vous verrez alors ceci. Pour l’instant, vous n’avez activé que Adobe Experience Platform. Votre configuration ressemblera à la configuration ci-dessous. (Selon votre environnement et votre instance Adobe Experience Platform, le nom de l’environnement de test peut être différent).

![Nommez le flux de données et enregistrez](./images/edgecfg2.png)

Vous devez interpréter les champs ci-dessous comme suit :

Pour ce flux de données...

- Toutes les données collectées seront stockées dans l’environnement de test `--aepSandboxName--` de Adobe Experience Platform.
- Toutes les données d’événement d’expérience sont collectées par défaut dans le jeu de données **Demo System - Event Dataset for Website (Global v1.1)**
- Toutes les données Profile seront collectées par défaut dans le jeu de données **Demo System - Profile Dataset for Website (Global v1.1)** (l’ingestion de données de profil en mode natif avec le SDK Web n’est actuellement pas encore prise en charge par le SDK Web)
- Si vous souhaitez utiliser le service d’application **Offer decisioning** pour cette banque de données, vous devez cocher la case pour l’Offer decisioning. (Cela fera partie du [module 3.3](./../../../modules/ajo-b2c/module3.3/offer-decisioning.md))
- **La segmentation Edge** est activée par défaut, ce qui signifie que les segments admissibles seront évalués à la périphérie, lors de l’ingestion du trafic entrant.
- Si vous souhaitez utiliser les **destinations Personalization**, vous devez cocher la case correspondant aux destinations Personalization.
- 
   - Si vous souhaitez utiliser les fonctionnalités de **Adobe Journey Optimizer** dans ce flux de données, vous devez cocher la case correspondant à Adobe Journey Optimizer.


Pour l’instant, aucune autre configuration n’est nécessaire pour votre flux de données.

Étape suivante : [1.1.3 Introduction à la collecte de données Adobe Experience Platform](./ex3.md)

[Revenir au module 1.1](./data-ingestion-launch-web-sdk.md)

[Revenir à tous les modules](./../../../overview.md)
