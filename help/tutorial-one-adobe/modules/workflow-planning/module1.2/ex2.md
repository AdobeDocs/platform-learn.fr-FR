---
title: Relecture avec Workfront
description: Relecture avec Workfront
kt: 5342
doc-type: tutorial
exl-id: 5feb9486-bdb4-4d59-941c-09fc2e38163b
source-git-commit: a63c01ebe81df39569981d62b85d0461119ecf66
workflow-type: tm+mt
source-wordcount: '1613'
ht-degree: 0%

---

# 1.2.2 Relecture avec Workfront

>[!IMPORTANT]
>
>Si vous avez précédemment configuré un programme AEM CS avec un environnement AEM Assets CS, il se peut que votre sandbox AEM CS ait été mis en veille. Étant donné que la réactivation d’un tel sandbox prend entre 10 et 15 minutes, il serait judicieux de lancer le processus de réactivation maintenant afin de ne pas avoir à l’attendre plus tard.

## 1.2.2.1 Créer un flux d’approbation

Revenez à **Adobe Workfront**. Cliquez sur l&#39;icône **menu** et sélectionnez **Vérification**.

![WF](./images/wfp1.png)

Accédez à **Workflows**, cliquez sur **+ Nouveau** puis sélectionnez **Nouveau modèle**.

![WF](./images/wfp2.png)

Définissez le **Nom du modèle** sur `--aepUserLdap-- - Approval Workflow` et définissez le **Propriétaire du modèle** sur vous-même.

![WF](./images/wfp3.png)

Faites défiler vers le bas, puis sous **Étapes** > **Étape 1**, remplacez le rôle **Créateur d’épreuve** par **Réviseur et approbateur**. Vous pouvez également ajouter n’importe qui d’autre. Par exemple, ajoutez-vous en sélectionnant votre utilisateur et en définissant le **Rôle** de **Réviseur et approbateur**.

Cliquez sur **Créer**.

![WF](./images/wfp4.png)

Votre workflow d’approbation de base est maintenant prêt à être utilisé.

![WF](./images/wfp5.png)

## 1.2.2.2 Activer le plan directeur Workfront

À l’étape suivante, vous allez créer un projet à l’aide d’un modèle. Adobe Workfront vous fournit un certain nombre de plans directeurs disponibles qui doivent simplement être activés.

Pour le cas d&#39;utilisation de CitiSignal, le plan directeur **Exécution de campagne intégrée** est celui que vous devez utiliser.

Pour installer ce plan directeur, ouvrez le menu et sélectionnez **Plans directeurs**.

![WF](./images/blueprint1.png)

Sélectionnez le filtre **Marketing** puis faites défiler l’écran vers le bas pour trouver le plan directeur **Exécution de campagne intégrée**. Cliquez sur **Installer**.

![WF](./images/blueprint2.png)

Cliquez sur **Continuer**.

![WF](./images/blueprint3.png)

Cliquez sur **Installer en l’état...**.

![WF](./images/blueprint4.png)

Vous devriez alors voir ceci. L’installation peut prendre quelques minutes.

![WF](./images/blueprint5.png)

Après quelques minutes, le plan directeur sera installé.

![WF](./images/blueprint6.png)

## 1.2.2.3 Créer un projet

Ouvrez le **menu** et accédez à **Programmes**.

![WF](./images/wfp6a.png)

Cliquez sur le programme que vous avez créé précédemment et qui s’appelle `--aepUserLdap-- CitiSignal Fiber Launch`.

>[!NOTE]
>
>Vous avez créé un programme dans le cadre de l&#39;exercice sur [Workfront Planning](./../module1.1/ex1.md) avec l&#39;automatisation que vous avez créée et exécutée. Si vous ne l&#39;avez pas encore fait, vous pouvez trouver les instructions ici.

![WF](./images/wfp6b.png)

Dans votre programme, accédez à **Projets**. Cliquez sur **+ Nouveau projet** puis sélectionnez **Nouveau projet à partir d’un modèle**.

![WF](./images/wfp6.png)

Sélectionnez le modèle **Exécution de campagne intégrée** et cliquez sur **Utiliser le modèle**.

![WF](./images/wfp6g.png)

Vous devriez alors voir ceci. Remplacez le nom par `--aepUserLdap-- - CitiSignal Fiber Launch Winter 2026` et cliquez sur **Créer un projet**.

![WF](./images/wfp6c.png)

Votre projet est maintenant créé. Accédez à **Détails du projet**.

![WF](./images/wfp6h.png)

Accédez à **Détails du projet**. Cliquez pour sélectionner le texte actif sous **Description**.

