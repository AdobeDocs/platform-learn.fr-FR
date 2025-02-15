---
title: Utilisation des API Photoshop
description: Découvrez comment utiliser les API Photoshop et les services Firefly
role: Developer
level: Beginner
jira: KT-5342
doc-type: Tutorial
exl-id: 60eecc24-1713-4fec-9ffa-a3186db1a8ca
source-git-commit: f20a4fc49cc3f3ac411e4017179d0ae2f83df9c3
workflow-type: tm+mt
source-wordcount: '939'
ht-degree: 0%

---

# 1.1.3 Utilisation des API Photoshop

Découvrez comment utiliser les API Photoshop et les services Firefly.

## 1.1.3.1 Mettre à jour votre intégration Adobe I/O

1. Accédez à [https://developer.adobe.com/console/home](https://developer.adobe.com/console/home){target="_blank"}.

![Nouvelle intégration Adobe I/O](./images/iohome.png){zoomable="yes"}

1. Accédez à **Projets** et sélectionnez le projet que vous avez créé dans l’exercice précédent, appelé `--aepUserLdap-- Firefly`.

![ Stockage Azure ](./images/ps1.png){zoomable="yes"}

1. Sélectionnez **+ Ajouter au projet** puis sélectionnez **API**.

![ Stockage Azure ](./images/ps2.png){zoomable="yes"}

1. Sélectionnez **Creative Cloud** puis **Photoshop - Services Firefly**. Sélectionnez **Suivant**.

![ Stockage Azure ](./images/ps3.png){zoomable="yes"}

1. Sélectionnez **Suivant**.

![ Stockage Azure ](./images/ps4.png){zoomable="yes"}

Ensuite, vous devez sélectionner un profil de produit qui définit les autorisations disponibles pour cette intégration.

1. Sélectionnez **Configuration des services Firefly par défaut** et **Configuration des services Creative Cloud Automation par défaut**.

1. Sélectionnez **Enregistrer l’API configurée**.

![ Stockage Azure ](./images/ps5.png){zoomable="yes"}

Votre projet Adobe I/O est maintenant mis à jour pour fonctionner avec les API Photoshop et Firefly Services.

![ Stockage Azure ](./images/ps6.png){zoomable="yes"}

## 1.1.3.2 Interagir par programmation avec un fichier PSD

1. Téléchargez [citisignal-fibre.psd](./../../../assets/ff/citisignal-fiber.psd){target="_blank"} sur votre bureau.

1. Ouvrez **citisignal-fibre.psd** dans Photoshop.

![ Stockage Azure ](./images/ps7.png){zoomable="yes"}

Dans le volet **Calques**, le concepteur du fichier a attribué un nom unique à chaque calque. Vous pouvez afficher les informations sur le calque en ouvrant le fichier PSD dans Photoshop, mais vous pouvez également le faire par programmation.

Envoyons votre première requête d’API aux API Photoshop.

1. Dans Postman, avant d’envoyer des requêtes d’API à Photoshop, vous devez vous authentifier auprès d’Adobe I/O. Ouvrez la requête précédente nommée **POST - Get Access Token**.

1. Accédez à **Params** et vérifiez que le paramètre **Scope** est correctement défini. La **Valeur** pour **Portée** doit se présenter comme suit :

`openid,session,AdobeID,read_organizations,additional_info.projectedProductContext, ff_apis, firefly_api`

1. Sélectionnez **Envoyer**.

![ Stockage Azure ](./images/ps8.png){zoomable="yes"}

Vous disposez désormais d’un jeton d’accès valide pour interagir avec les API Photoshop.

![ Stockage Azure ](./images/ps9.png){zoomable="yes"}

### API Photoshop - Bonjour le monde

Ensuite, disons bonjour aux API Photoshop pour tester si toutes les autorisations et tous les accès sont correctement définis.

1. Dans la collection **Photoshop**, ouvrez la requête **Photoshop Hello (Tester l’authentification).**. Sélectionnez **Envoyer**.

![ Stockage Azure ](./images/ps10.png){zoomable="yes"}

Vous devriez recevoir la réponse **Bienvenue dans l’API Photoshop !**.

![ Stockage Azure ](./images/ps11.png){zoomable="yes"}

Ensuite, pour interagir par programmation avec le fichier PSD **citisignal-fibre.psd**, vous devez le charger sur votre compte de stockage . Vous pouvez le faire manuellement, en le faisant glisser et en le déposant dans votre conteneur à l’aide de l’explorateur de stockage Azure, mais cette fois, vous devez le faire via l’API.

### Chargement de PSD vers Azure

1. Dans Postman, ouvrez la demande **Chargement de PSD vers le compte de stockage Azure**. Dans l’exercice précédent, vous avez configuré ces variables d’environnement dans Postman, que vous allez utiliser maintenant :

- `AZURE_STORAGE_URL`
- `AZURE_STORAGE_CONTAINER`
- `AZURE_STORAGE_SAS_READ`
- `AZURE_STORAGE_SAS_WRITE`

Comme vous pouvez le voir dans la requête **Charger PSD sur le compte de stockage Azure**, l’URL est configurée pour utiliser ces variables.

![ Stockage Azure ](./images/ps12.png){zoomable="yes"}

1. Dans **Body**, sélectionnez le fichier **citisignal-fibre.psd**.

![ Stockage Azure ](./images/ps13.png){zoomable="yes"}

1. Votre écran devrait ressembler à ceci. Sélectionnez **Envoyer**.

![ Stockage Azure ](./images/ps14.png){zoomable="yes"}

Vous devriez obtenir cette réponse vide en retour d’Azure, ce qui signifie que votre fichier est stocké dans votre conteneur dans votre compte de stockage Azure.

![ Stockage Azure ](./images/ps15.png){zoomable="yes"}

Si vous utilisez Azure Storage Explorer pour consulter votre fichier, veillez à actualiser votre dossier.

![ Stockage Azure ](./images/ps16.png){zoomable="yes"}

### API Photoshop - Obtenir le manifeste

Ensuite, vous devez obtenir le fichier manifeste de votre fichier PSD.

1. Dans Postman, ouvrez la requête **Photoshop - Obtenir le manifeste PSD**. Accédez à **Corps**.

Le corps doit ressembler à ceci :

```json
{
  "inputs": [
    {
      "storage": "external",
      "href": "{{AZURE_STORAGE_URL}}/{{AZURE_STORAGE_CONTAINER}}/citisignal-fiber.psd{{AZURE_STORAGE_SAS_READ}}"
    }
  ],
  "options": {
    "thumbnails": {
      "type": "image/jpeg"
    }
  }
}
```

1. Sélectionnez **Envoyer**.

Un lien s’affiche désormais dans la réponse. Les opérations dans Photoshop pouvant parfois prendre un certain temps, Photoshop fournit un fichier de statut en réponse à la plupart des requêtes entrantes. Pour comprendre ce qui se passe avec votre requête, vous devez lire le fichier de statut.

![ Stockage Azure ](./images/ps17.png){zoomable="yes"}

1. Pour lire le fichier de statut, ouvrez la requête **Photoshop - Obtenir le statut PS**. Vous pouvez constater que cette requête utilise une variable comme URL, qui est une variable définie par la requête précédente que vous avez envoyée, **Photoshop - Get PSD Manifest**. Les variables sont définies dans les **Scripts** de chaque requête. Sélectionnez **Envoyer**.

![ Stockage Azure ](./images/ps18.png){zoomable="yes"}

Votre écran devrait ressembler à ceci. Actuellement, le statut est défini sur **en attente**, ce qui signifie que le processus n’est pas encore terminé.

![ Stockage Azure ](./images/ps19.png){zoomable="yes"}

1. Sélectionnez Envoyer plusieurs fois de plus sur **Photoshop - Obtenir le statut PS**, jusqu&#39;à ce que le statut passe à **réussi**. Cela peut prendre quelques minutes.

Lorsque la réponse est disponible, vous pouvez voir que le fichier json contient des informations sur tous les calques du fichier PSD. Il s’agit d’informations utiles, car des éléments tels que le nom ou l’identifiant du calque peuvent être identifiés.

![ Stockage Azure ](./images/ps20.png){zoomable="yes"}

Par exemple, recherchez le `2048x2048-cta` de texte . Votre écran doit ressembler à ceci :

![ Stockage Azure ](./images/ps21.png){zoomable="yes"}

### API Photoshop - Modifier le texte

Vous devez ensuite modifier le texte de l’appel à l’action à l’aide des API.

1. Dans Postman, ouvrez la requête **Photoshop - Modifier le texte** et accédez à **Corps**.

Votre écran doit ressembler à ceci :

- tout d&#39;abord, un fichier d&#39;entrée est spécifié : `citisignal-fiber.psd`
- ensuite, le calque à modifier est spécifié, avec le texte à modifier
- troisièmement, un fichier de sortie est spécifié : `citisignal-fiber-changed-text.psd`

```json
{
  "inputs": [
    {
      "storage": "external",
      "href": "{{AZURE_STORAGE_URL}}/{{AZURE_STORAGE_CONTAINER}}/citisignal-fiber.psd{{AZURE_STORAGE_SAS_READ}}"
    }
  ],
  "options": {
    "layers": [
      {
        "name": "2048x2048-cta",
        "text": {
          "content": "Get Fiber now!"
        }
      }
    ]
  },
  "outputs": [
    {
      "storage": "azure",
      "href": "{{AZURE_STORAGE_URL}}/{{AZURE_STORAGE_CONTAINER}}/citisignal-fiber-changed-text.psd{{AZURE_STORAGE_SAS_WRITE}}",
      "type": "vnd.adobe.photoshop",
      "overwrite": true
    }
  ]
}
```

Le fichier de sortie porte un nom différent, car vous ne souhaitez pas remplacer le fichier d’entrée d’origine.

1. Sélectionnez **Envoyer**.

![ Stockage Azure ](./images/ps23.png){zoomable="yes"}

Comme auparavant, la réponse contient un lien pointant vers le fichier de statut qui effectue le suivi de la progression.

![ Stockage Azure ](./images/ps22.png){zoomable="yes"}

1. Pour lire le fichier de statut, ouvrez la requête **Photoshop - Obtenir le statut PS** et sélectionnez **Envoyer**. Si le statut n’est pas défini sur **réussi** attendez immédiatement quelques secondes, puis sélectionnez à nouveau **Envoyer**.

1. Sélectionnez l’URL pour télécharger le fichier de sortie.

![ Stockage Azure ](./images/ps24.png){zoomable="yes"}

1. Ouvrez **citisignal-fibre-changed-text.psd** après avoir téléchargé le fichier sur votre ordinateur. Vous devriez voir que l’espace réservé pour l’appel à l’action a été remplacé par le texte **Get Fiber now !**.

![ Stockage Azure ](./images/ps25.png){zoomable="yes"}

Vous pouvez également voir ce fichier dans votre conteneur à l’aide de l’explorateur de stockage Azure.

![ Stockage Azure ](./images/ps26.png){zoomable="yes"}

## Étapes suivantes

Accédez à l’API [Modèles personnalisés Firefly](./ex4.md){target="_blank"}

Revenez à [ Présentation des services Adobe Firefly ](./firefly-services.md){target="_blank"}

Revenir à [Tous les modules](./../../../overview.md){target="_blank"}
