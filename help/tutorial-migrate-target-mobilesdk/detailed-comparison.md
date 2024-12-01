---
title: Comparaison de l’extension Target avec l’extension de prise de décision
description: Découvrez les différences entre l’extension Target et l’extension de prise de décision, notamment les fonctionnalités, les fonctions, les paramètres et le flux de données.
exl-id: 6c854049-4126-45cf-8b2b-683cf29549f3
source-git-commit: 8e4e23413c842f84159891287d09e8a6cfbbbc53
workflow-type: tm+mt
source-wordcount: '986'
ht-degree: 5%

---

# Comparaison de l’extension Target avec l’extension de prise de décision

L’extension Adobe Journey Optimizer - Prise de décision diffère de l’extension Adobe Target pour les applications mobiles. Les tableaux suivants constituent une référence pour vous aider à évaluer les zones de votre mise en oeuvre sur lesquelles vous devrez peut-être vous concentrer pendant le processus de migration.

Après avoir examiné les informations ci-dessous et évalué votre mise en oeuvre technique actuelle de l’extension Target, vous devriez être en mesure de comprendre les éléments suivants :

- Quelles fonctionnalités Target sont prises en charge par Adobe Journey Optimizer - Prise de décision ?
- Quelles fonctions d’extension Adobe Target ont des équivalents Adobe Journey Optimizer - Decisioning ?
- Application des paramètres Target avec Adobe Journey Optimizer - Prise de décision
- Flux de données à l’aide de l’extension Adobe Journey Optimizer - Decisioning


## Comparaison des fonctionnalités

| Fonctionnalité | Extension Target | Extension de prise de décision (Target via Edge) |
|---|---|---|
| Mode de prérécupération | Pris en charge | Pris en charge |
| Mode d’exécution | Pris en charge | Non pris en charge |
| Paramètres personnalisés | Pris en charge | Pris en charge* |
| Paramètres de profil | Pris en charge | Pris en charge* |
| Paramètres d’entité | Pris en charge | Pris en charge* |
| Audiences cibles | Pris en charge | Pris en charge |
| Audiences Real-Time CDP | Non pris en charge | Pris en charge |
| Attributs Real-Time CDP | Non pris en charge | Pris en charge |
| Mesures de cycle de vie | Pris en charge | Pris en charge via les règles de collecte de données |
| thirdPartyId (mbox3rdPartyId) | Pris en charge | Pris en charge par le biais d’Identity Map et de l’espace de noms des identifiants tiers Target dans le flux de données |
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
>Conservez la configuration et les paramètres des balises de l’extension Target en place même après la migration du code de votre application vers l’extension de prise de décision. Cela permettra de s’assurer que Target continue de fonctionner pour les clients qui n’ont pas encore mis à jour l’application vers la nouvelle version.
>
>Si vous utilisez l’intégration d’Analytics for Target (A4T), veillez également à migrer votre mise en oeuvre d’Analytics avec l’extension Bridge Edge au même moment que vous migrez votre mise en oeuvre de Target vers l’extension de prise de décision.

## Fonctions de l’extension Target et équivalents de l’extension de prise de décision

