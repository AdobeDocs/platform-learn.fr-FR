---
title: Foundation - Configuration de la collecte de données Adobe Experience Platform et de l’extension du SDK Web - Mise en oeuvre d’Adobe Target
description: Foundation - Configuration de la collecte de données Adobe Experience Platform et de l’extension du SDK Web - Mise en oeuvre d’Adobe Target
kt: 5342
doc-type: tutorial
exl-id: 475e9a34-c80e-41e4-9660-61c79f26922d
source-git-commit: 3a19e88e820c63294eff38bb8f699a9f690afcb9
workflow-type: tm+mt
source-wordcount: '168'
ht-degree: 1%

---

# 1.1.6 Mise en oeuvre d’Adobe Target

## Mettre à jour votre flux de données pour utiliser Adobe Target

Si vous souhaitez envoyer des données collectées par le SDK Web à Adobe Target et obtenir une réponse d’Adobe Target avec une expérience personnalisée pour chaque client, procédez comme suit.

Accédez à [https://experience.adobe.com/launch/](https://experience.adobe.com/launch/) et à **Datastreams**.

Dans le coin supérieur droit de votre écran, sélectionnez le nom de votre environnement de test, qui doit être `--aepSandboxName--`. Ouvrez votre flux de données spécifique, appelé `--aepUserLdap-- - Demo System Datastream`.

![Cliquez sur l’icône de configuration Edge dans le volet de navigation de gauche](./images/edgeconfig1b.png)

Vous verrez alors ceci. Pour activer Adobe Target, cliquez sur **+Ajouter un service**.

![Débogueur AEP](./images/aa2.png)

Vous verrez alors ceci. Sélectionnez le service **Adobe Target**, après lequel vous pouvez éventuellement fournir des informations supplémentaires. Cliquez sur **Enregistrer**.

![Débogueur AEP](./images/at1.png)

Étape suivante : [1.1.7 Exigences de schéma XDM dans Adobe Experience Platform](./ex7.md)

[Revenir au module 1.1](./data-ingestion-launch-web-sdk.md)

[Revenir à tous les modules](./../../../overview.md)
