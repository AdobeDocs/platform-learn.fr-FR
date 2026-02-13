---
title: Prise en main des workflows personnalisés Firefly
description: Prise en main des workflows personnalisés Firefly
role: Developer
level: Beginner
jira: KT-5342
doc-type: Tutorial
exl-id: 7d9ad7ec-7744-4ba6-9c11-c434e6cdef09
source-git-commit: 4ddfc850f335ad773c89c10e18bb3541e514bf5f
workflow-type: tm+mt
source-wordcount: '1333'
ht-degree: 4%

---

# 1.7.1 Prise en main des workflows personnalisés Firefly

[!BADGE Beta]

+++Détails Beta
En utilisant le Adobe Marketing Agent avec Microsoft 365 Copilot Beta, vous reconnaissez que le Beta est fourni « en l’état », sans garantie d’aucune sorte. Adobe n’a aucune obligation de tenir à jour, corriger, mettre à jour, modifier, remplacer ou prendre en charge Beta. Il est recommandé de faire preuve de prudence et de ne pas se fier, de quelque manière que ce soit, au bon fonctionnement ou aux performances de ce Beta et/ou des éléments qui l’accompagnent. Le Beta est considéré comme des informations confidentielles d’Adobe.  Tout « commentaire » (informations relatives à la version Beta, y compris, mais sans s’y limiter, les problèmes ou défauts que vous rencontrez lors de son utilisation, les suggestions, les améliorations et les recommandations) que vous fournissez à Adobe est par la présente cédé à Adobe. Cela inclut tous les droits, titres et intérêts relatifs à ce commentaire.

+++

