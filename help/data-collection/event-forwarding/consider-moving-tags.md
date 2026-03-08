---
title: Envisagez de déplacer les balises de fournisseur vers le transfert d’événement
description: Découvrez comment évaluer une balise de fournisseur côté client pour la distribution de données côté serveur.
feature: Event Forwarding, Tags, Integrations
role: Admin, Developer
level: Intermediate, Experienced
jira: KT-9921
exl-id: f8fd351a-435c-4cc1-b987-ed2ead20d4d6
source-git-commit: 070fc02801d3403bf65ca732323338481e25b581
workflow-type: tm+mt
source-wordcount: '1279'
ht-degree: 4%

---

# Envisagez de déplacer les balises de fournisseur côté client vers le transfert d’événement

Il existe plusieurs raisons impérieuses de déplacer les balises de fournisseur côté client des navigateurs et des appareils vers un serveur. Dans cet article, nous expliquons comment évaluer une balise de fournisseur côté client pour éventuellement la déplacer vers une propriété de transfert d’événement.

Cette évaluation n’est nécessaire que si vous envisagez de supprimer une balise fournisseur côté client et de la remplacer par une distribution de données côté serveur dans une propriété de transfert d’événements. Cet article suppose que vous connaissez les principes de base de la [collecte de données](https://experienceleague.adobe.com/docs/data-collection.html) et du [transfert d’événement](https://experienceleague.adobe.com/docs/experience-platform/tags/event-forwarding/overview.html?lang=fr).

>[!NOTE]
>
>Adobe Experience Platform Launch est désormais une suite de technologies destinées à la collecte de données dans Adobe Experience Platform. Plusieurs modifications terminologiques ont par conséquent été apportées à la documentation du produit. Reportez-vous au [document](https://experienceleague.adobe.com/docs/experience-platform/tags/term-updates.html?lang=fr) suivant pour consulter une référence consolidée des modifications terminologiques.

Les fournisseurs de navigateur modifient la façon dont ils traitent les cookies tiers. Les fournisseurs et technologies Advertising et marketing nécessitent souvent l’utilisation de nombreuses balises côté client. Ces défis ne sont que deux raisons majeures pour lesquelles nos clients ajoutent la distribution de données côté serveur.

>[!NOTE]
>
>`Tag` dans cet article désigne le code côté client, généralement JavaScript d’un fournisseur, utilisé pour la collecte de données dans le navigateur ou l’appareil lorsqu’un visiteur interagit avec le site ou l’application. `Website` ou `site` fait ici référence à un site web, une application web ou une application pour un appareil mobile. Une « balise » à ces fins est également souvent appelée pixel.

## Cas d’utilisation et données {#use-cases-data}

La première étape consiste à définir les cas d’utilisation implémentés avec la balise de fournisseur côté client. Prenons l’exemple du pixel Facebook (Meta). Le déplacer de notre site vers l’API [Meta Conversions](https://exchange.adobe.com/apps/ec/109168/meta-conversions-api) avec l’extension de transfert d’événement signifie d’abord documenter les cas d’utilisation spécifiques.

Pour le code fournisseur côté client actuel :

- Quel événement spécifique et quels autres points de données sont exposés et transmis à la balise côté client ?
- Quand et où ce transfert de données a-t-il lieu ?

Il est utile de faire une liste, une feuille de calcul, un diagramme ou tout autre enregistrement des données et de la séquence des événements pour documenter cette évaluation, même si c&#39;est seulement pour votre propre usage. Veillez à inclure des libellés pour les sources de données : d’où viennent-ils ? Destinations : où vont-elles ? Et les transformations : qu’advient-il entre la source et la destination ?

Dans notre exemple, nous suivons les conversions avec le pixel Facebook lorsque les visiteurs interagissent avec notre site après avoir vu une publicité Facebook. Ils pourraient également interagir avec notre site après avoir visionné des annonces connexes sur une autre plateforme sociale. Pour afficher ces conversions dans les outils et les rapports publicitaires de Facebook, les données requises doivent être transmises à Facebook. Ces données peuvent inclure des événements de conversion tels que des téléchargements, des enregistrements, des mentions J’aime ou des achats.

### Données {#data}

Avec la balise côté client existante, lorsqu’elle s’exécute sur notre site, que se passe-t-il avec les données de notre cas d’utilisation ? Pouvons-nous capturer les données dont nous avons besoin dans le client, sans la balise de fournisseur, afin de pouvoir les envoyer au transfert d’événement ? Lors de l’utilisation de [balises](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html?lang=fr) ou d’autres systèmes de gestion des balises, la plupart des données d’interaction des visiteurs sont disponibles pour la collecte et la distribution. Mais les données dont nous avons besoin pour notre cas d’utilisation sont-elles disponibles quand nous en avons besoin, où nous en avons besoin et au format dont nous avons besoin, sans balise de fournisseur côté client ? Voici d’autres questions relatives aux données à prendre en compte :

- Un ID d’utilisateur fournisseur est-il requis pour chaque événement ?
- Si tel est le cas, comment peut-il être collecté ou généré sans la balise côté client ?
- Le fournisseur exige-t-il spécifiquement son code côté client au moment de l’exécution ?
- Quelles autres données sont requises ? D&#39;où viendront ces données ?

La plupart des balises de fournisseur côté client ne nécessitent pas de nombreux points de données pour un cas d’utilisation particulier, mais il est utile de noter les cas d’utilisation et les données requises lors de ces évaluations.

## API du fournisseur {#vendor-apis}

Nous connaissons désormais les cas d’utilisation spécifiques à implémenter, les données requises et la séquence d’événements, de la source à la destination. Pour déterminer si le cas d’utilisation est adapté au transfert d’événement, nous pouvons désormais examiner les détails de l’API du fournisseur.

>[!IMPORTANT]
>
>Bien que de nombreux fournisseurs activent des API pour le transfert serveur à serveur, il existe également de nombreux fournisseurs qui ne disposent pas actuellement d’API adaptées à ces objectifs.

### Examen des API {#investigate-apis}

Voici quelques étapes que nous pouvons suivre pour examiner les points d’entrée de l’API du fournisseur.

Le fournisseur dispose-t-il d’API conçues pour le transfert serveur à serveur des données d’événement ? Tout d’abord, recherchez les exigences relatives à ces points d’entrée d’API spécifiques :

- Les points d’entrée de l’API existent-ils pour envoyer les données requises ? Pour trouver les points d’entrée qui prennent en charge vos cas d’utilisation, consultez la documentation du développeur ou de l’API du fournisseur.
- Autorisent-elles les données d’événement de diffusion en continu ou uniquement les données par lots ?
- Quelles méthodes d’authentification prennent-elles en charge ? Jeton, HTTP, version des informations d’identification du client OAuth ou autre ? Voir [ici](https://experienceleague.adobe.com/docs/experience-platform/tags/event-forwarding/secrets.html?lang=fr) pour connaître les méthodes prises en charge par le transfert d’événement.
- Quel est le décalage d’actualisation de leur API ? Cette limitation est-elle compatible avec les minimums de transfert d’événement ? Détails [ici](https://experienceleague.adobe.com/docs/experience-platform/tags/event-forwarding/secrets.html#:~:text=you%20can%20configure%20the%20Refresh%20Offset%20value%20for%20the%20secret).
- De quelles données ont-ils besoin pour les points d’entrée pertinents ?
- Nécessitent-ils un identifiant utilisateur spécifique au fournisseur pour chaque appel au point d’entrée ?
- S’ils ont besoin de cet identifiant, où et comment peut-il être généré ou capturé sans code côté client ?

En d’autres termes :

- Le fournisseur fournit-il les points d’entrée d’API requis pour nos cas d’utilisation ?
- Disposent-ils d’une méthode d’authentification compatible pour le transfert d’événement ?
- Pouvons-nous accéder à toutes les données requises pour une implémentation du transfert d’événement (soit du côté client, soit à partir d’autres appels d’API) ?

La balise est probablement un bon candidat pour passer du client à nos serveurs dans une propriété de transfert d’événement si nous pouvons répondre oui à ces questions.

Si le fournisseur ne dispose pas des points d’entrée d’API pour prendre en charge nos cas d’utilisation, il est évident que cette balise de fournisseur n’est pas un bon candidat pour utiliser le transfert d’événement à la place de la balise de fournisseur côté client.

Que se passe-t-il s’ils disposent d’API mais ont également besoin d’un identifiant visiteur ou utilisateur unique à chaque appel API ? Comment pouvons-nous accéder à cet ID si le code côté client (balise) du fournisseur n’est pas en cours d’exécution sur le site ?

Certains fournisseurs changent leurs systèmes pour le nouveau monde sans cookies tiers. Ces modifications incluent l’utilisation d’identifiants uniques alternatifs, tels qu’un [UUID](https://developer.mozilla.org/en-US/docs/Glossary/UUID) ou d’autres [ID générés par le client](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/first-party-device-ids.html). Si le fournisseur autorise un identifiant généré par le client, nous pouvons l’envoyer du client vers Platform Edge Network avec Web ou Mobile SDK, ou l’obtenir à partir d’un appel API dans le transfert d’événement. Lorsque nous envoyons des données à ce fournisseur dans une règle de transfert d’événement, nous incluons simplement cet identifiant si nécessaire.

Si le fournisseur a besoin de données (un ID unique spécifique à un fournisseur, par exemple) qui ne peuvent être générées ou accessibles que par sa propre balise côté client, il n’est probablement pas recommandé de déplacer cette balise fournisseur. _Il est déconseillé d’essayer de rétroconcevoir une balise côté client avec l’idée de déplacer cette collecte de données vers le transfert d’événement sans les API appropriées._

L’extension [Adobe Experience Platform Cloud Connector](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/cloud-connector/overview.html) peut effectuer des requêtes HTTP selon les besoins avec les fournisseurs qui disposent des API appropriées pour le transfert de données d’événement de serveur à serveur. Bien que des extensions spécifiques à un fournisseur soient intéressantes et que d’autres extensions soient en cours de développement, nous pouvons mettre en œuvre des règles de transfert d’événement dès aujourd’hui à l’aide de l’extension Cloud Connector, sans attendre d’extensions fournisseur supplémentaires.

## Outils {#tools}

Il est plus facile d’enquêter et de tester les points d’entrée de l’API du fournisseur avec des outils tels que [Postman](https://www.postman.com/) ou les extensions d’éditeur de texte comme Visual Studio Code [client Thunder](https://marketplace.visualstudio.com/items?itemName=rangav.vscode-thunder-client) ou [client HTTP](https://marketplace.visualstudio.com/items?itemName=mkloubert.vscode-http-client).

## Étapes suivantes {#next-steps}

Cet article fournit une séquence d’étapes permettant d’évaluer une balise côté client d’un fournisseur et éventuellement de la déplacer côté serveur dans une propriété de transfert d’événement. Pour plus d’informations sur les rubriques connexes, consultez les liens suivants :

- [Gestion des balises](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html?lang=fr) dans Adobe Experience Platform
- [ Transfert d’événement ](https://experienceleague.adobe.com/docs/experience-platform/tags/event-forwarding/overview.html?lang=fr) pour le traitement côté serveur
- [Mises à jour terminologiques](https://experienceleague.adobe.com/docs/experience-platform/tags/term-updates.html?lang=fr) dans la collecte de données
