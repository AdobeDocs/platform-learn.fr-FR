---
title: Foundation - Real-time Customer Profile - Création d’un segment - API
description: Foundation - Real-time Customer Profile - Création d’un segment - API
kt: 5342
doc-type: tutorial
source-git-commit: 2cdc145d7f3933ec593db4e6f67b60961a674405
workflow-type: tm+mt
source-wordcount: '706'
ht-degree: 3%

---

# 2.1.5 Création d’un segment - API

Au cours de cet exercice, vous utiliserez Postman et Adobe I/O pour créer un segment et stocker les résultats de ce segment sous la forme d’un jeu de données, à l’aide des API Adobe Experience Platform.

## Histoire

Dans Real-time Customer Profile, toutes les données de profil s’affichent avec les données d’événement et les appartenances à des segments existants. Les données affichées peuvent provenir de n’importe où, des applications d’Adobe et des solutions externes. Il s’agit de la vue la plus puissante de Adobe Experience Platform, le système d’enregistrement d’expérience.

## 2.1.5.1 - Création d’un segment via l’API Platform

Accédez à Postman.

Recherchez la collection : **_Adobe Experience Platform Enablement**. Dans cette collection, un dossier **2 s&#39;affiche. Segmentation**. Nous utiliserons ces requêtes dans cet exercice.

![Segmentation](./images/pmdtl.png)

Nous allons ensuite suivre toutes les étapes requises pour créer un segment via l’API. Nous allons créer un segment simple : &quot;**ldap** - Toutes les clientes&quot;.

### Étape 1 - Création d’une définition de segment

Cliquez sur la requête nommée **Etape 1 - Profil : créer une définition de segment**.

![Segmentation](./images/s1_call.png)

Accédez à la section **Body** de cette requête.

![Segmentation](./images/s1_body.png)

Dans le **Body** de cette requête, les éléments suivants s’affichent :

![Segmentation](./images/s1_bodydtl.png)

La langue utilisée pour cette requête est appelée Profile Query Language ou **PQL**.

