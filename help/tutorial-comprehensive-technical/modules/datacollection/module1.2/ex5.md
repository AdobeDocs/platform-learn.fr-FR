---
title: Foundation - Ingestion de données - Ingestion de données à partir de sources hors ligne
description: Foundation - Ingestion de données - Ingestion de données à partir de sources hors ligne
kt: 5342
doc-type: tutorial
exl-id: 21b84a77-4115-4ba7-b847-b236aa14bbdd
source-git-commit: 8bdcd03bd38a6da98b82439ad86482cad5f4e684
workflow-type: tm+mt
source-wordcount: '771'
ht-degree: 4%

---

# 1.2.5 Zone d’entrée des données

Dans cet exercice, l’objectif est de configurer votre connecteur Source de zone d’entrée de données avec le stockage Azure Blob.

Data Landing Zone est une interface de stockage Azure Blob configurée par Adobe Experience Platform, qui vous permet d’accéder à une fonctionnalité de stockage de fichiers sécurisée basée sur le cloud pour importer des fichiers dans Platform. Data Landing Zone prend en charge l’authentification basée sur SAS et ses données sont protégées par des mécanismes de sécurité de stockage Azure Blob standard au repos et en transit. L’authentification SAS vous permet d’accéder en toute sécurité au conteneur de votre zone d’entrée de données par le biais d’une connexion Internet publique.

>[!NOTE]
>
> Adobe Experience Platform **applique une durée de vie stricte de sept jours (TTL)** sur tous les fichiers chargés dans un conteneur de zone d’entrée de données. Tous les fichiers sont supprimés au bout de sept jours.


## Conditions préalables

