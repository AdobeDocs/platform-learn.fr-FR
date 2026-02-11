---
title: Foundation - Ingestion de données - Ingestion de données à partir de sources hors ligne
description: Foundation - Ingestion de données - Ingestion de données à partir de sources hors ligne
kt: 5342
doc-type: tutorial
exl-id: 9fce6ece-f454-45de-9c95-35d604b3ae95
source-git-commit: 23816907de778cbe3b9708f4a7273bdcb8e86d5c
workflow-type: tm+mt
source-wordcount: '767'
ht-degree: 4%

---

# 1.2.5 Zone D’Atterrissage Des Données

Dans cet exercice, l’objectif est de configurer votre connecteur Source de zone d’atterrissage de données avec le stockage Blob d’Azure.

Data Landing Zone est une interface de stockage Blob d’Azure fournie par Adobe Experience Platform. Elle vous permet d’accéder à une fonctionnalité de stockage de fichiers sécurisée basée sur le cloud pour importer des fichiers dans Platform. La zone d’atterrissage de données prend en charge l’authentification SAS et ses données sont protégées par des mécanismes de sécurité de stockage Blob Azure standard au repos et en transit. L’authentification SAS vous permet d’accéder en toute sécurité à votre conteneur Data Landing Zone par le biais d’une connexion Internet publique.

>[!NOTE]
>
> Adobe Experience Platform **applique une durée de vie (TTL) stricte de sept jours sur tous les fichiers chargés dans un conteneur Data Landing Zone** Tous les fichiers sont supprimés au bout de sept jours.


## Conditions préalables

