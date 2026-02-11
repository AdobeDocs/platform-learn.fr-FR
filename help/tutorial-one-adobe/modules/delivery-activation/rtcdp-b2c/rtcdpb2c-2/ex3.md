---
title: Customer AI - Tableau de bord de notation et segmentation (prédire et agir)
description: Customer AI - Tableau de bord de notation et segmentation (prédire et agir)
kt: 5342
doc-type: tutorial
exl-id: a6df3ff1-f907-4185-8189-f0b39c67c943
source-git-commit: 2d5ca888eb24c1f65b4ecd48030ec8d1659b7f84
workflow-type: tm+mt
source-wordcount: '269'
ht-degree: 3%

---

# 2.2.3 IA dédiée aux clients - Tableau de bord de notation et segmentation (prévoir et prendre des mesures)

Une fois que votre instance IA dédiée aux clients a terminé l’exécution d’un modèle, elle vous permet de visualiser le score de propension qui est évalué pour prédire qu’un client effectuera un achat au cours des 30 prochains jours.

![AI](./images/caiinstancesummary1.png)

>[!NOTE]
>
>Seule une instance IA dédiée aux clients dont le statut est **Succès** vous permettra de prévisualiser les informations du service.

## Prédiction de propension

Examinons maintenant la propension prévue générée par le modèle d’instance de l’IA dédiée aux clientes et clients. Cliquez sur le nom de l’instance pour afficher le tableau de bord.

![AI](./images/caimodels1.png)

Le tableau de bord de l’IA dédiée aux clientes et clients présente le résumé du score, la répartition de la population et les facteurs d’influence que le modèle doit évaluer.

![Description IA](./images/caidescription.png)

Passez la souris sur les facteurs d’influence pour afficher la répartition détaillée de la distribution des données.

![Facteurs d’influence](./images/caiinfluencefactors.png)

## Actions de l’entreprise

### Segmenter les clients

Le tableau de bord de l’IA dédiée aux clients permet de définir des segments en un seul clic. Cliquez sur le bouton **Créer un segment** sur les cartes de propension.

![Création d’un segment](./images/caiinfluencefactors1.png)

Une définition de segment est créée automatiquement.

![ Règle de segment ](./images/caicreatesegment.png)

Attribuez un nom à votre segment en suivant cette convention de nommage : `--aepUserLdap-- - Customer AI High Propensity`. Cliquez sur **Publier**.

![ Règle de segment ](./images/caicreatesegment1.png)

Vous pouvez désormais utiliser ce segment pour le ciblage à l’aide de Real-Time CDP, Journey Optimizer et Adobe Target, par exemple.

## Nettoyage

Pour vous assurer qu’aucune donnée de démonstration inutile n’est conservée dans votre environnement, veillez à supprimer le jeu de données `--aepUserLdap-- - Demo System - Customer Experience Event Dataset` une fois cet exercice terminé. Si vous ne supprimez pas les données de démonstration, votre instance AEP subira un impact sur les coûts.

![Profile](./images/cleanup.png)

## Étapes suivantes

Revenir à [Services intelligents](./intelligent-services.md){target="_blank"}

Revenir à [Tous les modules](./../../../../overview.md){target="_blank"}
