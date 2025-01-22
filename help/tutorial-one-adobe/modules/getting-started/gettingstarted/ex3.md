---
title: Prise en main - Création de votre flux de données
description: Prise en main - Création de votre flux de données
kt: 5342
doc-type: tutorial
exl-id: d36057b4-64c6-4389-9612-d3c9cf013117
source-git-commit: e505b8401509f6171d9c98f85a93af27c38a8303
workflow-type: tm+mt
source-wordcount: '825'
ht-degree: 1%

---

# Créer votre flux de données

Accédez à [https://experience.adobe.com/#/data-collection/](https://experience.adobe.com/#/data-collection/).

![DSN ](./images/launchprop.png)

Dans le menu de gauche, cliquez sur **[!UICONTROL Balises]**. Après l’exercice précédent, vous disposez désormais de 3 propriétés de collecte de données : une pour le web, une pour le mobile et une pour l’application CX.

![DSN ](./images/launchprop1.png)

Ces propriétés sont presque prêtes à être utilisées, mais avant de pouvoir commencer à collecter des données à l’aide de ces propriétés, vous devez configurer un flux de données. Vous obtiendrez plus d’informations sur le concept de flux de données et ce qu’il signifie dans un exercice ultérieur du module Collecte de données .

Pour l’instant, procédez comme suit.

## Créer un flux de données pour le web

Cliquez sur **[!UICONTROL Flux de données]**.

![Cliquez sur l’icône Configuration Edge dans le volet de navigation de gauche](./images/edgeconfig1a.png)

Dans le coin supérieur droit de l’écran, sélectionnez le nom du sandbox, qui doit être `--aepSandboxName--`.

![Cliquez sur l’icône Configuration Edge dans le volet de navigation de gauche](./images/edgeconfig1b.png)

Cliquez sur **[!UICONTROL Nouveau flux de données]**.

![Cliquez sur l’icône Configuration Edge dans le volet de navigation de gauche](./images/edgeconfig1.png)

Pour le **[!UICONTROL Nom]** et pour la description facultative, saisissez `--aepUserLdap-- - One Adobe Datastream`. Pour **Schéma de mappage**, sélectionnez **Système de démonstration - Schéma d’événement pour le site web (global v1.1)**. Cliquez sur **Enregistrer**.

![Nommez la configuration Edge et enregistrez](./images/edgeconfig2.png)

Tu verras ça. Cliquez sur **Ajouter un service**.

![Nommez la configuration Edge et enregistrez](./images/edgeconfig3.png)

Sélectionnez le service **[!UICONTROL Adobe Experience Platform]**, qui exposera des champs supplémentaires. Tu verras ça.

Pour Jeu de données d’événement, sélectionnez **Système de démonstration - Jeu de données d’événement pour le site web (global v1.1)** et pour Jeu de données de profil, sélectionnez **Système de démonstration - Jeu de données de profil pour le site web (global v1.1)**. Cliquez sur **Enregistrer**.

![Nommez la configuration Edge et enregistrez](./images/edgeconfig4.png)

Vous allez voir ceci.

![Nommez la configuration Edge et enregistrez](./images/edgeconfig5.png)

Dans le menu de gauche, cliquez sur **[!UICONTROL Balises]**.

Filtrez les résultats de la recherche pour afficher les propriétés de la collecte de données. Ouvrez la propriété pour **Web** en cliquant dessus.

![Nommez la configuration Edge et enregistrez](./images/edgeconfig10a.png)

Tu verras ça. Cliquez sur **Extensions**.

![Nommez la configuration Edge et enregistrez](./images/edgeconfig11.png)

Cliquez d’abord sur l’extension Adobe Experience Platform Web SDK, puis sur **Configurer**.

![Nommez la configuration Edge et enregistrez](./images/edgeconfig12.png)

Tu verras ça. Consultez le menu **Flux de données** et assurez-vous que le bon sandbox est sélectionné, ce qui, dans votre cas, doit être `--aepSandboxName--`.

![Nommez la configuration Edge et enregistrez](./images/edgeconfig12a.png)

Ouvrez la liste déroulante **Flux de données** et sélectionnez le flux de données que vous avez créé précédemment.

![Nommez la configuration Edge et enregistrez](./images/edgeconfig13.png)

Assurez-vous d’avoir sélectionné votre **flux de données** dans les trois environnements différents. Cliquez ensuite sur **Enregistrer**.

![Nommez la configuration Edge et enregistrez](./images/edgeconfig14.png)

Accédez à **Flux de publication**.

![Nommez la configuration Edge et enregistrez](./images/edgeconfig15.png)

Cliquez sur le **...** pour **Principal**, puis sur **Modifier**.

![Nommez la configuration Edge et enregistrez](./images/edgeconfig16.png)

Cliquez sur **Ajouter toutes les ressources modifiées** puis sur **Enregistrer et créer pour développement**.

![Nommez la configuration Edge et enregistrez](./images/edgeconfig17.png)

Vos modifications sont maintenant publiées et seront prêtes dans quelques minutes, après quoi vous verrez le point vert à côté de **Main**.

![Nommez la configuration Edge et enregistrez](./images/edgeconfig17a.png)

## Créer votre flux de données pour Mobile

Accédez à [https://experience.adobe.com/#/data-collection/](https://experience.adobe.com/#/data-collection/).

Cliquez sur **[!UICONTROL Flux de données]**.

![Cliquez sur icône Flux de données dans le volet de navigation de gauche](./images/edgeconfig1a.png)

Dans le coin supérieur droit de l’écran, sélectionnez le nom du sandbox, qui doit être `--aepSandboxName--`.

![Cliquez sur l’icône Configuration Edge dans le volet de navigation de gauche](./images/edgeconfig1b.png)

Cliquez sur **[!UICONTROL Nouveau flux de données]**.

![Cliquez sur icône Flux de données dans le volet de navigation de gauche](./images/edgeconfig1.png)

Pour le **[!UICONTROL Nom convivial]** et pour la description facultative, saisissez `--aepUserLdap-- - One Adobe Datastream (Mobile)`. Pour **Schéma de mappage**, sélectionnez **Système de démonstration - Schéma d’événement pour l’application mobile (global v1.1)**. Cliquez sur **Enregistrer**.

Cliquez sur **[!UICONTROL Enregistrer]**.

![Nommez le flux de données et enregistrez](./images/edgeconfig2m.png)

Tu verras ça. Cliquez sur **Ajouter un service**.

![Nommez le flux de données et enregistrez](./images/edgeconfig3m.png)

Sélectionnez le service **[!UICONTROL Adobe Experience Platform]**, qui exposera des champs supplémentaires. Tu verras ça.

Pour Jeu de données d’événement, sélectionnez **Système de démonstration - Jeu de données d’événement pour l’application mobile (Global v1.1)** et pour Jeu de données de profil, sélectionnez **Système de démonstration - Jeu de données de profil pour l’application mobile (Global v1.1)**. Cliquez sur **Enregistrer**.

![Nommez la configuration du flux de données et enregistrez](./images/edgeconfig4m.png)

Tu verras ça.

![Nommez la configuration du flux de données et enregistrez](./images/edgeconfig5m.png)

Votre flux de données est maintenant prêt à être utilisé dans votre propriété Client de collecte de données Adobe Experience Platform pour Mobile.

Accédez à **Balises** et filtrez les résultats de la recherche pour afficher vos deux propriétés de collecte de données. Ouvrez la propriété pour **Mobile** en cliquant dessus.

![Nommez la configuration Edge et enregistrez](./images/edgeconfig10am.png)

Tu verras ça. Cliquez sur **Extensions**.

![Nommez la configuration Edge et enregistrez](./images/edgeconfig11m.png)

Cliquez sur l’extension **Adobe Experience Platform Edge Network**, puis sur **Configurer**.

![Nommez la configuration Edge et enregistrez](./images/edgeconfig12m.png)

Tu verras ça. Vous devez maintenant sélectionner le sandbox et le flux de données corrects que vous venez de configurer. Le sandbox à utiliser est `--aepSandboxName--` et le flux de données est appelé `--aepUserLdap-- - Demo System Datastream (Mobile)`.

Pour le domaine **Edge Network**, veuillez utiliser le domaine par défaut.

Cliquez sur **Enregistrer** pour enregistrer vos modifications.

![Nommez la configuration Edge et enregistrez](./images/edgeconfig13m.png)

Accédez à **Flux de publication**.

![Nommez la configuration Edge et enregistrez](./images/edgeconfig15m.png)

Cliquez sur le **...** en regard de **Principal**, puis cliquez sur **Modifier**.

![Nommez la configuration Edge et enregistrez](./images/edgeconfig16m.png)

Cliquez sur **Ajouter toutes les ressources modifiées**, puis sur **Enregistrer et créer pour développement**.

![Nommez la configuration Edge et enregistrez](./images/edgeconfig17m.png)

Vos modifications sont maintenant publiées et seront prêtes dans quelques minutes, après quoi vous verrez le point vert à côté de **Main**.

![Nommez la configuration Edge et enregistrez](./images/edgeconfig17ma.png)

Étape suivante : [Utiliser le site web](./ex4.md)

[Revenir à la prise en main](./getting-started.md)

[Revenir à tous les modules](./../../../overview.md)
