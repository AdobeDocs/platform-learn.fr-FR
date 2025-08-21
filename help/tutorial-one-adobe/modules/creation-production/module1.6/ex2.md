---
title: GenStudio for Performance Marketing Créez votre compartiment Amazon AWS S3
description: GenStudio for Performance Marketing Créez votre compartiment Amazon AWS S3
role: Developer
level: Beginner
jira: KT-5342
doc-type: Tutorial
exl-id: 044677e4-7ca3-4dfe-9067-640983681ea7
source-git-commit: 1f9a868c5e4ef4aa0e09d7f5d73a951006ee6c5a
workflow-type: tm+mt
source-wordcount: '502'
ht-degree: 7%

---

# 1.6.2 Création de votre compartiment AWS S3

## 1.6.2.1 Créer votre compartiment S3

Accédez à [https://console.aws.amazon.com](https://console.aws.amazon.com) et connectez-vous.

>[!NOTE]
>
>Si vous ne disposez pas encore d’un compte AWS, créez un compte AWS à l’aide de votre adresse e-mail personnelle.

![ETL](./images/awshome.png)

Après vous être connecté, vous serez redirigé vers la **console de gestion AWS**.

![ETL](./images/awsconsole.png)

Dans la barre de recherche, recherchez **s3**. Cliquez sur le premier résultat de la recherche : **S3 - Scalable Storage in the Cloud**.

![ETL](./images/awsconsoles3.png)

Vous verrez alors la page d’accueil **Amazon S3**. Cliquez sur **Créer un compartiment**.

![ETL](./images/s3home.png)

Sur l’écran **Créer un compartiment**, utilisez le nom `--aepUserLdap---gspem-dam`.

![ETL](./images/bucketname.png)

Gardez tous les autres paramètres par défaut tels quels. Faites défiler vers le bas et cliquez sur **Créer un compartiment**.

![ETL](./images/createbucket.png)

Votre compartiment est alors en cours de création et est redirigé vers la page d’accueil S3 d’Amazon.

![ETL](./images/S3homeb.png)

## Définir les autorisations d’accès à votre compartiment S3

L’étape suivante consiste à configurer l’accès à votre compartiment S3.

Pour ce faire, accédez à [https://console.aws.amazon.com/iam/home](https://console.aws.amazon.com/iam/home).

L’accès aux ressources AWS est contrôlé par Amazon Identity and Access Management (IAM).

Cette page s’affiche maintenant.

![ETL](./images/iam.png)

Dans le menu de gauche, cliquez sur **Utilisateurs**. L’écran **Utilisateurs** s’affiche alors. Cliquez sur **Créer un utilisateur**.

![ETL](./images/iammenu.png)

Configurez ensuite votre utilisateur ou utilisatrice :

- Nom d’utilisateur : utilisez `s3_--aepUserLdap--_gspem_dam`

Cliquez sur **Suivant**.

![ETL](./images/configuser.png)

Cet écran d’autorisations s’affiche alors. Cliquez sur **Joindre directement des politiques**.

![ETL](./images/perm1.png)

Saisissez le terme de recherche **s3** pour afficher toutes les politiques S3 associées. Sélectionnez la politique **AmazonS3FullAccess**. Faites défiler vers le bas et cliquez sur **Suivant**.

![ETL](./images/perm2.png)

Vérifiez votre configuration. Cliquez sur **Créer un utilisateur**.

![ETL](./images/review.png)

Tu verras ça. Cliquez sur **Afficher utilisateur**.

![ETL](./images/review1.png)

Cliquez sur **Informations d’identification de sécurité** puis sur **Créer une clé d’accès**.

![ETL](./images/cred.png)

Sélectionnez **Application s’exécutant en dehors d’AWS**. Faites défiler vers le bas et cliquez sur **Suivant**.

![ETL](./images/creda.png)

Cliquez sur **Créer une clé d’accès**

![ETL](./images/credb.png)

Tu verras ça. Cliquez sur **Afficher** pour afficher votre clé d’accès secrète :

![ETL](./images/cred1.png)

Votre **clé d’accès secrète** s’affiche maintenant.

>[!IMPORTANT]
>
>Stockez vos informations d’identification dans un fichier texte sur votre ordinateur.
>
> - ID de clé d&#39;accès : ...
> - Clé d’accès secrète : ...
>
> Une fois que vous aurez cliqué sur **Terminé** vos informations d’identification ne s’afficheront plus.

Cliquez sur **Terminé**.

![ETL](./images/cred2.png)

Vous avez maintenant créé un compartiment AWS S3 et vous avez créé un utilisateur disposant des autorisations pour accéder à ce compartiment.

## 1.6.2.2 Charger Assets dans votre compartiment S3

Dans la barre de recherche, recherchez **s3**. Cliquez sur le premier résultat de la recherche : **S3 - Scalable Storage in the Cloud**.

![ETL](./images/bucket1.png)

Cliquez pour ouvrir le compartiment S3 que vous venez de créer et qui doit être nommé `--aepUserLdap---gspem-dam`.

![ETL](./images/bucket2.png)

Cliquez sur **Télécharger**.

![ETL](./images/bucket3.png)

Vous devriez alors voir ceci.

![ETL](./images/bucket4.png)

Vous pouvez télécharger les fichiers image CitiSignal [ici](./images/package.zip){target="_blank"}.

Exportez les fichiers sur votre bureau.

![ETL](./images/bucket5.png)

Cliquez sur **Ajouter un dossier**.

![ETL](./images/bucket6.png)

Sélectionnez le dossier **ressources** dans le dossier de téléchargement **package**. Cliquez sur **Télécharger**.

![ETL](./images/bucket7.png)

Vous devriez alors voir ceci. Cliquez de nouveau sur **Ajouter un dossier**.

![ETL](./images/bucket8.png)

Sélectionnez le dossier **miniatures** dans le dossier de téléchargement **package**. Cliquez sur **Télécharger**.

![ETL](./images/bucket9.png)

Vous devriez alors voir ceci. Cliquez sur **Télécharger**.

![ETL](./images/bucket10.png)

Votre chargement est maintenant terminé. Cliquez sur **Fermer**.

![ETL](./images/bucket11.png)

Vous devriez maintenant avoir cette structure de dossiers dans votre compartiment S3.

![ETL](./images/bucket12.png)

## Étapes suivantes

Accédez à [Créer votre application DAM externe](./ex3.md){target="_blank"}

Revenir à [GenStudio for Performance Marketing - Extensibilité](./genstudioext.md){target="_blank"}

Revenir à [Tous les modules](./../../../overview.md){target="_blank"}
