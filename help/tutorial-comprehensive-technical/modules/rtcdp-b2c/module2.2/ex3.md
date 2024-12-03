---
title: Customer AI - Tableau de bord de notation et segmentation (prévision et action)
description: Customer AI - Tableau de bord de notation et segmentation (prévision et action)
kt: 5342
doc-type: tutorial
exl-id: 4dd8489a-65e4-489a-9228-3c642b10e761
source-git-commit: b53ee64ae8438b8f48f842ed1f44ee7ef3e813fc
workflow-type: tm+mt
source-wordcount: '272'
ht-degree: 2%

---

# 2.2.3 Customer AI - Tableau de bord de notation et segmentation (prévoir et prendre des mesures)

Une fois que votre instance Customer AI a terminé une exécution de modèle, vous pouvez visualiser le score de propension évalué afin de prédire un client effectuant un achat au cours des 30 prochains jours.

![AI](./images/caiinstancesummary1.png)

>[!NOTE]
>
>Seule une instance Customer AI dont l’état est **Success** vous permet de prévisualiser les informations du service.

## Prédiction de propension

Examinons maintenant la propension prédite générée par le modèle d’instance de Customer AI. Cliquez sur le nom de l&#39;instance pour afficher le tableau de bord.

![AI](./images/caimodels1.png)

Le tableau de bord de Customer AI présente un résumé du score, de la répartition de la population et des facteurs d’influence à évaluer par le modèle.

![Description de l’IA](./images/caidescription.png)

Passez la souris sur les facteurs d’influence pour afficher la ventilation ultérieure des données.

![Facteurs d’influence](./images/caiinfluencefactors.png)

## Actions commerciales

### Segmentation des clients

Le tableau de bord de Customer AI permet de définir des segments en un seul clic. Cliquez sur le bouton **Créer un segment** sur les cartes de propension.

![Création d’un segment](./images/caiinfluencefactors1.png)

Vous verrez qu’une définition de segment est créée automatiquement.

![Règle de segment](./images/caicreatesegment.png)

Donnez un nom à votre segment, en respectant cette convention d’affectation des noms : `--aepUserLdap-- - Customer AI High Propensity`. Cliquez sur **Publier**.

![Règle de segment](./images/caicreatesegment1.png)

Vous pouvez désormais utiliser ce segment pour le ciblage à l’aide de la plateforme de données clients en temps réel, de Journey Optimizer et d’Adobe Target, par exemple.

## Nettoyage

Pour vous assurer qu’aucune donnée de démonstration inutile n’est conservée dans votre environnement, veillez à supprimer le jeu de données `--aepUserLdap-- - Demo System - Customer Experience Event Dataset` une fois cet exercice terminé. Si vous ne supprimez pas les données de démonstration, il y aura un impact sur les coûts pour votre instance AEP.

![Profile](./images/cleanup.png)

Étape suivante : [Résumé et avantages](./summary.md)

[Revenir au module 2.2](./intelligent-services.md)

[Revenir à tous les modules](./../../../overview.md)
