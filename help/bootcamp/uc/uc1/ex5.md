---
title: Bootcamp - CDP en temps réel - Créer une audience et agir - Envoyer votre audience à DV360
description: Bootcamp - CDP en temps réel - Créer une audience et agir - Envoyer votre audience à DV360
jira: KT-5342
audience: Data Architect, Orchestration Engineer, Marketer
doc-type: tutorial
activity: develop
feature: Destinations
exl-id: 31f46e37-f1c0-4730-8520-1ccd98df6501
source-git-commit: 5876de5015e4c8c337c235c24cc28b0a32e274dd
workflow-type: tm+mt
source-wordcount: '281'
ht-degree: 3%

---

# 1.5 Action : envoyez votre audience à Facebook

Accédez à [Adobe Experience Platform](https://experience.adobe.com/platform). Une fois connecté, vous accédez à la page d’accueil de Adobe Experience Platform.

![Ingestion des données](./images/home.png)

Avant de continuer, vous devez sélectionner un **sandbox**. L’environnement de test à sélectionner est nommé ``Bootcamp``. Pour ce faire, cliquez sur le texte **[!UICONTROL Production Prod]** dans la ligne bleue en haut de votre écran. Après avoir sélectionné l’[!UICONTROL sandbox] approprié, vous verrez le changement d’écran et vous êtes désormais dans votre [!UICONTROL sandbox] dédié.

![Ingestion des données](./images/sb1.png)

Dans le menu de gauche, accédez à **Destinations**, puis à **Catalogue**. Vous verrez ensuite le **catalogue des destinations**. Dans **Destinations**, cliquez sur **Activer les audiences** sur la carte **Audience personnalisée Facebook**.

![RTCDP](./images/rtcdpgoogleseg.png)

Sélectionnez la destination **bootcamp-facebook** et cliquez sur **Suivant**.

![RTCDP](./images/rtcdpcreatedest2.png)

Dans la liste des audiences disponibles, sélectionnez l’audience que vous avez créée lors de l’exercice précédent. Cliquez sur **Suivant**.

![RTCDP](./images/rtcdpcreatedest3.png)

Sur la page **Mapping**, assurez-vous que la case **Apply Transformation** est activée. Cliquez sur **Suivant**.

![RTCDP](./images/rtcdpcreatedest4a.png)

Sur la page **Audience Schedule**, sélectionnez l’ **origine de votre audience** et définissez-la sur **Directly from clients**. Cliquez sur **Suivant**.

![RTCDP](./images/rtcdpcreatedest4.png)

Enfin, sur la page **Review**, cliquez sur **Terminer**.

![RTCDP](./images/rtcdpcreatedest5.png)

Votre audience est maintenant liée aux audiences personnalisées Facebook. Chaque fois qu’un client est admissible pour cette audience, un signal est envoyé côté serveur à Facebook pour inclure ce client dans l’audience personnalisée côté Facebook.

Dans Facebook, vous trouverez votre audience de Adobe Experience Platform sous Audiences personnalisées :

![RTCDP](./images/rtcdpcreatedest5b.png)

Vous pouvez maintenant voir votre audience personnalisée apparaître dans Facebook :

![RTCDP](./images/rtcdpcreatedest5a.png)

[Retour au flux utilisateur 1](./uc1.md)

[Revenir à tous les modules](../../overview.md)
