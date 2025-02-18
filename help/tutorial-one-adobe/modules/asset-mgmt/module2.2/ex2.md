---
title: Relecture avec Workfront
description: Relecture avec Workfront
kt: 5342
doc-type: tutorial
exl-id: 1b5ca13b-2a32-44a1-a3ae-342bccc6baeb
source-git-commit: dd075b0296c6ba06d72b229145635060c2c6abb1
workflow-type: tm+mt
source-wordcount: '661'
ht-degree: 0%

---

# 1.2.2 Relecture avec Workfront

## 1.2.2.1 Créer un flux d’approbation

Accédez à [https://experienceplatform.my.workfront.com/](https://experienceplatform.my.workfront.com/){target="_blank"}.

Cliquez sur l’icône des 9 points **hamburger** et sélectionnez **Vérification**.

![WF](./images/wfp1.png)

Accédez à **Workflows**, cliquez sur **+ Nouveau** puis sélectionnez **Nouveau modèle**.

![WF](./images/wfp2.png)

Définissez le **Nom du modèle** sur `--aepUserLdap-- - Approval Workflow` et définissez le **Propriétaire du modèle** sur vous-même.

![WF](./images/wfp3.png)

Faites défiler vers le bas, puis sous **Étapes** > **Étape 1**, ajoutez **Wouter Van Geluwe** avec le **Rôle** de **Réviseur et approbateur**.

Cliquez sur **Créer**.

![WF](./images/wfp4.png)

Votre workflow d’approbation de base est maintenant prêt à être utilisé.

![WF](./images/wfp5.png)

## 1.2.2.2 Créer un projet

Sur la page d’accueil de Workfront, cliquez sur **Nouveau** dans l’onglet **Mes projets**. Sélectionnez **Projet vierge**.

![WF](./images/wfp6.png)

Vous devriez alors voir ceci. Remplacez le nom par `--aepUserLdap-- - CitiSignal Fiber Launch`.

![WF](./images/wfp6a.png)

Votre projet est maintenant créé.

![WF](./images/wfp7.png)

## 1.2.2.3 Créer une nouvelle tâche

Saisissez le nom de votre tâche : **Créer des ressources pour une campagne Fibre optique**. Cliquez sur **Créer une tâche**.

![WF](./images/wfp8.png)

Vous devriez alors voir ceci.

![WF](./images/wfp9.png)

## 1.2.2.4 Ajouter un nouveau document à votre tâche via le flux d’approbation

Cliquez sur **+ Ajouter** puis sélectionnez **Document**.

![WF](./images/wfp10.png)

Téléchargez [ce fichier](./images/2048x2048.png) sur votre bureau.

![WF](./images/2048x2048.png){width="50px" align="left"}

Sélectionnez le fichier **2048x2048.png** et cliquez sur **Ouvrir**.

![WF](./images/wfp12.png)

Tu devrais avoir ça. Cliquez sur **Créer une épreuve** puis choisissez **Épreuve avancée**.

![WF](./images/wfp13.png)

Dans la fenêtre **nouveau BAT**, sélectionnez le modèle de workflow que vous avez créé précédemment et qui doit être nommé `--aepuserLdap-- - Approval Workflow`. Cliquez sur **Créer une épreuve**.

![WF](./images/wfp14.png)

Vous reprendrez alors votre tâche. Cliquez sur le bouton **Affecter à** et sélectionnez **M’affecter**.

![WF](./images/wfp15.png)

Cliquez sur **Enregistrer**.

![WF](./images/wfp16.png)

Cliquez sur **Travailler dessus**.

![WF](./images/wfp17.png)

Cliquez sur **Ouvrir l&#39;épreuve**

![WF](./images/wfp18.png)

Vous pouvez maintenant examiner le BAT. Sélectionnez **Ajouter un commentaire** pour ajouter une remarque qui nécessite la modification du document.

![WF](./images/wfp19.png)

Saisissez votre commentaire et cliquez sur **Publier**. Cliquez sur **Fermer**.

![WF](./images/wfp20.png)

Ensuite, vous devez modifier votre rôle de **Réviseur** en **Réviseur et approbateur**. Pour ce faire, revenez à votre tâche et cliquez sur **Workflow de relecture**.

![WF](./images/wfp21.png)

Remplacez votre rôle **Réviseur** par **Réviseur et approbateur**.

![WF](./images/wfp22.png)

Revenez à votre tâche et ouvrez à nouveau l’épreuve. Un nouveau bouton apparaît, **Prendre une décision**. Cliquez dessus.

![WF](./images/wfp23.png)

Sélectionnez **Modifications requises** puis cliquez sur **Prendre une décision**.

![WF](./images/wfp24.png)

Tu devrais alors être de retour ici. Vous devez maintenant charger une deuxième image qui prend en compte les commentaires qui ont été fournis.

![WF](./images/wfp25.png)

Téléchargez [ce fichier](./images/2048x2048_buynow.png) sur votre bureau.

![ce fichier](./images/2048x2048_buynow.png){width="50px" align="left"}

Dans l&#39;affichage Tâche, sélectionnez l&#39;ancien fichier image qui n&#39;a pas été approuvé. Cliquez ensuite sur **+ Ajouter nouveau**, sélectionnez **Version** puis **Document**.

![WF](./images/wfp26.png)

Sélectionnez le fichier **2048x2048_buynow.png** et cliquez sur **Ouvrir**.

![WF](./images/wfp27.png)

Tu devrais avoir ça. Cliquez sur **Créer une épreuve** puis sélectionnez à nouveau **Épreuve avancée**.

![WF](./images/wfp28.png)

Tu verras ça. Le **modèle de workflow** est maintenant présélectionné, car Workfront suppose que le workflow d’approbation précédent est toujours valide. Cliquez sur **Créer une épreuve**.

![WF](./images/wfp29.png)

Sélectionnez **Ouvrir l’épreuve**.

![WF](./images/wfp30.png)

Vous pouvez maintenant voir 2 versions du fichier l’une à côté de l’autre.

![WF](./images/wfp31.png)

Cliquez sur **Prendre une décision**, sélectionnez **Approuvé** et cliquez de nouveau sur **Prendre une décision**.

![WF](./images/wfp32.png)

Fermez l&#39;aperçu de l&#39;épreuve.

![WF](./images/wfp33.png)

Vous serez alors de retour dans la vue Tâche avec une ressource approuvée. Cette ressource doit maintenant être partagée vers AEM Assets.

![WF](./images/wfp34.png)

Cliquez sur l’icône **flèche de partage** et sélectionnez votre intégration AEM Assets, qui doit être nommée `--aepUserLdap-- - Citi Signal AEM`.

![WF](./images/wfp35.png)

Double-cliquez sur le dossier que vous avez créé précédemment et qui doit être nommé `--aepUserLdap-- - Workfront Assets`.

![WF](./images/wfp36.png)

Cliquez sur **Sélectionner un dossier**.

![WF](./images/wfp37.png)

Au bout de 1 à 2 minutes, votre document sera désormais publié dans AEM Assets. Une icône AEM apparaît en regard du nom du document.

![WF](./images/wfp37a.png)

Cliquez sur **Ouvrir le résumé**.

![WF](./images/wfp38.png)

Accédez à **Métadonnées**, vous devriez voir ceci :

![WF](./images/wfp39.png)

Accédez à **Aperçu** et cliquez sur **+ Ajouter** pour ajouter une description.

![WF](./images/wfp40.png)

Saisissez votre description. Les paramètres de votre épreuve et de votre document sont maintenant définis.

![WF](./images/wfp41.png)

## 1.2.2.5 Afficher votre fichier dans AEM Assets

Accédez à votre dossier dans AEM Assets, qui s’appelle `--aepUserLdap-- - Workfront Assets`.

![WF](./images/wfppaem1.png)

Cliquez sur les 3 points de votre image, puis sélectionnez **Détails**.

![WF](./images/wfppaem2.png)

Vous verrez ensuite le formulaire de métadonnées que vous avez créé précédemment, avec les valeurs qui ont été renseignées automatiquement par l’intégration entre Workfront et AEM Assets.

![WF](./images/wfppaem3.png)

Revenir à [Gestion des workflows avec Adobe Workfront](./workfront.md){target="_blank"}

[Revenir à tous les modules](./../../../overview.md){target="_blank"}
