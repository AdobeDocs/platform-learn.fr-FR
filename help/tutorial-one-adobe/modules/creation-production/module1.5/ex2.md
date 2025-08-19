---
title: Validations avec Frame.io
description: Validations avec Frame.io
role: Developer
level: Beginner
jira: KT-5342
doc-type: Tutorial
source-git-commit: 96711c78cecdce13e2e2fd6e5a43e0815f59e079
workflow-type: tm+mt
source-wordcount: '707'
ht-degree: 0%

---

# 1.5.2 Approbations avec Frame.io

>[!NOTE]
>
> La capture d’écran ci-dessous montre un environnement spécifique utilisé. Lorsque vous parcourez ce tutoriel, il est très probable que votre environnement porte un nom différent. Lorsque vous vous êtes inscrit à ce tutoriel, les détails de l’environnement à utiliser vous ont été fournis. Veuillez suivre ces instructions.

Pour parcourir le workflow d’approbation dans Frame.io, vous devez disposer d’une ressource. Dans cet exercice, vous allez commencer par créer cette ressource vous-même à l’aide d’Adobe Firefly et d’Adobe Express. Une fois que vous disposez de la ressource, vous la chargez dans Frame.io, puis la validez.

## 1.5.2.1 Créer une ressource avec Adobe Firefly Services et Adobe Express

