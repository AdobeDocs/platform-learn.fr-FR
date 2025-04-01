---
title: Comparaison de l’extension Target à l’extension Decisioning
description: Découvrez les différences entre l’extension Target et l’extension Decisioning, notamment les fonctionnalités, les fonctions, les paramètres et le flux de données.
exl-id: 6c854049-4126-45cf-8b2b-683cf29549f3
source-git-commit: 24effdb0905c6fd146a80031e0a39eed9672306d
workflow-type: tm+mt
source-wordcount: '791'
ht-degree: 3%

---

# Comparaison de l’extension Target à l’extension Decisioning

L’extension Adobe Journey Optimizer - Decisioning diffère de l’extension Adobe Target pour les applications mobiles. Les tableaux suivants servent de référence pour vous aider à évaluer les aspects de votre implémentation sur lesquels vous devrez peut-être vous concentrer au cours du processus de migration.

Après avoir consulté les informations ci-dessous et évalué votre implémentation technique actuelle de l’extension Target, vous devriez être en mesure de comprendre les éléments suivants :

- Les fonctionnalités de Target prises en charge par Adobe Journey Optimizer - Prise de décision
- Quelles fonctions d’extension Adobe Target ont des équivalents Adobe Journey Optimizer - Prise de décision
- Application des paramètres de Target avec Adobe Journey Optimizer - Prise de décision
- Flux de données à l’aide de l’extension Adobe Journey Optimizer - Decisioning

## Différences opérationnelles

| | Extension Target | Extension Decisioning |
|---|---|---|
| Processus | Les modifications apportées à une implémentation de Target peuvent suivre un processus dont la cadence ou les exigences en matière d’assurance qualité sont différentes de celles d’autres applications telles qu’Analytics. | Les modifications apportées à une implémentation d’extension Decisioning doivent prendre en compte toutes les applications en aval. Le processus d’assurance qualité et de publication doit être adapté en conséquence. |
| Collaboration | Les données spécifiques à Target peuvent être transmises directement dans les appels de Target. Si la source de création de rapports Target est Adobe Analytics (A4T), les données spécifiques à Target peuvent également être transmises à Adobe Analytics lorsque des méthodes de suivi appropriées dans l’extension Target sont appelées pour l’affichage du contenu de Target et l’interaction. | Les données transmises dans les appels de l’extension Decisioning peuvent être transférées vers Target et Analytics si la source de création de rapports cible est Adobe Analytics (A4T), si Adobe Analytics est activé dans le flux de données et si les méthodes de suivi appropriées dans l’extension Decisioning sont appelées lorsque le contenu Target est affiché et qu’il interagit avec celui-ci. |

## Différences de base

| | Extension Target | Extension Decisioning |
|---|---|---|
| Dépendances | Dépend uniquement de Mobile Core SDK | Dépend de Mobile Core et Edge Network SDK |
| Fonctionnalité de bibliothèque | Prend uniquement en charge la récupération de contenu d’Adobe Target | Prise en charge de la récupération de contenu d’Adobe Target et d’Offer Decisioning |
| Demandes | Les appels Target sont largement indépendants des autres appels réseau | Les appels réseau Target sont mis en file d’attente avec les appels réseau pour d’autres solutions basées sur Edge, telles que Messaging dans Edge SDK, et exécutés en série. |
| Edge Network | Utilise la valeur du serveur Target ou l’Edge Network Adobe Experience Cloud avec le code client (clientcode.tt.omtrdc.net), tous deux spécifiés dans la [configuration de Target](https://developer.adobe.com/client-sdks/solution/adobe-target/#configure-the-target-extension-in-the-data-collection-ui) dans l’interface utilisateur de collecte de données | Utilise le domaine réseau Edge spécifié dans la configuration Adobe Experience Platform [Edge Network](https://developer.adobe.com/client-sdks/edge/edge-network/#configure-the-edge-network-extension-in-data-collection-ui) dans l’interface utilisateur de collecte de données. |
| Terminologie de base | mbox, TargetParameters | DecisionScope, mappage (Android)/dictionnaire (iOS) pour les paramètres Target |
| Contenu par défaut | Permet de transmettre le contenu par défaut côté client dans TargetRequest qui est renvoyé si l’appel réseau échoue ou génère une erreur. | N’autorise pas la transmission de contenu par défaut côté client. Ne renvoie aucun contenu si l’appel réseau échoue ou génère une erreur. |
| Paramètres de la cible | Permet de transmettre des paramètres Target globaux par requête et différents paramètres Target par mbox | Permet uniquement de transmettre des paramètres Target globaux par requête. |



## Comparaison des fonctionnalités

| Fonctionnalité | Extension Target | Extension Decisioning (Target via Edge) |
|---|---|---|
| Mode de prérécupération | Pris en charge | Pris en charge |
| Mode d’exécution | Pris en charge | Non pris en charge |
| Paramètres personnalisés | Pris en charge | Pris en charge* |
| Paramètres de profil | Pris en charge | Pris en charge* |
| Paramètres de l’entité | Pris en charge | Pris en charge* |
| Audiences cibles | Pris en charge | Pris en charge |
| Audiences Real-Time CDP | Non pris en charge | Pris en charge |
| Attributs Real-Time CDP | Non pris en charge | Pris en charge |
| Mesures de cycle de vie | Pris en charge | Pris en charge via les règles de collecte de données |
| thirdPartyId (mbox3rdPartyId) | Pris en charge | Pris en charge via la carte des identités et l’espace de noms des identifiants tiers cibles dans le flux de données |
| Notifications (affichage, clic) | Pris en charge | Pris en charge |
| Jetons de réponse | Pris en charge | Pris en charge |
| Aperçus mobiles (mode AQ) | Pris en charge | Prise en charge limitée d’Assurance |

>[!IMPORTANT]
>
> \* Les paramètres envoyés dans une requête s’appliquent à toutes les portées de la requête. Si vous devez définir des paramètres différents pour différentes portées, vous devez effectuer des requêtes supplémentaires.



## Légendes dignes de mention

>[!NOTE]
>
>Conservez la configuration et les paramètres des balises d’extension Target même après avoir migré le code de votre application vers l’extension Decisioning. Cela permet de s’assurer que Target continue de fonctionner pour les clients qui n’ont pas encore mis à jour l’application vers la nouvelle version.
>
>Si vous utilisez l’intégration Analytics for Target (A4T), veillez également à migrer votre implémentation Analytics avec l’extension Edge Bridge au même moment que vous migrez votre implémentation Target vers l’extension Decisioning.





>[!IMPORTANT]
>
> Conservez les paramètres de l’extension Target même après avoir migré le code de votre application vers l’extension Decisioning. Cela permet de s’assurer que Target continue de fonctionner pour les utilisateurs qui n’ont pas encore mis à jour leur application.

## Diagramme du système d’extension Decisioning

Le diagramme suivant doit vous aider à comprendre le flux de données à l’aide de l’extension Adobe Journey Optimizer - Prise de décision .

![Prise de décision Adobe Target Edge avec SDK mobile côté client](assets/diagram.png)


>[!NOTE]
>
>Nous nous engageons à vous aider à réussir votre migration mobile de Target de l’extension Target vers l’extension Decisioning. Si vous rencontrez des obstacles avec votre migration ou si vous pensez qu&#39;il manque des informations essentielles dans ce guide, veuillez nous le faire savoir en postant dans [cette discussion communautaire](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-target-from-at-js-to-web-sdk/m-p/575587#M463).
