---
title: Prise en main des services Firefly
description: Découvrez comment utiliser Postman et Adobe I/O pour interroger les API Adobe Firefly Services
role: Developer
level: Beginner
jira: KT-5342
doc-type: Tutorial
exl-id: 52385c33-f316-4fd9-905f-72d2d346f8f5
source-git-commit: e6a549441d425801f2a554da9af803dca646009e
workflow-type: tm+mt
source-wordcount: '832'
ht-degree: 1%

---

# 1.1.1 Prise en main des services Firefly

Découvrez comment utiliser Postman et Adobe I/O pour interroger les API des services d’Adobe Firefly.

## 1.1.1.2 Configurer votre projet d’Adobe I/O

Dans cet exercice, l’Adobe I/O est utilisé pour effectuer des requêtes sur les API Firefly Services. Pour configurer l’Adobe I/O, procédez comme suit.

1. Accédez à [https://developer.adobe.com/console/home](https://developer.adobe.com/console/home){target="_blank"}.

![Adobe I/O d&#39;une nouvelle intégration](./images/iohome.png)

1. Veillez à sélectionner l’instance appropriée dans le coin supérieur droit de l’écran. Votre instance est `--aepImsOrgName--`. Sélectionnez ensuite **Créer un projet**.

![Adobe I/O d&#39;une nouvelle intégration](./images/iocomp.png)

1. Sélectionnez **+ Ajouter au projet** et choisissez **API**.

![Adobe I/O d&#39;une nouvelle intégration](./images/adobe_io_access_api.png)

Votre écran devrait ressembler à ceci.

![Adobe I/O d&#39;une nouvelle intégration](./images/api1.png)

1. Sélectionnez **Creative Cloud** puis choisissez **Firefly - Services Firefly**, puis sélectionnez **Suivant**.

![Adobe I/O d&#39;une nouvelle intégration](./images/api3.png)

1. Attribuez un nom à vos informations d’identification : `--aepUserLdap-- - Firefly Services OAuth credential`, puis sélectionnez **Suivant**.

![Adobe I/O d&#39;une nouvelle intégration](./images/api4.png)

1. Sélectionnez le profil par défaut **Configuration des services de Firefly par défaut** et sélectionnez **Enregistrer l’API configurée**.

![Adobe I/O d&#39;une nouvelle intégration](./images/api9.png)

Votre intégration Adobe I/O est maintenant prête.

![Adobe I/O d&#39;une nouvelle intégration](./images/api11.png)

## 1.1.1.3 Télécharger l’environnement Postman

1. Sélectionnez **Télécharger pour Postman**, puis choisissez **OAuth serveur à serveur** pour télécharger un environnement Postman.

![Adobe I/O d&#39;une nouvelle intégration](./images/iopm.png)

1. Sélectionnez le nom du projet.

![Adobe I/O d&#39;une nouvelle intégration](./images/api13.png)

1. Sélectionnez **Modifier le projet**.

![Adobe I/O d&#39;une nouvelle intégration](./images/api14.png)

1. Saisissez un nom convivial pour votre intégration : `--aepUserLdap-- Firefly`et sélectionnez **Enregistrer**.

![Adobe I/O d&#39;une nouvelle intégration](./images/api15.png)

La configuration de votre intégration Adobe I/O est maintenant terminée.

![Adobe I/O d&#39;une nouvelle intégration](./images/api16.png)

## 1.1.1.4 l’authentification Postman à l’Adobe I/O

>[!IMPORTANT]
>
>Si vous êtes un employé Adobe, veuillez suivre les instructions ici pour utiliser [PostBuster](./../../../postbuster.md).

1. Téléchargez et installez la version de Postman appropriée à votre système d’exploitation sur [Postman Downloads](https://www.postman.com/downloads/){target="_blank"}.

![Adobe I/O d&#39;une nouvelle intégration](./images/getstarted.png)

1. Démarrez l’application.

Dans Postman, il existe 2 concepts : Environnements et Collections.

- Le fichier d’environnement contient toutes vos variables d’environnement qui sont plus ou moins cohérentes. Dans l’environnement , vous trouverez des éléments tels que l’IMSOrg de votre environnement d’Adobe, ainsi que des informations d’identification de sécurité telles que votre identifiant client et d’autres. Vous avez téléchargé le fichier d’environnement lors de la configuration d’Adobe I/O précédente et il est nommé **`oauth_server_to_server.postman_environment.json`**.

- La collection contient un certain nombre de requêtes d’API que vous pouvez utiliser. Nous utiliserons 2 collections
   - 1 collection pour l’authentification à l’Adobe I/O
   - 1 Collection pour les exercices de ce module

1. Téléchargez [postman.zip](./../../../assets/postman/postman-ff.zip) sur votre bureau local.

![Adobe I/O d&#39;une nouvelle intégration](./images/pmfolder.png)

Dans le fichier **postman.zip** se trouvent les fichiers suivants :

    - `Adobe IO - OAuth.postman_collection.json`
    - `FF - Firefly Services Tech Insiders.postman_collection.json`

1. Décompressez **postman-ff.zip** et stockez les 2 fichiers suivants dans un dossier sur votre bureau :
- Adobe IO - OAuth.postman_collection.json
- FF - Insiders techniques des services Firefly.postman_collection.json
- oauth_server_to_server.postman_environment.json

![Adobe I/O d&#39;une nouvelle intégration](./images/pmfolder1.png)

1. Dans Postman, sélectionnez **Importer**.

![Adobe I/O d&#39;une nouvelle intégration](./images/postmanui.png)

1. Sélectionnez **Fichiers**.

![Adobe I/O d&#39;une nouvelle intégration](./images/choosefiles.png)

1. Sélectionnez les trois fichiers dans le dossier, puis sélectionnez **Ouvrir** et **Importer**.

![Adobe I/O d&#39;une nouvelle intégration](./images/selectfiles.png)

![Adobe I/O d&#39;une nouvelle intégration](./images/impconfirm.png)

Vous disposez désormais de tout ce dont vous avez besoin dans Postman pour commencer à interagir avec les services de Firefly via les API.

## 1.1.1.5 Demander un jeton d’accès

Ensuite, pour vous assurer que vous êtes correctement authentifié, vous devez demander un jeton d’accès.

1. Assurez-vous que l’environnement approprié est sélectionné avant d’exécuter une requête en vérifiant la liste déroulante Environnement dans le coin supérieur droit. L’environnement sélectionné doit porter un nom similaire à celui-ci, `--aepUserLdap-- Firefly Services OAuth Credential`.

![Postman](./images/envselemea1.png)

L’environnement sélectionné doit porter un nom similaire à celui-ci, `--aepUserLdap-- Firefly Services OAuth Credential`.

![Postman](./images/envselemea.png)

Maintenant que votre environnement et vos collections Postman sont configurés et fonctionnent, vous pouvez vous authentifier de Postman à Adobe I/O.

1. Dans la collection **Adobe IO - OAuth**, sélectionnez la requête nommée **POST - Obtenir le jeton d’accès** et sélectionnez **Envoyer**.

Notez que sous **Paramètres de requête**, deux variables sont référencées : `API_KEY` et `CLIENT_SECRET`. Ces variables sont extraites de l’environnement sélectionné, `--aepUserLdap-- Firefly Services OAuth Credential`.

![Postman](./images/ioauth.png)

En cas de réussite, une réponse contenant un jeton porteur, un jeton d’accès et une fenêtre d’expiration s’affiche dans la section **Corps** de Postman.

![Postman](./images/ioauthresp.png)


Vous devriez voir une réponse similaire contenant les informations suivantes :

| Clé | Valeur |
|:-------------:| :---------------:| 
| token_type | **porteur** |
| access_token | **eyJhbGciOiJSU..** |
| expires_in | **86399** |

L’Adobe I/O **bearer-token** a une valeur spécifique (le très long access_token) et une fenêtre d’expiration et est désormais valide pendant 24 heures. Cela signifie qu’au bout de 24 heures, si vous souhaitez utiliser Postman pour vous authentifier sur Adobe I/O, vous devrez générer un nouveau jeton en exécutant à nouveau cette requête.

## API 1.1.1.6 Firefly Services, image Texte 2

Vous êtes maintenant prêt à envoyer votre première requête aux API des services de Firefly.

1. Sélectionnez la requête nommée **POST - Firefly - T2I V3** dans la collection **FF - Services de Firefly Tech Insiders**.

![Firefly ](./images/ff1.png)

1. Copiez l’URL de l’image à partir de la réponse et ouvrez-la dans votre navigateur web pour afficher l’image.

![Firefly ](./images/ff2.png)

Vous devriez voir une belle image représentant `horses in a field`.

![Firefly ](./images/ff3.png)

N’hésitez pas à lire la requête API avant de passer à l’exercice suivant.

## Étapes suivantes

Accédez à [Optimiser le processus de votre Firefly à l’aide de Microsoft Azure et des URL prédéfinies](./ex2.md){target="_blank"}

Revenir à [Présentation des services d’Adobe Firefly ](./firefly-services.md){target="_blank"}

Revenir à [Tous les modules](./../../../overview.md){target="_blank"}
