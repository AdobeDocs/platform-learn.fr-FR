---
title: Exécuter votre workflow personnalisé par programmation
description: Exécuter votre workflow personnalisé par programmation
role: Developer
level: Beginner
jira: KT-5342
doc-type: Tutorial
source-git-commit: a3a78b12f8244c8288eb0fffc82ad769776eb118
workflow-type: tm+mt
source-wordcount: '910'
ht-degree: 0%

---

# 1.7.2 Exécuter votre workflow personnalisé par programmation

## 1.7.2.1 Exécuter un workflow personnalisé avec Postman

Après avoir publié votre workflow dans l’exercice précédent, vous devriez voir un élément similaire à ceci. Cliquez sur le bouton **Copier** pour copier l’exemple de payload.

![Workflows personnalisés Firefly](./images/ffcw61.png)

Ouvrez Postman et créez une **collection** en utilisant le nom **Workflows personnalisés Firefly**. Cliquez ensuite sur **Ajouter une requête**.

![Workflows personnalisés Firefly](./images/ffcw62.png)

Vous devriez alors voir une nouvelle requête vide. Dans la barre d’adresse, collez la payload que vous avez copiée à partir du workflow publié.

Postman reconnaîtra la commande cURL que vous avez collée et prendra toutes les informations de la payload et les ajoutera dans la requête de la manière appropriée.

![Workflows personnalisés Firefly](./images/ffcw63.png)

Vous devriez maintenant voir ces variables **Header**.

![Workflows personnalisés Firefly](./images/ffcw64.png)

Accédez à **Corps**, où vous devriez voir quelque chose de similaire à ceci.

![Workflows personnalisés Firefly](./images/ffcw65.png)

Vous devez maintenant fournir les instructions requises dans le corps de cette requête. Lorsque vous utilisez des fichiers par programmation, l’utilisation d’URL prédéfinies est requise. Pour cet exercice, vous trouverez ci-dessous des URL prédéfinies pour les 3 images qui font partie de cet exercice. Ces URL prédéfinies ont été créées à l’aide des fonctionnalités de stockage Microsoft Azure. Si vous souhaitez en savoir plus sur la création d’URL présignées, cliquez ici : [Optimisation de votre processus Firefly à l’aide de Microsoft Azure et des URL présignées](./../module1.1/ex2.md).

Pour cet exercice, vous pouvez utiliser les URL ci-dessous afin de ne pas avoir à créer de nouvelles URL prédéfinies.

- **airpods.jpg**

```
https://techinsiders.blob.core.windows.net/vangeluw/airpods.jpg?sv=2023-01-03&st=2026-03-11T01%3A22%3A04Z&se=2027-03-12T01%3A22%3A00Z&sr=b&sp=r&sig=MmQi9lS4lm4DJM1BELmZZM7VLa4ln5zYOcuGisLnrz4%3D
```

- **watch.jpg**

```
https://techinsiders.blob.core.windows.net/vangeluw/watch.jpg?sv=2023-01-03&st=2026-03-11T01%3A26%3A54Z&se=2027-03-12T01%3A26%3A00Z&sr=b&sp=r&sig=xCwQ09E%2F%2FT%2B7RLcb31Fum4uUBfsX0xHITKZTz4Ds9Zs%3D
```

- **phone.jpg**

```
https://techinsiders.blob.core.windows.net/vangeluw/phone.png?sv=2023-01-03&st=2026-03-11T01%3A27%3A20Z&se=2027-03-12T01%3A27%3A00Z&sr=b&sp=r&sig=VVbX88P2sFSHHo9lmgoRhXRIXb42c0nDQhM9Z8nUG%2Bc%3D
```

Vous devez également fournir des invites dans le cadre de la requête Postman. Vous trouverez ci-dessous les invites à utiliser.

- **Invite 1** :

```
magazine quality photo of a phone on a red pedestal with a pink background surrounded by origami style pink paper hearts
```

- **Invite 2** :

```
background hearts fluttering
```

Voici un exemple de payload, mais vous ne pouvez pas le copier et le réutiliser, car les champs **node_id** sont propres à votre workflow. Par conséquent, nous allons simplement vous donner une idée de l’aspect que doit prendre la payload :

```json
{
    "workflow": {
        "workflowId": "e0c63806-cf7c-442d-8884-26d57e9c0518",
        "inputs": [
            [
                {
                    "node_id": "node_1772156869527_d8mjasues_1_u10dlg",
                    "content": [
                        {
                            "presignedUrl": "https://techinsiders.blob.core.windows.net/vangeluw/airpods.jpg?sv=2023-01-03&st=2026-03-11T01%3A22%3A04Z&se=2027-03-12T01%3A22%3A00Z&sr=b&sp=r&sig=MmQi9lS4lm4DJM1BELmZZM7VLa4ln5zYOcuGisLnrz4%3D",
                            "storageType": "Azure"
                        }
                    ]
                },
                {
                    "node_id": "node_1772157264659_oq2csr2nn_5_fh5hek",
                    "content": "magazine quality photo of a phone on a red pedestal with a pink background surrounded by origami style pink paper hearts"
                },
                {
                    "node_id": "node_1772157397147_qdwxiyktg_8_nm0o2k",
                    "content": "background hearts fluttering"
                }
            ]
        ]
    }
}
```

Une fois la payload modifiée, elle doit se présenter comme suit : Une fois que vous avez terminé, cliquez sur **Envoyer**. Ensuite, utilisez **CMD + S** ou **CTRL + S** pour **enregistrer** votre requête.

