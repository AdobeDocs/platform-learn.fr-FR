---
title: Foundation - Configuration de la collecte de données Adobe Experience Platform et de l’extension du SDK web - Edge Network, Datastreams et Server Side Data Collection
description: Foundation - Configuration de la collecte de données Adobe Experience Platform et de l’extension du SDK web - Edge Network, Datastreams et Server Side Data Collection
kt: 5342
audience: Data Engineer, Data Architect
doc-type: tutorial
activity: develop
exl-id: 6f7c540f-3804-483d-90f9-b26b4a252b8b
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '580'
ht-degree: 2%

---

# 1.2 Collecte de données côté serveur, flux de données et réseau Edge

## Contexte

Dans cet exercice, vous allez créer une **Datastream**. A **Datastream** indique aux serveurs Adobe Edge où envoyer les données après leur collecte par le SDK Web. Par exemple, souhaitez-vous envoyer les données à Adobe Experience Platform ? Adobe Analytics? Adobe Audience Manager? Adobe Target?

Les flux de données sont toujours gérés dans l’interface utilisateur de la collecte de données Adobe Experience Platform et sont essentiels à la collecte de données Adobe Experience Platform avec le SDK Web. Même lorsque vous implémentez un SDK Web avec une solution de gestion des balises non-Adobe, vous devrez toujours créer votre flux de données dans l’interface utilisateur de la collecte de données Adobe Experience Platform.

Vous allez mettre en oeuvre le SDK Web sur le navigateur au cours de l’exercice suivant. Il vous sera alors plus clair à quoi ressemblent les données collectées. Pour l’instant, nous disons simplement au Datastream où transférer les données.

## Création d’un flux de données

Dans [Exercice 0.2](./../module0/ex2.md) vous avez déjà créé un Datastream, mais nous n’avons pas discuté du contexte et de la raison d’être du Datastream.

Un flux de données indique aux serveurs Adobe Edge où envoyer les données une fois qu’elles ont été collectées par le SDK Web. Par exemple, souhaitez-vous envoyer les données à Adobe Experience Platform ? Adobe Analytics? Adobe Audience Manager? Adobe Target? Les flux de données sont gérés dans l’interface utilisateur de la collecte de données Adobe Experience Platform et sont essentiels à la collecte de données Platform avec le SDK Web, que vous mettiez ou non en oeuvre le SDK Web via la collecte de données Adobe Experience Platform.

Examinons votre **[!UICONTROL Datastream]**:

Accédez à [https://experience.adobe.com/launch/](https://experience.adobe.com/launch/).

Cliquez sur **[!UICONTROL Datastreams]** ou **[!UICONTROL Flux de données (bêta)]** dans le menu de gauche.

![Cliquez sur l’icône de la structure de données dans le volet de navigation de gauche.](./images/edgeconfig1.png)

Recherchez votre flux de données, qui est nommé `--demoProfileLdap-- - Demo System Datastream`.

![Nommez la banque de données et enregistrez-la.](./images/edgeconfig2.png)

Vous verrez ensuite les détails de votre flux de données.

![Nommez la banque de données et enregistrez-la.](./images/edgecfg1.png)

Cliquez sur **...** en regard de **Adobe Experience Platform** et cliquez sur **Modifier**.

![Nommez la banque de données et enregistrez-la.](./images/edgecfg1a.png)

Vous verrez alors ceci. Pour l’instant, vous n’avez activé que Adobe Experience Platform. Votre configuration ressemblera à la configuration ci-dessous. (Selon votre environnement et votre instance Adobe Experience Platform, le nom de l’environnement de test peut être différent).

![Nommez la banque de données et enregistrez-la.](./images/edgecfg2.png)

Vous devez interpréter les champs suivants :

Pour ce flux de données...

- Toutes les données collectées seront stockées dans la variable `--aepSandboxId--` environnement de test dans Adobe Experience Platform
- Toutes les données d’événement d’expérience sont collectées par défaut dans le jeu de données. **Système de démonstration - Jeu de données d’événement pour le site web (Global v1.1)**
- Toutes les données de profil seront collectées par défaut dans le jeu de données. **Système de démonstration - Jeu de données de profil pour le site web (Global v1.1)** (L’ingestion de données de profil en mode natif avec le SDK Web n’est actuellement pas encore prise en charge par le SDK Web et sera rendue disponible ultérieurement)
- Si vous souhaitez utiliser la variable **offer decisioning** service applicatif pour ce Datastream, vous devez cocher la case correspondant à Offer decisioning. (Cela fera partie de [Module 9](./../module9/offer-decisioning.md))
- Si vous souhaitez utiliser la variable **Segmentation Edge**, vous devez cocher la case pour la segmentation Edge.
- Si vous souhaitez utiliser la variable **Destinations de personnalisation**, vous devez cocher la case Destinations de personnalisation .

Pour l’instant, aucune autre configuration n’est nécessaire pour votre flux de données.

Étape suivante : [1.3 Présentation de la collecte de données Adobe Experience Platform](./ex3.md)

[Revenir au module 1](./data-ingestion-launch-web-sdk.md)

[Revenir à tous les modules](./../../overview.md)
