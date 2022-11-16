---
title: Mise en oeuvre de l’Experience Cloud dans les sites web avec des balises
description: La mise en oeuvre de l’Experience Cloud dans les sites web avec balises est le point de départ idéal pour les développeurs front-end ou les spécialistes du marketing technique qui souhaitent apprendre à mettre en oeuvre les solutions Adobe Experience Cloud sur leur site web.
recommendations: catalog, noDisplay
exl-id: 1b95f0b2-3062-49d1-9b0b-e6824a54008f
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '906'
ht-degree: 44%

---

# Présentation

_Mise en oeuvre de l’Experience Cloud dans les sites web avec des balises_ est le point de départ idéal pour les développeurs front-end ou les spécialistes du marketing technique qui souhaitent apprendre à mettre en oeuvre les solutions Adobe Experience Cloud sur leur site web.

Chaque leçon comprend des exercices pratiques et des informations essentielles pour vous aider à mettre en œuvre Experience Cloud et à comprendre sa valeur. Les sites de démonstration vous permettent de suivre le tutoriel afin que vous puissiez apprendre les techniques sous-jacentes dans un environnement sûr. Après avoir terminé ce tutoriel, vous devriez être prêt à commencer à mettre en oeuvre toutes vos solutions marketing par le biais de balises sur votre propre site web.

>[!INFO]
>
>Ce tutoriel utilise des extensions et des bibliothèques spécifiques à l’application (AppMeasurement.js pour Adobe Analytics, at.js pour Adobe Target). Si vous souhaitez mettre en oeuvre le SDK Web de Adobe Experience Platform, reportez-vous à la section [Mise en oeuvre de Adobe Experience Cloud avec le SDK Web](/help/tutorial-web-sdk/overview.md) tutoriel .


Après avoir terminé cette formation, vous saurez comment :

* Créer une propriété de balise

* Installation d’une propriété de balise sur un site web

* ajouter les solutions Adobe Experience Cloud suivantes :
   * **[Adobe Experience Platform Identity Service](id-service.md)**
   * **[Adobe Target](target.md)**
   * **[Adobe Analytics](analytics.md)**
   * **[Adobe Audience Manager](audience-manager.md)**

* créer des règles et des éléments de données pour envoyer des données aux solutions Adobe ;

* valider votre mise en œuvre à l’aide du débogueur Adobe Experience Cloud Debugger ;

* Publier les modifications via les environnements de développement, d’évaluation et de production

