---
title: CDP en temps réel - Créer un segment et agir - Envoyer votre segment à DV360
description: CDP en temps réel - Créer un segment et agir - Envoyer votre segment à DV360
kt: 5342
doc-type: tutorial
source-git-commit: 2cdc145d7f3933ec593db4e6f67b60961a674405
workflow-type: tm+mt
source-wordcount: '238'
ht-degree: 2%

---

# 2.3.3 Action : envoyez votre segment à DV360

Accédez à [Adobe Experience Platform](https://experience.adobe.com/platform). Une fois connecté, vous accédez à la page d’accueil de Adobe Experience Platform.

![Ingestion des données](./../../../modules/datacollection/module1.2/images/home.png)

Avant de continuer, vous devez sélectionner un **sandbox**. L’environnement de test à sélectionner est nommé ``--aepSandboxId--``. Pour ce faire, cliquez sur le texte **[!UICONTROL Production Prod]** dans la ligne bleue en haut de votre écran. Après avoir sélectionné l’[!UICONTROL sandbox] approprié, vous verrez le changement d’écran et vous êtes désormais dans votre [!UICONTROL sandbox] dédié.

![Ingestion des données](./../../../modules/datacollection/module1.2/images/sb1.png)

Dans le menu de gauche, accédez à **Destinations**, puis à **Catalogue**. Vous verrez ensuite le **catalogue des destinations**.

![RTCDP](./images/rtcdpmenudest.png)

Dans **Destinations**, cliquez sur l’icône **Activer les segments** de la carte **Google Display &amp; Video 360**.

![RTCDP](./images/rtcdpgoogleseg.png)

Sélectionnez votre destination et cliquez sur **Suivant**.

![RTCDP](./images/rtcdpcreatedest2.png)

Dans la liste des segments disponibles, sélectionnez le segment que vous avez créé lors de l’exercice précédent. Cliquez sur **Suivant**.

![RTCDP](./images/rtcdpcreatedest3.png)

Sur la page **Planification du segment**, cliquez sur **Suivant**.

![RTCDP](./images/rtcdpcreatedest4.png)

Enfin, sur la page **Review**, cliquez sur **Terminer**.

![RTCDP](./images/rtcdpcreatedest5.png)

Votre segment est maintenant lié à Google DV360. Chaque fois qu’un client est admissible pour ce segment, un signal est envoyé à Google DV360 pour inclure ce client dans l’audience de Google DV360.

Étape suivante : [2.3.4 Take Action : envoyez votre segment à une destination S3](./ex4.md)

[Revenir au module 2.3](./real-time-cdp-build-a-segment-take-action.md)

[Revenir à tous les modules](../../../overview.md)
