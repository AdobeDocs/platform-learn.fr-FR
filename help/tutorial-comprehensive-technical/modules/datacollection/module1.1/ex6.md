---
title: Foundation - Configuration de la collecte de données Adobe Experience Platform et de l’extension Web SDK - Implémentation d’Adobe Target
description: Foundation - Configuration de la collecte de données Adobe Experience Platform et de l’extension Web SDK - Implémentation d’Adobe Target
kt: 5342
doc-type: tutorial
exl-id: 475e9a34-c80e-41e4-9660-61c79f26922d
source-git-commit: 1526661a80b4d551627dfca42a7e97c9498dd1f2
workflow-type: tm+mt
source-wordcount: '168'
ht-degree: 1%

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

Étape suivante : [1.1.7 Exigences du schéma XDM dans Adobe Experience Platform](./ex7.md)

[Retour au module 1.1](./data-ingestion-launch-web-sdk.md)

[Revenir à tous les modules](./../../../overview.md)
