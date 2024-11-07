---
title: Foundation - Configuration de la collecte de données Adobe Experience Platform et de l’extension du SDK Web - Schéma XDM requis dans Adobe Experience Platform
description: Foundation - Configuration de la collecte de données Adobe Experience Platform et de l’extension du SDK Web - Schéma XDM requis dans Adobe Experience Platform
kt: 5342
doc-type: tutorial
source-git-commit: 2cdc145d7f3933ec593db4e6f67b60961a674405
workflow-type: tm+mt
source-wordcount: '241'
ht-degree: 0%

---

# Exigences de schéma XDM 1.1.7 dans Adobe Experience Platform

Pour que le SDK Web et alloy.js puissent ingérer des données dans Adobe Experience Platform, un mixin XDM spécifique doit faire partie du schéma XDM dans Adobe Experience Platform.

Accédez à [https://experience.adobe.com/platform](https://experience.adobe.com/platform) et connectez-vous.

![Débogueur AEP](./images/exp1.png)

Une fois connecté, sélectionnez l’environnement de test approprié en cliquant sur le texte **Production Prod** dans la ligne bleue en haut de votre écran. Sélectionnez l’environnement de test `--aepSandboxId--`.

Après avoir sélectionné votre environnement de test, l’écran change et vous êtes maintenant dans votre environnement de test.

![Débogueur AEP](./images/exp2.png)

Dans le menu de gauche, accédez à **Schémas** et ouvrez le schéma **Demo System - Event Schema for Website (Global v1.1)**.

![Débogueur AEP](./images/exp3.png)

Sur ce schéma, vous verrez que le groupe de champs **AEP Web SDK ExperienceEvent Mixin** a été ajouté. Ce groupe de champs ajoute tous les champs minimalement requis au schéma. Chaque schéma d’événement d’expérience dans Adobe Experience Platform qui sera utilisé par le SDK Web nécessite toujours que ce groupe de champs fasse partie du schéma.

![Débogueur AEP](./images/exp4.png)

Dans le [module 1.2](./../module1.2/data-ingestion.md), vous apprendrez à ajouter des groupes de champs aux schémas.

Étape suivante : [Résumé et avantages](./summary.md)

[Revenir au module 1.1](./data-ingestion-launch-web-sdk.md)

[Revenir à tous les modules](./../../../overview.md)
