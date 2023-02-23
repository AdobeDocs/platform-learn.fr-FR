---
title: Présentation de la migration | Migration de Target depuis at.js 2.x vers le SDK Web
description: Découvrez les principales différences entre at.js et le SDK Web Platform et comment planifier votre effort de migration.=
source-git-commit: 287ebcb275c4fca574dbd6cdf7e07ba4268bddb5
workflow-type: tm+mt
source-wordcount: '802'
ht-degree: 1%

---

# Présentation de la migration d’at.js vers le SDK Web Platform

Le niveau d’effort nécessaire pour migrer d’at.js vers le SDK Web Platform dépend de la complexité de votre mise en oeuvre actuelle et des fonctionnalités du produit utilisées.

Quelle que soit la simplicité ou la complexité de votre mise en oeuvre, il est important de bien comprendre votre état actuel avant la migration. Ce guide vous aide à ventiler les composants de votre mise en oeuvre actuelle et à élaborer un plan gérable pour la migration de chaque élément.

Le processus de migration comprend les étapes clés suivantes :

1. Évaluer votre mise en oeuvre actuelle et déterminer une approche de migration
1. Configuration des composants initiaux pour la connexion au réseau Adobe Experience Platform Edge
1. Mettez à jour l’implémentation de base pour remplacer at.js par le SDK Web Platform.
1. Améliorez la mise en oeuvre du SDK Web Platform pour vos cas d’utilisation spécifiques. Cela peut impliquer la transmission de paramètres supplémentaires, la prise en compte des modifications d’affichage d’une seule page (SPA), l’utilisation de jetons de réponse, etc.
1. Mise à jour d’objets dans l’interface de Target, tels que les scripts de profil, les activités et les définitions d’audience
1. Validation de la mise en oeuvre finale avant d’effectuer le changement dans votre environnement de production

## Principales différences entre at.js et le SDK Web Platform

Avant de commencer le processus de migration, il est important de comprendre les différences entre at.js et le SDK Web Platform.

### Différences opérationnelles

Le SDK Web Platform combine les fonctionnalités de plusieurs applications Adobe en une seule bibliothèque. Cette approche unifiée signifie que vous devez tenir compte des responsabilités et des processus entre les équipes pour garantir une mise en oeuvre saine.

|  | Target at.js 2.x | SDK Web de Platform |
|---|---|---|
| Propriété | La bibliothèque at.js est indépendante des autres bibliothèques d’applications. Les personnalisations et la propriété de ces bibliothèques disparates peuvent s’aligner sur différentes équipes de l’entreprise. | La bibliothèque SDK Web Platform et les données transmises sont unifiées pour toutes les applications Adobe. La propriété de l’implémentation du SDK Web Platform doit représenter les parties prenantes de toutes les applications en aval. |
| Maintenance | Des équipes distinctes peuvent travailler sur les améliorations de mise en oeuvre pour chaque application d’Adobe, telles que Target et Analytics. | Idéalement, une seule équipe doit être responsable des améliorations qui affectent l’implémentation du SDK Web Platform. |
| Processus | Les modifications apportées à une mise en oeuvre de Target peuvent suivre un processus dont la cadence ou les exigences d’assurance qualité sont différentes de celles d’autres applications telles qu’Analytics. | Les modifications apportées à une implémentation du SDK Web Platform doivent prendre en compte toutes les applications en aval, et le processus d’assurance qualité et de publication doit être adapté en conséquence. |
| Collaboration | Les données spécifiques à Target peuvent être transmises directement dans les appels Target. Selon l’implémentation, il peut y avoir d’autres appels Target. Cela n’a aucun impact direct sur les données Adobe Analytics et la coordination avec l’équipe d’analyse n’est pas aussi essentielle. | Les données transmises dans les appels du SDK Web Platform peuvent être transférées à Target et à Analytics. Une coordination entre les équipes est nécessaire pour s’assurer que les modifications n’ont pas d’incidence négative sur une application spécifique. |

### Différences techniques

Le SDK Web Platform n’est pas une évolution de la bibliothèque at.js de Target. Il s’agit d’une nouvelle approche unifiée pour la mise en oeuvre de toutes les applications Adobe pour le canal web. Il y a plusieurs différences techniques à connaître.

|  | Target at.js 2.x | SDK Web de Platform |
|---|---|---|
| Fonctionnalité de bibliothèque | Fonctionnalité de Target fournie par at.js. Intégrations à d’autres applications fournies par Visitor.js et AppMeasurement.js | Fonctionnalité pour toutes les applications Adobe fournies par une seule bibliothèque SDK Web Platform : alloy.js |
| Performance | at.js est l’une des nombreuses bibliothèques qui doivent être chargées pour une intégration correcte dans les applications. Cela se traduit par un temps de chargement inférieur à la durée optimale. | Le SDK Web Platform est une bibliothèque légère unique qui élimine la nécessité de plusieurs bibliothèques spécifiques à l’application, ce qui se traduit par de meilleures performances de chargement de page. |
| Demandes | Séparez les appels pour chaque application d’Adobe. Les appels Target sont largement indépendants des autres appels réseau. | Un seul appel pour toutes les applications Adobe. Les modifications apportées aux données transmises dans ces appels peuvent avoir un impact sur plusieurs applications en aval. |
| Ordre de chargement | Une intégration correcte avec d’autres applications Adobe nécessite un ordre de chargement spécifique de bibliothèques et d’appels réseau. | Une intégration correcte ne repose pas sur l’assemblage de données à partir d’appels réseau disparates spécifiques à l’application. Par conséquent, l’ordre de chargement n’est pas un problème. |
| Edge Network | Utilise le réseau Adobe Experience Cloud Edge (tt.omtrdc.net), éventuellement avec un CNAME spécifique à Target. | Utilise le réseau Edge Adobe Experience Platform (edge.adobedc.net), éventuellement avec un seul CNAME. |
| Terminologie de base | Nom d’at.js : <br> - `mbox` <br> - `pageLoad` event (mbox globale) <br> - `offer` | SDK Web Platform équivalent : <br> - `decisionScope` <br> - `__view__` décisionScope <br> - `proposition` |

### Vue d’ensemble des vidéos

La vidéo suivante présente un aperçu du SDK web Adobe Experience Platform et du réseau Adobe Experience Platform Edge.

>[!VIDEO](https://video.tv.adobe.com/v/34141/?quality=12&learn=on)

Maintenant que vous comprenez les différences de haut niveau entre at.js et le SDK Web Platform, vous pouvez [planifier la migration](plan-migration.md).

>[!NOTE]
>
>Nous nous engageons à vous aider à réussir la migration de Target d’at.js vers le SDK Web. Si vous rencontrez des obstacles lors de votre migration ou si vous pensez qu’il manque des informations essentielles dans ce guide, faites-le nous savoir en publiant sur [cette discussion communautaire](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-target-from-at-js-to-web-sdk/m-p/575587#M463).