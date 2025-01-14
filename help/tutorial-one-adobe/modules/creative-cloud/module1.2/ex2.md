---
title: Prise en main des services Firefly
description: Prise en main des services Firefly
kt: 5342
doc-type: tutorial
exl-id: 23ebf8b4-3f16-474c-afe1-520d88331417
source-git-commit: a0c16a47372d322a7931578adca30a246b537183
workflow-type: tm+mt
source-wordcount: '594'
ht-degree: 2%

---

# 1.2.2 Utilisation d’API Adobes dans Workfront Fusion

## 1.2.2.1 utiliser l’API Firefly Text To Image avec Workfront Fusion

Pointez sur le deuxième nœud **Définir plusieurs variables** et cliquez sur **+** pour ajouter un autre module.

![WF Fusion](./images/wffusion48.png)

Recherchez **http**, puis sélectionnez **HTTP**.

![WF Fusion](./images/wffusion49.png)

Sélectionnez **Effectuer une requête**.

![WF Fusion](./images/wffusion50.png)

Sélectionnez les variables suivantes :

- **URL** : `https://firefly-api.adobe.io/v3/images/generate`
- **Méthode** : `POST`

Cliquez sur **Ajouter un en-tête**.

![WF Fusion](./images/wffusion51.png)

Vous devez saisir les en-têtes suivants :

| Clé | Valeur |
|:-------------:| :---------------:| 
| `x-api-key` | votre variable stockée pour `CONST_client_id` |
| `Authorization` | `Bearer ` + votre variable stockée pour `bearer_token` |
| `Content-Type` | `application/json` |
| `Accept` | `*/*` |

Saisissez les détails de la `x-api-key`. Cliquez sur **Ajouter**.

![WF Fusion](./images/wffusion52.png)

Cliquez sur **Ajouter un en-tête**.

![WF Fusion](./images/wffusion53.png)

Saisissez les détails de la `Authorization`. Cliquez sur **Ajouter**.

![WF Fusion](./images/wffusion54.png)

Cliquez sur **Ajouter un en-tête**. Saisissez les détails de la `Content-Type`. Cliquez sur **Ajouter**.

![WF Fusion](./images/wffusion541.png)

Cliquez sur **Ajouter un en-tête**. Saisissez les détails de la `Accept`. Cliquez sur **Ajouter**.

![WF Fusion](./images/wffusion542.png)

Définissez le **Type de corps** sur **Brut**. Pour **Type de contenu**, sélectionnez **JSON (application/json)**.

![WF Fusion](./images/wffusion55.png)

Collez cette payload dans le champ **Demander le contenu**.

```json
{
  "numVariations": 1,
  "size": {
    "width": 2048,
    "height": 2048
  },
  "prompt": "Horses in a field",
  "promptBiasingLocaleCode": "en-US"
}
```

Cochez la case **Analyser la réponse**. Cliquez sur **OK**.

![WF Fusion](./images/wffusion56.png)

Cliquez sur **Exécuter une fois**.

![WF Fusion](./images/wffusion57.png)

Une fois votre scénario exécuté, vous devriez voir ceci.

![WF Fusion](./images/wffusion58.png)

Cliquez sur le **?** l’icône sur le quatrième nœud, HTTP, pour afficher la réponse. Vous devriez voir un fichier image dans la réponse.

![WF Fusion](./images/wffusion59.png)

Copiez l’URL de l’image et ouvrez-la dans une fenêtre de navigateur. Vous devriez alors voir quelque chose comme ceci :

![WF Fusion](./images/wffusion60.png)

Cliquez avec le bouton droit sur l’objet **HTTP** et renommez-le en **Firefly T2I**.

![WF Fusion](./images/wffusion62.png)

Cliquez sur **Enregistrer** pour enregistrer vos modifications.

![WF Fusion](./images/wffusion61.png)

## 1.2.2.2 utiliser l’API Photoshop avec Workfront Fusion

Cliquez sur l’icône **clé à molette** entre les nœuds **Définir le jeton du porteur** et **T2I du Firefly**. Sélectionnez **Ajouter un routeur**.

![WF Fusion](./images/wffusion63.png)

Cliquez avec le bouton droit sur l&#39;objet T2I **du Firefly** et sélectionnez **Cloner**.

![WF Fusion](./images/wffusion64.png)

Faites glisser et déposez l’objet cloné à proximité de l’objet **Router** pour qu’il se connecte automatiquement à l’objet **Router**. Tu devrais avoir ça.

![WF Fusion](./images/wffusion65.png)