De nombreuses fonctions d’extension Target ont une approche équivalente utilisant l’extension de prise de décision décrite dans le tableau ci-dessous. Pour plus d’informations sur les [fonctions](https://developer.adobe.com/target/implement/client-side/atjs/atjs-functions/atjs-functions/), consultez le Guide du développeur d’Adobe Target.

| Extension Target | Extension de prise de décision | Notes |
| --- | --- | --- | 
| `prefetchContent` | `updatePropositions` |  |
| `retrieveLocationContent` | `getPropositions` | Lors de l’utilisation de l’API `getPropositions`, aucun appel distant n’est effectué pour récupérer les portées non mises en cache dans le SDK. |
| `displayedLocations` | Offre -> `displayed()` | En outre, la méthode d’offre `generateDisplayInteractionXdm` peut être utilisée pour générer le XDM pour l’affichage des éléments. Par la suite, l’API sendEvent du SDK réseau Edge peut être utilisée pour joindre des données XDM supplémentaires de forme libre et envoyer un événement d’expérience à distance. |
| `clickedLocation` | Offre -> `tapped()` | En outre, la méthode d’offre `generateTapInteractionXdm` peut être utilisée pour générer le fichier XDM pour le clic sur l’élément. Par la suite, l’API sendEvent du SDK réseau Edge peut être utilisée pour joindre des données XDM supplémentaires de forme libre et envoyer un événement d’expérience à distance. |
| `clearPrefetchCache` | `clearCachedPropositions` |  |
| `resetExperience` | S.O. | Utilisez l’API `removeIdentity` d’ Identity for Edge Network extension pour que le SDK cesse d’envoyer l’identifiant visiteur au réseau Edge. Pour plus d’informations, voir [la documentation de l’API removeIdentity](https://developer.adobe.com/client-sdks/edge/identity-for-edge-network/api-reference/#removeidentity). <br><br>Remarque : L’API `resetIdentities` de Mobile Core efface toutes les identités stockées dans le SDK, y compris l’identifiant Experience Cloud (ECID) et doit être utilisée avec modération ! |
| `getSessionId` | S.O. | Le gestionnaire de réponse `state:store` contient des informations relatives à la session. L’extension réseau Edge permet de la gérer en associant des éléments de magasin d’états non expirés aux demandes suivantes. |
| `setSessionId` | S.O. | Le gestionnaire de réponse `state:store` contient des informations relatives à la session. L’extension réseau Edge permet de la gérer en associant des éléments de magasin d’états non expirés aux demandes suivantes. |
| `getThirdPartyId` | S.O. | Utilisez l’API updateIdentities d’Identity pour l’extension de l’Edge Network afin de fournir la valeur de l’ID tiers. Ensuite, configurez l’espace de noms de l’ID tiers dans le flux de données. Pour plus d’informations, voir [la documentation mobile de Target Third Party Id](https://developer.adobe.com/client-sdks/edge/adobe-journey-optimizer-decisioning/#target-third-party-id). |
| `setThirdPartyId` | S.O. | Utilisez l’API updateIdentities d’Identity pour l’extension de l’Edge Network afin de fournir la valeur de l’ID tiers. Ensuite, configurez l’espace de noms de l’ID tiers dans le flux de données. Pour plus d’informations, voir [la documentation mobile de Target Third Party Id](https://developer.adobe.com/client-sdks/edge/adobe-journey-optimizer-decisioning/#target-third-party-id). |
| `getTntId` | S.O. | La gestion de la réponse `locationHint:result` contient les informations d’indicateur de l’emplacement cible. Il est supposé que Target Edge sera colocalisé avec Experience Edge. <br> <br>L’extension réseau Edge utilise l’indicateur d’emplacement EdgeNetwork pour déterminer la grappe réseau Edge à laquelle envoyer des requêtes. Pour partager des conseils d’emplacement réseau Edge sur les SDK (applications hybrides), utilisez les API `getLocationHint` et `setLocationHint` de l’extension Edge Network. Pour plus d’informations, voir [la `getLocationHint` documentation de l’API](https://developer.adobe.com/client-sdks/edge/edge-network/api-reference/#getlocationhint). |
| `setTntId` | S.O. | La gestion de la réponse `locationHint:result` contient les informations d’indicateur de l’emplacement cible. Il est supposé que Target Edge sera colocalisé avec Experience Edge. <br> <br>L’extension réseau Edge utilise l’indicateur d’emplacement EdgeNetwork pour déterminer la grappe réseau Edge à laquelle envoyer des requêtes. Pour partager des conseils d’emplacement réseau Edge sur les SDK (applications hybrides), utilisez les API `getLocationHint` et `setLocationHint` de l’extension Edge Network. Pour plus d’informations, voir [la `getLocationHint` documentation de l’API](https://developer.adobe.com/client-sdks/edge/edge-network/api-reference/#getlocationhint). |

## Paramètres de l’extension Target et équivalents de l’extension de prise de décision

L’extension Target dispose de [ paramètres configurables ](https://developer.adobe.com/client-sdks/solution/adobe-target/#configure-the-target-extension-in-the-data-collection-ui) qui sont [ configurés dans la zone de données ](https://developer.adobe.com/client-sdks/edge/adobe-journey-optimizer-decisioning/#adobe-experience-platform-data-collection-setup) avec l’extension de prise de décision.

| Extension Target | Extension de prise de décision | Notes |
| --- | --- | --- | 
| Code client | S.O. | Défini automatiquement par le serveur Edge à l’aide des détails de l’organisation IMS |
| Identifiant d’environnement | Identifiant d’environnement de Target | Configuré dans le flux de données |
| Propriété Workspace de Target | Jeton de propriété | Configuré dans le flux de données |
| Temporisation | Non configurable | Le délai d’attente avec l’extension de prise de décision est de 10 secondes. |
| Server Domain (Domaine du serveur) | Domaine Edge Network | Défini dans l’extension Adobe Experience Platform Edge Network |

>[!IMPORTANT]
>
> Conservez les paramètres de l’extension Target en place même après la migration du code de votre application vers l’extension de prise de décision. Cela permettra de s’assurer que Target continue de fonctionner pour les utilisateurs qui n’ont pas encore mis à jour leur application.

## Diagramme du système d’extension de prise de décision

Le diagramme suivant devrait vous aider à comprendre le flux de données à l’aide de l’extension Adobe Journey Optimizer - Decisioning.

![Adobe Target Edge Decisioning avec SDK Mobile côté client](assets/diagram.png)


>[!NOTE]
>
>Nous nous engageons à vous aider à réussir la migration de Target mobile de l’extension Target vers l’extension de prise de décision. Si vous rencontrez des obstacles lors de votre migration ou si vous pensez qu’il manque des informations essentielles dans ce guide, faites-le-nous savoir en publiant sur [cette discussion communautaire](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-target-from-at-js-to-web-sdk/m-p/575587#M463).
