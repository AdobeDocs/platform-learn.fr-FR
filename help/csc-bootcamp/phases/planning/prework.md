---
title: Le camp d'entraînement du CSC - Autres travaux préliminaires
description: Le camp d'entraînement du CSC - Autres travaux préliminaires
doc-type: multipage-overview
source-git-commit: 989e4e2add1d45571462eccaeebcbe66a77291db
workflow-type: tm+mt
source-wordcount: '478'
ht-degree: 0%

---

# Autres prétâches

## Sélection de ressources de marque

Comme décrit dans le dossier créatif, il y a des ressources nécessaires pour lancer efficacement notre campagne. Ces ressources de marque seront ajoutées à la campagne dans Workfront afin que nous y ayons accès de manière centralisée.

- Développez la tâche 1, &quot;TÂCHES INITIALES&quot;, puis ouvrez la tâche &quot;Sélectionner 5 ressources de marque (avant, arrière, etc.)&quot; en cliquant dessus.

![tâche d’ouverture de ressources](./images/wf-open-assets-task.png)

- Cliquez sur &quot;Documents&quot;, puis sur &quot;Ajouter nouveau :

![ajouter un document](./images/wf-add-new-doc.png)

- Sélectionnez &quot;From experience-manager&quot;; cela nous permet de sélectionner des ressources de marque déjà disponibles dans AEM Assets :

![depuis experience-manager](./images/wf-from-aem.png)

- Une fois la hiérarchie AEM Dossier affichée, accédez au chemin suivant : experience-manager > Adobe Assets > Blocs de vélos Sélectionnez 5 ressources, puis cliquez sur &quot;Lien&quot;.

![ressources sélectionnées](./images/selected-assets.png)

- Nous avons maintenant nos ressources de marque sur notre tâche. Cela signifie que nous pouvons définir la tâche 2 comme 100 % terminée :

![tâche complète](./images/wf-task-2-complete.png)


## Démonstration d’Adobe Commerce

Adobe Commerce est l’un des nombreux produits de Adobe Experience Cloud qui peuvent vous aider à offrir les meilleures expériences numériques à vos clients. Cependant, il y avait tout simplement trop peu de temps pour tout faire ensemble pendant le bootcamp.

Cette vidéo vous fait connaitre Adobe Commerce et montre le produit que nous avons créé pour l’utiliser pendant le bootcamp. Dans un scénario réel, vous téléchargerez les ressources de marque sélectionnées précédemment dans Adobe Commerce vers la configuration du produit.

>[!VIDEO](https://video.tv.adobe.com/v/3418945?quality=12&learn=on)

Une fois cette tâche terminée, vous pouvez marquer la tâche 3 comme étant entièrement terminée dans Workfront.

## Des campagnes flexibles sont une condition préalable

En examinant notre plan de travail, nous avons remarqué un petit problème : Notre gestionnaire de produit (le demandeur) a mis à jour une demande qu’il a oubliée pour une &quot;bannière de page d’accueil de produit&quot;.  Nous l&#39;ajouterons à notre plan de projet.

- Accédez à la liste Tâches et ajoutez notre tâche &quot;Créer une bannière de page d’accueil de produit&quot; juste en dessous de la tâche 4 &quot;PRODUCTION&quot;. Pour ce faire, sélectionnez la tâche &quot;Préparer le contenu de l’application mobile&quot; et cliquez sur &quot;Ajouter la tâche au-dessus de l’icône&quot; :

![ajouter une tâche ci-dessus](./images/wf-add-task-above.png)

- Attribuez à la tâche ajoutée un nom significatif, tel que &quot;Créer une bannière de page d’accueil de produit&quot;.

![créer une tâche](./images/wf-create-banner.png)

- Maintenant que nous avons créé la tâche, ajoutons du contenu à celle-ci. Cliquez sur les trois points à droite du titre de votre projet et sélectionnez &quot;Joindre un modèle&quot; :

![joindre un modèle](./images/wf-attach-template.png)

- Sélectionnez &quot;Créer une bannière de page d’accueil de produit&quot; et cliquez sur &quot;Personnaliser et joindre&quot; :

![créer une bannière de page d’accueil de produit](./images/wf-homepage-banner.png)

- Dans l’écran de personnalisation, veillez à mentionner la tâche &quot;Créer une bannière de page d’accueil de produit&quot; en tant que parent :

![ajouter un parent](./images/wf-create-banner-parent.png)

- Enfin, veillez à marquer la tâche parent &quot;Créer une page d’accueil de produit&quot; avec un prédécesseur de la tâche 3, car aucune production ne peut être lancée tant que le produit n’a pas été créé dans Adobe Commerce :

![ajouter le bon prédécesseur](./images/wf-predecessor.png)

Nous avons maintenant une campagne qui est terminée et planifiée, ce qui signifie que nous pouvons maintenant commencer par la production et la diffusion de notre campagne !


Étape suivante : [Phase 2 - Production : Créer une bannière de page d’accueil de produit](../production/banner.md)

[Revenir à la phase 1 - Planification : Planification](./planning.md)

[Revenir à tous les modules](../../overview.md)