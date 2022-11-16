---
title: Foundation - Real-time Customer Profile - Création d’un segment - API
description: Foundation - Real-time Customer Profile - Création d’un segment - API
kt: 5342
audience: Data Engineer, Data Architect, Marketer
doc-type: tutorial
activity: develop
exl-id: 3f537efd-7281-4c0c-b809-97f266a2a337
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '701'
ht-degree: 4%

---

# 3.5 Création d’un segment - API

Au cours de cet exercice, vous utiliserez Postman et Adobe I/O pour créer un segment et stocker les résultats de ce segment sous la forme d’un jeu de données, à l’aide des API Adobe Experience Platform.

## Histoire

Dans Real-time Customer Profile, toutes les données de profil s’affichent avec les données d’événement et les appartenances à des segments existants. Les données affichées peuvent provenir de n’importe où, des applications d’Adobe et des solutions externes. Il s’agit de la vue la plus puissante de Adobe Experience Platform, le système d’enregistrement d’expérience.

## Exercice 3.5.1 - Création d’un segment via l’API Platform

Accédez à Postman.

Recherchez la collection : **_Activation de Adobe Experience Platform**. Dans cette collection, un dossier s’affiche. **2. Segmentation**. Nous utiliserons ces requêtes dans cet exercice.

![Segmentation](./images/pmdtl.png)

Nous allons ensuite suivre toutes les étapes requises pour créer un segment via l’API. Nous allons créer un segment simple : &quot;**ldap** - Toutes les clientes femmes&quot;.

### Étape 1 - Création d’une définition de segment

Cliquez sur la requête nommée **Étape 1 - Profil Création D’Une Définition De Segment**.

![Segmentation](./images/s1_call.png)

Accédez au **Corps** de cette requête.

![Segmentation](./images/s1_body.png)

Dans le **Corps** de cette requête, vous verrez les éléments suivants :

![Segmentation](./images/s1_bodydtl.png)

La langue utilisée pour cette requête est appelée Langage de requête de profil, ou **PQL**.

