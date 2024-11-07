---
title: Ingestion et analyse de données Google Analytics dans Adobe Experience Platform avec le connecteur Source BigQuery - Chargement de données de BigQuery dans Adobe Experience Platform
description: Ingestion et analyse de données Google Analytics dans Adobe Experience Platform avec le connecteur Source BigQuery - Chargement de données de BigQuery dans Adobe Experience Platform
kt: 5342
doc-type: tutorial
source-git-commit: 2cdc145d7f3933ec593db4e6f67b60961a674405
workflow-type: tm+mt
source-wordcount: '767'
ht-degree: 4%

---

# 4.2.4 Chargement de données de BigQuery dans Adobe Experience Platform

## Objectifs

- Mappage des données BigQuery à un schéma XDM
- Chargement des données BigQuery dans Adobe Experience Platform
- Familiarisez-vous avec l’interface utilisateur de BigQuery Source Connector

## Avant de commencer

Après l’exercice 12.3, cette page doit être ouverte dans Adobe Experience Platform :

![demo](./images/datasets.png)

**Si vous l’avez ouvert, passez à l’exercice 12.4.1.**

**Si vous ne l’avez pas ouvert, accédez à [Adobe Experience Platform](https://experience.adobe.com/platform/home).**

Dans le menu de gauche, accédez à Sources. Vous verrez ensuite la page d’accueil **Sources**. Dans le menu **Sources**, cliquez sur **Bases de données**.

![demo](./images/sourceshome.png)

Sélectionnez le connecteur Source **Google BigQuery** et cliquez sur **+ Configurer**.

![demo](./images/bq.png)

L’écran de sélection Compte BigQuery Google s’affiche alors.

![demo](./images/0-c.png)

Sélectionnez votre compte et cliquez sur **Suivant**.

![demo](./images/ex4/0-d.png)

Vous verrez ensuite la vue **Ajouter des données**.

![demo](./images/datasets.png)

## 4.2.4.1 Sélection de tableau BigQuery

Dans la vue **Ajouter des données**, sélectionnez votre jeu de données BigQuery.

![demo](./images/datasets.png)

Vous pouvez maintenant voir un aperçu des données d’exemple des données Google Analytics dans BigQuery.

Cliquez sur **Suivant**.

![demo](./images/ex4/3.png)

## Mappage XDM 4.2.4.2

Vous verrez maintenant ceci :

![demo](./images/xdm4a.png)

Vous devez maintenant créer un nouveau jeu de données ou sélectionner un jeu de données existant dans lequel charger les données Google Analytics. Pour cet exercice, un jeu de données et un schéma ont déjà été créés. Vous n’avez pas besoin de créer un nouveau schéma ou jeu de données.

Sélectionnez **Jeu de données existant**. Ouvrez le menu déroulant pour sélectionner un jeu de données. Recherchez le jeu de données nommé `Demo System - Event Dataset for BigQuery (Global v1.1)` et sélectionnez-le. Cliquez sur **Suivant**.

![demo](./images/xdm6.png)

Faites défiler vers le bas. Vous devez maintenant mapper chaque **champ Source** de Google Analytics/BigQuery à un **champ cible XDM**, champ par champ.

![demo](./images/xdm8.png)

Utilisez le tableau de mappage ci-dessous pour cet exercice.

| Champ source | Champ cible |
| ----------------- |-------------| 
| **_id** | _id |
| **_id** | canal._id |
| timeStamp | date et heure |
| GA_ID | ``--aepTenantId--``.identification.core.gaid |
| customerID | ``--aepTenantId--``.identification.core.loyaltyId |
| Page | web.webPageDetails.name |
| Appareil | device.type |
| Navigateur | environment.browserDetails.vendor |
| MarketingChannel | marketing.trackingCode |
| TrafficSource | channel.typeAtSource |
| TrafficMedium | channel.mediaType |
| TransactionID | commerce.order.payments.transactionID |
| Ecommerce_Action_Type | eventType |
| Pages vues | web.webPageDetails.pageViews.value |
| Unique_Achats | commerce.purchases.value |
| Product_Detail_Views | commerce.productViews.value |
| Ajouts_To_Cart | commerce.productListAdds.value |
| Product_Removes_From_Cart | commerce.productListRemovals.value |
| Product_Checkouts | commerce.checkouts.value |

Après avoir copié et collé le mappage ci-dessus dans l’interface utilisateur de Adobe Experience Platform, vérifiez si vous ne voyez aucune erreur en raison de fautes de frappe ou d’espaces au début/à la fin.

Vous avez maintenant un **Mapping** comme celui-ci :

![demo](./images/xdm34.png)

Les champs source **GA_ID** et **customerID** sont mappés à un identifiant dans ce schéma XDM. Vous pourrez ainsi enrichir les données des Google Analytics (données de comportement web/app) avec d’autres jeux de données tels que Loyalty ou Call Center-data.

Cliquez sur **Suivant**.

![demo](./images/ex4/38.png)

## 4.2.4.3 Connexion et planification de l’ingestion des données

L’onglet **Planification** s’affiche désormais :

![demo](./images/xdm38a.png)

Dans l&#39;onglet **Planification** , vous pouvez définir une fréquence pour le processus d&#39;ingestion des données pour ce **mapping** et ces données.

Lorsque vous utilisez des données de démonstration dans Google BigQuery qui ne seront pas actualisées, il n’est pas nécessaire de définir une planification dans cet exercice. Vous devez sélectionner un élément et, pour éviter un trop grand nombre de processus d’ingestion de données inutiles, vous devez définir la fréquence suivante :

- Fréquence : **Semaine**
- Intervalle : **200**

![demo](./images/ex4/39.png)

**Important** : assurez-vous d’activer le commutateur **Renvoi** .

![demo](./images/ex4/39a.png)

Enfin, et surtout, vous devez définir un champ **delta**.

![demo](./images/ex4/36.png)

Le champ **delta** est utilisé pour planifier la connexion et charger uniquement les nouvelles lignes qui entrent dans votre jeu de données BigQuery. Un champ delta est généralement toujours une colonne d’horodatage. Ainsi, pour les prochaines assimilations de données planifiées, seules les lignes comportant un nouvel horodatage plus récent seront ingérées.

Sélectionnez **timeStamp** comme champ delta.

![demo](./images/ex4/37.png)

Vous avez maintenant ceci.

![demo](./images/xdm37a.png)

Cliquez sur **Suivant**.

![demo](./images/ex4/42.png)

## 4.2.4.4 Vérification et lancement de la connexion

Dans la vue **Détails du flux du jeu de données**. vous devez nommer votre connexion, ce qui vous aidera à la trouver ultérieurement.

Utilisez cette convention d’affectation des noms :

| Champ | Attribution d&#39;un nom | Exemple |
| ----------------- |-------------| -------------|
| Nom du flux de jeux de données | DataFlow - ldap - Interaction du site web BigQuery | DataFlow - vangeluw - Interaction du site web BigQuery |
| Description | DataFlow - ldap - Interaction du site web BigQuery | DataFlow - vangeluw - Interaction du site web BigQuery |

![demo](./images/xdm44.png)

Cliquez sur **Suivant**.

![demo](./images/ex4/45.png)

Vous voyez maintenant un aperçu détaillé de votre connexion. Assurez-vous que tout est correct avant de continuer, car certains paramètres ne peuvent plus être modifiés par la suite, comme le mappage XDM par exemple.

![demo](./images/xdm46.png)

Cliquez sur **Terminer**.

![demo](./images/ex4/finish.png)

La configuration de la connexion peut prendre un certain temps. Ne vous inquiétez donc pas si vous voyez ceci :

![demo](./images/ex4/47.png)

Une fois la connexion créée, vous verrez :

![demo](./images/xdm48.png)

Vous êtes maintenant prêt à poursuivre l’exercice suivant, au cours duquel vous utiliserez Customer Journey Analytics pour créer de puissantes visualisations en plus des données Google Analytics.

Étape suivante : [4.2.5 Analyser les données des Google Analytics à l’aide de Customer Journey Analytics](./ex5.md)

[Revenir au module 4.2](./customer-journey-analytics-bigquery-gcp.md)

[Revenir à tous les modules](./../../../overview.md)