Vous disposez désormais d’une copie identique basée sur la requête HTTP T2I **du Firefly**. Certains des paramètres de la requête HTTP T2I **du Firefly** sont similaires à ceux dont vous avez besoin pour interagir avec l’API **Photoshop**, ce qui vous permet de gagner du temps. Il vous suffit désormais de modifier les variables qui ne sont pas les mêmes, comme l’URL de requête et la payload.

Remplacez **URL** par `https://image.adobe.io/pie/psdService/text`.

![WF Fusion](./images/wffusion66.png)

Remplacez le **Demander du contenu** par la payload ci-dessous :

```json
{
  "inputs": [
    {
      "storage": "external",
      "href": "{{AZURE_STORAGE_URL}}/{{AZURE_STORAGE_CONTAINER}}/sevoi-psd.psd{{AZURE_STORAGE_SAS_READ}}"
    }
  ],
  "options": {
    "layers": [
      {
        "name": "2048x2048-button",
        "text": {
          "content": "Click here"
        }
      },
      {
        "name": "2048x2048-cta",
        "text": {
          "content": "Buy this stuff"
        }
      }
    ]
  },
  "outputs": [
    {
      "storage": "azure",
      "href": "{{AZURE_STORAGE_URL}}/{{AZURE_STORAGE_CONTAINER}}/sevoi-psd-changed-text.psd{{AZURE_STORAGE_SAS_WRITE}}",
      "type": "vnd.adobe.photoshop",
      "overwrite": true
    }
  ]
}
```

![WF Fusion](./images/wffusion67.png)

Pour que ce **Demander du contenu** fonctionne correctement, certaines variables sont manquantes :

- `AZURE_STORAGE_URL`
- `AZURE_STORAGE_CONTAINER`
- `AZURE_STORAGE_SAS_READ`
- `AZURE_STORAGE_SAS_WRITE`

Revenez à votre premier nœud, cliquez sur **Initialiser les constantes** puis sélectionnez **Ajouter un élément** pour chacune de ces variables.

![WF Fusion](./images/wffusion69.png)

| Clé | Exemple de valeur |
|:-------------:| :---------------:| 
| `AZURE_STORAGE_URL` | `https://vangeluw.blob.core.windows.net` |
| `AZURE_STORAGE_CONTAINER` | `vangeluw` |
| `AZURE_STORAGE_SAS_READ` | `?sv=2023-01-03&st=2025-01-13T07%3A36%3A35Z&se=2026-01-14T07%3A36%3A00Z&sr=c&sp=rl&sig=4r%2FcSJLlt%2BSt9HdFdN0VzWURxRK6UqhB8TEvbWkmAag%3D` |
| `AZURE_STORAGE_SAS_WRITE` | `?sv=2023-01-03&st=2025-01-13T17%3A21%3A09Z&se=2025-01-14T17%3A21%3A09Z&sr=c&sp=racwl&sig=FD4m0YyyqUj%2B5T8YyTFJDi55RiTDC9xKtLTgW0CShps%3D` |

Vous pouvez retrouver vos variables en revenant à Postman, puis en ouvrant votre **Variables d’environnement**.

![ Stockage Azure ](./../module1.1/images/az105.png)

Copiez ces valeurs dans Workfront Fusion et ajoutez un nouvel élément pour chacune de ces 4 variables.

Tu devrais avoir ça. Cliquez sur **OK**.

![WF Fusion](./images/wffusion68.png)

Ensuite, revenez à la requête HTTP clonée pour mettre à jour le **contenu de la requête**. Vous remarquerez ces variables noires dans la **Demander du contenu**, qui sont les variables que vous avez copiées à partir de Postman. Vous devez maintenant les modifier en fonction des variables que vous venez de définir dans Workfront Fusion. Remplacez chaque variable une par une en supprimant le texte noir et en le remplaçant par la variable correcte.

![WF Fusion](./images/wffusion70.png)

La section **entrées** comporte 3 modifications à apporter.

![WF Fusion](./images/wffusion71.png)

Il y a également 3 modifications à apporter à la section **sorties**. Cliquez sur **OK**.

![WF Fusion](./images/wffusion72.png)

Cliquez avec le bouton droit sur le nœud cloné, puis sélectionnez **Renommer**. Remplacez le nom par **Photoshop Modifier le texte**.

![WF Fusion](./images/wffusion73.png)

Tu devrais avoir ça.

![WF Fusion](./images/wffusion74.png)

Étape Suivante : [1.2.3 ...](./ex3.md)

[Retour au module 1.2](./automation.md)

[Revenir à tous les modules](./../../../overview.md)
