---
title: Foundation - Configuration de la collecte de données Adobe Experience Platform et de l’extension du SDK Web - Schéma XDM requis dans Adobe Experience Platform
description: Foundation - Configuration de la collecte de données Adobe Experience Platform et de l’extension du SDK Web - Schéma XDM requis dans Adobe Experience Platform
kt: 5342
audience: Data Engineer, Data Architect
doc-type: tutorial
activity: develop
exl-id: 8e17129c-633d-45bd-aa70-78cc3d3a2108
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '241'
ht-degree: 1%

---

# Exigences de schéma XDM 1.7 dans Adobe Experience Platform

Pour que le SDK Web et alloy.js puissent ingérer des données dans Adobe Experience Platform, un mixin XDM spécifique doit faire partie du schéma XDM dans Adobe Experience Platform.

Accédez à [https://experience.adobe.com/platform](https://experience.adobe.com/platform) et connectez-vous.

![Débogueur AEP](./images/exp1.png)

Une fois connecté, sélectionnez l’environnement de test approprié en cliquant sur le texte. **Production Prod** dans la ligne bleue en haut de votre écran. Sélection de l’environnement de test `--aepSandboxId--`.

Après avoir sélectionné votre environnement de test, l’écran change et vous êtes maintenant dans votre environnement de test.

![Débogueur AEP](./images/exp2.png)

Dans le menu de gauche, accédez à **Schémas** et ouvrez le **Système de démonstration - Schéma d’événement pour le site web (Global v1.1)** Schéma.

![Débogueur AEP](./images/exp3.png)

Sur ce schéma, vous verrez que le groupe de champs **Mixin ExperienceEvent du SDK Web AEP** a été ajouté. Ce groupe de champs ajoute tous les champs minimalement requis au schéma. Chaque schéma d’événement d’expérience dans Adobe Experience Platform qui sera utilisé par le SDK Web nécessite toujours que ce groupe de champs fasse partie du schéma.

![Débogueur AEP](./images/exp4.png)

Dans [Module 2](./../module2/data-ingestion.md) vous apprendrez à ajouter des groupes de champs aux schémas.

Étape suivante : [Résumé et avantages](./summary.md)

[Revenir au module 1](./data-ingestion-launch-web-sdk.md)

[Revenir à tous les modules](./../../overview.md)