Vous trouverez plus d’informations et de documentation sur PQL. [here](https://experienceleague.adobe.com/docs/experience-platform/segmentation/pql/overview.html?lang=fr).


Attention : mettre à jour la variable **name** dans la requête ci-dessous en remplaçant **ldap** avec votre **ldap**.

```json
{
    "name" : "ldap - API - All Female Customer",
    "expression" : {"type":"PQL", "format":"pql/json", "value":"{\"nodeType\":\"fnApply\",\"fnName\":\"in\",\"params\":[{\"nodeType\":\"fieldLookup\",\"fieldName\":\"gender\",\"object\":{\"nodeType\":\"fieldLookup\",\"fieldName\":\"person\",\"object\":{\"nodeType\":\"literal\",\"literalType\":\"XDMObject\",\"value\":\"profile\"}}},{\"literalType\":\"List\",\"nodeType\":\"literal\",\"value\":[\"female\"]}]}"},
    "createdBy": "ldap",
    "schema" : { "name" : "_xdm.context.profile"},
    "ttlInDays" : 90
}
```

Après avoir ajouté votre **ldap**, le corps doit ressembler à ceci :

```json
{
    "name" : "vangeluw - API - All Female Customer",
    "expression" : {"type":"PQL", "format":"pql/json", "value":"{\"nodeType\":\"fnApply\",\"fnName\":\"in\",\"params\":[{\"nodeType\":\"fieldLookup\",\"fieldName\":\"gender\",\"object\":{\"nodeType\":\"fieldLookup\",\"fieldName\":\"person\",\"object\":{\"nodeType\":\"literal\",\"literalType\":\"XDMObject\",\"value\":\"profile\"}}},{\"literalType\":\"List\",\"nodeType\":\"literal\",\"value\":[\"female\"]}]}"},
    "createdBy": "vangeluw",
    "schema" : { "name" : "_xdm.context.profile"},
    "ttlInDays" : 90
}
```

Vous devez également vérifier la variable **En-tête** : champs de votre requête. Accédez à **En-têtes**. Vous verrez alors :

![Postman](./images/s1_h.png)

| Clé | Valeur |
| -------------- | ------------------ |
| x-sandbox-name | `--aepSandboxId--` |

>[!NOTE]
>
>Vous devez spécifier le nom de l’environnement de test Adobe Experience Platform que vous utilisez. Votre x-sandbox-name doit être `--aepSandboxId--`.

Cliquez maintenant sur le bouton bleu **Envoyer** pour créer le segment et en visualiser les résultats.

![Segmentation](./images/s1_bodydtl_results.png)

Après cette étape, vous pouvez afficher votre définition de segment dans l’interface utilisateur de Platform. Pour vérifier cela, connectez-vous à Adobe Experience Platform et accédez à **Segments**.

![Segmentation](./images/s1_segmentdef.png)

### Étape 2 - Création d’une tâche de POST de segments

Dans l’exercice précédent, vous avez créé une _diffusion en continu_ segment. Un segment en continu évalue en permanence les qualifications en temps réel. Ce que vous faites ici, c&#39;est créer une _batch_ segment. Le segment par lot vous donne un aperçu de ce à quoi pourrait ressembler le segment en termes de qualifications, mais _cela ne signifie pas que le segment a réellement été exécuté._. Actuellement, _personne n’est admissible pour ce segment_. Pour que les utilisateurs soient qualifiés, le segment par lot doit s’exécuter, ce qui est exactement ce que nous allons faire ici.

Créons maintenant une tâche de segmentation.

Accédez à Postman.

![Segmentation](./images/pmdtl.png)

Dans votre collection Postman, cliquez sur la requête nommée **Étape 2 - Tâche de segment du POST** pour l’ouvrir.

![Segmentation](./images/s2_call.png)

Vous devez également vérifier la variable **En-tête** : champs de votre requête. Accédez à **En-têtes**. Vous verrez alors :

![Postman](./images/s2headers.png)

| Clé | Valeur |
| -------------- | ------------------ |
| x-sandbox-name | `--aepSandboxId--` |

>[!NOTE]
>
>Vous devez spécifier le nom de l’environnement de test Adobe Experience Platform que vous utilisez. Votre x-sandbox-name doit être `--aepSandboxId--`.

Cliquez sur le bouton bleu **Envoyer** bouton .

Vous devriez voir un résultat similaire :

![Segmentation](./images/s2_call_response.png)

Cette tâche de segmentation est maintenant en cours d’exécution, ce qui peut prendre un certain temps. À l’étape 3, vous pourrez vérifier l’état de cette tâche.


### Étape 3 - État de la tâche de segmentation du GET

Accédez à Postman.

![Segmentation](./images/pmdtl.png)

Dans votre collection Postman, cliquez sur la requête nommée **Étape 3 - État de la tâche de segmentation du GET**.

![Segmentation](./images/s3_call.png)

Vous devez également vérifier la variable **En-tête** : champs de votre requête. Accédez à **En-têtes**. Vous verrez alors :

![Postman](./images/s3headers.png)

| Clé | Valeur |
| -------------- | ------------------ |
| x-sandbox-name | `--aepSandboxId--` |

>[!NOTE]
>
>Vous devez spécifier le nom de l’environnement de test Adobe Experience Platform que vous utilisez. Votre x-sandbox-name doit être `--aepSandboxId--`.

Cliquez sur le bouton bleu **Envoyer** bouton .

Vous devriez voir un résultat similaire :

![Segmentation](./images/s3_status.png)

Dans cet exemple, la variable **status** de la tâche est définie sur **QUEUED**.

Répétez cette requête en cliquant sur le bouton bleu **Envoyer** toutes les deux minutes jusqu’à la valeur **status** est défini sur **SUCCEEDED**.

![Segmentation](./images/s3_status_succeeded.png)

Une fois que l’état est **SUCCEEDED**, votre tâche de segmentation s’est exécutée et les clients sont désormais qualifiés pour le segment.

Félicitations, vous avez terminé l’exercice de segmentation. Examinons maintenant comment Real-time Customer Profile peut être activé dans l’ensemble de l’entreprise.

Étape suivante : [3.6 Voir Real-time Customer Profile en action dans le centre d’appels](./ex6.md)

[Revenir au module 3](./real-time-customer-profile.md)

[Revenir à tous les modules](../../overview.md)
