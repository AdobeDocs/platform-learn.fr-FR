---
title: Planifiez la migration - Migrez l’implémentation d’Adobe Target dans votre application mobile vers l’extension Offer Decisioning et Target
description: Découvrez les principales différences entre at.js et Platform Web SDK et comment planifier vos efforts de migration.
exl-id: 86849319-d2ad-4338-aa1a-d307d8807d4a
source-git-commit: 876e664a213aec954105bf2d5547baab5d8a84ea
workflow-type: tm+mt
source-wordcount: '327'
ht-degree: 0%

---

# Planifier la migration

Le niveau d’effort à fournir pour migrer de l’extension Target à l’extension Offer Decisioning et Target dépend de la complexité de votre implémentation actuelle et des fonctionnalités de Target utilisées.

Quelle que soit la simplicité ou la complexité de votre implémentation, il est important de bien comprendre votre état actuel avant la migration. Ce guide vous aide à ventiler les composants de votre implémentation actuelle et à développer un plan gérable pour migrer chaque élément.

Le processus de migration implique les étapes clés suivantes :

1. Évaluez votre implémentation actuelle et déterminez une approche de migration
1. Configurer les composants initiaux pour la connexion à Adobe Experience Platform Edge Network
1. Mettez à jour la mise en œuvre de base pour remplacer l’extension Target par les extensions Offer Decisioning et Target
1. Améliorez l’implémentation de SDK pour vos cas d’utilisation spécifiques. Cela peut impliquer la transmission de paramètres supplémentaires, l’utilisation de jetons de réponse, etc.
1. Mettre à jour des objets dans l’interface Target, tels que des scripts de profil, des activités et des définitions d’audience
1. Validez la mise en œuvre finale avant d’effectuer le changement dans votre application de production.

>[!INFO]
>
>Dans l’écosystème Adobe Experience Platform Mobile SDK, les extensions sont implémentées par des SDK importés dans vos applications, qui peuvent porter des noms différents :
>
> * **Target SDK** met en œuvre l’extension **Adobe Target**
> * **Optimiser SDK** implémente l’extension **Offer Decisioning et Target**


Ensuite, passez en revue la comparaison détaillée [de l’extension Target et de l’extension Offer Decisioning et Target](detailed-comparison.md) afin de mieux comprendre les différences techniques et d’identifier les domaines nécessitant une attention particulière.

>[!NOTE]
>
>Nous nous engageons à vous aider à réussir votre migration mobile de Target vers l’extension Offer Decisioning et Target. Si vous rencontrez des obstacles avec votre migration ou si vous pensez qu&#39;il manque des informations essentielles dans ce guide, veuillez nous le faire savoir en postant dans [cette discussion communautaire](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-adobe-target-to-mobile-sdk-on-edge/m-p/747484?profile.language=fr#M625).
