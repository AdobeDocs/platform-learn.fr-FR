---
title: 'Planification : migration de Target dans les applications mobiles de l’extension Target vers l’extension Optimiser'
description: Découvrez comment planifier votre mise en oeuvre Adobe Target d’at.js 2.x au SDK Web Adobe Experience Platform.
source-git-commit: 009548969b88d1bfa6eac23f65b1ca2144f27c34
workflow-type: tm+mt
source-wordcount: '199'
ht-degree: 0%

---

# Planification de la migration de Target vers l’extension Optimisation

Avant de mettre à niveau Target de l’extension Target vers l’extension Optimiser de votre application mobile, vous devez évaluer votre mise en oeuvre actuelle.

## Évaluation de la mise en oeuvre actuelle de l’extension Target

La première étape d’une migration réussie consiste à maîtriser la mise en oeuvre de votre extension Target actuelle. Il existe des fonctionnalités, des fonctions et du code personnalisé que vous pouvez utiliser qui nécessitent des mises à jour. Tenez compte des points suivants lors de votre évaluation :

### Quelles fonctionnalités sont prises en charge ?

<!--Platform Web SDK is under continuous active development and features and enhancements are added regularly. As you evaluate your current at.js implementation, refer to the [supported use cases](https://github.com/orgs/adobe/projects/18/views/1) page for the latest information.-->

### Quelles fonctions utilises-tu aujourd&#39;hui ?

<!--Platform Web SDK is a new library that consolidates all Adobe solutions for the websites into a single SDK. This enables tighter integration and enables new capabilities unique to Adobe Experience Platform. However, this also means at.js functions are not backwards compatible with Platform Web SDK. As you evaluate your current implementation, make note of the following:

- at.js functions such as `getOffer()` and `applyOffer()`
- Modifications to Target's global settings
- Integration with Adobe Analytics
- Use of a flicker mitigation script
- Use of response tokens
- Use of mbox, profile, and entity parameters
- Custom code unique to your implementation-->

### Quelle approche de migration adopterez-vous ?

<!--Once you have revisited your at.js implementation, you need to determine a migration approach. There are two options:

- Migrate all Adobe applications at once across the entire site
- Migrate on a page-by-page basis

Because Platform Web SDK combines and enables multiple Adobe applications, you must coordinate the Target migration of other Adobe applications like Analytics and Audience Manager. All Adobe libraries on a given page should be migrated at the same time. A mixed implementation of Platform Web SDK for Target and AppMeasurement for Analytics on a particular page is not supported. However, a mixed implementation across different pages is supported, for example Platform Web SDK on page A, and at.js with AppMeasurement on page B.

As you migrate, you should plan on following your company's process for testing and releasing new code and use things like development, qa, and staging environments before you release to production.-->

<!--
>[!CAUTION]
>
>Redirect offers are not supported in page-by-page migrations if redirecting from a page with one library to a page with a different library
-->


Ensuite, passez en revue la [comparaison détaillée de l’extension Target et de l’extension Optimiser](detailed-comparison.md) pour mieux comprendre les différences techniques et identifier les domaines nécessitant un focus supplémentaire.

>[!NOTE]
>
>Nous nous engageons à vous aider à réussir la migration de Target mobile de l’extension Target vers l’extension Optimize. Si vous rencontrez des obstacles lors de votre migration ou si vous pensez qu’il manque des informations essentielles dans ce guide, faites-le-nous savoir en publiant sur [cette discussion communautaire](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-target-from-at-js-to-web-sdk/m-p/575587#M463).
