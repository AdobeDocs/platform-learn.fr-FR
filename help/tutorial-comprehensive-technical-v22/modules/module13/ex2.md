---
title: Activation des segments vers Microsoft Azure Event Hub - Configuration de la destination RTCDP du centre d’événements dans Adobe Experience Platform
description: Activation des segments vers Microsoft Azure Event Hub - Configuration de la destination RTCDP du centre d’événements dans Adobe Experience Platform
kt: 5342
audience: Data Engineer, Data Architect, Data Analyst
doc-type: tutorial
activity: develop
exl-id: b42b4ccb-1952-480b-b538-c1bd661e29eb
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '558'
ht-degree: 1%

---

# 13.2 Configuration de la destination Azure Event Hub dans Adobe Experience Platform

## 13.2.1 Identification des paramètres de connexion Azure requis

Pour définir une destination Event Hub dans Adobe Experience Platform, vous avez besoin de :

- Espace de noms des centres d’événements
- Centre d’événements
- Nom de clé Azure SAS
- Clé Azure SAS

Event Hub et EventHub namespace ont été définis dans l’exercice précédent : [Exercice 1 - Configuration du hub d’événements dans Azure](./ex1.md)

### Espace de noms des centres d’événements

Pour rechercher les informations ci-dessus dans Azure Portal, accédez à [https://portal.azure.com/#home](https://portal.azure.com/#home). Assurez-vous que vous utilisez le compte Azure approprié.

Sélectionner **Toutes les ressources** dans Azure Portal :

![2-01-azure-all-resources.png](./images/2-01-azure-all-resources.png)

### Centre d’événements

Rechercher une ressource avec un type de ressource **Espace de noms des centres d’événements**, si vous avez respecté les conventions d’affectation de noms utilisées dans l’exercice précédent, l’espace de noms des centres d’événements sera `--demoProfileLdap---aep-enablement`. Prenez note, vous en aurez besoin dans le prochain exercice.

![2-02-select-event-hubs-namespace.png](./images/2-02-select-event-hubs-namespace.png)

Cliquez sur le nom Espace de noms des centres d’événements pour obtenir les détails :

![2-03-select-event-hub.png](./images/2-03-select-event-hub.png)

Sélectionner **Centre d’événements** pour obtenir une liste des centres d’événements définis dans l’espace de noms des centres d’événements, si vous avez suivi les conventions d’affectation de noms utilisées dans l’exercice précédent, vous trouverez un centre d’événements nommé `--demoProfileLdap---aep-enablement-event-hub`. Prenez note, vous en aurez besoin dans le prochain exercice.

![2-04-event-hub-selected.png](./images/2-04-event-hub-selected.png)

### Nom de clé SAS

Sélectionner **Stratégies d’accès partagées** pour votre **Espace de noms des centres d’événements**

![2-05-select-sas.png](./images/2-05-select-sas.png)

Une liste des stratégies d’accès partagées s’affiche. La clé SAS que nous recherchons est **RootManageSharedAccessKey**. Il s’agit du nom de la clé SAS. Écris-le !

![2-06-sas-overview.png](./images/2-06-sas-overview.png)

### Valeur clé SAS

Cliquez sur le bouton **RootManageSharedAccessKey** pour obtenir la valeur de clé SAS. Et appuyez sur la touche **Copier dans le presse-papiers** pour copier l’icône **Clé Principal**:

![2-07-sas-key-value.png](./images/2-07-sas-key-value.png)

### Résumé des valeurs de destination

À ce stade, vous devez avoir identifié toutes les valeurs nécessaires pour définir la destination Azure Event Hub dans la plateforme de données clients en temps réel de Adobe Experience Platform.

| Nom de l’attribut de destination | Valeur d’attribut de destination | Exemple de valeur |
|---|---|---|
| sasKeyName | Nom de clé SAS | RootManageSharedAccessKey |
| sasKey | Valeur clé SAS | srREx9ShJG1Rv7f/... |
| espace de noms | Espace de noms des centres d’événements | `--demoProfileLdap---aep-enablement` |
| eventHubName | Centre d’événements | `--demoProfileLdap---aep-enablement-event-hub` |

## 13.2.2 Création d’une destination Azure Event Hub dans Adobe Experience Platform

Connectez-vous à Adobe Experience Platform en accédant à cette URL : [https://experience.adobe.com/platform](https://experience.adobe.com/platform).

Une fois connecté, vous accédez à la page d’accueil de Adobe Experience Platform.

![Ingestion des données](../module2/images/home.png)

Avant de continuer, vous devez sélectionner une **sandbox**. L’environnement de test à sélectionner est nommé ``--aepSandboxId--``. Pour ce faire, cliquez sur le texte **[!UICONTROL Production Prod]** dans la ligne bleue en haut de votre écran. Après avoir sélectionné l’environnement de test approprié, l’écran change et vous êtes désormais dans votre environnement de test dédié.

![Ingestion des données](../module2/images/sb1.png)

Accédez à **Destinations**, puis accédez à **Catalogue**.

![Ingestion des données](./images/sb2a.png)

Sélectionner **Stockage dans le cloud** et accédez à **Centre d’événements Azure** et cliquez sur **Configuration** ou **Configurer**:

![2-08-list-destinations.png](./images/2-08-list-destinations.png)

Renseignez les valeurs de destination que vous avez collectées lors de l’exercice précédent. Cliquez ensuite sur **Connexion à la destination**.

![2-09-destination-values.png](./images/2-09-destination-values.png)

Si vos informations d’identification étaient correctes, une confirmation s’affiche : **Connecté**.

![2-09-destination-values.png](./images/2-09-destination-valuesa.png)

Vous devez maintenant saisir le nom et la description au format `--demoProfileLdap---aep-enablement`. Saisissez le **eventHubName** (voir exercice précédent, il ressemble à ceci : `--demoProfileLdap---aep-enablement-event-hub`) et cliquez sur **Suivant**.

![2-10-create-destination.png](./images/2-10-create-destination.png)

Cliquez sur **Enregistrer et quitter**.

![2-11-save-exit-activation.png](./images/2-11-save-exit-activation.png)

Votre destination est maintenant créée et disponible dans Adobe Experience Platform.

![2-12-destination-created.png](./images/2-12-destination-created.png)

Étape suivante : [13.3 Création d’un segment](./ex3.md)

[Revenir au module 13](./segment-activation-microsoft-azure-eventhub.md)

[Revenir à tous les modules](./../../overview.md)