Pour copier des objets Blob ou des fichiers dans votre zone d’atterrissage de données Adobe Experience Platform, vous utiliserez AzCopy, un utilitaire de ligne de commande. Vous pouvez télécharger une version pour votre système d’exploitation via [https://docs.microsoft.com/en-us/azure/storage/common/storage-use-azcopy-v10](https://docs.microsoft.com/en-us/azure/storage/common/storage-use-azcopy-v10), faites défiler cette page vers le bas pour **Télécharger le fichier binaire portable AzCopy** et sélectionnez la version appropriée pour votre système d’exploitation.

![dlz-install-az-copy.png](./images/dlzinstallazcopy.png)

- Décompressez le fichier téléchargé

![dlz-install-az-copy.png](./images/dlz1.png)

- Téléchargez l’exemple de fichier de données [global-context-websiteinteractions.csv](./../../../../assets/csv/data-ingestion/global-context-websiteinteractions.csv), qui contient des exemples d’interactions de site web et enregistrez-le dans le dossier dans lequel vous avez décompressé **azcopy**.

![dlz-install-az-copy.png](./images/dlz2.png)

- Ouvrez une fenêtre de terminal et accédez au dossier sur votre bureau. Le contenu suivant doit s’afficher (azcopy et global-context-websiteinteractions.csv), par exemple sur OSX :

![dlz-unzip-azcopy.png](./images/dlzunzipazcopy.png)

## 1.2.5.2 Connecter Data Landing Zone à Adobe Experience Platform

Connectez-vous à Adobe Experience Platform en accédant à cette URL : [https://experience.adobe.com/platform](https://experience.adobe.com/platform).

Une fois connecté, vous accédez à la page d’accueil de Adobe Experience Platform.

![Ingestion des données](./images/home.png)

Avant de continuer, vous devez sélectionner un **sandbox**. Le sandbox à sélectionner est nommé ``--aepSandboxName--``.  Après avoir sélectionné la sandbox appropriée, la modification d’écran s’affiche et vous êtes maintenant dans votre sandbox dédiée.

![Ingestion des données](./images/sb1.png)

Dans le menu de gauche, accédez à **Sources**. Dans le catalogue des sources, recherchez **data landing**.

![Ingestion des données](./images/sourcesdlz.png)

Cliquez sur la carte **Zone d’atterrissage des données** pour afficher les informations d’identification dans l’onglet de droite.

![dlz-view-credentials.png](./images/dlzviewcredentials.png)

Cliquez sur l’icône comme indiqué pour copier le **SASUri**.

![dlz-copy-sas-uri.png](./images/dlzcopysasuri.png)

## Copiez votre fichier csv dans votre zone d’atterrissage de données AEP

Vous allez désormais ingérer des données dans Adobe Experience Platform à l’aide des outils de ligne de commande Azure à l’aide d’AZCopy.

Ouvrez un terminal à l’emplacement de votre installation azcopy et exécutez la commande suivante pour copier un fichier dans la zone d’atterrissage des données d’AEP :

``./azcopy copy <your-local-file> <your SASUri>``

Veillez à entourer votre SASUri de guillemets doubles. Remplacez `<your-local-file>` par le chemin d’accès à votre copie locale du fichier **global-context-websiteinteractions.csv** dans le répertoire azcopy, puis remplacez `<your SASUri>` par la valeur **SASUri** que vous avez copiée à partir de l’interface utilisateur de Adobe Experience Platform. Votre commande doit se présenter comme suit :

```command
./azcopy copy global-context-websiteinteractions.csv "https://sndbxdtlnd2bimpjpzo14hp6.blob.core.windows.net/dlz-user-container?sv=2020-04-08&si=dlz-xxxxxxx-9843-4973-ae52-xxxxxxxx&sr=c&sp=racwdlm&sig=DN3kdhKzard%2BQwKASKg67Zxxxxxxxxxxxxxxxx"
```

Après avoir exécuté la commande ci-dessus dans votre terminal, vous verrez ceci :

![dlz-exec-copy-command.png](./images/dlzexeccopycommand.png)

## Recherche de votre fichier dans votre zone d’atterrissage de données

Accédez à votre zone d’atterrissage de données dans Adobe Experience Platform.

Sélectionnez **Sources**, recherchez **data landing** et cliquez sur le bouton **Setup**.

![dlz-inspecter-datalanding-zone.png](./images/dlzinspectdatalandingzone.png)

Cela ouvrira la zone d’atterrissage de données. Le fichier que vous venez de charger s’affiche dans le panneau **Sélectionner les données** de la zone d’atterrissage de données.

![dlz-datalanding-zone-open.png](./images/dlzdatalandingzoneopen.png)

## Traiter votre fichier

Sélectionnez votre fichier et sélectionnez **Délimité** comme format de données. Un aperçu de vos données s’affiche alors. Cliquez sur **Suivant**.

![dlz-datalanding-select-file.png](./images/dlzdatalandingselectfile.png)

Vous pouvez maintenant commencer à mapper les données chargées pour qu’elles correspondent au schéma XDM de votre jeu de données.

Sélectionnez **Jeu de données existant** et sélectionnez le jeu de données **Système de démonstration - Jeu de données d’événement pour le site web (global v1.1)**. Cliquez sur **Suivant**.

![dlz-target-dataset.png](./images/dlztargetdataset.png)

Vous êtes maintenant prêt à mapper les données source entrantes de votre fichier csv aux champs cibles à partir du schéma XDM du jeu de données.

![dlz-start-mapping.png](./images/dlzstartmapping.png)

>[!NOTE]
>
> Peu importe les erreurs potentielles avec le mappage. Vous corrigerez le mappage à l’étape suivante.

## Champs de mappage

Tout d’abord, cliquez sur le bouton **Effacer tous les mappages**. Vous pouvez ensuite commencer avec un mapping propre.

![dlz-clear-mappings.png](./images/mappings1.png)

Cliquez ensuite sur **Nouveau type de champ** puis sélectionnez **Ajouter un nouveau champ**.

![dlz-clear-mappings.png](./images/dlzclearmappings.png)

Pour mapper le champ source **ecid**, sélectionnez le champ **identités.ecid** et cliquez sur **Sélectionner**.

![dlz-map-identity.png](./images/dlzmapidentity.png)

Cliquez ensuite sur **Mapper le champ cible**.

![dlz-map-select-target-field.png](./images/dlzmapselecttargetfield.png)

Sélectionnez le champ ``--aepTenantId--``.identification.core.ecid dans la structure du schéma.

![dlz-map-target-field.png](./images/dlzmaptargetfield.png)

Vous devez mapper d’autres champs, cliquer sur **+ Nouveau type de champ** suivi de **Ajouter un nouveau champ** et ajouter des champs pour ce mappage

| source | cible |
|---|---|
| resource.info.pagename | web.webPageDetails.name |
| date et heure | date et heure |
| date et heure | _id |

![dlz-add-other-mapping.png](./images/dlzaddothermapping.png)

Lorsque vous avez terminé, l’écran ci-dessous doit ressembler à ceci : Cliquez sur **Suivant**.

![dlz-mapping-result.png](./images/dlzmappingresult.png)

Cliquez sur **Suivant**.

![dlz-default-scheduling.png](./images/dlzdefaultscheduling.png)

Cliquez sur **Terminer**.

![dlz-import-finish.png](./images/dlzimportfinish.png)

## Surveiller le flux de données

Pour surveiller votre flux de données, accédez à **Sources**, **Flux de données** et cliquez sur votre flux de données :

![dlz-monitor-dataflow.png](./images/dlzmonitordataflow.png)

Le chargement des données peut prendre quelques minutes. En cas de réussite, le statut **Succès** s’affiche :

![dlz-monitor-dataflow-result.png](./images/dlzmonitordataflowresult.png)

## Étapes suivantes

Revenir à [Ingestion des données](./data-ingestion.md){target="_blank"}

Revenir à [Tous les modules](./../../../../overview.md){target="_blank"}
