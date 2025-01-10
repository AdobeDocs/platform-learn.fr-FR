---
title: Création de votre programme Cloud Manager
description: Création de votre programme Cloud Manager
kt: 5342
doc-type: tutorial
source-git-commit: cd7601002c7d18232fdd2e8e68cbc4315e118948
workflow-type: tm+mt
source-wordcount: '992'
ht-degree: 1%

---

# 2.1.2 Configuration de votre environnement AEM CS

## 2.1.2.1 Configurer votre référentiel GitHub

Accédez à [https://github.com](https://github.com). Cliquez sur **Se connecter**.

![ AEMCS ](./images/aemcssetup1.png)

Saisissez vos informations d’identification. Cliquez sur **Se connecter**.

![ AEMCS ](./images/aemcssetup2.png)

Une fois connecté, votre tableau de bord GitHub s’affiche.

![ AEMCS ](./images/aemcssetup3.png)

Accédez à [https://github.com/AdobeDevXSC/citisignal-one](https://github.com/AdobeDevXSC/citisignal-one). Tu verras ça. Cliquez sur **Utiliser ce modèle** puis sur **Créer un référentiel**.

![ AEMCS ](./images/aemcssetup4.png)

Pour le **Nom du référentiel**, utilisez `citisignal`. Définissez la visibilité sur **Privé**. Cliquez sur **Créer un référentiel**.

![ AEMCS ](./images/aemcssetup5.png)

Au bout de quelques secondes, votre référentiel sera alors créé.

![ AEMCS ](./images/aemcssetup6.png)

Ensuite, accédez à [https://github.com/apps/aem-code-sync](https://github.com/apps/aem-code-sync). Cliquez sur **Configurer**.

![ AEMCS ](./images/aemcssetup7.png)

Cliquez sur votre compte GitHub.

![ AEMCS ](./images/aemcssetup8.png)

Cliquez sur **Sélectionner uniquement les référentiels** puis ajoutez le référentiel que vous venez de créer. Cliquez ensuite sur **Installer**.

![ AEMCS ](./images/aemcssetup9.png)

Vous obtiendrez alors cette confirmation.

![ AEMCS ](./images/aemcssetup10.png)

## 2.1.2.2 Mettre à jour le fichier fstab.yaml

Dans votre référentiel GitHub, cliquez sur pour ouvrir le fichier `fstab.yaml`.

![ AEMCS ](./images/aemcssetup11.png)

Cliquez sur l’icône **modifier**.

![ AEMCS ](./images/aemcssetup12.png)

Vous devez maintenant mettre à jour la valeur du champ **url** à la ligne 4.

![ AEMCS ](./images/aemcssetup13.png)

Vous devez remplacer la valeur actuelle par l’URL de votre environnement AEM CS spécifique, en combinaison avec les paramètres de votre référentiel GitHub.

Il s’agit de la valeur actuelle de l’URL : `https://author-p131639-e1282833.adobeaemcloud.com/bin/franklin.delivery/adobedevxsc/citisignal-one/main`.

3 parties de l’URL doivent être mises à jour

`https://XXX/bin/franklin.delivery/YYY/ZZZ/main`

XXX doit être remplacé par l’URL de votre environnement de création AEM CS.

Vous devriez être remplacé par votre compte utilisateur GitHub.

ZZZ doit être remplacé par le nom du référentiel GitHub que vous avez utilisé dans l’exercice précédent.

Vous trouverez l’URL de votre environnement de création AEM CS à l’adresse [https://my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com). Cliquez sur votre **Programme** pour l’ouvrir.

![ AEMCS ](./images/aemcs6.png)

Cliquez ensuite sur le **de 3 points...** dans l’onglet **Environnements** et cliquez sur **Afficher les détails**.

![ AEMCS ](./images/aemcs9.png)

Vous verrez ensuite les détails de votre environnement, y compris l’URL de votre environnement **de création**. Copiez l’URL.

![ AEMCS ](./images/aemcs10.png)

XXX = `author-p148073-e1511503.adobeaemcloud.com`

Pour le nom de compte d’utilisateur GitHub, vous pouvez facilement le trouver dans l’URL de votre navigateur. Dans cet exemple, le nom du compte utilisateur est `woutervangeluwe`.

AAAA = `woutervangeluwe`

![ AEMCS ](./images/aemcs11.png)

Pour le nom du référentiel GitHub, vous pouvez également le trouver dans la fenêtre du navigateur que vous avez ouverte dans GitHub. Dans ce cas, le nom du référentiel est `citisignal`.

ZZZ = `citisignal`

![ AEMCS ](./images/aemcs12.png)

La combinaison de ces 3 valeurs entraîne la création de cette nouvelle URL qui doit être configurée dans le `fstab.yaml` de fichiers.

`https://author-p148073-e1511503.adobeaemcloud.com/bin/franklin.delivery/woutervangeluwe/citisignal/main`

Cliquez sur **Valider les modifications...**.

![ AEMCS ](./images/aemcs13.png)

Cliquez sur **Valider les modifications**.

![ AEMCS ](./images/aemcs14.png)

Le fichier `fstab.yaml` a été mis à jour.

## 2.1.2.3 Charger des ressources CitiSignal

Accédez à [https://my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com). Cliquez sur votre **Programme** pour l’ouvrir.

![ AEMCS ](./images/aemcs6.png)

Cliquez ensuite sur l’URL de votre environnement de création.

![ AEMCS ](./images/aemcssetup18.png)

Cliquez sur **Se connecter avec Adobe**.

![ AEMCS ](./images/aemcssetup19.png)

Votre environnement de création s’affiche alors.

![ AEMCS ](./images/aemcssetup20.png)

Votre URL ressemblera à ceci : `https://author-p148073-e1511503.adobeaemcloud.com/ui#/aem/aem/start.html?appId=aemshell`

Vous devez maintenant accéder à l’environnement **Gestionnaire de packages CRX** d’AEM. Pour ce faire, supprimez `ui#/aem/aem/start.html?appId=aemshell` de l’URL et remplacez-la par `crx/packmgr`, ce qui signifie que votre URL doit maintenant ressembler à ceci :
`https://author-p148073-e1511503.adobeaemcloud.com/crx/packmgr`.
Appuyez sur **Entrée** pour charger l’environnement du gestionnaire de packages.

![ AEMCS ](./images/aemcssetup22.png)

Cliquez ensuite sur **Télécharger le package**.

![ AEMCS ](./images/aemcssetup21.png)

Cliquez sur **Parcourir** pour localiser le package à charger.

Le package à charger est appelé **citisignal-assets.zip** et peut être téléchargé ici : [https://tech-insiders.s3.us-west-2.amazonaws.com/one-adobe/citisignal-assets.zip](https://tech-insiders.s3.us-west-2.amazonaws.com/one-adobe/citisignal-assets.zip).

![ AEMCS ](./images/aemcssetup23.png)

Sélectionnez le package et cliquez sur **Ouvrir**.

![ AEMCS ](./images/aemcssetup24.png)

Cliquez ensuite sur **OK**.

![ AEMCS ](./images/aemcssetup25.png)

Le package sera ensuite chargé.

![ AEMCS ](./images/aemcssetup26.png)

Cliquez ensuite sur **Installer** sur le package que vous venez de télécharger.

![ AEMCS ](./images/aemcssetup27.png)

Cliquez sur **Installer**.

![ AEMCS ](./images/aemcssetup28.png)

Au bout de quelques minutes, votre package sera alors installé.

![ AEMCS ](./images/aemcssetup29.png)

Vous pouvez maintenant fermer cette fenêtre.


## 2.1.2.4 de ressources CitiSignal Publish

Accédez à [https://my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com). Cliquez sur votre **Programme** pour l’ouvrir.

![ AEMCS ](./images/aemcs6.png)

Cliquez ensuite sur l’URL de votre environnement de création.

![ AEMCS ](./images/aemcssetup18.png)

Cliquez sur **Se connecter avec Adobe**.

![ AEMCS ](./images/aemcssetup19.png)

Votre environnement de création s’affiche alors. Cliquez sur **Sites**.

![ AEMCS ](./images/aemcsassets1.png)

Cliquez sur **Fichiers**.

![ AEMCS ](./images/aemcsassets2.png)

Cliquez pour sélectionner le dossier **CitiSignal**, puis cliquez sur **Gérer la publication**.

![ AEMCS ](./images/aemcsassets3.png)

Cliquez sur **Suivant**.

![ AEMCS ](./images/aemcsassets4.png)

Cliquez sur **Publier**.

![ AEMCS ](./images/aemcsassets5.png)

Vos ressources ont maintenant été publiées.

## 2.1.2.5 Créer un site web CitiSignal

Accédez à [https://my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com). Cliquez sur votre **Programme** pour l’ouvrir.

![ AEMCS ](./images/aemcs6.png)

Cliquez ensuite sur l’URL de votre environnement de création.

![ AEMCS ](./images/aemcssetup18.png)

Cliquez sur **Se connecter avec Adobe**.

![ AEMCS ](./images/aemcssetup19.png)

Votre environnement de création s’affiche alors. Cliquez sur **Sites**.

![ AEMCS ](./images/aemcssetup30.png)

Cliquez sur **Créer** puis sur **Site à partir d’un modèle**.

![ AEMCS ](./images/aemcssetup31.png)

Cliquez sur **Importer**.

![ AEMCS ](./images/aemcssetup32.png)

Vous devez maintenant importer un modèle préconfiguré pour votre site. Vous pouvez télécharger le modèle [ici](./../../../assets/aem/citisignal-edge-delivery-services-template-0.0.4.zip). Enregistrez le fichier sur votre bureau.

Sélectionnez ensuite le `citisignal-edge-delivery-services-template-0.0.4.zip` de fichier et cliquez sur **Ouvrir**.

![ AEMCS ](./images/aemcssetup33.png)

Tu verras ça. Cliquez pour sélectionner le modèle que vous venez de charger, puis cliquez sur **Suivant**.

![ AEMCS ](./images/aemcssetup34.png)

Vous devez maintenant renseigner certains détails.

- Titre du site : utiliser **CitiSignal**
- Nom du site : utilisez **citisignal-one**
- URL GitHub : copiez l’URL du référentiel GitHub que vous utilisiez précédemment

![ AEMCS ](./images/aemcssetup35.png)

Tu auras alors ceci. Cliquez sur **Créer**.

![ AEMCS ](./images/aemcssetup36.png)

Votre site est en cours de création. Cela peut prendre quelques minutes. Cliquez sur **OK**.

![ AEMCS ](./images/aemcssetup37.png)

Actualisez votre écran au bout de quelques minutes, vous verrez alors votre nouveau site CitiSignal.

![ AEMCS ](./images/aemcssetup38.png)

## Site web 2.1.2.6 Publish CitiSignal

Ensuite, cliquez sur la case à cocher devant **CitiSignal**. Cliquez ensuite sur **Gérer la publication**.

![ AEMCS ](./images/aemcssetup39.png)

Cliquez sur **Suivant**.

![ AEMCS ](./images/aemcssetup40.png)

Cliquez sur **Inclure les paramètres enfants**.

![ AEMCS ](./images/aemcssetup41.png)

Cochez la case **Inclure les enfants**, puis cliquez pour désélectionner les autres cases. Cliquez sur **OK**.

![ AEMCS ](./images/aemcssetup42.png)

Cliquez sur **Publier**.

![ AEMCS ](./images/aemcssetup43.png)

On vous renverra ensuite ici. Accédez à **CitiSignal** > **us** > **fr**. Cochez la case en regard de **index**, puis cliquez sur **Modifier**.

![ AEMCS ](./images/aemcssetup44.png)

Votre site web s’ouvre alors dans l’**éditeur universel**.

![ AEMCS ](./images/aemcssetup45.png)

Vous pourrez désormais accéder à votre site web en accédant à `main--citisignal--XXX.aem.page/us/en` et/ou `main--citisignal--XXX.aem.live/us/en`, après avoir remplacé XXX par votre compte utilisateur GitHub, qui est `woutervangeluwe` dans cet exemple.

Dans cet exemple, l’URL complète devient :
`https://main--citisignal--woutervangeluwe.aem.page/us/en` et/ou `https://main--citisignal--woutervangeluwe.aem.live/us/en`

Cela peut prendre un certain temps avant que toutes les ressources ne s’affichent correctement, car elles doivent d’abord être publiées.

Vous verrez alors ceci :

![ AEMCS ](./images/aemcssetup46.png)

Au bout de quelques minutes, les ressources se chargeront toutes correctement.

![ AEMCS ](./images/aemcssetup47.png)

## Performances de la page de test 2.1.2.7

Accédez à [https://pagespeed.web.dev/](https://pagespeed.web.dev/). Saisissez votre URL et cliquez sur **Analyser**.

![ AEMCS ](./images/aemcssetup48.png)

Votre site web obtient un score élevé dans les visualisations pour appareils mobiles et pour ordinateurs de bureau :

**Mobile** :

![ AEMCS ](./images/aemcssetup49.png)

**Ordinateur de bureau** :

![ AEMCS ](./images/aemcssetup50.png)

Étape suivante : [2.1.3 Configurer un bloc personnalisé](./ex3.md)

[Retour au module 2.1](./aemcs.md)

[Revenir à tous les modules](./../../../overview.md)
