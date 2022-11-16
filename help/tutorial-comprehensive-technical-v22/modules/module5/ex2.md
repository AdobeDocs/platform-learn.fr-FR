---
title: Intelligent Services - Customer AI Création d’une instance (configuration)
description: Customer AI - Création d’une instance (configuration)
kt: 5342
audience: Data Engineer, Data Architect
doc-type: tutorial
activity: develop
exl-id: d9377c97-efed-427a-a063-aa9c6bd1a78a
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '312'
ht-degree: 13%

---

# 5.2 Customer AI - Création d’une instance (configuration)

Customer AI analyse les données d’événement d’expérience existantes pour le client afin de prévoir les taux d’attrition ou de conversion. La création d’une instance Customer AI permet aux marketeurs de définir des objectifs et des mesures.

## 5.2.1 Configuration d’une nouvelle instance de Customer AI

Dans Adobe Experience Platform, cliquez sur **Services** dans le menu de gauche. Le navigateur **Services** apparaît et affiche tous les services disponibles. Dans la carte de Customer AI, cliquez sur **Ouvrir**.

![Navigation dans le service](./images/navigatetoservice.png)

Cliquez sur **Créer une instance**.

![Création d’une instance](./images/createnewinstance.png)

Vous verrez alors ceci.

![Création d’une instance](./images/custai1.png)

Saisissez les détails requis pour l’instance Customer AI :

- Nom : use `--demoProfileLdap-- Product Purchase Propensity`
- Description : use: **Prédire la probabilité pour les clients d’acheter un produit**
- Type de propension : select **Conversion**

![Configuration de la page 1](./images/setuppage1.png)

Cliquez sur **Suivant**.

![Configuration de la page 1](./images/next.png)

Vous verrez alors ceci. Sélectionnez le jeu de données que vous avez créé lors de l’exercice précédent qui est nommé `--demoProfileLdap - Demo System - Customer Experience Event Dataset`. Cliquez sur **Suivant**.

![Configuration de la page 1](./images/custai2.png)

Sélectionner **Se produit** et définir le champ **commerce.purchase.value** comme variable cible.

![Définition de l’objectif de l’IAI](./images/caidefinegoal.png)

Cliquez sur **Suivant**.

![Configuration de la page 1](./images/next.png)

Définissez ensuite votre planning pour qu’il s’exécute. **Hebdomadaire** et définissez l’heure aussi près que possible de l’heure actuelle. Assurez-vous que la bascule **Activation des scores pour Profile** est activée.

![Définition de l’avance CAI](./images/caiadvancepage.png)

Cliquez sur **Terminer**.

![Configuration de la page 1](./images/finish.png)

Vous verrez alors cette fenêtre contextuelle. Cliquez sur **OK**.

![Configuration de la page 1](./images/finish1.png)

Une fois l’instance configurée, vous pouvez l’afficher dans la liste des instances Customer AI et prévisualiser le résumé de la configuration et des détails d’exécution en cliquant sur la ligne de l’instance Customer AI. Le panneau de résumé affiche également les détails des erreurs en cas d’erreur.

![Synthèse de la configuration de l’instance](./images/caiinstancesummary.png)

>[!NOTE]
>
>Vous pouvez modifier n’importe quelle définition ou attribut tant que l’état de votre instance Customer AI est : **En attente de formation** ou **Erreur**

Étape suivante : [5.3 Customer AI - Tableau de bord de notation et segmentation (prévoir et prendre des mesures)](./ex3.md)

[Revenir au module 5](./intelligent-services.md)

[Revenir à tous les modules](./../../overview.md)
