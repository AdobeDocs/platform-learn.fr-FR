---
title: Comparaison de l’extension Target avec l’extension de prise de décision
description: Découvrez les différences entre l’extension Target et l’extension de prise de décision, notamment les fonctionnalités, les fonctions, les paramètres et le flux de données.
exl-id: 6c854049-4126-45cf-8b2b-683cf29549f3
source-git-commit: 05b0146256c6f8644e42f851498a0f49ff44bf68
workflow-type: tm+mt
source-wordcount: '829'
ht-degree: 4%

---

# Comparaison de l’extension Target avec l’extension de prise de décision

L’extension Adobe Journey Optimizer - Prise de décision diffère de l’extension Adobe Target pour les applications mobiles. Les tableaux suivants constituent une référence pour vous aider à évaluer les zones de votre mise en oeuvre sur lesquelles vous devrez peut-être vous concentrer pendant le processus de migration.

Après avoir examiné les informations ci-dessous et évalué votre mise en oeuvre technique actuelle de l’extension Target, vous devriez être en mesure de comprendre les éléments suivants :

- Quelles fonctionnalités Target sont prises en charge par Adobe Journey Optimizer - Prise de décision ?
- Quelles fonctions d’extension Adobe Target ont des équivalents Adobe Journey Optimizer - Decisioning ?
- Application des paramètres Target avec Adobe Journey Optimizer - Prise de décision
- Différence entre le flux de données de l’extension Adobe Target et l’extension Adobe Journey Optimizer - Decisioning

Si vous découvrez le SDK Web Platform, ne vous inquiétez pas : les éléments ci-dessous sont abordés plus en détail tout au long de ce tutoriel.

## Comparaison des fonctionnalités

| Fonctionnalité | Extension Target | Extension de prise de décision (Target via Edge) |
|---|---|---|
| Mode de prérécupération | Pris en charge | Pris en charge |
| Mode d’exécution | Pris en charge | Non pris en charge |
| Paramètres personnalisés | Pris en charge | Pris en charge* |
| Paramètres de profil | Pris en charge | Pris en charge* |
| Paramètres d’entité | Pris en charge | Pris en charge* |
| Audiences cibles | Pris en charge | Pris en charge |
| Audiences Real-Time CDP | ??? | Pris en charge |
| Attributs Real-Time CDP | ??? | Pris en charge |
| Mesures de cycle de vie | Pris en charge | Pris en charge via les règles de collecte de données |
| thirdPartyId (mbox3rdPartyId) | Pris en charge | Pris en charge par le biais de la configuration d’Identity Map et de l’espace de noms dans le flux de données |
| Notifications (affichage, clic) | Pris en charge | Pris en charge |
| Jetons de réponse | Pris en charge | Pris en charge |
| Analytics for Target (A4T) | Côté client uniquement | Côté client et côté serveur |
| Aperçus mobiles (mode AQ) | Pris en charge | Prise en charge limitée d’Assurance |

>[!IMPORTANT]
>
> \* Les paramètres envoyés dans une requête s’appliquent à toutes les portées de la requête. Si vous devez définir des paramètres différents pour des portées différentes, vous devez effectuer des requêtes supplémentaires.



## Légendes dignes de mention

