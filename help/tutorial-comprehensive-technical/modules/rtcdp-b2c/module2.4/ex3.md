---
title: Activation des segments vers Microsoft Azure Event Hub - Créer un segment en flux continu
description: Activation des segments vers Microsoft Azure Event Hub - Créer un segment en flux continu
kt: 5342
doc-type: tutorial
source-git-commit: 7d2f5f842559b2d6d9f115f3993268a4b36a0fe0
workflow-type: tm+mt
source-wordcount: '363'
ht-degree: 2%

---

# 2.4.3 Création d’un segment

## 2.4.3.1 Introduction

Vous allez créer un segment simple :

- **Centre d’intérêt pour l’équipement** dont les profils clients seront admissibles lorsqu’ils visitent la page **Matériel** du site web de démonstration de Luma.

### Bon à savoir

La plateforme des données clients en temps réel déclenche une activation vers une destination lorsque vous êtes admissible pour un segment qui fait partie de la liste d’activation de cette destination. Dans ce cas, la charge utile de qualification de segment qui sera envoyée à cette destination contiendra **tous les segments pour lesquels votre profil est admissible**.

L’objectif de ce module est de montrer que la qualification de segment de votre profil client est envoyée en temps réel à la destination **votre centre d’événements**.

### État du segment

Une qualification de segment dans Adobe Experience Platform a toujours une propriété **status** et peut être l’une des suivantes :

- **réalisé** : cela indique une nouvelle qualification de segment
- **existing** : cela indique une qualification de segment existante
- **exited** : cela indique que le profil n’est plus admissible pour le segment

## 2.4.3.2 Création du segment

La création d’un segment est expliquée en détail dans le [module 2.3](./../../../modules/rtcdp-b2c/module2.3/real-time-cdp-build-a-segment-take-action.md).

### Créer un segment

Connectez-vous à Adobe Experience Platform en accédant à cette URL : [https://experience.adobe.com/platform](https://experience.adobe.com/platform).

Une fois connecté, vous accédez à la page d’accueil de Adobe Experience Platform.

![Ingestion des données](./../../../modules/datacollection/module1.2/images/home.png)

Avant de continuer, vous devez sélectionner un **sandbox**. L’environnement de test à sélectionner est nommé ``--aepSandboxId--``. Pour ce faire, cliquez sur le texte **[!UICONTROL Production Prod]** dans la ligne bleue en haut de votre écran. Après avoir sélectionné l’environnement de test approprié, l’écran change et vous êtes désormais dans votre environnement de test dédié.

![Ingestion des données](./../../../modules/datacollection/module1.2/images/sb1.png)

Accédez à **Segments**. Cliquez sur le bouton **+ Créer un segment** .

![Ingestion des données](./images/seg.png)

Nommez votre segment `--demoProfileLdap-- - Interest in Equipment` et ajoutez l’événement d’expérience du nom de page :

Cliquez sur **Événements**, puis effectuez un glisser-déposer de **XDM ExperienceEvent > Web > Détails de la page Web > Nom**. Saisissez la valeur **device** :

![4-05-create-ee-2.png](./images/4-05-create-ee-2.png)

Effectuez un glisser-déposer de **XDM ExperienceEvent > `--aepTenantIdSchema--` > demoEnvironment > brandName**. Saisissez `--demoProfileLdap--` comme valeur, définissez le paramètre de comparaison sur **contains** et cliquez sur **Enregistrer** :

![4-05-create-ee-2-brand.png](./images/4-05-create-ee-2-brand.png)

### Définition PQL

Le PQL de votre segment ressemble à ce qui suit :

```code
CHAIN(xEvent, timestamp, [C0: WHAT(web.webPageDetails.name.equals("equipment", false) and _experienceplatform.demoEnvironment.brandName.contains("--demoProfileLdap--", false))])
```

Étape suivante : [2.4.4 Activation du segment](./ex4.md)

[Revenir au module 2.4](./segment-activation-microsoft-azure-eventhub.md)

[Revenir à tous les modules](./../../../overview.md)
