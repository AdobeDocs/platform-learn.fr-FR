---
title: Collecte de données Adobe Experience Platform et transfert côté serveur en temps réel - Mettez à jour votre flux de données pour rendre les données disponibles pour la propriété du serveur de collecte de données Adobe Experience Platform
description: Mettez à jour votre flux de données pour rendre les données disponibles pour la propriété du serveur de collecte de données Adobe Experience Platform.
kt: 5342
doc-type: tutorial
source-git-commit: 2cdc145d7f3933ec593db4e6f67b60961a674405
workflow-type: tm+mt
source-wordcount: '228'
ht-degree: 1%

---

# 2.5.2 Mise à jour de la matrice de données pour rendre les données disponibles pour la propriété du serveur de collecte de données Adobe Experience Platform

## 2.5.2.1 Mise à jour de la matrice de données

Dans l&#39; [exercice 0.2](./../../gettingstarted/gettingstarted/ex2.md), vous avez créé votre propre **[!UICONTROL Datastream]**. Vous avez ensuite utilisé le nom `--demoProfileLdap-- - Demo System Datastream`.

Dans cet exercice, vous devez configurer cet **[!UICONTROL Datastream]** pour qu’il fonctionne avec votre **[!DNL Data Collection Server property]**.

Pour ce faire, accédez à [https://experience.adobe.com/#/data-collection/](https://experience.adobe.com/#/data-collection/). Vous verrez alors ceci. Dans le menu de gauche, cliquez sur **[!UICONTROL Datastreams]**.

Dans le coin supérieur droit de votre écran, sélectionnez le nom de votre environnement de test, qui doit être `--aepSandboxId--`.

![Cliquez sur l’icône de configuration Edge dans le volet de navigation de gauche](./images/edgeconfig1b.png)

Recherchez votre **[!UICONTROL Datastream]**, qui est nommé `--demoProfileLdap-- - Demo System Datastream`. Cliquez sur votre **[!UICONTROL Datastream]** pour l’ouvrir.

![WebSDK](./images/websdk0.png)

Vous verrez alors ceci. Cliquez sur **[!UICONTROL + Ajouter un service]**.

![WebSDK](./images/websdk3.png)

Sélectionnez le service **Transfert d’événement**. Vous verrez alors 2 paramètres supplémentaires. Sélectionnez la propriété Event Forwarding que vous avez créée lors de l’exercice précédent et qui est nommée `--demoProfileLdap-- - Demo System (DD/MM/YYYY) (Edge)`. Sélectionnez ensuite **Développement** sous **Environnement**. Cliquez sur **Enregistrer**.

![WebSDK](./images/websdk4.png)

Votre flux de données a été mis à jour et est prêt à l’emploi.

![WebSDK](./images/websdk8a.png)

Votre flux de données est maintenant prêt à fonctionner avec votre **[!DNL Event Forwarding property]**.

Étape suivante : [2.5.3 Créer et configurer un webhook personnalisé](./ex3.md)

[Revenir au module 2.5](./aep-data-collection-ssf.md)

[Revenir à tous les modules](./../../../overview.md)
