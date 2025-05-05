---
title: Planification - Migration de Target depuis at.js 2.x vers le SDK Web
description: Découvrez comment planifier votre mise en oeuvre Adobe Target d’at.js 2.x au SDK Web Adobe Experience Platform.
exl-id: 0e8f9cde-f361-4f69-886d-aad3074cd9b2
source-git-commit: d4308b68d6974fe47eca668dd16555d15a8247c9
workflow-type: tm+mt
source-wordcount: '480'
ht-degree: 1%

---

# Planification de la migration d’at.js vers le SDK Web Platform

Avant de procéder à la mise à niveau vers le SDK Web Platform sur votre site, vous devez évaluer votre mise en oeuvre actuelle.

## Évaluation de l’implémentation actuelle d’at.js

La première étape d’une migration réussie consiste à maîtriser l’implémentation actuelle d’at.js Target. Il existe des fonctionnalités, des fonctions et du code personnalisé que vous pouvez utiliser qui nécessitent des mises à jour. Tenez compte des points suivants lors de votre évaluation :

### Quelles fonctionnalités sont prises en charge ?

Le SDK Web Platform est en cours de développement actif continu et des fonctionnalités et améliorations sont régulièrement ajoutées. Pour évaluer votre mise en oeuvre actuelle d’at.js, reportez-vous à la page [Cas d’utilisation pris en charge](https://github.com/orgs/adobe/projects/18/views/1) pour obtenir les informations les plus récentes.

### Quelles fonctions utilises-tu aujourd&#39;hui ?

Le SDK Web Platform est une nouvelle bibliothèque qui regroupe toutes les solutions d’Adobe pour les sites web en un seul SDK. Cela permet une intégration plus étroite et permet de nouvelles fonctionnalités propres à Adobe Experience Platform. Cependant, cela signifie également que les fonctions at.js ne sont pas rétrocompatibles avec le SDK Web Platform. Lorsque vous évaluez votre mise en oeuvre actuelle, prenez note des points suivants :

- Fonctions d’at.js telles que `getOffer()` et `applyOffer()`
- Modifications des paramètres globaux de Target
- Intégration avec Adobe Analytics
- Utilisation d’un script de réduction du scintillement
- Utilisation des jetons de réponse
- Utilisation des paramètres de mbox, de profil et d’entité
- Code personnalisé unique à votre implémentation

### Quelle approche de migration adopterez-vous ?

Une fois que vous avez revu votre implémentation d’at.js, vous devez déterminer une approche de migration. Deux options sont disponibles :

- Migration de toutes les applications d’Adobe à la fois sur l’ensemble du site
- Migrer page par page

Comme le SDK Web de Platform combine et active plusieurs applications d’Adobe, vous devez coordonner la migration Target d’autres applications d’Adobe telles qu’Analytics et Audience Manager. Toutes les bibliothèques d’Adobe d’une page donnée doivent être migrées en même temps. Une mise en oeuvre mixte du SDK Web Platform pour Target et d’AppMeasurement pour Analytics sur une page spécifique n’est pas prise en charge. Cependant, une mise en oeuvre mixte sur différentes pages est prise en charge, par exemple le SDK Web Platform sur la page A et at.js avec AppMeasurement sur la page B.

Au fur et à mesure de la migration, vous devriez prévoir de suivre le processus de test et de publication de nouveau code de votre entreprise et d’utiliser des éléments tels que les environnements de développement, de test et d’évaluation avant de passer en production.

>[!CAUTION]
>
>Les offres de redirection ne sont pas prises en charge dans les migrations page par page si la redirection d’une page avec une bibliothèque vers une page avec une bibliothèque différente est effectuée.


Ensuite, passez en revue la [comparaison détaillée d’at.js avec le SDK Web Platform](detailed-comparison.md) pour mieux comprendre les différences techniques et identifier les domaines nécessitant un focus supplémentaire.

>[!NOTE]
>
>Nous nous engageons à vous aider à réussir la migration de Target d’at.js vers le SDK Web. Si vous rencontrez des obstacles lors de votre migration ou si vous pensez qu’il manque des informations essentielles dans ce guide, faites-le-nous savoir en publiant sur [cette discussion communautaire](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-target-from-at-js-to-web-sdk/m-p/575587?profile.language=fr#M463).