![WF](./images/wfp6d.png)

Définissez la description sur `The CitiSignal Fiber Launch project is used to plan the upcoming launch of CitiSignal Fiber.`

Cliquez sur **Enregistrer les modifications**.

![WF](./images/wfp6e.png)

Votre projet est maintenant prêt à être utilisé.

![WF](./images/wfp7.png)

Les tâches et les dépendances du projet ont été créées à partir du modèle que vous avez choisi et vous avez été défini comme . propriétaire du projet. Le statut du projet a été défini sur **Planification**. Vous pouvez modifier le statut du projet en sélectionnant une autre valeur dans la liste.

![WF](./images/wfp7z.png)

## 1.2.2.4 Créer une nouvelle tâche

Pointez sur la tâche **Commencer à créer des modèles de conception** et cliquez sur le **de 3 points...**.

![WF](./images/wfp7a.png)

Sélectionnez l’option **Insérer la tâche ci-dessous**.

![WF](./images/wfp7x.png)

Saisissez le nom suivant pour votre tâche : `Create layout using approved assets and copy`.

Définissez le champ **Affectations** sur le rôle **Designer**.
Définissez le champ **Durée** sur **5 jours**.
Définissez le prédécesseur du champ sur **9**.
Saisissez une date pour les champs **Début le** et **Échéance le**.

Cliquez ailleurs dans l&#39;écran pour enregistrer la nouvelle tâche.

![WF](./images/wfp8.png)

Vous devriez alors voir ceci. Cliquez sur la tâche pour l’ouvrir.

![WF](./images/wfp9.png)

Accédez à **Détails de la tâche** et définissez le champ **Description** sur : `This task is used to track the progress of the creation of the assets for the CitiSignal Fiber Launch Campaign.`

Cliquez sur **Enregistrer les modifications**.

![WF](./images/wfp9a.png)

Vous devriez alors voir ceci. Cliquez sur le champ **Projet** pour revenir à votre projet.

![WF](./images/wfp9b.png)

Dans la vue **Projet**, accédez à **Équilibreur de charge de travail**.

![WF](./images/wfpwlb1.png)

Cliquez sur **Affectations en bloc**.

![WF](./images/wfpwlb2.png)

Sélectionnez le **Affectation de rôle** de **Designer** puis cliquez dans le champ **Utilisateur à affecter**. Tous les utilisateurs disposant d&#39;un rôle **Designer** dans votre instance Workfront s&#39;affichent. Dans ce cas, sélectionnez l’utilisatrice fictive **Melissa Jenkins**.

![WF](./images/wfpwlb3.png)

Cliquez sur **Attribuer**. L&#39;utilisateur que vous avez sélectionné sera désormais affecté aux tâches du projet liées au rôle **Designer**.

![WF](./images/wfpwlb4.png)

Les tâches sont maintenant affectées. Cliquez sur **Tâches** pour revenir à la page **Tâches** Aperçu.

![WF](./images/wfpwlb5.png)

Cliquez sur la tâche que vous avez créée, qui est nommée
**Créer une disposition à l’aide de ressources approuvées et de la copie**.

![WF](./images/wfpwlb6.png)

Vous allez maintenant commencer à travailler sur cette tâche dans le cadre de cet exercice. Vous pouvez voir que Melissa Jenkins est affectée à cette tâche pour le moment. Pour le modifier vous-même, cliquez sur le champ **Affectations** et sélectionnez **M’affecter**.

![WF](./images/wfpwlb7.png)

Cliquez sur **Enregistrer**.

![WF](./images/wfpwlb8.png)

Cliquez sur **Travailler dessus**.

![WF](./images/wfpwlb9.png)

Vous devriez alors voir ceci.

![WF](./images/wfpwlb10.png)

Dans le cadre de cette tâche, vous devez créer une nouvelle image, puis la charger sous forme de document dans Workfront. Vous allez à présent créer cette ressource vous-même à l’aide d’Adobe Express.

## 1.2.2.5 Créer une ressource avec Adobe Firely Services et Adobe Express