Vous trouverez plus d’informations et de documentation sur PQL [ici](https://experienceleague.adobe.com/docs/experience-platform/segmentation/pql/overview.html?lang=fr).


Attention : veuillez mettre à jour la variable **name** dans la requête ci-dessous en remplaçant **ldap** par votre **ldap** spécifique.

```json
{
    "name" : "ldap - API - All Female Customer",
    "expression" : {"type":"PQL", "format":"pql/json", "value":"{\"nodeType\":\"fnApply\",\"fnName\":\"in\",\"params\":[{\"nodeType\":\"fieldLookup\",\"fieldName\":\"gender\",\"object\":{\"nodeType\":\"fieldLookup\",\"fieldName\":\"person\",\"object\":{\"nodeType\":\"literal\",\"literalType\":\"XDMObject\",\"value\":\"profile\"}}},{\"literalType\":\"List\",\"nodeType\":\"literal\",\"value\":[\"female\"]}]}"},
    "createdBy": "ldap",
    "schema" : { "name" : "_xdm.context.profile"},
    "ttlInDays" : 90
}
```

Après avoir ajouté votre **ldap** spécifique, le corps doit ressembler à ceci :

```json
{
    "name" : "vangeluw - API - All Female Customer",
    "expression" : {"type":"PQL", "format":"pql/json", "value":"{\"nodeType\":\"fnApply\",\"fnName\":\"in\",\"params\":[{\"nodeType\":\"fieldLookup\",\"fieldName\":\"gender\",\"object\":{\"nodeType\":\"fieldLookup\",\"fieldName\":\"person\",\"object\":{\"nodeType\":\"literal\",\"literalType\":\"XDMObject\",\"value\":\"profile\"}}},{\"literalType\":\"List\",\"nodeType\":\"literal\",\"value\":[\"female\"]}]}"},
    "createdBy": "vangeluw",
    "schema" : { "name" : "_xdm.context.profile"},
    "ttlInDays" : 90
}
```

Vous devez également vérifier les champs **Header** - de votre requête. Accédez à **En-têtes**. Vous verrez alors :

![Postman](./images/s1_h.png)

| Clé | Valeur |
| -------------- | ------------------ |
| x-sandbox-name | `--aepSandboxId--` |

>[!NOTE]
>
>Vous devez spécifier le nom de l’environnement de test Adobe Experience Platform que vous utilisez. Votre x-sandbox-name doit être `--aepSandboxId--`.

Cliquez maintenant sur le bouton bleu **Envoyer** pour créer le segment et en afficher les résultats.

![Segmentation](./images/s1_bodydtl_results.png)

Après cette étape, vous pouvez afficher votre définition de segment dans l’interface utilisateur de Platform. Pour vérifier cela, connectez-vous à Adobe Experience Platform et accédez à **Segments**.

![Segmentation](./images/s1_segmentdef.png)

### Étape 2 - Création d’une tâche de POST de segments

Dans l’exercice précédent, vous avez créé un segment _streaming_. Un segment en continu évalue en permanence les qualifications en temps réel. Ce que vous faites ici, c’est créer un segment _batch_. Le segment par lot vous donne un aperçu de ce à quoi le segment pourrait ressembler en termes de qualifications, mais _cela ne signifie pas que le segment a réellement été exécuté_. Actuellement, _personne n’est admissible pour ce segment_. Pour que les utilisateurs soient qualifiés, le segment par lot doit s’exécuter, ce qui est exactement ce que nous allons faire ici.

Créons maintenant une tâche de segmentation.

Accédez à Postman.

![Segmentation](./images/pmdtl.png)

Dans votre collection Postman, cliquez sur la requête nommée **Step 2 - POST Segment Job** pour l’ouvrir.

![Segmentation](./images/s2_call.png)

Vous devez également vérifier les champs **Header** - de votre requête. Accédez à **En-têtes**. Vous verrez alors :

![Postman](./images/s2headers.png)

| Clé | Valeur |
| -------------- | ------------------ |
| x-sandbox-name | `--aepSandboxId--` |

>[!NOTE]
>
>Vous devez spécifier le nom de l’environnement de test Adobe Experience Platform que vous utilisez. Votre x-sandbox-name doit être `--aepSandboxId--`.

Cliquez sur le bouton bleu **Send** .

Vous devriez voir un résultat similaire :

![Segmentation](./images/s2_call_response.png)

Cette tâche de segmentation est maintenant en cours d’exécution, ce qui peut prendre un certain temps. À l’étape 3, vous pourrez vérifier l’état de cette tâche.


### Étape 3 - État de la tâche de segmentation du GET

Accédez à Postman.

![Segmentation](./images/pmdtl.png)

Dans votre collection Postman, cliquez sur la requête nommée **Etape 3 - GET de l’état de la tâche de segmentation**.

![Segmentation](./images/s3_call.png)

Vous devez également vérifier les champs **Header** - de votre requête. Accédez à **En-têtes**. Vous verrez alors :

![Postman](./images/s3headers.png)

| Clé | Valeur |
| -------------- | ------------------ |
| x-sandbox-name | `--aepSandboxId--` |

>[!NOTE]
>
>Vous devez spécifier le nom de l’environnement de test Adobe Experience Platform que vous utilisez. Votre x-sandbox-name doit être `--aepSandboxId--`.

Cliquez sur le bouton bleu **Send** .

Vous devriez voir un résultat similaire :

![Segmentation](./images/s3_status.png)

Dans cet exemple, le **statut** de la tâche est défini sur **QUEUED**.

Répétez cette requête en cliquant sur le bouton bleu **Envoyer** toutes les deux minutes jusqu’à ce que l’option **status** soit définie sur **SUCCEEDED**.

![Segmentation](./images/s3_status_succeeded.png)

Une fois que l’état est **SUCCEEDED**, votre tâche de segmentation s’est exécutée et les clients sont désormais qualifiés pour le segment.

Félicitations, vous avez terminé l’exercice de segmentation. Examinons maintenant comment Real-time Customer Profile peut être activé dans l’ensemble de l’entreprise.

Étape suivante : [2.1.6 Reportez-vous à Real-time Customer Profile en action dans le centre d’appels](./ex6.md)

[Revenir au module 2.1](./real-time-customer-profile.md)

[Revenir à tous les modules](../../../overview.md)
