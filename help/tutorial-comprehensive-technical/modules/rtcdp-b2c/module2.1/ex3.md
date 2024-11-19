---
title: Foundation - Real-time Customer Profile - Visualisez votre propre profil client en temps réel - API
description: Foundation - Real-time Customer Profile - Visualisez votre propre profil client en temps réel - API
kt: 5342
doc-type: tutorial
exl-id: fe07d873-f4de-437e-815e-e6e6c06a691c
source-git-commit: 3a19e88e820c63294eff38bb8f699a9f690afcb9
workflow-type: tm+mt
source-wordcount: '2295'
ht-degree: 2%

---

# 2.1.3 Visualiser votre propre profil client en temps réel - API

Au cours de cet exercice, vous utiliserez Postman et Adobe I/O pour interroger les API de Adobe Experience Platform afin d’afficher votre propre profil client en temps réel.

## Contexte

Dans Real-time Customer Profile, toutes les données de profil s’affichent avec les données d’événement, ainsi que les appartenances à des segments existants. Les données affichées peuvent provenir de n’importe où, des applications d’Adobe et des solutions externes. Il s’agit de la vue la plus puissante de Adobe Experience Platform, le système d’enregistrement d’expérience.

Le profil client en temps réel peut être utilisé par toutes les applications d’Adobe, mais également par des solutions externes comme les centres d’appels ou les applications client en magasin. Pour ce faire, connectez ces solutions externes aux API Adobe Experience Platform.

## Vos identifiants

Dans le panneau Visionneuse de profils du site web, vous pouvez trouver plusieurs identités. Chaque identité est liée à un espace de noms.

![Profil client](./images/identities.png)

Dans le panneau des rayons X, nous pouvons voir 4 combinaisons différentes d’identifiants et d’espaces de noms :

| Identité | Espace de noms |
|:-------------:| :---------------:|
| Identifiant Experience Cloud (ECID) | 79943948563923140522865572770524243489 |
| Identifiant Experience Cloud (ECID) | 70559351147248820114888181867542007989 |
| Email ID | woutervangeluwe+18112024-01@gmail.com |
| Identifiant du numéro de mobile | +32473622044+18112024-01 |

N’oubliez pas ces identifiants pour l’étape suivante.

## Configuration de votre projet Adobe I/O

Dans cet exercice, vous utiliserez l’Adobe I/O de manière très intensive pour effectuer des requêtes sur les API de Platform. Suivez les étapes ci-dessous pour configurer l’Adobe I/O.

Accédez à [https://developer.adobe.com/console/home](https://developer.adobe.com/console/home)

![Adobe I/O d’une nouvelle intégration](./images/iohome.png)

Veillez à sélectionner l’instance Adobe Experience Platform appropriée dans le coin supérieur droit de votre écran. Votre instance est `--aepImsOrgName--`. Cliquez sur **Créer un projet**.

![Adobe I/O d’une nouvelle intégration](./images/iocomp.png)

Sélectionnez **+ Ajouter au projet** et sélectionnez **API**.

![Adobe I/O d’une nouvelle intégration](./images/adobe_io_access_api.png)

Vous verrez alors :

![Adobe I/O d’une nouvelle intégration](./images/api1.png)

Cliquez sur l’icône **Adobe Experience Platform** .
/images/api2.png)

Sélectionnez **API Experience Platform** et cliquez sur **Suivant**.

![Adobe I/O d’une nouvelle intégration](./images/api3.png)

Vous allez maintenant voir ceci. Attribuez un nom à vos informations d’identification : `--aepUserLdap-- - OAuth credential`. Cliquez sur **Suivant**.

![Adobe I/O d’une nouvelle intégration](./images/api4.png)

Ensuite, vous devez sélectionner un profil de produit qui définira les autorisations disponibles pour cette intégration.

Sélectionnez les profils de produit requis.

>[!NOTE]
>
> Les noms des profils de produit varient dans votre instance Adobe Experience Platform, car il s’agit de spefici de l’instance. Vous devez sélectionner au moins un profil de produit avec les droits d’accès appropriés, qui sont configurés dans Adobe Admin Console et l’interface utilisateur des autorisations AEP.

