---
title: Optimisez votre processus Firefly à l’aide de Microsoft Azure et des URL présignées
description: Découvrez comment optimiser votre processus Firefly à l’aide de Microsoft Azure et des URL prédéfinies
role: Developer
level: Beginner
jira: KT-5342
doc-type: tutorial
exl-id: 5f9803a4-135c-4470-bfbb-a298ab1fee33
source-git-commit: a1da1c73cbddacde00211190a1ca3d36f7a2c329
workflow-type: tm+mt
source-wordcount: '1944'
ht-degree: 1%

---

# 1.1.2 Optimisez votre processus Firefly à l’aide de Microsoft Azure et des URL présignées.

Découvrez comment optimiser votre processus Firefly à l’aide de Microsoft Azure et des URL présignées.

## 1.1.2.1 Que sont les URL présignées ?

Une URL présignée est une URL qui vous accorde un accès temporaire à un objet spécifique dans un emplacement de stockage. En utilisant l’URL, un utilisateur peut par exemple LIRE l’objet ou ÉCRIRE un objet (ou mettre à jour un objet existant). L’URL contient des paramètres spécifiques définis par votre application.

Dans le contexte de la création de l’automatisation de la chaîne d’approvisionnement du contenu, plusieurs opérations de fichiers doivent souvent se produire pour un cas d’utilisation spécifique. Par exemple, il se peut que l’arrière-plan d’un fichier doive être modifié, que le texte de différents calques doive être modifié, etc. Il n’est pas toujours possible d’effectuer toutes les opérations de fichier en même temps, ce qui rend nécessaire une approche à plusieurs étapes. Après chaque étape intermédiaire, la sortie est alors un fichier temporaire qui est nécessaire pour que l’étape suivante soit exécutée. Une fois cette étape suivante exécutée, le fichier temporaire perd rapidement de la valeur et n’est souvent plus nécessaire, il doit donc être supprimé.

Adobe Firefly Services prend actuellement en charge les domaines suivants :

- Amazon AWS : *.amazonaws.com
- Microsoft Azure : *.windows.net
- Dropbox : *.dropboxusercontent.com

La raison pour laquelle des solutions de stockage dans le cloud sont souvent utilisées, c’est que les ressources intermédiaires en cours de création perdent rapidement de la valeur. Le problème résolu par les URL présignées est souvent mieux résolu avec une solution de stockage de ressources, qui est généralement l’un des services cloud ci-dessus.

L’écosystème Adobe comprend également des solutions de stockage, telles que Frame.io, Workfront Fusion et Adobe Experience Manager Assets. Ces solutions prennent également en charge les URL présignées, ce qui fait qu’il s’agit souvent d’un choix à effectuer lors de la mise en œuvre. Le choix est alors souvent basé sur une combinaison d&#39;applications déjà disponibles et de coûts de stockage.

Par conséquent, les URL présignées sont utilisées conjointement avec les opérations Adobe Firefly Services pour les raisons suivantes :

- les entreprises ont souvent besoin de traiter plusieurs modifications apportées à la même image à des étapes intermédiaires, ce qui nécessite un stockage intermédiaire.
- L’accès à la lecture et à l’écriture à partir des emplacements d’espace de stockage dans le cloud doit être sécurisé. Dans un environnement côté serveur, il n’est pas possible de se connecter manuellement. La sécurité doit donc être directement intégrée à l’URL.

Une URL présignée utilise trois paramètres pour limiter l’accès à l’utilisateur :

- Emplacement de stockage : il peut s’agir d’un emplacement de compartiment AWS S3, d’un emplacement de compte de stockage Microsoft Azure avec conteneur
- Nom de fichier : le fichier spécifique qui doit être lu, mis à jour, supprimé.
- Paramètre de chaîne de requête : un paramètre de chaîne de requête commence toujours par un point d’interrogation et est suivi d’une série complexe de paramètres

Exemple :

