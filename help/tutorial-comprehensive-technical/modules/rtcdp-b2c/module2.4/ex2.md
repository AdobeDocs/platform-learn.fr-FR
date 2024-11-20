---
title: Activation de segment vers Microsoft Azure Event Hub - Configuration d’un hub d’événement dans Azure
description: Activation de segment vers Microsoft Azure Event Hub - Configuration d’un hub d’événement dans Azure
kt: 5342
doc-type: tutorial
exl-id: 0c2e94ec-00e8-4f47-add7-ca3a08151225
source-git-commit: 216914c9d97827afaef90e21ed7d4f35eaef0cd3
workflow-type: tm+mt
source-wordcount: '579'
ht-degree: 1%

---

# 2.4.2 Configuration de votre environnement Microsoft Azure EventHub

Azure Event Hubs est un service de publication-abonnement hautement évolutif qui peut ingérer des millions d’événements par seconde et les diffuser dans plusieurs applications. Vous pouvez ainsi traiter et analyser les quantités massives de données produites par vos appareils et applications connectés.

## Qu’est-ce que les centres d’événements Azure ?

Azure Event Hubs est une plateforme de diffusion en continu de données volumineuses et un service d’ingestion d’événements. Il peut recevoir et traiter des millions d’événements par seconde. Les données envoyées à un hub d’événements peuvent être transformées et stockées à l’aide de n’importe quel fournisseur d’analyses en temps réel ou d’adaptateurs de traitement par lot/stockage.

Event Hubs représente la **porte d’entrée** d’un pipeline d’événements, souvent appelé &quot;gestionnaire d’événements&quot; dans les architectures de solution. Un moteur d’événement est un composant ou un service qui se trouve entre les éditeurs d’événements (comme Adobe Experience Platform RTCDP) et les consommateurs d’événements pour découpler la production d’un flux d’événements de la consommation de ces événements. Event Hubs fournit une plateforme de diffusion en continu unifiée avec tampon de conservation du temps, découplant les producteurs d’événements des consommateurs d’événements.

## Création d’un espace de noms Event Hubs

Accédez à [https://portal.azure.com/#home](https://portal.azure.com/#home) et sélectionnez **Créer une ressource**.

![1-01-open-azure-portal.png](./images/101openazureportal.png)

Dans l’écran de la ressource, saisissez **Event** dans la barre de recherche. Recherchez la carte **Event Hubs**, cliquez sur **Create**, puis sur **Event Hubs**.

![1-02-search-event-hubs.png](./images/102searcheventhubs.png)

Si c’est la première fois que vous créez une ressource dans Azure, vous devez créer un **groupe de ressources**. Si vous avez déjà un groupe de ressources, vous pouvez le sélectionner (ou en créer un).

Cliquez sur **Créer** et nommez votre groupe `--aepUserLdap---aep-enablement`, cliquez sur **OK**.

![1-04-create-resource-group.png](./images/104createresourcegroup.png)

Renseignez le reste des champs comme indiqué :

- Espace de noms : définissez votre espace de noms, il doit être unique, utilisez le modèle suivant `--aepUserLdap---aep-enablement`
- Emplacement : choisissez n’importe quel emplacement
- Niveau de prix : **De base**
- Unités de débit : **1**

Cliquez sur **Réviser + créer**.

![1-05-create-namespace.png](./images/105createnamespace.png)

Cliquez sur **Créer**.

![1-07-namespace-create.png](./images/107namespacecreate.png)

Le déploiement de votre groupe de ressources peut prendre entre 1 et 2 minutes. En cas de réussite, l’écran suivant s’affiche :

![1-08-namespace-deploy.png](./images/108namespacedeploy.png)

## Configuration de votre hub d’événements dans Azure

Accédez à [https://portal.azure.com/#home](https://portal.azure.com/#home) et sélectionnez **Toutes les ressources**.

![1-09-all-resources.png](./images/109allresources.png)

Dans la liste des ressources, cliquez sur l’espace de noms `--aepUserLdap---aep-enablement` Event Hubs :

![1-10-list-resources.png](./images/110listresources.png)

Dans l’écran de détails `--aepUserLdap---aep-enablement`, accédez à **Entities** et cliquez sur **Event Hubs** :

![1-11-eventhub-namespace.png](./images/111eventhubnamespace.png)

Cliquez sur **+ Event Hub**.

![1-12-add-event-hub.png](./images/112addeventhub.png)

Utilisez `--aepUserLdap---aep-enablement-event-hub` comme nom et cliquez sur **Réviser + Créer**.

![1-13-create-event-hub.png](./images/113createeventhub.png)

Cliquez sur **Créer**.

![1-13-create-event-hub.png](./images/113createeventhub1.png)

Dans **Event Hubs** sous l’espace de noms de votre centre d’événements, votre **Event Hub** est maintenant répertorié.

![1-14-event-hub-list.png](./images/114eventhublist.png)

## Configuration de votre compte Azure Storage

Pour déboguer votre fonction Azure Event Hub dans des exercices ultérieurs, vous devrez fournir un compte de stockage Azure dans le cadre de la configuration de votre projet Visual Studio Code. Vous allez maintenant créer ce compte Azure Storage.

Accédez à [https://portal.azure.com/#home](https://portal.azure.com/#home) et sélectionnez **Créer une ressource**.

![1-15-event-hub-storage.png](./images/115eventhubstorage.png)

Saisissez **compte de stockage** dans la recherche, recherchez la carte de **compte de stockage** et cliquez sur **Compte de stockage**.

![1-16-event-hub-search-storage.png](./images/116eventhubsearchstorage.png)

Spécifiez votre **Groupe de ressources** (créé au début de cet exercice), utilisez `--aepUserLdap--aepstorage` comme nom de votre compte de stockage et sélectionnez **Stockage redondant localement (LRS)**, puis cliquez sur **Réviser + créer**.

![1-18-event-hub-create-review-storage.png](./images/118eventhubcreatereviewstorage.png)

Cliquez sur **Créer**.

![1-19-event-hub-submit-storage.png](./images/119eventhubsubmitstorage.png)

La création de notre compte de stockage prendra quelques secondes :

![1-20-event-hub-deploy-storage.png](./images/120eventhubdeploystorage.png)

Lorsque vous avez terminé, votre écran affiche le bouton **Accéder à la ressource**.

Cliquez sur **Home**.

![1-21-event-hub-deploy-ready-storage.png](./images/121eventhubdeployreadystorage.png)

Votre compte de stockage est maintenant visible sous **Ressources récentes**.

![1-22-event-hub-deploy-resources-list.png](./images/122eventhubdeployresourceslist.png)

Étape suivante : [2.4.3 Configuration de votre destination Azure Event Hub dans Adobe Experience Platform](./ex3.md)

[Revenir au module 2.4](./segment-activation-microsoft-azure-eventhub.md)

[Revenir à tous les modules](./../../../overview.md)
