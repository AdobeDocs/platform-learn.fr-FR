---
title: Audience Activation à Microsoft Azure Event Hub - Activation d’Audience
description: Audience Activation à Microsoft Azure Event Hub - Activation d’Audience
kt: 5342
doc-type: tutorial
exl-id: 89cfda0e-6c5e-45ab-9506-f0f0f6211e7f
source-git-commit: b4a7144217a68bc0b1bc70b19afcbc52e226500f
workflow-type: tm+mt
source-wordcount: '216'
ht-degree: 4%

---

# 2.4.5 Activation de l’audience

## Ajout d’audience à la destination Azure Event Hub

Dans cet exercice, vous allez ajouter votre audience `--aepUserLdap-- - Interest in Plans` à votre destination `--aepUserLdap---aep-enablement` Azure Event Hub.

Connectez-vous à Adobe Experience Platform en accédant à cette URL : [https://experience.adobe.com/platform](https://experience.adobe.com/platform).

Une fois connecté, vous accédez à la page d’accueil de Adobe Experience Platform.

![Ingestion des données](./../../../modules/datacollection/module1.2/images/home.png)

Avant de continuer, vous devez sélectionner un **sandbox**. L’environnement de test à sélectionner est nommé ``--aepSandboxName--``. Après avoir sélectionné l’environnement de test approprié, l’écran change et vous êtes désormais dans votre environnement de test dédié.

![Ingestion des données](./../../../modules/datacollection/module1.2/images/sb1.png)

Accédez à **Destinations**, puis cliquez sur **Parcourir**. Vous verrez alors toutes les destinations disponibles. Recherchez votre destination et cliquez sur les 3 points**...** comme indiqué ci-dessous, puis cliquez sur **Activer les audiences**.

![5-01-select-destination.png](./images/501selectdestination.png)

Vous verrez alors ceci. Recherchez votre audience à l’aide de votre LDAP et sélectionnez `--aepUserLdap-- - Interest in Plans` dans la liste des audiences.

Cliquez sur **Suivant**.

![5-04-select-segment.png](./images/504selectsegment.png)

Cliquez sur **Ajouter un nouveau champ**, cliquez sur Parcourir le schéma et sélectionnez le champ `--aepTenantId--identification.core.ecid` (supprimez tout autre champ qui sera affiché automatiquement).

Cliquez sur **Suivant**.

![5-05-select-attributes.png](./images/505selectattributes.png)

Cliquez sur **Terminer**.

![5-06-destination-finish.png](./images/506destinationfinish.png)

Votre audience est maintenant activée vers votre destination de centre d’événements Microsoft.

![5-07-destination-segment-added.png](./images/507destinationsegmentadded.png)

Étape suivante : [2.4.6 Création de votre projet Azure Microsoft](./ex6.md)

[Revenir au module 2.4](./segment-activation-microsoft-azure-eventhub.md)

[Revenir à tous les modules](./../../../overview.md)
