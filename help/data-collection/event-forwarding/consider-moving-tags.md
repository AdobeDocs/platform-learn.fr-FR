---
title: Envisager de déplacer les balises du fournisseur vers le transfert d’événement
description: Découvrez comment évaluer une balise fournisseur côté client pour la distribution de données côté serveur.
feature: Event Forwarding, Tags, Integrations
solution: Data Collection
kt: 9921
level: Intermediate, Experienced
role: Admin, Developer, Architect
exl-id: f8fd351a-435c-4cc1-b987-ed2ead20d4d6
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '1369'
ht-degree: 6%

---

# Réfléchir au déplacement des balises de fournisseur côté client vers le transfert d’événement

Il existe plusieurs raisons impérieuses de considérer le déplacement des balises des fournisseurs côté client des navigateurs et des périphériques vers un serveur. Dans cet article, nous examinons comment évaluer une balise fournisseur côté client pour la déplacer potentiellement vers une propriété de transfert d’événement.

Cette évaluation n’est nécessaire que si vous envisagez de supprimer une balise du fournisseur côté client et de la remplacer par la distribution de données côté serveur dans une propriété de transfert d’événement. Cet article suppose que vous connaissez les principes de base de [collecte de données](https://experienceleague.adobe.com/docs/data-collection.html), et [transfert d’événement](https://experienceleague.adobe.com/docs/experience-platform/tags/event-forwarding/overview.html).

>[!NOTE]
>
>Adobe Experience Platform Launch est désormais une suite de technologies destinées à la collecte de données dans Adobe Experience Platform. Plusieurs modifications terminologiques ont par conséquent été apportées à la documentation du produit. Reportez-vous au [document](https://experienceleague.adobe.com/docs/experience-platform/tags/term-updates.html?lang=fr) suivant pour consulter une référence consolidée des modifications terminologiques.

Les fournisseurs de navigateurs modifient leur manière de traiter les cookies tiers. Les fournisseurs et technologies publicitaires et marketing nécessitent souvent l’utilisation de nombreuses balises côté client. Ces défis ne sont que deux raisons évidentes pour lesquelles nos clients ajoutent de la distribution de données côté serveur.

>[!NOTE]
>
>`Tag` dans cet article signifie code côté client, généralement du code JavaScript provenant d’un fournisseur qui est utilisé pour la collecte de données dans le navigateur ou le périphérique lorsqu’un visiteur interagit avec le site ou l’application. `Website` ou `site` ici fait référence à un site web, à une application web ou à une application pour un appareil mobile. Une &quot;balise&quot; à ces fins est également souvent appelée pixel.

## Cas d’utilisation et données {#use-cases-data}

La première étape consiste à définir les cas d’utilisation implémentés avec la balise du fournisseur côté client. Prenons l’exemple du pixel Facebook (Meta). Le déplacer de notre site vers le [API de conversion facebook](https://exchange.adobe.com/apps/ec/105509/facebook-conversions-api-extension) avec l’extension de transfert d’événement , vous devez d’abord documenter les cas d’utilisation spécifiques.

Pour le code du fournisseur côté client actuel :

- Quel événement spécifique et d’autres points de données sont exposés et transmis à la balise côté client ?
- Quand et où ce transfert de données a-t-il lieu ?

Il est utile de créer une liste, une feuille de calcul, un diagramme ou tout autre enregistrement des données et de la séquence d’événements pour documenter cette évaluation, même si elle est réservée à votre propre usage. Veillez à inclure des étiquettes pour les sources de données, d’où provient-elle ? Destinations : où cela nous mène-t-il ? Et les transformations : qu’en est-il entre la source et la destination ?

Dans notre exemple, nous effectuons le suivi des conversions avec le pixel Facebook lorsque les visiteurs interagissent avec notre site après avoir affiché une publicité Facebook. Ils peuvent également interagir avec notre site après avoir affiché des publicités associées sur une autre plateforme sociale. Pour afficher ces conversions dans les outils publicitaires et les rapports Facebook, les données requises doivent être envoyées à Facebook. Ces données peuvent inclure des événements de conversion tels que des téléchargements, des inscriptions, des mentions J’aime ou des achats.

### Données {#data}

Avec la balise côté client existante, que se passe-t-il avec les données de notre cas d’utilisation lorsqu’elle s’exécute ou s’exécute sur notre site ? Pouvons-nous capturer les données dont nous avons besoin dans le client, sans la balise du fournisseur, afin de pouvoir les envoyer au transfert d’événement ? Lors de l’utilisation de [tags](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html?lang=fr) Pour d’autres systèmes de gestion des balises, la plupart des données d’interaction des visiteurs sont disponibles pour la collecte et la distribution. Mais les données dont nous avons besoin pour notre cas d’utilisation sont-elles disponibles lorsque nous en avons besoin, là où nous en avons besoin, et dans le format dont nous en avons besoin, sans la balise du fournisseur côté client ? Voici quelques autres questions relatives aux données à prendre en compte :

- Un identifiant utilisateur fournisseur est-il requis pour chaque événement ?
- Si tel est le cas, comment peut-il être collecté ou généré sans la balise côté client ?
- Le fournisseur requiert-il spécifiquement son code côté client au moment de l’exécution ?
- Quelles autres données sont requises ? D&#39;où vont venir ces données ?

La plupart des balises du fournisseur côté client ne nécessitent pas de nombreux points de données pour un cas d’utilisation particulier, mais il est utile de noter les cas d’utilisation et les données requises lors de ces évaluations.

## API de fournisseur {#vendor-apis}

Nous connaissons maintenant les cas d’utilisation spécifiques à mettre en oeuvre, les données requises et la séquence d’événements de la source à la destination. Pour déterminer si le cas d’utilisation est adapté au transfert d’événement, nous pouvons désormais examiner les détails de l’API du fournisseur.

>[!IMPORTANT]
>
>Bien que de nombreux fournisseurs activent des API pour le transfert serveur à serveur, il existe également de nombreux fournisseurs qui ne disposent actuellement pas d’API adaptées à ces fins.

### Analyse des API {#investigate-apis}

Voici quelques étapes que nous pouvons suivre pour examiner les points de terminaison de l’API du fournisseur.

Le fournisseur dispose-t-il d’API conçues pour le transfert serveur à serveur des données d’événement ? Tout d’abord, recherchez les exigences relatives à ces points de terminaison d’API spécifiques :

- Existe-t-il des points de terminaison d’API pour envoyer les données requises ? Pour trouver les points de terminaison qui prennent en charge vos cas d’utilisation, consultez la documentation du développeur ou de l’API du fournisseur.
- Autorisent-elles la diffusion en continu de données d’événement ou uniquement de données par lots ?
- Quelles méthodes d’authentification prennent-elles en charge ? Jeton, HTTP, version des informations d’identification du client OAuth ou autre ? Voir [here](https://experienceleague.adobe.com/docs/experience-platform/tags/event-forwarding/secrets.html) pour les méthodes prises en charge par le transfert d’événement.
- Quel est le décalage d’actualisation de leur API ? Cette limitation est-elle compatible avec les minimums de transfert d’événement ? Détails [here](https://experienceleague.adobe.com/docs/experience-platform/tags/event-forwarding/secrets.html#:~:text=you%20can%20configure%20the%20Refresh%20Offset%20value%20for%20the%20secret).
- De quelles données ont-elles besoin pour les points de terminaison pertinents ?
- A-t-il besoin d’un identifiant utilisateur spécifique au fournisseur avec chaque appel au point de terminaison ?
- S’ils ont besoin de cet identifiant, où et comment peut-il être généré ou capturé, sans code côté client ?

En d’autres termes :

- Le fournisseur fournit-il les points de terminaison d’API requis pour nos cas d’utilisation ?
- Disposent-ils d’une méthode d’authentification compatible pour le transfert d’événement ?
- Pouvons-nous accéder à toutes les données requises pour une mise en oeuvre du transfert d’événement (soit du côté client, soit à partir d’autres appels API) ?

La balise est probablement un bon candidat pour passer du client à nos serveurs dans une propriété de transfert d’événement si nous pouvons répondre oui à ces questions.

Si le fournisseur ne dispose pas des points de terminaison d’API pour prendre en charge nos cas d’utilisation, alors, de toute évidence, cette balise de fournisseur n’est pas un bon choix pour utiliser le transfert d’événement à la place de la balise de fournisseur côté client.

Que se passe-t-il s’ils disposent d’API, mais nécessitent également un identifiant visiteur ou utilisateur unique avec chaque appel API ? Comment accéder à cet ID si le code (balise) côté client du fournisseur n’est pas en cours d’exécution sur le site ?

Certains fournisseurs changent leurs systèmes pour le nouveau monde sans cookies tiers. Ces modifications incluent l’utilisation d’autres identifiants uniques, comme une [UUID](https://developer.mozilla.org/en-US/docs/Glossary/UUID) ou autre [ID généré par le client](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/first-party-device-ids.html). Si le fournisseur autorise un ID généré par le client, nous pouvons l’envoyer du client au réseau Platform Edge avec le SDK Web ou mobile, ou peut-être l’obtenir à partir d’un appel API dans le transfert d’événement. Lorsque nous envoyons des données à ce fournisseur dans une règle de transfert d’événement, nous incluons simplement cet identifiant si nécessaire.

Si le fournisseur nécessite des données (comme un identifiant unique spécifique au fournisseur, par exemple) qui ne peuvent être générées ou accessibles que par sa propre balise côté client, alors cette balise du fournisseur n’est probablement pas un bon candidat pour le déplacement. _Il est déconseillé d’essayer de rétroconcevoir une balise côté client avec l’idée de déplacer cette collecte de données vers le transfert d’événement sans les API appropriées._

Le [Connecteur Adobe Experience Platform Cloud](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/cloud-connector/overview.html) L’extension peut effectuer des requêtes HTTP selon les besoins avec des fournisseurs disposant des API appropriées pour le transfert de données d’événement serveur à serveur. Bien que les extensions spécifiques à un fournisseur soient intéressantes et que d’autres extensions soient actuellement en cours de développement principal, nous pouvons aujourd’hui mettre en oeuvre des règles de transfert d’événement à l’aide de l’extension Cloud Connector, sans attendre d’autres extensions de fournisseur.

## Outils {#tools}

L’investigation et le test des points de terminaison de l’API du fournisseur est plus facile avec des outils tels que [Postman](https://www.postman.com/), ou des extensions d’éditeur de texte telles que Visual Studio Code [Tourner le client](https://marketplace.visualstudio.com/items?itemName=rangav.vscode-thunder-client)ou [Client HTTP](https://marketplace.visualstudio.com/items?itemName=mkloubert.vscode-http-client).

## Étapes suivantes {#next-steps}

Cet article fournit une séquence d’étapes permettant d’évaluer une balise côté client du fournisseur et de la déplacer potentiellement côté serveur dans une propriété de transfert d’événement. Pour plus d’informations sur les sujets connexes, voir les liens suivants :

- [Gestion des balises](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html) dans Adobe Experience Platform
- [Transfert d’événement](https://experienceleague.adobe.com/docs/experience-platform/tags/event-forwarding/overview.html) pour le traitement côté serveur
- [Mises à jour de terminologie](https://experienceleague.adobe.com/docs/experience-platform/tags/term-updates.html) dans la collecte de données