- **Amazon AWS** : `https://bucket.s3.eu-west-2.amazonaws.com/image.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AXXXXXXXXXX%2Feu-west-2%2Fs3%2Faws4_request&X-Amz-Date=20250510T171315Z&X-Amz-Expires=1800&X-Amz-Signature=XXXXXXXXX&X-Amz-SignedHeaders=host`
- **Microsoft Azure** : `https://storageaccount.blob.core.windows.net/container/image.png?sv=2023-01-03&st=2025-01-13T07%3A16%3A52Z&se=2026-01-14T07%3A16%3A00Z&sr=b&sp=r&sig=XXXXXX%3D`

## 1.1.2.2 Créer un abonnement Azure

>[!NOTE]
>
>Si vous disposez déjà d’un abonnement Azure, vous pouvez ignorer cette étape. Dans ce cas, veuillez procéder au prochain exercice.

>[!NOTE]
>
>Si vous suivez ce tutoriel dans le cadre d’un atelier guidé en personne ou d’une formation guidée à la demande, vous avez probablement déjà accès à un compte de stockage Azure Microsoft. Dans ce cas, vous n’avez pas besoin de créer votre propre compte. Veuillez utiliser le compte qui vous a été fourni dans le cadre de la formation.

Accédez à [https://portal.azure.com](https://portal.azure.com){target="_blank"} et connectez-vous avec votre compte Azure. Si vous n’en avez pas, veuillez utiliser votre adresse e-mail personnelle pour créer votre compte Azure.

![&#x200B; Stockage Azure &#x200B;](./images/02azureportalemail.png){zoomable="yes"}

Une fois la connexion établie, l’écran suivant s’affiche :

![&#x200B; Stockage Azure &#x200B;](./images/03azureloggedin.png){zoomable="yes"}

Dans le menu de gauche, sélectionnez **Toutes les ressources**, l’écran d’abonnement Azure s’affiche si vous n’êtes pas encore abonné.

Si vous n’êtes pas abonné, sélectionnez **Commencer avec une version d’évaluation gratuite d’Azure**.

![&#x200B; Stockage Azure &#x200B;](./images/04azurestartsubscribe.png){zoomable="yes"}

Remplissez le formulaire d&#39;abonnement Azure et fournissez votre téléphone mobile et votre carte de crédit pour l&#39;activation (vous aurez un niveau gratuit pendant 30 jours et vous ne serez pas facturé, sauf si vous effectuez une mise à niveau).

Une fois le processus d’abonnement terminé, tout est prêt.

![&#x200B; Stockage Azure &#x200B;](./images/06azuresubscriptionok.png){zoomable="yes"}

## 1.1.2.3 Créer Un Compte De Stockage Azure

Recherchez `storage account` puis sélectionnez **Comptes de stockage**.

![&#x200B; Stockage Azure &#x200B;](./images/azs1.png){zoomable="yes"}

Sélectionnez **+ Créer**.

![&#x200B; Stockage Azure &#x200B;](./images/azs2.png){zoomable="yes"}

Sélectionnez votre **Abonnement** et sélectionnez (ou créez) un **Groupe de ressources**.

Sous **Nom du compte de stockage** utilisez `--aepUserLdap--`.

Sélectionnez **Réviser + créer**.

![&#x200B; Stockage Azure &#x200B;](./images/azs3.png){zoomable="yes"}

Sélectionnez **Créer**.

![&#x200B; Stockage Azure &#x200B;](./images/azs4.png){zoomable="yes"}

Après confirmation, sélectionnez **Accéder à la ressource**.

![&#x200B; Stockage Azure &#x200B;](./images/azs5.png){zoomable="yes"}

Votre compte de stockage Azure est maintenant prêt à être utilisé.

![&#x200B; Stockage Azure &#x200B;](./images/azs6.png){zoomable="yes"}

Sélectionnez **Stockage de données**, puis accédez à **Conteneurs**. Sélectionnez Conteneur **+**.

![&#x200B; Stockage Azure &#x200B;](./images/azs7.png){zoomable="yes"}

Utilisez `--aepUserLdap--` pour le nom et sélectionnez **Créer**.

![&#x200B; Stockage Azure &#x200B;](./images/azs8.png){zoomable="yes"}

Votre conteneur est maintenant prêt à être utilisé.

![&#x200B; Stockage Azure &#x200B;](./images/azs9.png){zoomable="yes"}

## 1.1.2.4 Installer l’explorateur de stockage Azure

[Téléchargez l’explorateur de stockage Azure Microsoft pour gérer vos fichiers](https://azure.microsoft.com/en-us/products/storage/storage-explorer#Download-4){target="_blank"}. Sélectionnez la version appropriée pour votre système d’exploitation spécifique, téléchargez-la et installez-la.

![&#x200B; Stockage Azure &#x200B;](./images/az10.png){zoomable="yes"}

Ouvrez l’application et sélectionnez **Se connecter avec Azure**.

![&#x200B; Stockage Azure &#x200B;](./images/az11.png){zoomable="yes"}

Sélectionnez **Abonnement**.

![&#x200B; Stockage Azure &#x200B;](./images/az12.png){zoomable="yes"}

Sélectionnez **Azure** puis **Suivant**.

![&#x200B; Stockage Azure &#x200B;](./images/az13.png){zoomable="yes"}

Sélectionnez votre compte Microsoft Azure et terminez le processus d’authentification.

![&#x200B; Stockage Azure &#x200B;](./images/az14.png){zoomable="yes"}

Une fois l’authentification terminée, ce message s’affiche.

![&#x200B; Stockage Azure &#x200B;](./images/az15.png){zoomable="yes"}

De retour dans l’application Microsoft Azure Storage Explorer, sélectionnez votre abonnement et choisissez **Ouvrir l’explorateur**.

>[!NOTE]
>
>Si votre compte n’apparaît pas, cliquez sur l’icône **engrenage** en regard de votre adresse e-mail et sélectionnez **Annuler le filtrage**.

![&#x200B; Stockage Azure &#x200B;](./images/az16.png){zoomable="yes"}

Votre compte de stockage apparaît sous **Comptes de stockage**.

![&#x200B; Stockage Azure &#x200B;](./images/az17.png){zoomable="yes"}

Ouvrez **Conteneurs Blob** puis sélectionnez le conteneur que vous avez créé dans l’exercice précédent.

![&#x200B; Stockage Azure &#x200B;](./images/az18.png){zoomable="yes"}

## 1.1.2.5 Chargement manuel du fichier et utilisation d’un fichier image comme référence de style

Chargez un fichier image de votre choix ou [ce fichier](./images/gradient.jpg){target="_blank"} dans le conteneur.

>[!NOTE]
>
>Lorsque vous utilisez des images comme référence de style, référence de composition ou image de masque, les types d’image suivants sont acceptés :
>- image/jpeg
>- image/png
>- image/webp

![&#x200B; Stockage Azure &#x200B;](./images/gradient.jpg)

Une fois le chargement effectué, vous pouvez le voir dans votre conteneur :

![&#x200B; Stockage Azure &#x200B;](./images/az19.png){zoomable="yes"}

Cliquez avec le bouton droit sur `gradient.jpg`, puis sélectionnez **Obtenir la signature d’accès partagé**.

![&#x200B; Stockage Azure &#x200B;](./images/az20.png){zoomable="yes"}

Sous **Autorisations**, seule la mention **Lecture** est requise. Sélectionnez **Créer**.

![&#x200B; Stockage Azure &#x200B;](./images/az21.png){zoomable="yes"}

Copiez l’URL prédéfinie de ce fichier image pour la prochaine demande d’API dans Firefly.

![&#x200B; Stockage Azure &#x200B;](./images/az22.png){zoomable="yes"}

De retour dans Postman, ouvrez la requête **POST - Firefly - T2I (styleref) V3**.
Elle apparaît dans **Corps**.

![&#x200B; Stockage Azure &#x200B;](./images/az23.png){zoomable="yes"}

Remplacez l’URL de l’espace réservé par l’URL présignée pour votre fichier image et sélectionnez **Envoyer**.

![&#x200B; Stockage Azure &#x200B;](./images/az24.png){zoomable="yes"}

Ouvrez la nouvelle image du Firefly Services de réponse dans votre navigateur.

![&#x200B; Stockage Azure &#x200B;](./images/az25.png){zoomable="yes"}

Une autre image apparaît avec `horses in a field`, mais cette fois, le style est similaire au fichier image que vous avez fourni comme référence de style.

![&#x200B; Stockage Azure &#x200B;](./images/az26.png){zoomable="yes"}

## 1.1.2.6 Chargement de fichier par programmation

Pour utiliser le chargement de fichiers par programmation avec des comptes de stockage Azure, vous devez créer un jeton **Signature d’accès partagé (SAS)** avec des autorisations qui vous permettent d’écrire un fichier.

Dans l’explorateur de stockage Azure, cliquez avec le bouton droit sur votre conteneur, puis sélectionnez **Obtenir la signature d’accès partagé**.

![&#x200B; Stockage Azure &#x200B;](./images/az27.png){zoomable="yes"}

Sous **Autorisations**, sélectionnez les autorisations requises suivantes :

- **Lecture**
- **Ajouter**
- **Create**
- **Write**
- **Liste**

Sélectionnez **Créer**.

![&#x200B; Stockage Azure &#x200B;](./images/az28.png){zoomable="yes"}

Après avoir reçu votre **Signature d’accès partagé**, sélectionnez **Copier** pour copier l’URL.

![&#x200B; Stockage Azure &#x200B;](./images/az29.png){zoomable="yes"}

Utilisez l’**URL du jeton SAS** pour charger un fichier dans votre compte de stockage Azure.

De retour dans Postman, sélectionnez le dossier **FF - Firefly Services Tech Insiders**, puis sélectionnez **...** dans le dossier **Firefly** et enfin sélectionnez **Ajouter une requête**.

![&#x200B; Stockage Azure &#x200B;](./images/az30.png){zoomable="yes"}

Modifiez le nom de la requête vide en **Télécharger le fichier sur le compte de stockage Azure**, modifiez le **Type de requête** en **PUT** et collez l’URL du jeton SAS dans la section URL, puis sélectionnez **Corps**.

![&#x200B; Stockage Azure &#x200B;](./images/az31.png){zoomable="yes"}

Sélectionnez ensuite un fichier sur votre ordinateur local ou utilisez un autre fichier image situé [ici](./images/gradient2-p.jpg){target="_blank"}.

![Fichier de dégradé](./images/gradient2-p.jpg)

Dans **Corps**, sélectionnez **binaire** puis **Sélectionner un fichier**, puis sélectionnez **+ Nouveau fichier à partir de l’ordinateur local**.

![&#x200B; Stockage Azure &#x200B;](./images/az32.png){zoomable="yes"}

Sélectionnez le fichier de votre choix et sélectionnez **Ouvrir**.

![&#x200B; Stockage Azure &#x200B;](./images/az33.png){zoomable="yes"}

Indiquez ensuite le nom du fichier à utiliser dans votre compte de stockage Azure en plaçant votre curseur devant le point d’interrogation **?** dans l’URL comme suit :

![&#x200B; Stockage Azure &#x200B;](./images/az34.png){zoomable="yes"}

L’URL ressemble actuellement à ceci, mais doit être modifiée.

`https://vangeluw.blob.core.windows.net/vangeluw?sv=2023-01-03...`

Remplacez le nom du fichier par `gradient2-p.jpg`, puis modifiez l’URL afin d’inclure le nom du fichier comme suit :

`https://vangeluw.blob.core.windows.net/vangeluw/gradient2-p.jpg?sv=2023-01-03...`

![&#x200B; Stockage Azure &#x200B;](./images/az34a.png){zoomable="yes"}

Accédez ensuite à **En-têtes** pour ajouter manuellement un nouvel en-tête comme celui-ci :

| Clé | Valeur |
|:-------------:| :---------------:| 
| `x-ms-blob-type` | `BlockBlob` |


![&#x200B; Stockage Azure &#x200B;](./images/az35.png){zoomable="yes"}

Accédez à **Autorisation** et définissez le **Type d’authentification** sur **Aucune authentification**, puis sélectionnez **Envoyer**.

![&#x200B; Stockage Azure &#x200B;](./images/az36.png){zoomable="yes"}

Ensuite, cette réponse vide s’affiche dans Postman, ce qui signifie que votre chargement de fichier est correct.

![&#x200B; Stockage Azure &#x200B;](./images/az37.png){zoomable="yes"}

De retour dans l’explorateur de stockage Azure, actualisez le contenu de votre dossier pour faire apparaître le fichier nouvellement chargé.

![&#x200B; Stockage Azure &#x200B;](./images/az38.png){zoomable="yes"}

## 1.1.2.7 Utilisation des fichiers par programmation

Pour lire par programmation les fichiers des comptes de stockage Azure à long terme, vous devez créer un jeton **Signature d’accès partagé (SAS)** avec des autorisations qui vous permettent de lire un fichier. Techniquement, vous pouvez utiliser le jeton SAS créé dans l’exercice précédent, mais il est recommandé d’avoir un jeton distinct avec uniquement des autorisations **Lecture** et un jeton distinct avec uniquement des autorisations **Écriture**.

### Jeton SAS de lecture à long terme

Revenez à l’Explorateur de stockage Azure, cliquez avec le bouton droit sur votre conteneur, puis sélectionnez **Obtenir la signature d’accès partagé**.

![&#x200B; Stockage Azure &#x200B;](./images/az27.png){zoomable="yes"}

Sous **Autorisations**, sélectionnez les autorisations requises suivantes :

- **Lecture**
- **Liste**

Définissez **Délai d’expiration** sur 1 an à partir de maintenant.

Sélectionnez **Créer**.

![&#x200B; Stockage Azure &#x200B;](./images/az100.png){zoomable="yes"}

Copiez l’URL et écrivez-la dans un fichier sur votre ordinateur pour obtenir votre jeton SAS à long terme avec les autorisations de lecture.

![&#x200B; Stockage Azure &#x200B;](./images/az101.png){zoomable="yes"}

Votre URL doit se présenter comme suit :

`https://vangeluw.blob.core.windows.net/vangeluw?sv=2023-01-03&st=2025-01-13T07%3A36%3A35Z&se=2026-01-14T07%3A36%3A00Z&sr=c&sp=rl&sig=4r%2FcSJLlt%2BSt9HdFdN0VzWURxRK6UqhB8TEvbWkmAag%3D`

Vous pouvez dériver quelques valeurs de l’URL ci-dessus :

- `AZURE_STORAGE_URL` : `https://vangeluw.blob.core.windows.net`
- `AZURE_STORAGE_CONTAINER` : `vangeluw`
- `AZURE_STORAGE_SAS_READ` : `?sv=2023-01-03&st=2025-01-13T07%3A36%3A35Z&se=2026-01-14T07%3A36%3A00Z&sr=c&sp=rl&sig=4r%2FcSJLlt%2BSt9HdFdN0VzWURxRK6UqhB8TEvbWkmAag%3D`

### Jeton SAS d’écriture à long terme

Revenez à l’Explorateur de stockage Azure, cliquez avec le bouton droit sur votre conteneur et sélectionnez **Obtenir la signature d’accès partagé**.

![&#x200B; Stockage Azure &#x200B;](./images/az27.png){zoomable="yes"}

Sous **Autorisations**, sélectionnez les autorisations requises suivantes :

- **Lecture**
- **Liste**
- **Ajouter**
- **Create**
- **Write**

Définissez la variable **Délai d’expiration** sur 1 an à partir de maintenant.

Sélectionnez **Créer**.

![&#x200B; Stockage Azure &#x200B;](./images/az102.png){zoomable="yes"}

Copiez l’URL et écrivez-la dans un fichier sur votre ordinateur pour obtenir votre jeton SAS à long terme avec les autorisations de lecture/écriture.

![&#x200B; Stockage Azure &#x200B;](./images/az103.png){zoomable="yes"}

Votre URL doit se présenter comme suit :

`https://vangeluw.blob.core.windows.net/vangeluw?sv=2023-01-03&st=2025-01-13T07%3A38%3A59Z&se=2026-01-14T07%3A38%3A00Z&sr=c&sp=acw&sig=lR9%2FMUfyYLcBK7W9Kv7YJdYz5HEEEovExAdOCOCUdMk%3D`

Vous pouvez dériver quelques valeurs de l’URL ci-dessus :

- `AZURE_STORAGE_URL` : `https://vangeluw.blob.core.windows.net`
- `AZURE_STORAGE_CONTAINER` : `vangeluw`
- `AZURE_STORAGE_SAS_READ` : `?sv=2023-01-03&st=2025-01-13T07%3A36%3A35Z&se=2026-01-14T07%3A36%3A00Z&sr=c&sp=rl&sig=4r%2FcSJLlt%2BSt9HdFdN0VzWURxRK6UqhB8TEvbWkmAag%3D`
- `AZURE_STORAGE_SAS_WRITE` : `?sv=2023-01-03&st=2025-01-13T07%3A38%3A59Z&se=2026-01-14T07%3A38%3A00Z&sr=c&sp=acw&sig=lR9%2FMUfyYLcBK7W9Kv7YJdYz5HEEEovExAdOCOCUdMk%3D`

### Variables dans Postman

Comme vous pouvez le voir dans la section ci-dessus, il existe des variables communes dans les jetons Lecture et Écriture .

Vous devez ensuite créer des variables dans Postman qui stockent les différents éléments des jetons SAS ci-dessus. Certaines valeurs sont identiques dans les deux URL :

- `AZURE_STORAGE_URL` : `https://vangeluw.blob.core.windows.net`
- `AZURE_STORAGE_CONTAINER` : `vangeluw`
- `AZURE_STORAGE_SAS_READ` : `?sv=2023-01-03&st=2025-01-13T07%3A36%3A35Z&se=2026-01-14T07%3A36%3A00Z&sr=c&sp=rl&sig=4r%2FcSJLlt%2BSt9HdFdN0VzWURxRK6UqhB8TEvbWkmAag%3D`
- `AZURE_STORAGE_SAS_WRITE` : `?sv=2023-01-03&st=2025-01-13T07%3A38%3A59Z&se=2026-01-14T07%3A38%3A00Z&sr=c&sp=acw&sig=lR9%2FMUfyYLcBK7W9Kv7YJdYz5HEEEovExAdOCOCUdMk%3D`

Pour les interactions d’API futures, la principale chose qui change est le nom de la ressource, tandis que les variables ci-dessus restent les mêmes. Dans ce cas, il est logique de créer des variables dans Postman afin de ne pas avoir à les spécifier manuellement à chaque fois.

Dans Postman, sélectionnez **Environnements**, ouvrez **Toutes les variables** et sélectionnez **Environnement**.

![&#x200B; Stockage Azure &#x200B;](./images/az104.png){zoomable="yes"}

Créez ces 4 variables dans le tableau qui s’affiche. Pour les colonnes **Valeur initiale** et **Valeur actuelle**, saisissez vos valeurs personnelles spécifiques.

- `AZURE_STORAGE_URL` : votre url
- `AZURE_STORAGE_CONTAINER` : nom de votre conteneur
- `AZURE_STORAGE_SAS_READ` : votre jeton de lecture SAS
- `AZURE_STORAGE_SAS_WRITE` : votre jeton d’écriture SAS

Sélectionnez **Enregistrer**.

![&#x200B; Stockage Azure &#x200B;](./images/az105.png){zoomable="yes"}

### Variables dans PostBuster

Comme vous pouvez le voir dans la section ci-dessus, il existe des variables communes dans les jetons Lecture et Écriture .

Vous devez ensuite créer des variables dans PostBuster qui stockent les différents éléments des jetons SAS ci-dessus. Certaines valeurs sont identiques dans les deux URL :

- `AZURE_STORAGE_URL` : `https://vangeluw.blob.core.windows.net`
- `AZURE_STORAGE_CONTAINER` : `vangeluw`
- `AZURE_STORAGE_SAS_READ` : `?sv=2023-01-03&st=2025-01-13T07%3A36%3A35Z&se=2026-01-14T07%3A36%3A00Z&sr=c&sp=rl&sig=4r%2FcSJLlt%2BSt9HdFdN0VzWURxRK6UqhB8TEvbWkmAag%3D`
- `AZURE_STORAGE_SAS_WRITE` : `?sv=2023-01-03&st=2025-01-13T07%3A38%3A59Z&se=2026-01-14T07%3A38%3A00Z&sr=c&sp=acw&sig=lR9%2FMUfyYLcBK7W9Kv7YJdYz5HEEEovExAdOCOCUdMk%3D`

Ouvrez PostBuster. Sélectionnez **Environnement de base** puis cliquez sur l’icône **Modifier** pour ouvrir l’environnement de base.

![&#x200B; Stockage Azure &#x200B;](./images/pbbe1.png)

Vous verrez alors 4 variables vides. Saisissez les détails de votre compte de stockage Azure ici.

![&#x200B; Stockage Azure &#x200B;](./images/pbbe2.png)

Votre fichier d’environnement de base doit maintenant se présenter comme suit : Cliquez sur **Fermer**.

![&#x200B; Stockage Azure &#x200B;](./images/pbbe3.png)

### Tester votre configuration

Dans l’un des exercices précédents, le **Corps** de votre requête **Firefly - T2I (styleref) V3** ressemblait à ceci :

`"url": "https://vangeluw.blob.core.windows.net/vangeluw/gradient.jpg?sv=2023-01-03&st=2025-01-13T07%3A16%3A52Z&se=2026-01-14T07%3A16%3A00Z&sr=b&sp=r&sig=x4B1XZuAx%2F6yUfhb28hF0wppCOMeH7Ip2iBjNK5A%2BFw%3D"`

![&#x200B; Stockage Azure &#x200B;](./images/az24.png){zoomable="yes"}

Modifiez l’URL en :

`"url": "{{AZURE_STORAGE_URL}}/{{AZURE_STORAGE_CONTAINER}}/gradient.jpg{{AZURE_STORAGE_SAS_READ}}"`

Sélectionnez **Envoyer** pour tester les modifications que vous avez apportées.

![&#x200B; Stockage Azure &#x200B;](./images/az106.png){zoomable="yes"}

Si les variables ont été configurées correctement, une URL d’image est renvoyée.

![&#x200B; Stockage Azure &#x200B;](./images/az107.png){zoomable="yes"}

Ouvrez l’URL de l’image pour vérifier votre image.

![&#x200B; Stockage Azure &#x200B;](./images/az108.jpg)

## Étapes suivantes

Accédez à [&#x200B; Utilisation des API Photoshop &#x200B;](./ex3.md){target="_blank"}

Revenez à [&#x200B; Présentation de Adobe Firefly Services &#x200B;](./firefly-services.md){target="_blank"}

Revenir à [Tous les modules](./../../../overview.md){target="_blank"}