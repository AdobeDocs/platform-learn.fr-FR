---
title: Ingérer et analyser des données Google Analytics dans Adobe Experience Platform avec le connecteur Source BigQuery - Charger des données de BigQuery dans Adobe Experience Platform
description: Ingérer et analyser des données Google Analytics dans Adobe Experience Platform avec le connecteur Source BigQuery - Charger des données de BigQuery dans Adobe Experience Platform
kt: 5342
doc-type: tutorial
exl-id: f58af1cf-6f2e-420c-9eed-29382806a9f4
source-git-commit: 1e3a8d585503eddad4c642a3b13d2b5f7ddc9943
workflow-type: tm+mt
source-wordcount: '724'
ht-degree: 3%

---

# 1.2.4 Chargement de données BigQuery dans Adobe Experience Platform

## Objectifs

- Mappage des données BigQuery à un schéma XDM
- Chargement des données BigQuery dans Adobe Experience Platform
- Familiarisez-vous avec l’interface utilisateur du connecteur Source BigQuery

## Avant de commencer

Après l’exercice précédent, vous devriez voir cette page s’ouvrir dans Adobe Experience Platform :

![demo](./images/datasets.png)

**Si vous l’avez ouvert, passez à l’exercice suivant.**

**Si vous ne l’avez pas ouvert, accédez à [Adobe Experience Platform](https://experience.adobe.com/platform/home).**

Dans le menu de gauche, accédez à Sources. Vous verrez ensuite la page d’accueil **Sources**. Dans le menu **Sources**, accédez au connecteur source **Google BigQuery** et cliquez sur **Configurer**.

![demo](./images/sourceshome.png)

L’écran de sélection Compte BigQuery Google s’affiche alors. Sélectionnez votre compte et cliquez sur **Suivant**.

![demo](./images/0c.png)

L’écran **Sélectionner les données** s’affiche alors.

![demo](./images/datasets.png)

## Sélection 1.2.4.1 tableau BigQuery

Dans l’écran **Sélectionner des données**, sélectionnez votre jeu de données BigQuery. Vous pouvez désormais afficher un aperçu des données d’exemple du Google Analytics dans BigQuery.

Cliquez sur **Suivant**.

![demo](./images/datasets1.png)

## Mappage XDM 1.2.4.2

Vous verrez maintenant ceci :

![demo](./images/xdm4a.png)

Vous devez maintenant créer un jeu de données ou sélectionner un jeu de données existant dans lequel charger les données Google Analytics. Pour cet exercice, un jeu de données et un schéma ont déjà été créés. Vous n’avez pas besoin de créer un schéma ou un jeu de données.

Sélectionnez **Jeu de données existant**. Ouvrez le menu déroulant pour sélectionner un jeu de données. Recherchez le jeu de données nommé `Demo System - Event Dataset for BigQuery (Global v1.1)` et sélectionnez-le. Cliquez sur **Suivant**.

![demo](./images/xdm6.png)

Faites défiler vers le bas. Vous devez désormais mapper chaque **champ Source** de Google Analytics/BigQuery à un XDM **champ cible**, champ par champ. Il se peut que vous rencontriez un certain nombre d’erreurs, qui seront corrigées par l’exercice de mappage ci-dessous.

![demo](./images/xdm8.png)

Utilisez le tableau de mappage ci-dessous pour cet exercice.

| Champ source | Champ cible |
| ----------------- |-------------| 
| `_id` | `_id` |
| `_id` | canal._id |
| `timeStamp` | date et heure |
| `GA_ID` | ``--aepTenantId--``.identification.core.gaid |
| `customerID` | ``--aepTenantId--``. identification.core.crmId |
| `Page` | web.webPageDetails.name |
| `Device` | device.type |
| `Browser` | environment.browserDetails.vendor |
| `MarketingChannel` | marketing.trackingCode |
| `TrafficSource` | channel.typeAtSource |
| `TrafficMedium` | channel.mediaType |
| `TransactionID` | commerce.order.payments.transactionID |
| `Ecommerce_Action_Type` | eventType |
| `Pageviews` | web.webPageDetails.pageViews.value |


Pour certains champs, vous devez supprimer le mappage d’origine et en créer un nouveau, par exemple un **champ calculé**.

| Champ Calculé | Champ cible |
| ----------------- |-------------| 
| `iif(Unique_Purchases == null, 0, Unique_Purchases)` | commerce.purchases.value |
| `iif(Product_Detail_Views == null, 0, Product_Detail_Views)` | commerce.productViews.value |
| `iif(Adds_To_Cart == null, 0, Adds_To_Cart)` | commerce.productListAdds.value |
| `iif(Product_Removes_From_Cart == null, 0, Product_Removes_From_Cart), 1, 0)` | commerce.productListRemovals.value |
| `iif(Product_Checkouts == null, 0, Product_Checkouts)` | commerce.checkouts.value |

Pour créer un **Champ calculé**, cliquez sur **+ Nouveau type de champ** puis sur **Champ calculé**.

![demo](./images/xdm8a.png)

Collez la règle ci-dessus et cliquez sur **Enregistrer** pour chacun des champs du tableau ci-dessus.

![demo](./images/xdm8b.png)

Vous disposez désormais d’un **Mapping** comme celui-ci.

Les champs sources **GA_ID** et **customerID** sont mappés à un identifiant dans ce schéma XDM. Vous pouvez ainsi enrichir les données de Google Analytics (données de comportement web/d’application) avec d’autres jeux de données tels que les données de fidélité ou de centre d’appels.

Cliquez sur **Suivant**.

![demo](./images/xdm34.png)

## 1.2.4.3 la connexion et la planification de l’ingestion des données

L’onglet **Planification** s’affiche maintenant :

Dans l’onglet **Planification**, vous pouvez définir une fréquence pour le processus d’ingestion des données pour ce **Mappage** et ces données.

Comme vous utilisez des données de démonstration dans Google BigQuery qui ne seront pas actualisées, il n’est pas vraiment nécessaire de définir un planning dans cet exercice. Vous devez sélectionner quelque chose. Pour éviter de trop nombreux processus d’ingestion de données inutiles, vous devez définir la fréquence comme suit :

- Fréquence : **Semaine**
- Intervalle : **200**
- Heure de début : **à tout moment dans l’heure suivante**

**Important** : assurez-vous d’activer le commutateur **Renvoi**.

Enfin, vous devez définir un champ **delta**.

Le champ **delta** est utilisé pour planifier la connexion et charger uniquement les nouvelles lignes qui entrent dans votre jeu de données BigQuery. Un champ delta est généralement toujours une colonne d’horodatage. Ainsi, pour les futures ingestions de données planifiées, seules les lignes dotées d’un nouvel horodatage plus récent seront ingérées.

Sélectionnez **timeStamp** comme champ delta.
Cliquez sur **Suivant**.

![demo](./images/ex437.png)

## 1.2.4.4 Vérifier et lancer la connexion

Un aperçu détaillé de votre connexion s’affiche maintenant. Assurez-vous que tout est correct avant de continuer, car certains paramètres ne peuvent plus être modifiés par la suite, comme par exemple le mappage XDM.

Cliquez sur **Terminer**.

![demo](./images/xdm46.png)

Une fois la connexion créée, voici ce que vous verrez :

![demo](./images/xdm48.png)

Vous êtes maintenant prêt à passer au prochain exercice, dans lequel vous utiliserez Customer Journey Analytics pour créer des visualisations puissantes en plus des données de Google Analytics.

## Étapes suivantes

Accédez à [1.2.5 Analyse des données Google Analytics à l’aide de Customer Journey Analytics](./ex5.md){target="_blank"}

Revenez à [Ingérer et analyser des données Google Analytics dans Adobe Experience Platform avec le connecteur Source BigQuery](./customer-journey-analytics-bigquery-gcp.md){target="_blank"}

Revenir à [Tous les modules](./../../../../overview.md){target="_blank"}
