---
title: Query Service - API Query Service
description: Query Service - API Query Service
kt: 5342
doc-type: tutorial
exl-id: d356f7e2-523b-41a2-9cc6-1ea2a028c3a7
source-git-commit: c49b41e1b033573dbebc9ced3a3f4071bf94d04e
workflow-type: tm+mt
source-wordcount: '995'
ht-degree: 3%

---

# 5.1.8 API Query Service

## Objectif

- Utiliser l’API Query Service pour gérer les modèles de requête et les plannings de requête

## Contexte

Dans cet exercice, vous allez exécuter des appels API pour gérer les modèles et les plannings de requête à l’aide d’une collection Postman. Vous définissez des modèles de requête, exécutez des requêtes standard et des requêtes CTAS. Une requête **CTAS** (créer une table sous forme de requête Select) stocke son jeu de résultats dans un jeu de données explicite. Bien que les requêtes standard soient stockées dans un jeu de données implicite (ou généré par le système), celui-ci est généralement exporté au format de fichier parquet.

## Documentation

- [Aide de Adobe Experience Platform Query Service](https://experienceleague.adobe.com/docs/experience-platform/query/api/getting-started.html?lang=fr)
- [API Query Service](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/qs-api.yaml)

## API Query Service

L’API Query Service vous permet de gérer des requêtes non interactives par rapport au lac de données Adobe Experience Platform.

Non interactif signifie qu’une demande d’exécution d’une requête n’entraînera pas de réponse immédiate. La requête sera traitée et son jeu de résultats sera stocké dans un jeu de données implicite ou explicite (CTAS : create table as select).

## Exemple de requête

Comme exemple de requête, vous utiliserez la première requête répertoriée dans [4.3 - Requêtes, requêtes, requêtes... et analyse de l’attrition &#x200B;](./ex3.md) :

Combien de consultations de produits avons-nous par jour ?

**SQL**

```sql
select date_format( timestamp , 'yyyy-MM-dd') AS Day,
       count(*) AS productViews
from   demo_system_event_dataset_for_website_global_v1_1
where  --aepTenantId--.demoEnvironment.brandName IN ('Citi Signal')
and eventType = 'commerce.productViews'
group by Day
limit 10;
```

## Requêtes

>[!IMPORTANT]
>
>Si vous êtes un employé Adobe, veuillez suivre les instructions ici pour utiliser [PostBuster](./../../../postbuster.md).

Ouvrez Postman sur votre ordinateur. Dans le cadre du module 2.1, vous avez créé un environnement Postman et importé une collection Postman. Suivez les instructions de la section [Exercice 2.1.3](./../../../modules/rtcdp-b2c/module2.1/ex3.md) au cas où vous ne l’auriez pas encore fait.

Un dossier **3 s’affiche dans la collection Postman que vous avez importée. Query Service**. Si ce dossier ne s’affiche pas, téléchargez à nouveau la collection [Postman](./../../../assets/postman/postman_profile.zip) puis importez à nouveau cette collection dans Postman comme indiqué dans l’[Exercice 2.1.3](./../../../modules/rtcdp-b2c/module2.1/ex3.md).

![QS](./images/pm3.png)

>[!NOTE]
>
>À ce stade, seul le dossier **1 est concerné. Requêtes** contient des requêtes. D’autres requêtes seront ajoutées ultérieurement.

Ouvrez ce dossier et découvrez les appels de l’API Query Service pour exécuter, surveiller et télécharger le jeu de résultats de la requête.

Un appel du POST à [/query/queries] avec la payload suivante, déclenchera l’exécution de votre requête ;

### Créer la requête

Cliquez sur la requête nommée **1.1 QS - Create Query** et accédez à **Headers**. Vous verrez alors ceci :

![Segmentation](./images/s1_call.png)

Concentrons-nous sur ce champ d’en-tête :

| Clé | Valeur |
| ----------- | ----------- |
| x-sandbox-name | `--aepSandboxName--` |

>[!NOTE]
>
>Vous devez spécifier le nom du sandbox Adobe Experience Platform que vous utilisez. Le champ d’en-tête **x-sandbox-name** doit être `--aepSandboxName--`.

Accédez à la section **Corps** de cette requête. Dans le **corps** de cette requête, vous verrez les éléments suivants :

![Segmentation](./images/s1_bodydtl.png)

```sql
{
    "name" : "ldap - QS API demo - Citi Signal - Product Views Per Day",
	"description": "ldap - QS API demo - Citi Signal - Product Views Per Day",
	"dbName": "--aepSandboxName--:all",
	"sql": "select date_format( timestamp , 'yyyy-MM-dd') AS Day, count(*) AS productViews from demo_system_event_dataset_for_website_global_v1_1 where --aepTenantId--.demoEnvironment.brandName IN ('Citi Signal') and eventType = 'commerce.productViews' group by Day limit 10"
}
```

Attention : veuillez mettre à jour la variable **name** dans la requête ci-dessous en remplaçant **ldap** par votre **spécifique, aepUserLdap—**.

Après avoir ajouté votre **ldap** spécifique, le corps doit ressembler à ceci :

```json
{
    "name" : "vangeluw - QS API demo - Citi Signal - Product Views Per Day",
	"description": "vangeluw - QS API demo - Citi Signal - Product Views Per Day",
	"dbName": "tech-insiders:all",
	"sql": "select date_format( timestamp , 'yyyy-MM-dd') AS Day, count(*) AS productViews from demo_system_event_dataset_for_website_global_v1_1 where _experienceplatform.demoEnvironment.brandName IN ('Citi Signal') and eventType = 'commerce.productViews' group by Day limit 10"
}
```

>[!NOTE]
>
>La clé **dbName** dans le corps JSON ci-dessus fait référence au sandbox utilisé dans votre instance Adobe Experience Platform. Si vous utilisez le sandbox PROD, le dbName doit être **prod:all**. Si vous utilisez un autre sandbox, tel que **tech-insiders**, le dbName doit être égal à **tech-insiders:all**.

Cliquez ensuite sur le bouton bleu **Envoyer** pour créer le segment et afficher les résultats.

![Segmentation](./images/s1_bodydtl_results.png)

Une fois cette opération réussie, la requête du POST renvoie la réponse suivante :

```json
{
    "isInsertInto": false,
    "request": {
        "dbName": "module7:all",
        "sql": "select date_format( timestamp , 'yyyy-MM-dd') AS Day, count(*) AS productViews from demo_system_event_dataset_for_website_global_v1_1 where _experienceplatform.demoEnvironment.brandName IN ('Luma Telco', 'Citi Signal') and eventType = 'commerce.productViews' group by Day limit 10",
        "name": "vangeluw - QS API demo - Citi Signal - Product Views Per Day",
        "description": "vangeluw - QS API demo - Citi Signal - Product Views Per Day"
    },
    "clientId": "5a143b5ae4aa4631a1f3b09cd051333f",
    "state": "SUBMITTED",
    "rowCount": 0,
    "errors": [],
    "isCTAS": false,
    "version": 1,
    "id": "8f0d7f25-f7aa-493b-9792-290f884a7e5b",
    "elapsedTime": 0,
    "updated": "2021-01-20T13:23:13.951Z",
    "client": "API",
    "userId": "A3392DB95FFF08EE0A495E87@techacct.adobe.com",
    "created": "2021-01-20T13:23:13.951Z",
    "_links": {
        "self": {
            "href": "https://platform-va7.adobe.io/data/foundation/query/queries/8f0d7f25-f7aa-493b-9792-290f884a7e5b",
            "method": "GET"
        },
        "soft_delete": {
            "href": "https://platform-va7.adobe.io/data/foundation/query/queries/8f0d7f25-f7aa-493b-9792-290f884a7e5b",
            "method": "PATCH",
            "body": "{ \"op\": \"soft_delete\"}"
        },
        "cancel": {
            "href": "https://platform-va7.adobe.io/data/foundation/query/queries/8f0d7f25-f7aa-493b-9792-290f884a7e5b",
            "method": "PATCH",
            "body": "{ \"op\": \"cancel\"}"
        }
    }
}
```

L’**état** actuel de la requête est **SOUMIS**. Une fois exécuté, son état devient **SUCCÈS**.

Vous pouvez également rechercher des requêtes envoyées via l’interface utilisateur de Adobe Experience Platform, ouvrir [Adobe Experience Platform](https://experience.adobe.com/#/@experienceplatform/platform/home), accéder à **Requêtes**, **Consigner** et sélectionner votre requête :

![Segmentation](./images/s1_bodydtl_results_qs.png)

### Obtenir des requêtes

Cliquez sur la requête nommée **1.2 QS - Get Queries** (Obtenir les requêtes) et accédez à **Headers**. Vous verrez alors ceci :

![Segmentation](./images/s2_call.png)

Concentrons-nous sur ce champ d’en-tête :

| Clé | Valeur |
| ----------- | ----------- |
| x-sandbox-name | `--aepSandboxName--` |

>[!NOTE]
>
>Vous devez spécifier le nom du sandbox Adobe Experience Platform que vous utilisez. Le champ d’en-tête **x-sandbox-name** doit être `--aepSandboxName--`.

Accédez à **Params**. Vous verrez alors ceci :

![Segmentation](./images/s2_call_p.png)

Le paramètre **orderby** vous permet de spécifier un ordre de tri en fonction de la propriété **created**. Remarquez le signe **&#39;-&#39;** devant created, ce qui signifie que l’ordre dans lequel la liste des requêtes est renvoyée utilisera leur date de création dans l’ordre **décroissant**. Votre requête doit se trouver en haut de la liste.

Cliquez ensuite sur le bouton bleu **Envoyer** pour créer le segment et afficher les résultats.

![Segmentation](./images/s2_bodydtl_results.png)

Une fois cette opération réussie, la requête renvoie une réponse similaire à celle ci-dessous. Le **état** de la réponse peut être **SOUMIS**, **EN_COURS** ou **SUCCÈS**. Il peut s’écouler plusieurs minutes avant que la requête ait un état **SUCCÈS**. Vous pouvez envoyer cette requête plusieurs fois de suite, jusqu’à ce que l’état **SUCCÈS** s’affiche.

```json
{
    "queries": [
        {
            "isInsertInto": false,
            "sessionType": "HTTP_SESSION",
            "request": {
                "dbName": "tech-insiders:all",
                "sql": "select date_format( timestamp , 'yyyy-MM-dd') AS Day, count(*) AS productViews from demo_system_event_dataset_for_website_global_v1_1 where _experienceplatform.demoEnvironment.brandName IN ('Citi Signal') and eventType = 'commerce.productViews' group by Day limit 10",
                "name": "vangeluw - QS API demo - Citi Signal - Product Views Per Day",
                "description": "vangeluw - QS API demo - Citi Signal - Product Views Per Day"
            },
            "computeMetrics": null,
            "clientId": "b7d8a1fc396242889bb31dc83644e91d",
            "state": "IN_PROGRESS",
            "rowCount": 0,
            "isService": false,
            "errors": [],
            "isCTAS": false,
            "version": 1,
            "id": "a535234e-dc0c-42ea-bcad-eb09c5997d76",
            "elapsedTime": 8088,
            "updated": "2024-12-04T14:17:10.627Z",
            "client": "API",
            "effectiveSQL": "select date_format( timestamp , 'yyyy-MM-dd') AS Day, count(*) AS productViews from demo_system_event_dataset_for_website_global_v1_1 where _experienceplatform.demoEnvironment.brandName IN ('Citi Signal') and eventType = 'commerce.productViews' group by Day limit 10",
            "userId": "8CD31E54673C49EE0A495E05@techacct.adobe.com",
            "isParentLevel": true,
            "created": "2024-12-04T14:14:22.637Z",
                "version": 1,
    "_links": {
        "next": {
            "href": "https://platform-va7.adobe.io/data/foundation/query/queries?orderby=-created&start=2024-11-22T00:32:04.505Z"
        },
        "prev": {
            "href": "https://platform-va7.adobe.io/data/foundation/query/queries?orderby=-created&start=2024-12-04T14:14:22.637Z&isPrevLink=true"
        }
    }
}
```

Lorsque l’état est **SUCCÈS**, veuillez poursuivre avec la requête suivante.

### Obtenir le statut de la requête

Cliquez sur la requête nommée **1.3 QS - Get Query Status** et accédez à **Headers**. Vous verrez alors ceci :

![Segmentation](./images/s3_call.png)

Concentrons-nous sur ce champ d’en-tête :

| Clé | Valeur |
| ----------- | ----------- |
| x-sandbox-name | `--aepSandboxName--` |

>[!NOTE]
>
>Vous devez spécifier le nom du sandbox Adobe Experience Platform que vous utilisez. Le champ d’en-tête **x-sandbox-name** doit être `--aepSandboxName--`.

Cliquez ensuite sur le bouton bleu **Envoyer** pour créer le segment et afficher les résultats.

![Segmentation](./images/s3_bodydtl_results.png)

Une fois cette opération réussie, la requête renvoie une réponse similaire à celle ci-dessous.

```json
{
    "isInsertInto": false,
    "sessionType": "HTTP_SESSION",
    "request": {
        "dbName": "tech-insiders:all",
        "sql": "select date_format( timestamp , 'yyyy-MM-dd') AS Day, count(*) AS productViews from demo_system_event_dataset_for_website_global_v1_1 where _experienceplatform.demoEnvironment.brandName IN ('Citi Signal') and eventType = 'commerce.productViews' group by Day limit 10",
        "name": "vangeluw - QS API demo - Citi Signal - Product Views Per Day",
        "description": "vangeluw - QS API demo - Citi Signal - Product Views Per Day"
    },
    "computeMetrics": {
        "executorVMSeconds": 138,
        "clusterCpuSeconds": 3312,
        "clusterVMHours": 0.07666666805744171,
        "driverVMSeconds": 138,
        "clusterVMSeconds": 276
    },
    "clientId": "b7d8a1fc396242889bb31dc83644e91d",
    "state": "SUCCESS",
    "rowCount": 1,
    "isService": false,
    "errors": [],
    "isCTAS": false,
    "version": 1,
    "id": "a535234e-dc0c-42ea-bcad-eb09c5997d76",
    "elapsedTime": 199219,
    "updated": "2024-12-04T14:17:41.856Z",
    "client": "API",
    "effectiveSQL": "select date_format( timestamp , 'yyyy-MM-dd') AS Day, count(*) AS productViews from demo_system_event_dataset_for_website_global_v1_1 where _experienceplatform.demoEnvironment.brandName IN ('Citi Signal') and eventType = 'commerce.productViews' group by Day limit 10",
    "userId": "8CD31E54673C49EE0A495E05@techacct.adobe.com",
    "isParentLevel": true,
    "created": "2024-12-04T14:14:22.637Z",
    "_links": {
        "self": {
            "href": "https://platform-va7.adobe.io/data/foundation/query/queries/a535234e-dc0c-42ea-bcad-eb09c5997d76",
            "method": "GET"
        },
        "soft_delete": {
            "href": "https://platform-va7.adobe.io/data/foundation/query/queries/a535234e-dc0c-42ea-bcad-eb09c5997d76",
            "method": "PATCH",
            "body": "{ \"op\": \"soft_delete\"}"
        },
        "referenced_datasets": [
            {
                "id": "672a10b1074ceb2af0aa7034",
                "href": "https://platform-va7.adobe.io/data/foundation/catalog/dataSets/672a10b1074ceb2af0aa7034"
            }
        ]
    }
}
```

Lorsqu’une requête atteint l’état **SUCCESS**, la réponse indique également le nombre de lignes récupérées par la requête via la propriété **rowCount**. Dans notre exemple, 10 lignes sont renvoyées par la requête . Voyons dans la section suivante comment nous pouvons récupérer les 10 lignes.

### Récupérer le résultat de la requête

La réponse **SUCCESS** ci-dessus inclut une propriété **reference_datasets** qui pointe vers le jeu de données implicite qui stocke le résultat de la requête. Pour accéder au résultat, nous utilisons sa propriété **href** ou **id**.

Cliquez sur la requête nommée **1.4 QS - Get Query Result** et accédez à **Headers**. Vous verrez alors ceci :

![Segmentation](./images/s4_call.png)

Concentrons-nous sur ce champ d’en-tête :

| Clé | Valeur |
| ----------- | ----------- |
| x-sandbox-name | `--aepSandboxName--` |

>[!NOTE]
>
>Vous devez spécifier le nom du sandbox Adobe Experience Platform que vous utilisez. Le champ d’en-tête **x-sandbox-name** doit être `--aepSandboxName--`.

Cliquez ensuite sur le bouton bleu **Envoyer** pour créer le segment et afficher les résultats.

![Segmentation](./images/s4_bodydtl_results.png)

La réponse de cette requête pointe vers les fichiers du jeu de données :

```json
{
    "672a10b1074ceb2af0aa7034": {
        "name": "Demo System - Event Dataset for Website (Global v1.1)",
        "description": "Demo System - Event Dataset for Website (Global v1.1)",
        "enableErrorDiagnostics": false,
        "tags": {
            "adobe/siphon/partition/definition": [
                "day(timestamp, _ACP_DATE)",
                "identity(_ACP_BATCHID)"
            ],
            "adobe/siphon/meta": [
                "acpBufferedFlag::false"
            ],
            "aep/siphon/partitions": [
                "_ACP_DATE",
                "_ACP_BATCHID"
            ],
            "acp_granular_plugin_validation_flags": [
                "identity:enabled",
                "profile:disabled"
            ],
            "adobe/pqs/table": [
                "demo_system_event_dataset_for_website_global_v1_1"
            ],
            "acp_granular_validation_flags": [
                "requiredFieldCheck:enabled"
            ],
            "aep/siphon/cleanup/trash/timestamp": [
                "1733302532212"
            ],
            "acp_validationContext": [
                "enabled"
            ],
            "adobe/siphon/table/format": [
                "delta"
            ],
            "unifiedProfile": [
                "enabled:true",
                "enabledAt:2024-11-05 12:33:59"
            ],
            "aep/siphon/cleanup/meta/timestamp": [
                "1733302532287"
            ],
            "unifiedIdentity": [
                "enabled:true"
            ]
        },
        "state": "ACTIVE",
        "imsOrg": "907075E95BF479EC0A495C73@AdobeOrg",
        "sandboxId": "79e3c8b2-0609-4564-a3c8-b20609a5648c",
        "extensions": {
            "adobe_lakeHouse": {
                "metrics": {
                    "storageSize": 810709,
                    "rowCount": 1141,
                    "asOf": 1732494676514
                }
            },
            "adobe_unifiedProfile": {}
        },
        "version": "1.0.21",
        "created": 1730810034023,
        "updated": 1733302532348,
        "createdClient": "d75039d36ca543c78612f7aac18e6c2b",
        "createdUser": "53FB1E5E66CDC87D0A495FC0@techacct.adobe.com",
        "updatedUser": "acp_foundation_dataTracker@AdobeID",
        "classification": {
            "dataBehavior": "time-series",
            "managedBy": "CUSTOMER"
        },
        "viewId": "672a10b2074ceb2af0aa7035",
        "fileDescription": {
            "format": "parquet"
        },
        "files": "@/dataSetFiles?dataSetId=672a10b1074ceb2af0aa7034",
        "schemaRef": {
            "id": "https://ns.adobe.com/experienceplatform/schemas/d9b88a044ad96154637965a97ed63c7b20bdf2ab3b4f642e",
            "contentType": "application/vnd.adobe.xed-full+json;version=1"
        }
    }
}
```

Étape suivante : [Résumé et avantages](./summary.md)

[Retour au module 5.1](./query-service.md)

[Revenir à tous les modules](../../../overview.md)
