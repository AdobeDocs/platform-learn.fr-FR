---
title: Query Service - API Query Service
description: Query Service - API Query Service
kt: 5342
audience: Data Engineer, Data Architect, Data Analyst, BI Expert
doc-type: tutorial
activity: develop
exl-id: 6f437bd3-b134-4509-8e32-ad6f7b70608e
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '1000'
ht-degree: 5%

---

# 4.7 API Query Service

## Objectif

- Utilisez l’API Query Service pour gérer les modèles de requête et les plannings de requête.

## Contexte

Dans cet exercice, vous exécuterez des appels API pour gérer des modèles de requête et des plannings de requête à l’aide d’une collection Postman. Vous allez définir des modèles de requête, exécuter des requêtes standard et des requêtes CTAS. A **CTAS** query (créer une table en tant que requête sélectionnée) stocke son jeu de résultats dans un jeu de données explicite. Bien que les requêtes standard soient stockées dans un jeu de données implicite (ou généré par le système), qui est généralement exporté au format de fichier parquet.

## Documentation

- [Aide d’Adobe Experience Platform Query Service](https://experienceleague.adobe.com/docs/experience-platform/query/api/getting-started.html?lang=fr)
- [API Query Service](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/qs-api.yaml)

## 4.7.1 API Query Service

L’API Query Service vous permet de gérer des requêtes non interactives par rapport au lac de données de Adobe Experience Platform.

Non interactif signifie qu’une demande d’exécution d’une requête n’entraîne pas de réponse immédiate. La requête sera traitée et son jeu de résultats sera stocké dans un CTAS implicite ou explicite : créer un tableau en tant que sélectionné) jeu de données.

## 4.7.2 Exemple de requête

Vous utiliserez comme exemple de requête la première requête répertoriée dans [4.3 - Requêtes, requêtes, requêtes.. et analyse de perte de clientèle](./ex3.md):

Combien de consultations de produits y a-t-il chaque jour ?

**SQL**

```sql
select date_format( timestamp , 'yyyy-MM-dd') AS Day,
       count(*) AS productViews
from   demo_system_event_dataset_for_website_global_v1_1
where  --aepTenantId--.demoEnvironment.brandName IN ('Luma Telco', 'Citi Signal')
and eventType = 'commerce.productViews'
group by Day
limit 10;
```

## 4.7.3 Requêtes

Ouvrez Postman sur votre ordinateur. Dans le cadre du module 3, vous avez créé un environnement Postman et importé une collection Postman. Suivez les instructions de la section [Exercice 3.3.3](./../module3/ex3.md) au cas où tu n&#39;aurais pas encore fait ça.

Dans le cadre de la collection Postman que vous avez importée, un dossier s’affiche. **3. Query Service**. Si ce dossier ne s’affiche pas, téléchargez à nouveau le fichier [Collection Postman](../../assets/postman/postman_profile.zip) et réimportez cette collection dans Postman en suivant les instructions de la section [Exercice 3.3.3](./../module3/ex3.md).

![QS](./images/pm3.png)

>[!NOTE]
>
>Actuellement, seul le dossier **1. Requêtes** contient des requêtes. D’autres requêtes seront ajoutées à l’étape du calque.

Ouvrez ce dossier et découvrez les appels de l’API Query Service pour exécuter, surveiller et télécharger le jeu de résultats de la requête.

Un appel POST à [/query/query] avec la charge utile suivante déclenche l’exécution de notre requête ;

### 4.7.3.1 Création d’une requête

Cliquez sur la requête nommée **1.1 QS - Créer une requête** et accédez à **En-têtes**. Vous verrez alors :

![Segmentation](./images/s1_call.png)

Concentrons-nous sur ce champ d’en-tête :

| Clé | Valeur |
| ----------- | ----------- |
| x-sandbox-name | `--module7sandbox--` |

