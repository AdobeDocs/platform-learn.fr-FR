---
title: Bootcamp - CDP en temps réel - Création d’un segment et action - Envoyez votre segment à DV360
description: Bootcamp - CDP en temps réel - Création d’un segment et action - Envoyez votre segment à DV360
jira: KT-5342
audience: Data Architect, Orchestration Engineer, Marketer
doc-type: tutorial
activity: develop
feature: Destinations
exl-id: 31f46e37-f1c0-4730-8520-1ccd98df6501
source-git-commit: 3c86f9b19cecf92c9a324fb6fcfcefaebf82177f
workflow-type: tm+mt
source-wordcount: '281'
ht-degree: 4%

---

# 1.5 Agir : envoyer votre segment à Facebook ;

Accédez à [Adobe Experience Platform](https://experience.adobe.com/platform). Une fois connecté, vous accédez à la page d’accueil de Adobe Experience Platform.

![Ingestion des données](./images/home.png)

Avant de continuer, vous devez sélectionner une **sandbox**. L’environnement de test à sélectionner est nommé ``Bootcamp``. Pour ce faire, cliquez sur le texte **[!UICONTROL Production Prod]** dans la ligne bleue en haut de votre écran. Après avoir sélectionné le [!UICONTROL sandbox], vous verrez le changement d’écran et vous êtes maintenant dans votre [!UICONTROL sandbox].

![Ingestion des données](./images/sb1.png)

Dans le menu de gauche, accédez à **Destinations**, puis accédez à **Catalogue**. Vous verrez alors le **Catalogue des destinations**. Dans **Destinations**, cliquez sur **Activation des segments** sur le **Audience personnalisée facebook** carte.

![RTCDP](./images/rtcdpgoogleseg.png)

Sélectionner la destination **bootcamp-facebook** et cliquez sur **Suivant**.

![RTCDP](./images/rtcdpcreatedest2.png)

Dans la liste des segments disponibles, sélectionnez le segment que vous avez créé lors de l’exercice précédent. Cliquez sur **Suivant**.

![RTCDP](./images/rtcdpcreatedest3.png)

Sur le **Mappage** , assurez-vous que la variable **Appliquer la transformation** est activée. Cliquez sur **Suivant**.

![RTCDP](./images/rtcdpcreatedest4a.png)

Sur le **Planification des segments** , sélectionnez **Origine de votre audience** et définissez-le sur **Directement des clients**. Cliquez sur **Suivant**.

![RTCDP](./images/rtcdpcreatedest4.png)

Enfin, le **Réviser** page, cliquez sur **Terminer**.

![RTCDP](./images/rtcdpcreatedest5.png)

Votre segment est maintenant lié aux audiences personnalisées Facebook. Chaque fois qu’un client est admissible pour ce segment, un signal est envoyé côté serveur à Facebook pour inclure ce client dans l’audience personnalisée côté Facebook.

Dans Facebook, vous trouverez votre segment de Adobe Experience Platform sous Audiences personnalisées :

![RTCDP](./images/rtcdpcreatedest5b.png)

Vous pouvez maintenant voir votre audience personnalisée apparaître dans Facebook :

![RTCDP](./images/rtcdpcreatedest5a.png)

[Retour au flux utilisateur 1](./uc1.md)

[Revenir à tous les modules](../../overview.md)