Accédez à [https://firefly.adobe.com/](https://firefly.adobe.com/){target="_blank"}. Saisissez le `a neon rabbit running very fast through space` d’invite et cliquez sur **Générer**.

![GSPeM](./images/gsasset1.png)

Plusieurs images sont alors générées. Choisissez l’image qui vous plaît le plus, cliquez sur l’icône **Partager** sur l’image, puis sélectionnez **Ouvrir dans Adobe Express**.

![GSPeM](./images/gsasset2.png)

L’image que vous venez de générer est alors disponible pour modification dans Adobe Express. Vous devez maintenant ajouter le logo CitiSignal sur l&#39;image. Pour ce faire, accédez à **Marques**.

![GSPeM](./images/gsasset3.png)

Vous devriez alors voir un modèle de marque CitiSignal. qui a été créé dans GenStudio for Performance Marketing s’affichent dans Adobe Express. Cliquez pour sélectionner un modèle de marque dont le nom contient `CitiSignal`.

![GSPeM](./images/gsasset4.png)

Accédez à **Logos** et cliquez sur le logo **blanc** Citisignal pour le déposer sur l’image.

![GSPeM](./images/gsasset5.png)

Positionnez le logo CitiSignal en haut de votre image, pas trop loin du milieu.

![GSPeM](./images/gsasset6.png)

Accédez à **Texte**.

![GSPeM](./images/gsasset6a.png)

Cliquez sur **Ajouter votre texte**.

![GSPeM](./images/gsasset6b.png)

Saisissez la `Timetravel now!` de texte, modifiez la couleur et la taille de la police, définissez le texte en **Gras** afin d’obtenir une image similaire à celle-ci.

![GSPeM](./images/gsasset6c.png)

Cliquez ensuite sur **Partager**.

![GSPeM](./images/gsasset7.png)

Sélectionnez **AEM Assets**.

![GSPeM](./images/gsasset8.png)

Remplacez le nom du fichier par `CitiSignal - Neon Rabbit - Timetravel now!`.
Cliquez sur **Sélectionner un dossier**.

![GSPeM](./images/gsasset9.png)

Sélectionnez votre référentiel CS AEM Assets, qui doit être nommé `--aepUserLdap-- - CitiSignal`, puis sélectionnez le dossier `--aepUserLdap-- - CitiSignal Fiber Campaign`. Cliquez sur **Sélectionner**.

![GSPeM](./images/gsasset11.png)

Vous devriez alors voir ceci. Cliquez sur **Charger 1 ressource**. Votre image sera maintenant téléchargée sur AEM Assets CS.

![GSPeM](./images/gsasset12.png)

## 1.2.2.6 Ajouter un nouveau document à votre tâche et lancer le flux d’approbation

Revenez à l’écran **Détails de la tâche**. Accédez à **Documents**. Cliquez sur **+ Ajouter nouveau** puis sélectionnez votre référentiel CS AEM Assets, qui doit être nommé `--aepUserLdap-- - CitiSignal`.

![WF](./images/wfp10.png)

Double-cliquez pour ouvrir la `--aepUserLdap-- CitiSignal Fiber Campaign` du dossier.

![WF](./images/wfp10a.png)

Sélectionnez le fichier que vous avez créé à l’étape précédente, qui s’appelle **CitiSignal - Neon rabbit - Timetravel Now !.png**. Cliquez sur **Sélectionner**.

![WF](./images/2048x2048.png){width="50px" align="left"}

Tu devrais avoir ça. Pointez sur le document chargé. Cliquez sur **Créer une épreuve** puis choisissez **Épreuve avancée**.

![WF](./images/wfp13.png)

Dans la fenêtre **nouveau BAT**, sélectionnez **Automatisé** puis sélectionnez le modèle de workflow que vous avez créé précédemment et qui doit être nommé `--aepUserLdap-- - Approval Workflow`. Cliquez sur **Créer une épreuve**.

![WF](./images/wfp14.png)

Cliquez sur **Ouvrir l&#39;épreuve**

![WF](./images/wfp18.png)

Vous pouvez maintenant examiner le BAT. Sélectionnez **Ajouter un commentaire** pour ajouter une remarque qui nécessite la modification du document.

![WF](./images/wfp19.png)

Saisissez votre commentaire et cliquez sur **Publier**. Cliquez ensuite sur **Prendre une décision**.

![WF](./images/wfp20.png)

Sélectionnez **Modifications requises** puis cliquez sur **Prendre une décision**.

![WF](./images/wfp24.png)

Revenez à votre **Tâche** et au **Document**. Le texte **Modifications requises** apparaît également à cet endroit.

![WF](./images/wfp25.png)

Vous devez maintenant apporter des modifications à la conception, ce que vous ferez dans Adobe Express.

## 1.2.2.7 Apporter des modifications de conception dans Adobe Express

Accédez à [https://new.express.adobe.com/your-stuff/files](https://new.express.adobe.com/your-stuff/files) puis ouvrez à nouveau l’image que vous avez créée précédemment.

![WF](./images/wfp25a.png)

Remplacez le texte CTA par `Get On Board Now!`.

![WF](./images/wfp25b.png)

Cliquez sur **Partager** puis sélectionnez **AEM Assets**.

![WF](./images/wfp25c.png)

Saisissez le nom `CitiSignal - Neon Rabbit - Get On Board Now!`, puis cliquez sur **Sélectionner un dossier** pour sélectionner un dossier de destination.

![WF](./images/wfp25d.png)

Sélectionnez votre référentiel CS AEM Assets, qui doit être nommé `--aepUserLdap-- - CitiSignal`, puis sélectionnez le dossier `--aepUserLdap-- - CitiSignal Fiber Campaign`. Cliquez sur **Sélectionner**.

![WF](./images/wfp25e.png)

Cliquez sur **charger 1 ressource**.

![WF](./images/wfp25f.png)

Votre nouvelle ressource est maintenant créée et stockée dans AEM Assets.

## 1.2.2.8 Ajouter une nouvelle version de votre document à votre tâche

Dans l’affichage Tâche d’Adobe Workfront, sélectionnez l’ancien fichier image qui n’a pas été approuvé. Cliquez ensuite sur **+ Ajouter nouveau**, sélectionnez **Version**, puis sélectionnez votre référentiel CS AEM Assets, qui doit être nommé `--aepUserLdap-- - CitiSignal`.

![WF](./images/wfp26.png)

Accédez au `--aepUserLdap-- CitiSignal Fiber Campaign` du dossier et sélectionnez le `CitiSignal - Neon Rabit - Get On Board Now!.png` du fichier. Cliquez sur **Sélectionner**.

![WF](./images/wfp26a.png)

Tu devrais avoir ça. Cliquez sur **Créer une épreuve** puis sélectionnez à nouveau **Épreuve avancée**.

![WF](./images/wfp28.png)

Tu verras ça. Le **modèle de workflow** est maintenant présélectionné, car Workfront suppose que le workflow d’approbation précédent est toujours valide. Cliquez sur **Créer une épreuve**.

![WF](./images/wfp29.png)

Sélectionnez **Ouvrir l’épreuve**.

![WF](./images/wfp30.png)

Vous pouvez maintenant voir 2 versions du fichier l’une à côté de l’autre. Cliquez sur le bouton **Comparer des BAT**.

![WF](./images/wfp31.png)

Vous devriez alors voir les deux versions de l’image l’une à côté de l’autre. Cliquez sur **Prendre une décision**.

![WF](./images/wfp32.png)

Sélectionnez **Approuvé** et cliquez de nouveau sur **Prendre une décision**.

![WF](./images/wfp32a.png)

Fermez la vue **Comparer les épreuves** en fermant la version gauche de l’image. Cliquez sur le **Nom de la tâche** pour revenir à l’aperçu de la tâche.

![WF](./images/wfp33.png)

Vous serez alors de retour dans la vue Tâche avec une ressource approuvée. Cette ressource doit maintenant être partagée vers AEM Assets.

![WF](./images/wfp34.png)

Sélectionnez le document approuvé. Cliquez sur l’icône **flèche de partage** et sélectionnez votre intégration AEM Assets, qui doit être nommée `--aepUserLdap-- - CitiSignal AEM`.

![WF](./images/wfp35.png)

Double-cliquez sur le dossier que vous avez créé précédemment et qui doit être nommé `--aepUserLdap-- - CitiSignal Fiber Launch Assets`.

![WF](./images/wfp36.png)

Cliquez sur **Sélectionner un dossier**.

![WF](./images/wfp37.png)

Au bout de 1 à 2 minutes, votre document sera désormais publié dans AEM Assets. Une icône AEM apparaît en regard du nom du document.

![WF](./images/wfp37a.png)

Cliquez sur **Marquer comme terminé** pour terminer cette tâche.

![WF](./images/wfp37b.png)

Vous devriez alors voir ceci.

![WF](./images/wfp37c.png)

## 1.2.2.9 Afficher votre fichier dans AEM Assets

Accédez à votre dossier dans AEM Assets CS, qui est nommé `--aepUserLdap-- - CitiSignal Fiber Launch Assets`.

![WF](./images/wfppaem1.png)

Sélectionnez l’image, puis choisissez **Détails**.

![WF](./images/wfppaem2.png)

Vous verrez ensuite le formulaire de métadonnées que vous avez créé précédemment, avec les valeurs qui ont été renseignées automatiquement par l’intégration entre Workfront et AEM Assets.

![WF](./images/wfppaem3.png)

Revenir à [Gestion des workflows avec Adobe Workfront](./workfront.md){target="_blank"}

[Revenir à tous les modules](./../../../overview.md){target="_blank"}
