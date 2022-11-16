---
title: Tutoriel sur lʼimplémentation dʼAdobe Experience Cloud à lʼaide du SDK web
description: Découvrez comment implémenter des applications Experience Cloud à l’aide du SDK web d’Adobe Experience Platform.
recommendations: catalog, noDisplay
exl-id: cf0ff74b-e81e-4f6d-ab7d-6c70e9b52d78
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '386'
ht-degree: 27%

---

# Tutoriel sur lʼimplémentation dʼAdobe Experience Cloud à lʼaide du SDK web

Découvrez comment implémenter des applications Experience Cloud à l’aide du SDK web d’Adobe Experience Platform.

Experience Platform Web SDK est une bibliothèque JavaScript côté client qui permet aux clients de Adobe Experience Cloud d’interagir avec les applications Adobe et les services tiers via Adobe Experience Platform Edge Network. Voir [Présentation du SDK Web Adobe Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/edge/home.html?lang=fr) pour plus d’informations.

Ce tutoriel vous guide tout au long de l’implémentation du SDK Web de Platform sur un exemple de site web de vente au détail appelé Luma. Le site [](https://luma.enablementadobe.com/content/luma/us/en.html)Luma possède une couche de données et des fonctionnalités riches qui vous permettent dʼeffectuer une implémentation réaliste. Après avoir terminé ce tutoriel, vous devriez être prêt à commencer à mettre en oeuvre toutes vos solutions marketing par le biais du SDK Web Platform sur votre propre site web.

[![Site web Luma](assets/old-overview-luma.png)](https://luma.enablementadobe.com/content/luma/us/en.html)


## Objectifs d&#39;apprentissage

Après avoir terminé le tutoriel, vous pourrez :

* Configurer les flux de données

* Création de schémas XDM

* Ajoutez les applications Adobe Experience Cloud suivantes :
   * **[Adobe Experience Platform](setup-experience-platform.md)** (et les applications créées sur Platform telles qu’Adobe Real-time Customer Data Platform, Adobe Journey Optimizer et Adobe Customer Journey Analytics)
   * **[Adobe Analytics](setup-analytics.md)**
   * **[Adobe Audience Manager](setup-audience-manager.md)**
   * **[Adobe Target](setup-target.md)**

* Création de règles de balise et d’éléments de données d’objet XDM pour envoyer des données aux applications Adobe

* Validation de la mise en oeuvre à l’aide du débogueur Adobe Experience Platform

* Capture du consentement de l’utilisateur

* Transfert de données vers des tiers avec transfert d’événement

>[!NOTE]
>
>Un tutoriel multisolution similaire est disponible pour [SDK Mobile](../tutorial-mobile-sdk/overview.md).

## Conditions préalables

Dans ces leçons, on suppose que vous disposez d’une Adobe ID et d’une [autorisations requises](configure-permissions.md) pour terminer les leçons. Dans le cas contraire, vous devez contacter votre administrateur Experience Cloud pour demander l’accès.

En outre, vous êtes censé connaitre les langages de développement d’interfaces tels que HTML et JavaScript. Vous n’avez pas besoin d’être un expert dans ces langues, mais ce tutoriel vous permet de mieux comprendre et lire le code.

C’est parti !

[Suivant : ](configure-permissions.md)

>[!NOTE]
>
>Merci d’avoir consacré du temps à l’apprentissage du SDK Web Adobe Experience Platform. Si vous avez des questions, souhaitez partager des commentaires généraux ou avez des suggestions sur le contenu futur, partagez-les à ce sujet. [Article de discussion de la communauté Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996)
