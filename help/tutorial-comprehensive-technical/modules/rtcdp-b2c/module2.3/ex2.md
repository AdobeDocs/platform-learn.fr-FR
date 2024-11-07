---
title: CDP en temps réel - Création d’un segment et action - Configuration d’une destination Advertising telle que Google DV360
description: CDP en temps réel - Création d’un segment et action - Configuration d’une destination Advertising telle que Google DV360
kt: 5342
doc-type: tutorial
source-git-commit: 2cdc145d7f3933ec593db4e6f67b60961a674405
workflow-type: tm+mt
source-wordcount: '336'
ht-degree: 1%

---

# 2.3.2 Configuration d’une destination Advertising telle que Google DV360

>[!IMPORTANT]
>
>Le contenu ci-dessous est conçu comme FYI : vous ne devez **PAS** configurer une nouvelle destination pour DV360. La destination a déjà été créée et vous pouvez l’utiliser dans l’exercice suivant.

Accédez à [Adobe Experience Platform](https://experience.adobe.com/platform). Une fois connecté, vous accédez à la page d’accueil de Adobe Experience Platform.

![Ingestion des données](./../../../modules/datacollection/module1.2/images/home.png)

Avant de continuer, vous devez sélectionner un **sandbox**. L’environnement de test à sélectionner est nommé ``--aepSandboxId--``. Pour ce faire, cliquez sur le texte **[!UICONTROL Production Prod]** dans la ligne bleue en haut de votre écran. Après avoir sélectionné l’[!UICONTROL sandbox] approprié, vous verrez le changement d’écran et vous êtes désormais dans votre [!UICONTROL sandbox] dédié.

![Ingestion des données](./../../../modules/datacollection/module1.2/images/sb1.png)

Dans le menu de gauche, accédez à **Destinations**, puis à **Catalogue**. Vous verrez ensuite le **catalogue des destinations**.

![RTCDP](./images/rtcdp.png)

Dans **Destinations**, cliquez sur **Google Display &amp; Video 360**, puis sur **+ Configurer**.

![RTCDP](./images/rtcdpgoogle.png)

Vous verrez alors ceci. Cliquez sur **Se connecter à la destination**.

![RTCDP](./images/rtcdpgooglecreate1.png)

Dans l’écran suivant, vous pouvez configurer votre destination vers Google DV360.

![RTCDP](./images/rtcdpgooglecreatedest.png)

Saisissez une valeur dans les champs **Name** et **Description**.

Le champ **Identifiant de compte** est l’ **identifiant publicitaire** du compte DV360. Vous pouvez le trouver ici :

![RTCDP](./images/rtcdpgoogledv360advid.png)

Le **Type de compte** doit être défini sur **Invite Advertiser**.

Maintenant, vous avez ceci. Cliquez sur **Suivant**.

![RTCDP](./images/rtcdpgoogldv360new.png)

>[!NOTE]
>
>Google doit disposer d’un Adobe de liste autorisée pour que Adobe Experience Platform puisse envoyer des données à Google DV360. Contactez votre gestionnaire de compte Google pour activer ce flux de données.

Après avoir créé la destination, vous verrez ceci. Vous pouvez éventuellement sélectionner une stratégie de gouvernance des données. Cliquez ensuite sur **Save &amp; exit**.

![RTCDP](./images/rtcdpcreatedest1.png)

Une liste des destinations disponibles s’affiche alors.
Au cours de l’exercice suivant, vous allez connecter le segment que vous avez créé lors de l’exercice précédent à la destination Google DV360.

Étape suivante : [2.3.3 Agir : envoyez votre segment à DV360](./ex3.md)

[Revenir au module 2.3](./real-time-cdp-build-a-segment-take-action.md)

[Revenir à tous les modules](../../../overview.md)