![Workflows personnalisés Firefly](./images/ffcw66.png)

Dans la payload de réponse, vous pouvez désormais trouver quelques liens. Ces liens permettent d’interroger le **statut** du workflow. Une fois le statut **terminé**, vous pouvez utiliser l’URL **résultats** pour récupérer l’image et la vidéo générées.

Sélectionnez l’URL **status** et copiez-la.

![Workflows personnalisés Firefly](./images/ffcw67.png)

Cliquez sur les 3 points de la requête que vous utilisez actuellement, puis sélectionnez **Dupliquer**.

![Workflows personnalisés Firefly](./images/ffcw69.png)

Dans la nouvelle requête, modifiez le type de requête en **GET** et remplacez l’URL par l’URL de statut que vous venez de copier.

![Workflows personnalisés Firefly](./images/ffcw70.png)

Sous **Corps**, assurez-vous que tout est supprimé. Cliquez ensuite sur **Envoyer**. Vous devriez ensuite recevoir une payload de réponse similaire, qui affichera un statut . Vous pouvez envoyer à nouveau cette demande jusqu&#39;à ce que le statut soit passé à **terminé**. N’oubliez pas d’utiliser **CMD + S** ou **CTRL + S** pour **enregistrer** votre demande.

![Workflows personnalisés Firefly](./images/ffcw71.png)

Revenez à la première requête **POST**. Copiez maintenant l’URL **results**.

![Workflows personnalisés Firefly](./images/ffcw72.png)

Cliquez sur le **de 3 points...** sur la deuxième demande que vous avez créée, puis sélectionnez **Dupliquer**.

![Workflows personnalisés Firefly](./images/ffcw73.png)

Dans la nouvelle requête, collez l’URL **results** que vous avez copiée, puis cliquez sur **Envoyer**. N’oubliez pas d’utiliser **CMD + S** ou **CTRL + S** pour **enregistrer** votre demande.

![Workflows personnalisés Firefly](./images/ffcw74.png)

Faites défiler la page vers le bas dans la payload de réponse, où vous trouverez des références à l’image et à la vidéo qui ont été créées. Cliquez sur les liens pour ouvrir ces fichiers.

![Workflows personnalisés Firefly](./images/ffcw75.png)

Voici l’image qui a été générée.

![Workflows personnalisés Firefly](./images/ffcw76.png)

## 1.7.2.2 Exécuter un workflow personnalisé avec Workfront Fusion

Accédez à [https://experience.adobe.com/](https://experience.adobe.com/){target="_blank"}. Ouvrez **Workfront Fusion**.

![WF Fusion](./images/wffusion1.png)

Accédez à **Scénarios**. Si vous ne disposez pas encore d’un dossier, créez-en un, puis pour le nom du dossier, utilisez : `--aepUserLdap--`. Sélectionnez votre dossier, puis sélectionnez **Créer un scénario**.

![WF Fusion](./images/wffusion2.png)

Vous devriez alors voir ceci.

![WF Fusion](./images/wffusion3.png)

Après avoir publié votre workflow dans l’exercice précédent, vous devriez voir un élément similaire à ceci. Cliquez sur le bouton **Copier** pour copier l’exemple de payload.

![Workflows personnalisés Firefly](./images/ffcw61.png)

Revenez à votre scénario Workfront Fusion. Utilisez **CMD + V** ou **Ctrl + V** pour coller la payload que vous avez copiée dans le scénario. Workfront Fusion détecte automatiquement la requête cURL et crée automatiquement un module **HTTP - Make a request**.

Faites glisser l’icône **horloge** sur le module **HTTP - Make a request**.

![WF Fusion](./images/wffusion5.png)

Vous devriez alors voir ceci. Cliquez sur le module **HTTP - Effectuer une requête** pour l’ouvrir.

![WF Fusion](./images/wffusion6.png)

Vous devriez alors constater que les variables **Header** sont déjà disponibles.

![WF Fusion](./images/wffusion7.png)

Faites défiler la page vers le bas pour afficher la payload par défaut. Cliquez sur l’**icône** comme indiqué pour embellir la payload JSON.

![WF Fusion](./images/wffusion8.png)

Revenez à Postman, à la première requête **POST**. Copiez la payload.

![WF Fusion](./images/wffusion9.png)

Revenez à votre scénario Workfront Fusion. Remplacez la payload par défaut existante par la payload que vous avez copiée à partir de Postman. Cliquez sur l’**icône** comme indiqué pour embellir la payload JSON.

Cochez la case **Analyser la réponse**.

Cliquez sur **OK**.

![WF Fusion](./images/wffusion10.png)

Enregistrez vos modifications, puis cliquez sur **Exécuter une fois**.

![WF Fusion](./images/wffusion11.png)

Une fois votre scénario exécuté, vous pouvez voir une réponse similaire à celle obtenue dans Postman. Grâce à ces informations disponibles dans Workfront Fusion, vous pouvez désormais en tirer parti pour interroger l’URL **status** jusqu’à ce que le statut soit terminé. Une fois cette opération effectuée, vous pouvez utiliser l’URL **results** pour collecter l’image et la vidéo générées.

![WF Fusion](./images/wffusion12.png)

## Étapes suivantes

Revenir aux [workflows personnalisés Firefly](./workflowbuilder.md){target="_blank"}

Revenir à [Tous les modules](./../../../overview.md){target="_blank"}
