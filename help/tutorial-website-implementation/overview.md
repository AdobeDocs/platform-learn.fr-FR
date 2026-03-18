---
title: Implémentation d’Experience Cloud dans les sites web à l’aide de balises
description: Implémenter Experience Cloud dans les sites web avec des balises constitue le point de départ idéal pour les développeurs front-end ou les spécialistes du marketing technique qui souhaitent apprendre à mettre en œuvre les solutions Adobe Experience Cloud sur leur site web.
recommendations: catalog, noDisplay
exl-id: 1b95f0b2-3062-49d1-9b0b-e6824a54008f
source-git-commit: 935b8d18b6aef506fc5f48c64331803fe8a7ea9e
workflow-type: tm+mt
source-wordcount: '828'
ht-degree: 36%

---

# Vue d’ensemble

_Implémenter Experience Cloud dans les sites web avec des balises_ est le point de départ idéal pour les développeurs front-end ou les spécialistes du marketing technique qui souhaitent apprendre à mettre en œuvre les solutions Adobe Experience Cloud sur leur site web.

Chaque leçon comprend des exercices pratiques et des informations essentielles pour vous aider à mettre en œuvre Experience Cloud et à comprendre sa valeur. Les sites de démonstration vous permettent de suivre le tutoriel afin que vous puissiez apprendre les techniques sous-jacentes dans un environnement sûr. Après avoir suivi ce tutoriel, vous devriez être prêt à commencer à mettre en œuvre toutes vos solutions marketing par le biais de balises sur votre propre site web.

