---
title: Collecte de données - AEC - Création de schémas, de modèles de données et de liens
description: Foundation - AEC - Création de schémas, de modèles de données et de liens
kt: 5342
doc-type: tutorial
exl-id: e863ab3a-44df-4bb4-b081-a62616aaa1f1
source-git-commit: e32d415d2997b43834e9fc2495c4394b13f4d49f
workflow-type: tm+mt
source-wordcount: '639'
ht-degree: 5%

---

# 1.3.2 Création de schémas, de modèles de données et de liens

Vous pouvez désormais configurer votre base de données fédérée dans Adobe Experience Platform.

Connectez-vous à Adobe Experience Platform en accédant à cette URL : [https://experience.adobe.com/platform](https://experience.adobe.com/platform).

Une fois connecté, vous accédez à la page d’accueil de Adobe Experience Platform.

![Ingestion des données](./../module1.2/images/home.png)

Avant de continuer, vous devez sélectionner un **sandbox**. Le sandbox à sélectionner est nommé ``--aepSandboxName--``. Après avoir sélectionné la sandbox appropriée, la modification d’écran s’affiche et vous êtes maintenant dans votre sandbox dédiée.

![Ingestion des données](./../module1.2/images/sb1.png)

## 1.3.2.1 Configurer une base de données fédérée dans AEP

Cliquez sur **Bases de données fédérées** dans le menu de gauche. Cliquez ensuite sur **Ajouter une base de données fédérée**.

![AAAA](./images/fdb1.png)

Comme **Libellé**, utilisez `--aepUserLdap-- - CitiSignal Snowflake` et pour le type, choisissez **Snowflake**.

Sous détails, vous devez remplir vos informations d’identification, qui ressembleront à ceci :

![AAAA](./images/fdb2.png)

**Serveur** :

Dans Snowflake, accédez à **Admin > Comptes**. Cliquez sur le bouton 3 **...** en regard de votre compte, puis sur **Gérer les URL**.

![AAAA](./images/fdburl1.png)

Tu verras ça. Copiez l’**URL actuelle** et collez-la dans le champ **Serveur** d’AEP.

![AAAA](./images/fdburl2.png)

**Utilisateur** : nom d’utilisateur que vous avez créé précédemment, dans l’exercice 1.3.1.1
**Mot de passe** : mot de passe que vous avez créé précédemment, dans l’exercice 1.3.1.1
**Base de données** : utilisez **CITISIGNAL**

Donc, finalement, vous devriez avoir ceci. Cliquez sur **Tester la connexion**. Si le test réussit, cliquez sur **Déployer les fonctions**, ce qui créera des fonctions côté Snowflake qui sont nécessaires au moteur de workflow.

Une fois la connexion testée avec succès et les fonctions déployées, votre configuration sera stockée.

![AAAA](./images/fdb3.png)

Lorsque vous revenez ensuite au menu **Bases de données fédérées**, votre connexion s’affiche.

![AAAA](./images/fdb4.png)

## 1.3.2.2 Créer des schémas dans AEP

Dans le menu de gauche, cliquez sur **Modèles** puis accédez à **Schémas**. Cliquez sur **Créer un schéma**.

![AAAA](./images/fdb5.png)

Sélectionnez votre base de données fédérée et cliquez sur **+ Ajouter des tables**.

![AAAA](./images/fdb6.png)

Tu verras ça. Sélectionnez les 5 tables que vous avez créées précédemment dans Snowflake :

- `--aepUserLdap--_HOUSEHOLDS`
- `--aepUserLdap--_MOBILE_DATA_USAGE`
- `--aepUserLdap--_MONTHLY_DATA_USAGE`
- `--aepUserLdap--_PERSONS`
- `--aepUserLdap--_USERS`

Cliquez sur **Ajouter**.

![AAAA](./images/fdb7.png)

AEP charge alors les informations de chaque tableau et les affiche dans l’interface utilisateur.

Pour chaque tableau, vous pouvez effectuer les actions suivantes :

- Modifier le libellé du schéma
- Ajouter une description
- Renommer tous les champs et décider de leur visibilité
- sélection de la clé primaire du schéma

Pour cet exercice, aucune modification n’est nécessaire.

Cliquez sur **Créer**.

![AAAA](./images/fdb8.png)

Tu verras ça. Vous pouvez cliquer sur n’importe quel schéma et consulter les informations. Par exemple, cliquez sur **—aepUserLdap—_PERSON**.

![AAAA](./images/fdb9.png)

Vous verrez alors ceci, avec la possibilité de modifier la configuration. Cliquez sur **Données** pour afficher un exemple des données contenues dans la base de données Snowflake.

![AAAA](./images/fdb10.png)

Vous verrez ensuite un échantillon des données.

![AAAA](./images/fdb11.png)

## 1.3.2.3 Créer un modèle dans AEP

Dans le menu de gauche, accédez à **Modèles** puis à **Modèle de données**. Cliquez sur **Créer un modèle de données**.

![AAAA](./images/fdb12.png)

Pour l’étiquette, utilisez `--aepUserLdap-- - CitiSignal Snowflake Data Model`. Cliquez sur **Créer**.

![AAAA](./images/fdb13.png)

Cliquez sur **Ajouter des schémas**.

![AAAA](./images/fdb14.png)

Sélectionnez vos schémas et cliquez sur **Ajouter**.

![AAAA](./images/fdb15.png)

Tu verras ça. Cliquez sur **Enregistrer**.

![AAAA](./images/fdb16.png)

### `--aepUserLdap--_PERSONS` - `--aepUserLdap--_USERS`

Vous pouvez maintenant commencer à définir des liens entre les schémas. Pour commencer à définir un lien, vous devez cliquer sur **Créer des liens**.

![AAAA](./images/fdb16.png)

Tout d’abord, définissons le lien entre le `--aepUserLdap--_USERS` de la table et `--aepUserLdap--_PERSONS`.

Cliquez sur **Ajouter**.

![AAAA](./images/fdb18.png)

### `--aepUserLdap--_HOUSEHOLDS` - `--aepUserLdap--_PERSONS`

Tu seras de retour ici. Cliquez sur **Créer des liens** pour créer un autre lien.

![AAAA](./images/fdb17.png)

Définissons ensuite le lien entre le `--aepUserLdap--_HOUSEHOLDS` de la table et `--aepUserLdap--_PERSONS`.

![AAAA](./images/fdb19.png)

### `--aepUserLdap--_USERS` - `--aepUserLdap--_MONTHLY_DATA_USAGE`

Tu seras de retour ici. Cliquez sur **Créer des liens** pour créer un autre lien.

![AAAA](./images/fdb20.png)

Définissons ensuite le lien entre le `--aepUserLdap--_USERS` de la table et `--aepUserLdap--_MONTHLY_DATA_USAGE`.

![AAAA](./images/fdb21.png)


### `--aepUserLdap--_USERS` - `--aepUserLdap--_HOUSEHOLDS`

Tu seras de retour ici. Cliquez sur **Créer des liens** pour créer un autre lien.

![AAAA](./images/fdb22.png)

Définissons ensuite le lien entre le `--aepUserLdap--_USERS` de la table et `--aepUserLdap--_HOUSEHOLDS`.

![AAAA](./images/fdb23.png)

### `--aepUserLdap--_USERS` - `--aepUserLdap--_MOBILE_DATA_USAGE`

Tu seras de retour ici. Cliquez sur **Créer des liens** pour créer un autre lien.

![AAAA](./images/fdb24.png)

Définissons ensuite le lien entre le `--aepUserLdap--_USERS` de la table et `--aepUserLdap--_MOBILE_DATA_USAGE`.

![AAAA](./images/fdb25.png)

Vous devriez alors voir ceci. Cliquez sur **Enregistrer**.

![AAAA](./images/fdb26.png)

Votre configuration dans AEP est maintenant terminée. Vous pouvez maintenant commencer à utiliser vos données fédérées dans une composition d’audience fédérée.

Étape suivante : [1.3.3 Créer une composition fédérée](./ex3.md)

[Retour au module 1.3](./fac.md)

[Revenir à tous les modules](../../../overview.md)
