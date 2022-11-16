---
title: Collecte de données Adobe Experience Platform et transfert côté serveur en temps réel - Mettez à jour votre flux de données pour rendre les données disponibles pour la propriété du serveur de collecte de données Adobe Experience Platform
description: Mettez à jour votre flux de données pour rendre les données disponibles pour la propriété du serveur de collecte de données Adobe Experience Platform.
kt: 5342
audience: Data Engineer, Data Architect, Data Analyst
doc-type: tutorial
activity: develop
exl-id: 0c42350c-c38a-410e-bdab-41aff6024f81
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '224'
ht-degree: 2%

---

# 14.2 Mise à jour de la matrice de données pour rendre les données disponibles pour la propriété du serveur de collecte de données Adobe Experience Platform

## 14.2.1 Mettre à jour votre flux de données

Dans [Exercice 0.2](./../../modules/module0/ex2.md), vous avez créé votre propre **[!UICONTROL Datastream]**. Vous avez ensuite utilisé le nom `--demoProfileLdap-- - Demo System Datastream`.

Dans cet exercice, vous devez configurer **[!UICONTROL Datastream]** pour travailler avec votre **[!DNL Data Collection Server property]**.

Pour ce faire, accédez à [https://experience.adobe.com/#/data-collection/](https://experience.adobe.com/#/data-collection/). Vous verrez alors ceci. Dans le menu de gauche, cliquez sur **[!UICONTROL Datastreams]**.

Dans le coin supérieur droit de votre écran, sélectionnez le nom de votre environnement de test, qui doit être `--aepSandboxId--`.

![Cliquez sur l’icône Edge Configuration dans le volet de navigation de gauche.](./images/edgeconfig1b.png)

Recherchez votre **[!UICONTROL Datastream]**, qui est nommé `--demoProfileLdap-- - Demo System Datastream`. Cliquez sur **[!UICONTROL Datastream]** pour l’ouvrir.

![WebSDK](./images/websdk0.png)

Vous verrez alors ceci. Cliquez sur **[!UICONTROL + Ajouter un service]**.

![WebSDK](./images/websdk3.png)

Sélectionner le service **Transfert d’événement**. Vous verrez alors 2 paramètres supplémentaires. Sélectionnez la propriété Event Forwarding que vous avez créée lors de l’exercice précédent et qui est nommée `--demoProfileLdap-- - Demo System (DD/MM/YYYY) (Edge)`. Sélectionnez **Développement** under **Environnement**. Cliquez sur **Enregistrer**.

![WebSDK](./images/websdk4.png)

Votre flux de données a été mis à jour et est prêt à l’emploi.

![WebSDK](./images/websdk8a.png)

Votre flux de données est maintenant prêt à fonctionner avec votre **[!DNL Event Forwarding property]**.

Étape suivante : [14.3 Création et configuration d’un webhook personnalisé](./ex3.md)

[Revenir au module 14](./aep-data-collection-ssf.md)

[Revenir à tous les modules](./../../overview.md)