>[!NOTE]
>
>Adobe Experience Platform Launch est intégré à Adobe Experience Platform comme une suite de technologies destinées à la collecte de données. Plusieurs modifications terminologiques ont été apportées à l’interface que vous devez connaître lors de l’utilisation de ce contenu :
>
> * Le platform launch (côté client) est désormais **[[!DNL tags]](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html?lang=fr)**
> * Le platform launch côté serveur est désormais **[[!DNL event forwarding]](https://experienceleague.adobe.com/docs/experience-platform/tags/event-forwarding/overview.html)**
> * Les configurations Edge sont désormais **[[!DNL datastreams]](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/datastreams.html?lang=fr)**


>[!NOTE]
>
>Des tutoriels multisolutions similaires sont également disponibles pour [SDK Web](../tutorial-web-sdk/overview.md) et [SDK Mobile](../tutorial-mobile-sdk/overview.md).

## Conditions préalables

Dans ces leçons, nous supposons que vous disposez d’un Adobe ID et des autorisations requises pour effectuer les exercices. Dans le cas contraire, vous devrez peut-être contacter votre administrateur Experience Cloud pour demander l’accès.

* Pour les balises, vous devez disposer des autorisations Develop (Développer), Approve (Approuver), Publish (Publier), Manage Extensions (Gérer les extensions) et Manage Environments (Gérer les environnements). Pour plus d’informations sur les autorisations d’utilisateur de balises, voir [la documentation](https://experienceleague.adobe.com/docs/experience-platform/tags/admin/user-permissions.html?lang=fr).
* Pour Adobe Analytics, vous devez connaitre votre serveur de suivi et les suites de rapports que vous utiliserez pour terminer ce tutoriel.
* Pour toute Audience Manager, vous devez connaître votre sous-domaine d’Audience Manager (également appelé &quot;Nom de partenaire&quot;, &quot;Identifiant de partenaire&quot; ou &quot;Sous-domaine de partenaire&quot;).

En outre, vous êtes censé connaitre les langages de développement d’interfaces tels que HTML et JavaScript. Vous n’avez pas besoin d’être un expert dans ces langues pour terminer les leçons, mais vous en tirerez plus d’informations si vous pouvez facilement lire et comprendre le code.

## À propos des balises

La fonctionnalité de balises de Adobe Experience Platform est la nouvelle génération de fonctionnalités de gestion de SDK mobile et de balises de sites web d’Adobe. Les balises offrent aux clients un moyen simple de déployer et gérer toutes les solutions d’analyse, de marketing et de publicité nécessaires pour proposer des expériences client pertinentes. Les balises ne sont pas soumises à des frais supplémentaires. Il est disponible pour tout client Adobe Experience Cloud.

Les balises de sites web vous permettent de gérer de manière centralisée l’ensemble du code JavaScript associé aux solutions d’analyse, de marketing et de publicité utilisées sur vos sites pour mobiles et ordinateurs de bureau. Par exemple, si vous déployez Adobe Analytics, les balises gèrent la bibliothèque JavaScript AppMeasurement, renseignent les variables et déclenchent les demandes.

Le contenu de votre conteneur est réduit, y compris votre code personnalisé. Tout est modulaire. Si vous n’avez pas besoin d’un élément, celui-ci n’est pas inclus dans votre bibliothèque. Vous obtenez ainsi une mise en œuvre rapide et compacte.

Les balises sont également une plateforme qui permet aux fournisseurs tiers de créer des extensions pour faciliter le déploiement de leurs solutions par le biais de balises. Une extension est un module de code (JavaScript, HTML et CSS) qui étend l’interface des balises et les fonctionnalités du client. Vous pouvez considérer les balises comme un système d’exploitation et les extensions comme les applications que vous utilisez pour exécuter vos tâches.

## À propos des leçons

Dans ces leçons, vous allez mettre en œuvre Adobe Experience Cloud dans un faux site web de vente au détail appelé Luma. Le [site Luma](https://luma.enablementadobe.com/content/luma/us/en.html) possède une couche de données et des fonctionnalités riches qui vous permettront de faire une mise en œuvre réaliste. Vous allez créer votre propre propriété de balise, dans votre propre organisation Experience Cloud, et la mapper à notre site Luma hébergé à l’aide de l’Experience Cloud Debugger.

[![Site web Luma](images/overview-luma.png)](https://luma.enablementadobe.com/content/luma/us/en.html)

## Obtention des outils

1. Puisque vous utiliserez certaines extensions spécifiques au navigateur, nous vous recommandons de suivre le tutoriel en utilisant le [navigateur web Chrome](https://www.google.com/intl/fr/chrome/)
1. Ajoutez l’extension [Adobe Experience Cloud Debugger](https://chrome.google.com/webstore/detail/adobe-experience-cloud-de/ocdmogmohccmeicdhlhhgepeaijenapj) à votre navigateur Chrome.
1. Téléchargez la [page HTML d’exemple](https://www.enablementadobe.com/multi/web/basic-sample.html) (cliquez avec le bouton droit sur ce lien et cliquez sur « Enregistrer le lien sous »).
1. Utilisez un éditeur de texte dans lequel vous pouvez modifier la page HTML d’exemple. (Si vous n’en avez pas, nous vous recommandons d’essayer [Brackets](https://brackets.io/)).
1. Ajoutez le [site Luma](https://luma.enablementadobe.com/content/luma/us/en.html) à vos favoris.

>[!NOTE]
>
>Il vous sera peut-être plus facile de suivre ce tutoriel avec le site Luma ouvert dans Chrome. Vous pourrez lire ce tutoriel et suivre les étapes de l’interface de collecte de données dans un autre navigateur.

C’est parti !

[Suite : &quot;Créer une propriété de balise&quot; >](create-a-property.md)
