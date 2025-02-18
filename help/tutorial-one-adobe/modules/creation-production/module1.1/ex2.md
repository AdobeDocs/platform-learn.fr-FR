---
title: Optimisez votre processus Firefly à l’aide de Microsoft Azure et des URL présignées
description: Découvrez comment optimiser votre processus Firefly à l’aide de Microsoft Azure et des URL prédéfinies
role: Developer
level: Beginner
jira: KT-5342
doc-type: tutorial
exl-id: 5f9803a4-135c-4470-bfbb-a298ab1fee33
source-git-commit: b083a817700320e8e45645702c2868423c1fae99
workflow-type: tm+mt
source-wordcount: '1473'
ht-degree: 1%

---

# 1.1.2 Optimisez votre processus Firefly à l’aide de Microsoft Azure et des URL présignées.

Découvrez comment optimiser votre processus Firefly à l’aide de Microsoft Azure et des URL prédéfinies.

## 1.1.2.1 Créer un abonnement Azure

>[!NOTE]
>
>Si vous disposez déjà d’un abonnement Azure, vous pouvez ignorer cette étape. Dans ce cas, veuillez procéder au prochain exercice.

1. Accédez à [https://portal.azure.com](https://portal.azure.com){target="_blank"} et connectez-vous avec votre compte Azure. Si vous n’en avez pas, veuillez utiliser votre adresse e-mail personnelle pour créer votre compte Azure.

   ![ Stockage Azure ](./images/02azureportalemail.png){zoomable="yes"}

   Une fois la connexion établie, l’écran suivant s’affiche :

   ![ Stockage Azure ](./images/03azureloggedin.png){zoomable="yes"}

1. Dans le menu de gauche, sélectionnez **Toutes les ressources**, l’écran d’abonnement Azure s’affiche si vous n’êtes pas encore abonné.

1. Si vous n’êtes pas abonné, sélectionnez **Commencer avec une version d’évaluation gratuite d’Azure**.

   ![ Stockage Azure ](./images/04azurestartsubscribe.png){zoomable="yes"}

1. Remplissez le formulaire d&#39;abonnement Azure et fournissez votre téléphone mobile et votre carte de crédit pour l&#39;activation (vous aurez un niveau gratuit pendant 30 jours et vous ne serez pas facturé, sauf si vous effectuez une mise à niveau).

   Une fois le processus d’abonnement terminé, tout est prêt.

   ![ Stockage Azure ](./images/06azuresubscriptionok.png){zoomable="yes"}

## 1.1.2.2 Créer Un Compte De Stockage Azure

1. Recherchez `storage account` puis sélectionnez **Comptes de stockage**.

   ![ Stockage Azure ](./images/azs1.png){zoomable="yes"}

1. Sélectionnez **+ Créer**.

![ Stockage Azure ](./images/azs2.png){zoomable="yes"}

1. Sélectionnez votre **Abonnement** et sélectionnez (ou créez) un **Groupe de ressources**.

1. Sous **Nom du compte de stockage** utilisez `--aepUserLdap--`.

1. Sélectionnez **Réviser + créer**.

   ![ Stockage Azure ](./images/azs3.png){zoomable="yes"}

1. Sélectionnez **Créer**.

   ![ Stockage Azure ](./images/azs4.png){zoomable="yes"}

1. Après confirmation, sélectionnez **Accéder à la ressource**.

   ![ Stockage Azure ](./images/azs5.png){zoomable="yes"}

Votre compte de stockage Azure est maintenant prêt à être utilisé.

![ Stockage Azure ](./images/azs6.png){zoomable="yes"}

1. Sélectionnez **Stockage de données**, puis accédez à **Conteneurs**. Sélectionnez Conteneur **+**.

   ![ Stockage Azure ](./images/azs7.png){zoomable="yes"}

1. Utilisez `--aepUserLdap--` pour le nom et sélectionnez **Créer**.

   ![ Stockage Azure ](./images/azs8.png){zoomable="yes"}

   Votre conteneur est maintenant prêt à être utilisé.

   ![ Stockage Azure ](./images/azs9.png){zoomable="yes"}

## 1.1.2.3 Installer l’explorateur de stockage Azure

1. [Téléchargez l’explorateur de stockage Azure Microsoft pour gérer vos fichiers](https://azure.microsoft.com/en-us/products/storage/storage-explorer#Download-4){target="_blank"}. Sélectionnez la version appropriée pour votre système d’exploitation spécifique, téléchargez-la et installez-la.

   ![ Stockage Azure ](./images/az10.png){zoomable="yes"}

1. Ouvrez l’application et sélectionnez **Se connecter avec Azure**.

   ![ Stockage Azure ](./images/az11.png){zoomable="yes"}

1. Sélectionnez **Abonnement**.

   ![ Stockage Azure ](./images/az12.png){zoomable="yes"}

1. Sélectionnez **Azure** puis **Suivant**.

   ![ Stockage Azure ](./images/az13.png){zoomable="yes"}

1. Sélectionnez votre compte Microsoft Azure et terminez le processus d’authentification.

   ![ Stockage Azure ](./images/az14.png){zoomable="yes"}

   Une fois l’authentification terminée, ce message s’affiche.

   ![ Stockage Azure ](./images/az15.png){zoomable="yes"}

1. De retour dans l’application Microsoft Azure Storage Explorer, sélectionnez votre abonnement et choisissez **Ouvrir l’explorateur**.

>[!NOTE]
>
>Si votre compte n’apparaît pas, cliquez sur l’icône **engrenage** en regard de votre adresse e-mail et sélectionnez **Annuler le filtrage**.

![ Stockage Azure ](./images/az16.png){zoomable="yes"}

Votre compte de stockage apparaît sous **Comptes de stockage**.

![ Stockage Azure ](./images/az17.png){zoomable="yes"}

1. Ouvrez **Conteneurs Blob** puis sélectionnez le conteneur que vous avez créé dans l’exercice précédent.

   ![ Stockage Azure ](./images/az18.png){zoomable="yes"}

## 1.1.2.4 Chargement manuel du fichier et utilisation d’un fichier image comme référence de style

1. Chargez un fichier image de votre choix ou [ce fichier](./images/gradient.jpg){target="_blank"} dans le conteneur.

   ![ Stockage Azure ](./images/gradient.jpg)

   Une fois le chargement effectué, vous pouvez le voir dans votre conteneur :

   ![ Stockage Azure ](./images/az19.png){zoomable="yes"}

1. Cliquez avec le bouton droit sur `gradient.jpg`, puis sélectionnez **Obtenir la signature d’accès partagé**.

   ![ Stockage Azure ](./images/az20.png){zoomable="yes"}

1. Sous **Autorisations**, seule la mention **Lecture** est requise. Sélectionnez **Créer**.

   ![ Stockage Azure ](./images/az21.png){zoomable="yes"}

1. Copiez l’URL prédéfinie de ce fichier image pour la prochaine demande d’API dans Firefly.

   ![ Stockage Azure ](./images/az22.png){zoomable="yes"}

1. De retour dans Postman, ouvrez la requête **POST - Firefly - T2I (styleref) V3**.
Il apparaît dans **Corps**.

   ![ Stockage Azure ](./images/az23.png){zoomable="yes"}

1. Remplacez l’URL de l’espace réservé par l’URL présignée pour votre fichier image et sélectionnez **Envoyer**.

   ![ Stockage Azure ](./images/az24.png){zoomable="yes"}

1. Ouvrez la nouvelle image des services Firefly de réponse dans votre navigateur.

   ![ Stockage Azure ](./images/az25.png){zoomable="yes"}

   Une autre image apparaît avec `horses in a field`, mais cette fois, le style est similaire au fichier image que vous avez fourni comme référence de style.

   ![ Stockage Azure ](./images/az26.png){zoomable="yes"}

## 1.1.2.5 Chargement de fichier par programmation

Pour utiliser le chargement de fichiers par programmation avec des comptes de stockage Azure, vous devez créer un jeton **Signature d’accès partagé (SAS)** avec des autorisations qui vous permettent d’écrire un fichier.

1. Dans l’explorateur de stockage Azure, cliquez avec le bouton droit sur votre conteneur, puis sélectionnez **Obtenir la signature d’accès partagé**.

   ![ Stockage Azure ](./images/az27.png){zoomable="yes"}

1. Sous **Autorisations**, sélectionnez les autorisations requises suivantes :

   - **Lecture**
   - **Ajouter**
   - **Create**
   - **Write**
   - **Liste**

1. Sélectionnez **Créer**.

   ![ Stockage Azure ](./images/az28.png){zoomable="yes"}

1. Après avoir reçu votre **jeton SAS**, sélectionnez **Copier**.

   ![ Stockage Azure ](./images/az29.png){zoomable="yes"}

   Utilisez le **jeton SAS** pour charger un fichier dans votre compte de stockage Azure.

1. De retour dans Postman, sélectionnez le dossier **FF - Firefly Services Tech Insiders**, puis sélectionnez **...** dans le dossier **Firefly** et enfin sélectionnez **Ajouter une requête**.

   ![ Stockage Azure ](./images/az30.png){zoomable="yes"}

1. Modifiez le nom de la requête vide en **Télécharger le fichier sur le compte de stockage Azure**, modifiez le **Type de requête** en **PUT** et collez l’URL du jeton SAS dans la section URL, puis sélectionnez **Corps**.

   ![ Stockage Azure ](./images/az31.png){zoomable="yes"}

1. Sélectionnez ensuite un fichier sur votre ordinateur local ou utilisez un autre fichier image situé [ici](./images/gradient2-p.jpg){target="_blank"}.

   ![Fichier de dégradé](./images/gradient2-p.jpg)

1. Dans **Corps**, sélectionnez **binaire** puis **Sélectionner un fichier**, puis sélectionnez **+ Nouveau fichier à partir de l’ordinateur local**.

   ![ Stockage Azure ](./images/az32.png){zoomable="yes"}

1. Sélectionnez le fichier de votre choix et sélectionnez **Ouvrir**.

   ![ Stockage Azure ](./images/az33.png){zoomable="yes"}

1. Indiquez ensuite le nom du fichier à utiliser dans votre compte de stockage Azure en plaçant votre curseur devant le point d’interrogation **?** dans l’URL comme suit :

   ![ Stockage Azure ](./images/az34.png){zoomable="yes"}

   L’URL ressemble actuellement à ceci, mais doit être modifiée.

   `https://vangeluw.blob.core.windows.net/vangeluw?sv=2023-01-03...`

1. Remplacez le nom du fichier par `gradient2-p.jpg`, puis modifiez l’URL afin d’inclure le nom du fichier comme suit :

   `https://vangeluw.blob.core.windows.net/vangeluw/gradient2-p.jpg?sv=2023-01-03...`

   ![ Stockage Azure ](./images/az34a.png){zoomable="yes"}

1. Accédez ensuite à **En-têtes** pour ajouter manuellement un nouvel en-tête comme celui-ci :

   | Clé | Valeur |
   |:-------------:| :---------------:| 
   | `x-ms-blob-type` | `BlockBlob` |


   ![ Stockage Azure ](./images/az35.png){zoomable="yes"}

1. Accédez à **Autorisation** et définissez le **Type d’authentification** sur **Aucune authentification**, puis sélectionnez **Envoyer**.

   ![ Stockage Azure ](./images/az36.png){zoomable="yes"}

1. Ensuite, cette réponse vide s’affiche dans Postman, ce qui signifie que votre chargement de fichier est correct.

   ![ Stockage Azure ](./images/az37.png){zoomable="yes"}

1. De retour dans l’explorateur de stockage Azure, actualisez le contenu de votre dossier pour faire apparaître le fichier nouvellement chargé.

   ![ Stockage Azure ](./images/az38.png){zoomable="yes"}

## 1.1.2.6 Utilisation des fichiers par programmation

Pour lire par programmation les fichiers des comptes de stockage Azure à long terme, vous devez créer un jeton **Signature d’accès partagé (SAS)** avec des autorisations qui vous permettent de lire un fichier. Techniquement, vous pouvez utiliser le jeton SAS créé dans l’exercice précédent, mais il est recommandé d’avoir un jeton distinct avec uniquement des autorisations **Lecture** et un jeton distinct avec uniquement des autorisations **Écriture**.

### Jeton SAS de lecture à long terme

1. Revenez à l’Explorateur de stockage Azure, cliquez avec le bouton droit sur votre conteneur, puis sélectionnez **Obtenir la signature d’accès partagé**.

   ![ Stockage Azure ](./images/az27.png){zoomable="yes"}

1. Sous **Autorisations**, sélectionnez les autorisations requises suivantes :

   - **Lecture**
   - **Liste**

1. Définissez **Délai d’expiration** sur 1 an à partir de maintenant.

1. Sélectionnez **Créer**.

   ![ Stockage Azure ](./images/az100.png){zoomable="yes"}

1. Copiez l’URL et écrivez-la dans un fichier sur votre ordinateur pour obtenir votre jeton SAS à long terme avec les autorisations de lecture.

   ![ Stockage Azure ](./images/az101.png){zoomable="yes"}

   Votre URL doit se présenter comme suit :

   `https://vangeluw.blob.core.windows.net/vangeluw?sv=2023-01-03&st=2025-01-13T07%3A36%3A35Z&se=2026-01-14T07%3A36%3A00Z&sr=c&sp=rl&sig=4r%2FcSJLlt%2BSt9HdFdN0VzWURxRK6UqhB8TEvbWkmAag%3D`

   Vous pouvez dériver quelques valeurs de l’URL ci-dessus :

   - `AZURE_STORAGE_URL` : `https://vangeluw.blob.core.windows.net`
   - `AZURE_STORAGE_CONTAINER` : `vangeluw`
   - `AZURE_STORAGE_SAS_READ` : `?sv=2023-01-03&st=2025-01-13T07%3A36%3A35Z&se=2026-01-14T07%3A36%3A00Z&sr=c&sp=rl&sig=4r%2FcSJLlt%2BSt9HdFdN0VzWURxRK6UqhB8TEvbWkmAag%3D`

### Jeton SAS d’écriture à long terme

1. Revenez à l’Explorateur de stockage Azure, cliquez avec le bouton droit sur votre conteneur et sélectionnez **Obtenir la signature d’accès partagé**.

   ![ Stockage Azure ](./images/az27.png){zoomable="yes"}

1. Sous **Autorisations**, sélectionnez les autorisations requises suivantes :

   - **Lecture**
   - **Liste**
   - **Ajouter**
   - **Create**
   - **Write**

1. Définissez la variable **Délai d’expiration** sur 1 an à partir de maintenant.

1. Sélectionnez **Créer**.

   ![ Stockage Azure ](./images/az102.png){zoomable="yes"}

1. Copiez l’URL et écrivez-la dans un fichier sur votre ordinateur pour obtenir votre jeton SAS à long terme avec les autorisations de lecture.

   ![ Stockage Azure ](./images/az103.png){zoomable="yes"}

   Votre URL doit se présenter comme suit :

   `https://vangeluw.blob.core.windows.net/vangeluw?sv=2023-01-03&st=2025-01-13T07%3A38%3A59Z&se=2026-01-14T07%3A38%3A00Z&sr=c&sp=acw&sig=lR9%2FMUfyYLcBK7W9Kv7YJdYz5HEEEovExAdOCOCUdMk%3D`

Vous pouvez dériver quelques valeurs de l’URL ci-dessus :

    - `AZURE_STORAGE_URL` : `https://vangeluw.blob.core.windows.net`
    - `AZURE_STORAGE_CONTAINER` : `vangeluw`
    - `AZURE_STORAGE_SAS_READ` : `?sv=2023-01-03&amp;st=2025-01-13T07%3A36%3A35Z&amp;se=2026-01-14T07%3A36%3A00Z&amp;sr=c&amp;sp=rl&amp;sig=4r%2FcSJLlt%2BSt9HdFdN0VzWURxRK6UqhB8TEvbWkmAag_SAS%3D`
    - AZURE `?sv=2023-01-03&amp;st=2025-01-13T07%3A38%3A59Z&amp;se=2026-01-14T07%3A38%3A00Z&amp;sr=c&amp;sp=acw&amp;sig=lR9%2FMUfyYLcBK7W9Kv7YJdYz5HEEEovExAdOCOCUdMk%3D`

### Variables dans Postman

Comme vous pouvez le voir dans la section ci-dessus, il existe des variables communes dans les jetons Lecture et Écriture .

Vous devez ensuite créer des variables dans Postman qui stockent les différents éléments des jetons SAS ci-dessus. Certaines valeurs sont identiques dans les deux URL :

- `AZURE_STORAGE_URL` : `https://vangeluw.blob.core.windows.net`
- `AZURE_STORAGE_CONTAINER` : `vangeluw`
- `AZURE_STORAGE_SAS_READ` : `?sv=2023-01-03&st=2025-01-13T07%3A36%3A35Z&se=2026-01-14T07%3A36%3A00Z&sr=c&sp=rl&sig=4r%2FcSJLlt%2BSt9HdFdN0VzWURxRK6UqhB8TEvbWkmAag%3D`
- `AZURE_STORAGE_SAS_WRITE` : `?sv=2023-01-03&st=2025-01-13T07%3A38%3A59Z&se=2026-01-14T07%3A38%3A00Z&sr=c&sp=acw&sig=lR9%2FMUfyYLcBK7W9Kv7YJdYz5HEEEovExAdOCOCUdMk%3D`

Pour les interactions d’API futures, la principale chose qui change est le nom de la ressource, tandis que les variables ci-dessus restent les mêmes. Dans ce cas, il est logique de créer des variables dans Postman afin de ne pas avoir à les spécifier manuellement à chaque fois.

1. Dans Postman, sélectionnez **Environnements**, ouvrez **Toutes les variables** et sélectionnez **Environnement**.

   ![ Stockage Azure ](./images/az104.png){zoomable="yes"}

1. Créez ces 4 variables dans le tableau qui s’affiche. Pour les colonnes **Valeur initiale** et **Valeur actuelle**, saisissez vos valeurs personnelles spécifiques.

   - `AZURE_STORAGE_URL` : votre url
   - `AZURE_STORAGE_CONTAINER` : nom de votre conteneur
   - `AZURE_STORAGE_SAS_READ` : votre jeton de lecture SAS
   - `AZURE_STORAGE_SAS_WRITE` : votre jeton d’écriture SAS

1. Sélectionnez **Enregistrer**.

   ![ Stockage Azure ](./images/az105.png){zoomable="yes"}

### Variables dans PostBuster

Comme vous pouvez le voir dans la section ci-dessus, il existe des variables communes dans les jetons Lecture et Écriture .

Vous devez ensuite créer des variables dans PostBuster qui stockent les différents éléments des jetons SAS ci-dessus. Certaines valeurs sont identiques dans les deux URL :

- `AZURE_STORAGE_URL` : `https://vangeluw.blob.core.windows.net`
- `AZURE_STORAGE_CONTAINER` : `vangeluw`
- `AZURE_STORAGE_SAS_READ` : `?sv=2023-01-03&st=2025-01-13T07%3A36%3A35Z&se=2026-01-14T07%3A36%3A00Z&sr=c&sp=rl&sig=4r%2FcSJLlt%2BSt9HdFdN0VzWURxRK6UqhB8TEvbWkmAag%3D`
- `AZURE_STORAGE_SAS_WRITE` : `?sv=2023-01-03&st=2025-01-13T07%3A38%3A59Z&se=2026-01-14T07%3A38%3A00Z&sr=c&sp=acw&sig=lR9%2FMUfyYLcBK7W9Kv7YJdYz5HEEEovExAdOCOCUdMk%3D`

Ouvrez PostBuster. Sélectionnez **Environnement de base** puis cliquez sur l’icône **Modifier** pour ouvrir l’environnement de base.

![ Stockage Azure ](./images/pbbe1.png)

Vous verrez alors 4 variables vides. Saisissez les détails de votre compte de stockage Azure ici.

![ Stockage Azure ](./images/pbbe2.png)

Votre fichier d’environnement de base doit maintenant se présenter comme suit : Cliquez sur **Fermer**.

![ Stockage Azure ](./images/pbbe3.png)

### Tester votre configuration

Dans l’un des exercices précédents, le **Corps** de votre requête **Firefly - T2I (styleref) V3** ressemblait à ceci :

    `« url »: « https://vangeluw.blob.core.windows.net/vangeluw/gradient.jpg?sv=2023-01-03&amp;st=2025-01-13T07%3A16%3A52Z&amp;se=2026-01-14T07%3A16%3A00Z&amp;sr=b&amp;sp=r&amp;sig=x4B1XZuAx%2F6yUfhb28hF0wppCOMeH7Ip2iBjNK5A%2BFw%3D« `
    
     ![Stockage Azure](./images/az24.png){zoomable="yes"}

1. Modifiez l’URL en :

   `"url": "{{AZURE_STORAGE_URL}}/{{AZURE_STORAGE_CONTAINER}}/gradient.jpg{{AZURE_STORAGE_SAS_READ}}"`

1. Sélectionnez **Envoyer** pour tester les modifications que vous avez apportées.

   ![ Stockage Azure ](./images/az106.png){zoomable="yes"}

   Si les variables ont été configurées correctement, une URL d’image est renvoyée.

   ![ Stockage Azure ](./images/az107.png){zoomable="yes"}

1. Ouvrez l’URL de l’image pour vérifier votre image.

   ![ Stockage Azure ](./images/az108.jpg)

## Étapes suivantes

Accédez à [ Utilisation des API Photoshop ](./ex3.md){target="_blank"}

Revenez à [ Présentation des services Adobe Firefly ](./firefly-services.md){target="_blank"}

Revenir à [Tous les modules](./../../../overview.md){target="_blank"}