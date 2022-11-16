---
title: CDP en temps réel - Créer un segment et agir - Envoyer votre segment à DV360
description: CDP en temps réel - Créer un segment et agir - Envoyer votre segment à DV360
kt: 5342
audience: Data Architect, Orchestration Engineer, Marketer
doc-type: tutorial
activity: develop
exl-id: 7a78260f-cd25-4ed0-801b-87174babaffe
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '235'
ht-degree: 3%

---

# 6.3 Agir : envoyer votre segment à DV360 ;

Accédez à [Adobe Experience Platform](https://experience.adobe.com/platform). Une fois connecté, vous accédez à la page d’accueil de Adobe Experience Platform.

![Ingestion des données](../module2/images/home.png)

Avant de continuer, vous devez sélectionner une **sandbox**. L’environnement de test à sélectionner est nommé ``--aepSandboxId--``. Pour ce faire, cliquez sur le texte **[!UICONTROL Production Prod]** dans la ligne bleue en haut de votre écran. Après avoir sélectionné le [!UICONTROL sandbox], vous verrez le changement d’écran et vous êtes maintenant dans votre [!UICONTROL sandbox].

![Ingestion des données](../module2/images/sb1.png)

Dans le menu de gauche, accédez à **Destinations**, puis accédez à **Catalogue**. Vous verrez alors le **Catalogue des destinations**.

![RTCDP](./images/rtcdpmenudest.png)

Dans **Destinations**, cliquez sur le bouton **Activation des segments** sur le **Google Display &amp; Video 360** carte.

![RTCDP](./images/rtcdpgoogleseg.png)

Sélectionnez votre destination et cliquez sur **Suivant**.

![RTCDP](./images/rtcdpcreatedest2.png)

Dans la liste des segments disponibles, sélectionnez le segment que vous avez créé lors de l’exercice précédent. Cliquez sur **Suivant**.

![RTCDP](./images/rtcdpcreatedest3.png)

Sur le **Planification des segments** page, cliquez sur **Suivant**.

![RTCDP](./images/rtcdpcreatedest4.png)

Enfin, le **Réviser** page, cliquez sur **Terminer**.

![RTCDP](./images/rtcdpcreatedest5.png)

Votre segment est maintenant lié à Google DV360. Chaque fois qu’un client est admissible pour ce segment, un signal est envoyé à Google DV360 pour inclure ce client dans l’audience de Google DV360.

Étape suivante : [6.4 Agir : envoyer votre segment à une destination S3 ;](./ex4.md)

[Revenir au module 6](./real-time-cdp-build-a-segment-take-action.md)

[Revenir à tous les modules](../../overview.md)