Accédez à [https://firefly.adobe.com/](https://firefly.adobe.com/){target="_blank"}. Saisissez le `a neon rabbit running very fast through space` d’invite et cliquez sur **Générer**.

![GSPeM](./../../workflow-planning/module1.2/images/gsasset1.png)

Plusieurs images sont alors générées. Choisissez l’image qui vous plaît le plus, cliquez sur l’icône **Partager** sur l’image, puis sélectionnez **Ouvrir dans Adobe Express**.

![GSPeM](./../../workflow-planning/module1.2/images/gsasset2.png)

L’image que vous venez de générer est alors disponible pour modification dans Adobe Express. Vous devez maintenant ajouter le logo CitiSignal sur l&#39;image. Pour ce faire, accédez à **Marques**.

![GSPeM](./../../workflow-planning/module1.2/images/gsasset3.png)

Vous devriez alors voir un modèle de marque CitiSignal. qui a été créé dans GenStudio for Performance Marketing s’affichent dans Adobe Express. Cliquez pour sélectionner un modèle de marque dont le nom contient `CitiSignal`.

![GSPeM](./../../workflow-planning/module1.2/images/gsasset4.png)

Accédez à **Logos** et cliquez sur le logo **blanc** Citisignal pour le déposer sur l’image.

![GSPeM](./../../workflow-planning/module1.2/images/gsasset5.png)

Positionnez le logo CitiSignal en haut de votre image, pas trop loin du milieu.

![GSPeM](./../../workflow-planning/module1.2/images/gsasset6.png)

Accédez à **Texte**.

![GSPeM](./../../workflow-planning/module1.2/images/gsasset6a.png)

Cliquez sur **Ajouter votre texte**.

![GSPeM](./../../workflow-planning/module1.2/images/gsasset6b.png)

Saisissez la `Timetravel now!` de texte, modifiez la couleur et la taille de la police, définissez le texte en **Gras** afin d’obtenir une image similaire à celle-ci.

![GSPeM](./../../workflow-planning/module1.2/images/gsasset6c.png)

Cliquez ensuite sur **Partager**.

![GSPeM](./../../workflow-planning/module1.2/images/gsasset7.png)

Cliquez sur **... Tout afficher**.

![Frame.io](./images/frameioasset1.png)

Faites défiler vers le bas et sélectionnez **Télécharger**.

![Frame.io](./images/frameioasset2.png)

Cliquez sur **Télécharger**.

![Frame.io](./images/frameioasset3.png)

Vous disposerez alors de votre ressource sur votre ordinateur local.

![Frame.io](./images/frameioasset4.png)

## 1.5.2.2 Approuver votre ressource dans Frame.io

Accédez à [https://next.frame.io/](https://next.frame.io/). Assurez-vous d’être connecté au `--aepImsOrgName--` d’environnement.

![Frame.io](./images/frameio1.png)

Si vous n’êtes pas connecté à l’environnement de droite, cliquez sur le logo dans le coin inférieur gauche, puis cliquez pour sélectionner l’environnement à utiliser.

![Frame.io](./images/frameio2.png)

Accédez à votre espace de travail, qui doit être nommé `--aepUserLdap--`, puis ouvrez le dossier **CitiSignal**. Cliquez sur l’icône **+**, puis sélectionnez **Nouveau dossier**.

![Frame.io](./images/frameioappr1.png)

Nommez le dossier `--aepUserLdap-- - Approvals`. Double-cliquez sur le dossier pour l’ouvrir.

![Frame.io](./images/frameioappr2.png)

Vous allez maintenant charger le fichier que vous avez créé dans l&#39;exercice précédent dans ce dossier. Cliquez sur **Télécharger**.

![Frame.io](./images/frameioappr3.png)

Sélectionnez le fichier et cliquez sur **Ouvrir**.

![Frame.io](./images/frameioappr4.png)

Tu devrais avoir ça. Double-cliquez sur le fichier pour l’ouvrir.

![Frame.io](./images/frameioappr5.png)

Activez l’icône pour laisser un commentaire ancré.

![Frame.io](./images/frameioappr6.png)

Saisissez un commentaire, tel que `Change CTA to "Get on board now!"`. Cliquez sur l’icône **envoyer** pour partager votre commentaire.

![Frame.io](./images/frameioappr7.png)

Tu devrais avoir ça. Accédez à **Champs**.

![Frame.io](./images/frameioappr8.png)

Dans le champ **Statut**, modifiez le statut en **Révision requise**.

![Frame.io](./images/frameioappr9.png)

Tu devrais avoir ça. Revenez au dossier en cliquant sur la flèche pour revenir en arrière.

![Frame.io](./images/frameioappr10.png)

Cliquez sur le **de 3 points...** et sélectionnez **Renommer**.

![Frame.io](./images/frameioappr11.png)

Remplacez le nom du fichier par `version1.png`.

![Frame.io](./images/frameioappr12.png)

## 1.5.2.3 Apporter des modifications de conception dans Adobe Express

Accédez à [https://new.express.adobe.com/your-stuff/files](https://new.express.adobe.com/your-stuff/files) puis ouvrez à nouveau l’image que vous avez créée précédemment.

![WF](./../../workflow-planning/module1.2/images/wfp25a.png)

Remplacez le texte CTA par `Get On Board Now!`.

![WF](./../../workflow-planning/module1.2/images/wfp25b.png)

Cliquez sur **Partager** puis sélectionnez **Télécharger**.

![WF](./images/frameioasset5.png)

Cliquez sur **Télécharger**.

![WF](./images/frameioasset6.png)

Une nouvelle image sera alors téléchargée sur votre ordinateur local. Renommez le fichier en `version2.png`.

![WF](./images/frameioasset7.png)

## 1.5.2.4 Approuver la version 2 dans Frame.io

Dans votre dossier Frame.io, cliquez sur l’icône **+** et sélectionnez **Charger une ressource**.

![Frame.io](./images/frameioappr13.png)

Sélectionnez le fichier **version2.png** et cliquez sur **Ouvrir**.

![Frame.io](./images/frameioappr14.png)

Faites ensuite glisser le fichier **version2.png** au-dessus du fichier **version1.png**. Cette action active l&#39;empilement de versions dans Frame.io.

![Frame.io](./images/frameioappr15.png)

Vous devriez alors voir ceci.

![Frame.io](./images/frameioappr16.png)

Cliquez sur le **de 3 points...** sur l’image, puis sélectionnez **Comparer les versions**.

![Frame.io](./images/frameioappr17.png)

Vous devriez alors voir cette vue de comparaison qui affiche les deux versions du fichier. Accédez à **Champs**.

![Frame.io](./images/frameioappr18.png)

Remplacez le champ **Statut** par **Approuvé**.

![Frame.io](./images/frameioappr19.png)

Tu devrais avoir ça. Cliquez sur l’icône de flèche pour revenir à la vue de votre dossier.

![Frame.io](./images/frameioappr20.png)

Cliquez sur le **3 points...** et sélectionnez **Télécharger** au cas où vous souhaiteriez utiliser ce fichier dans une autre application.

![Frame.io](./images/frameioappr21.png)

## Étapes suivantes

[1.5.3 Frame.io et Premiere Pro](./ex3.md){target="_blank"}

Revenez à [Rationaliser votre workflow avec Frame.io](./frameio.md){target="_blank"}

Revenir à [Tous les modules](./../../../overview.md){target="_blank"}
