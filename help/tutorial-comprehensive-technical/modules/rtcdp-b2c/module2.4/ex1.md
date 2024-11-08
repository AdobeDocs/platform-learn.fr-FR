---
title: Activation de segment vers Microsoft Azure Event Hub - Configuration d’un hub d’événement dans Azure
description: Activation de segment vers Microsoft Azure Event Hub - Configuration d’un hub d’événement dans Azure
kt: 5342
doc-type: tutorial
source-git-commit: 6962a0d37d375e751a05ae99b4f433b0283835d0
workflow-type: tm+mt
source-wordcount: '589'
ht-degree: 1%

---

# 2.4.1 Configuration de votre environnement Microsoft Azure EventHub

Azure Event Hubs est un service de publication-abonnement hautement évolutif qui peut ingérer des millions d’événements par seconde et les diffuser dans plusieurs applications. Vous pouvez ainsi traiter et analyser les quantités massives de données produites par vos appareils et applications connectés.

## 2.4.1.1 Qu’est-ce que les centres d’événements Azure ?

Azure Event Hubs est une plateforme de diffusion en continu de données volumineuses et un service d’ingestion d’événements. Il peut recevoir et traiter des millions d’événements par seconde. Les données envoyées à un hub d’événements peuvent être transformées et stockées à l’aide de n’importe quel fournisseur d’analyses en temps réel ou d’adaptateurs de traitement par lot/stockage.

Event Hubs représente la **porte d’entrée** d’un pipeline d’événements, souvent appelé &quot;gestionnaire d’événements&quot; dans les architectures de solution. Un moteur d’événement est un composant ou un service qui se trouve entre les éditeurs d’événements (comme Adobe Experience Platform RTCDP) et les consommateurs d’événements pour découpler la production d’un flux d’événements de la consommation de ces événements. Event Hubs fournit une plateforme de diffusion en continu unifiée avec tampon de conservation du temps, découplant les producteurs d’événements des consommateurs d’événements.

## 2.4.1.2 Création d’un espace de noms Event Hubs

Accédez à [https://portal.azure.com/#home](https://portal.azure.com/#home) et sélectionnez **Créer une ressource**.

![1-01-open-azure-portal.png](./images/1-01-open-azure-portal.png)

Dans l’écran de la ressource, saisissez **Event** dans la barre de recherche et sélectionnez **Event Hubs** dans la liste déroulante :

![1-02-search-event-hubs.png](./images/1-02-search-event-hubs.png)

Cliquez sur **Créer** :

![1-03-event-hub-create.png](./images/1-03-event-hub-create.png)

Si c’est la première fois que vous créez une ressource dans Azure, vous devez créer un **groupe de ressources**. Si vous avez déjà un groupe de ressources, vous pouvez le sélectionner (ou en créer un).

Sélectionnez **Créer**, nommez votre groupe `--aepUserLdap---aep-enablement`.

![1-04-create-resource-group.png](./images/1-04-create-resource-group.png)

Effectuez le test des champs comme indiqué :

- Espace de noms : définissez votre espace de noms, il doit être unique, utilisez le modèle suivant `--aepUserLdap---aep-enablement`
- Emplacement : **West-Europe** fait référence au centre de données Azure à Amsterdam
- Niveau de prix : **De base**
- Unités de débit : **1**

![1-05-create-namespace.png](./images/1-05-create-namespace.png)

Cliquez sur **Réviser + créer**.

![1-06-namespace-review-create.png](./images/1-06-namespace-review-create.png)

Cliquez sur **Créer**.

![1-07-namespace-create.png](./images/1-07-namespace-create.png)

Le déploiement de votre groupe de ressources peut prendre entre 1 et 2 minutes. En cas de réussite, l’écran suivant s’affiche :

![1-08-namespace-deploy.png](./images/1-08-namespace-deploy.png)

## 2.4.1.3 Configuration de votre hub d’événements dans Azure

Accédez à [https://portal.azure.com/#home](https://portal.azure.com/#home) et sélectionnez **Toutes les ressources**.

![1-09-all-resources.png](./images/1-09-all-resources.png)

Dans la liste des ressources, sélectionnez votre espace de noms `--aepUserLdap---aep-enablement` :

![1-10-list-resources.png](./images/1-10-list-resources.png)

Dans l’écran de détails `--aepUserLdap---aep-enablement`, sélectionnez **Event Hubs** :

![1-11-eventhub-namespace.png](./images/1-11-eventhub-namespace.png)

Cliquez sur **+ Event Hub**.

![1-12-add-event-hub.png](./images/1-12-add-event-hub.png)

Utilisez `--aepUserLdap---aep-enablement-event-hub` comme nom et cliquez sur **Créer**.

![1-13-create-event-hub.png](./images/1-13-create-event-hub.png)

Cliquez sur **Event Hubs** dans l’espace de noms de votre hub d’événements. Votre **Centre d’événements** devrait maintenant être répertorié. Si c’est le cas, vous pouvez passer à l’exercice suivant.

![1-14-event-hub-list.png](./images/1-14-event-hub-list.png)

## 2.4.1.4 Configuration de votre compte Azure Storage

Pour déboguer votre fonction Azure Event Hub dans des exercices ultérieurs, vous devrez fournir un compte de stockage Azure dans le cadre de la configuration de votre projet Visual Studio Code. Vous allez maintenant créer ce compte Azure Storage.

Accédez à [https://portal.azure.com/#home](https://portal.azure.com/#home) et sélectionnez **Créer une ressource**.

![1-15-event-hub-storage.png](./images/1-15-event-hub-storage.png)

Saisissez **storage** dans la recherche et sélectionnez **Compte de stockage** dans la liste.

![1-16-event-hub-search-storage.png](./images/1-16-event-hub-search-storage.png)

Sélectionnez **Créer**.

![1-17-event-hub-create-storage.png](./images/1-17-event-hub-create-storage.png)

Spécifiez votre **Groupe de ressources** (créé au début de cet exercice), utilisez `--aepUserLdap--aepstorage` comme nom de compte de stockage, sélectionnez **Stockage redondant localement (LRS)**, puis cliquez sur **Réviser + créer**.

![1-18-event-hub-create-review-storage.png](./images/1-18-event-hub-create-review-storage.png)

Cliquez sur **Créer**.

![1-19-event-hub-submit-storage.png](./images/1-19-event-hub-submit-storage.png)

La création de votre compte de stockage prendra quelques secondes :

![1-20-event-hub-deploy-storage.png](./images/1-20-event-hub-deploy-storage.png)

Lorsque vous avez terminé, votre écran affiche le bouton **Accéder à la ressource**.

Cliquez sur **Microsoft Azure**.

![1-21-event-hub-deploy-ready-storage.png](./images/1-21-event-hub-deploy-ready-storage.png)

Votre compte de stockage est maintenant visible sous **Ressources récentes**.

![1-22-event-hub-deploy-resources-list.png](./images/1-22-event-hub-deploy-resources-list.png)

Étape suivante : [2.4.2 Configuration de votre destination Azure Event Hub dans Adobe Experience Platform](./ex2.md)

[Revenir au module 2.4](./segment-activation-microsoft-azure-eventhub.md)

[Revenir à tous les modules](./../../../overview.md)