Pour copier des objets Blob ou des fichiers dans votre zone d’entrée de données Adobe Experience Platform, vous utiliserez AzCopy, un utilitaire de ligne de commande. Vous pouvez télécharger une version de votre système d’exploitation via [https://docs.microsoft.com/en-us/azure/storage/common/storage-use-azcopy-v10](https://docs.microsoft.com/en-us/azure/storage/common/storage-use-azcopy-v10), faire défiler cette page vers le bas jusqu’à **Télécharger le binaire portable AzCopy** et sélectionner la version appropriée pour votre système d’exploitation.

![dlz-install-az-copy.png](./images/dlzinstallazcopy.png)

- Décompressez le fichier téléchargé.

![dlz-install-az-copy.png](./images/dlz1.png)

- Téléchargez le fichier de données d’exemple global-context-websiteinteractions.csv, qui contient des exemples d’interactions de site web et enregistrez-le dans le dossier dans lequel vous avez décompressé **azcopy**.

![dlz-install-az-copy.png](./images/dlz2.png)

- Ouvrez une fenêtre de terminal et accédez au dossier sur votre bureau. Vous devriez voir le contenu suivant (azcopy et global-context-websiteinteractions.csv), par exemple sur OSX :

![dlz-unzip-azcopy.png](./images/dlzunzipazcopy.png)

## 1.2.5.2 Connexion de la zone d’entrée des données à Adobe Experience Platform

Connectez-vous à Adobe Experience Platform en accédant à cette URL : [https://experience.adobe.com/platform](https://experience.adobe.com/platform).

Une fois connecté, vous accédez à la page d’accueil de Adobe Experience Platform.

![Ingestion des données](./images/home.png)

Avant de continuer, vous devez sélectionner un **sandbox**. L’environnement de test à sélectionner est nommé ``--aepSandboxName--``.  Après avoir sélectionné l’environnement de test approprié, l’écran change et vous êtes désormais dans votre environnement de test dédié.

![Ingestion des données](./images/sb1.png)

Dans le menu de gauche, accédez à **Sources**. Dans le catalogue Sources, recherchez **entrée de données**.

![Ingestion des données](./images/sourcesdlz.png)

Cliquez sur la carte **Zone d’entrée des données** . Les informations d’identification s’affichent dans l’onglet de droite.

![dlz-view-credentials.png](./images/dlzviewcredentials.png)

Cliquez sur l’icône comme indiqué pour copier le **SASUri**.

![dlz-copy-sas-uri.png](./images/dlzcopysasuri.png)

## Copiez votre fichier csv dans votre zone d’entrée de données AEP.

Vous allez désormais ingérer des données dans Adobe Experience Platform à l’aide des outils de ligne de commande Azure à l’aide d’AZCopy.

Ouvrez un terminal à l’emplacement de votre installation azcopy et exécutez la commande suivante pour copier un fichier dans la zone d’entrée de données d’AEP :

``./azcopy copy <your-local-file> <your SASUri>``

Veillez à entourer votre SASUri de guillemets doubles. Remplacez `<your-local-file>` par le chemin d’accès à votre copie locale du fichier **global-context-websiteinteractions.csv** dans le répertoire azcopy, et remplacez `<your SASUri>` par la valeur **SASUri** que vous avez copiée à partir de l’interface utilisateur de Adobe Experience Platform. Votre commande doit se présenter comme suit :

```command
./azcopy copy global-context-websiteinteractions.csv "https://sndbxdtlnd2bimpjpzo14hp6.blob.core.windows.net/dlz-user-container?sv=2020-04-08&si=dlz-xxxxxxx-9843-4973-ae52-xxxxxxxx&sr=c&sp=racwdlm&sig=DN3kdhKzard%2BQwKASKg67Zxxxxxxxxxxxxxxxx"
```

Après avoir exécuté la commande ci-dessus dans votre terminal, vous verrez ceci :

![dlz-exec-copy-command.png](./images/dlzexeccopycommand.png)

## Rechercher votre fichier dans votre zone d’entrée des données

Accédez à votre zone d’entrée de données dans Adobe Experience Platform.

Sélectionnez **Sources**, recherchez **l&#39;entrée de données** et cliquez sur le bouton **Configuration**.

![dlz-inspection-datalanding-zone.png](./images/dlzinspectdatalandingzone.png)

Cela ouvrira la zone d’entrée des données. Vous verrez le fichier que vous venez de télécharger dans le panneau **select data** de la zone d’entrée de données.

![dlz-datalanding-zone-open.png](./images/dlzdatalandingzoneopen.png)

## Traiter votre fichier

Sélectionnez votre fichier et sélectionnez le format de données **Délimité**. Vous verrez alors un aperçu de vos données. Cliquez sur **Suivant**.

![dlz-datalanding-select-file.png](./images/dlzdatalandingselectfile.png)

Vous pouvez maintenant commencer à mapper les données chargées pour qu’elles correspondent au schéma XDM de votre jeu de données.

Sélectionnez **Jeu de données existant** et sélectionnez le jeu de données **Demo System - Event Dataset for Website (Global v1.1)**. Cliquez sur **Suivant**.

![dlz-target-dataset.png](./images/dlztargetdataset.png)

Vous êtes maintenant prêt à mapper les données source entrantes de votre fichier csv aux champs cibles du schéma XDM du jeu de données.

![dlz-start-mapping.png](./images/dlzstartmapping.png)

>[!NOTE]
>
> Peu importe les erreurs potentielles avec le mappage. Vous corrigerez le mappage à l’étape suivante.

## Mapper les champs

Tout d&#39;abord, cliquez sur le bouton **Effacer tous les mappages** . Vous pouvez ensuite commencer avec un mapping propre.

![dlz-clear-mappings.png](./images/mappings1.png)

Cliquez ensuite sur **Nouveau type de champ** et sélectionnez **Ajouter un nouveau champ**.

![dlz-clear-mappings.png](./images/dlzclearmappings.png)

Pour mapper le champ source **ecid**, sélectionnez le champ **identities.ecid** et cliquez sur **Sélectionner**.

![dlz-map-identity.png](./images/dlzmapidentity.png)

Cliquez ensuite sur **Mapper le champ cible**.

![dlz-map-select-target-field.png](./images/dlzmapselecttargetfield.png)

Sélectionnez le champ ``--aepTenantId--``.identification.core.ecid dans la structure du schéma.

![dlz-map-target-field.png](./images/dlzmaptargetfield.png)

Vous devez mapper deux autres champs, cliquer sur **+ Nouveau type de champ** suivi de **Ajouter un nouveau champ** et ajouter des champs pour ce mappage.

| source | cible |
|---|---|
| resource.info.pagename | web.webPageDetails.name |
| date et heure | date et heure |
| date et heure | _id |

![dlz-add-other-mapping.png](./images/dlzaddothermapping.png)

Lorsque vous avez terminé, l’écran ci-dessous doit ressembler à celui qui est affiché. Cliquez sur **Suivant**.

![dlz-mapping-result.png](./images/dlzmappingresult.png)

Cliquez sur **Suivant**.

![dlz-default-schedule.png](./images/dlzdefaultscheduling.png)

Cliquez sur **Terminer**.

![dlz-import-end.png](./images/dlzimportfinish.png)

## Surveiller le flux de données

Pour surveiller votre flux de données, accédez à **Sources**, **Flux de données** et cliquez sur votre flux de données :

![dlz-monitor-dataflow.png](./images/dlzmonitordataflow.png)

Le chargement des données peut prendre quelques minutes. En cas de réussite, l’état de **Succès** s’affiche :

![dlz-monitor-dataflow-result.png](./images/dlzmonitordataflowresult.png)

Étape suivante : [Résumé et avantages](./summary.md)

[Revenir au module 1.2](./data-ingestion.md)

[Revenir à tous les modules](../../../overview.md)
