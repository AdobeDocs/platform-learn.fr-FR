---
title: AEM CS - Création de votre site web basé sur des documents
description: AEM CS - Création de votre site web basé sur des documents
kt: 5342
doc-type: tutorial
exl-id: db366111-3873-4504-95f1-b240836c833f
source-git-commit: dd075b0296c6ba06d72b229145635060c2c6abb1
workflow-type: tm+mt
source-wordcount: '769'
ht-degree: 1%

---

# 1.1.2 Création de votre site web basé sur des documents

En attendant la création de votre programme Cloud Manager, vous disposez de suffisamment de temps pour configurer votre premier site web de création documentaire. L’exercice ci-dessous est basé sur le tutoriel du développeur [aem.live](https://www.aem.live/developer/tutorial){target="_blank"}. Suivez les étapes ci-dessous pour commencer.

## 1.1.2.1 Configurer votre lecteur Google

Accédez à [https://drive.google.com](https://drive.google.com){target="_blank"}. Cliquez sur **+ Nouveau** puis sur **Nouveau dossier**.

![ AEMCS ](./images/googledrive1.png){zoomable="yes"}

Nommez votre dossier `aemdocb-test`. Cliquez sur **Créer**.

![ AEMCS ](./images/googledrive2.png){zoomable="yes"}

Téléchargez le fichier [aemboilerplate.zip](./../../../assets/aem/aemboilerplate.zip){target="_blank"} et extrayez-le sur votre ordinateur.

![ AEMCS ](./images/googledrive3.png){zoomable="yes"}

Vous verrez 3 fichiers dans ce dossier. Copiez ces fichiers dans votre nouveau dossier Google Drive.

![ AEMCS ](./images/googledrive4.png){zoomable="yes"}

Vous devez maintenant convertir ces fichiers en fichier Google natif. Pour ce faire, ouvrez chaque fichier, puis accédez à **Fichier** > **Enregistrer sous Google Docs**.

![ AEMCS ](./images/googledrive5.png){zoomable="yes"}

Vous devez effectuer cette opération pour les 3 fichiers, puis vous verrez 6 fichiers dans votre dossier Google Drive.

![ AEMCS ](./images/googledrive6.png){zoomable="yes"}

Vous l’avez ensuite dans votre dossier .

![ AEMCS ](./images/googledrive7.png){zoomable="yes"}

Pour que la démonstration de création documentaire fonctionne, vous devez maintenant partager votre dossier Google Drive avec l’adresse e-mail **helix@adobe.com**. Cliquez sur le nom de votre dossier, puis sur **Partager** et de nouveau sur **Partager**.

![ AEMCS ](./images/googledrive8.png){zoomable="yes"}

Saisissez l’adresse électronique **helix@adobe.com** puis cliquez sur **Envoyer**.

![ AEMCS ](./images/googledrive9.png){zoomable="yes"}

Ensuite, copiez et notez l’URL de votre dossier Google Drive, car vous en aurez besoin dans l’exercice suivant. Cliquez sur le nom de votre dossier, sur **Partager**, puis sur **Copier le lien**.

![ AEMCS ](./images/googledrive10.png){zoomable="yes"}

`https://drive.google.com/drive/folders/1PNIOFeptIfszSebawT-Y_bwB4_anQWk5?usp=drive_link`

Vous devez supprimer le paramètre de chaîne de requête `?usp=drive_link` pour que l’URL ressemble à ceci :

`https://drive.google.com/drive/folders/1PNIOFeptIfszSebawT-Y_bwB4_anQWk5`

## 1.1.2.2 Configurer votre référentiel GitHub

Accédez à [https://github.com](https://github.com){target="_blank"}. Cliquez sur **Se connecter**.

![ AEMCS ](./images/aemcssetup1.png){zoomable="yes"}

Saisissez vos informations d’identification. Cliquez sur **Se connecter**.

![ AEMCS ](./images/aemcssetup2.png){zoomable="yes"}

Une fois connecté, votre tableau de bord GitHub s’affiche.

![ AEMCS ](./images/aemcssetup3.png){zoomable="yes"}

Accédez à [https://github.com/adobe/aem-boilerplate](https://github.com/adobe/aem-boilerplate){target="_blank"}. Tu verras ça. Cliquez sur **Utiliser ce modèle** puis sur **Créer un référentiel**.

![ AEMCS ](./images/aemdocbcssetup4.png){zoomable="yes"}

Pour le **Nom du référentiel**, utilisez `aemdocb-test`. Définissez la visibilité sur **Privé**. Cliquez sur **Créer un référentiel**.

![ AEMCS ](./images/aemdocbcssetup5.png){zoomable="yes"}

Au bout de quelques secondes, votre référentiel sera alors créé.

![ AEMCS ](./images/aemdocbcssetup6.png){zoomable="yes"}

Ensuite, accédez à [https://github.com/apps/aem-code-sync](https://github.com/apps/aem-code-sync){target="_blank"}. Cliquez sur **Configurer**.

![ AEMCS ](./images/aemcssetup7.png){zoomable="yes"}

Cliquez sur votre compte GitHub.

![ AEMCS ](./images/aemcssetup8.png){zoomable="yes"}

Cliquez sur **Sélectionner uniquement les référentiels** puis ajoutez le référentiel que vous venez de créer. Cliquez ensuite sur **Installer**.

![ AEMCS ](./images/aemdocbcssetup9.png){zoomable="yes"}

Vous obtiendrez alors cette confirmation.

![ AEMCS ](./images/aemcssetup10.png){zoomable="yes"}

## 1.1.2.3 Mettre à jour le fichier fstab.yaml

Dans votre référentiel GitHub, cliquez sur pour ouvrir le fichier `fstab.yaml`.

![ AEMCS ](./images/aemdocbcssetup11.png){zoomable="yes"}

Cliquez sur l’icône **modifier**.

![ AEMCS ](./images/aemdocbcssetup12.png){zoomable="yes"}

Vous devez maintenant mettre à jour la valeur du champ **url** à la ligne 2.

![ AEMCS ](./images/aemdocbcssetup13.png){zoomable="yes"}

Vous devez remplacer la valeur actuelle par l’URL de votre environnement AEM CS spécifique, en combinaison avec les paramètres de votre référentiel GitHub.

Il s’agit de la valeur actuelle de l’URL : `https://drive.google.com/drive/u/0/folders/1MGzOt7ubUh3gu7zhZIPb7R7dyRzG371j`.

Remplacez cette valeur par l’URL que vous avez copiée à partir de votre dossier Google Drive, `https://drive.google.com/drive/folders/1PNIOFeptIfszSebawT-Y_bwB4_anQWk5`. Cliquez sur **Valider les modifications...**.

![ AEMCS ](./images/aemdocbcssetup14.png){zoomable="yes"}

Cliquez sur **Valider les modifications**.

![ AEMCS ](./images/aemdocbcssetup15.png){zoomable="yes"}

## 1.1.2.4 Installer l’extension AEM Sidekick

Accédez à [https://chromewebstore.google.com/detail/aem-sidekick/ccfggkjabjahcjoljmgmklhpaccedipo](https://chromewebstore.google.com/detail/aem-sidekick/ccfggkjabjahcjoljmgmklhpaccedipo){target="_blank"}. Cliquez sur **Ajouter à Chrome**.

![ AEMCS ](./images/aemdocbcssetup16.png){zoomable="yes"}

Épinglez l’extension **AEM Sidekick**.

![ AEMCS ](./images/aemdocbcssetup17.png){zoomable="yes"}

## 1.1.2.5 et publier votre site web basé sur des documents

Revenez à votre dossier Google Drive. Dans la barre des tâches, cliquez sur l’extension **AEM Sidekick**. Une fenêtre contextuelle de la barre AEM Sidekick apparaît alors dans votre dossier.

![ AEMCS ](./images/aemdocbcssetup18.png){zoomable="yes"}

Sélectionnez les 3 fichiers dans votre dossier Google Drive. Cliquez sur **Aperçu**.

![ AEMCS ](./images/aemdocbcssetup19.png){zoomable="yes"}

Cliquez de nouveau sur **Aperçu**.

![ AEMCS ](./images/aemdocbcssetup20.png){zoomable="yes"}

Cliquez pour fermer la boîte de dialogue contextuelle verte.

![ AEMCS ](./images/aemdocbcssetup21.png){zoomable="yes"}

Sélectionnez à nouveau les 3 fichiers dans votre dossier Google Drive. Cliquez maintenant sur **Publier**.

![ AEMCS ](./images/aemdocbcssetup22.png){zoomable="yes"}

Cliquez sur **Publier**.

![ AEMCS ](./images/aemdocbcssetup23.png){zoomable="yes"}

Cliquez pour fermer à nouveau la boîte de dialogue verte. Sélectionnez à présent le fichier **index**, cliquez sur **Copier les URL** puis sur **Copier les URL dynamiques**.

![ AEMCS ](./images/aemdocbcssetup24.png){zoomable="yes"}

L’URL qui a été copiée ressemblera à ceci : `https://main--aemdocb-test--woutervangeluwe.aem.live/`.

Dans l’URL ci-dessus :

- **main** fait référence à la branche de votre référentiel GitHub
- **aemdocb-test** fait référence au nom du référentiel GitHub
- **woutervangeluwe** fait référence au nom du compte utilisateur GitHub
- **.live** fait référence à l’environnement en ligne de votre instance AEM
- Vous pouvez remplacer **.live** par **.page** pour ouvrir l’environnement de prévisualisation de votre instance AEM

Ouvrez une nouvelle fenêtre de navigateur et accédez à l’URL.

![ AEMCS ](./images/aemdocbcssetup25.png){zoomable="yes"}

## 1.1.2.6 Apporter une modification et publier votre modification

Revenez sur votre lecteur Google et ouvrez le filtre **index** dans Google.

![ AEMCS ](./images/aemdocbcssetup27.png){zoomable="yes"}

Remplacez le texte **Test** par tout autre texte de votre choix. Cliquez sur **Aperçu**.

![ AEMCS ](./images/aemdocbcssetup28.png){zoomable="yes"}

La version d’aperçu de votre site web s’ouvre alors. Vérifiez votre modification et cliquez sur **Publier**.

![ AEMCS ](./images/aemdocbcssetup29.png){zoomable="yes"}

Vous verrez alors la version en direct de votre site web.

![ AEMCS ](./images/aemdocbcssetup30.png){zoomable="yes"}

L’exercice ci-dessus était un bon moyen de commencer et de découvrir vous-même la création basée sur des documents. Vous pouvez maintenant passer à l’exercice suivant, au cours duquel vous allez configurer votre propre site web de démonstration à l’aide de CitiSignal en tant que marque de démonstration.

Étape suivante : [1.1.3 Configurer votre environnement AEM CS](./ex3.md){target="_blank"}

Revenir à [Adobe Experience Manager Cloud Service et Edge Delivery Services](./aemcs.md){target="_blank"}

[Revenir à tous les modules](./../../../overview.md){target="_blank"}
