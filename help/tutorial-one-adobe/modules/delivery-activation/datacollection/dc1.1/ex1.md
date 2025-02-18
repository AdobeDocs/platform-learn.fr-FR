---
title: Foundation - Configuration de la collecte de données Adobe Experience Platform et de l’extension Web SDK - Explication de la collecte de données Adobe Experience Platform
description: Foundation - Configuration de la collecte de données Adobe Experience Platform et de l’extension Web SDK - Explication de la collecte de données Adobe Experience Platform
kt: 5342
doc-type: tutorial
exl-id: 1f5dd730-d84a-4d3a-b5ef-2be3e089c7fd
source-git-commit: 3d61d91111d8693ab031fbd7b26706c02818108c
workflow-type: tm+mt
source-wordcount: '517'
ht-degree: 3%

---

# 1.1.1 Comprendre la collecte de données Adobe Experience Platform

## Contexte

Les marques utilisent la collecte de données Adobe Experience Platform pour un certain nombre de cas d’utilisation. Il s’agit d’un système Tag Management de nouvelle génération (TMS) qui offre aux clients un moyen simple de déployer et de gérer toutes les solutions d’analyse, de marketing et de publicité nécessaires pour offrir des expériences client pertinentes. La collecte de données Adobe Experience Platform n’entraîne aucun frais supplémentaire et est disponible pour tout client Adobe Experience Cloud. Une marque peut utiliser la collecte de données Adobe Experience Platform pour :

- Mettez en œuvre des applications Adobe Experience Cloud ainsi que Adobe Experience Platform.
- Gérez les différentes exigences des différentes parties de l’organisation en fournissant à chacune d’elles ses propres **Propriétés** à gérer.
- Permet les tests et la gestion du cycle de vie.
- Injectez des balises JavaScript et tierces personnalisées, toutes gérées en un seul endroit.

## Explorer l’interface utilisateur

Accédez à [Collecte de données Adobe Experience Platform](https://experience.adobe.com/#/data-collection/).

Accédez à **Balises**. La vue **[!UICONTROL Propriétés]** s’affiche maintenant. Les propriétés répertoriées ici servent à la gestion de tutoriels. Ces propriétés représentent :

- Propriétés d’application et web
- Différents sites web qui proposent des services aux clients de différentes manières. Par exemple, Luma Retail aurait une propriété, Luma Travel en aurait une autre.
- Sites web hérités et actuels
- Une conception Adobe Analytics spécifique commune à plusieurs sites web différents
- Pages intranet internes à côté de sites externes

![Vue Propriétés de Launch](./images/launch1.png)

Maintenant, regardez le rail de gauche.

![Lancer le rail de gauche](./images/launch2.png)

- **[!UICONTROL Balises]** donne un aperçu de toutes les propriétés côté client
- **[!UICONTROL Surfaces d’application]** donne un aperçu de toutes les configurations d’application pour activer les notifications push (qui est utilisée/activée en combinaison avec Project Sierra).
- Les **[!UICONTROL flux de données]** sont détaillés dans l’exercice [suivant](./ex2.md)
- **[!UICONTROL Transfert d’événement]** donne un aperçu de toutes les propriétés côté serveur qui sont explorées dans [Module 2.5 - Connexions Real-Time CDP : transfert d’événement](./../../../../modules/delivery-activation/rtcdp-b2c/rtcdpb2c-5/aep-data-collection-ssf.md)
- La section **[!UICONTROL Surveillance]** donne un aperçu du trafic d’événement entrant et sortant via le transfert d’événement
- **[!UICONTROL Assurance]** permet d’accéder au débogage d’une implémentation à l’aide d’Adobe Debugger
- **[!UICONTROL Places]** permet d’accéder à la gestion des points d’intérêt qui deviennent accessibles pour la personnalisation basée sur l’emplacement dans les applications mobiles
- **[!UICONTROL Schémas]** permet d’accéder à l’éditeur de schémas de Adobe Experience Platform
- **[!UICONTROL Identités]** permet d’accéder à la configuration du graphique d’identités Adobe Experience Platform

## Informations supplémentaires

La collecte de données Adobe Experience Platform est un outil très avancé qui a une portée dépassant le tutoriel de Adobe Experience Platform. Les entreprises peuvent ne pas utiliser la collecte de données Adobe Experience Platform pour ses fonctionnalités de gestion des balises et utiliser plutôt des solutions de gestion des balises autres qu’Adobe pour injecter du code et gérer les balises. L’utilisation d’une solution de gestion des balises non Adobe est prise en charge par Adobe et Adobe Professional Services.
Vous trouverez ci-dessous quelques informations supplémentaires pour ceux qui souhaitent en savoir plus sur la collecte de données Adobe Experience Platform.

- [Guide De L’Utilisateur De La Collecte De Données Adobe Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html?lang=fr)
- [Tutoriel sur lʼimplémentation dʼAdobe Experience Cloud à lʼaide du SDK web](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/overview.html?lang=fr)
- [Configurer les autorisations utilisateur](https://experienceleague.adobe.com/docs/experience-platform/tags/admin/user-permissions.html?lang=fr)
- [Documentation des API](https://developer.adobelaunch.com/api/)

## Étapes suivantes

Accédez à [1.1.2 Edge Network, flux de données et collecte de données côté serveur](./ex2.md){target="_blank"}

Revenez à [Configuration de la collecte de données Adobe Experience Platform et de l’extension de balise Web SDK](./data-ingestion-launch-web-sdk.md){target="_blank"}

Revenir à [Tous les modules](./../../../../overview.md){target="_blank"}
