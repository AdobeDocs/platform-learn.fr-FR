---
title: Customer AI - Tableau de bord de notation et segmentation (prévision et action)
description: Customer AI - Tableau de bord de notation et segmentation (prévision et action)
kt: 5342
doc-type: tutorial
source-git-commit: 2cdc145d7f3933ec593db4e6f67b60961a674405
workflow-type: tm+mt
source-wordcount: '335'
ht-degree: 2%

---

# 2.2.3 Customer AI - Tableau de bord de notation et segmentation (prévoir et prendre des mesures)

Une fois que votre instance Customer AI a terminé une exécution de modèle, vous pouvez visualiser le score de propension évalué afin de prédire un client effectuant un achat au cours des 30 prochains jours.

![AI](./images/caimodels.png)

>[!NOTE]
>
>Seule une instance Customer AI dont l’état est **Success** vous permet de prévisualiser les informations du service.

## 2.2.3.1 Prédiction de propension

Examinons maintenant la propension prédite générée par le modèle d’instance de Customer AI. Cliquez sur le nom de l&#39;instance pour afficher le tableau de bord.

![AI](./images/caimodels1.png)

Le tableau de bord de Customer AI présente un résumé du score, de la répartition de la population et des facteurs d’influence à évaluer par le modèle.

![Description de l’IA](./images/caidescription.png)

![Résumé du tableau de bord](./images/caidashboard.png)

Passez la souris sur les facteurs d’influence pour afficher la ventilation ultérieure des données.

![Facteurs d’influence](./images/caiinfluencefactors.png)

## 2.2.3.2 Actions commerciales

### 2.2.3.2.1 Segmentation des clients

Le tableau de bord de Customer AI permet de définir des segments en un seul clic. Cliquez sur le bouton **Créer un segment** sur les cartes de propension.

![Création d’un segment](./images/caiinfluencefactors1.png)

Vous verrez qu’une définition de segment est créée automatiquement.

![Règle de segment](./images/caicreatesegment.png)

Donnez un nom à votre segment, en respectant cette convention d’affectation des noms : `--demoProfileLdap-- - Customer AI High Propensity`. Cliquez sur **Enregistrer**.

![Règle de segment](./images/caicreatesegment1.png)

Vous pouvez désormais utiliser ce segment pour le ciblage à l’aide de la plateforme CDP, Journey Orchestration et Adobe Target en temps réel, par exemple.

### 2.2.3.2.2 Présentation du profil

Puisque le score de propension de Customer AI fait partie de Real-time Customer Profile, vous pouvez afficher le score de chaque client.

Dans Adobe Experience Platform, accédez à **Profils** dans le menu de gauche et sélectionnez **Parcourir**.

Recherchez un profil à l’aide de l’un des identifiants, comme par exemple **EMAIL hbirkenshawa@businessweek.com**, disponibles dans le fichier JSON que vous avez ingéré. Cliquez sur l’ **ID de profil** pour ouvrir le profil.

![Profile](./images/profile1.png)

Vous verrez alors :

![Profile](./images/profile2.png)

Accédez à **Attributs**, qui contient la sortie de votre modèle Customer AI.

![Profile](./images/profile3.png)

Faites défiler l’écran vers le bas pour voir le score de propension tel que calculé par votre modèle Customer AI.

![Profile](./images/profile4.png)

Étape suivante : [Résumé et avantages](./summary.md)

[Revenir au module 2.2](./intelligent-services.md)

[Revenir à tous les modules](./../../../overview.md)
