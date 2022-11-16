---
title: CDP en temps réel - Création d’un segment et action - Configuration d’une destination publicitaire telle que Google DV360
description: CDP en temps réel - Création d’un segment et action - Configuration d’une destination publicitaire telle que Google DV360
kt: 5342
audience: Data Architect, Orchestration Engineer, Marketer
doc-type: tutorial
activity: develop
exl-id: 40441815-428a-48dc-a12e-91220d4ba307
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '332'
ht-degree: 2%

---

# 6.2 Configuration d’une destination publicitaire telle que Google DV360

>[!IMPORTANT]
>
>Le contenu ci-dessous est conçu comme FYI - Vous le faites **NOT** Vous devez configurer une nouvelle destination pour DV360. La destination a déjà été créée et vous pouvez l’utiliser dans l’exercice suivant.

Accédez à [Adobe Experience Platform](https://experience.adobe.com/platform). Une fois connecté, vous accédez à la page d’accueil de Adobe Experience Platform.

![Ingestion des données](../module2/images/home.png)

Avant de continuer, vous devez sélectionner une **sandbox**. L’environnement de test à sélectionner est nommé ``--aepSandboxId--``. Pour ce faire, cliquez sur le texte **[!UICONTROL Production Prod]** dans la ligne bleue en haut de votre écran. Après avoir sélectionné le [!UICONTROL sandbox], vous verrez le changement d’écran et vous êtes maintenant dans votre [!UICONTROL sandbox].

![Ingestion des données](../module2/images/sb1.png)

Dans le menu de gauche, accédez à **Destinations**, puis accédez à **Catalogue**. Vous verrez alors le **Catalogue des destinations**.

![RTCDP](./images/rtcdp.png)

Dans **Destinations**, cliquez sur **Google Display &amp; Video 360** puis cliquez sur **+ Configuration**.

![RTCDP](./images/rtcdpgoogle.png)

Vous verrez alors ceci. Cliquez sur **Se connecter à la destination**.

![RTCDP](./images/rtcdpgooglecreate1.png)

Dans l’écran suivant, vous pouvez configurer votre destination vers Google DV360.

![RTCDP](./images/rtcdpgooglecreatedest.png)

Saisissez une valeur dans les champs. **Nom** et **Description**.

Le champ **Identifiant de compte** est la valeur **Identifiant publicitaire** du compte DV360. Vous pouvez le trouver ici :

![RTCDP](./images/rtcdpgoogledv360advid.png)

Le **Type de compte** doit être défini sur **Inviter un annonceur**.

Maintenant vous avez ceci. Cliquez sur **Suivant**.

![RTCDP](./images/rtcdpgoogldv360new.png)

>[!NOTE]
>
>Google doit placer sur la liste autorisée l’Adobe pour que Adobe Experience Platform puisse envoyer des données à Google DV360. Contactez votre gestionnaire de compte Google pour activer ce flux de données.

Après avoir créé la destination, vous verrez ceci. Vous pouvez éventuellement sélectionner une stratégie de gouvernance des données. Cliquez ensuite sur **Enregistrer et quitter**.

![RTCDP](./images/rtcdpcreatedest1.png)

Une liste des destinations disponibles s’affiche alors.
Au cours de l’exercice suivant, vous allez connecter le segment que vous avez créé lors de l’exercice précédent à la destination Google DV360.

Étape suivante : [6.3 Agir : envoyer votre segment à DV360 ;](./ex3.md)

[Revenir au module 6](./real-time-cdp-build-a-segment-take-action.md)

[Revenir à tous les modules](../../overview.md)