Accédez à [https://firefly.adobe.com](https://firefly.adobe.com). Cliquez sur l’icône de profil dans le coin supérieur droit et vérifiez que vous avez sélectionné l’instance appropriée, qui doit être `--aepImsOrgName--`.

Accédez à **Production**.

![Workflows personnalisés Firefly](./images/ffcw1.png)

Vous devriez alors voir ceci. Cliquez sur **Créer un workflow (version bêta)**.

![Workflows personnalisés Firefly](./images/ffcw2.png)

## 1.7.1.1 Supprimer l’arrière-plan

Pour découvrir les workflows personnalisés de Firefly, vous allez maintenant implémenter un cas d’utilisation de base axé sur la suppression de l’arrière-plan d’une image spécifique.

Remplacez le nom de votre workflow par `vangeluw - remove background`.

![Workflows personnalisés Firefly](./images/ffcw3.png)

Ouvrez l’**Image**

![Workflows personnalisés Firefly](./images/ffcw4.png)

Sélectionnez **Supprimer l’arrière-plan**, puis faites glisser et déposez ce nœud sur la zone de travail.

Vous devez maintenant connecter un nœud d’image d’entrée et un nœud d’image de sortie au **Supprimer l’arrière-plan**.

![Workflows personnalisés Firefly](./images/ffcw5.png)

Faites défiler vers le haut et accédez à **Entrée et Sortie**. Cliquez sur le nœud **Images d’entrée** et faites-le glisser sur la zone de travail.

![Workflows personnalisés Firefly](./images/ffcw6.png)

Tu devrais avoir ça. Connectez le nœud **Images d’entrée** au nœud **Supprimer l’arrière-plan** en pointant sur le point bleu en regard de **Image** sur le nœud **Images d’entrée** et en dessinant une ligne sur le point bleu en regard de **Image d’entrée** sur le nœud **Supprimer l’arrière-plan**.

![Workflows personnalisés Firefly](./images/ffcw7.png)

Tu devrais avoir ça. Cliquez ensuite sur le nœud **Images de sortie** et faites-le glisser sur la zone de travail.

![Workflows personnalisés Firefly](./images/ffcw8.png)

Tu devrais avoir ça. Connectez le nœud **Supprimer l’arrière-plan** au nœud **Images de sortie** en pointant sur le point bleu en regard de **Image de sortie** sur le nœud **Supprimer l’arrière-plan** et en dessinant une ligne sur le point bleu en regard de **Image** sur le nœud **Images de sortie**.

![Workflows personnalisés Firefly](./images/ffcw9.png)

Tu devrais avoir ça.

![Workflows personnalisés Firefly](./images/ffcw10.png)

Votre workflow de base est maintenant prêt à être testé. Téléchargez l’image [phone.png](./assets/phone.png) sur votre bureau.

![Workflows personnalisés Firefly](./images/ffcw11.png)

Revenez à votre workflow. Cliquez sur la zone **Glisser-déposer** du nœud **Images d’entrée**.

![Workflows personnalisés Firefly](./images/ffcw11a.png)

Sélectionnez le fichier **phone.png**. Cliquez sur **Ouvrir**.

![Workflows personnalisés Firefly](./images/ffcw12.png)

Vous devriez alors voir ceci. Cliquez sur **Exécuter**.

![Workflows personnalisés Firefly](./images/ffcw13.png)

Après 1 à 2 minutes, vous devriez voir ce résultat.

![Workflows personnalisés Firefly](./images/ffcw14.png)

## 1.7.1.2 Supprimer l’arrière-plan + Recadrer

Vous devez maintenant ajouter un nœud **Crop** à la zone de travail. Dans le menu, accédez à **Image** et faites défiler l’écran vers le bas pour trouver **Recadrer**. Faites-le glisser sur la zone de travail.

![Workflows personnalisés Firefly](./images/ffcw15.png)

Placez le nœud **Crop** entre le nœud **Remove Background** et le nœud **Output Image**.

Vous devez maintenant supprimer la connexion entre le nœud **Remove Background** et le nœud **Output Image**. Pour ce faire, double-cliquez sur la ligne entre les deux nœuds.

![Workflows personnalisés Firefly](./images/ffcw16.png)

Tu devrais avoir ça. Connectez le nœud **Supprimer l’arrière-plan** au nœud **Recadrer**, puis connectez le nœud **Recadrer** au nœud **Image de sortie**.

![Workflows personnalisés Firefly](./images/ffcw17.png)

Cochez la case **Recadrage automatique**, puis vous pouvez tester votre workflow en cliquant sur **Exécuter**.

![Workflows personnalisés Firefly](./images/ffcw18.png)

Après 1 à 2 minutes, vous devriez voir ceci, qui montre une image avec une résolution différente maintenant.

![Workflows personnalisés Firefly](./images/ffcw19.png)

## 1.7.1.3 Supprimer l’arrière-plan + Recadrer + Image composite

Dans le menu, sous **Image** sélectionnez un nœud **Images composites (2D)** et faites-le glisser sur la zone de travail.

![Workflows personnalisés Firefly](./images/ffcw20.png)

Ajoutez une seconde connexion au nœud **Recadrer** en connectant le point bleu en regard de **Image recadrée** au point bleu en regard de **Image d’entrée** sur le nœud **Images composites (2D)**.

![Workflows personnalisés Firefly](./images/ffcw21.png)

Dans le menu, sous **Entrée et sortie**, sélectionnez un nœud **Texte d’entrée** et faites-le glisser sur la zone de travail.

Connectez le point vert en regard de **Texte** sur le nœud **Texte d’entrée** au point vert en regard de **Invite** sur le nœud **Images composites (2D)**.

![Workflows personnalisés Firefly](./images/ffcw22.png)

Tu devrais avoir ça. Saisissez l’invite ci-dessous dans le nœud **Texte de saisie**.

`magazine quality photo of a phone on a red pedestal with a pink background surrounded by origami style pink paper hearts`

Dans le menu, sous **Entrée et sortie**, sélectionnez un nœud **Images de sortie** et faites-le glisser sur la zone de travail.

Connectez le point bleu en regard de **Image composite** sur le nœud **Images composites (2D)** au point bleu en regard de **Image d’entrée** sur le nœud **Image de sortie**.

Cliquez sur **Exécuter**.

![Workflows personnalisés Firefly](./images/ffcw23.png)

Après quelques minutes, vous devriez voir quelque chose comme ceci, qui montre votre image d’origine dans une composition basée sur l’invite fournie, dans une résolution spécifique.

![Workflows personnalisés Firefly](./images/ffcw24.png)

## 1.7.1.4 Supprimer l’arrière-plan + Recadrer + Image composite + Générer la vidéo

Dans le menu, accédez à **Vidéo**. Sélectionnez le nœud **Générer la vidéo** et faites-le glisser sur la zone de travail.

Connectez le point bleu en regard de **Image composite** du nœud **Images composites (2D)** au point bleu en regard de **Image d’entrée** du nœud **Générer une vidéo**.

![Workflows personnalisés Firefly](./images/ffcw25.png)

Dans le menu, accédez à **Entrée et sortie**. Sélectionnez le nœud **Texte d’entrée** et faites-le glisser sur la zone de travail.

Connectez le point vert en regard de **Texte** sur le nœud **Texte d’entrée** au point vert en regard de **Invite** du nœud **Générer une vidéo**.

Saisissez le `background hearts fluttering` d’invite dans le nœud **Texte de saisie**.

Dans le menu, accédez à **Entrée et sortie**. Sélectionnez le nœud **Vidéo de sortie** et faites-le glisser sur la zone de travail.

Connectez le point violet en regard de **Sortie vidéo** du nœud **Générer la vidéo** au point violet en regard de **Vidéo** sur le nœud **Vidéo de sortie**.

Cliquez sur **Exécuter**.

![Workflows personnalisés Firefly](./images/ffcw26.png)

Après quelques vidéos, vous devriez voir ceci qui montre une vidéo basée sur la combinaison de l’image fournie et de l’invite.

![Workflows personnalisés Firefly](./images/ffcw27.png)

## Échelle de 1.7.1.5

Vous l’avez maintenant fait pour 1 image. Utilisons maintenant ce workflow, mais pour plusieurs images.

Téléchargez ces images sur votre bureau :

- [watch.jpg](./assets/watch.jpg)
- [airpods.jpg](./assets/airpods.jpg)

![Workflows personnalisés Firefly](./images/ffcw28.png)

Dans votre workflow, revenez au premier nœud, **Images d’entrée**. Supprimez l’image actuellement sélectionnée.

![Workflows personnalisés Firefly](./images/ffcw29.png)

Cliquez sur la zone **Glisser-déposer**.

![Workflows personnalisés Firefly](./images/ffcw30.png)

Sélectionnez les 3 images que vous avez téléchargées. Cliquez sur **Ouvrir**.

![Workflows personnalisés Firefly](./images/ffcw31.png)

Vous devriez alors voir ceci. cliquez sur **Exécuter**.

![Workflows personnalisés Firefly](./images/ffcw32.png)

Au bout de quelques minutes, vous devriez voir une sortie similaire, avec 3 images générées et 3 vidéos.

![Workflows personnalisés Firefly](./images/ffcw33.png)

## 1.7.1.5 Store dans AEM Assets CS

Dans cet exercice, vous allez stocker les ressources créées dans le cadre de votre workflow personnalisé dans AEM Assets CS.

Vous devez d’abord créer un dossier dans votre environnement AEM Assets CS.

Pour ce faire, accédez à [https://experience.adobe.com](https://experience.adobe.com?lang=fr). Cliquez pour ouvrir **Experience Manager Assets**.

![Workflows personnalisés Firefly](./images/ffcw50.png)

Sélectionnez votre environnement AEM Assets CS, qui doit être nommé `--aepUserLdap-- - CitiSignal AEM + ACCS`.

![Workflows personnalisés Firefly](./images/ffcw51.png)

Accédez à **Assets** puis cliquez sur **Créer un dossier**.

![Workflows personnalisés Firefly](./images/ffcw52.png)

Saisissez le nom : `--aepUserLdap-- - Firefly Custom Workflows`. Cliquez sur **Créer**.

![Workflows personnalisés Firefly](./images/ffcw53.png)

Revenez à votre workflow personnalisé et accédez au nœud **Images de sortie**. Cliquez sur **Par défaut** puis sélectionnez **AEM Assets**.

![Workflows personnalisés Firefly](./images/ffcw57.png)

Vous devriez alors voir cette fenêtre contextuelle. Sélectionnez votre référentiel AEM Assets CS, puis sélectionnez le dossier que vous venez de créer et qui doit être nommé : `--aepUserLdap-- - Firefly Custom Workflows`. Cliquez sur **Sélectionner**.

![Workflows personnalisés Firefly](./images/ffcw54.png)

Accédez au nœud **Vidéo de sortie**. Cliquez sur **Par défaut** puis sélectionnez **AEM Assets**.

![Workflows personnalisés Firefly](./images/ffcw55.png)

Vous devriez alors voir cette fenêtre contextuelle. Sélectionnez votre référentiel AEM Assets CS, puis sélectionnez le dossier que vous venez de créer et qui doit être nommé : `--aepUserLdap-- - Firefly Custom Workflows`. Cliquez sur **Sélectionner**.

![Workflows personnalisés Firefly](./images/ffcw56.png)

Tu devrais avoir ça. Cliquez sur **Exécuter**.

![Workflows personnalisés Firefly](./images/ffcw56a.png)

Au bout de quelques minutes, vous devriez voir les ressources créées devenir disponibles dans le dossier dans AEM Assets CS.

![Workflows personnalisés Firefly](./images/ffcw58.png)

## Étapes suivantes

Revenez au [créateur de workflows](./workflowbuilder.md){target="_blank"}

Revenir à [Tous les modules](./../../../overview.md){target="_blank"}
