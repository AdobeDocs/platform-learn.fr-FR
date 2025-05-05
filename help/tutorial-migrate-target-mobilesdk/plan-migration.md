---
title: Planifiez la migration - Migrez l’implémentation d’Adobe Target dans votre application mobile vers l’extension Adobe Journey Optimizer - Decisioning
description: Découvrez les principales différences entre at.js et Platform Web SDK et comment planifier vos efforts de migration.
exl-id: 86849319-d2ad-4338-aa1a-d307d8807d4a
source-git-commit: 2ebad2014d4c29a50af82328735258958893b42c
workflow-type: tm+mt
source-wordcount: '315'
ht-degree: 0%

---

# Planifier la migration

Le niveau d’effort à fournir pour migrer de l’extension Target à l’extension Decisioning dépend de la complexité de votre implémentation actuelle et des fonctionnalités Target utilisées.

Quelle que soit la simplicité ou la complexité de votre implémentation, il est important de bien comprendre votre état actuel avant la migration. Ce guide vous aide à ventiler les composants de votre implémentation actuelle et à développer un plan gérable pour migrer chaque élément.

Le processus de migration implique les étapes clés suivantes :

1. Évaluez votre implémentation actuelle et déterminez une approche de migration
1. Configurer les composants initiaux pour la connexion à Adobe Experience Platform Edge Network
1. Mettez à jour la mise en œuvre de base pour remplacer l’extension Target par l’extension Decisioning
1. Améliorez l’implémentation de SDK pour vos cas d’utilisation spécifiques. Cela peut impliquer la transmission de paramètres supplémentaires, l’utilisation de jetons de réponse, etc.
1. Mettre à jour des objets dans l’interface Target, tels que des scripts de profil, des activités et des définitions d’audience
1. Validez la mise en œuvre finale avant d’effectuer le changement dans votre application de production.

>[!INFO]
>
>Dans l’écosystème Adobe Experience Platform Mobile SDK, les extensions sont implémentées par des SDK importés dans vos applications, qui peuvent porter des noms différents :
>
> * **Target SDK** met en œuvre l’extension **Adobe Target**
> * **Optimiser SDK** implémente l’extension **Adobe Journey Optimizer - Decisioning**


Ensuite, passez en revue la comparaison détaillée [de l’extension Target et de l’extension Decisioning](detailed-comparison.md) pour mieux comprendre les différences techniques et identifier les domaines nécessitant une attention supplémentaire.

>[!NOTE]
>
>Nous nous engageons à vous aider à réussir votre migration mobile de Target de l’extension Target vers l’extension Decisioning. Si vous rencontrez des obstacles avec votre migration ou si vous pensez qu&#39;il manque des informations essentielles dans ce guide, veuillez nous le faire savoir en postant dans [cette discussion communautaire](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-adobe-target-to-mobile-sdk-on-edge/m-p/747484?profile.language=fr#M625).
