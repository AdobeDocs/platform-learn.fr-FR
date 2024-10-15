---
title: Comparaison de l’extension Target avec l’extension Optimisation
description: Découvrez les différences entre at.js 2.x et le SDK Web Platform, notamment les fonctionnalités, les fonctions, les paramètres et le flux de données.
source-git-commit: 009548969b88d1bfa6eac23f65b1ca2144f27c34
workflow-type: tm+mt
source-wordcount: '499'
ht-degree: 5%

---

# Comparaison de l’extension Target avec l’extension Optimisation

La bibliothèque Adobe Target at.js autonome diffère considérablement du SDK Web Platform. Les tableaux suivants constituent une référence pour vous aider à évaluer les zones de votre mise en oeuvre sur lesquelles vous devrez peut-être vous concentrer pendant le processus de migration.

Après avoir examiné les informations ci-dessous et évalué votre implémentation technique actuelle d’at.js, vous devriez être en mesure de comprendre les éléments suivants :

- Quelles fonctionnalités Target sont prises en charge par le SDK Web Platform ?
- Quelles fonctions at.js ont des équivalents du SDK Web Platform ?
- Application des paramètres Target avec le SDK Web Platform
- Différence entre le flux de données d’at.js et le SDK Web Platform

Si vous découvrez le SDK Web Platform, ne vous inquiétez pas : les éléments ci-dessous sont abordés plus en détail tout au long de ce tutoriel.

## Comparaison des fonctionnalités

| | Extension Target | Optimiser l’extension (Target via Edge) | Expériences basées sur un code AJO (SDK de messagerie) |
|---|---|---|---|
| Mode de prérécupération | Pris en charge | Pris en charge | Pris en charge |
| Mode d’exécution | Pris en charge | Non pris en charge | Non pris en charge |
| Paramètres personnalisés | Pris en charge | Par paramètres de mbox ne sont pas pris en charge | Non pris en charge |
| Accès aux audiences | Pris en charge | Pris en charge | Pris en charge via l’audience Campaign et le paramètre d’exclusion de l’expérience |
| Segmentation d’audience à l’aide des mesures de cycle de vie mobile | Pris en charge | Pris en charge via les règles de collecte de données | Le ciblage d’expérience n’est actuellement pas pris en charge |
| thirdPartyId (mbox3rdPartyId) | Pris en charge par le biais de la configuration d’Identity Map et de l’espace de noms dans le flux de données | Non pris en charge |
| Notifications (affichage, clic) | Pris en charge | Pris en charge | Pris en charge |
| Jetons de réponse | Pris en charge | Pris en charge | Aucun équivalent pour le renvoi de métadonnées spécifiques à Campaign en dehors du contenu |
| Offres dynamiques | Pris en charge | Pris en charge | Le rendu du jeton associé au profil et à l’élément de décision dans le contenu est pris en charge |
| Analytics for Target (A4T) | Côté client uniquement | Côté client et côté serveur | Non pris en charge |
| Aperçus mobiles (mode AQ) | Pris en charge | Prise en charge limitée | En cours |



## Légendes dignes de mention

>[!NOTE]
>
>La migration de Target vers le SDK Web Platform tout en conservant une mise en oeuvre Adobe Analytics d’AppMeasurement existante pour une page donnée n’est pas prise en charge.
>
> Il est possible de migrer votre implémentation d’at.js (et d’AppMeasurement.js) vers le SDK Web Platform une page à la fois. Si vous optez pour cette approche, il est préférable de définir les options [`idMigrationEnabled`](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-the-sdk.html#id-migration-enabled) et [`targetMigrationEnabled`](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-the-sdk.html#targetMigrationEnabled) sur `true` avec la commande `configure`.

## Fonctions d’extension de Target et leurs équivalents d’optimisation

De nombreuses fonctions d’extension Target ont une approche équivalente utilisant l’extension Optimiser décrite dans le tableau ci-dessous. Pour plus d’informations sur les [fonctions](https://developer.adobe.com/target/implement/client-side/atjs/atjs-functions/atjs-functions/), consultez le Guide du développeur d’Adobe Target.

| Extension Target | Optimisation de l’extension |
| --- | --- | 
| |  |

## Paramètres de l’extension Target et Optimiser les équivalents de l’extension

L’extension Target peut être configurée et téléchargée avec divers paramètres dans ...

| Extension Target | Optimisation de l’extension |
| --- | --- | 
| |  |


## Comparaison des diagrammes système

Les diagrammes suivants doivent vous aider à comprendre les différences de flux de données entre une implémentation Target à l’aide d’at.js et une implémentation à l’aide du SDK Web Platform.

### Diagramme du système d’extension Target



### Optimiser le diagramme du système d’extension




>[!NOTE]
>
>Nous nous engageons à vous aider à réussir la migration de Target mobile de l’extension Target vers l’extension Optimize. Si vous rencontrez des obstacles lors de votre migration ou si vous pensez qu’il manque des informations essentielles dans ce guide, faites-le-nous savoir en publiant sur [cette discussion communautaire](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-target-from-at-js-to-web-sdk/m-p/575587#M463).
