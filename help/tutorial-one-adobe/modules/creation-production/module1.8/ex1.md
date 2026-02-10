---
title: Prise en main de Workfront, Frame.io et ESM
description: Prise en main de Workfront, Frame.io et ESM
role: Developer
level: Beginner
jira: KT-5342
doc-type: Tutorial
exl-id: 2f9a3eef-16ef-497c-97f7-377ff9ed2f82
source-git-commit: 8f746831d4a1481f8ccc14539273c4b16ca5170b
workflow-type: tm+mt
source-wordcount: '1022'
ht-degree: 1%

---

# 1.8.1 Prise en main de Workfront, Frame.io et ESM

## Terminologie des workflows 1.8.1.1 Workfront

Les principaux objets et concepts de Workfront sont les suivants :

| Nom | Dernière mise à jour |
| ---------------------- | ------------ | 
| Portefeuille | Ensemble de projets présentant des caractéristiques unificatrices. Ces projets se disputent généralement les mêmes ressources, le même budget ou le même créneau horaire. |
| Programme | Sous-ensemble au sein d’un portefeuille, dans lequel des projets similaires peuvent être regroupés afin d’obtenir un bénéfice bien défini. |
| Projet | Une grande quantité de travail qui doit être achevée dans un délai spécifique et qui doit utiliser un budget et un nombre de ressources spécifiques. Pour le rendre gérable, vous divisez le projet en une série de tâches. Lorsque vous terminez toutes les tâches, le projet est également terminé. |
| Modèle de projet | Vous pouvez utiliser des modèles de projet pour capturer la plupart des processus, informations et paramètres répétables associés aux projets de votre entreprise. Après avoir créé des modèles, vous pouvez les joindre à des projets existants ou les utiliser pour créer de nouveaux projets. |
| Tâche | Une activité qui doit être effectuée comme une étape vers l’atteinte d’un objectif final (terminer le projet). Les tâches ne peuvent jamais exister indépendamment. Ils font toujours partie d&#39;un projet. |
| Affectation | Utilisateur, fonction ou équipe affecté à un événement ou à une tâche. Les projets, portefeuilles ou programmes ne peuvent pas avoir d&#39;affectations. |
| Document/Version | Tout fichier joint à un objet dans Workfront. Chaque fois qu’un même document est chargé dans le même objet, un numéro de version lui est attribué. Les utilisateurs et utilisatrices peuvent afficher et modifier plusieurs options d’une version précédente d’un document. |
| Validation | Un élément de travail donné, tel qu’une tâche, un document ou une feuille de temps, peut nécessiter l’approbation d’un superviseur ou d’un autre utilisateur sur l’élément de travail. Ce processus d’approbation est appelé approbation. |