>[!NOTE]
>
>Vous devez spécifier le nom de l’environnement de test Adobe Experience Platform que vous utilisez. Champ d’en-tête **x-sandbox-name** should `--module7sandbox--`.

Accédez au **Corps** de cette requête. Dans le **Corps** de cette requête, vous verrez les éléments suivants :

![Segmentation](./images/s1_bodydtl.png)

```sql
{
    "name" : "ldap - QS API demo - Citi Signal - Product Views Per Day",
	"description": "ldap - QS API demo - Citi Signal - Product Views Per Day",
	"dbName": "module7:all",
	"sql": "select date_format( timestamp , 'yyyy-MM-dd') AS Day, count(*) AS productViews from demo_system_event_dataset_for_website_global_v1_1 where _experienceplatform.demoEnvironment.brandName IN ('Luma Telco', 'Citi Signal') and eventType = 'commerce.productViews' group by Day limit 10"
}
```

Attention : mettre à jour la variable **name** dans la requête ci-dessous en remplaçant **ldap** avec votre **ldap**.

Après avoir ajouté votre **ldap**, le corps doit ressembler à ceci :

```json
{
    "name" : "vangeluw - QS API demo - Citi Signal - Product Views Per Day",
	"description": "vangeluw - QS API demo - Citi Signal - Product Views Per Day",
	"dbName": "module7:all",
	"sql": "select date_format( timestamp , 'yyyy-MM-dd') AS Day, count(*) AS productViews from demo_system_event_dataset_for_website_global_v1_1 where _experienceplatform.demoEnvironment.brandName IN ('Luma Telco', 'Citi Signal') and eventType = 'commerce.productViews' group by Day limit 10"
}
```

>[!NOTE]
>
>La clé **dbName** dans le corps JSON ci-dessus fait référence à l’environnement de test utilisé dans votre instance Adobe Experience Platform. Si vous utilisez l’environnement de test PROD, dbName doit être **prod:all**, si vous utilisez un autre environnement de test comme par exemple **module7**, la valeur dbName doit être égale à **module7:all**.

Cliquez ensuite sur le bouton bleu **Envoyer** pour créer le segment et en visualiser les résultats.

![Segmentation](./images/s1_bodydtl_results.png)

En cas de réussite, la requête du POST renvoie la réponse suivante :

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

La variable **state** de la requête est **ENVOYÉ**, une fois exécuté son état devient **SUCCÈS**.

