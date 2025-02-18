---
title: Audience Activation vers Microsoft Azure Event Hub - Activer l’audience
description: Audience Activation vers Microsoft Azure Event Hub - Activer l’audience
kt: 5342
doc-type: tutorial
exl-id: e6bac0ce-4a1e-4458-af3e-3d6ac40b9cb5
source-git-commit: 3d61d91111d8693ab031fbd7b26706c02818108c
workflow-type: tm+mt
source-wordcount: '225'
ht-degree: 5%

---

# 2.4.5 Activer votre audience

## Ajouter une audience à la destination Azure Event Hub

Dans cet exercice, vous allez ajouter votre audience `--aepUserLdap-- - Interest in Plans` à votre destination Azure Event Hub `--aepUserLdap---aep-enablement`.

Connectez-vous à Adobe Experience Platform en accédant à cette URL : [https://experience.adobe.com/platform](https://experience.adobe.com/platform).

Une fois connecté, vous accédez à la page d’accueil de Adobe Experience Platform.

![Ingestion des données](./../../../../modules/delivery-activation/datacollection/dc1.2/images/home.png)

Avant de continuer, vous devez sélectionner un **sandbox**. Le sandbox à sélectionner est nommé ``--aepSandboxName--``. Après avoir sélectionné la sandbox appropriée, la modification d’écran s’affiche et vous êtes maintenant dans votre sandbox dédiée.

![Ingestion des données](./../../../../modules/delivery-activation/datacollection/dc1.2/images/sb1.png)

Accédez à **Destinations**, puis cliquez sur **Parcourir**. Vous verrez alors toutes les destinations disponibles. Localisez votre destination et cliquez sur les 3 points**...** comme indiqué ci-dessous, puis cliquez sur **Activer les audiences**.

![5-01-select-destination.png](./images/501selectdestination.png)

Tu verras ça. Recherchez votre audience à l’aide de votre ldap et sélectionnez `--aepUserLdap-- - Interest in Plans` dans la liste des audiences.

Cliquez sur **Suivant**.

![5-04-select-segment.png](./images/504selectsegment.png)

Cliquez sur **Ajouter un nouveau champ**, cliquez sur Parcourir le schéma et sélectionnez le `--aepTenantId--identification.core.ecid` du champ (supprimez tout autre champ qui s’afficherait automatiquement).

Cliquez sur **Suivant**.

![5-05-select-attributes.png](./images/505selectattributes.png)

Cliquez sur **Terminer**.

![5-06-destination-finish.png](./images/506destinationfinish.png)

Votre audience est maintenant activée vers votre destination Microsoft Event Hub .

![5-07-destination-segment-added.png](./images/507destinationsegmentadded.png)

## Étapes suivantes

Accédez à [2.4.6 Création de votre projet Microsoft Azure](./ex6.md){target="_blank"}

Revenez à [Real-Time CDP : Audience Activation vers Microsoft Azure Event Hub](./segment-activation-microsoft-azure-eventhub.md){target="_blank"}

Revenir à [Tous les modules](./../../../../overview.md){target="_blank"}
