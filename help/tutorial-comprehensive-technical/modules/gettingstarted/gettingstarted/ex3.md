---
title: Prise en main - Création de la matrice de données
description: Prise en main - Création de la matrice de données
kt: 5342
doc-type: tutorial
source-git-commit: 7d2f5f842559b2d6d9f115f3993268a4b36a0fe0
workflow-type: tm+mt
source-wordcount: '838'
ht-degree: 1%

---

# 0.3 Création de la matrice de données

Accédez à [https://experience.adobe.com/#/data-collection/](https://experience.adobe.com/#/data-collection/). Après l’exercice précédent, vous disposez désormais de deux propriétés de collecte de données : une pour le web et une pour le mobile.

![DSN](./images/launchprop.png)

Ces propriétés sont presque prêtes à être utilisées, mais avant de pouvoir commencer à collecter des données à l’aide de ces propriétés, vous devez configurer un flux de données. Vous obtiendrez plus d’informations sur le concept d’un flux de données et sur ce qu’il signifie dans l’exercice 1.2.

Pour l&#39;instant, veuillez suivre ces étapes.

## 0.3.1 Création d’un flux de données pour le Web

Cliquez sur **[!UICONTROL Datastreams]** ou **[!UICONTROL Datastreams (Beta)]**.

![Cliquez sur l’icône de configuration Edge dans le volet de navigation de gauche](./images/edgeconfig1a.png)

Dans le coin supérieur droit de votre écran, sélectionnez le nom de votre environnement de test, qui doit être `--aepSandboxId--`.

![Cliquez sur l’icône de configuration Edge dans le volet de navigation de gauche](./images/edgeconfig1b.png)

Cliquez sur **[!UICONTROL New Datastream]**.

![Cliquez sur l’icône de configuration Edge dans le volet de navigation de gauche](./images/edgeconfig1.png)

Pour le **[!UICONTROL nom convivial]** et pour la description facultative, saisissez `--demoProfileLdap-- - Demo System Datastream`. Pour le schéma d’événement, sélectionnez **Demo System - Event Schema for Website (Global v1.1)**. Cliquez sur **Enregistrer**.

![Nommez la configuration Edge et enregistrez](./images/edgeconfig2.png)

Vous verrez alors ceci. Cliquez sur **Ajouter un service**.

![Nommez la configuration Edge et enregistrez](./images/edgeconfig3.png)

Sélectionnez le service **[!UICONTROL Adobe Experience Platform]** qui présentera des champs supplémentaires. Vous verrez alors ceci.

Pour le jeu de données d’événement, sélectionnez **Système de démonstration - Jeu de données d’événement pour le site web (Global v1.1)** et, pour le jeu de données de profil, sélectionnez **Système de démonstration - Jeu de données de profil pour le site web (Global v1.1)**. Cliquez sur **Enregistrer**.

![Nommez la configuration Edge et enregistrez](./images/edgeconfig4.png)

Vous allez maintenant voir ceci.

![Nommez la configuration Edge et enregistrez](./images/edgeconfig5.png)

C&#39;est tout pour le moment. Dans le [module 1.1](./../../../modules/datacollection/module1.1/data-ingestion-launch-web-sdk.md), vous en apprendrez plus sur le SDK Web et sur la configuration de toutes ses fonctionnalités.

Dans le menu de gauche, cliquez sur **[!UICONTROL Balises]**.

Filtrez les résultats de la recherche pour afficher vos deux propriétés de collecte de données. Ouvrez la propriété de **Web** en cliquant dessus.

![Nommez la configuration Edge et enregistrez](./images/edgeconfig10a.png)

Vous verrez alors ceci. Cliquez sur **Extensions**.

![Nommez la configuration Edge et enregistrez](./images/edgeconfig11.png)

Sur l’extension SDK Web Adobe Experience Platform, cliquez sur **Configurer**.

![Nommez la configuration Edge et enregistrez](./images/edgeconfig12.png)

Vous verrez alors ceci. Pour **Datastreams**, une valeur factice est actuellement définie sur 1. Vous devez maintenant cliquer sur le bouton radio **Choisir dans la liste** . Dans la liste déroulante, sélectionnez le Datastream que vous avez créé précédemment.

![Nommez la configuration Edge et enregistrez](./images/edgeconfig13.png)

Assurez-vous d’avoir sélectionné votre **Datastream**. CONSEIL : vous pouvez filtrer facilement les résultats dans la liste déroulante en saisissant votre `--demoProfileLdap--`.

![Nommez la configuration Edge et enregistrez](./images/edgeconfig14.png)

Faites défiler l’écran vers le bas jusqu’à ce que vous puissiez voir **Collecte de données**. Assurez-vous que la case à cocher de la **collecte de données de clic activée** n’est pas activée. Cliquez sur **Enregistrer** pour enregistrer vos modifications.

![Nommez la configuration Edge et enregistrez](./images/edgeconfig14a.png)

Accédez à **Flux de publication**.

![Nommez la configuration Edge et enregistrez](./images/edgeconfig15.png)

Cliquez sur **...** pour **Main**, puis cliquez sur **Modifier**.

![Nommez la configuration Edge et enregistrez](./images/edgeconfig16.png)

Cliquez sur **Ajouter toutes les ressources modifiées**, puis sur **Enregistrer et créer pour le développement**.

![Nommez la configuration Edge et enregistrez](./images/edgeconfig17.png)

Vos modifications sont en cours de publication et seront prêtes dans quelques minutes.

## 0.3.2 Création d’un flux de données pour Mobile

Accédez à [https://experience.adobe.com/#/data-collection/](https://experience.adobe.com/#/data-collection/).

Cliquez sur **[!UICONTROL Datastreams]** ou **[!UICONTROL Datastreams (Beta)]**.

![Cliquez sur l’icône Datastream dans le volet de navigation de gauche](./images/edgeconfig1a.png)

Dans le coin supérieur droit de votre écran, sélectionnez le nom de votre environnement de test, qui doit être `--aepSandboxId--`.

![Cliquez sur l’icône de configuration Edge dans le volet de navigation de gauche](./images/edgeconfig1b.png)

Cliquez sur **[!UICONTROL New Datastream]**.

![Cliquez sur l’icône Datastream dans le volet de navigation de gauche](./images/edgeconfig1.png)

Pour le **[!UICONTROL nom convivial]** et pour la description facultative, saisissez `--demoProfileLdap-- - Demo System Datastream (Mobile)`. Pour le schéma d’événement, sélectionnez **Demo System - Event Schema for Mobile App (Global v1.1)**. Cliquez sur **Enregistrer**.

Cliquez sur **[!UICONTROL Enregistrer]**.

![Nommez le flux de données et enregistrez](./images/edgeconfig2m.png)

Vous verrez alors ceci. Cliquez sur **Ajouter un service**.

![Nommez le flux de données et enregistrez](./images/edgeconfig3m.png)

Sélectionnez le service **[!UICONTROL Adobe Experience Platform]** qui présentera des champs supplémentaires. Vous verrez alors ceci.

Pour le jeu de données d’événement, sélectionnez **Système de démonstration - Jeu de données d’événement pour l’application mobile (Global v1.1)** et, pour le jeu de données de profil, sélectionnez **Système de démonstration - Jeu de données de profil pour l’application mobile (Global v1.1)**. Cliquez sur **Enregistrer**.

![Nommez la configuration de la chaîne de données et enregistrez](./images/edgeconfig4m.png)

Vous verrez alors ceci.

![Nommez la configuration de la chaîne de données et enregistrez](./images/edgeconfig5m.png)

Votre flux de données est maintenant prêt à être utilisé dans la propriété du client de collecte de données Adobe Experience Platform pour Mobile.

Accédez à **Balises** et filtrez les résultats de la recherche pour afficher vos deux propriétés de collecte de données. Ouvrez la propriété de **Mobile** en cliquant dessus.

![Nommez la configuration Edge et enregistrez](./images/edgeconfig10am.png)

Vous verrez alors ceci. Cliquez sur **Extensions**.

![Nommez la configuration Edge et enregistrez](./images/edgeconfig11m.png)

Sur l’extension **Adobe Experience Platform Edge Network**, cliquez sur **Configurer**.

![Nommez la configuration Edge et enregistrez](./images/edgeconfig12m.png)

Vous verrez alors ceci. Vous devez maintenant sélectionner l’environnement de test et le flux de données corrects que vous venez de configurer. L’environnement de test à utiliser est `--aepSandboxId--` et le flux de données est appelé `--demoProfileLdap-- - Demo System Datastream (Mobile)`.

Pour le **domaine Edge Network**, utilisez le domaine par défaut **edge.adobedc.net**.

Cliquez sur **Enregistrer** pour enregistrer vos modifications.

![Nommez la configuration Edge et enregistrez](./images/edgeconfig13m.png)

Accédez à **Flux de publication**.

![Nommez la configuration Edge et enregistrez](./images/edgeconfig15m.png)

Cliquez sur **...** en regard de **Main**, puis cliquez sur **Modifier**.

![Nommez la configuration Edge et enregistrez](./images/edgeconfig16m.png)

Cliquez sur **Ajouter toutes les ressources modifiées**, puis sur **Enregistrer et créer pour le développement**.

![Nommez la configuration Edge et enregistrez](./images/edgeconfig17m.png)

Vos modifications sont en cours de publication et seront prêtes dans quelques minutes.

Étape suivante : [0.4 Utilisation du site Web](./ex4.md)

[Revenir au module 0](./getting-started.md)

[Revenir à tous les modules](./../../../overview.md)