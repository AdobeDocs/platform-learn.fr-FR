---
title: Configurer votre base de données relationnelle
description: Configurer votre base de données relationnelle
kt: 5342
doc-type: tutorial
exl-id: 532e5f2c-971f-488f-bef4-3a8141408cc8
source-git-commit: defdae3329e1409159f59c4a0ef2aa21c7e3949b
workflow-type: tm+mt
source-wordcount: '2159'
ht-degree: 8%

---

# 3.8.1 Configurer votre base de données relationnelle

Connectez-vous à Adobe Journey Optimizer en allant sur [https://experience.adobe.com](https://experience.adobe.com?lang=fr). Cliquez sur **Journey Optimizer**.

![AJO OC](./images/aechome.png)

Vous serez redirigé vers la vue **Accueil** dans Journey Optimizer. Tout d’abord, assurez-vous d’utiliser le bon sandbox. Le sandbox à utiliser est appelé `--aepSandboxName--`.

![AJO OC](./images/ajohome.png)

## Configuration 3.8.1.1 schéma basé sur relationnel

Un schéma relationnel est la définition formelle du modèle de données basé sur un modèle.

Il précise :

- L’ensemble de tables
- Les colonnes de chaque table
- Les contraintes
- Les relations entre les tables

L’organisation des schémas ou des tables dans un modèle de données basé sur un modèle consiste à structurer vos données en plusieurs tables. Assurez-vous que chaque table stocke un type d’entité/de schéma.

Lors de l’ingestion de données dans en vue de les utiliser avec des campagnes orchestrées par Adobe Journey Optimizer, les sources suivantes sont disponibles :

- Amazon S3
- Google Cloud Storage
- SFTP
- Snowflake
- Google BigQuery
- Data Landing Zone
- Azure Databricks
- Chargement de fichiers locaux

La première étape de cet exercice consiste à configurer vos schémas XDM basés sur des relations. Dans le menu de gauche, faites défiler l’écran jusqu’à **Gestion des données** et sélectionnez **Schémas**. Cliquez sur **+ Créer un schéma**.

![AJO OC](./images/ajoocdata1.png)

Sélectionnez **Relationnel**.

![AJO OC](./images/ajoocdata2.png)

Sélectionnez **Charger le fichier DDL** puis cliquez sur **Choisir les fichiers**.

![AJO OC](./images/ajoocdata3.png)

Téléchargez le fichier [citisignal_ddl_tables_only.sql](./assets/citisignal_ddl_tables_only.sql) sur votre bureau.

![AJO OC](./images/ajoocdata4.png)

Sélectionnez le **`citisignal_ddl_tables_only.sql`** de fichier et cliquez sur **ouvrir**.

![AJO OC](./images/ajoocdata5.png)

Vous devriez alors voir ceci. Cliquez sur **Suivant**.

![AJO OC](./images/ajoocdata6.png)

### Identité

Certains de vos schémas contiennent des identifiants personnels et ces champs doivent être marqués comme **Identité**. Vous devez également sélectionner l’**Espace de noms** applicable à ce type d’identité spécifique.

**`citisignal_accounts`**

Pour ce schéma, accédez au champ **account_id** et définissez le type **Identité** sur **Système de démonstration - CRMID**.

![AJO OC](./images/ajoocdata7.png)

**`citisignal_recipients`**

Pour ce schéma, accédez au champ **account_id** et définissez le type **Identité** sur **Système de démonstration - CRMID**, accédez au champ **e-mail** et définissez le type **Identité** sur **E-mail**.

![AJO OC](./images/ajoocdata8.png)

### Contrôle de version

Pour suivre les mises à jour des données qui seront ingérées par rapport à ces schémas, il est nécessaire de définir un champ qui sera utilisé pour suivre la version des données chargées. Le champ utilisé à cet effet dans tous ces schémas est le champ **lastmodified**, qui contient la date et l’heure des données chargées.

Vous devez maintenant cocher la case **Contrôle de version** pour le champ **dernière modification** dans chacun de ces schémas.

**`citisignal_products`**

Cochez la case **Contrôle de version** pour le champ **dernière modification**.

![AJO OC](./images/ajoocdata9.png)

**`citisignal_product_bundles`**

Cochez la case **Contrôle de version** pour le champ **dernière modification**.

![AJO OC](./images/ajoocdata10.png)

**`citisignal_product_relationships`**

Cochez la case **Contrôle de version** pour le champ **dernière modification**.

![AJO OC](./images/ajoocdata11.png)

**`citisignal_accounts`**

Cochez la case **Contrôle de version** pour le champ **dernière modification**.

![AJO OC](./images/ajoocdata12.png)

**`citisignal_recipients`**

Cochez la case **Contrôle de version** pour le champ **dernière modification**.

![AJO OC](./images/ajoocdata13.png)

**`citisignal_mobile_subscriptions`**

Cochez la case **Contrôle de version** pour le champ **dernière modification**.

![AJO OC](./images/ajoocdata14.png)

**`citisignal_internet_subscriptions`**

Cochez la case **Contrôle de version** pour le champ **dernière modification**.

![AJO OC](./images/ajoocdata15.png)

**`citisignal_tv_subscriptions`**

Cochez la case **Contrôle de version** pour le champ **dernière modification**.

![AJO OC](./images/ajoocdata16.png)

**`citisignal_equipment_subscriptions`**

Cochez la case **Contrôle de version** pour le champ **dernière modification**.

![AJO OC](./images/ajoocdata17.png)

**`citisignal_mobile_usage_summary`**

Cochez la case **Contrôle de version** pour le champ **dernière modification**.

![AJO OC](./images/ajoocdata18.png)

**`citisignal_internet_usage_summary`**

Cochez la case **Contrôle de version** pour le champ **dernière modification**.

![AJO OC](./images/ajoocdata19.png)

**`citisignal_offers`**

Cochez la case **Contrôle de version** pour le champ **dernière modification**.

![AJO OC](./images/ajoocdata20.png)

**`citisignal_offer_eligibility`**

Cochez la case **Contrôle de version** pour le champ **dernière modification**.

![AJO OC](./images/ajoocdata21.png)

### Nom du schéma

Lors de l’ingestion de ces schémas à des fins d’activation dans un sandbox partagé, il est nécessaire de modifier le nom de chaque schéma afin qu’il soit unique dans ce sandbox spécifique. La raison de cette modification est d’éviter les conflits de dénomination de schéma.

Pour cet atelier, vous devez ajouter votre LDAP devant chaque nom de schéma, ce qui signifie que chaque nom de schéma doit comporter le préfixe suivant : `--aepUserLdap--_`

**`citisignal_products`**

Remplacez le nom de votre schéma par `--aepUserLdap--_ citisignal_products`.

![AJO OC](./images/ajoocdatan9.png)

**`citisignal_product_bundles`**

Remplacez le nom de votre schéma par `--aepUserLdap--_ citisignal_product_bundles`.

![AJO OC](./images/ajoocdatan10.png)

**`citisignal_product_relationships`**

Remplacez le nom de votre schéma par `--aepUserLdap--_ citisignal_product_relationships`.

![AJO OC](./images/ajoocdatan11.png)

**`citisignal_accounts`**

Remplacez le nom de votre schéma par `--aepUserLdap--_ citisignal_accounts`.

![AJO OC](./images/ajoocdatan12.png)

**`citisignal_recipients`**

Remplacez le nom de votre schéma par `--aepUserLdap--_ citisignal_recipients`.

![AJO OC](./images/ajoocdatan13.png)

**`citisignal_mobile_subscriptions`**

Remplacez le nom de votre schéma par `--aepUserLdap--_ citisignal_mobile_subscriptions`.

![AJO OC](./images/ajoocdatan14.png)

**`citisignal_internet_subscriptions`**

Remplacez le nom de votre schéma par `--aepUserLdap--_ citisignal_internet_subscriptions`.

![AJO OC](./images/ajoocdatan15.png)

**`citisignal_tv_subscriptions`**

Remplacez le nom de votre schéma par `--aepUserLdap--_ citisignal_internet_subscriptions`.

![AJO OC](./images/ajoocdatan16.png)

**`citisignal_equipment_subscriptions`**

Remplacez le nom de votre schéma par `--aepUserLdap--_ citisignal_equipment_subscriptions`.

![AJO OC](./images/ajoocdatan17.png)

**`citisignal_mobile_usage_summary`**

Remplacez le nom de votre schéma par `--aepUserLdap--_ citisignal_mobile_usage_summary`.

![AJO OC](./images/ajoocdatan18.png)

**`citisignal_internet_usage_summary`**

Remplacez le nom de votre schéma par `--aepUserLdap--_ citisignal_internet_usage_summary`.

![AJO OC](./images/ajoocdatan19.png)

**`citisignal_offers`**

Remplacez le nom de votre schéma par `--aepUserLdap--_ citisignal_offers`.

![AJO OC](./images/ajoocdatan20.png)

**`citisignal_offer_eligibility`**

Remplacez le nom de votre schéma par `--aepUserLdap--_ citisignal_offer_eligibility`.

![AJO OC](./images/ajoocdatan21.png)

Vos schémas sont maintenant prêts à être enregistrés. Cliquez sur **Terminé**.

![AJO OC](./images/ajoocdata22.png)

Vous devriez alors voir ceci. Cliquez sur **Enregistrer**.

![AJO OC](./images/ajoocdata23.png)

Cliquez sur **Ouvrir les tâches**.

![AJO OC](./images/ajoocdata24.png)

Vous devriez alors voir ceci. Vous devez attendre que le traitement soit terminé avant de passer à l’étape suivante.

![AJO OC](./images/ajoocdata25.png)

Une fois la tâche terminée avec succès, vous pouvez passer à l’étape suivante. Cela peut prendre 5 à 10 minutes.

![AJO OC](./images/ajoocdata26.png)

Maintenant que vos schémas XDM relationnels sont configurés et que les données sont ingérées, vous pouvez commencer à utiliser ces données pour créer votre campagne orchestrée dans l’exercice suivant.

## Ingestion des données 3.8.1.2

Accédez à **Jeux de données**. Vous devriez alors voir un jeu de données qui a été créé pour chaque schéma que vous avez créé.

![AJO OC](./images/ajoocdata27.png)

Téléchargez le fichier [data.zip](./assets/data.zip) sur votre bureau et décompressez-le.

![AJO OC](./images/ajoocdata28.png)

Ouvrez le dossier **data**. Vous devriez voir un fichier CSV pour chacun des schémas qui ont été créés. Vous devez maintenant charger ces données dans chaque jeu de données correspondant. Pour cet atelier, vous effectuerez un chargement de fichier local dans chaque jeu de données.

![AJO OC](./images/ajoocdata29.png)

**`vangeluw_citisignal_products`**

Accédez à **Sources**, recherchez `local` puis cliquez sur **Ajouter des données** sous **Chargement de fichier local**.

![AJO OC](./images/ajoocdatas10.png)

Activez le bouton (bascule) **Activer la capture de données de modification**.

Sélectionnez l’`vangeluw_citisignal_products` du jeu de données.

Cliquez sur **Suivant**.

![AJO OC](./images/ajoocdatas9a.png)

Cliquez sur **Choisir les fichiers**. Sélectionnez le **`citisignal_products.csv`** de fichier et cliquez sur **ouvrir**.

![AJO OC](./images/ajoocdatas9b.png)

Cliquez sur **Suivant**.

![AJO OC](./images/ajoocdatas9c.png)

Cliquez sur **Terminer**.

![AJO OC](./images/ajoocdatas9d.png)

Au bout de quelques minutes, vous pouvez voir les données ingérées dans votre jeu de données.

![AJO OC](./images/ajoocdatas9e.png)

**`vangeluw_citisignal_product_bundles`**

Accédez à **Sources**, recherchez `local` puis cliquez sur **Ajouter des données** sous **Chargement de fichier local**.

![AJO OC](./images/ajoocdatas10.png)

Activez le bouton (bascule) **Activer la capture de données de modification**.

Sélectionnez l’`vangeluw_citisignal_product_bundles` du jeu de données.

Cliquez sur **Suivant**.

![AJO OC](./images/ajoocdatas10a.png)

Cliquez sur **Choisir les fichiers**. Sélectionnez le **`citisignal_product_bundles.csv`** de fichier et cliquez sur **ouvrir**.

![AJO OC](./images/ajoocdatas10b.png)

Cliquez sur **Suivant**.

![AJO OC](./images/ajoocdatas10c.png)

Cliquez sur **Terminer**.

![AJO OC](./images/ajoocdatas10d.png)

Au bout de quelques minutes, vous pouvez voir les données ingérées dans votre jeu de données.

![AJO OC](./images/ajoocdatas10e.png)

**`vangeluw_citisignal_product_relationships`**

Accédez à **Sources**, recherchez `local` puis cliquez sur **Ajouter des données** sous **Chargement de fichier local**.

![AJO OC](./images/ajoocdatas10.png)

Activez le bouton (bascule) **Activer la capture de données de modification**.

Sélectionnez l’`vangeluw_citisignal_product_relationships` du jeu de données.

Cliquez sur **Suivant**.

![AJO OC](./images/ajoocdatas11a.png)

Cliquez sur **Choisir les fichiers**. Sélectionnez le **`citisignal_product_relationships.csv`** de fichier et cliquez sur **ouvrir**.

![AJO OC](./images/ajoocdatas11b.png)

Cliquez sur **Suivant**.

![AJO OC](./images/ajoocdatas11c.png)

Cliquez sur **Terminer**.

![AJO OC](./images/ajoocdatas11d.png)

Au bout de quelques minutes, vous pouvez voir les données ingérées dans votre jeu de données.

![AJO OC](./images/ajoocdatas11e.png)

**`vangeluw_citisignal_accounts`**

Accédez à **Sources**, recherchez `local` puis cliquez sur **Ajouter des données** sous **Chargement de fichier local**.

![AJO OC](./images/ajoocdatas10.png)

Activez le bouton (bascule) **Activer la capture de données de modification**.

Sélectionnez l’`vangeluw_citisignal_accounts` du jeu de données.

Cliquez sur **Suivant**.

![AJO OC](./images/ajoocdatas12a.png)

Cliquez sur **Choisir les fichiers**. Sélectionnez le **`citisignal_accounts.csv`** de fichier et cliquez sur **ouvrir**.

![AJO OC](./images/ajoocdatas12b.png)

Cliquez sur **Suivant**.

![AJO OC](./images/ajoocdatas12c.png)

Cliquez sur **Terminer**.

![AJO OC](./images/ajoocdatas12d.png)

Au bout de quelques minutes, vous pouvez voir les données ingérées dans votre jeu de données.

![AJO OC](./images/ajoocdatas12e.png)

**`vangeluw_citisignal_recipients`**

Accédez à **Sources**, recherchez `local` puis cliquez sur **Ajouter des données** sous **Chargement de fichier local**.

![AJO OC](./images/ajoocdatas10.png)

Activez le bouton (bascule) **Activer la capture de données de modification**.

Sélectionnez l’`vangeluw_citisignal_recipients` du jeu de données.

Cliquez sur **Suivant**.

![AJO OC](./images/ajoocdatas13a.png)

Cliquez sur **Choisir les fichiers**. Sélectionnez le **`citisignal_recipients.csv`** de fichier et cliquez sur **ouvrir**.

![AJO OC](./images/ajoocdatas13b.png)

Cliquez sur **Suivant**.

![AJO OC](./images/ajoocdatas13c.png)

Cliquez sur **Terminer**.

![AJO OC](./images/ajoocdatas13d.png)

Au bout de quelques minutes, vous pouvez voir les données ingérées dans votre jeu de données.

![AJO OC](./images/ajoocdatas13e.png)

**`vangeluw_citisignal_mobile_subscriptions`**

Accédez à **Sources**, recherchez `local` puis cliquez sur **Ajouter des données** sous **Chargement de fichier local**.

![AJO OC](./images/ajoocdatas10.png)

Activez le bouton (bascule) **Activer la capture de données de modification**.

Sélectionnez l’`vangeluw_citisignal_mobile_subscriptions` du jeu de données.

Cliquez sur **Suivant**.

![AJO OC](./images/ajoocdatas14a.png)

Cliquez sur **Choisir les fichiers**. Sélectionnez le **`citisignal_mobile_subscriptions.csv`** de fichier et cliquez sur **ouvrir**.

![AJO OC](./images/ajoocdatas14b.png)

Cliquez sur **Suivant**.

![AJO OC](./images/ajoocdatas14c.png)

Cliquez sur **Terminer**.

![AJO OC](./images/ajoocdatas14d.png)

Au bout de quelques minutes, vous pouvez voir les données ingérées dans votre jeu de données.

![AJO OC](./images/ajoocdatas14e.png)

**`vangeluw_citisignal_internet_subscriptions`**

Accédez à **Sources**, recherchez `local` puis cliquez sur **Ajouter des données** sous **Chargement de fichier local**.

![AJO OC](./images/ajoocdatas10.png)

Activez le bouton (bascule) **Activer la capture de données de modification**.

Sélectionnez l’`vangeluw_citisignal_internet_subscriptions` du jeu de données.

Cliquez sur **Suivant**.

![AJO OC](./images/ajoocdatas15a.png)

Cliquez sur **Choisir les fichiers**. Sélectionnez le **`citisignal_internet_subscriptions.csv`** de fichier et cliquez sur **ouvrir**.

![AJO OC](./images/ajoocdatas15b.png)

Cliquez sur **Suivant**.

![AJO OC](./images/ajoocdatas15c.png)

Cliquez sur **Terminer**.

![AJO OC](./images/ajoocdatas15d.png)

Au bout de quelques minutes, vous pouvez voir les données ingérées dans votre jeu de données.

![AJO OC](./images/ajoocdatas15e.png)

**`vangeluw_citisignal_tv_subscriptions`**

Accédez à **Sources**, recherchez `local` puis cliquez sur **Ajouter des données** sous **Chargement de fichier local**.

![AJO OC](./images/ajoocdatas10.png)

Activez le bouton (bascule) **Activer la capture de données de modification**.

Sélectionnez l’`vangeluw_citisignal_tv_subscriptions` du jeu de données.

Cliquez sur **Suivant**.

![AJO OC](./images/ajoocdatas16a.png)

Cliquez sur **Choisir les fichiers**. Sélectionnez le **`citisignal_tv_subscriptions.csv`** de fichier et cliquez sur **ouvrir**.

![AJO OC](./images/ajoocdatas16b.png)

Cliquez sur **Suivant**.

![AJO OC](./images/ajoocdatas16c.png)

Cliquez sur **Terminer**.

![AJO OC](./images/ajoocdatas16d.png)

Au bout de quelques minutes, vous pouvez voir les données ingérées dans votre jeu de données.

![AJO OC](./images/ajoocdatas16e.png)

**`vangeluw_citisignal_equipment_subscriptions`**

Accédez à **Sources**, recherchez `local` puis cliquez sur **Ajouter des données** sous **Chargement de fichier local**.

![AJO OC](./images/ajoocdatas10.png)

Activez le bouton (bascule) **Activer la capture de données de modification**.

Sélectionnez l’`vangeluw_citisignal_equipment_subscriptions` du jeu de données.

Cliquez sur **Suivant**.

![AJO OC](./images/ajoocdatas17a.png)

Cliquez sur **Choisir les fichiers**. Sélectionnez le **`citisignal_equipment_subscriptions.csv`** de fichier et cliquez sur **ouvrir**.

![AJO OC](./images/ajoocdatas17b.png)

Cliquez sur **Suivant**.

![AJO OC](./images/ajoocdatas17c.png)

Cliquez sur **Terminer**.

![AJO OC](./images/ajoocdatas17d.png)

Au bout de quelques minutes, vous pouvez voir les données ingérées dans votre jeu de données.

![AJO OC](./images/ajoocdatas17e.png)

**`vangeluw_citisignal_mobile_usage_summary`**

Accédez à **Sources**, recherchez `local` puis cliquez sur **Ajouter des données** sous **Chargement de fichier local**.

![AJO OC](./images/ajoocdatas10.png)

Activez le bouton (bascule) **Activer la capture de données de modification**.

Sélectionnez l’`vangeluw_citisignal_mobile_usage_summary` du jeu de données.

Cliquez sur **Suivant**.

![AJO OC](./images/ajoocdatas18a.png)

Cliquez sur **Choisir les fichiers**. Sélectionnez le **`citisignal_mobile_usage_summary.csv`** de fichier et cliquez sur **ouvrir**.

![AJO OC](./images/ajoocdatas18b.png)

Cliquez sur **Suivant**.

![AJO OC](./images/ajoocdatas18c.png)

Cliquez sur **Terminer**.

![AJO OC](./images/ajoocdatas18d.png)

Au bout de quelques minutes, vous pouvez voir les données ingérées dans votre jeu de données.

![AJO OC](./images/ajoocdatas18e.png)

**`vangeluw_citisignal_internet_usage_summary`**

Accédez à **Sources**, recherchez `local` puis cliquez sur **Ajouter des données** sous **Chargement de fichier local**.

![AJO OC](./images/ajoocdatas10.png)

Activez le bouton (bascule) **Activer la capture de données de modification**.

Sélectionnez l’`vangeluw_citisignal_internet_usage_summary` du jeu de données.

Cliquez sur **Suivant**.

![AJO OC](./images/ajoocdatas19a.png)

Cliquez sur **Choisir les fichiers**. Sélectionnez le **`citisignal_internet_usage_summary.csv`** de fichier et cliquez sur **ouvrir**.

![AJO OC](./images/ajoocdatas19b.png)

Cliquez sur **Suivant**.

![AJO OC](./images/ajoocdatas19c.png)

Cliquez sur **Terminer**.

![AJO OC](./images/ajoocdatas19d.png)

Au bout de quelques minutes, vous pouvez voir les données ingérées dans votre jeu de données.

![AJO OC](./images/ajoocdatas19e.png)

**`vangeluw_citisignal_offers`**

Accédez à **Sources**, recherchez `local` puis cliquez sur **Ajouter des données** sous **Chargement de fichier local**.

![AJO OC](./images/ajoocdatas10.png)

Activez le bouton (bascule) **Activer la capture de données de modification**.

Sélectionnez l’`vangeluw_citisignal_offers` du jeu de données.

Cliquez sur **Suivant**.

![AJO OC](./images/ajoocdatas20a.png)

Cliquez sur **Choisir les fichiers**. Sélectionnez le **`citisignal_offers.csv`** de fichier et cliquez sur **ouvrir**.

![AJO OC](./images/ajoocdatas20b.png)

Cliquez sur **Suivant**.

![AJO OC](./images/ajoocdatas20c.png)

Cliquez sur **Terminer**.

![AJO OC](./images/ajoocdatas20d.png)

Au bout de quelques minutes, vous pouvez voir les données ingérées dans votre jeu de données.

![AJO OC](./images/ajoocdatas20e.png)

**`vangeluw_citisignal_offer_eligibility`**

Accédez à **Sources**, recherchez `local` puis cliquez sur **Ajouter des données** sous **Chargement de fichier local**.

![AJO OC](./images/ajoocdatas10.png)

Activez le bouton (bascule) **Activer la capture de données de modification**.

Sélectionnez l’`vangeluw_citisignal_offer_eligibility` du jeu de données.

Cliquez sur **Suivant**.

![AJO OC](./images/ajoocdatas21a.png)

Cliquez sur **Choisir les fichiers**. Sélectionnez le **`citisignal_offer_eligibility.csv`** de fichier et cliquez sur **ouvrir**.

![AJO OC](./images/ajoocdatas21b.png)

Cliquez sur **Suivant**.

![AJO OC](./images/ajoocdatas21c.png)

Cliquez sur **Terminer**.

![AJO OC](./images/ajoocdatas21d.png)

Au bout de quelques minutes, vous pouvez voir les données ingérées dans votre jeu de données.

![AJO OC](./images/ajoocdatas21e.png)

Toutes les données sont maintenant ingérées.

## 3.8.1.3 Profile Target Dimension

Grâce aux campagnes orchestrées, vous pouvez concevoir et diffuser des communications ciblées au niveau de l’entité, en exploitant les fonctionnalités de schéma relationnel de Adobe Experience Platform. Experience Platform utilise des schémas pour décrire la structure des données de manière cohérente et réutilisable. Lorsque des données sont ingérées dans Experience Platform, elles sont structurées en fonction d’un schéma XDM.

Bien que la segmentation des campagnes orchestrées s’effectue principalement sur des schémas relationnels, la diffusion réelle des messages se produit toujours au niveau du profil.

Lors de la configuration du ciblage, vous devez définir deux aspects essentiels :

- Schémas cibles : vous spécifiez les schémas relationnels éligibles au ciblage. Par défaut, le schéma appelé Destinataire est utilisé, mais vous pouvez configurer d’autres schémas tels que Visiteurs, Clients, etc.

- Liaison de profil : le système doit comprendre comment le schéma cible est mappé au schéma de profil. Pour ce faire, un champ d’identité partagé, qui existe à la fois dans le schéma cible et le schéma de profil, est configuré comme un espace de noms d’identité.

Vous devez maintenant configurer vos dimensions cibles de profil. Accédez à **Administration** > **Configuration**, puis cliquez sur **Gérer** sous **Dimension cible du profil**.

![AJO OC](./images/ajoocptd1.png)

Vous devriez alors voir ceci. Cliquez sur **Créer**.

![AJO OC](./images/ajoocptd2.png)

Pour le **Schéma**, sélectionnez `--aepUserLdap--_citisignal_accounts`. Pour l’option **Valeur d’identité**, sélectionnez **account_id**.

Cliquez sur **Enregistrer**.

![AJO OC](./images/ajoocptd3.png)

Cliquez de nouveau sur **Créer**.

![AJO OC](./images/ajoocptd4.png)

Pour le **Schéma**, sélectionnez `--aepUserLdap--_citisignal_recipients`. Pour l’option **Valeur d’identité**, sélectionnez **account_id**.

Cliquez sur **Enregistrer**.

![AJO OC](./images/ajoocptd5.png)

Cliquez de nouveau sur **Créer**.

![AJO OC](./images/ajoocptd6.png)

Pour le **Schéma**, sélectionnez `--aepUserLdap--_citisignal_recipients`. Pour l’**Valeur d’identité**, sélectionnez **e-mail**.

Cliquez sur **Enregistrer**.

![AJO OC](./images/ajoocptd7.png)

Tu devrais avoir ça.

![AJO OC](./images/ajoocptd8.png)

## Canal e-mail 3.8.1.4

Dans le menu de gauche, accédez à **Canaux**. Cliquez sur **Créer une configuration de canal**.

![AJO OC](./images/ajoocchannel1.png)

Utilisez le nom : `--aepUserLdap---citisignal-email-oc`. Sélectionnez le canal **Email**

![AJO OC](./images/ajoocchannel2.png)

Sélectionnez un **sous-domaine** et **groupe d’adresses IP** disponibles.

![AJO OC](./images/ajoocchannel3.png)

Faites défiler vers le bas et renseignez les **Paramètres d’en-tête**.

- **Nom de l’expéditeur** : `info@techinsiders.org`
- **Préfixe d’e-mail de l’expéditeur** : `info`
- **Nom de la réponse** : `info@techinsiders.org`
- **Répondre à un e-mail** : `info@techinsiders.org`
- **Préfixe e-mail d’erreur** : `error`

![AJO OC](./images/ajoocchannel4.png)

Faites défiler vers le bas. Accédez à **Campagne orchestrée**. Cochez la case **Activé**. Sélectionnez **Dimension de ciblage**.

![AJO OC](./images/ajoocchannel5.png)

Pour **Profile Target Dimension**, sélectionnez `--aepUserLdap--_citisignal_recipients - email`.

Sélectionnez **Dimension cible** et cliquez sur l’icône **ouvrir le dossier**.

![AJO OC](./images/ajoocchannel6.png)

Cliquez sur `--aepUserLdap--_citisignal_recipients`.

![AJO OC](./images/ajoocchannel7.png)

Sélectionnez le champ **e-mail** et cliquez sur **Sélectionner**.

![AJO OC](./images/ajoocchannel8.png)

Faites défiler vers le haut et cliquez sur **Envoyer**.

![AJO OC](./images/ajoocchannel9.png)

Dans l’exercice suivant, vous commencerez à utiliser ces données dans le cadre d’une campagne orchestrée.

## Étapes suivantes

Accédez à [Créer votre campagne orchestrée](./ex2.md){target="_blank"}

Revenez à [Adobe Journey Optimizer : Campagnes orchestrées](./ajocampaigns.md){target="_blank"}

Revenir à [Tous les modules](./../../../../overview.md){target="_blank"}
