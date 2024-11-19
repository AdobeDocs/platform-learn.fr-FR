---
title: CDP en temps réel - SDK Destinations
description: CDP en temps réel - SDK Destinations
kt: 5342
doc-type: tutorial
exl-id: 5606ca2f-85ce-41b3-80f9-3c137f66a8c0
source-git-commit: 3a19e88e820c63294eff38bb8f699a9f690afcb9
workflow-type: tm+mt
source-wordcount: '1049'
ht-degree: 6%

---

# SDK de destinations 2.3.7

## Configuration de votre projet d’Adobe I/O

Au cours de cet exercice, vous utiliserez à nouveau Adobe I/O pour interroger les API de Adobe Experience Platform. Si vous n’avez pas encore configuré votre projet d’Adobe I/O, revenez à l’ [exercice 3 dans le module 2.1](../module2.1/ex3.md) et suivez les instructions qui s’y rapportent.

## Authentification Postman à Adobe I/O

Au cours de cet exercice, vous utiliserez à nouveau Postman pour interroger les API de Adobe Experience Platform. Si vous n’avez pas encore configuré votre application Postman, revenez à l’ [exercice 3 dans le module 2.1](../module2.1/ex3.md) et suivez les instructions qui s’y rapportent.

## Définition du point de fin et du format