Cliquez sur **Enregistrer l’API configurée**.

![Adobe I/O d’une nouvelle intégration](./images/api9.png)

Votre intégration d’Adobe I/O est maintenant prête.

![Adobe I/O d’une nouvelle intégration](./images/api11.png)

Cliquez sur le bouton **Télécharger pour Postman** , puis sur **OAuth Server-to-Server** pour télécharger un environnement Postman (attendez que l’environnement soit téléchargé, ce qui peut prendre quelques secondes).

![Adobe I/O d’une nouvelle intégration](./images/iopm.png)

Votre projet d’E/S a actuellement un nom générique. Vous devez donner un nom convivial à votre intégration. Cliquez sur **Projet X** (ou un nom similaire) comme indiqué

![Adobe I/O d’une nouvelle intégration](./images/api13.png)

Cliquez sur **Modifier le projet**.

![Adobe I/O d’une nouvelle intégration](./images/api14.png)

Saisissez un Nom et une Description pour votre intégration : `--aepUserLdap-- AEP Tutorial`.

Cliquez sur **Enregistrer**.

![Adobe I/O d’une nouvelle intégration](./images/api15.png)

L’intégration de votre Adobe I/O est maintenant terminée.

![Adobe I/O d’une nouvelle intégration](./images/api16.png)

>[!NOTE]
>
>Il existe une étape supplémentaire pour s’assurer que ce projet Adobe I/O a accès aux paramètres d’autorisation Adobe Experience Platform. Les informations d’identification d’API de votre projet doivent être ajoutées dans l’interface utilisateur Autorisations de Adobe Experience Platform, pour laquelle des droits d’accès d’administrateur système sont requis. Les étapes sont décrites ci-dessous, mais vous devrez peut-être contacter votre administrateur système pour que cela soit traité pour vous si vous ne disposez pas des droits d’accès requis.

## Autorisations AEP pour les informations d’identification d’API

