---
title: Activation de segment vers Microsoft Azure Event Hub - Activation de segment
description: Activation de segment vers Microsoft Azure Event Hub - Activation de segment
kt: 5342
audience: Data Engineer, Data Architect, Data Analyst
doc-type: tutorial
activity: develop
exl-id: 250f8536-b6bd-4c64-a552-80d5c6fb6358
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '340'
ht-degree: 3%

---

# 13.4 Activation du segment

## 13.4.1 Ajout d’un segment à la destination Azure Event Hub

Dans cet exercice, vous allez ajouter votre segment. `--demoProfileLdap-- - Interest in Equipment` à `--demoProfileLdap---aep-enablement` Destination Azure Event Hub.

Connectez-vous à Adobe Experience Platform en accédant à cette URL : [https://experience.adobe.com/platform](https://experience.adobe.com/platform).

Une fois connecté, vous accédez à la page d’accueil de Adobe Experience Platform.

![Ingestion des données](../module2/images/home.png)

Avant de continuer, vous devez sélectionner une **sandbox**. L’environnement de test à sélectionner est nommé ``--aepSandboxId--``. Pour ce faire, cliquez sur le texte **[!UICONTROL Production Prod]** dans la ligne bleue en haut de votre écran. Après avoir sélectionné l’environnement de test approprié, l’écran change et vous êtes désormais dans votre environnement de test dédié.

![Ingestion des données](../module2/images/sb1.png)

Accédez à **Destinations**, puis cliquez sur **Parcourir**. Vous verrez alors toutes les destinations disponibles. Recherchez votre destination et cliquez sur le bouton **+** comme indiqué ci-dessous.

![5-01-select-destination.png](./images/5-01-select-destination.png)

Vous verrez alors ceci. Recherchez votre segment à l’aide de votre LDAP et sélectionnez `--demoProfileLdap-- - Interest in Equipment` dans la liste des segments.

Cliquez sur **Suivant**.

![5-04-select-segment.png](./images/5-04-select-segment.png)

La plateforme de données clients en temps réel de Adobe Experience Platform peut fournir une charge utile à deux types de destinations, des destinations de segment et des destinations de profil.

Les destinations de segment recevront une charge utile de qualification de segment prédéfinie qui sera discutée ultérieurement. Ce payload contient **all** les qualifications de segment pour un profil spécifique. Même pour les segments qui ne figurent pas dans la liste d’activation de la destination. Voici un exemple de destination de segment : **Centre d’événements Azure** et **AWS Kinesis**.

Les destinations basées sur un profil vous permettent de sélectionner n’importe quel attribut (firstName, lastName, etc.) du schéma d’union XDM Profile et de l’inclure dans la payload d’activation. Voici un exemple de destination : **Marketing par e-mail**.

Parce que votre destination Azure Event Hub est une **segment** destination, sélectionnez par exemple le champ `--aepTenantId--.identification.core.ecid`.

Cliquez sur **Ajouter un nouveau champ**, cliquez sur parcourir le schéma et sélectionnez le champ `--aepTenantId--identification.core.ecid` (supprimez tout autre champ qui s’afficherait automatiquement).

Cliquez sur **Suivant**.

![5-05-select-attributes.png](./images/5-05-select-attributes.png)

Cliquez sur **Terminer**.

![5-06-destination-finish.png](./images/5-06-destination-finish.png)

Votre segment est maintenant activé vers votre destination de centre d’événements Microsoft.

![5-07-destination-segment-added.png](./images/5-07-destination-segment-added.png)

Étape suivante : [13.5 Création de votre projet Microsoft Azure](./ex5.md)

[Revenir au module 13](./segment-activation-microsoft-azure-eventhub.md)

[Revenir à tous les modules](./../../overview.md)
