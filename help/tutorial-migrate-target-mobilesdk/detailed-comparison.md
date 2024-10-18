---
title: Comparaison de l’extension Target avec l’extension de prise de décision
description: Découvrez les différences entre l’extension Target et l’extension de prise de décision, notamment les fonctionnalités, les fonctions, les paramètres et le flux de données.
source-git-commit: e727fbfc82dea9ab6244b669b2f06c47987db1b1
workflow-type: tm+mt
source-wordcount: '468'
ht-degree: 4%

---

# Comparaison de l’extension Target avec l’extension de prise de décision

L’extension Adobe Journey Optimizer - Prise de décision diffère de l’extension Adobe Target pour les applications mobiles. Les tableaux suivants constituent une référence pour vous aider à évaluer les zones de votre mise en oeuvre sur lesquelles vous devrez peut-être vous concentrer pendant le processus de migration.

Après avoir examiné les informations ci-dessous et évalué votre mise en oeuvre technique actuelle de l’extension Target, vous devriez être en mesure de comprendre les éléments suivants :

- Quelles fonctionnalités Target sont prises en charge par Adobe Journey Optimizer - Prise de décision ?
- Quelles fonctions d’extension Adobe Target ont des équivalents Adobe Journey Optimizer - Decisioning ?
- Application des paramètres Target avec Adobe Journey Optimizer - Prise de décision
- Différence entre le flux de données de l’extension Adobe Target et l’extension Adobe Journey Optimizer - Decisioning

Si vous découvrez le SDK Web Platform, ne vous inquiétez pas : les éléments ci-dessous sont abordés plus en détail tout au long de ce tutoriel.

## Comparaison des fonctionnalités

| | Extension Target | Extension de prise de décision (Target via Edge) |
|---|---|---|---|
| Mode de prérécupération | Pris en charge | Pris en charge |
| Mode d’exécution | Pris en charge | Non pris en charge |
| Paramètres personnalisés | Pris en charge | Par paramètres de mbox ne sont pas pris en charge |
| Accès aux audiences | Pris en charge | Pris en charge |
| Segmentation d’audience à l’aide des mesures de cycle de vie mobile | Pris en charge | Pris en charge via les règles de collecte de données |
| thirdPartyId (mbox3rdPartyId) | Pris en charge par le biais de la configuration d’Identity Map et de l’espace de noms dans le flux de données |
| Notifications (affichage, clic) | Pris en charge | Pris en charge |
| Jetons de réponse | Pris en charge | Pris en charge |
| Offres dynamiques | Pris en charge | Pris en charge |
| Analytics for Target (A4T) | Côté client uniquement | Côté client et côté serveur |
| Aperçus mobiles (mode AQ) | Pris en charge | Prise en charge limitée |



## Légendes dignes de mention

>[!NOTE]
>
>La migration de Target vers le SDK Web Platform tout en conservant une mise en oeuvre Adobe Analytics d’AppMeasurement existante pour une page donnée n’est pas prise en charge.
>
> Il est possible de migrer votre implémentation d’at.js (et d’AppMeasurement.js) vers le SDK Web Platform une page à la fois. Si vous optez pour cette approche, il est préférable de définir les options [`idMigrationEnabled`](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-the-sdk.html#id-migration-enabled) et [`targetMigrationEnabled`](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-the-sdk.html#targetMigrationEnabled) sur `true` avec la commande `configure`.

## Fonctions de l’extension Target et équivalents de l’extension de prise de décision

De nombreuses fonctions d’extension Target ont une approche équivalente utilisant l’extension de prise de décision décrite dans le tableau ci-dessous. Pour plus d’informations sur les [fonctions](https://developer.adobe.com/target/implement/client-side/atjs/atjs-functions/atjs-functions/), consultez le Guide du développeur d’Adobe Target.

| Extension Target | Extension de prise de décision |
| --- | --- | 
| |  |

## Paramètres de l’extension Target et équivalents de l’extension de prise de décision

L’extension Target peut être configurée et téléchargée avec divers paramètres dans ...

| Extension Target | Extension de prise de décision |
| --- | --- | 
| |  |


## Comparaison des diagrammes système

Les diagrammes suivants doivent vous aider à comprendre les différences de flux de données entre une mise en oeuvre Target à l’aide de l’extension Adobe Journey Optimizer - Prise de décision et une mise en oeuvre à l’aide de l’extension Adobe Target.

### Diagramme du système d’extension Target



### Diagramme du système d’extension de prise de décision




>[!NOTE]
>
>Nous nous engageons à vous aider à réussir la migration de Target mobile de l’extension Target vers l’extension de prise de décision. Si vous rencontrez des obstacles lors de votre migration ou si vous pensez qu’il manque des informations essentielles dans ce guide, faites-le-nous savoir en publiant sur [cette discussion communautaire](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-target-from-at-js-to-web-sdk/m-p/575587#M463).