Accédez à [Adobe Experience Platform](https://experience.adobe.com/platform). Une fois connecté, vous accédez à la page d’accueil de Adobe Experience Platform.

Accédez à **Permissions**, à **Roles**, puis cliquez sur le profil de produit approprié.

>[!NOTE]
>
> Les noms des profils de produit varient dans votre instance Adobe Experience Platform, car il s’agit de spefici de l’instance. Vous devez sélectionner au moins un profil de produit avec les droits d’accès appropriés, qui sont configurés dans Adobe Admin Console et l’interface utilisateur des autorisations AEP.

![Autorisations](./images/perm1.png)

Cliquez sur **Informations d’identification de l’API**.

![Autorisations](./images/perm2.png)

Cliquez sur **+ Ajouter les informations d’identification d’API**.

![Autorisations](./images/perm3.png)

Sélectionnez le projet d’Adobe I/O nouvellement créé et cliquez sur **Enregistrer**.

![Autorisations](./images/perm4.png)

## Authentification Postman à Adobe I/O

Accédez à [https://www.postman.com/downloads/](https://www.postman.com/downloads/).

Téléchargez et installez la version appropriée de Postman pour votre système d’exploitation.

![Adobe I/O d’une nouvelle intégration](./images/getstarted.png)

Après l’installation de Postman, démarrez l’application.

Dans Postman, il existe deux concepts : Environnements et Collections.

- L’environnement contient toutes vos variables d’environnement qui sont plus ou moins cohérentes. Dans l’environnement, vous trouverez des éléments tels que l’IMSOrg de notre environnement Platform, ainsi que des informations d’identification de sécurité telles que votre clé privée et d’autres. Le fichier d’environnement est celui que vous avez téléchargé lors de la configuration de l’Adobe I/O dans l’exercice précédent. Il s’appelle comme suit : **`oauth_server_to_server.postman_environment.json`**.

- La collection contient un certain nombre de requêtes d’API que vous pouvez utiliser. Nous utiliserons 2 collections
   - 1 collection pour l’authentification pour Adobe I/0
   - 1 Collection pour les exercices de ce module
   - 1 collection pour les exercices dans le module Real-Time CDP, pour la création de destination

Téléchargez le fichier [postman.zip](./../../../assets/postman/postman_profile.zip) sur votre bureau local.

Dans ce fichier **postman.zip**, vous trouverez les fichiers suivants :

- `Adobe IO - OAuth.postman_collection.json`
- `AEP Tutorial.postman_collection.json`
- `Destination_Authoring_API.json`

Décompressez le fichier **postman.zip** et stockez ces 3 fichiers dans un dossier sur votre bureau, ainsi que dans l’environnement Postman téléchargé depuis Adobe I/O. Ce dossier doit contenir les 4 fichiers suivants :

![Adobe I/O d’une nouvelle intégration](./images/pmfolder.png)

Revenez à Postman. Cliquez sur **Importer**.

![Adobe I/O d’une nouvelle intégration](./images/postmanui.png)

Cliquez sur **files**.

![Adobe I/O d’une nouvelle intégration](./images/choosefiles.png)

Accédez au dossier de votre bureau dans lequel vous avez extrait les 4 fichiers téléchargés. Sélectionnez ces 4 fichiers en même temps et cliquez sur **Ouvrir**.

![Adobe I/O d’une nouvelle intégration](./images/selectfiles.png)

Après avoir cliqué sur **Ouvrir**, Postman vous présente un aperçu de l’environnement et des collections que vous êtes sur le point d’importer. Cliquez sur **Importer**.

![Adobe I/O d’une nouvelle intégration](./images/impconfirm.png)

Vous avez désormais tout ce dont vous avez besoin dans Postman pour commencer à interagir avec Adobe Experience Platform par le biais des API.

La première chose à faire est de vous assurer que vous êtes correctement authentifié. Pour être authentifié, vous devez demander un jeton d’accès.

Assurez-vous que l’environnement approprié est sélectionné avant d’exécuter une requête. Vous pouvez vérifier l’environnement actuellement sélectionné en vérifiant la liste déroulante Environnement dans le coin supérieur droit.

L’environnement sélectionné doit avoir un nom similaire à celui-ci, `--aepUserLdap-- OAuth Credential`.

![Postman](./images/envselemea.png)

Votre environnement et vos collections Postman sont maintenant configurés et fonctionnent. Vous pouvez désormais vous authentifier de Postman vers Adobe I/O.

Dans la collection **Adobe IO - OAuth**, sélectionnez la requête avec le nom **POST - Obtenir le jeton d’accès**. Cliquez sur **Envoyer**.

![Postman](./images/ioauth.png)

Au bout de quelques secondes, une réponse devrait s’afficher dans la section **Body** de Postman :

![Postman](./images/ioauthresp.png)

Si votre configuration a réussi, vous devriez voir une réponse similaire contenant les informations suivantes :

| Clé | Valeur |
|:-------------:| :---------------:| 
| token_type | **bearer** |
| access_token | **eyJhbGciOiJSU...jrNZ6mdaQ** |
| expires_in | **86399** |

Adobe I/O vous a donné un jeton **porteur**, avec une valeur spécifique (le très long access_token) et une fenêtre d&#39;expiration.

Le jeton que nous avons reçu est maintenant valide pendant 24 heures. Cela signifie qu’au bout de 24 heures, si vous souhaitez utiliser Postman pour vous authentifier sur Adobe I/O, vous devrez générer un nouveau jeton en exécutant à nouveau cette requête.

## API Real-time Customer Profile, schéma : Profil

Vous pouvez maintenant envoyer votre première requête aux API Real-time Customer Profile de Platform.

Dans Postman, recherchez la collection **Tutoriel AEP**.

![Postman](./images/coll_enablement.png)

Dans **1. Unified Profile Service**, cliquez sur la première requête avec le nom **UPS - GET Profile by Entity ID &amp; NS**.

![Postman](./images/upscall.png)

Pour cette requête, trois variables sont requises :

| Clé | Valeur | Définition |
|:-------------:| :---------------:| :---------------:| 
| entityId | **identifiant** | l’ID de client spécifique ; |
| entityIdNS | **espace de noms** | l’espace de noms spécifique qui s’applique à l’ID ; |
| schema.name | **_xdm.context.profile** | le schéma spécifique pour lequel vous souhaitez recevoir des informations ; |

Ainsi, si vous souhaitez demander aux API Adobe Experience Platform de vous renvoyer toutes les informations de profil pour votre propre ECID, vous devez configurer la requête comme suit :

| Clé | Valeur |
|:-------------:| :---------------:| 
| entityId | **yourECID** |
| entityIdNS | **ecid** |
| schema.name | **_xdm.context.profile** |

![Postman](./images/callecid.png)

Vous devez également vérifier les champs **Header** - de votre requête. Accédez à **En-têtes**. Vous verrez alors :

![Postman](./images/callecidheaders.png)

>[!NOTE]
>
>Vous devez spécifier le nom de l’environnement de test Adobe Experience Platform que vous utilisez. Votre x-sandbox-name doit être `--aepSandboxName--`.

| Clé | Valeur |
| ----------- | ----------- |
| x-sandbox-name | `--aepSandboxName--` |



Une fois que vous avez coché le nom de l’environnement de test, cliquez sur **Envoyer** pour envoyer votre demande à Platform.

Vous devriez obtenir une réponse immédiate de Platform, qui vous montre quelque chose comme ceci :

![Postman](./images/callecidresponse.png)

Voici la réponse complète de Platform :

```javascript
{
    "A2_ETHkJxMvxbiEmIZlAj8Qn": {
        "entityId": "A2_ETHkJxMvxbiEmIZlAj8Qn",
        "mergePolicy": {
            "id": "64e4b0ed-dfc3-4084-8e67-643e977168d7"
        },
        "sources": [
            "672a10cdb015162aefedfc0f",
            "672a10b1a05e282aee19737c"
        ],
        "tags": [
            "0938B898-469A-4513-8E86-87464307120F:va7",
            "3ba34930-405e-4b31-aafa-bac22d35203e:va7"
        ],
        "identityGraph": [
            "G7z3JAFBY4I6Rzg",
            "A2_ETHkJxMvxbiEmIZlAj8Qn",
            "BkFvK4QcJpSPByuDGF4UAS0wMQ",
            "BUF9zMKLrXq72p4HpbsHv1SDGF4UAS0wMUBnbWFpbC5jb20",
            "A29btmFXmrfrYbXQWISCT9ZD"
        ],
        "entity": {
            "_experienceplatform": {
                "identification": {
                    "core": {
                        "ecid": "79943948563923140522865572770524243489",
                        "phoneNumber": "+32473622044+18112024-01",
                        "email": "woutervangeluwe+18112024-01@gmail.com"
                    }
                }
            },
            "userAccount": {
                "ID": "3688250"
            },
            "pushNotificationDetails": [
                {
                    "denylisted": false,
                    "token": "2E0945F186CE5ED8CBFD1EB519A8CF38BA2B28A67FB381D45AA15EE37D289214",
                    "identity": {
                        "namespace": {
                            "code": "ECID"
                        },
                        "id": "70559351147248820114888181867542007989"
                    },
                    "platform": "apns",
                    "appID": "com.adobe.demosystem.dxdemo"
                }
            ],
            "personalEmail": {
                "address": "woutervangeluwe+18112024-01@gmail.com"
            },
            "_repo": {
                "createDate": "2024-11-18T10:39:12.296Z"
            },
            "extSourceSystemAudit": {
                "lastUpdatedDate": "2024-11-19T07:46:52.001Z"
            },
            "testProfile": true,
            "mobilePhone": {
                "number": "+32473622044"
            },
            "consents": {
                "metadata": {
                    "time": "2024-11-19T07:46:52.001Z"
                },
                "idSpecific": {
                    "ECID": {
                        "70559351147248820114888181867542007989": {
                            "collect": {
                                "val": "y"
                            }
                        }
                    }
                }
            },
            "person": {
                "name": {
                    "lastName": "Van Geluwe",
                    "firstName": "Wouter"
                }
            },
            "userActivityRegions": {
                "IRL1": {
                    "captureTimestamp": "2024-11-19T07:46:51.239Z"
                }
            },
            "identityMap": {
                "ecid": [
                    {
                        "id": "70559351147248820114888181867542007989"
                    },
                    {
                        "id": "79943948563923140522865572770524243489"
                    }
                ],
                "email": [
                    {
                        "id": "woutervangeluwe+18112024-01@gmail.com"
                    }
                ],
                "phone": [
                    {
                        "id": "+32473622044+18112024-01"
                    }
                ],
                "userid": [
                    {
                        "id": "3688250"
                    }
                ]
            }
        },
        "lastModifiedAt": "2024-11-19T07:47:23Z"
    }
}
```

Il s’agit actuellement de toutes les données de profil disponibles dans Platform pour cet ECID.

Vous n’êtes pas tenu d’utiliser l’ECID pour demander des données de profil auprès du profil client en temps réel de Platform. Vous pouvez utiliser n’importe quel identifiant dans n’importe quel espace de noms pour demander ces données.

Revenons à Postman et prétendons que nous sommes le centre d’appel, et envoyons une demande à Platform spécifiant l’espace de noms **Phone** et votre numéro de mobile.

Ainsi, si vous souhaitez demander aux API de Platform de vous renvoyer toutes les informations de profil pour un téléphone spécifique, vous devez configurer la requête comme suit :

| Clé | Valeur |
|:-------------:| :---------------:| 
| entityId | **votre numéro de téléphone** |
| entityIdNS | **phone** (remplacez ecid par phone) |
| schema.name | **_xdm.context.profile** |

Si votre numéro de téléphone contient des symboles spéciaux tels que **+**, vous devez sélectionner votre numéro de téléphone complet, cliquer avec le bouton droit de la souris et cliquer sur **EncodeURIComponent**.

![Postman](./images/encodephone.png)

Vous obtiendrez alors ce qui suit :

![Postman](./images/callmobilenr.png)

Vous devez également vérifier les champs **Header** - de votre requête. Accédez à **En-têtes**. Vous verrez alors :

![Postman](./images/callecidheaders.png)

>[!NOTE]
>
>Vous devez spécifier le nom de l’environnement de test Adobe Experience Platform que vous utilisez. Votre x-sandbox-name doit être `--aepSandboxName--`.

| Clé | Valeur |
| ----------- | ----------- |
| x-sandbox-name | `--aepSandboxName--` |


Cliquez sur **Envoyer** et vérifiez la réponse. Vous constaterez qu’elle est identique à celle d’avant lorsque vous utilisiez l’ECID comme identité.

![Postman](./images/callmobilenrresponse.png)

Faisons la même chose pour votre adresse électronique en spécifiant l’espace de noms **email** et votre adresse électronique.

Ainsi, si vous souhaitez demander aux API de Platform de vous renvoyer toutes les informations de profil pour une adresse électronique spécifique, vous devez configurer la requête comme suit :

| Clé | Valeur |
|:-------------:| :---------------:| 
| entityId | **youremail** |
| entityIdNS | **email** (remplacer Téléphone par email) |
| schema.name | **_xdm.context.profile** |

Si votre adresse électronique contient des symboles spéciaux tels que **+**, vous devez sélectionner votre adresse électronique complète, cliquer avec le bouton droit de la souris et cliquer sur **EncodeURIComponent**.

![Postman](./images/encodeemail.png)

Vous obtiendrez alors ce qui suit :

![Postman](./images/callemail.png)

Vous devez également vérifier les champs **Header** - de votre requête. Accédez à **En-têtes**. Vous verrez alors :

>[!NOTE]
>
>Vous devez spécifier le nom de l’environnement de test Adobe Experience Platform que vous utilisez. Votre x-sandbox-name doit être `--aepSandboxName--`.

![Postman](./images/callecidheaders.png)

| Clé | Valeur |
| ----------- | ----------- |
| x-sandbox-name | `--aepSandboxName--` |

Cliquez sur **Envoyer** et vérifiez la réponse. Vous verrez à nouveau que c’est la même chose qu’auparavant avec l’ECID et le numéro de téléphone.

![Postman](./images/callemailresponse.png)

C&#39;est un type de flexibilité très important qui est offert aux marques. Cela signifie que tout environnement peut envoyer une requête à Platform, à l’aide de son propre ID et de son propre espace de noms, sans avoir à comprendre la complexité de plusieurs espaces de noms et ID.

Par exemple :

- Le centre d’appels peut demander des données à Platform à l’aide de l’espace de noms **phone**
- Loyalty System peut demander des données à Platform à l’aide de l’espace de noms **email**
- les applications en ligne peuvent utiliser l’espace de noms **ecid**

Le centre d’appels ne sait pas nécessairement quel type d’identifiant est utilisé dans le système de fidélité et le système de fidélité ne sait pas nécessairement quel type d’identifiant est utilisé par les applications en ligne. Chaque système peut utiliser les informations qu&#39;il a et qu&#39;il comprend pour obtenir les informations dont il a besoin, quand il en a besoin.

## API Real-time Customer Profile, schéma : Profile et ExperienceEvent

Après avoir interrogé les API de Platform avec succès pour les données de profil, faisons maintenant de même avec les données ExperienceEvent.

Dans Postman, recherchez la collection **Tutoriel AEP**.

![Postman](./images/coll_enablement.png)

Dans **1. Unified Profile Service**, sélectionnez la seconde requête avec le nom **UPS - GET Profile &amp; EE par Entity ID &amp; NS**.

![Postman](./images/upseecall.png)

Pour cette requête, il existe quatre variables requises :

| Clé | Valeur | Définition |
|:-------------:| :---------------:|  :---------------:| 
| schema.name | **_xdm.context.experienceevent** | le schéma spécifique pour lequel vous souhaitez recevoir des informations. Dans ce cas, nous recherchons des données mappées sur le schéma ExperienceEvent. |
| relatedSchema.name | **_xdm.context.profile** | Lors de la recherche de données mappées sur le schéma ExperienceEvent, nous devons spécifier une identité pour laquelle nous voulons recevoir ces données. Le schéma qui a accès à l’identité est le schéma-profil, de sorte que le schéma-associé ici est le schéma-profil. |
| relatedEntityId | **identifiant** | ID de client spécifique |
| relatedEntityIdNS | **espace de noms** | l’espace de noms spécifique qui s’applique à l’ID ; |

Ainsi, si vous souhaitez demander aux API de Platform de vous renvoyer toutes les informations de profil pour votre propre ecid, vous devez configurer la requête comme suit :

| Clé | Valeur |
|:-------------:| :---------------:| 
| schema.name | **_xdm.context.experienceevent** |
| relatedSchema.name | **_xdm.context.profile** |
| relatedEntityId | **yourECID** |
| relatedEntityIdNS | **ecid** |

![Postman](./images/eecallecid.png)

Vous devez également vérifier les champs **Header** - de votre requête. Accédez à **En-têtes**. Vous verrez alors :

![Postman](./images/eecallecidheaders.png)

>[!NOTE]
>
>Vous devez spécifier le nom de l’environnement de test Adobe Experience Platform que vous utilisez. Votre x-sandbox-name doit être `--aepSandboxName--`.

| Clé | Valeur |
| ----------- | ----------- |
| x-sandbox-name | `--aepSandboxName--` |

Cliquez sur **Envoyer** pour envoyer votre demande à Platform.

Vous devriez obtenir une réponse immédiate de Platform, qui vous montre quelque chose comme ceci :

![Postman](./images/eecallecidresponse.png)

Vous trouverez ci-dessous la réponse complète de Platform. Dans cet exemple, huit ExperienceEvent sont liés à l’ECID de ce client. Consultez les variables ci-dessous pour afficher les différentes variables sur la requête, car ce que vous voyez ci-dessous est la conséquence directe de votre configuration dans Launch dans les exercices précédents.

En outre, lorsque le panneau de rayons X affiche des informations ExperienceEvent, il utilise la payload ci-dessous pour analyser et récupérer les informations telles que Nom du produit (rechercher productName dans la payload ci-dessous) et URL de l’image du produit (rechercher productImageUrl dans la payload ci-dessous).

```javascript
{
    "_page": {
        "orderby": "timestamp",
        "start": "b1325606-9b96-4e51-b7dd-73aacf527c72-0",
        "count": 14,
        "next": ""
    },
    "children": [
        {
            "relatedEntityId": "A2_ETHkJxMvxbiEmIZlAj8Qn",
            "entityId": "b1325606-9b96-4e51-b7dd-73aacf527c72-0",
            "sourceId": "672a10b1074ceb2af0aa7034",
            "timestamp": 1731923802848,
            "entity": {
                "environment": {
                    "ipV4": "141.134.241.99",
                    "type": "browser",
                    "browserDetails": {
                        "userAgentClientHints": {
                            "mobile": false,
                            "platform": "macOS",
                            "brands": [
                                {
                                    "brand": "Chromium",
                                    "version": "130"
                                },
                                {
                                    "brand": "Google Chrome",
                                    "version": "130"
                                },
                                {
                                    "brand": "Not?A_Brand",
                                    "version": "99"
                                }
                            ]
                        },
                        "userAgent": "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/130.0.0.0 Safari/537.36",
                        "viewportHeight": 992,
                        "viewportWidth": 1920
                    }
                },
                "web": {
                    "webPageDetails": {
                        "name": "Home",
                        "viewName": "Home",
                        "pageViews": {
                            "value": 1
                        },
                        "URL": "https://dsn.adobe.com/web/vangeluw-QIMU"
                    },
                    "webReferrer": {
                        "URL": "https://auth.services.adobe.com/"
                    }
                },
                "_experienceplatform": {
                    "interactionDetails": {
                        "core": {
                            "channel": "web"
                        }
                    },
                    "demoEnvironment": {
                        "brandName": "vangeluw-QIMU"
                    },
                    "identification": {
                        "core": {
                            "ecid": "79943948563923140522865572770524243489"
                        }
                    }
                },
                "implementationDetails": {
                    "name": "https://ns.adobe.com/experience/alloy/reactor",
                    "version": "2.24.0+2.27.0",
                    "environment": "browser"
                },
                "identityMap": {
                    "ECID": [
                        {
                            "id": "79943948563923140522865572770524243489",
                            "authenticatedState": "ambiguous",
                            "primary": true
                        }
                    ]
                },
                "eventType": "web.webpagedetails.pageViews",
                "_id": "b1325606-9b96-4e51-b7dd-73aacf527c72-0",
                "placeContext": {
                    "localTime": "2024-11-18T10:56:42.848+01:00",
                    "localTimezoneOffset": -60
                },
                "device": {
                    "screenOrientation": "landscape",
                    "screenWidth": 1920,
                    "screenHeight": 1080
                },
                "timestamp": "2024-11-18T09:56:42.848Z"
            },
            "lastModifiedAt": "2024-11-18T09:56:45Z"
        },
    "_links": {
        "next": {
            "href": ""
        }
    }
}
```

Il s’agit actuellement de toutes les données ExperienceEvent disponibles dans Platform pour cet ECID.

Vous n’avez pas besoin d’utiliser l’ECID pour demander des données ExperienceEvent à Adobe Experience Platform Real-time Profile. Vous pouvez utiliser n’importe quel identifiant dans n’importe quel espace de noms pour demander ces données.

Étape suivante : [2.1.4 Création d’un segment - IU](./ex4.md)

[Revenir au module 2.1](./real-time-customer-profile.md)

[Revenir à tous les modules](../../../overview.md)
