---
title: CDP en temps réel - Créer un segment et agir - Envoyer votre segment à une destination S3
description: CDP en temps réel - Créer un segment et agir - Envoyer votre segment à une destination S3
kt: 5342
audience: Data Architect, Orchestration Engineer, Marketer
doc-type: tutorial
activity: develop
exl-id: 5b0bcd69-7131-48a3-bd3e-773ba95cc42b
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '909'
ht-degree: 4%

---

# 6.4 Agir : envoyer votre segment à une destination S3 ;

Adobe Experience Platform peut également partager des audiences vers des destinations de marketing par e-mail telles que Salesforce Marketing Cloud, Oracle Eloqua, Oracle Responsys et Adobe Campaign.

Vous pouvez utiliser le protocole FTP ou SFTP dans le cadre des destinations dédiées pour chacune de ces destinations de marketing par e-mail, ou vous pouvez utiliser AWS S3 pour échanger des listes de clients entre Adobe Experience Platform et ces destinations de marketing par e-mail.

Dans ce module, vous allez configurer une telle destination en utilisant un compartiment AWS S3.

## 6.4.1 Création de votre compartiment S3

Accédez à [https://console.aws.amazon.com](https://console.aws.amazon.com) et connectez-vous avec le compte Amazon que vous avez créé précédemment.

![ETL](./images/awshome.png)

Une fois connecté, vous serez redirigé vers le **Console de gestion AWS**.

![ETL](./images/awsconsole.png)

Dans le **Recherche de services** menu, rechercher **s3**. Cliquez sur le premier résultat de la recherche : **S3 - Stockage évolutif dans le cloud**.

![ETL](./images/awsconsoles3.png)

Vous verrez alors le **Amazon S3** page d’accueil. Cliquez sur **Créer un compartiment**.

![ETL](./images/s3home.png)

Dans le **Créer un compartiment** vous devez configurer deux éléments :

- Nom : utiliser le nom `aepmodulertcdp--demoProfileLdap--`. Par exemple, dans cet exercice, le nom du compartiment est **aepmoduertcdpvangeluw**
- Région : utiliser la région ; **UE (Francfort) eu-central-1**

![ETL](./images/bucketname.png)

Conservez tous les autres paramètres par défaut tels quels. Faites défiler la page vers le bas et cliquez sur **Créer un compartiment**.

![ETL](./images/createbucket.png)

Vous verrez alors votre compartiment en cours de création et vous serez redirigé vers la page d’accueil d’Amazon S3.

![ETL](./images/S3homeb.png)

## 6.4.2 Définition des autorisations d’accès à votre compartiment S3

L’étape suivante consiste à configurer l’accès à votre compartiment S3.

Pour ce faire, accédez à [https://console.aws.amazon.com/iam/home](https://console.aws.amazon.com/iam/home).

L’accès aux ressources AWS est contrôlé par Amazon Identity and Access Management (IAM).

Vous allez maintenant voir cette page.

![ETL](./images/iam.png)

Dans le menu de gauche, cliquez sur **Utilisateurs**. Vous verrez alors le **Utilisateurs** écran. Cliquez sur **Ajout d’utilisateurs**.

![ETL](./images/iammenu.png)

Configurez ensuite votre utilisateur :

- Nom d’utilisateur : use `s3_--demoProfileLdap--_rtcdp` comme nom. Dans cet exemple, le nom est `s3_vangeluw_rtcdp`.
- Type d’accès AWS : select **Clé d’accès - Accès programmatique**.

Cliquez sur **Suivant : Autorisations**.

![ETL](./images/configuser.png)

Cet écran des autorisations s’affiche alors. Cliquez sur **Association directe des stratégies existantes**.

![ETL](./images/perm1.png)

Saisissez le terme à rechercher. **s3** pour afficher toutes les stratégies S3 connexes. Sélection de la stratégie **AmazonS3FullAccess**. Cliquez sur **Suivant : Balises**.

![ETL](./images/perm2.png)

Sur le **Balises** , il n’est pas nécessaire de configurer quoi que ce soit. Cliquez sur **Suivant : Réviser**.

![ETL](./images/perm3.png)

Vérifiez votre configuration. Cliquez sur **Créer un utilisateur**.

![ETL](./images/review.png)

Votre utilisateur est maintenant créé et vos informations d’identification s’affichent pour accéder à votre environnement S3. C&#39;est la seule fois où vous verrez vos informations d&#39;identification, veuillez les noter.

![ETL](./images/cred.png)

Cliquez sur **Afficher** pour afficher votre clé d’accès secrète :

![ETL](./images/cred1.png)

>[!IMPORTANT]
>
>Stockez vos informations d’identification dans un fichier texte sur votre ordinateur.
>
> - Identifiant de clé d’accès : ...
> - Clé d’accès secrète : ...
>
> Une fois que vous avez cliqué sur **Fermer** vous ne verrez plus jamais vos identifiants !

Cliquez sur **Fermer**.

![ETL](./images/close.png)

Vous avez maintenant créé un compartiment AWS S3 et vous avez créé un utilisateur avec les autorisations d’accès à ce compartiment.

## 6.4.3 Configuration de la destination dans Adobe Experience Platform

Accédez à [Adobe Experience Platform](https://experience.adobe.com/platform). Une fois connecté, vous accédez à la page d’accueil de Adobe Experience Platform.

![Ingestion des données](../module2/images/home.png)

Avant de continuer, vous devez sélectionner une **sandbox**. L’environnement de test à sélectionner est nommé ``--aepSandboxId--``. Pour ce faire, cliquez sur le texte **[!UICONTROL Production Prod]** dans la ligne bleue en haut de votre écran. Après avoir sélectionné le [!UICONTROL sandbox], vous verrez le changement d’écran et vous êtes maintenant dans votre [!UICONTROL sandbox].

![Ingestion des données](../module2/images/sb1.png)

Dans le menu de gauche, accédez à **Destinations**, puis accédez à **Catalogue**. Vous verrez alors le **Catalogue des destinations**.

![RTCDP](./images/rtcdpmenudest.png)

Cliquez sur **Stockage dans le cloud**, puis cliquez sur le bouton **Configuration** (ou activé) **Activation des segments**, selon votre environnement) sur la variable **Amazon S3** carte.

![RTCDP](./images/rtcdp2.png)

Selon votre environnement, vous devrez peut-être cliquer sur **+ Configurer une nouvelle destination** pour commencer à créer votre destination.

![RTCDP](./images/rtcdp2a.png)

Sélectionner **Nouveau compte** comme Type de compte. Utilisez les informations d’identification S3 qui vous ont été fournies à l’étape précédente :

| Accès ID de clé | Clé d’accès secrète |
|:-----------------------:| :-----------------------:|
| L&#39;AKIA.... | Cm5Ln.... |

Cliquez sur **Se connecter à la destination**.

![RTCDP](./images/rtcdpsfs3.png)

Vous verrez alors une confirmation visuelle que cette destination est maintenant connectée.

![RTCDP](./images/rtcdpsfs3connected.png)

Vous devez fournir un nom et un dossier pour que Adobe Experience Platform puisse se connecter au compartiment S3.

Pour définir une convention d’affectation des noms, utilisez les éléments suivants :

| Accès ID de clé | Clé d’accès secrète |
|:-----------------------:| :-----------------------:|
| Nom | `AWS - S3 - --demoProfileLdap--` |
| Description | `AWS - S3 - --demoProfileLdap--` |
| Nom du compartiment | `aepmodulertcdp--demoProfileLdap--` |
| Chemin du dossier | / |

Cliquez sur **Suivant**.

![RTCDP](./images/rtcdpsfs3connect2.png)

Vous pouvez désormais joindre une stratégie de gouvernance des données à votre nouvelle destination. Cliquez sur **Suivant**.

![RTCDP](./images/rtcdpsfs3connect2gov.png)

Dans la liste des segments, recherchez le segment que vous avez créé dans l’exercice 1 et sélectionnez-le. Cliquez sur **Suivant**.

![RTCDP](./images/s3a.png)

Vous verrez alors ceci. Si vous le souhaitez, vous pouvez modifier le planning en cliquant sur le bouton **crayon** icône . **Créer une planification**.

![RTCDP](./images/s3bb.png)

Définissez votre planning de choix. Sélectionner **Exportation de fichiers incrémentiels** et définissez la fréquence sur **Horaire** each **3 heures**. Cliquez sur **Créer**.

![RTCDP](./images/s3bbc.png)

Vous aurez alors ceci. Cliquez sur **Suivant**.

![RTCDP](./images/s3bbca.png)

Vous pouvez désormais sélectionner des attributs pour l’exportation vers AWS S3. Cliquez sur **Ajouter un nouveau champ** et assurez-vous que le champ `--aepTenantId--.identification.core.ecid` est ajouté et marqué comme **Clé de déduplication**.

Vous pouvez éventuellement ajouter autant de champs que nécessaire.

Une fois tous les champs ajoutés, cliquez sur **Suivant**.

![RTCDP](./images/s3c.png)

Vérifiez votre configuration. Cliquez sur **Terminer** pour terminer votre configuration.

![RTCDP](./images/s3g.png)

Vous serez alors de retour à l’écran Activation de la destination et votre segment sera ajouté à cette destination.

![RTCDP](./images/s3j.png)

Si vous souhaitez ajouter d’autres exportations de segments, vous pouvez cliquer sur **Activation des segments** pour redémarrer le processus et ajouter d’autres segments.

![RTCDP](./images/s3k.png)

Étape suivante : [6.5 Agir : envoyer votre segment à Adobe Target ;](./ex5.md)

[Revenir au module 6](./real-time-cdp-build-a-segment-take-action.md)

[Revenir à tous les modules](../../overview.md)
