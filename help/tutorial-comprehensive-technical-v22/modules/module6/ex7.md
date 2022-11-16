---
title: CDP en temps réel - SDK Destinations
description: CDP en temps réel - SDK Destinations
kt: 5342
audience: Data Architect, Orchestration Engineer, Marketer
doc-type: tutorial
activity: develop
exl-id: 9585f858-569b-421e-a21d-aa623cd6c819
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '2386'
ht-degree: 4%

---

# SDK de destinations 6.7

## 6.7.1 Configuration de votre projet Adobe I/O

>[!IMPORTANT]
>
>Si vous avez créé votre projet Adobe I/O après décembre 2021, vous pouvez le réutiliser, ignorer cet exercice et passer immédiatement à l’exercice 6.7.2.
>
>Si vous avez créé votre projet Adobe I/O avant décembre 2021, créez un projet pour vous assurer qu’il est compatible avec l’API de création de destinations.

Dans cet exercice, vous utiliserez l’Adobe I/O de manière très intensive pour effectuer des requêtes sur les API de Platform. Suivez les étapes ci-dessous pour configurer l’Adobe I/O.

Accédez à [https://developer.adobe.com/console/home](https://developer.adobe.com/console/home)

![Adobe I/O d’une nouvelle intégration](../module3/images/iohome.png)

Veillez à sélectionner l’instance Adobe Experience Platform appropriée dans le coin supérieur droit de votre écran. Votre instance est `--envName--`.

![Adobe I/O d’une nouvelle intégration](../module3/images/iocomp.png)

Cliquez sur **Create new project** (Créer un projet). 

![Adobe I/O d’une nouvelle intégration](../module3/images/adobe_io_new_integration.png) ou
![Adobe I/O d’une nouvelle intégration](../module3/images/adobe_io_new_integration1.png)

Sélectionner **+ Ajouter au projet** et sélectionnez **API**.

![Adobe I/O d’une nouvelle intégration](../module3/images/adobe_io_access_api.png)

Vous verrez alors :

![Adobe I/O d’une nouvelle intégration](../module3/images/api1.png)

Cliquez sur le bouton **Adobe Experience Platform** icône .

![Adobe I/O d’une nouvelle intégration](../module3/images/api2.png)

Cliquez sur **API Experience Platform**.

![Adobe I/O d’une nouvelle intégration](../module3/images/api3.png)

Cliquez sur **Suivant**.

![Adobe I/O d’une nouvelle intégration](../module3/images/next.png)

Vous pouvez désormais choisir de faire en sorte qu’Adobe I/O génère votre paire de clés de sécurité ou de télécharger une paire existante.

Choisir **Option 1 - Génération d’une paire de clés**.

![Adobe I/O d’une nouvelle intégration](../module3/images/api4.png)

Cliquez sur **Générer une paire de clés**.

![Adobe I/O d’une nouvelle intégration](../module3/images/generate.png)

Vous verrez un compteur pendant environ 30 secondes.

![Adobe I/O d’une nouvelle intégration](../module3/images/spin.png)

Vous verrez alors ceci, et votre paire de clés générée sera téléchargée sous la forme d’un fichier zip : **config.zip**.

Décompressez le fichier. **config.zip** sur votre bureau, vous verrez qu’il contient 2 fichiers :

![Adobe I/O d’une nouvelle intégration](../module3/images/zip.png)

- **certificate_pub.crt** est votre certificat de clé publique. Du point de vue de la sécurité, il s’agit du certificat librement utilisé pour configurer des intégrations à des applications en ligne.
- **private.key** est votre clé privée. Ça ne devrait jamais, jamais être partagé avec qui que ce soit. La clé privée est ce que vous utilisez pour vous authentifier à votre implémentation d’API et est censée être un secret. Si vous partagez votre clé privée avec n’importe qui, il peut accéder à votre implémentation et utiliser l’API pour ingérer des données malveillantes dans Platform et extraire toutes les données qui se trouvent dans Platform.

![Adobe I/O d’une nouvelle intégration](../module3/images/config.png)

Veillez à enregistrer la variable **config.zip** dans un emplacement sécurisé, car vous en aurez besoin pour les étapes suivantes et pour un accès futur aux API Adobe I/O et Adobe Experience Platform.

Cliquez sur **Suivant**.

![Adobe I/O d’une nouvelle intégration](../module3/images/next.png)

Vous devez maintenant sélectionner la variable **Profil(s) de produit** pour votre intégration.

Sélectionnez les profils de produit requis.

**FYI**: dans votre instance Adobe Experience Platform, les profils de produit auront un nom différent. Vous devez sélectionner au moins un profil de produit avec les droits d’accès appropriés, qui sont configurés dans Adobe Admin Console.

![Adobe I/O d’une nouvelle intégration](../module3/images/api9.png)

Cliquez sur **Enregistrer l’API configurée**.

![Adobe I/O d’une nouvelle intégration](../module3/images/saveconfig.png)

Vous verrez un compteur pendant quelques secondes.

![Adobe I/O d’une nouvelle intégration](../module3/images/api10.png)

Ensuite, vous verrez votre intégration.

![Adobe I/O d’une nouvelle intégration](../module3/images/api11.png)

Cliquez sur le bouton **Téléchargement pour Postman** puis cliquez sur **Compte de service (JWT)** pour télécharger un environnement Postman (patientez jusqu’à ce que l’environnement soit téléchargé, cela peut prendre quelques secondes).

![Adobe I/O d’une nouvelle intégration](../module3/images/iopm.png)

Faites défiler l’écran vers le bas jusqu’à ce que vous voyiez **Compte de service (JWT)**, où vous trouverez tous les détails de l’intégration utilisés pour configurer l’intégration avec Adobe Experience Platform.

![Adobe I/O d’une nouvelle intégration](../module3/images/api12.png)

Votre projet d’E/S a actuellement un nom générique. Vous devez donner un nom convivial à votre intégration. Cliquez sur **Projet 1** (ou nom similaire) comme indiqué

![Adobe I/O d’une nouvelle intégration](../module3/images/api13.png)

Cliquez sur **Modifier le projet**.

![Adobe I/O d’une nouvelle intégration](../module3/images/api14.png)

Saisissez un nom et une description pour votre intégration. Comme convention d’affectation des noms, nous utiliserons `AEP API --demoProfileLdap--`. Remplacez ldap par votre ldap.
Par exemple, si votre ldap est vangeluw, le nom et la description de votre intégration deviennent vangeluw de l’API AEP.

Entrée `AEP API --demoProfileLdap--` comme la propriété **Titre du projet**. Cliquez sur **Enregistrer**.

![Adobe I/O d’une nouvelle intégration](../module3/images/api15.png)

L’intégration de votre Adobe I/O est maintenant terminée.

![Adobe I/O d’une nouvelle intégration](../module3/images/api16.png)

## 6.7.2 Authentification Postman vers Adobe I/O

Accédez à [https://www.getpostman.com/](https://www.getpostman.com/).

Cliquez sur **Prise en main**.

![Adobe I/O d’une nouvelle intégration](../module3/images/getstarted.png)

Ensuite, téléchargez et installez Postman.

![Adobe I/O d’une nouvelle intégration](../module3/images/downloadpostman.png)

Après l’installation de Postman, démarrez l’application.

Dans Postman, il existe deux concepts : Environnements et collections.

- L’environnement contient toutes vos variables d’environnement qui sont plus ou moins cohérentes. Dans l’environnement, vous trouverez des éléments tels que l’IMSOrg de notre environnement Platform, ainsi que des informations d’identification de sécurité telles que votre clé privée et d’autres. Le fichier d’environnement est celui que vous avez téléchargé lors de la configuration de l’Adobe I/O dans l’exercice précédent. Il porte le nom suivant : **service.postman_environment.json**.

- La collection contient un certain nombre de requêtes d’API que vous pouvez utiliser. Nous utiliserons 2 collections
   - 1 collection pour l’authentification pour l’Adobe I/0
   - 1 Collection pour les exercices de ce module
   - 1 collection pour les exercices dans le module Real-Time CDP, pour la création de destination

Téléchargez le fichier [postman.zip](../../assets/postman/postman_profile.zip) sur votre bureau local.

Dans ce **postman.zip** , vous trouverez les fichiers suivants :

- `_Adobe I-O - Token.postman_collection.json`
- `_Adobe Experience Platform Enablement.postman_collection.json`
- `Destination_Authoring_API.json`

Décompressez le fichier **postman.zip** et stockez ces 3 fichiers dans un dossier de votre bureau, ainsi que dans l’environnement Postman téléchargé depuis Adobe I/O. Ce dossier doit contenir les 4 fichiers suivants :

![Adobe I/O d’une nouvelle intégration](../module3/images/pmfolder.png)

Revenez à Postman. Cliquez sur **Importer**.

![Adobe I/O d’une nouvelle intégration](../module3/images/postmanui.png)

Cliquez sur **Chargement de fichiers**.

![Adobe I/O d’une nouvelle intégration](../module3/images/choosefiles.png)

Accédez au dossier de votre bureau dans lequel vous avez extrait les 4 fichiers téléchargés. Sélectionnez ces 4 fichiers en même temps et cliquez sur **Ouvrir**.

![Adobe I/O d’une nouvelle intégration](../module3/images/selectfiles.png)

Après avoir cliqué **Ouvrir**, Postman affiche un aperçu de l’environnement et des collections que vous êtes sur le point d’importer. Cliquez sur **Importer**.

![Adobe I/O d’une nouvelle intégration](../module3/images/impconfirm.png)

Vous avez désormais tout ce dont vous avez besoin dans Postman pour commencer à interagir avec Adobe Experience Platform par le biais des API.

La première chose à faire est de vous assurer que vous êtes correctement authentifié. Pour être authentifié, vous devez demander un jeton d’accès.

Assurez-vous que l’environnement approprié est sélectionné avant d’exécuter une requête. Vous pouvez vérifier l’environnement actuellement sélectionné en vérifiant la liste déroulante Environnement dans le coin supérieur droit.

L’environnement sélectionné doit porter un nom similaire à celui-ci :

![Postman](../module3/images/envselemea.png)

Cliquez sur le bouton **oeil** puis cliquez sur **Modifier** pour mettre à jour la clé privée dans le fichier d’environnement.

![Postman](../module3/images/gear.png)

Vous verrez alors ceci. Tous les champs sont prérenseignés, à l’exception du champ **PRIVATE_KEY**.

![Postman](../module3/images/pk2.png)

La clé privée a été générée lorsque vous avez créé votre projet Adobe I/O. Il a été téléchargé sous la forme d’un fichier zip, nommé **config.zip**. Extrayez ce fichier zip sur votre bureau.

![Postman](../module3/images/pk3.png)

Ouvrir le dossier **config** et ouvrez le fichier **private.key** avec votre éditeur de texte de votre choix.

![Postman](../module3/images/pk4.png)

Vous verrez alors quelque chose qui ressemble à ça, copiez tout le texte dans le presse-papiers.

![Postman](../module3/images/pk5.png)

Revenez à Postman et collez la clé privée dans les champs en regard de la variable . **PRIVATE_KEY**, pour les deux colonnes **VALEUR INITIALE** et **VALEUR ACTUELLE**. Cliquez sur **Enregistrer**.

![Postman](../module3/images/pk6.png)

Votre environnement et vos collections Postman sont maintenant configurés et fonctionnent. Vous pouvez désormais vous authentifier de Postman vers Adobe I/O.

Pour ce faire, vous devez charger une bibliothèque externe qui prendra en charge le cryptage et le décryptage de la communication. Pour charger cette bibliothèque, vous devez exécuter la requête avec le nom . **INIT : Chargement de la bibliothèque de chiffrement pour RS256**. Sélectionnez cette requête dans le **_Adobe I/O - Collection de jetons** et vous le verrez affiché au milieu de votre écran.

![Postman](../module3/images/iocoll.png)

![Postman](../module3/images/cryptolib.png)

Cliquez sur le bouton bleu **Envoyer** bouton . Après quelques secondes, une réponse doit s’afficher dans la variable **Corps** de Postman :

![Postman](../module3/images/cryptoresponse.png)

Une fois la bibliothèque de cryptage chargée, nous pouvons nous authentifier sur Adobe I/O.

Dans le **\_Adobe I/O - Collection de jetons**, sélectionnez la requête avec le nom . **IMS : JWT Generate + Auth**. Là encore, les détails de la requête s’affichent au milieu de l’écran.

![Postman](../module3/images/ioauth.png)

Cliquez sur le bouton bleu **Envoyer** bouton . Après quelques secondes, une réponse doit s’afficher dans la variable **Corps** de Postman :

![Postman](../module3/images/ioauthresp.png)

Si votre configuration a réussi, vous devriez voir une réponse similaire contenant les informations suivantes :

| Clé | Valeur |
|:-------------:| :---------------:| 
| token_type | **porteur** |
| access_token | **eyJ4NXUiOiJpbXNfbmEx...QT7mqZkumN1tdsPEioOEl4087Dg** |
| expires_in | **86399973** |

L&#39;Adobe I/O vous a donné un **porteur**-token, avec une valeur spécifique (ce jeton d’accès très long) et une fenêtre d’expiration.

Le jeton que nous avons reçu est maintenant valide pendant 24 heures. Cela signifie qu’au bout de 24 heures, si vous souhaitez utiliser Postman pour vous authentifier sur Adobe I/O, vous devrez générer un nouveau jeton en exécutant à nouveau cette requête.

## 6.7.3 Définition du point de fin et du format

Pour cet exercice, vous aurez besoin d’un point de terminaison afin que, lorsqu’un segment est admissible, l’événement de qualification puisse être diffusé en continu vers ce point de terminaison. Dans cet exercice, vous utiliserez un exemple de point de terminaison à l’aide de [https://webhook.site/](https://webhook.site/). Accédez à [https://webhook.site/](https://webhook.site/), où vous verrez quelque chose de similaire. Cliquez sur **Copier dans le presse-papiers** pour copier l’URL. Vous devrez spécifier cette URL lors de l’exercice suivant. L’URL de cet exemple est la suivante : `https://webhook.site/e0eb530c-15b4-4a29-8b50-e40877d5490a`.

![Ingestion des données](./images/webhook1.png)

En ce qui concerne le format, nous utiliserons un modèle standard qui diffusera les qualifications ou les qualifications de segments avec des métadonnées telles que les identifiants de client. Les modèles peuvent être personnalisés pour répondre aux attentes de points de terminaison spécifiques, mais dans cet exercice, nous réutiliserons un modèle standard, ce qui entraînera une payload comme celle-ci, qui sera diffusée en continu vers le point de terminaison.

```json
{
  "profiles": [
    {
      "identities": [
        {
          "type": "ecid",
          "id": "64626768309422151580190219823409897678"
        }
      ],
      "AdobeExperiencePlatformSegments": {
        "add": [
          "f58c723c-f1e5-40dd-8c79-7bb4ab47f041"
        ],
        "remove": []
      }
    }
  ]
}
```

## 6.7.4 Création d’une configuration de serveur et de modèle

La première étape de la création de votre propre destination dans Adobe Experience Platform consiste à créer une configuration de serveur et de modèle.

Pour ce faire, accédez à **API de création de destination**, à **Serveurs et modèles de destination** et cliquez pour ouvrir la requête. **POST : création d’une configuration de serveur de destination**. Vous verrez alors ceci. Sous **En-têtes**, vous devez mettre à jour manuellement la valeur de la clé . **x-sandbox-name** et définissez-le sur `--aepSandboxId--`. Sélectionner la valeur **{{SANDBOX_NAME}}**.

![Ingestion des données](./images/sdkpm1.png)

Remplacez-le par `--aepSandboxId--`.

![Ingestion des données](./images/sdkpm2.png)

Ensuite, accédez à **Corps**. sélectionner l’espace réservé **{{body}}**.

![Ingestion des données](./images/sdkpm3.png)

Vous devez maintenant remplacer l’espace réservé. **{{body}}** par le code ci-dessous :

```json
{
    "name": "Custom HTTP Destination",
    "destinationServerType": "URL_BASED",
    "urlBasedDestination": {
        "url": {
            "templatingStrategy": "PEBBLE_V1",
            "value": "yourURL"
        }
    },
    "httpTemplate": {
        "httpMethod": "POST",
        "requestBody": {
            "templatingStrategy": "PEBBLE_V1",
            "value": "{\n    \"profiles\": [\n    {%- for profile in input.profiles %}\n        {\n            \"identities\": [\n            {%- for idMapEntry in profile.identityMap -%}\n            {%- set namespace = idMapEntry.key -%}\n                {%- for identity in idMapEntry.value %}\n                {\n                    \"type\": \"{{ namespace }}\",\n                    \"id\": \"{{ identity.id }}\"\n                }{%- if not loop.last -%},{%- endif -%}\n                {%- endfor -%}{%- if not loop.last -%},{%- endif -%}\n            {% endfor %}\n            ],\n            \"AdobeExperiencePlatformSegments\": {\n                \"add\": [\n                {%- for segment in profile.segmentMembership.ups | added %}\n                    \"{{ segment.key }}\"{%- if not loop.last -%},{%- endif -%}\n                {% endfor %}\n                ],\n                \"remove\": [\n                {#- Alternative syntax for filtering segments by status: -#}\n                {% for segment in removedSegments(profile.segmentMembership.ups) %}\n                    \"{{ segment.key }}\"{%- if not loop.last -%},{%- endif -%}\n                {% endfor %}\n                ]\n            }\n        }{%- if not loop.last -%},{%- endif -%}\n    {% endfor %}\n    ]\n}"
        },
        "contentType": "application/json"
    }
}
```

Après avoir collé le code ci-dessus, vous devez mettre à jour manuellement le champ. **urlBasedDestination.url.value**, et vous devez le définir sur l’URL du webhook que vous avez créé à l’étape précédente, qui était `https://webhook.site/e0eb530c-15b4-4a29-8b50-e40877d5490a` dans cet exemple.

![Ingestion des données](./images/sdkpm4.png)

Après la mise à jour du champ **urlBasedDestination.url.value**, il devrait ressembler à ceci. Cliquez sur **Envoyer**.

![Ingestion des données](./images/sdkpm5.png)

Après avoir cliqué sur **Envoyer**, votre modèle de serveur sera créé. Dans le cadre de la réponse, un champ nommé **instanceId**. Notez-le, car vous en aurez besoin à l’étape suivante. Dans cet exemple, la variable **instanceId** is
`eb0f436f-dcf5-4993-a82d-0fcc09a6b36c`.

![Ingestion des données](./images/sdkpm6.png)

## 6.7.5 Création de votre configuration de destination

Dans Postman, sous **API de création de destination**, accédez à **Paramétrages des destinations** et cliquez pour ouvrir la requête. **POST : création d’une configuration de destination**. Vous verrez alors ceci. Sous **En-têtes**, vous devez mettre à jour manuellement la valeur de la clé . **x-sandbox-name** et définissez-le sur `--aepSandboxId--`. Sélectionner la valeur **{{SANDBOX_NAME}}**.

![Ingestion des données](./images/sdkpm7.png)

Remplacez-le par `--aepSandboxId--`.

![Ingestion des données](./images/sdkpm8.png)

Ensuite, accédez à **Corps**. sélectionner l’espace réservé **{{body}}**.

![Ingestion des données](./images/sdkpm9.png)

Vous devez maintenant remplacer l’espace réservé. **{{body}}** par le code ci-dessous :

```json
{
    "name": "--demoProfileLdap-- - Webhook",
    "description": "Exports segment qualifications and identities to a custom webhook via Destination SDK.",
    "status": "TEST",
    "customerAuthenticationConfigurations": [
        {
            "authType": "BEARER"
        }
    ],
    "customerDataFields": [
        {
            "name": "endpointsInstance",
            "type": "string",
            "title": "Select Endpoint",
            "description": "We could manage several instances across the globe for REST endpoints that our customers are provisioned for. Select your endpoint in the dropdown list.",
            "isRequired": true,
            "enum": [
                "US",
                "EU",
                "APAC",
                "NZ"
            ]
        }
    ],
    "uiAttributes": {
        "documentationLink": "https://experienceleague.adobe.com/docs/experience-platform/destinations/home.html?lang=en",
        "category": "streaming",
        "connectionType": "Server-to-server",
        "frequency": "Streaming"
    },
    "identityNamespaces": {
        "ecid": {
            "acceptsAttributes": true,
            "acceptsCustomNamespaces": false
        }
    },
    "segmentMappingConfig": {
        "mapExperiencePlatformSegmentName": true,
        "mapExperiencePlatformSegmentId": true,
        "mapUserInput": false
    },
    "aggregation": {
        "aggregationType": "BEST_EFFORT",
        "bestEffortAggregation": {
            "maxUsersPerRequest": "1000",
            "splitUserById": false
        }
    },
    "schemaConfig": {
        "profileRequired": false,
        "segmentRequired": true,
        "identityRequired": true
    },
    "destinationDelivery": [
        {
            "authenticationRule": "NONE",
            "destinationServerId": "yourTemplateInstanceID"
        }
    ]
}
```

![Ingestion des données](./images/sdkpm11.png)

Après avoir collé le code ci-dessus, vous devez mettre à jour manuellement le champ. **destinationDelivery. destinationServerId**, et vous devez la définir sur la valeur **instanceId** du modèle de serveur de destination que vous avez créé à l’étape précédente, qui était `eb0f436f-dcf5-4993-a82d-0fcc09a6b36c` dans cet exemple. Cliquez ensuite sur **Envoyer**.

![Ingestion des données](./images/sdkpm10.png)

Vous verrez alors cette réponse.

![Ingestion des données](./images/sdkpm12.png)

Votre destination est maintenant créée dans Adobe Experience Platform. Allons-y et vérifions.

Accédez à [Adobe Experience Platform](https://experience.adobe.com/platform). Une fois connecté, vous accédez à la page d’accueil de Adobe Experience Platform.

![Ingestion des données](../module2/images/home.png)

Avant de continuer, vous devez sélectionner une **sandbox**. L’environnement de test à sélectionner est nommé ``--aepSandboxId--``. Pour ce faire, cliquez sur le texte **[!UICONTROL Production Prod]** dans la ligne bleue en haut de votre écran. Après avoir sélectionné le [!UICONTROL sandbox], vous verrez le changement d’écran et vous êtes maintenant dans votre [!UICONTROL sandbox].

![Ingestion des données](../module2/images/sb1.png)

Dans le menu de gauche, accédez à **Destinations**, cliquez sur **Catalogue** et faites défiler jusqu’à la catégorie **Diffusion en continu**. Vous verrez maintenant votre destination disponible là-bas.

![Ingestion des données](./images/destsdk1.png)

## 6.7.6 Lier votre segment à votre destination

Dans **Destinations** > **Catalogue**, cliquez sur **Configuration** sur votre destination pour commencer à ajouter des segments à votre nouvelle destination.

![Ingestion des données](./images/destsdk2.png)

Saisissez un jeton de support factice, comme **1234**. Cliquez sur **Se connecter à la destination**.

![Ingestion des données](./images/destsdk3.png)

Vous verrez alors ceci. Pour nommer votre destination, utilisez `--demoProfileLdap-- - Webhook`. Sélectionnez un point de terminaison de votre choix, dans cet exemple **UE**. Cliquez sur **Suivant**.

![Ingestion des données](./images/destsdk4.png)

Vous pouvez éventuellement sélectionner une stratégie de gouvernance des données. Cliquez sur **Suivant**.

![Ingestion des données](./images/destsdk5.png)

Sélectionnez le segment que vous avez créé précédemment, qui est nommé `--demoProfileLdap-- - Interest in PROTEUS FITNESS JACKSHIRT`. Cliquez sur **Suivant**.

![Ingestion des données](./images/destsdk6.png)

Vous verrez alors ceci. Veillez à mapper la variable **CHAMP SOURCE** `--aepTenantId--.identification.core.ecid` au champ `Identity: ecid`. Cliquez sur **Suivant**.

![Ingestion des données](./images/destsdk7.png)

Cliquez sur **Terminer**.

![Ingestion des données](./images/destsdk8.png)

Votre destination est maintenant en ligne. De nouvelles qualifications de segment seront diffusées à votre webhook personnalisé.

![Ingestion des données](./images/destsdk9.png)

## 6.7.7 Test de l’activation de votre segment

Accédez à [https://builder.adobedemo.com/projects](https://builder.adobedemo.com/projects). Une fois connecté avec votre Adobe ID, vous verrez ceci. Cliquez sur le projet de votre site web pour l’ouvrir.

![DSN](../module0/images/web8.png)

Vous pouvez maintenant suivre le flux ci-dessous pour accéder au site web. Cliquez sur **Intégrations**.

![DSN](../module0/images/web1.png)

Sur le **Intégrations** , vous devez sélectionner la propriété de collecte de données qui a été créée dans l’exercice 0.1.

![DSN](../module0/images/web2.png)

Vous verrez alors votre site web de démonstration ouvert. Sélectionnez l’URL et copiez-la dans le presse-papiers.

![DSN](../module0/images/web3.png)

Ouvrez une nouvelle fenêtre de navigateur incognito.

![DSN](../module0/images/web4.png)

Collez l’URL de votre site web de démonstration, que vous avez copiée à l’étape précédente. Vous serez alors invité à vous connecter à l’aide de votre Adobe ID.

![DSN](../module0/images/web5.png)

Sélectionnez le type de compte et procédez à la connexion.

![DSN](../module0/images/web6.png)

Votre site web est alors chargé dans une fenêtre de navigateur incognito. Pour chaque démonstration, vous devez utiliser une fenêtre de navigateur incognito actualisée pour charger l’URL de votre site web de démonstration.

![DSN](../module0/images/web7.png)

Dans la **Luma** homepage, accédez à **Hommes**, puis cliquez sur le produit **PROTÉGER UN JACKSHIRT D&#39;AFFICHAGE**.

![Ingestion des données](./images/homenadia.png)

Vous avez maintenant consulté la page de produits pour **PROTÉGER UN JACKSHIRT D&#39;AFFICHAGE**, ce qui signifie que vous serez désormais admissible pour le segment que vous avez créé précédemment dans cet exercice.

![Ingestion des données](./images/homenadiapp.png)

Lorsque vous ouvrez la visionneuse de profils, accédez à **Segments**, vous verrez que le segment est admissible.

![Ingestion des données](./images/homenadiapppb.png)

Revenez à votre webhook ouvert sur [https://webhook.site/](https://webhook.site/), où vous devriez voir une nouvelle requête entrante, qui provient de Adobe Experience Platform et qui contient l’événement de qualification de segment .

![Ingestion des données](./images/destsdk10.png)

Étape suivante : [Résumé et avantages](./summary.md)

[Revenir au module 6](./real-time-cdp-build-a-segment-take-action.md)

[Revenir à tous les modules](../../overview.md)
