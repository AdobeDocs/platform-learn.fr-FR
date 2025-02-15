---
title: Prise en main des services Firefly
description: Découvrez comment utiliser Postman et Adobe I/O pour interroger les API des services Adobe Firefly
role: Developer
level: Beginner
jira: KT-5342
doc-type: Tutorial
exl-id: 52385c33-f316-4fd9-905f-72d2d346f8f5
source-git-commit: 219945c74c620b9a4b93cb2b7462137118d42d33
workflow-type: tm+mt
source-wordcount: '819'
ht-degree: 1%

---

# 1.1.1 Prise en main des services Firefly

Découvrez comment utiliser Postman et Adobe I/O pour interroger les API Adobe Firefly Services.

## 1.1.1.1 Configurer votre projet Adobe I/O

Dans cet exercice, Adobe I/O est utilisé pour effectuer des requêtes sur les API Firefly Services. Pour configurer Adobe I/O, procédez comme suit.

1. Accédez à [https://developer.adobe.com/console/home](https://developer.adobe.com/console/home){target="_blank"}.

![Nouvelle intégration Adobe I/O](./images/iohome.png){zoomable="yes"}

1. Veillez à sélectionner l’instance appropriée dans le coin supérieur droit de l’écran. Votre instance est `--aepImsOrgName--`. Sélectionnez ensuite **Créer un projet**.

![Nouvelle intégration Adobe I/O](./images/iocomp.png){zoomable="yes"}

1. Sélectionnez **+ Ajouter au projet** et choisissez **API**.

![Nouvelle intégration Adobe I/O](./images/adobe_io_access_api.png){zoomable="yes"}

Votre écran devrait ressembler à ceci.

![Nouvelle intégration Adobe I/O](./images/api1.png){zoomable="yes"}

1. Sélectionnez **Creative Cloud** puis **Firefly - Services Firefly**, puis sélectionnez **Suivant**.

![Nouvelle intégration Adobe I/O](./images/api3.png){zoomable="yes"}

1. Attribuez un nom à vos informations d’identification : `--aepUserLdap-- - Firefly Services OAuth credential`, puis sélectionnez **Suivant**.

![Nouvelle intégration Adobe I/O](./images/api4.png){zoomable="yes"}

1. Sélectionnez le profil par défaut **Configuration par défaut des services Firefly** et sélectionnez **Enregistrer l’API configurée**.

![Nouvelle intégration Adobe I/O](./images/api9.png){zoomable="yes"}

Votre intégration Adobe I/O est maintenant prête.

![Nouvelle intégration Adobe I/O](./images/api11.png){zoomable="yes"}

## 1.1.1.2 Télécharger l’environnement Postman

1. Sélectionnez **Télécharger pour Postman**, puis choisissez **OAuth serveur à serveur** pour télécharger un environnement Postman.

![Nouvelle intégration Adobe I/O](./images/iopm.png){zoomable="yes"}

1. Sélectionnez le nom du projet.

![Nouvelle intégration Adobe I/O](./images/api13.png){zoomable="yes"}

1. Sélectionnez **Modifier le projet**.

![Nouvelle intégration Adobe I/O](./images/api14.png){zoomable="yes"}

1. Saisissez un nom convivial pour votre intégration : `--aepUserLdap-- Firefly`et sélectionnez **Enregistrer**.

![Nouvelle intégration Adobe I/O](./images/api15.png){zoomable="yes"}

La configuration de votre intégration Adobe I/O est maintenant terminée.

![Nouvelle intégration Adobe I/O](./images/api16.png){zoomable="yes"}

## 1.1.1.3 de l’authentification Postman à Adobe I/O

1. Téléchargez et installez la version de Postman appropriée à votre système d’exploitation sur [Postman Downloads](https://www.postman.com/downloads/){target="_blank"}.

![Nouvelle intégration Adobe I/O](./images/getstarted.png){zoomable="yes"}

1. Démarrez l’application.

Dans Postman, il existe 2 concepts : Environnements et Collections.

- Le fichier d’environnement contient toutes vos variables d’environnement qui sont plus ou moins cohérentes. Dans l’environnement , vous trouverez des éléments tels que l’IMSOrg de votre environnement Adobe, ainsi que des informations d’identification de sécurité telles que votre identifiant client et d’autres. Vous avez téléchargé le fichier d’environnement lors de la configuration précédente d’Adobe I/O et il est nommé **`oauth_server_to_server.postman_environment.json`**.

- La collection contient un certain nombre de requêtes d’API que vous pouvez utiliser. Nous utiliserons 2 collections
   - 1 collection pour l’authentification à Adobe I/O
   - 1 Collection pour les exercices de ce module

1. Téléchargez [postman-ff.zip](./../../../assets/postman/postman-ff.zip) sur votre bureau local.

![Nouvelle intégration Adobe I/O](./images/pmfolder.png){zoomable="yes"}

Dans le fichier **postman.zip** se trouvent les fichiers suivants :

    - `Adobe IO - OAuth.postman_collection.json`
    - `FF - Firefly Services Tech Insiders.postman_collection.json`

1. Décompressez **postman-ff.zip** et stockez les 2 fichiers suivants dans un dossier sur votre bureau :
- Adobe IO - OAuth.postman_collection.json
- FF - Firefly Services Tech Insiders.postman_collection.json
- oauth_server_to_server.postman_environment.json

![Nouvelle intégration Adobe I/O](./images/pmfolder1.png){zoomable="yes"}

1. Dans Postman, sélectionnez **Importer**.

![Nouvelle intégration Adobe I/O](./images/postmanui.png){zoomable="yes"}

1. Sélectionnez **Fichiers**.

![Nouvelle intégration Adobe I/O](./images/choosefiles.png){zoomable="yes"}

1. Sélectionnez les trois fichiers dans le dossier, puis sélectionnez **Ouvrir** et **Importer**.

![Nouvelle intégration Adobe I/O](./images/selectfiles.png){zoomable="yes"}

![Nouvelle intégration Adobe I/O](./images/impconfirm.png){zoomable="yes"}

Vous disposez désormais de tout ce dont vous avez besoin dans Postman pour commencer à interagir avec les services Firefly par le biais des API.

## 1.1.1.4 Demander un jeton d’accès

Ensuite, pour vous assurer que vous êtes correctement authentifié, vous devez demander un jeton d’accès.

1. Assurez-vous que l’environnement approprié est sélectionné avant d’exécuter une requête en vérifiant la liste déroulante Environnement dans le coin supérieur droit. L’environnement sélectionné doit porter un nom similaire à celui-ci, `--aepUserLdap-- Firefly Services OAuth Credential`.

![Postman](./images/envselemea1.png){zoomable="yes"}

L’environnement sélectionné doit porter un nom similaire à celui-ci, `--aepUserLdap-- Firefly Services OAuth Credential`.

![Postman](./images/envselemea.png){zoomable="yes"}

Maintenant que votre environnement Postman et vos collections sont configurés et fonctionnent, vous pouvez vous authentifier de Postman à Adobe I/O.

1. Dans la collection **Adobe IO - OAuth**, sélectionnez la requête nommée **POST - Obtenir le jeton d’accès** et sélectionnez **Envoyer**.

Notez que sous **Paramètres de requête**, deux variables sont référencées : `API_KEY` et `CLIENT_SECRET`. Ces variables sont extraites de l’environnement sélectionné, `--aepUserLdap-- Firefly Services OAuth Credential`.

![Postman](./images/ioauth.png){zoomable="yes"}

En cas de réussite, une réponse contenant un jeton porteur, un jeton d’accès et une fenêtre d’expiration s’affiche dans la section **Corps** de Postman.

![Postman](./images/ioauthresp.png){zoomable="yes"}


Vous devriez voir une réponse similaire contenant les informations suivantes :

| Clé | Valeur |
|:-------------:| :---------------:| 
| token_type | **porteur** |
| access_token | **eyJhbGciOiJSU..** |
| expires_in | **86399** |

L’Adobe I/O **bearer-token** a une valeur spécifique (le très long access_token) et une fenêtre d’expiration et est désormais valide pendant 24 heures. Cela signifie qu’au bout de 24 heures, si vous souhaitez utiliser Postman pour vous authentifier auprès d’Adobe I/O, vous devrez générer un nouveau jeton en exécutant à nouveau cette requête.

## 1.1.1.5 API Firefly Services, Texte 2 Image

Vous êtes maintenant prêt à envoyer votre première requête aux API Firefly Services.

1. Sélectionnez la requête nommée **POST - Firefly - T2I V3** dans la collection **FF - Firefly Services Tech Insiders**.

![Firefly](./images/ff1.png){zoomable="yes"}

1. Copiez l’URL de l’image à partir de la réponse et ouvrez-la dans votre navigateur web pour afficher l’image.

![Firefly](./images/ff2.png){zoomable="yes"}

Vous devriez voir une belle image représentant `horses in a field`.

![Firefly](./images/ff3.png){zoomable="yes"}

N’hésitez pas à lire la requête API avant de passer à l’exercice suivant.

## Étapes suivantes

Accédez à [Optimiser votre processus Firefly à l’aide de Microsoft Azure et des URL prédéfinies](./ex2.md){target="_blank"}

Revenez à [ Présentation des services Adobe Firefly ](./firefly-services.md){target="_blank"}

Revenir à [Tous les modules](./../../../overview.md){target="_blank"}
