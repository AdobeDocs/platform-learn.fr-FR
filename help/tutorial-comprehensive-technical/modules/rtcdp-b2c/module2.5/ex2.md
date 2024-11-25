---
title: Collecte de données Adobe Experience Platform et transfert côté serveur en temps réel - Mettez à jour votre flux de données pour rendre les données disponibles pour la propriété du serveur de collecte de données Adobe Experience Platform
description: Mettez à jour votre flux de données pour rendre les données disponibles pour la propriété du serveur de collecte de données Adobe Experience Platform.
kt: 5342
doc-type: tutorial
exl-id: 7b5b598e-e54c-4f0f-b260-d643600ee6ca
source-git-commit: 6485bfa1c75c43bb569f77c478a273ace24a61d4
workflow-type: tm+mt
source-wordcount: '231'
ht-degree: 1%

---

# 2.5.2 Mise à jour de la matrice de données pour rendre les données disponibles pour la propriété du serveur de collecte de données Adobe Experience Platform

## Mettre à jour votre flux de données

Dans [Prise en main](./../../gettingstarted/gettingstarted/ex2.md), vous avez créé votre propre **[!UICONTROL Datastream]**. Vous avez ensuite utilisé le nom `--aepUserLdap-- - Demo System Datastream`.

Dans cet exercice, vous devez configurer cet **[!UICONTROL entrepôt de données]** pour qu’il fonctionne avec votre **propriété du serveur de collecte de données**.

Pour ce faire, accédez à [https://experience.adobe.com/#/data-collection/](https://experience.adobe.com/#/data-collection/). Vous verrez alors ceci. Dans le menu de gauche, cliquez sur **[!UICONTROL Datastreams]**.

Dans le coin supérieur droit de votre écran, sélectionnez le nom de votre environnement de test, qui doit être `--aepSandboxName--`.

![Cliquez sur l’icône de configuration Edge dans le volet de navigation de gauche](./images/edgeconfig1b.png)

Recherchez votre **[!UICONTROL Datastream]**, qui est nommé `--aepUserLdap-- - Demo System Datastream`. Cliquez sur votre **[!UICONTROL Datastream]** pour l’ouvrir.

![WebSDK](./images/websdk0.png)

Vous verrez alors ceci. Cliquez sur **[!UICONTROL + Ajouter un service]**.

![WebSDK](./images/websdk3.png)

Sélectionnez le service **Transfert d’événement**. Vous verrez alors 2 paramètres supplémentaires. Sélectionnez la propriété Event Forwarding que vous avez créée lors de l’exercice précédent et qui est nommée `--aepUserLdap-- - Demo System (DD/MM/YYYY) (Edge)`. Sélectionnez ensuite **Développement** sous **Environnement**. Cliquez sur **Enregistrer**.

![WebSDK](./images/websdk4.png)

Votre flux de données a été mis à jour et est prêt à l’emploi.

![WebSDK](./images/websdk8a.png)

Votre flux de données est maintenant prêt à fonctionner avec votre **[!DNL Event Forwarding property]**.

Étape suivante : [2.5.3 Créer et configurer un webhook personnalisé](./ex3.md)

[Revenir au module 2.5](./aep-data-collection-ssf.md)

[Revenir à tous les modules](./../../../overview.md)