>[!NOTE]
>
>La migration de Target vers le SDK Web Platform tout en conservant une mise en oeuvre Adobe Analytics d’AppMeasurement existante pour une page donnée n’est pas prise en charge.
>
> Il est possible de migrer votre implémentation d’at.js (et d’AppMeasurement.js) vers le SDK Web Platform une page à la fois. Si vous optez pour cette approche, il est préférable de définir les options [`idMigrationEnabled`](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-the-sdk.html#id-migration-enabled) et [`targetMigrationEnabled`](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-the-sdk.html#targetMigrationEnabled) sur `true` avec la commande `configure`.

## Fonctions de l’extension Target et équivalents de l’extension de prise de décision

De nombreuses fonctions d’extension Target ont une approche équivalente utilisant l’extension de prise de décision décrite dans le tableau ci-dessous. Pour plus d’informations sur les [fonctions](https://developer.adobe.com/target/implement/client-side/atjs/atjs-functions/atjs-functions/), consultez le Guide du développeur d’Adobe Target.

| Extension Target | Extension de prise de décision | Notes |
| --- | --- | --- | 
| `prefetchContent` | `updatePropositions` |  |
| `retrieveLocationContent` | `getPropositions` | Lors de l’utilisation de l’API `getPropositions`, aucun appel distant n’est effectué pour récupérer les portées non mises en cache dans le SDK. |
| `displayedLocations` | Offre -> `displayed()` | En outre, la méthode d’offre `generateDisplayInteractionXdm` peut être utilisée pour générer le XDM pour l’affichage des éléments. Par la suite, l’API sendEvent du SDK réseau Edge peut être utilisée pour joindre des données XDM supplémentaires de forme libre et envoyer un événement d’expérience à distance. |
| `clickedLocation` | Offre -> `tapped()` | En outre, la méthode d’offre `generateTapInteractionXdm` peut être utilisée pour générer le fichier XDM pour le clic sur l’élément. Par la suite, l’API sendEvent du SDK réseau Edge peut être utilisée pour joindre des données XDM supplémentaires de forme libre et envoyer un événement d’expérience à distance. |
| `clearPrefetchCache` | `clearCachedPropositions` |  |
| `resetExperience` |  | Utilisez l’API `removeIdentity` d’ Identity for Edge Network extension pour que le SDK cesse d’envoyer l’identifiant visiteur au réseau Edge. Pour plus d’informations, voir [la documentation de l’API removeIdentity](https://developer.adobe.com/client-sdks/edge/identity-for-edge-network/api-reference/#removeidentity). <br><br>Remarque : L’API `resetIdentities` de Mobile Core efface toutes les identités stockées dans le SDK, y compris l’identifiant Experience Cloud (ECID) et doit être utilisée avec modération ! |
| `getSessionId` |  | Le gestionnaire de réponse `state:store` contient des informations relatives à la session. L’extension réseau Edge permet de la gérer en associant des éléments de magasin d’états non expirés aux demandes suivantes. |
| `setSessionId` |  | Le gestionnaire de réponse `state:store` contient des informations relatives à la session. L’extension réseau Edge permet de la gérer en associant des éléments de magasin d’états non expirés aux demandes suivantes. |
| `getThirdPartyId` | S.O. | Utilisez l’API updateIdentities d’Identity pour l’extension de l’Edge Network afin de fournir la valeur de l’ID tiers. Ensuite, configurez l’espace de noms de l’ID tiers dans le flux de données. Pour plus d’informations, voir [la documentation mobile de Target Third Party Id](https://developer.adobe.com/client-sdks/edge/adobe-journey-optimizer-decisioning/#target-third-party-id). |
| `setThirdPartyId` | S.O. | Utilisez l’API updateIdentities d’Identity pour l’extension de l’Edge Network afin de fournir la valeur de l’ID tiers. Ensuite, configurez l’espace de noms de l’ID tiers dans le flux de données. Pour plus d’informations, voir [la documentation mobile de Target Third Party Id](https://developer.adobe.com/client-sdks/edge/adobe-journey-optimizer-decisioning/#target-third-party-id). |
| `getTntId` |  | La gestion de la réponse `locationHint:result` contient les informations d’indicateur de l’emplacement cible. Il est supposé que Target Edge sera colocalisé avec Experience Edge. <br> <br>L’extension réseau Edge utilise l’indicateur d’emplacement EdgeNetwork pour déterminer la grappe réseau Edge à laquelle envoyer des requêtes. Pour partager des conseils d’emplacement réseau Edge sur les SDK (applications hybrides), utilisez les API `getLocationHint` et `setLocationHint` de l’extension Edge Network. Pour plus d’informations, voir [la `getLocationHint` documentation de l’API](https://developer.adobe.com/client-sdks/edge/edge-network/api-reference/#getlocationhint). |
| `setTntId` |  |  |
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |

## Paramètres de l’extension Target et équivalents de l’extension de prise de décision

L’extension Target peut être configurée et téléchargée avec divers paramètres dans ...

| Extension Target | Extension de prise de décision |
| --- | --- | 
| |  |


## Comparaison des diagrammes système

Les diagrammes suivants doivent vous aider à comprendre les différences de flux de données entre une mise en oeuvre Target à l’aide de l’extension Adobe Journey Optimizer - Prise de décision et une mise en oeuvre à l’aide de l’extension Adobe Target.

### Diagramme du système d’extension Target



### Diagramme du système d’extension de prise de décision




>[!NOTE]
>
>Nous nous engageons à vous aider à réussir la migration de Target mobile de l’extension Target vers l’extension de prise de décision. Si vous rencontrez des obstacles lors de votre migration ou si vous pensez qu’il manque des informations essentielles dans ce guide, faites-le-nous savoir en publiant sur [cette discussion communautaire](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-target-from-at-js-to-web-sdk/m-p/575587#M463).
