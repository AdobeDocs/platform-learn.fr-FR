---
title: Activation de segment vers Microsoft Azure Event Hub - Activation de segment
description: Activation de segment vers Microsoft Azure Event Hub - Activation de segment
kt: 5342
doc-type: tutorial
source-git-commit: 6962a0d37d375e751a05ae99b4f433b0283835d0
workflow-type: tm+mt
source-wordcount: '347'
ht-degree: 2%

---

# 2.4.4 Activation du segment

## 2.4.4.1 Ajout d’un segment à la destination Azure Event Hub

Dans cet exercice, vous allez ajouter votre segment `--aepUserLdap-- - Interest in Equipment` à votre destination `--aepUserLdap---aep-enablement` Azure Event Hub.

Connectez-vous à Adobe Experience Platform en accédant à cette URL : [https://experience.adobe.com/platform](https://experience.adobe.com/platform).

Une fois connecté, vous accédez à la page d’accueil de Adobe Experience Platform.

![Ingestion des données](./../../../modules/datacollection/module1.2/images/home.png)

Avant de continuer, vous devez sélectionner un **sandbox**. L’environnement de test à sélectionner est nommé ``--aepSandboxName--``. Pour ce faire, cliquez sur le texte **[!UICONTROL Production Prod]** dans la ligne bleue en haut de votre écran. Après avoir sélectionné l’environnement de test approprié, l’écran change et vous êtes désormais dans votre environnement de test dédié.

![Ingestion des données](./../../../modules/datacollection/module1.2/images/sb1.png)

Accédez à **Destinations**, puis cliquez sur **Parcourir**. Vous verrez alors toutes les destinations disponibles. Recherchez votre destination et cliquez sur l’icône **+** comme indiqué ci-dessous.

![5-01-select-destination.png](./images/5-01-select-destination.png)

Vous verrez alors ceci. Recherchez votre segment à l’aide de votre LDAP et sélectionnez `--aepUserLdap-- - Interest in Equipment` dans la liste de segments.

Cliquez sur **Suivant**.

![5-04-select-segment.png](./images/5-04-select-segment.png)

La plateforme de données clients en temps réel de Adobe Experience Platform peut fournir une charge utile à deux types de destinations, des destinations de segment et des destinations de profil.

Les destinations de segment recevront une charge utile de qualification de segment prédéfinie qui sera discutée ultérieurement. Un tel payload contient **tous** les qualifications de segment pour un profil spécifique. Même pour les segments qui ne figurent pas dans la liste d’activation de la destination. **Azure Event Hubs** et **AWS Kinesis** sont un exemple de destination de segment de ce type.

Les destinations basées sur un profil vous permettent de sélectionner n’importe quel attribut (firstName, lastName, etc.) du schéma d’union XDM Profile et de l’inclure dans la payload d’activation. **Marketing par e-mail** est un exemple de destination de ce type.

Comme votre destination Azure Event Hub est une destination **segment**, sélectionnez par exemple le champ `--aepTenantId--.identification.core.ecid`.

Cliquez sur **Ajouter un nouveau champ**, cliquez sur Parcourir le schéma et sélectionnez le champ `--aepTenantId--identification.core.ecid` (supprimez tout autre champ qui sera affiché automatiquement).

Cliquez sur **Suivant**.

![5-05-select-attributes.png](./images/5-05-select-attributes.png)

Cliquez sur **Terminer**.

![5-06-destination-finish.png](./images/5-06-destination-finish.png)

Votre segment est maintenant activé vers votre destination de centre d’événements Microsoft.

![5-07-destination-segment-added.png](./images/5-07-destination-segment-added.png)

Étape suivante : [2.4.5 Création de votre projet Azure Microsoft](./ex5.md)

[Revenir au module 2.4](./segment-activation-microsoft-azure-eventhub.md)

[Revenir à tous les modules](./../../../overview.md)