>[!WARNING]
>
> Ce tutoriel et les exercices de son site web Luma ne sont plus conservés et reposent sur d’anciennes bibliothèques JavaScript. Pour connaître les bonnes pratiques en vigueur, suivez le tutoriel [Implémentation de Adobe Experience Cloud avec Web SDK](https://experienceleague.adobe.com/fr/docs/platform-learn/implement-web-sdk/overview).


Après avoir terminé cette formation, vous saurez comment :

* Création d’une propriété de balise

* Installation d’une propriété de balise sur un site web

* ajouter les solutions Adobe Experience Cloud suivantes :
   * **[Adobe Experience Platform Identity Service](id-service.md)**
   * **[Adobe Target](target.md)**
   * **[Adobe Analytics](analytics.md)**
   * **[Adobe Audience Manager](audience-manager.md)**

* créer des règles et des éléments de données pour envoyer des données aux solutions Adobe ;

* valider votre mise en œuvre à l’aide du débogueur Adobe Experience Cloud Debugger ;

* Publier les modifications par le biais des environnements de développement, d’évaluation et de production


>[!NOTE]
>
>Des tutoriels multi-solutions similaires sont également disponibles pour [Web SDK](../tutorial-web-sdk/overview.md) et [Mobile SDK](../tutorial-mobile-sdk/overview.md).

## Conditions préalables

Dans ces leçons, nous supposons que vous disposez d’un Adobe ID et des autorisations requises pour effectuer les exercices. Dans le cas contraire, vous devrez peut-être contacter votre administrateur Experience Cloud pour demander l’accès.

* Pour les balises, vous devez disposer des autorisations de développement, d’approbation, de publication, de gestion des extensions et de gestion des environnements. Pour plus d’informations sur les autorisations des utilisateurs de balises, consultez [la documentation](https://experienceleague.adobe.com/docs/experience-platform/tags/admin/user-permissions.html?lang=fr).
* Pour Adobe Analytics, vous devez connaitre votre serveur de suivi et les suites de rapports que vous utiliserez pour terminer ce tutoriel.
* Pour Audience Manager, vous devez connaître votre sous-domaine Audience Manager (également appelé « Nom de partenaire », « Identifiant de partenaire » ou « Sous-domaine de partenaire »)

En outre, on suppose que vous connaissez bien les langages de développement front-end tels que HTML et JavaScript. Vous n’avez pas besoin d’être un expert de ces langages pour suivre les leçons, mais vous en tirerez davantage si vous pouvez lire et comprendre le code confortablement.

## À propos des balises

La fonctionnalité Balises de Adobe Experience Platform représente la nouvelle génération des fonctionnalités de gestion des balises de sites web et des SDK mobiles d’Adobe. Les balises offrent aux clients un moyen simple de déployer et de gérer toutes les solutions d’analyse, de marketing et de publicité nécessaires pour offrir des expériences client pertinentes. Les balises n’entraînent pas de frais supplémentaires. Il est disponible pour tout client Adobe Experience Cloud.

Les balises pour les sites web vous permettent de gérer de manière centralisée tous les JavaScript liés aux solutions d’analyse, de marketing et de publicité utilisées sur vos sites de bureau et mobiles. Par exemple, si vous déployez Adobe Analytics, les balises gèrent la bibliothèque AppMeasurement JavaScript, renseignent les variables et déclenchent les requêtes.

Le contenu de votre conteneur est réduit, y compris votre code personnalisé. Tout est modulaire. Si vous n’avez pas besoin d’un élément, celui-ci n’est pas inclus dans votre bibliothèque. Vous obtenez ainsi une mise en œuvre rapide et compacte.

Tags est également une plateforme qui permet aux fournisseurs tiers de créer des extensions pour faciliter le déploiement de leurs solutions par le biais de balises. Une extension est un package de code (JavaScript, HTML et CSS) qui étend l’interface des balises et la fonctionnalité client. Vous pouvez considérer les balises comme un système d’exploitation, et les extensions comme les applications que vous utilisez pour exécuter vos tâches.

## À propos des leçons


>[!WARNING]
>
> Ce tutoriel et les exercices de son site web Luma ne sont plus conservés et reposent sur d’anciennes bibliothèques JavaScript. Pour connaître les bonnes pratiques en vigueur, suivez le tutoriel [Implémentation de Adobe Experience Cloud avec Web SDK](https://experienceleague.adobe.com/fr/docs/platform-learn/implement-web-sdk/overview).

Dans ces leçons, vous allez mettre en œuvre Adobe Experience Cloud dans un faux site web de vente au détail appelé Luma. Le [site Luma](https://luma.enablementadobe.com/content/luma/us/en.html) possède une couche de données et des fonctionnalités riches qui vous permettront de faire une mise en œuvre réaliste. Vous allez créer votre propre propriété de balise, dans votre propre organisation Experience Cloud, et la mapper à notre site Luma hébergé à l’aide du débogueur Experience Cloud Debugger.

[![Site web de Luma](images/overview-luma.png)](https://luma.enablementadobe.com/content/luma/us/en.html)

## Obtention des outils

1. Puisque vous utiliserez certaines extensions spécifiques au navigateur, nous vous recommandons de suivre le tutoriel en utilisant le [navigateur web Chrome](https://www.google.com/intl/fr/chrome/)
1. Ajouter l’extension [Adobe Experience Platform Debugger](https://chromewebstore.google.com/detail/adobe-experience-platform/bfnnokhpnncpkdmbokanobigaccjkpob) à votre navigateur Chrome
1. Copiez l’exemple de code de page HTML

   +++Exemple de code de page HTML

   ```html
   <!doctype html>
   <html lang="en">
   <head>
       <title>Tags: Sample HTML Page</title>
       <!--Preconnect and DNS-Prefetch to improve page load time. REPLACE "techmarketingdemos" WITH YOUR OWN AAM PARTNER ID, TARGET CLIENT CODE, AND ANALYTICS TRACKING SERVER-->
       <link rel="preconnect" href="//dpm.demdex.net">
       <link rel="preconnect" href="//fast.techmarketingdemos.demdex.net">
       <link rel="preconnect" href="//techmarketingdemos.demdex.net">
       <link rel="preconnect" href="//cm.everesttech.net">
       <link rel="preconnect" href="//techmarketingdemos.tt.omtrdc.net">
       <link rel="preconnect" href="//techmarketingdemos.sc.omtrdc.net">
       <link rel="dns-prefetch" href="//dpm.demdex.net">
       <link rel="dns-prefetch" href="//fast.techmarketingdemos.demdex.net">
       <link rel="dns-prefetch" href="//techmarketingdemos.demdex.net">
       <link rel="dns-prefetch" href="//cm.everesttech.net">
       <link rel="dns-prefetch" href="//techmarketingdemos.tt.omtrdc.net">
       <link rel="dns-prefetch" href="//techmarketingdemos.sc.omtrdc.net">
       <!--/Preconnect and DNS-Prefetch-->
       <!--Data Layer to enable rich data collection and targeting-->
       <script>
       var digitalData = {
           "page": {
               "pageInfo" : {
                   "pageName": "Home"
                   }
               }
       };
       </script>
       <!--/Data Layer-->
       <!--jQuery or other helper libraries-->
       <script src="https://code.jquery.com/jquery-3.3.1.min.js"></script>
       <!--/jQuery-->
       <!--Tags Header Embed Code: REPLACE THE NEXT LINE WITH THE EMBED CODE FROM YOUR OWN DEVELOPMENT ENVIRONMENT-->
       <script src="//assets.adobedtm.com/launch-EN93497c30fdf0424eb678d5f4ffac66dc.min.js" async></script>
       <!--/Tags Header Embed Code-->
   </head>
   <body>
       <h1>Tags: Sample HTML Page</h1>
       <p>This is a very simple page to demonstrate basic implementation concepts of Tags</p>
       <p>See <a href="https://docs.adobe.com/content/help/en/experience-cloud/implementing-in-websites-with-launch/index.html">Implementing the Experience Cloud in Websites with Tags</a> for the complete tutorial</p>
   </body>
   </html>
   ```

   +++

1. Utilisez un éditeur de texte dans lequel vous pouvez modifier la page HTML d’exemple. (Si vous n’en avez pas, nous vous recommandons d’essayer [Brackets](https://brackets.io/)).
1. Ajoutez le [site Luma](https://luma.enablementadobe.com/content/luma/us/en.html) à vos favoris.

>[!NOTE]
>
>Il peut vous être plus facile de suivre ce tutoriel avec le site Luma ouvert dans Chrome, tandis que vous lisez ce tutoriel et suivez les étapes de l’interface de collecte de données dans un autre navigateur.

C’est parti !

[Suite : « Créer une propriété de balise » >](create-a-property.md)