Vous pouvez également rechercher des requêtes envoyées via l’interface utilisateur de Adobe Experience Platform, ouvrir [Adobe Experience Platform](https://experience.adobe.com/#/@experienceplatform/platform/home), accédez à **Requêtes**, à **Journal** et sélectionnez votre requête :

![Segmentation](./images/s1_bodydtl_results_qs.png)

### 4.7.3.2 Obtention de requêtes

Cliquez sur la requête nommée **1.2 QS - Obtention de requêtes** et accédez à **En-têtes**. Vous verrez alors :

![Segmentation](./images/s2_call.png)

Concentrons-nous sur ce champ d’en-tête :

| Clé | Valeur |
| ----------- | ----------- |
| x-sandbox-name | `--module7sandbox--` |

>[!NOTE]
>
>Vous devez spécifier le nom de l’environnement de test Adobe Experience Platform que vous utilisez. Champ d’en-tête **x-sandbox-name** should `--module7sandbox--`.

Accédez à **Paramètres**. Vous verrez alors :

![Segmentation](./images/s2_call_p.png)

Le **orderby** vous permet de spécifier un ordre de tri en fonction de la variable **created** . Remarquez la variable **&#39;-&#39;** vous connecter devant created, ce qui signifie que l&#39;ordre dans lequel la liste des requêtes est renvoyée utilisera la date de création dans **descendant** commande. Votre requête doit figurer en haut de la liste.

Cliquez ensuite sur le bouton bleu **Envoyer** pour créer le segment et en visualiser les résultats.

![Segmentation](./images/s2_bodydtl_results.png)

En cas de réussite, la requête renvoie une réponse similaire à celle ci-dessous. Le **state** de la réponse peut être **ENVOYÉ**, **IN_PROGRESS** ou **SUCCÈS**. Plusieurs minutes peuvent s’écouler avant que la requête n’ait une **SUCCÈS** état. Vous pouvez envoyer cette requête plusieurs fois, jusqu’à ce que la fonction **SUCCÈS** état.

```json
{
    "queries": [
        {
            "isInsertInto": false,
            "request": {
                "dbName": "module7:all",
                "sql": "select date_format( timestamp , 'yyyy-MM-dd') AS Day, count(*) AS productViews from demo_system_event_dataset_for_website_global_v1_1 where _experienceplatform.demoEnvironment.brandName IN ('Luma Telco', 'Citi Signal') and eventType = 'commerce.productViews' group by Day limit 10",
                "name": "vangeluw - QS API demo - Citi Signal - Product Views Per Day",
                "description": "vangeluw - QS API demo - Citi Signal - Product Views Per Day"
            },
            "clientId": "5a143b5ae4aa4631a1f3b09cd051333f",
            "state": "SUCCESS",
            "rowCount": 1,
            "errors": [],
            "isCTAS": false,
            "version": 1,
            "id": "8f0d7f25-f7aa-493b-9792-290f884a7e5b",
            "elapsedTime": 217481,
            "updated": "2021-01-20T13:26:51.432Z",
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
                "referenced_datasets": [
                    {
                        "id": "60080ace62c49a19490c5870",
                        "href": "https://platform-va7.adobe.io/data/foundation/catalog/dataSets/60080ace62c49a19490c5870"
                    }
                ]
            }
        }
     ]
    },
    "version": 1
}
```

Lorsque l’état est **SUCCÈS**, veuillez poursuivre avec la requête suivante.

### 4.7.3.3 Obtention de l’état de la requête

Cliquez sur la requête nommée **1.3 QS - Obtention de l’état de la requête** et accédez à **En-têtes**. Vous verrez alors :

![Segmentation](./images/s3_call.png)

Concentrons-nous sur ce champ d’en-tête :

| Clé | Valeur |
| ----------- | ----------- |
| x-sandbox-name | `--module7sandbox--` |

>[!NOTE]
>
>Vous devez spécifier le nom de l’environnement de test Adobe Experience Platform que vous utilisez. Champ d’en-tête **x-sandbox-name** should `--module7sandbox--`.

Cliquez ensuite sur le bouton bleu **Envoyer** pour créer le segment et en visualiser les résultats.

![Segmentation](./images/s3_bodydtl_results.png)

En cas de réussite, la requête renvoie une réponse similaire à celle ci-dessous.

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
    "state": "SUCCESS",
    "rowCount": 1,
    "errors": [],
    "isCTAS": false,
    "version": 1,
    "id": "8f0d7f25-f7aa-493b-9792-290f884a7e5b",
    "elapsedTime": 217481,
    "updated": "2021-01-20T13:26:51.432Z",
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
        "referenced_datasets": [
            {
                "id": "60080ace62c49a19490c5870",
                "href": "https://platform-va7.adobe.io/data/foundation/catalog/dataSets/60080ace62c49a19490c5870"
            }
        ]
    }
}
```

Lorsqu’une requête atteint l’état de **SUCCÈS**, la réponse indiquera également le nombre de lignes récupérées par la requête via le **rowCount** . Dans notre exemple, 10 lignes sont renvoyées par la requête. Voyons dans la section suivante comment récupérer les 10 lignes.

### 4.7.3.4 Récupération du résultat de la requête

Le **SUCCÈS** la réponse ci-dessus inclut une **referenced_datasets** qui pointe vers le jeu de données implicite qui stocke le résultat de la requête. Pour accéder au résultat, nous utilisons son **href** ou **id** .

Cliquez sur la requête nommée **1.4 QS - Obtenir le résultat de la requête** et accédez à **En-têtes**. Vous verrez alors :

![Segmentation](./images/s4_call.png)

Concentrons-nous sur ce champ d’en-tête :

| Clé | Valeur |
| ----------- | ----------- |
| x-sandbox-name | `--module7sandbox--` |

>[!NOTE]
>
>Vous devez spécifier le nom de l’environnement de test Adobe Experience Platform que vous utilisez. Champ d’en-tête **x-sandbox-name** should `--module7sandbox--`.

Cliquez ensuite sur le bouton bleu **Envoyer** pour créer le segment et en visualiser les résultats.

![Segmentation](./images/s4_bodydtl_results.png)

La réponse de cette requête pointe vers les fichiers de jeu de données :

```json
{
    "60080ace62c49a19490c5870": {
        "name": "Demo System - Event Dataset for Website (Global v1.1)",
        "description": "Demo System - Event Dataset for Website (Global v1.1)",
        "enableErrorDiagnostics": false,
        "tags": {
            "adobe/siphon/partition/definition": [
                "day(timestamp, _ACP_DATE)",
                "identity(_ACP_BATCHID)"
            ],
            "aep/siphon/partitions": [
                "_ACP_DATE",
                "_ACP_BATCHID"
            ],
            "acp_granular_plugin_validation_flags": [
                "identity:enabled",
                "profile:enabled"
            ],
            "adobe/siphon/buffered-promotion-recency": [
                "live"
            ],
            "adobe/siphon/use-buffered-promotion": [
                "true"
            ],
            "adobe/pqs/table": [
                "demo_system_event_dataset_for_website_global_v1_1"
            ],
            "aep/siphon/expire-snapshot-timestamp": [
                "1611141272703"
            ],
            "acp_granular_validation_flags": [
                "requiredFieldCheck:enabled"
            ],
            "acp_validationContext": [
                "enabled"
            ],
            "adobe/siphon/table/format": [
                "iceberg"
            ],
            "unifiedProfile": [
                "enabled:true",
                "enabledAt:2021-01-20 10:49:51"
            ],
            "unifiedIdentity": [
                "enabled:true"
            ]
        },
        "namespace": "ACP",
        "state": "DRAFT",
        "imsOrg": "907075E95BF479EC0A495C73@AdobeOrg",
        "sandboxId": "62cd9f38-8529-4b05-8d9f-388529db0540",
        "lastBatchId": "01EWFQZ15XRNNB1FPKPW5ETRVP",
        "lastBatchStatus": "success",
        "lastSuccessfulBatch": "01EWFQZ15XRNNB1FPKPW5ETRVP",
        "version": "1.0.6",
        "created": 1611139790698,
        "updated": 1611149266031,
        "createdClient": "750e24ee855b4ac18ccc4f4817f96ee1",
        "createdUser": "3A260B485E909A170A495E76@techacct.adobe.com",
        "updatedUser": "acp_foundation_dataTracker@AdobeID",
        "viewId": "60080ace62c49a19490c5871",
        "fileDescription": {
            "persisted": true,
            "containerFormat": "parquet",
            "format": "parquet"
        },
        "files": "@/dataSets/60080ace62c49a19490c5870/views/60080ace62c49a19490c5871/files",
        "schemaMetadata": {
            "delta": [],
            "gdpr": []
        },
        "schemaRef": {
            "id": "https://ns.adobe.com/experienceplatform/schemas/d9b88a044ad96154637965a97ed63c7b20bdf2ab3b4f642e",
            "contentType": "application/vnd.adobe.xed-full+json;version=1"
        }
    }
}
```

>[!NOTE]
>
>D’autres exercices seront bientôt ajoutés pour vous aider à interagir avec l’API Query Service.

Étape suivante : [Résumé et avantages](./summary.md)

[Revenir au module 4](./query-service.md)

[Revenir à tous les modules](../../overview.md)
