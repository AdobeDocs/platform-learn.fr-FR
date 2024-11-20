---
title: Audience Activation à Microsoft Azure Event Hub - Création d’une audience
description: Audience Activation à Microsoft Azure Event Hub - Création d’une audience
kt: 5342
doc-type: tutorial
exl-id: 56f6a6dc-82aa-4b64-a3f6-b6f59c484ccb
source-git-commit: 216914c9d97827afaef90e21ed7d4f35eaef0cd3
workflow-type: tm+mt
source-wordcount: '338'
ht-degree: 2%

---

# 2.4.4 Création d’une audience

## Introduction

Vous allez créer une audience simple :

- **L&#39;intérêt dans les plans** pour lesquels les clients seront éligibles lorsqu&#39;ils visitent la page **Plans** du site web de démonstration CitiSignal.

### Bon à savoir

La plateforme de données clients en temps réel déclenche une activation vers une destination lorsque vous remplissez les critères d’une audience qui fait partie de la liste d’activation de cette destination. Dans ce cas, la charge utile de qualification de l’audience qui sera envoyée à cette destination contiendra **toutes les audiences pour lesquelles votre profil client est admissible**.

L’objectif de ce module est d’indiquer que la qualification de l’audience de votre profil client est envoyée à votre destination Event Hub en temps quasi réel.

### État de l’audience

Une qualification d’audience dans Adobe Experience Platform a toujours une propriété **status** et peut être l’une des suivantes :

- **réalisé** : cela indique une nouvelle qualification d’audience
- **exited** : cela indique que le profil n&#39;est plus admissible pour l&#39;audience

## Création de l’audience

Connectez-vous à Adobe Experience Platform en accédant à cette URL : [https://experience.adobe.com/platform](https://experience.adobe.com/platform).

Une fois connecté, vous accédez à la page d’accueil de Adobe Experience Platform.

![Ingestion des données](./../../../modules/datacollection/module1.2/images/home.png)

Avant de continuer, vous devez sélectionner un **sandbox**. L’environnement de test à sélectionner est nommé ``--aepSandboxName--``. Après avoir sélectionné l’environnement de test approprié, l’écran change et vous êtes désormais dans votre environnement de test dédié.

![Ingestion des données](./../../../modules/datacollection/module1.2/images/sb1.png)

Accédez à **Audiences**. Cliquez sur le bouton **+ Créer une audience** .

![Ingestion des données](./images/seg.png)

Sélectionnez **Créer la règle** et cliquez sur **Créer**.

![Ingestion des données](./images/seg1.png)

Nommez votre audience `--aepUserLdap-- - Interest in Plans`, définissez la méthode d’évaluation sur **Edge** et ajoutez le nom de page de l’événement d’expérience.

Cliquez sur **Événements**, puis effectuez un glisser-déposer de **XDM ExperienceEvent > Web > Détails de la page Web > Nom**. Saisissez **plans** comme valeur :

![4-05-create-ee-2.png](./images/405createee2.png)

Effectuez un glisser-déposer de **XDM ExperienceEvent > `--aepTenantId--` > demoEnvironment > brandName**. Saisissez `--aepUserLdap--` comme valeur, définissez le paramètre de comparaison sur **contains** et cliquez sur **Publish** :

![4-05-create-ee-2-brand.png](./images/405createee2brand.png)

Votre audience est maintenant publiée.

![4-05-create-ee-2-brand.png](./images/405createee2brand1.png)

Étape suivante : [2.4.5 Activation de votre audience](./ex5.md)

[Revenir au module 2.4](./segment-activation-microsoft-azure-eventhub.md)

[Revenir à tous les modules](./../../../overview.md)