Pour cet exercice, vous aurez besoin d’un point de terminaison afin que, lorsqu’un segment est admissible, l’événement de qualification puisse être diffusé en continu vers ce point de terminaison. Dans cet exercice, vous utiliserez un exemple de point de terminaison à l’aide de [https://webhook.site/](https://webhook.site/). Accédez à [https://webhook.site/](https://webhook.site/), où vous trouverez quelque chose de similaire. Cliquez sur **Copier dans le presse-papiers** pour copier l’URL. Vous devrez spécifier cette URL lors de l’exercice suivant. L’URL dans cet exemple est `https://webhook.site/e0eb530c-15b4-4a29-8b50-e40877d5490a`.

![Ingestion des données](./images/webhook1.png)

En ce qui concerne le format, nous utiliserons un modèle standard qui diffusera les qualifications ou les qualifications de segments avec des métadonnées telles que les identifiants de client. Les modèles peuvent être personnalisés pour répondre aux attentes de points de terminaison spécifiques, mais dans cet exercice, nous réutiliserons un modèle standard, ce qui entraînera une payload comme celle-ci, qui sera diffusée en continu vers le point de terminaison .

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

## Créer une configuration de serveur et de modèle

La première étape de la création de votre propre destination dans Adobe Experience Platform consiste à créer une configuration de serveur et de modèle.

Pour ce faire, accédez à **API de création de destination**, à **Serveurs et modèles de destination** et cliquez pour ouvrir la requête **POST - Créer une configuration de serveur de destination**. Vous verrez alors ceci. Sous **Headers**, vous devez mettre à jour manuellement la valeur de la clé **x-sandbox-name** et la définir sur `--aepSandboxName--`. Sélectionnez la valeur **{{SANDBOX_NAME}}**.

![Ingestion des données](./images/sdkpm1.png)

Remplacez-le par `--aepSandboxName--`.

![Ingestion des données](./images/sdkpm2.png)

Ensuite, accédez à **Body**. sélectionnez l’espace réservé **{{body}}**.

![Ingestion des données](./images/sdkpm3.png)

Vous devez maintenant remplacer l’espace réservé **{{body}}** par le code ci-dessous :

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

Après avoir collé le code ci-dessus, vous devez mettre à jour manuellement le champ **urlBasedDestination.url.value** et vous devez le définir sur l’URL du webhook que vous avez créé à l’étape précédente, `https://webhook.site/e0eb530c-15b4-4a29-8b50-e40877d5490a` dans cet exemple.

![Ingestion des données](./images/sdkpm4.png)

Après la mise à jour du champ **urlBasedDestiantion.url.value**, il doit ressembler à ceci. Cliquez sur **Envoyer**.

![Ingestion des données](./images/sdkpm5.png)

Après avoir cliqué sur **Envoyer**, votre modèle de serveur est créé. Dans le cadre de la réponse, un champ nommé **instanceId** s’affiche. Notez-le, car vous en aurez besoin à l’étape suivante. Dans cet exemple, **instanceId** est
`eb0f436f-dcf5-4993-a82d-0fcc09a6b36c`.

![Ingestion des données](./images/sdkpm6.png)

## Création de votre configuration de destination

Dans Postman, sous **API de création de destination**, accédez à **Configurations de destination** et cliquez pour ouvrir la requête **POST - Créer une configuration de destination**. Vous verrez alors ceci. Sous **Headers**, vous devez mettre à jour manuellement la valeur de la clé **x-sandbox-name** et la définir sur `--aepSandboxName--`. Sélectionnez la valeur **{{SANDBOX_NAME}}**.

![Ingestion des données](./images/sdkpm7.png)

Remplacez-le par `--aepSandboxName--`.

![Ingestion des données](./images/sdkpm8.png)

Ensuite, accédez à **Body**. sélectionnez l’espace réservé **{{body}}**.

![Ingestion des données](./images/sdkpm9.png)

Vous devez maintenant remplacer l’espace réservé **{{body}}** par le code ci-dessous :

```json
{
    "name": "--aepUserLdap-- - Webhook",
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

Après avoir collé le code ci-dessus, vous devez mettre à jour manuellement le champ **destinationDelivery. destinationServerId** et vous devez le définir sur l’ **instanceId** du modèle de serveur de destination que vous avez créé à l’étape précédente, qui était `eb0f436f-dcf5-4993-a82d-0fcc09a6b36c` dans cet exemple. Cliquez ensuite sur **Send**.

![Ingestion des données](./images/sdkpm10.png)

Vous verrez alors cette réponse.

![Ingestion des données](./images/sdkpm12.png)

Votre destination est maintenant créée dans Adobe Experience Platform. Allons-y et vérifions.

Accédez à [Adobe Experience Platform](https://experience.adobe.com/platform). Une fois connecté, vous accédez à la page d’accueil de Adobe Experience Platform.

![Ingestion des données](./../../../modules/datacollection/module1.2/images/home.png)

Avant de continuer, vous devez sélectionner un **sandbox**. L’environnement de test à sélectionner est nommé ``--aepSandboxName--``. Pour ce faire, cliquez sur le texte **[!UICONTROL Production Prod]** dans la ligne bleue en haut de votre écran. Après avoir sélectionné l’[!UICONTROL sandbox] approprié, vous verrez le changement d’écran et vous êtes désormais dans votre [!UICONTROL sandbox] dédié.

![Ingestion des données](./../../../modules/datacollection/module1.2/images/sb1.png)

Dans le menu de gauche, accédez à **Destinations**, cliquez sur **Catalogue** et faites défiler l’écran jusqu’à la catégorie **Diffusion en continu**. Vous verrez maintenant votre destination disponible là-bas.

![Ingestion des données](./images/destsdk1.png)

## Lier votre segment à votre destination

Dans **Destinations** > **Catalogue**, cliquez sur **Configurer** sur votre destination pour commencer à ajouter des segments à votre nouvelle destination.

![Ingestion des données](./images/destsdk2.png)

Saisissez un jeton de support factice, tel que **1234**. Cliquez sur **Se connecter à la destination**.

![Ingestion des données](./images/destsdk3.png)

Vous verrez alors ceci. Pour nommer votre destination, utilisez `--aepUserLdap-- - Webhook`. Sélectionnez un point de terminaison de votre choix, dans cet exemple **EU**. Cliquez sur **Suivant**.

![Ingestion des données](./images/destsdk4.png)

Vous pouvez éventuellement sélectionner une stratégie de gouvernance des données. Cliquez sur **Suivant**.

![Ingestion des données](./images/destsdk5.png)

Sélectionnez le segment que vous avez créé précédemment, nommé `--aepUserLdap-- - Interest in PROTEUS FITNESS JACKSHIRT`. Cliquez sur **Suivant**.

![Ingestion des données](./images/destsdk6.png)

Vous verrez alors ceci. Veillez à mapper le **CHAMP SOURCE** `--aepTenantId--.identification.core.ecid` au champ `Identity: ecid`. Cliquez sur **Suivant**.

![Ingestion des données](./images/destsdk7.png)

Cliquez sur **Terminer**.

![Ingestion des données](./images/destsdk8.png)

Votre destination est maintenant en ligne. De nouvelles qualifications de segment seront diffusées à votre webhook personnalisé.

![Ingestion des données](./images/destsdk9.png)

## Test de votre activation de segment

Accédez à [https://builder.adobedemo.com/projects](https://builder.adobedemo.com/projects). Une fois connecté avec votre Adobe ID, vous verrez ceci. Cliquez sur le projet de votre site web pour l’ouvrir.

![DSN](../../gettingstarted/gettingstarted/images/web8.png)

Vous pouvez maintenant suivre le flux ci-dessous pour accéder au site web. Cliquez sur **Intégrations**.

![DSN](../../gettingstarted/gettingstarted/images/web1.png)

Sur la page **Intégrations**, vous devez sélectionner la propriété de collecte de données qui a été créée dans l’exercice 0.1.

![DSN](../../gettingstarted/gettingstarted/images/web2.png)

Vous verrez alors votre site web de démonstration ouvert. Sélectionnez l’URL et copiez-la dans le presse-papiers.

![DSN](../../gettingstarted/gettingstarted/images/web3.png)

Ouvrez une nouvelle fenêtre de navigateur incognito.

![DSN](../../gettingstarted/gettingstarted/images/web4.png)

Collez l’URL de votre site web de démonstration, que vous avez copiée à l’étape précédente. Vous serez alors invité à vous connecter à l’aide de votre Adobe ID.

![DSN](../../gettingstarted/gettingstarted/images/web5.png)

Sélectionnez le type de compte et procédez à la connexion.

![DSN](../../gettingstarted/gettingstarted/images/web6.png)

Votre site web est alors chargé dans une fenêtre de navigateur incognito. Pour chaque démonstration, vous devez utiliser une fenêtre de navigateur incognito actualisée pour charger l’URL de votre site web de démonstration.

![DSN](../../gettingstarted/gettingstarted/images/web7.png)

Sur la page d’accueil **Luma**, accédez à **Men** et cliquez sur le produit **PROTEUS FITNESS JACKSHIRT**.

![Ingestion des données](./images/homenadia.png)

Vous avez maintenant consulté la page du produit pour **PROTEUS FITNESS JACKSHIRT**, ce qui signifie que vous serez désormais admissible pour le segment que vous avez créé précédemment dans cet exercice.

![Ingestion des données](./images/homenadiapp.png)

Lorsque vous ouvrez la visionneuse de profils et accédez à **Segments**, vous verrez que le segment est admissible.

![Ingestion des données](./images/homenadiapppb.png)

Revenez maintenant à votre webhook ouvert sur [https://webhook.site/](https://webhook.site/), où une nouvelle requête entrante doit apparaître, qui provient de Adobe Experience Platform et qui contient l’événement de qualification de segment.

![Ingestion des données](./images/destsdk10.png)

Étape suivante : [Résumé et avantages](./summary.md)

[Revenir au module 2.3](./real-time-cdp-build-a-segment-take-action.md)

[Revenir à tous les modules](../../../overview.md)
