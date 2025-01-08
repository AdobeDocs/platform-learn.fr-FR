---
title: Prise en main des services Firefly
description: Prise en main des services Firefly
kt: 5342
doc-type: tutorial
exl-id: 5f9803a4-135c-4470-bfbb-a298ab1fee33
source-git-commit: ea06ca2d05195efa57643d45d7e50d3d914081d3
workflow-type: tm+mt
source-wordcount: '1017'
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

## 1.1.2.4 Chargement manuel du fichier et utilisation d’un fichier de gradient comme référence de style

Vous devez maintenant charger un fichier de dégradé de votre choix dans votre conteneur. Vous pouvez utiliser n’importe quel fichier de gradient de votre choix ou utiliser [ce fichier](./images/gradient.jpg) en le téléchargeant sur votre ordinateur.

![ Stockage Azure ](./images/gradient.jpg)

Déposez le fichier de gradient dans votre conteneur dans l’explorateur de stockage Azure.

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

Remplacez l’URL de l’espace réservé par l’URL prédéfinie de votre fichier gradient, que vous avez copiée à partir de l’explorateur de stockage Azure. Tu auras alors ceci. Cliquez sur **Envoyer**.

![ Stockage Azure ](./images/az24.png)

Vous obtiendrez ensuite une réponse des services de Firefly, avec une nouvelle image. Ouvrez le fichier image dans votre navigateur.

![ Stockage Azure ](./images/az25.png)

Vous verrez ensuite une autre image avec `horses in a field`, mais cette fois, le style sera similaire au fichier de dégradés que vous avez fourni comme référence de style.

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

Vous devez maintenant sélectionner un fichier sur votre ordinateur local. Vous pouvez utiliser un nouveau fichier image de votre choix ou un autre fichier de dégradés que vous pouvez trouver [ici](./images/gradient2-p.jpg).

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

BlockBlob de type x-ms-blob

![ Stockage Azure ](./images/az35.png)

Accédez à **Autorisation** et définissez le **Type d’authentification** sur **Aucune authentification**. Cliquez sur **Envoyer**.

![ Stockage Azure ](./images/az36.png)

Cette réponse vide s’affiche alors dans Postman, ce qui signifie que votre chargement de fichier s’est correctement déroulé.

![ Stockage Azure ](./images/az37.png)

Si vous revenez ensuite à l’Explorateur de stockage Azure et actualisez le contenu de votre dossier, le fichier nouvellement chargé s’y trouve désormais.

![ Stockage Azure ](./images/az38.png)

Étape Suivante : [1.1.3 ...](./ex3.md)

[Retour au module 1.1](./firefly-services.md)

[Revenir à tous les modules](./../../../overview.md)
