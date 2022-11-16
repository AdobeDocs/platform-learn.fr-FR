---
title: Foundation - Configuration de la collecte de données Adobe Experience Platform et de l’extension du SDK Web - Mise en oeuvre d’Adobe Target
description: Foundation - Configuration de la collecte de données Adobe Experience Platform et de l’extension du SDK Web - Mise en oeuvre d’Adobe Target
kt: 5342
audience: Data Engineer, Data Architect
doc-type: tutorial
activity: develop
exl-id: 4aee8ae2-38ca-49a3-8f1b-57713d16f5b5
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '177'
ht-degree: 0%

---

# 1.6 Mise en oeuvre d’Adobe Target

## 1.6. Mettre à jour votre flux de données pour utiliser Adobe Target

Si vous souhaitez envoyer des données collectées par le SDK Web à Adobe Target et obtenir une réponse d’Adobe Target avec une expérience personnalisée pour chaque client, procédez comme suit.

Accédez à [https://experience.adobe.com/launch/](https://experience.adobe.com/launch/) et accédez à **Datastreams**.

Dans le coin supérieur droit de votre écran, sélectionnez le nom de votre environnement de test, qui doit être `--aepSandboxId--`. Ouvrez votre flux de données spécifique, nommé `--demoProfileLdap-- - Demo System Datastream`.

![Cliquez sur l’icône Edge Configuration dans le volet de navigation de gauche.](./images/edgeconfig1b.png)

Vous verrez alors ceci. Pour activer Adobe Target, cliquez sur **+Ajouter un service**.

![Débogueur AEP](./images/aa2.png)

Vous verrez alors ceci. Sélectionner le service **Adobe Target**, après quoi vous pouvez éventuellement fournir des informations supplémentaires. Pour l’instant, il n’est pas nécessaire de l’enregistrer, donc cliquez sur **Annuler**.

![Débogueur AEP](./images/at1.png)

Étape suivante : [Exigences de schéma XDM 1.7 dans Adobe Experience Platform](./ex7.md)

[Revenir au module 1](./data-ingestion-launch-web-sdk.md)

[Revenir à tous les modules](./../../overview.md)
