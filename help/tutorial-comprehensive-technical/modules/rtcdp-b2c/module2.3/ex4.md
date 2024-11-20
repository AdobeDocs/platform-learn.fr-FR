---
title: CDP en temps réel - Créer une audience et agir - Envoyer votre audience vers une destination S3
description: CDP en temps réel - Créer une audience et agir - Envoyer votre audience vers une destination S3
kt: 5342
doc-type: tutorial
exl-id: 656fc93c-74ff-4d8f-8674-6520d2a70b86
source-git-commit: acb941e4ee668248ae0767bb9f4f42e067c181ba
workflow-type: tm+mt
source-wordcount: '832'
ht-degree: 5%

---

# 2.3.4 Action à effectuer : envoyez votre audience vers une destination S3

Adobe Experience Platform peut également partager des audiences vers des destinations de marketing par e-mail telles que Salesforce Marketing Cloud, Oracle Eloqua, Oracle Responsys et Adobe Campaign.

Vous pouvez utiliser le protocole FTP ou SFTP dans le cadre des destinations dédiées pour chacune de ces destinations de marketing par e-mail ou vous pouvez utiliser AWS S3 pour exchange des listes de clients entre Adobe Experience Platform et ces destinations de marketing par e-mail.

Dans ce module, vous allez configurer une telle destination en utilisant un compartiment AWS S3.

## Création de votre compartiment S3

