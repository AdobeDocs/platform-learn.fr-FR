---
title: CDP en temps réel - Créer une audience et agir - Envoyer votre audience à DV360
description: CDP en temps réel - Créer une audience et agir - Envoyer votre audience à DV360
kt: 5342
doc-type: tutorial
exl-id: bb76524e-52c1-4c2c-8bcd-33cd39d12741
source-git-commit: acb941e4ee668248ae0767bb9f4f42e067c181ba
workflow-type: tm+mt
source-wordcount: '206'
ht-degree: 2%

---

# 2.3.3 Action : envoyez votre audience à DV360

Accédez à [Adobe Experience Platform](https://experience.adobe.com/platform). Une fois connecté, vous accédez à la page d’accueil de Adobe Experience Platform.

![Ingestion des données](./../../../modules/datacollection/module1.2/images/home.png)

Avant de continuer, vous devez sélectionner un **sandbox**. L’environnement de test à sélectionner est nommé ``--aepSandboxName--``. Après avoir sélectionné l’[!UICONTROL sandbox] approprié, vous verrez le changement d’écran et vous êtes désormais dans votre [!UICONTROL sandbox] dédié.

![Ingestion des données](./../../../modules/datacollection/module1.2/images/sb1.png)

Dans le menu de gauche, accédez à **Destinations**, puis à **Parcourir**. Vous verrez ensuite la destination **DV360**. Cliquez sur les 3 points **...** et cliquez sur **Activer les audiences**.

![RTCDP](./images/rtcdpmenudest.png)

Dans la liste des audiences disponibles, sélectionnez l’audience que vous avez créée lors de l’exercice précédent. Cliquez sur **Suivant**.

![RTCDP](./images/rtcdpcreatedest3.png)

Sur la page **Audience Schedule**, cliquez sur **Next**.

![RTCDP](./images/rtcdpcreatedest4.png)

Enfin, sur la page **Review**, cliquez sur **Terminer**.

![RTCDP](./images/rtcdpcreatedest5.png)

Votre audience est maintenant liée à Google DV360. Chaque fois qu’un client est admissible pour cette audience, un signal est envoyé à Google DV360 pour inclure ce client dans l’audience du côté Google DV360.

Étape suivante : [2.3.4 Take Action : envoyez votre audience à une destination S3](./ex4.md)

[Revenir au module 2.3](./real-time-cdp-build-a-segment-take-action.md)

[Revenir à tous les modules](../../../overview.md)
