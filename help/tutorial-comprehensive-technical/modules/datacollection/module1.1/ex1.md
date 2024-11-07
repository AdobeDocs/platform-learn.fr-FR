---
title: Foundation - Configuration de la collecte de données Adobe Experience Platform et de l’extension du SDK Web - Explication de la collecte de données Adobe Experience Platform
description: Foundation - Configuration de la collecte de données Adobe Experience Platform et de l’extension du SDK Web - Explication de la collecte de données Adobe Experience Platform
kt: 5342
doc-type: tutorial
source-git-commit: 7d2f5f842559b2d6d9f115f3993268a4b36a0fe0
workflow-type: tm+mt
source-wordcount: '445'
ht-degree: 3%

---

# 1.1.1 Présentation de la collecte de données Adobe Experience Platform

## Contexte

La collecte de données Adobe Experience Platform est utilisée par les marques pour plusieurs cas d’utilisation. Il s’agit d’un système Tag Management de nouvelle génération (TMS) qui offre aux clients un moyen simple de déployer et de gérer toutes les solutions d’analyse, de marketing et de publicité nécessaires pour proposer des expériences client pertinentes. La collecte de données Adobe Experience Platform n’entraîne aucuns frais supplémentaires et est disponible pour tous les clients Adobe Experience Cloud. Une marque peut utiliser la collecte de données Adobe Experience Platform pour :

- Implémentez des applications Adobe Experience Cloud ainsi que Adobe Experience Platform.
- Gérez les différentes exigences des différentes parties de l’organisation en fournissant à chacune d’elles sa propre **propriété** à gérer.
- Autoriser le test et la gestion du cycle de vie.
- Injectez des balises JavaScript personnalisées et tierces, toutes gérées à un seul endroit.

## Explorer l’interface utilisateur

Accédez à [Adobe Experience Platform Data Collection](https://experience.adobe.com/#/data-collection/).

Accédez à **Balises**. Vous voyez maintenant la vue **[!UICONTROL Propriétés]**. Les propriétés répertoriées ici sont pour la gestion des tutoriels. Ces propriétés représentent...

- Propriétés d’application et web
- Différents sites web qui servent les clients de différentes manières. Par exemple, Luma Retail aurait une propriété, Luma Travel en aurait une autre.
- Anciens et sites web actuels
- Une conception Adobe Analytics spécifique commune à plusieurs sites web différents
- Pages intranet internes et sites externes

![Vue Propriétés du lancement](./images/launch1.png)

Maintenant, regardez le rail de gauche.

![Rail de gauche de lancement](./images/launch2.png)

- **[!UICONTROL Balises]** donne un aperçu de toutes les propriétés côté client.
- **[!UICONTROL App Surfaces]** donne un aperçu de toutes les configurations d’application pour activer les notifications push (qui sont utilisées/activées conjointement avec Project Sierra).
- **[!UICONTROL Les flux de données]** sont explorés dans l’ [exercice suivant](./ex2.md)
- **[!UICONTROL Transfert d’événement]** donne un aperçu de toutes les propriétés côté serveur qui sont explorées dans [Module 14 - Connexions Real-Time CDP : Transfert d’événement](./../../../modules/rtcdp-b2c/module2.5/aep-data-collection-ssf.md)

## Informations supplémentaires

La collecte de données Adobe Experience Platform est un outil très avancé qui a une portée au-delà d’un tutoriel Adobe Experience Platform. Les organisations peuvent ne pas utiliser la collecte de données Adobe Experience Platform pour leurs fonctionnalités de gestion des balises et utiliser à la place des solutions de gestion des balises non-Adobes pour l’injection de code et la gestion des balises. L’utilisation d’une solution de gestion des balises non-Adobe est prise en charge par Adobe et Adobe Professional Services.
Vous trouverez ci-dessous quelques lectures supplémentaires pour ceux qui souhaitent mieux comprendre la collecte de données Adobe Experience Platform.

- [Guide de l’utilisateur de la collecte de données Adobe Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html?lang=fr)
- [Tutoriel sur lʼimplémentation dʼAdobe Experience Cloud à lʼaide du SDK web](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/overview.html?lang=fr)
- [Configuration des autorisations utilisateur](https://experienceleague.adobe.com/docs/experience-platform/tags/admin/user-permissions.html?lang=fr)
- [Documentation des API](https://developer.adobelaunch.com/api/)

Étape suivante : [1.1.2 Edge Network, flux de données et collecte de données côté serveur](./ex2.md)

[Revenir au module 1.1](./data-ingestion-launch-web-sdk.md)

[Revenir à tous les modules](./../../../overview.md)
