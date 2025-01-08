---
title: Prise en main des services Firefly
description: Prise en main des services Firefly
kt: 5342
doc-type: tutorial
exl-id: 52385c33-f316-4fd9-905f-72d2d346f8f5
source-git-commit: ea06ca2d05195efa57643d45d7e50d3d914081d3
workflow-type: tm+mt
source-wordcount: '935'
ht-degree: 1%

---

# 1.1.1 Prise en main des services Firefly

Dans cet exercice, vous allez utiliser Postman et Adobe I/O pour interroger les API Adobe Firefly Services.

## Configuration de votre projet d’Adobe I/O

Dans cet exercice, vous utiliserez Adobe I/O de manière assez intensive pour effectuer des requêtes sur les API Firefly Services. Pour configurer l’Adobe I/O, procédez comme suit.

Accédez à [https://developer.adobe.com/console/home](https://developer.adobe.com/console/home)

![Adobe I/O d&#39;une nouvelle intégration](./images/iohome.png)

Veillez à sélectionner l’instance appropriée dans le coin supérieur droit de l’écran. Votre instance est `--aepImsOrgName--`. Cliquez sur **Créer un projet**.

![Adobe I/O d&#39;une nouvelle intégration](./images/iocomp.png)

Sélectionnez **+ Ajouter au projet** puis **API**.

![Adobe I/O d&#39;une nouvelle intégration](./images/adobe_io_access_api.png)

Vous verrez alors ceci :

![Adobe I/O d&#39;une nouvelle intégration](./images/api1.png)

Sélectionnez **Creative Cloud** puis cliquez sur **Firefly - Services de Firefly**. Cliquez sur **Suivant**.

![Adobe I/O d&#39;une nouvelle intégration](./images/api3.png)

Vous allez voir ceci. Attribuez un nom à vos informations d’identification : `--aepUserLdap-- - Firefly Services OAuth credential`. Cliquez sur **Suivant**.

![Adobe I/O d&#39;une nouvelle intégration](./images/api4.png)

Ensuite, vous devez sélectionner un profil de produit qui définira les autorisations disponibles pour cette intégration.

Sélectionnez le profil **Configuration des services de Firefly par défaut**.

Cliquez sur **Enregistrer l’API configurée**.

![Adobe I/O d&#39;une nouvelle intégration](./images/api9.png)

Votre intégration Adobe I/O est maintenant prête.

![Adobe I/O d&#39;une nouvelle intégration](./images/api11.png)

Cliquez sur le bouton **Télécharger pour Postman** puis sur **OAuth de serveur à serveur** pour télécharger un environnement Postman.

![Adobe I/O d&#39;une nouvelle intégration](./images/iopm.png)

Votre projet d&#39;E/S porte actuellement un nom générique. Vous devez donner un nom convivial à votre intégration. Cliquez sur **Projet X** (ou un nom similaire) comme indiqué

![Adobe I/O d&#39;une nouvelle intégration](./images/api13.png)

Cliquez sur **Modifier le projet**.

![Adobe I/O d&#39;une nouvelle intégration](./images/api14.png)

Saisissez un nom pour votre intégration : `--aepUserLdap-- Firefly`.

Cliquez sur **Enregistrer**.

![Adobe I/O d&#39;une nouvelle intégration](./images/api15.png)

La configuration de votre intégration Adobe I/O est maintenant terminée.

![Adobe I/O d&#39;une nouvelle intégration](./images/api16.png)

## Authentification Postman à l’Adobe I/O

Accédez à [https://www.postman.com/downloads/](https://www.postman.com/downloads/).

Téléchargez et installez la version de Postman appropriée à votre système d’exploitation.

![Adobe I/O d&#39;une nouvelle intégration](./images/getstarted.png)

Après l’installation de Postman, démarrez l’application.

Dans Postman, il existe 2 concepts : Environnements et Collections.

- Le fichier d’environnement contient toutes vos variables d’environnement qui sont plus ou moins cohérentes. Dans l’environnement , vous trouverez des éléments tels que l’IMSOrg de votre environnement d’Adobe, ainsi que des informations d’identification de sécurité telles que votre identifiant client et d’autres. Le fichier d’environnement est celui que vous avez téléchargé lors de la configuration de l’Adobe I/O dans l’exercice précédent. Il est nommé comme suit : **`oauth_server_to_server.postman_environment.json`**.

- La collection contient un certain nombre de requêtes d’API que vous pouvez utiliser. Nous utiliserons 2 collections
   - 1 collection pour l’authentification à l’Adobe I/O
   - 1 Collection pour les exercices de ce module

Téléchargez le fichier [postman.zip](./../../../assets/postman/postman-ff.zip) sur votre bureau local.

![Adobe I/O d&#39;une nouvelle intégration](./images/pmfolder.png)

Dans ce fichier **postman.zip**, vous trouverez les fichiers suivants :

- `Adobe IO - OAuth.postman_collection.json`
- `FF - Firefly Services Tech Insiders.postman_collection.json`

Décompressez le fichier **postman-ff.zip** et stockez ces 2 fichiers dans un dossier sur votre bureau, avec l’environnement Postman téléchargé à partir d’Adobe I/O, qui est le `oauth_server_to_server.postman_environment.json` de fichiers. Vous devez avoir ces 3 fichiers dans ce dossier :

![Adobe I/O d&#39;une nouvelle intégration](./images/pmfolder1.png)

Revenez à Postman. Cliquez sur **Importer**.

![Adobe I/O d&#39;une nouvelle intégration](./images/postmanui.png)

Cliquez sur **fichiers**.

![Adobe I/O d&#39;une nouvelle intégration](./images/choosefiles.png)

Accédez au dossier sur votre bureau dans lequel vous avez extrait les 2 fichiers téléchargés. Sélectionnez ces 3 fichiers en même temps et cliquez sur **Ouvrir**.

![Adobe I/O d&#39;une nouvelle intégration](./images/selectfiles.png)

Après avoir cliqué sur **Ouvrir**, Postman vous présente un aperçu de l’environnement et des collections que vous êtes sur le point d’importer. Cliquez sur **Importer**.

![Adobe I/O d&#39;une nouvelle intégration](./images/impconfirm.png)

Vous disposez désormais de tout ce dont vous avez besoin dans Postman pour commencer à interagir avec les services de Firefly via les API.

La première chose à faire est de vous assurer que vous êtes correctement authentifié. Pour être authentifié, vous devez demander un jeton d’accès.

Assurez-vous que l’environnement approprié est sélectionné avant d’exécuter toute requête. Vous pouvez vérifier l’environnement actuellement sélectionné en vérifiant la liste déroulante Environnement dans le coin supérieur droit.

L’environnement sélectionné doit porter un nom similaire à celui-ci, `--aepUserLdap-- Firefly Services OAuth Credential`.

![Postman](./images/envselemea.png)

Votre environnement et vos collections Postman sont maintenant configurés et fonctionnent. Vous pouvez désormais vous authentifier de Postman à Adobe I/O.

Dans la collection **Adobe IO - OAuth**, sélectionnez la requête nommée **POST - Obtenir le jeton d’accès**. Vous constaterez que sous **Params**, 2 variables sont référencées, `API_KEY` et `CLIENT_SECRET`. Ces variables sont extraites de l’environnement sélectionné, `--aepUserLdap-- Firefly Services OAuth Credential`.

Cliquez sur **Envoyer**.

![Postman](./images/ioauth.png)

Après avoir cliqué sur **Envoyer**, une réponse s’affiche dans la section **Corps** de Postman :

![Postman](./images/ioauthresp.png)

Si votre configuration a réussi, vous devriez voir une réponse similaire contenant les informations suivantes :

| Clé | Valeur |
|:-------------:| :---------------:| 
| token_type | **porteur** |
| access_token | **eyJhbGciOiJSU..** |
| expires_in | **86399** |

L’Adobe I/O vous a donné un **bearer**-token, avec une valeur spécifique (le très long access_token) et une fenêtre d’expiration.

Le jeton que nous avons reçu est maintenant valide pendant 24 heures. Cela signifie qu’au bout de 24 heures, si vous souhaitez utiliser Postman pour vous authentifier sur Adobe I/O, vous devrez générer un nouveau jeton en exécutant à nouveau cette requête.

## API Firefly Services, image Texte 2

Vous pouvez maintenant envoyer votre première requête aux API des services de Firefly.

Dans la collection **FF - Firefly Services Tech Insiders**, sélectionnez la demande nommée **POST - Firefly - T2I V3**. Dans la section **Corps**, vous verrez une invite par défaut indiquant `Horses in a field`. Cliquez sur **Envoyer** pour que les services de Firefly génèrent cette image.

![Firefly ](./images/ff1.png)

Une réponse similaire, contenant une URL d’image, s’affiche ensuite. Copiez l’URL de l’image et ouvrez-la dans votre navigateur web.

![Firefly ](./images/ff2.png)

Vous verrez maintenant une belle image représentant `horses in a field`.

![Firefly ](./images/ff3.png)

N’hésitez pas à lire la requête API avant de passer à l’exercice suivant.

Étape suivante : [1.1.2 Optimisez le processus de votre Firefly à l’aide de Microsoft Azure et des URL présignées](./ex2.md)

[Retour au module 1.1](./firefly-services.md)

[Revenir à tous les modules](./../../../overview.md)
