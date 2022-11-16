---
title: 'CDP en temps réel : créez un segment et prenez des mesures.'
description: 'CDP en temps réel : créez un segment et prenez des mesures.'
kt: 5342
audience: Data Architect, Orchestration Engineer, Marketer
doc-type: tutorial
activity: develop
exl-id: 147d9153-5742-4857-aae1-0ec434a1e626
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '454'
ht-degree: 2%

---

# 6. CDP en temps réel : créez un segment et prenez des mesures.

**Auteur : [Wouter Van Geluwe](https://www.linkedin.com/in/woutervangeluwe/), [Alberto De Caro](https://www.linkedin.com/in/albertodecaro/), [Benedikt Wedenik](https://www.linkedin.com/in/benedikt-wedenik/)**

Dans ce module, vous allez configurer un segment en continu et activer le segment vers plusieurs destinations.

## Objectifs d’apprentissage

- Découvrez comment créer un segment et l’activer pour la diffusion en continu.
- Découvrez comment configurer une destination publicitaire à l’aide de l’interface utilisateur de Adobe Experience Platform.
- Découvrez comment connecter un segment à une destination et l’activer.
- Découvrez comment utiliser les segments Adobe Experience Platform dans Adobe Audience Manager et comment utiliser les segments Adobe Audience Manager dans Adobe Experience Platform, grâce au partage bidirectionnel de segments.

## Conditions préalables

- Accès à Adobe Experience Platform : [https://experience.adobe.com/platform](https://experience.adobe.com/platform)
- Accès à Adobe Target
- Accès à AWS S3

>[!IMPORTANT]
>
>Ce tutoriel a été créé pour faciliter un format d’atelier particulier. Il utilise des systèmes et des comptes spécifiques auxquels vous n’avez peut-être pas accès. Même sans accès, nous pensons que vous pouvez encore apprendre beaucoup en lisant à travers ce contenu très détaillé. Si vous participez à l’un des ateliers et que vous avez besoin de vos informations d’identification d’accès, veuillez contacter votre représentant d’Adobe qui vous fournira les informations requises.

## Aperçu de l’architecture

Regardez l’architecture ci-dessous, qui met en évidence les composants qui seront discutés et utilisés dans ce module.

![Aperçu de l’architecture](../../assets/images/architecturem11.png)

## Environnement de test à utiliser

Pour ce module, utilisez cet environnement de test : `--module11sandbox--`.

>[!NOTE]
>
>N’oubliez pas d’installer, de configurer et d’utiliser l’extension Chrome comme référencé dans [0.1 - Installation de l’extension Chrome pour la documentation Experience League](../module0/ex1.md)

## Exercices

[6.1 Création d’un segment](./ex1.md)

Découvrez comment créer un segment.

[6.2 Découvrez comment configurer une destination DV360 à l’aide de destinations](./ex2.md)

Découvrez comment configurer une destination publicitaire à l’aide de l’interface utilisateur de Real-Time CDP.

[6.3 Agir : envoyer votre segment à DV360 ;](./ex3.md)

Connectez le segment que vous avez créé dans l’exercice 6.1 au DV360 de destination.

[6.4 Agir : envoyer votre segment à une destination S3 ;](./ex4.md)

Utilisez le segment que vous avez créé dans l’exercice 6.1 et envoyez-le à une destination S3, généralement utilisée pour les destinations de marketing par e-mail.

[6.5 Agir : envoyer votre segment à Adobe Target ;](./ex5.md)

Utilisez le segment que vous avez créé dans l’exercice 6.1 pour configurer une activité de ciblage d’expérience dans Adobe Target.

[6.6 Audiences externes](./ex6.md)

Importation d’audiences d’un système source externe dans Adobe Experience Platform.

[SDK de destinations 6.7](./ex7.md)

Configurez votre propre destination à l’aide du SDK Destinations .

[Résumé et avantages](./summary.md)

Résumé de ce module et aperçu des avantages.

>[!NOTE]
>
>Merci d&#39;investir votre temps dans l&#39;apprentissage de Adobe Experience Platform. Si vous avez des questions, souhaitez partager les commentaires généraux d&#39;avoir des suggestions sur le contenu futur, contactez directement Wouter Van Geluwe en envoyant un email à **vangeluw@adobe.com**.

[Revenir à tous les modules](../../overview.md)