Accédez à [https://console.aws.amazon.com](https://console.aws.amazon.com) et connectez-vous.

>[!NOTE]
>
>Si vous ne disposez pas encore d’un compte AWS, créez un compte AWS à l’aide de votre adresse électronique personnelle.

![ETL](./images/awshome.png)

Une fois connecté, vous serez redirigé vers la **console de gestion AWS**.

![ETL](./images/awsconsole.png)

Dans la barre de recherche, recherchez **s3**. Cliquez sur le premier résultat de la recherche : **S3 - Stockage évolutif dans le cloud**.

![ETL](./images/awsconsoles3.png)

Vous verrez ensuite la page d’accueil **Amazon S3**. Cliquez sur **Créer un compartiment**.

![ETL](./images/s3home.png)

Dans l&#39;écran **Créer un compartiment**, utilisez le nom `aepmodulertcdp--aepUserLdap--`

![ETL](./images/bucketname.png)

Conservez tous les autres paramètres par défaut tels quels. Faites défiler l’écran vers le bas et cliquez sur **Créer un compartiment**.

![ETL](./images/createbucket.png)

Votre compartiment sera alors créé et redirigé vers la page d’accueil d’Amazon S3.

![ETL](./images/S3homeb.png)

## Définition des autorisations d’accès à votre compartiment S3

L’étape suivante consiste à configurer l’accès à votre compartiment S3.

Pour ce faire, accédez à [https://console.aws.amazon.com/iam/home](https://console.aws.amazon.com/iam/home).

L’accès aux ressources AWS est contrôlé par Amazon Identity and Access Management (IAM).

Vous allez maintenant voir cette page.

![ETL](./images/iam.png)

Dans le menu de gauche, cliquez sur **Utilisateurs**. L’écran **Utilisateurs** s’affiche alors. Cliquez sur **Créer un utilisateur**.

![ETL](./images/iammenu.png)

Configurez ensuite votre utilisateur :

- Nom d’utilisateur : utilisez `s3_--aepUserLdap--_rtcdp`

Cliquez sur **Suivant**.

![ETL](./images/configuser.png)

Cet écran des autorisations s’affiche alors. Cliquez sur **Joindre directement des stratégies**.

![ETL](./images/perm1.png)

Saisissez le terme de recherche **s3** pour afficher toutes les stratégies S3 associées. Sélectionnez la stratégie **AmazonS3FullAccess**. Faites défiler l’écran vers le bas et cliquez sur **Suivant**.

![ETL](./images/perm2.png)

Vérifiez votre configuration. Cliquez sur **Créer un utilisateur**.

![ETL](./images/review.png)

Vous verrez alors ceci. Cliquez sur **Afficher l’utilisateur**.

![ETL](./images/review1.png)

Cliquez sur **Informations d’identification de sécurité**, puis sur **Créer une clé d’accès**.

![ETL](./images/cred.png)

Sélectionnez **Application s’exécutant en dehors d’AWS**. Faites défiler l’écran vers le bas et cliquez sur **Suivant**.

![ETL](./images/creda.png)

Cliquez sur **Créer une clé d’accès**

![ETL](./images/credb.png)

Vous verrez alors ceci. Cliquez sur **Afficher** pour afficher votre clé d’accès secrète :

![ETL](./images/cred1.png)

Votre **clé d’accès secrète** s’affiche maintenant.

>[!IMPORTANT]
>
>Stockez vos informations d’identification dans un fichier texte sur votre ordinateur.
>
> - Accéder à l’ID de clé : ...
> - Clé d’accès secrète : ...
>
> Une fois que vous avez cliqué sur **Terminé**, vous ne verrez plus jamais vos informations d’identification !

Cliquez sur **Terminé**.

![ETL](./images/cred2.png)

Vous avez maintenant créé un compartiment AWS S3 et vous avez créé un utilisateur avec les autorisations d’accès à ce compartiment.

## Configuration de la destination dans Adobe Experience Platform

Accédez à [Adobe Experience Platform](https://experience.adobe.com/platform). Une fois connecté, vous accédez à la page d’accueil de Adobe Experience Platform.

![Ingestion des données](./../../../modules/datacollection/module1.2/images/home.png)

Avant de continuer, vous devez sélectionner un **sandbox**. L’environnement de test à sélectionner est nommé ``--aepSandboxName--``. Après avoir sélectionné l’[!UICONTROL sandbox] approprié, vous verrez le changement d’écran et vous êtes désormais dans votre [!UICONTROL sandbox] dédié.

![Ingestion des données](./../../../modules/datacollection/module1.2/images/sb1.png)

Dans le menu de gauche, accédez à **Destinations**, puis à **Catalogue**. Vous verrez ensuite le **catalogue des destinations**.

![RTCDP](./images/rtcdpmenudest1.png)

Cliquez sur **Cloud Storage**, puis sur le bouton **Configurer** (ou sur **Activer les audiences**, selon votre environnement) sur la carte **Amazon S3**.

![RTCDP](./images/rtcdp2.png)

Sélectionnez **Access Key** comme Type de compte. Utilisez les informations d’identification S3 qui vous ont été fournies à l’étape précédente :

| Identifiant de la clé d’accès | Clé d’accès secrète |
|:-----------------------:| :-----------------------:|
| AKIA..... | 7Icm..... |

Cliquez sur **Se connecter à la destination**.

![RTCDP](./images/rtcdpsfs3.png)

Vous verrez alors une confirmation visuelle que cette destination est maintenant connectée.

![RTCDP](./images/rtcdpsfs3connected.png)

Vous devez fournir des détails sur le compartiment S3 afin que Adobe Experience Platform puisse se connecter au compartiment S3.

Pour définir une convention d’affectation des noms, utilisez ce qui suit :

| Identifiant de la clé d’accès | Clé d’accès secrète |
|:-----------------------:| :-----------------------:|
| Nom | `AWS - S3 - --aepUserLdap--` |
| Description | `AWS - S3 - --aepUserLdap--` |
| Nom du compartiment | `aepmodulertcdp--aepUserLdap--` |
| Chemin du dossier | /now |

Sélectionnez **Audiences**.

Pour **Type de fichier**, sélectionnez **CSV** et laissez les paramètres par défaut inchangés.

![RTCDP](./images/rtcdpsfs3connect2.png)

Faites défiler vers le bas. Pour **Format de compression**, sélectionnez **Aucun**. Cliquez sur **Suivant**.

![RTCDP](./images/rtcdpsfs3connect3.png)

Vous pouvez désormais joindre une stratégie de gouvernance des données à votre nouvelle destination. Cliquez sur **Suivant**.

![RTCDP](./images/rtcdpsfs3connect2gov.png)

Dans la liste des audiences, recherchez l’audience que vous avez créée lors de l’exercice précédent, `--aepUserLdap-- - Interest in Galaxy S24`, puis sélectionnez-la. Cliquez sur **Suivant**.

![RTCDP](./images/s3a.png)

Vous verrez alors ceci. Si vous le souhaitez, vous pouvez modifier le planning et le nom du fichier en cliquant sur l’icône **crayon** . Cliquez sur **Suivant**.

![RTCDP](./images/s3bb.png)

Vous pouvez désormais sélectionner les attributs de profil pour l’exportation vers AWS S3. Cliquez sur **Ajouter un nouveau champ** et assurez-vous que le champ `--aepTenantId--.identification.core.ecid` est ajouté et marqué comme **Clé de déduplication**.

Vous pouvez éventuellement ajouter autant d’autres attributs de profil que nécessaire.

Une fois tous les champs ajoutés, cliquez sur **Suivant**.

![RTCDP](./images/s3c.png)

Vérifiez votre configuration. Cliquez sur **Terminer** pour terminer votre configuration.

![RTCDP](./images/s3g.png)

Vous serez alors de retour à l’écran Activation de la destination et votre audience sera ajoutée à cette destination.

Si vous souhaitez ajouter d’autres exportations d’audiences, vous pouvez cliquer sur **Activer les audiences** pour redémarrer le processus et ajouter d’autres audiences.

![RTCDP](./images/s3j.png)

Étape suivante : [2.3.5 Agir : envoyez votre audience à Adobe Target](./ex5.md)

[Revenir au module 2.3](./real-time-cdp-build-a-segment-take-action.md)

[Revenir à tous les modules](../../../overview.md)
