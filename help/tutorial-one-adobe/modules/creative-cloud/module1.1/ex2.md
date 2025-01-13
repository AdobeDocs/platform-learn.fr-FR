---
title: Prise en main des services Firefly
description: Prise en main des services Firefly
kt: 5342
doc-type: tutorial
exl-id: 5f9803a4-135c-4470-bfbb-a298ab1fee33
source-git-commit: 6d627312073bb2cecd724226f1730aed7133700c
workflow-type: tm+mt
source-wordcount: '1500'
ht-degree: 1%

---

# 1.1.2 Optimisation du processus de Firefly à l’aide de Microsoft Azure et des URL présignées

## 1.1.2.1 Créer un abonnement Azure

>[!NOTE]
>
>Si vous disposez déjà d’un abonnement Azure, vous pouvez ignorer cette étape. Dans ce cas, veuillez procéder au prochain exercice.

Accédez à [https://portal.azure.com](https://portal.azure.com) et connectez-vous avec votre compte Azure. Si vous n’en avez pas, veuillez utiliser votre adresse e-mail personnelle pour créer votre compte Azure.

![ Stockage Azure ](./images/02azureportalemail.png)

Une fois la connexion établie, l’écran suivant s’affiche :

![ Stockage Azure ](./images/03azureloggedin.png)

Cliquez sur le menu de gauche et sélectionnez **Toutes les ressources**. L’écran d’abonnement Azure s’affiche si vous n’êtes pas encore abonné. Dans ce cas, sélectionnez **Démarrer avec une version d’évaluation gratuite d’Azure**.

![ Stockage Azure ](./images/04azurestartsubscribe.png)

Remplissez le formulaire d&#39;abonnement Azure, fournissez votre téléphone mobile et votre carte de crédit pour l&#39;activation (vous aurez un niveau gratuit pendant 30 jours et vous ne serez pas facturé, sauf si vous effectuez une mise à niveau).

Une fois le processus d’abonnement terminé, tout est prêt :

![ Stockage Azure ](./images/06azuresubscriptionok.png)

## 1.1.2.2 Créer Un Compte De Stockage Azure

Recherchez `storage account` puis cliquez sur **Comptes de stockage**.

![ Stockage Azure ](./images/azs1.png)

Cliquez sur **+ Créer**.

![ Stockage Azure ](./images/azs2.png)

Renseignez les détails suivants :

- Sélectionnez votre **abonnement**
- Sélectionner (ou créer) un **groupe de ressources**
- **Nom du compte de stockage** : utilisez `--aepUserLdap--`

Cliquez sur **Vérifier + créer**.

![ Stockage Azure ](./images/azs3.png)

Cliquez sur **Créer**.

![ Stockage Azure ](./images/azs4.png)

Vous obtiendrez alors une confirmation similaire. Cliquez sur **Accéder à la ressource**.

![ Stockage Azure ](./images/azs5.png)

Votre compte de stockage Azure est maintenant prêt à être utilisé.

![ Stockage Azure ](./images/azs6.png)

Cliquez sur **Stockage de données** puis accédez à **Conteneurs**. Cliquez sur **+ Conteneur**.

![ Stockage Azure ](./images/azs7.png)

Pour le nom, utilisez `--aepUserLdap--`. Cliquez sur **Créer**.

![ Stockage Azure ](./images/azs8.png)

Votre conteneur est maintenant prêt à être utilisé.

![ Stockage Azure ](./images/azs9.png)

## 1.1.2.3 Installer l’explorateur de stockage Azure

Vous utiliserez l’explorateur de stockage Azure Microsoft pour gérer vos fichiers. Vous pouvez le télécharger via [ce lien](https://azure.microsoft.com/en-us/products/storage/storage-explorer#Download-4). Sélectionnez la version adaptée à votre système d’exploitation, téléchargez-la et installez-la.

![ Stockage Azure ](./images/az10.png)

Une fois l’application installée, ouvrez-la. Vous verrez quelque chose de similaire à ceci. Cliquez sur **Se connecter avec Azure**.

![ Stockage Azure ](./images/az11.png)

Cliquez sur **Abonnement**.

![ Stockage Azure ](./images/az12.png)

Sélectionnez **Azure** et cliquez sur **Suivant**.

![ Stockage Azure ](./images/az13.png)

Sélectionnez votre compte Microsoft Azure et terminez le processus d’authentification.

![ Stockage Azure ](./images/az14.png)

Une fois authentifié, un message comme celui-ci s’affiche.

![ Stockage Azure ](./images/az15.png)

Revenez à l’application Explorateur de stockage Azure Microsoft. Sélectionnez votre abonnement et cliquez sur **Ouvrir l’explorateur**.

![ Stockage Azure ](./images/az16.png)

Vous trouverez ensuite votre compte de stockage sous **Comptes de stockage**.

![ Stockage Azure ](./images/az17.png)

Ouvrez **Conteneurs Blob**, puis cliquez sur le conteneur que vous avez créé dans l’exercice précédent.

![ Stockage Azure ](./images/az18.png)

## 1.1.2.4 Chargement manuel du fichier et utilisation d’un fichier image comme référence de style

Vous devez maintenant charger un fichier image de votre choix dans votre conteneur. Vous pouvez utiliser n’importe quel fichier image de votre choix ou [ce fichier](./images/gradient.jpg) en le téléchargeant sur votre ordinateur.

![ Stockage Azure ](./images/gradient.jpg)

Déposez le fichier image dans votre conteneur dans l’explorateur de stockage Azure.

Une fois le chargement effectué, il s’affiche dans votre conteneur :

![ Stockage Azure ](./images/az19.png)

Cliquez avec le bouton droit sur votre `gradient.jpg` de fichier, puis cliquez sur **Obtenir la signature d&#39;accès partagé**.

![ Stockage Azure ](./images/az20.png)

Sous **Autorisations**, seule la mention **Lecture** est requise. Cliquez sur **Créer**.

![ Stockage Azure ](./images/az21.png)

L’URL qui vous a été assignée pour ce fichier image s’affiche alors. Copiez-le comme vous en aurez besoin pour la prochaine demande d’API dans Firefly.

![ Stockage Azure ](./images/az22.png)

Revenez à Postman. Ouvrez la demande **POST - Firefly - T2I (styleref) V3**. Vous verrez alors ceci dans **Body**.

![ Stockage Azure ](./images/az23.png)

Remplacez l’URL de l’espace réservé par l’URL présignée de votre fichier image, que vous avez copiée à partir de l’explorateur de stockage Azure. Tu auras alors ceci. Cliquez sur **Envoyer**.

![ Stockage Azure ](./images/az24.png)

Vous obtiendrez ensuite une réponse des services de Firefly, avec une nouvelle image. Ouvrez le fichier image dans votre navigateur.

![ Stockage Azure ](./images/az25.png)

Vous verrez ensuite une autre image avec `horses in a field`, mais cette fois, le style sera similaire au fichier image que vous avez fourni comme référence de style.

![ Stockage Azure ](./images/az26.png)

## 1.1.2.5 Chargement de fichier par programmation

Pour utiliser le chargement de fichiers par programmation avec des comptes de stockage Azure, vous devez créer un jeton **Signature d’accès partagé (SAS)**, avec des autorisations qui vous permettent d’écrire un fichier.

Pour ce faire, revenez à l’Explorateur de stockage Azure. Cliquez avec le bouton droit sur votre conteneur, puis cliquez sur **Obtenir la signature d&#39;accès partagé**.

![ Stockage Azure ](./images/az27.png)

Sous **Autorisations**, les autorisations suivantes sont requises :

- **Lecture**
- **Ajouter**
- **Create**
- **Write**
- **Liste**

Cliquez sur **Créer**.

![ Stockage Azure ](./images/az28.png)

Vous obtiendrez alors votre **jeton SAS**. Cliquez sur **Copier**.

![ Stockage Azure ](./images/az29.png)

Vous pouvez désormais utiliser ce **jeton SAS** pour charger un fichier dans votre compte de stockage Azure. Revenez à Postman pour ce faire.

Cliquez pour sélectionner le dossier **FF - Firefly Services Tech Insiders**, puis cliquez sur le **à 3 points...** dans le dossier **Firefly** et enfin sur **Ajouter une demande**.

![ Stockage Azure ](./images/az30.png)

Vous obtiendrez alors une requête vide. Modifiez le nom de la requête en **Charger le fichier sur le compte de stockage Azure**, modifiez le **Type de requête** en **PUT** et collez l’URL du jeton SAS dans la section URL.

Cliquez ensuite sur **Corps**.

![ Stockage Azure ](./images/az31.png)

Vous devez maintenant sélectionner un fichier sur votre ordinateur local. Vous pouvez utiliser un nouveau fichier image de votre choix ou un autre fichier image que vous pouvez trouver [ici](./images/gradient2-p.jpg).

![Fichier de dégradé](./images/gradient2-p.jpg)

Dans **Body**, sélectionnez **binary**, puis cliquez sur **Select file**, puis sur **+ New file from local machine**.

![ Stockage Azure ](./images/az32.png)

Sélectionnez le fichier de votre choix et cliquez sur **Ouvrir**.

![ Stockage Azure ](./images/az33.png)

Tu verras ça. La prochaine chose à faire est de spécifier le nom du fichier qui sera utilisé dans votre compte de stockage Azure. Pour ce faire, vous devez placer votre curseur devant le point d&#39;interrogation **?** dans l’URL. Vous pouvez actuellement le voir ici :

![ Stockage Azure ](./images/az34.png)

L’URL ressemble actuellement à ceci, mais devra être modifiée.

`https://vangeluw.blob.core.windows.net/vangeluw?sv=2023-01-03...`

Le nom de fichier à utiliser est `gradient2-p.jpg`, ce qui signifie que l’URL doit être modifiée pour inclure le nom du fichier, comme suit :

`https://vangeluw.blob.core.windows.net/vangeluw/gradient2-p.jpg?sv=2023-01-03...`

![ Stockage Azure ](./images/az34a.png)

Accédez ensuite à **En-têtes** où vous devez ajouter manuellement un nouvel en-tête. Utilisez la commande suivante :

| Clé | Valeur |
|:-------------:| :---------------:| 
| `x-ms-blob-type` | `BlockBlob` |


![ Stockage Azure ](./images/az35.png)

Accédez à **Autorisation** et définissez le **Type d’authentification** sur **Aucune authentification**. Cliquez sur **Envoyer**.

![ Stockage Azure ](./images/az36.png)

Cette réponse vide s’affiche alors dans Postman, ce qui signifie que votre chargement de fichier s’est correctement déroulé.

![ Stockage Azure ](./images/az37.png)

Si vous revenez ensuite à l’Explorateur de stockage Azure et actualisez le contenu de votre dossier, le fichier nouvellement chargé s’y trouve désormais.

![ Stockage Azure ](./images/az38.png)

## 1.1.2.5 Utilisation des fichiers par programmation

Pour utiliser à long terme la lecture par programmation de fichiers à partir des comptes de stockage Azure, vous devez créer un jeton **Signature d’accès partagé (SAS)**, avec des autorisations qui vous permettent de lire un fichier. Techniquement, vous pouvez utiliser le jeton SAS que vous avez créé dans l’exercice précédent, mais il est recommandé d’utiliser un jeton distinct avec uniquement des autorisations **Lecture** et un jeton distinct avec uniquement des autorisations **Écriture**.

### Jeton SAS de lecture à long terme

Pour ce faire, revenez à l’Explorateur de stockage Azure. Cliquez avec le bouton droit sur votre conteneur, puis cliquez sur **Obtenir la signature d&#39;accès partagé**.

![ Stockage Azure ](./images/az27.png)

Sous **Autorisations**, les autorisations suivantes sont requises :

- **Lecture**
- **Liste**

Définissez la variable **Délai d’expiration** sur 1 an à partir de maintenant.

Cliquez sur **Créer**.

![ Stockage Azure ](./images/az100.png)

Vous obtiendrez ensuite votre jeton SAS à long terme avec des autorisations de lecture. Copiez l’URL et notez-la dans un fichier sur votre ordinateur.

![ Stockage Azure ](./images/az101.png)

Votre URL ressemblera à ceci :

`https://vangeluw.blob.core.windows.net/vangeluw?sv=2023-01-03&st=2025-01-13T07%3A36%3A35Z&se=2026-01-14T07%3A36%3A00Z&sr=c&sp=rl&sig=4r%2FcSJLlt%2BSt9HdFdN0VzWURxRK6UqhB8TEvbWkmAag%3D`

Vous pouvez dériver quelques valeurs de l’URL ci-dessus :

- `AZURE_STORAGE_URL` : `https://vangeluw.blob.core.windows.net`
- `AZURE_STORAGE_CONTAINER` : `vangeluw`
- `AZURE_STORAGE_SAS_READ` : `?sv=2023-01-03&st=2025-01-13T07%3A36%3A35Z&se=2026-01-14T07%3A36%3A00Z&sr=c&sp=rl&sig=4r%2FcSJLlt%2BSt9HdFdN0VzWURxRK6UqhB8TEvbWkmAag%3D`

### Jeton SAS d’écriture à long terme

Pour ce faire, revenez à l’Explorateur de stockage Azure. Cliquez avec le bouton droit sur votre conteneur, puis cliquez sur **Obtenir la signature d&#39;accès partagé**.

![ Stockage Azure ](./images/az27.png)

Sous **Autorisations**, les autorisations suivantes sont requises :

- **Ajouter**
- **Create**
- **Write**

Définissez la variable **Délai d’expiration** sur 1 an à partir de maintenant.

Cliquez sur **Créer**.

![ Stockage Azure ](./images/az102.png)

Vous obtiendrez ensuite votre jeton SAS à long terme avec des autorisations de lecture. Copiez l’URL et notez-la dans un fichier sur votre ordinateur.

![ Stockage Azure ](./images/az103.png)

Votre URL ressemblera à ceci :

`https://vangeluw.blob.core.windows.net/vangeluw?sv=2023-01-03&st=2025-01-13T07%3A38%3A59Z&se=2026-01-14T07%3A38%3A00Z&sr=c&sp=acw&sig=lR9%2FMUfyYLcBK7W9Kv7YJdYz5HEEEovExAdOCOCUdMk%3D`

Vous pouvez à nouveau dériver quelques valeurs de l’URL ci-dessus :

- `AZURE_STORAGE_URL` : `https://vangeluw.blob.core.windows.net`
- `AZURE_STORAGE_CONTAINER` : `vangeluw`
- `AZURE_STORAGE_SAS_READ` : `?sv=2023-01-03&st=2025-01-13T07%3A36%3A35Z&se=2026-01-14T07%3A36%3A00Z&sr=c&sp=rl&sig=4r%2FcSJLlt%2BSt9HdFdN0VzWURxRK6UqhB8TEvbWkmAag%3D`
- `AZURE_STORAGE_SAS_WRITE` : `?sv=2023-01-03&st=2025-01-13T07%3A38%3A59Z&se=2026-01-14T07%3A38%3A00Z&sr=c&sp=acw&sig=lR9%2FMUfyYLcBK7W9Kv7YJdYz5HEEEovExAdOCOCUdMk%3D`

### Variables dans Postman

Comme vous pouvez le voir dans la section ci-dessus, il existe des variables communes dans les jetons Lecture et Écriture .

Vous devez maintenant créer des variables dans Postman qui stockeront les différents éléments des jetons SAS ci-dessus.
Certaines valeurs sont identiques dans les deux URL :

- `AZURE_STORAGE_URL` : `https://vangeluw.blob.core.windows.net`
- `AZURE_STORAGE_CONTAINER` : `vangeluw`
- `AZURE_STORAGE_SAS_READ` : `?sv=2023-01-03&st=2025-01-13T07%3A36%3A35Z&se=2026-01-14T07%3A36%3A00Z&sr=c&sp=rl&sig=4r%2FcSJLlt%2BSt9HdFdN0VzWURxRK6UqhB8TEvbWkmAag%3D`
- `AZURE_STORAGE_SAS_WRITE` : `?sv=2023-01-03&st=2025-01-13T07%3A38%3A59Z&se=2026-01-14T07%3A38%3A00Z&sr=c&sp=acw&sig=lR9%2FMUfyYLcBK7W9Kv7YJdYz5HEEEovExAdOCOCUdMk%3D`

Pour les interactions d’API futures, la principale chose qui changera sera le nom de la ressource, tandis que les variables ci-dessus resteront les mêmes. Dans ce cas, il est logique de créer des variables dans Postman afin de ne pas avoir à les spécifier manuellement à chaque fois.

Pour ce faire, ouvrez Postman. Cliquez sur l’icône **Environnements**, ouvrez le menu **Toutes les variables** et cliquez sur **Environnement**.

![ Stockage Azure ](./images/az104.png)

Vous voyez alors ceci. Créez ces 4 variables dans le tableau qui s’affiche. Pour les colonnes **Valeur initiale** et **Valeur actuelle**, saisissez vos valeurs personnelles spécifiques.

- `AZURE_STORAGE_URL` : votre url
- `AZURE_STORAGE_CONTAINER` : nom de votre conteneur
- `AZURE_STORAGE_SAS_READ` : votre jeton de lecture SAS
- `AZURE_STORAGE_SAS_WRITE` : votre jeton d’écriture SAS

Cliquez sur **Enregistrer**.

![ Stockage Azure ](./images/az105.png)

Dans l’un des exercices précédents, le **Corps** de votre requête **Firefly - T2I (styleref) V3** ressemblait à ceci :

`"url": "https://vangeluw.blob.core.windows.net/vangeluw/gradient.jpg?sv=2023-01-03&st=2025-01-13T07%3A16%3A52Z&se=2026-01-14T07%3A16%3A00Z&sr=b&sp=r&sig=x4B1XZuAx%2F6yUfhb28hF0wppCOMeH7Ip2iBjNK5A%2BFw%3D"`

![ Stockage Azure ](./images/az24.png)

Vous pouvez maintenant modifier l’URL en :

`"url": "{{AZURE_STORAGE_URL}}/{{AZURE_STORAGE_CONTAINER}}/gradient.jpg{{AZURE_STORAGE_SAS_READ}}"`

Cliquez sur **Envoyer** pour tester les modifications que vous avez apportées.

![ Stockage Azure ](./images/az106.png)

Si les variables ont été configurées correctement, une URL d’image s’affiche alors renvoyée.

![ Stockage Azure ](./images/az107.png)

Ouvrez l’URL de l’image pour vérifier votre image.

![ Stockage Azure ](./images/az108.png)

Étape suivante : [1.1.3 Adobe Firefly et Adobe Photoshop](./ex3.md)

[Retour au module 1.1](./firefly-services.md)

[Revenir à tous les modules](./../../../overview.md)
