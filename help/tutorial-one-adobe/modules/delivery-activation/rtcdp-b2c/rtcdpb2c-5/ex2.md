---
title: 'Collecte de données Adobe Experience Platform et transfert côté serveur en temps réel : mettez à jour votre flux de données pour rendre les données disponibles pour la propriété du serveur de collecte de données Adobe Experience Platform'
description: Mettez à jour votre flux de données pour rendre les données disponibles pour la propriété de votre serveur de collecte de données Adobe Experience Platform
kt: 5342
doc-type: tutorial
exl-id: f4bb0673-d553-4027-8bfd-53d2608efaf5
source-git-commit: 3d61d91111d8693ab031fbd7b26706c02818108c
workflow-type: tm+mt
source-wordcount: '236'
ht-degree: 2%

---

# 2.5.2 Mettez à jour votre flux de données pour rendre les données disponibles pour la propriété de votre serveur de collecte de données Adobe Experience Platform

## Mettre à jour votre flux de données

Dans [Prise en main](./../../../getting-started/gettingstarted/ex2.md), vous avez créé votre propre **[!UICONTROL flux de données]**. Vous avez ensuite utilisé le nom `--aepUserLdap-- - Demo System Datastream`.

Dans cet exercice, vous devez configurer ce **[!UICONTROL flux de données]** pour qu’il fonctionne avec votre **propriété du serveur de collecte de données**.

Pour ce faire, accédez à [https://experience.adobe.com/#/data-collection/](https://experience.adobe.com/#/data-collection/). Tu verras ça. Dans le menu de gauche, cliquez sur **[!UICONTROL Flux de données]**.

Dans le coin supérieur droit de l’écran, sélectionnez le nom du sandbox, qui doit être `--aepSandboxName--`.

![Cliquez sur l’icône Configuration Edge dans le volet de navigation de gauche](./images/edgeconfig1b.png)

Recherchez votre **[!UICONTROL Flux de données]**, qui est nommé `--aepUserLdap-- - Demo System Datastream`. Cliquez sur votre **[!UICONTROL flux de données]** pour l’ouvrir.

![WebSDK](./images/websdk0.png)

Tu verras ça. Cliquez sur **[!UICONTROL + Ajouter un service]**.

![WebSDK](./images/websdk3.png)

Sélectionnez le service **Transfert d’événement**. 2 paramètres supplémentaires s’affichent. Sélectionnez votre propriété Transfert d’événement, que vous avez créée dans l’exercice précédent et qui est nommée `--aepUserLdap-- - Demo System (DD/MM/YYYY) (Edge)`. Sélectionnez ensuite **Développement** sous **Environnement**. Cliquez sur **Enregistrer**.

![WebSDK](./images/websdk4.png)

Votre flux de données a été mis à jour et est prêt à être utilisé.

![WebSDK](./images/websdk8a.png)

Votre flux de données est maintenant prêt à fonctionner avec votre **[!DNL Event Forwarding property]**.

## Étapes suivantes

Accédez à [2.5.3 Créer et configurer un webhook personnalisé](./ex3.md){target="_blank"}

Revenez à [Connexions Real-Time CDP : transfert d’événement](./aep-data-collection-ssf.md){target="_blank"}

Revenir à [Tous les modules](./../../../../overview.md){target="_blank"}
