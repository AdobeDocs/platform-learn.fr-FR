---
title: Prise en main de Firefly Creative Production for Enterprise
description: Prise en main de Firefly Creative Production for Enterprise
role: Developer
level: Beginner
jira: KT-5342
doc-type: Tutorial
exl-id: 7d9ad7ec-7744-4ba6-9c11-c434e6cdef09
source-git-commit: 7850713bf116c8a9aa9dc4e055d0e501aa783cb0
workflow-type: tm+mt
source-wordcount: '1356'
ht-degree: 1%

---

# 1.7.1 Prise en main de Firefly Creative Production for Enterprise

Accédez à [](https://firefly.adobe.com). Cliquez sur l’icône de profil dans le coin supérieur droit et vérifiez que vous avez sélectionné l’instance appropriée, qui doit être `--aepImsOrgName--`.

Accédez à **Production**.

![](./images/ffcw1.png)

Vous devriez alors voir ceci. Cliquez sur **Créer un workflow (version bêta)**.

![](./images/ffcw2.png)

## 1.7.1.1 Supprimer l’arrière-plan

Pour découvrir Firefly Creative Production for Enterprise, vous allez maintenant mettre en œuvre un cas d’utilisation de base axé sur la suppression de l’arrière-plan d’une image spécifique.

Remplacez le nom de votre workflow par `vangeluw - remove background`.

![](./images/ffcw3.png)

Ouvrez l’**Image**

![](./images/ffcw4.png)

Sélectionnez **Supprimer l’arrière-plan**, puis faites glisser et déposez ce nœud sur la zone de travail.

Vous devez maintenant connecter un nœud d’image d’entrée et un nœud d’image de sortie au **Supprimer l’arrière-plan**.

![](./images/ffcw5.png)

Faites défiler vers le haut et accédez à **Entrée et Sortie**. Cliquez sur le nœud **Images d’entrée** et faites-le glisser sur la zone de travail.

![](./images/ffcw6.png)

Tu devrais avoir ça. Connectez le nœud **Images d’entrée** au nœud **Supprimer l’arrière-plan** en pointant sur le point bleu en regard de **Image** sur le nœud **Images d’entrée** et en dessinant une ligne sur le point bleu en regard de **Image d’entrée** sur le nœud **Supprimer l’arrière-plan**.

![](./images/ffcw7.png)

Tu devrais avoir ça. Cliquez ensuite sur le nœud **Images de sortie** et faites-le glisser sur la zone de travail.

![](./images/ffcw8.png)

Tu devrais avoir ça. Connectez le nœud **Supprimer l’arrière-plan** au nœud **Images de sortie** en pointant sur le point bleu en regard de **Image de sortie** sur le nœud **Supprimer l’arrière-plan** et en dessinant une ligne sur le point bleu en regard de **Image** sur le nœud **Images de sortie**.

![](./images/ffcw9.png)

Tu devrais avoir ça.

![](./images/ffcw10.png)

Votre workflow de base est maintenant prêt à être testé. Téléchargez l’image [phone.png](./assets/phone.png) sur votre bureau.

![](./images/ffcw11.png)

Revenez à votre workflow. Cliquez sur la zone **Glisser-déposer** du nœud **Images d’entrée**.

![](./images/ffcw11a.png)

Sélectionnez le fichier **phone.png**. Cliquez sur **Ouvrir**.

![](./images/ffcw12.png)

Vous devriez alors voir ceci. Cliquez sur **Exécuter**.

![](./images/ffcw13.png)

Après 1 à 2 minutes, vous devriez voir ce résultat.

![](./images/ffcw14.png)

## 1.7.1.2 Supprimer l’arrière-plan + Recadrer

Vous devez maintenant ajouter un nœud **Crop** à la zone de travail. Dans le menu, accédez à **Image** et faites défiler l’écran vers le bas pour trouver **Recadrer**. Faites-le glisser sur la zone de travail.

![](./images/ffcw15.png)

Placez le nœud **Crop** entre le nœud **Remove Background** et le nœud **Output Image**.

Vous devez maintenant supprimer la connexion entre le nœud **Remove Background** et le nœud **Output Image**. Pour ce faire, double-cliquez sur la ligne entre les deux nœuds.

![](./images/ffcw16.png)

Tu devrais avoir ça. Connectez le nœud **Supprimer l’arrière-plan** au nœud **Recadrer**, puis connectez le nœud **Recadrer** au nœud **Image de sortie**.

![](./images/ffcw17.png)

Cochez la case **Recadrage automatique**, puis vous pouvez tester votre workflow en cliquant sur **Exécuter**.

![](./images/ffcw18.png)

Après 1 à 2 minutes, vous devriez voir ceci, qui montre une image avec une résolution différente maintenant.

![](./images/ffcw19.png)

## 1.7.1.3 Supprimer l’arrière-plan + Recadrer + Image composite

Dans le menu, sous **Image** sélectionnez un nœud **Images composites (2D)** et faites-le glisser sur la zone de travail.

![](./images/ffcw20.png)

Ajoutez une seconde connexion au nœud **Recadrer** en connectant le point bleu en regard de **Image recadrée** au point bleu en regard de **Image d’entrée** sur le nœud **Images composites (2D)**.

![](./images/ffcw21.png)

Dans le menu, sous **Entrée et sortie**, sélectionnez un nœud **Texte d’entrée** et faites-le glisser sur la zone de travail.

Connectez le point vert en regard de **Texte** sur le nœud **Texte d’entrée** au point vert en regard de **Invite** sur le nœud **Images composites (2D)**.

![](./images/ffcw22.png)

Tu devrais avoir ça. Saisissez l’invite ci-dessous dans le nœud **Texte de saisie**.

`magazine quality photo of a phone on a red pedestal with a pink background surrounded by origami style pink paper hearts`

Dans le menu, sous **Entrée et sortie**, sélectionnez un nœud **Images de sortie** et faites-le glisser sur la zone de travail.

Connectez le point bleu en regard de **Image composite** sur le nœud **Images composites (2D)** au point bleu en regard de **Image d’entrée** sur le nœud **Image de sortie**.

Cliquez sur **Exécuter**.

![](./images/ffcw23.png)

Après quelques minutes, vous devriez voir quelque chose comme ceci, qui montre votre image d’origine dans une composition basée sur l’invite fournie, dans une résolution spécifique.

![](./images/ffcw24.png)

## 1.7.1.4 Supprimer l’arrière-plan + Recadrer + Image composite + Générer la vidéo

Dans le menu, accédez à **Vidéo**. Sélectionnez le nœud **Générer la vidéo** et faites-le glisser sur la zone de travail.

Connectez le point bleu en regard de **Image composite** du nœud **Images composites (2D)** au point bleu en regard de **Image d’entrée** du nœud **Générer une vidéo**.

![](./images/ffcw25.png)

Dans le menu, accédez à **Entrée et sortie**. Sélectionnez le nœud **Texte d’entrée** et faites-le glisser sur la zone de travail.

Connectez le point vert en regard de **Texte** sur le nœud **Texte d’entrée** au point vert en regard de **Invite** du nœud **Générer une vidéo**.

Saisissez le `background hearts fluttering` d’invite dans le nœud **Texte de saisie**.

Dans le menu, accédez à **Entrée et sortie**. Sélectionnez le nœud **Vidéo de sortie** et faites-le glisser sur la zone de travail.

Connectez le point violet en regard de **Sortie vidéo** du nœud **Générer la vidéo** au point violet en regard de **Vidéo** sur le nœud **Vidéo de sortie**.

Cliquez sur **Exécuter**.

![](./images/ffcw26.png)

Après quelques vidéos, vous devriez voir ceci qui montre une vidéo basée sur la combinaison de l’image fournie et de l’invite.

![](./images/ffcw27.png)

## Échelle de 1.7.1.5

Vous l’avez maintenant fait pour 1 image. Utilisons maintenant ce workflow, mais pour plusieurs images.

Téléchargez ces images sur votre bureau :

- [watch.jpg](./assets/watch.jpg)
- [airpods.jpg](./assets/airpods.jpg)

![](./images/ffcw28.png)

Dans votre workflow, revenez au premier nœud, **Images d’entrée**. Supprimez l’image actuellement sélectionnée.

![](./images/ffcw29.png)

Cliquez sur la zone **Glisser-déposer**.

![](./images/ffcw30.png)

Sélectionnez les 3 images que vous avez téléchargées. Cliquez sur **Ouvrir**.

![](./images/ffcw31.png)

Vous devriez alors voir ceci. cliquez sur **Exécuter**.

![](./images/ffcw32.png)

Au bout de quelques minutes, vous devriez voir une sortie similaire, avec 3 images générées et 3 vidéos.

![](./images/ffcw33.png)

## 1.7.1.5 Store dans AEM Assets CS

Dans cet exercice, vous allez stocker les ressources créées dans le cadre de votre workflow personnalisé dans AEM Assets CS.

Vous devez d’abord créer un dossier dans votre environnement AEM Assets CS.

Pour ce faire, accédez à [](https://experience.adobe.com?lang=fr). Cliquez pour ouvrir ****.

![](./images/ffcw50.png)

Sélectionnez votre environnement AEM Assets CS, qui doit être nommé `--aepUserLdap-- - CitiSignal AEM + ACCS`.

![](./images/ffcw51.png)

Accédez à **** puis cliquez sur **Créer un dossier**.

![](./images/ffcw52.png)

Saisissez le nom : `--aepUserLdap-- - Firefly Creative Production for Enterprise`. Cliquez sur **Créer**.

![](./images/ffcw53.png)

Revenez à votre workflow personnalisé et accédez au nœud **Images de sortie**. Cliquez sur **Par défaut** puis sélectionnez **AEM Assets**.

![](./images/ffcw57.png)

Vous devriez alors voir cette fenêtre contextuelle. Sélectionnez votre référentiel AEM Assets CS, puis sélectionnez le dossier que vous venez de créer et qui doit être nommé : `--aepUserLdap-- - Firefly Creative Production for Enterprise`. Cliquez sur **Sélectionner**.

![](./images/ffcw54.png)

Accédez au nœud **Vidéo de sortie**. Cliquez sur **Par défaut** puis sélectionnez **AEM Assets**.

![](./images/ffcw55.png)

Vous devriez alors voir cette fenêtre contextuelle. Sélectionnez votre référentiel AEM Assets CS, puis sélectionnez le dossier que vous venez de créer et qui doit être nommé : `--aepUserLdap-- - Firefly Creative Production for Enterprise`. Cliquez sur **Sélectionner**.

![](./images/ffcw56.png)

Tu devrais avoir ça. Cliquez sur **Exécuter**.

![](./images/ffcw56a.png)

Au bout de quelques minutes, vous devriez voir les ressources créées devenir disponibles dans le dossier dans AEM Assets CS.

![](./images/ffcw58.png)

Revenez à votre workflow. Cliquez sur **Publier**.

![](./images/ffcw59.png)

Vous devriez alors voir ceci.

![](./images/ffcw60.png)

Votre workflow est maintenant publié et peut être exécuté par programmation dans le cadre de l’exercice suivant.

## Étapes suivantes

Accédez à [1.7.2 Exécuter votre workflow personnalisé par programmation](./ex2.md){target="_blank"}

Revenir à [](./workflowbuilder.md){target="_blank"}

Revenir à [Tous les modules](./../../../overview.md){target="_blank"}
