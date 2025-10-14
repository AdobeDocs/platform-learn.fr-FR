---
title: Foundation - Configuration de la collecte de données Adobe Experience Platform et de l’extension Web SDK - Implémentation d’Adobe Target
description: Foundation - Configuration de la collecte de données Adobe Experience Platform et de l’extension Web SDK - Implémentation d’Adobe Target
kt: 5342
doc-type: tutorial
exl-id: 31cdde2f-011d-442d-8e47-15a318a6c89d
source-git-commit: 3d61d91111d8693ab031fbd7b26706c02818108c
workflow-type: tm+mt
source-wordcount: '181'
ht-degree: 2%

---

# 1.1.6 Mise en œuvre d’Adobe Target

## Mettre à jour votre flux de données pour utiliser Adobe Target

Si vous souhaitez envoyer les données collectées par Web SDK à Adobe Target et obtenir une réponse d’Adobe Target avec une expérience personnalisée pour chaque client, procédez comme suit.

Accédez à [https://experience.adobe.com/launch/](https://experience.adobe.com/launch/) puis à **Flux de données**.

Dans le coin supérieur droit de l’écran, sélectionnez le nom du sandbox, qui doit être `--aepSandboxName--`. Ouvrez votre flux de données spécifique, nommé `--aepUserLdap-- - Demo System Datastream`.

![Cliquez sur l’icône Configuration Edge dans le volet de navigation de gauche](./images/edgeconfig1b.png)

Tu verras ça. Pour activer Adobe Target, cliquez sur **Ajouter un service**.

![&#x200B; Débogueur AEP &#x200B;](./images/aa2.png)

Tu verras ça. Sélectionnez le service **Adobe Target**, après quoi vous pouvez éventuellement fournir des informations supplémentaires. Cliquez sur **Enregistrer**.

![&#x200B; Débogueur AEP &#x200B;](./images/at1.png)

## Étapes suivantes

Accédez à Exigences du schéma XDM [1.1.7 dans Adobe Experience Platform](./ex7.md){target="_blank"}

Revenez à [Configuration de la collecte de données Adobe Experience Platform et de l’extension de balise Web SDK](./data-ingestion-launch-web-sdk.md){target="_blank"}

Revenir à [Tous les modules](./../../../../overview.md){target="_blank"}