Accédez à [https://experience.adobe.com/](https://experience.adobe.com/){target="_blank"}. Cliquez pour ouvrir **Workfront**.

![Planification Workfront](./images/wfpl1.png)

Tu verras ça.

![WF](./images/wfb1.png)

## 1.8.1.2 Activer le plan directeur Workfront

À l’étape suivante, vous allez créer un projet à l’aide d’un modèle. Adobe Workfront vous fournit un certain nombre de plans directeurs disponibles qui doivent simplement être activés.

Pour le cas d&#39;utilisation de CitiSignal, le plan directeur **Exécution de campagne intégrée** est celui que vous devez utiliser.

Pour installer ce plan directeur, ouvrez le menu et sélectionnez **Plans directeurs**.

![WF](./images/blueprint1.png)

Sélectionnez le filtre **Marketing** puis faites défiler l’écran vers le bas pour trouver le plan directeur **Exécution de campagne intégrée**. Cliquez sur **Installer**.

![WF](./images/blueprint2.png)

Cliquez sur **Continuer**.

![WF](./images/blueprint3.png)

Remplacez **Nom du modèle de projet** par `--aepUserLdap-- - Integrated Campaign Execution`.

Cliquez sur **Installer le plan directeur**.

![WF](./images/blueprint4.png)

Après quelques minutes, le plan directeur sera installé.

![WF](./images/blueprint6.png)

## 1.8.1.3 Créer un projet

Ouvrez le **menu** et accédez à **Portefeuilles**.

![WF](./images/wfp6a.png)

Cliquez sur **+ Nouveau Portfolio**.

![WF](./images/wfpfolio1.png)

Saisissez le nom du portefeuille `--aepUserLdap-- - CitiSignal`.

![WF](./images/wfpfolio2.png)

Accédez à **Programmes** et cliquez sur **+ Nouveau programme**. Sélectionnez **Nouveau programme**.

![WF](./images/wfnp1.png)

Saisissez le nom du programme : `--aepUserLdap-- - CitiSignal Fiber Launch`.

![WF](./images/wfp6b.png)

Dans votre programme, accédez à **Projets**. Cliquez sur **+ Nouveau projet** puis sélectionnez **Nouveau projet à partir d’un modèle**.

![WF](./images/wfp6.png)

Sélectionnez la `--aepUserLdap-- - Integrated Campaign Execution` du modèle et cliquez sur **Utiliser le modèle**.

![WF](./images/wfp6g.png)

Vous devriez alors voir ceci. Remplacez le nom par `--aepUserLdap-- - CitiSignal Fiber Launch Winter 2026` et cliquez sur **Créer un projet**.

![WF](./images/wfp6c.png)

Votre projet est maintenant créé. Accédez à **Détails du projet**.

![WF](./images/wfp6h.png)

Accédez à **Détails du projet**. Cliquez pour sélectionner le texte actif sous **Description**.

Définissez la description sur `The CitiSignal Fiber Launch project is used to plan the upcoming launch of CitiSignal Fiber.`

Cliquez sur **Enregistrer les modifications**.

![WF](./images/wfp6e.png)

Votre projet est maintenant prêt à être utilisé.

![WF](./images/wfp7.png)

Les tâches et les dépendances du projet ont été créées à partir du modèle que vous avez choisi et vous avez été défini comme . propriétaire du projet. Le statut du projet a été défini sur **Planification**. Vous pouvez modifier le statut du projet en sélectionnant une autre valeur dans la liste.

![WF](./images/wfp7z.png)

## Vue Projet 1.8.1.4 dans Frame.io

Accédez à [https://next.frame.io/](https://next.frame.io/){target="_blank"}. Connectez-vous et sélectionnez l’instance à utiliser. Dans cet exemple **Experience Platform International ESM**. Vous remarquerez qu&#39;un dossier existe déjà dans Frame.io pour le projet que vous venez de créer. Le dossier porte le nom du projet que vous avez saisi précédemment.

Il s’agit d’une fonctionnalité de la gestion du stockage d’entreprise, une solution de stockage dans le cloud qui sert de référentiel central pour les ressources des produits d’entreprise Adobe, notamment Workfront et Frame.io.

Les principaux avantages du stockage d’entreprise dans Adobe sont les suivants :

- Couche de stockage unifiée pour les ressources de création et de gestion de travail
- Autorisations centralisées via le système Adobe Identity Management (IMS) pour un contrôle d’accès sécurisé
- Visibilité complète des ressources dans Workfront et Frame.io
- Stockage évolutif et gestion des quotas pour les besoins de l&#39;entreprise

![WF](./images/fio1.png)

## 1.8.1.5 Créer une nouvelle tâche

Revenez à Workfront. Accédez à **Tâches**, placez le pointeur de la souris sur la tâche **Commencer à créer des modèles de conception** et cliquez sur le **de 3 points...**.

![WF](./images/wfp7a.png)

Sélectionnez l’option **Insérer la tâche ci-dessous**.

![WF](./images/wfp7x.png)

Saisissez le nom suivant pour votre tâche : `Create layout using approved assets and copy`.

Définissez le champ **Affectations** sur le rôle **Designer**.
Définissez le champ **Durée** sur **5 jours**.
Définissez le prédécesseur du champ sur **9**.
Saisissez une date pour les champs **Début le** et **Échéance le** (la date de début de cette tâche doit être planifiée après la date de fin de la tâche précédente).

Cliquez ailleurs dans l&#39;écran pour enregistrer la nouvelle tâche.

![WF](./images/wfp8.png)

Vous devriez alors voir ceci. Cliquez sur la tâche pour l’ouvrir.

![WF](./images/wfp9.png)

Accédez à **Détails de la tâche** et définissez le champ **Description** sur : `This task is used to track the progress of the creation of the assets for the CitiSignal Fiber Launch Campaign.`

Cliquez sur **Enregistrer les modifications**.

![WF](./images/wfp9a.png)

Vous devriez alors voir ceci. Cliquez sur le champ **Affectations** et sélectionnez **M’affecter**.

![WF](./images/wfpwlb7.png)

Cliquez sur **Enregistrer**.

![WF](./images/wfpwlb8.png)

Cliquez sur **Travailler dessus**.

![WF](./images/wfpwlb9.png)

Vous devriez alors voir ceci.

![WF](./images/wfpwlb10.png)

Dans le cadre de cette tâche, une nouvelle ressource doit être créée. À l’étape suivante, vous allez d’abord fournir des images de référence dans Workfront afin que le concepteur sache ce qui est attendu. Ensuite, vous passerez au rôle de Designer et créerez vous-même cette ressource à l’aide d’Adobe Express.

## 1.8.1.6 Charger des images de référence

Téléchargez les images de référence [ici](./assets/reference_images.zip) sur votre bureau et décompressez-les.

![WF](./images/wfrefimg1.png)

Dans Workfront, accédez au niveau **Projet**.

![WF](./images/wfrefimg2.png)

Accédez à **Documents**, cliquez sur **+ Ajouter** puis sélectionnez **Document**.

![WF](./images/wfrefimg3.png)

Accédez au dossier que vous avez téléchargé et qui contient les images de référence. Sélectionnez toutes les images et cliquez sur **Ouvrir**.

![WF](./images/wfrefimg4.png)

Au bout de quelques minutes, toutes les images seront chargées et jointes au projet.

![WF](./images/wfrefimg5.png)

Une fois les images de référence en place, le concepteur peut créer la nouvelle ressource pour cette campagne.

## Étapes suivantes

Étape suivante : [Créer une ressource, la réviser et l’approuver](./ex2.md){target="_blank"}

Revenez à [Révision et approbation unifiées avec Workfront, Frame.io et Enterprise Storage Management](./esm.md){target="_blank"}

Revenir à [Tous les modules](./../../../overview.md){target="_blank"}
