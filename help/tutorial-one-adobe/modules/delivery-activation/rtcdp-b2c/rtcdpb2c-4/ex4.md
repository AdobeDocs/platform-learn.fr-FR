---
title: Audience Activation vers Microsoft Azure Event Hub - Création d’une audience
description: Audience Activation vers Microsoft Azure Event Hub - Création d’une audience
kt: 5342
doc-type: tutorial
exl-id: d9450e18-7c9b-4a6c-8317-19baf99d43a3
source-git-commit: 3d61d91111d8693ab031fbd7b26706c02818108c
workflow-type: tm+mt
source-wordcount: '347'
ht-degree: 3%

---

# 2.4.4 Création d’une audience

## Introduction

Vous allez créer une audience simple :

- **Intérêt pour les plans** pour lesquels les clients se qualifieront lorsqu’ils visiteront la page **Plans** du site web de démonstration de CitiSignal.

### Bon à savoir

Real-Time CDP déclenche une activation vers une destination lorsque vous remplissez les critères d’une audience qui fait partie de la liste d’activation de cette destination. Lorsque c’est le cas, la payload de qualification d’audience qui sera envoyée à cette destination contiendra **toutes les audiences pour lesquelles votre profil client se qualifie**.

L’objectif de ce module est de montrer que la qualification de l’audience de votre profil client est envoyée à votre destination Event Hub en temps quasi réel.

### Statut de l’audience

Une qualification d’audience dans Adobe Experience Platform a toujours une **status**-propriété et peut être l’une des suivantes :

- **réalisé** : indique une nouvelle qualification d’audience
- **sorti** : cela indique que le profil n’est plus éligible à l’audience

## Créer l’audience

Connectez-vous à Adobe Experience Platform en accédant à cette URL : [https://experience.adobe.com/platform](https://experience.adobe.com/platform).

Une fois connecté, vous accédez à la page d’accueil de Adobe Experience Platform.

![Ingestion des données](./../../../../modules/delivery-activation/datacollection/dc1.2/images/home.png)

Avant de continuer, vous devez sélectionner un **sandbox**. Le sandbox à sélectionner est nommé ``--aepSandboxName--``. Après avoir sélectionné la sandbox appropriée, la modification d’écran s’affiche et vous êtes maintenant dans votre sandbox dédiée.

![Ingestion des données](./../../../../modules/delivery-activation/datacollection/dc1.2/images/sb1.png)

Accédez à **Audiences**. Cliquez sur le bouton **+ Créer une audience**.

![Ingestion des données](./images/seg.png)

Sélectionnez **Créer une règle** puis cliquez sur **Créer**.

![Ingestion des données](./images/seg1.png)

Nommez votre audience `--aepUserLdap-- - Interest in Plans`, définissez la méthode d’évaluation sur **Edge** puis ajoutez le nom de la page à partir de l’événement d’expérience.

Cliquez sur **Événements**, puis effectuez un glisser-déposer **XDM ExperienceEvent > Web > Détails de la page web > Nom**. Saisissez **plans** comme valeur :

![4-05-create-ee-2.png](./images/405createee2.png)

Effectuez un glisser-déposer **XDM ExperienceEvent > `--aepTenantId--` > demoEnvironment > brandName**. Saisissez `--aepUserLdap--` comme valeur, définissez le paramètre de comparaison sur **contient** puis cliquez sur **Publier** :

![4-05-create-ee-2-brand.png](./images/405createee2brand.png)

Votre audience est maintenant publiée.

![4-05-create-ee-2-brand.png](./images/405createee2brand1.png)

## Étapes suivantes

Accédez à [2.4.5 Activer votre audience](./ex5.md){target="_blank"}

Revenez à [Real-Time CDP : Audience Activation vers Microsoft Azure Event Hub](./segment-activation-microsoft-azure-eventhub.md){target="_blank"}

Revenir à [Tous les modules](./../../../../overview.md){target="_blank"}
