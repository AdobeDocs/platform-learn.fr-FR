---
title: Camp d'entraînement du SCC - Autres travaux préalables
description: Camp d'entraînement du SCC - Autres travaux préalables
doc-type: multipage-overview
exl-id: 76546141-68d5-4f09-b44a-e06cc08bbaa7
source-git-commit: 286c85aa88d44574f00ded67f0de8e0c945a153e
workflow-type: tm+mt
source-wordcount: '489'
ht-degree: 0%

---

# Autres travaux préalables

## Sélectionner Brand Assets

Comme indiqué dans le dossier de création, certaines ressources seront nécessaires pour lancer efficacement notre campagne. Ces ressources de marque seront ajoutées à la campagne dans Workfront afin que nous y ayons accès de manière centralisée.

- Développez la tâche 1, « TÂCHES INITIALES », puis ouvrez la tâche « Sélectionner 5 ressources de marque (au premier plan, à l’arrière, etc.) » en cliquant dessus.

![tâche ouvrir les ressources](./images/wf-open-assets-task.png)

- Cliquez sur &#39;Documents&#39; puis sur &#39;Ajouter nouveau :

![ajouter document](./images/wf-add-new-doc.png)

- Sélectionnez « Depuis experience-manager » ; cela nous permettra de sélectionner les ressources de marque déjà disponibles sur AEM Assets :

![from experience-manager](./images/wf-from-aem.png)

- Une fois que la hiérarchie des dossiers AEM s’affiche, accédez au chemin suivant : experience-manager > Adobe Bike Assets > Vélos Sélectionnez 5 ressources, puis cliquez sur « Lien ».

![ ressources sélectionnées ](./images/selected-assets.png)

- Nous avons désormais nos ressources de marque à notre disposition. Cela signifie que nous pouvons définir la tâche 2 comme 100 % terminée :

![terminer la tâche](./images/wf-task-2-complete.png)


## Démonstration d’Adobe Commerce

Adobe Commerce est l’un des nombreux produits de Adobe Experience Cloud qui peuvent vous aider à offrir les meilleures expériences digitales à vos clients. Cependant, il y avait tout simplement trop peu de temps pour tout faire ensemble pendant le camp d&#39;entraînement.

Cette vidéo vous familiarise avec Adobe Commerce et présente le produit que nous avons créé pour être utilisé pendant le bootcamp. Dans un scénario réel, vous pouvez charger les ressources de marque sélectionnées précédemment dans Adobe Commerce vers la configuration du produit.

>[!VIDEO](https://video.tv.adobe.com/v/3418945?quality=12&learn=on&enablevpops)

Une fois cette tâche terminée, vous pouvez marquer la tâche 3 comme 100 % terminée dans Workfront.

## Des campagnes flexibles sont indispensables

Lors de l’examen de notre plan de travail, nous avons remarqué un petit problème : notre chef de produit (le demandeur) a mis à jour une mise à jour qu’il a oublié de demander pour une « bannière de page d’accueil du produit ».  Nous l’ajouterons à notre plan de projet.

- Accédez à la liste Tâches et ajoutez notre tâche « Créer une bannière de page d’accueil de produit » juste en dessous de la tâche 4 « PRODUCTION ». Pour ce faire, sélectionnez la tâche « Préparer le contenu de l’application mobile » et cliquez sur l’icône « Ajouter une tâche au-dessus de » :

![ajouter une tâche ci-dessus](./images/wf-add-task-above.png)

- Donnez un nom explicite à la tâche ajoutée, comme « Créer une bannière de page d’accueil de produit ».

![créer une tâche](./images/wf-create-banner.png)

- Maintenant que nous avons créé la tâche, nous allons lui ajouter du contenu. Cliquez sur les trois points à droite du titre de votre projet et sélectionnez « Joindre un modèle » :

![joindre un modèle](./images/wf-attach-template.png)

- Sélectionnez « Créer une bannière de page d’accueil de produit » et cliquez sur « Personnaliser et joindre » :

![créer une bannière de page d’accueil de produit](./images/wf-homepage-banner.png)

- Dans l’écran de personnalisation, veillez à mentionner la tâche « Créer une bannière de page d’accueil de produit » comme parent :

![ajouter un parent](./images/wf-create-banner-parent.png)

- Enfin, veillez à marquer la tâche parent « Créer la page d’accueil du produit » avec un prédécesseur de la tâche 3, car aucune production ne peut être démarrée tant que le produit n’a pas été créé dans Adobe Commerce :

![ajouter le prédécesseur approprié](./images/wf-predecessor.png)

Nous disposons désormais d’une campagne terminée et planifiée, ce qui signifie que nous pouvons maintenant commencer la production et la diffusion de notre campagne !


Étape suivante : [Phase 2 - Production : créer une bannière de page d’accueil de produit](../production/banner.md)

[Revenir à la phase 1 - Planification : Planification](./planning.md)

[Revenir à tous les modules](../../overview.md)
