---
title: Présentation de la migration - Migration de Target d’at.js 2.x vers Web SDK
description: Découvrez les principales différences entre at.js et Platform Web SDK et comment planifier vos efforts de migration.
exl-id: a8ed78e4-c8c2-4505-b4b5-e5d508f5ed87
source-git-commit: 286c85aa88d44574f00ded67f0de8e0c945a153e
workflow-type: tm+mt
source-wordcount: '796'
ht-degree: 1%

---

# Présentation de la migration de Target at.js vers Platform Web SDK

Le niveau d’effort à fournir pour migrer d’at.js vers Platform Web SDK dépend de la complexité de votre implémentation actuelle et des fonctionnalités de produit utilisées.

Quelle que soit la simplicité ou la complexité de votre implémentation, il est important de bien comprendre votre état actuel avant la migration. Ce guide vous aide à ventiler les composants de votre implémentation actuelle et à développer un plan gérable pour migrer chaque élément.

Le processus de migration implique les étapes clés suivantes :

1. Évaluez votre implémentation actuelle et déterminez une approche de migration
1. Configurer les composants initiaux pour la connexion à Adobe Experience Platform Edge Network
1. Mettez à jour l’implémentation de base pour remplacer at.js par Platform Web SDK
1. Améliorez l’implémentation de Platform Web SDK pour vos cas d’utilisation spécifiques. Cela peut impliquer la transmission de paramètres supplémentaires, la prise en compte des modifications d’affichage des applications monopages (SPA), l’utilisation de jetons de réponse, etc.
1. Mettre à jour des objets dans l’interface Target, tels que des scripts de profil, des activités et des définitions d’audience
1. Validez la mise en œuvre finale avant d’effectuer le changement dans votre environnement de production.

## Principales différences entre at.js et Platform Web SDK

Avant de commencer le processus de migration, il est important de comprendre les différences entre at.js et le SDK web de Platform.

### Différences opérationnelles

Platform Web SDK combine les fonctionnalités de plusieurs applications Adobe en une seule bibliothèque. Cette approche unifiée signifie que vous devez tenir compte des responsabilités et des processus au sein de l’équipe afin d’assurer une implémentation saine.

| | Target at.js 2.x | SDK Web de Platform |
|---|---|---|
| Propriété | La bibliothèque at.js est indépendante des autres bibliothèques d’applications. Les personnalisations et la propriété de ces bibliothèques disparates peuvent correspondre à différentes équipes de l’organisation. | La bibliothèque SDK Web Platform et les données transmises sont unifiées pour toutes les applications Adobe. La propriété de l’implémentation de Platform Web SDK doit représenter les parties prenantes de toutes les applications en aval. |
| Maintenance | Des équipes distinctes peuvent travailler sur les améliorations de l’implémentation pour chaque application Adobe, comme Target et Analytics. | Idéalement, une seule équipe doit être responsable des améliorations qui affectent l’implémentation de Platform Web SDK. |
| Processus | Les modifications apportées à une implémentation de Target peuvent suivre un processus dont la cadence ou les exigences en matière d’assurance qualité sont différentes de celles d’autres applications telles qu’Analytics. | Les modifications apportées à une implémentation de Platform Web SDK doivent prendre en compte toutes les applications en aval. Le processus d’assurance qualité et de publication doit être adapté en conséquence. |
| Collaboration | Les données spécifiques à Target peuvent être transmises directement dans les appels de Target. Selon la mise en œuvre, il peut y avoir d’autres appels Target. Cela n’a aucun impact direct sur les données Adobe Analytics et la coordination avec l’équipe Analytics n’est pas aussi essentielle. | Les données transmises dans les appels de SDK Web Platform peuvent être transférées vers Target et Analytics. La coordination entre les équipes est nécessaire pour s’assurer que les modifications n’ont pas d’impact négatif sur une application spécifique. |

### Différences techniques

Platform Web SDK n’est pas une évolution de la bibliothèque at.js de Target. Il s’agit d’une nouvelle approche unifiée pour la mise en œuvre de toutes les applications Adobe pour le canal web. Il existe plusieurs différences techniques à connaître.

| | Target at.js 2.x | SDK Web de Platform |
|---|---|---|
| Fonctionnalité de bibliothèque | Fonctionnalité de Target fournie par at.js Intégrations à d’autres applications fournies par Visitor.js et AppMeasurement.js | Fonctionnalité pour toutes les applications Adobe fournies par une seule bibliothèque SDK web Platform : alloy.js |
| Performances | at.js fait partie des nombreuses bibliothèques qui doivent être chargées pour une intégration correcte entre les applications. Le temps de chargement n’est donc pas optimal. | Platform Web SDK est une bibliothèque allégée unique qui rend inutiles plusieurs bibliothèques spécifiques à l’application, ce qui se traduit par de meilleures performances de chargement des pages. |
| Demandes | Appels distincts pour chaque application Adobe. Les appels Target sont largement indépendants des autres appels réseau. | Un seul appel pour toutes les applications Adobe. Les modifications apportées aux données transmises dans ces appels peuvent avoir un impact sur plusieurs applications en aval. |
| Ordre de chargement | Une intégration correcte avec d’autres applications Adobe nécessite un ordre de chargement spécifique des bibliothèques et des appels réseau. | Une intégration correcte ne repose pas sur l’assemblage de données provenant d’appels réseau disparates spécifiques à une application. L’ordre de chargement n’est donc pas un problème. |
| Edge Network | Utilise Adobe Experience Cloud Edge Network (tt.omtrdc.net), éventuellement avec un CNAME spécifique à Target. | Utilise l’Edge Network Adobe Experience Platform (edge.adobedc.net), éventuellement avec un seul CNAME. |
| Terminologie de base | dénomination d’at.js : <br> - <br> `mbox` - événement `pageLoad` (mbox globale) <br> - `offer` | Équivalent de Platform Web SDK : <br> - `decisionScope` <br> - `__view__` decisionScope <br> - `proposition` |

### Vue d’ensemble des vidéos

La vidéo suivante donne un aperçu de Adobe Experience Platform Web SDK et de Adobe Experience Platform Edge Network.

>[!VIDEO](https://video.tv.adobe.com/v/34141/?learn=on&enablevpops)

Maintenant que vous comprenez les différences de haut niveau entre at.js et le SDK web de Platform, vous pouvez [planifier la migration](plan-migration.md).

>[!NOTE]
>
>Nous nous engageons à vous aider à réussir la migration de Target d’at.js vers Web SDK. Si vous rencontrez des obstacles avec votre migration ou si vous pensez qu&#39;il manque des informations essentielles dans ce guide, veuillez nous le faire savoir en postant dans [cette discussion communautaire](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-target-from-at-js-to-web-sdk/m-p/575587#M463).
