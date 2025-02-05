---
title: Planifier la migration - Migrer d’Adobe Target vers Adobe Journey Optimizer - Extension mobile Decisioning
description: Découvrez les principales différences entre at.js et Platform Web SDK et comment planifier vos efforts de migration.
exl-id: 86849319-d2ad-4338-aa1a-d307d8807d4a
source-git-commit: f3fd5f45412900dcb871bc0b346ce89108fa8913
workflow-type: tm+mt
source-wordcount: '644'
ht-degree: 0%

---

# Planifier la migration

Le niveau d’effort à fournir pour migrer de l’extension Target à l’extension Decisioning dépend de la complexité de votre implémentation actuelle et des fonctionnalités de produit utilisées.

Quelle que soit la simplicité ou la complexité de votre implémentation, il est important de bien comprendre votre état actuel avant la migration. Ce guide vous aide à ventiler les composants de votre implémentation actuelle et à développer un plan gérable pour migrer chaque élément.

Le processus de migration implique les étapes clés suivantes :

1. Évaluez votre implémentation actuelle et déterminez une approche de migration
1. Configurer les composants initiaux pour la connexion à l’Edge Network Adobe Experience Platform
1. Mettez à jour la mise en œuvre de base pour remplacer les extensions Target et Decisioning
1. Améliorez l’implémentation de SDK pour vos cas d’utilisation spécifiques. Cela peut impliquer la transmission de paramètres supplémentaires, l’utilisation de jetons de réponse, etc.
1. Mettre à jour des objets dans l’interface Target, tels que des scripts de profil, des activités et des définitions d’audience
1. Validez la mise en œuvre finale avant d’effectuer le changement dans votre environnement de production.

## Principales différences entre l’extension Target et l’extension Decisioning

Avant de commencer le processus de migration, il est important de comprendre les différences entre l’extension Target et l’extension Decisioning.

### Différences opérationnelles

| | Target at.js 2.x | SDK Web de Platform |
|---|---|---|
| Processus | Les modifications apportées à une implémentation de Target peuvent suivre un processus dont la cadence ou les exigences en matière d’assurance qualité sont différentes de celles d’autres applications telles qu’Analytics. | Les modifications apportées à une implémentation d’extension Decisioning doivent prendre en compte toutes les applications en aval. Le processus d’assurance qualité et de publication doit être adapté en conséquence. |
| Collaboration | Les données spécifiques à Target peuvent être transmises directement dans les appels de Target. Si la source de création de rapports Target est Adobe Analytics, les données spécifiques à Target peuvent également être transmises à Adobe Analytics lorsque des méthodes de suivi appropriées dans l’extension Target sont appelées pour l’affichage et l’interaction du contenu de Target. | Les données transmises dans les appels d’extension Decisioning peuvent être transférées vers Target et Analytics si la source de création de rapports Target est Adobe Analytics, si Adobe Analytics est activé dans le flux de données et si les méthodes de suivi appropriées dans l’extension Decisioning sont appelées lorsque le contenu Target est affiché et qu’il interagit avec celui-ci. |

### Différences techniques

| | Extension Target | Extension Decisioning |
|---|---|---|
| Dépendances | Dépend uniquement de Mobile Core SDK | Dépend de Mobile Core et Edge Network SDK |
| Fonctionnalité de bibliothèque | Prend uniquement en charge la récupération de contenu d’Adobe Target | Prise en charge de la récupération de contenu à partir d’Adobe Target et d’Offer decisioning |
| Demandes | Les appels Target sont largement indépendants des autres appels réseau | Les appels réseau Target sont mis en file d’attente avec les appels réseau pour d’autres solutions basées sur Edge, telles que Messaging dans Edge SDK, et exécutés en série. |
| Edge Network | Utilise la valeur du serveur Target ou l’Edge Network Adobe Experience Cloud avec le code client (clientcode.tt.omtrdc.net), tous deux spécifiés dans la [configuration de Target](https://developer.adobe.com/client-sdks/solution/adobe-target/#configure-the-target-extension-in-the-data-collection-ui) dans l’interface utilisateur de collecte de données | Utilise le domaine réseau Edge spécifié dans la configuration Adobe Experience Platform [Edge Network ](https://developer.adobe.com/client-sdks/edge/edge-network/#configure-the-edge-network-extension-in-data-collection-ui) dans l’interface utilisateur de collecte de données. |
| Terminologie de base | mbox, TargetParameters | DecisionScope, mappage (Android)/dictionnaire (iOS) pour les paramètres cibles |
| Contenu par défaut | Permet de transmettre le contenu par défaut côté client dans TargetRequest qui est renvoyé si l’appel réseau échoue ou génère une erreur. | N’autorise pas la transmission de contenu par défaut côté client. Ne renvoie aucun contenu si l’appel réseau échoue ou génère une erreur. |
| Paramètres de la cible | Permet de transmettre des paramètres Target globaux par requête et différents paramètres Target par mbox | Permet uniquement de transmettre des paramètres Target globaux par requête. |

Ensuite, passez en revue la comparaison détaillée [de l’extension Target et de l’extension Decisioning](detailed-comparison.md) pour mieux comprendre les différences techniques et identifier les domaines nécessitant une attention supplémentaire.

>[!NOTE]
>
>Nous nous engageons à vous aider à réussir votre migration mobile de Target de l’extension Target vers l’extension Decisioning. Si vous rencontrez des obstacles avec votre migration ou si vous pensez qu&#39;il manque des informations essentielles dans ce guide, veuillez nous le faire savoir en postant dans [cette discussion communautaire](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-target-from-at-js-to-web-sdk/m-p/575587#M463).
