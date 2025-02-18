---
title: 1.1 Configuration de la collecte de données Adobe Experience Platform et de l’extension Web SDK
description: Foundation - Configuration de la collecte de données Adobe Experience Platform et de l’extension Web SDK
kt: 5342
doc-type: tutorial
exl-id: 8c613648-9007-49fb-898f-039c366297da
source-git-commit: 3d61d91111d8693ab031fbd7b26706c02818108c
workflow-type: tm+mt
source-wordcount: '590'
ht-degree: 1%

---

# 1.1 Configuration de la collecte de données Adobe Experience Platform et de l’extension de balise Web SDK

Ce module fondamental vous présente la vision de la collecte de données d’Adobe et explique comment obtenir des données d’un site web et d’une application mobile dans Adobe Experience Platform et d’autres applications via la collecte de données Adobe Experience Platform, les SDK Adobe Experience Platform et Adobe Experience Platform Edge Network.

Ce module présente certains concepts et technologies qui ont un impact au-delà de la portée d’un tutoriel technique Adobe Experience Platform. Vous devriez savoir clairement quelles parties de ces exercices sont fondamentales pour la suite du tutoriel complet, qui vous en apprendra plus sur Edge Network et ses fonctionnalités, et où aller pour obtenir plus d’informations et de tutoriels.

## Objectifs d’apprentissage

- Découvrez comment une marque utilise la collecte de données Adobe Experience Platform comme système Tag Management (TMS).
- Découvrez les flux de données utilisés par une marque pour ingérer des données dans ses produits Adobe.
- Découvrez comment envoyer des données au Adobe Experience Platform et à d’autres produits via Adobe Experience Platform Edge Network.
- Découvrez comment créer des éléments de données et des règles qui collectent des données sur le Web et les appareils mobiles.
- Découvrez les événements de tracking [Web SDK](https://experienceleague.adobe.com/fr/docs/experience-platform/web-sdk/home) et comment déboguer leur contenu.
- Découvrez ce qu’est une couche de données et ce qu’Adobe recommande lors de son implémentation.
- Découvrez les étapes à suivre pour implémenter [Web SDK](https://experienceleague.adobe.com/fr/docs/experience-platform/web-sdk/home) à partir de zéro.
- Découvrez la différence entre une implémentation web et mobile.

## Conditions préalables

- Accès à Adobe Experience Platform : [https://experience.adobe.com/platform](https://experience.adobe.com/platform)
- Accès à la collecte de données Adobe Experience Platform : [https://experience.adobe.com/#/data-collection/](https://experience.adobe.com/#/data-collection/)
- Accès au site web de démonstration

>[!NOTE]
>
>N’oubliez pas d’installer, de configurer et d’utiliser l’extension Chrome, comme indiqué dans [Installation de l’extension Chrome pour la documentation Experience League](../../../getting-started/gettingstarted/ex1.md)

## Exercices

[1.1.1 Comprendre la collecte de données Adobe Experience Platform](./ex1.md)

Dans cet exercice, explorez l’interface utilisateur de la collecte de données Adobe Experience Platform et découvrez ses fonctionnalités.

[1.1.2 Edge Network, flux de données et collecte de données côté serveur](./ex2.md)

Dans cet exercice, vous apprendrez à transférer des données vers les produits Adobe dans l’interface de collecte de données de Adobe Experience Platform et à étudier les flux de données utilisés par le site web de démonstration.

[1.1.3 Présentation de la collecte de données Adobe Experience Platform](./ex3.md)

Dans cet exercice, vous apprendrez à configurer une extension, à créer des éléments de données et des règles, puis à les publier sur le web.

[1.1.4 Collecte de données web côté client](./ex4.md)

Dans cet exercice, déboguez le SDK Web qui a été installé pour en comprendre le fonctionnement et les données qui seront utilisées dans les exercices futurs.

[1.1.5 Mise en œuvre d’Adobe Analytics et de Adobe Audience Manager](./ex5.md)

Dans cet exercice, consultez et utilisez les données web collectées avec le SDK Web dans Adobe Analytics et Adobe Audience Manager.

[1.1.6 Mise en œuvre d’Adobe Target](./ex6.md)

Dans cet exercice, configurez une activité dans Adobe Target, implémentée via le SDK Web.

[1.1.7 Exigences relatives aux schémas XDM dans Adobe Experience Platform](./ex7.md)

Pour que le SDK Web puisse ingérer des données dans Adobe Experience Platform, un mixin XDM spécifique doit faire partie du schéma XDM dans Adobe Experience Platform.

[Résumé et avantages](./summary.md)

Résumé de ce module et aperçu des avantages.

![Insiders de la technologie ](./../../../../assets/images/techinsiders.png){width="50px" align="left"}

>[!NOTE]
>
>Merci d’avoir consacré votre temps à apprendre tout ce qu’il y a à savoir sur Adobe Experience Platform et ses applications. Si vous avez des questions, si vous souhaitez partager des commentaires généraux ou si vous avez des suggestions sur le contenu futur, veuillez contacter directement les initiés techniques, en envoyant un e-mail à **techinsiders@adobe.com**.

[Revenir à tous les modules](./../../../../overview.md)
