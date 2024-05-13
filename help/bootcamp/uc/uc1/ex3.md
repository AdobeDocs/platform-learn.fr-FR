---
title: Bootcamp - Real-time Customer Profile - Création d’une audience - interface utilisateur
description: Bootcamp - Real-time Customer Profile - Création d’une audience - interface utilisateur
jira: KT-5342
audience: Data Engineer, Data Architect, Marketer
doc-type: tutorial
activity: develop
feature: Audiences
exl-id: 37d4a5e8-e2bc-4c8c-a74f-09f74ea79962
source-git-commit: 5876de5015e4c8c337c235c24cc28b0a32e274dd
workflow-type: tm+mt
source-wordcount: '533'
ht-degree: 3%

---

# 1.3 Création d’une audience - IU

Au cours de cet exercice, vous allez créer une audience en utilisant le créateur d’audiences Adobe Experience Platform.

## Histoire

Accédez à [Adobe Experience Platform](https://experience.adobe.com/platform). Une fois connecté, vous accédez à la page d’accueil de Adobe Experience Platform.

![Ingestion des données](./images/home.png)

Avant de continuer, vous devez sélectionner une **sandbox**. L’environnement de test à sélectionner est nommé ``Bootcamp``. Pour ce faire, cliquez sur le texte **[!UICONTROL Production]** dans la ligne bleue en haut de votre écran. Après avoir sélectionné le [!UICONTROL sandbox], vous verrez le changement d’écran et vous êtes maintenant dans votre [!UICONTROL sandbox].

![Ingestion des données](./images/sb1.png)

Dans le menu de gauche, accédez à **Audiences**. Sur cette page, vous verrez des tableaux de bord contenant des informations essentielles sur **Audience** performance.

![Segmentation](./images/menuseg.png)

Cliquez sur **Parcourir** pour afficher un aperçu de toutes les audiences existantes. Cliquez sur le bouton **+ Créer une audience** pour créer une audience.


![Segmentation](./images/segmentationui.png)

Une pop-Ip s’affiche, vous demandant si vous souhaitez : **&#39;Composer l&#39;audience&#39;** ou **&#39;Créer une règle&#39;**. Choisir **&#39;Créer une règle&#39;** pour continuer et cliquez sur **create**.

![Segmentation][def]

Une fois que vous êtes dans le créateur d’audiences, vous remarquez immédiatement le **Attributs** et l’option **XDM Individual Profile** référence.


Étant donné que XDM est le langage qui alimente les activités d’expérience, XDM est également la base du créateur d’audiences. Toutes les données ingérées dans Platform doivent être mappées sur XDM. Par conséquent, toutes les données font partie du même modèle de données, quel que soit l’endroit d’où elles proviennent. Cela vous offre un grand avantage lors de la création d’audiences. Comme dans cette interface utilisateur du créateur d’audiences, vous pouvez combiner des données provenant de n’importe quelle origine dans le même workflow. Les audiences créées dans Audience Builder peuvent être envoyées à des solutions telles qu’Adobe Target, Adobe Campaign ou tout autre canal d’activation.

Vous devez maintenant créer une audience de tous les clients qui ont consulté le produit. **Real-Time CDP**.

Pour créer cette audience, vous devez ajouter un événement d’expérience. Vous pouvez trouver tous les événements d’expérience en cliquant sur la variable **Événements** dans le **Champs** de la barre de menus.

![Segmentation](./images/findee.png)

Ensuite, vous verrez le niveau supérieur, **XDM ExperienceEvents** noeud . Cliquez sur **XDM ExperienceEvent**.

![Segmentation](./images/see.png)

Accédez à **Éléments de liste de produits**.

![Segmentation](./images/plitems.png)

Sélectionner **Nom** et faites glisser et déposez le **Nom** du menu de gauche sur le canevas du créateur d’audiences dans la **Événements** . Vous verrez alors :

![Segmentation](./images/eewebpdtlname.png)

Le paramètre de comparaison doit être **est égal à** et dans le champ de saisie, saisissez **CDP en temps réel**.

![Segmentation](./images/pv.png)

Chaque fois que vous ajoutez un élément au créateur d’audiences, vous pouvez cliquer sur le **Actualiser l’estimation** pour obtenir une nouvelle estimation de la population de votre audience.

![Segmentation](./images/refreshest.png)

As **Méthode d’évaluation**, sélectionnez **Edge**.

![Segmentation](./images/evedge.png)

Enfin, attribuons un nom à votre audience et enregistrez-le.

Pour définir une convention d’affectation des noms, utilisez :

- `yourLastName - Interest in Real-Time CDP`

Cliquez ensuite sur le bouton **Enregistrer et fermer** pour enregistrer votre audience.

![Segmentation](./images/segmentname.png)

Revenez maintenant à la page d’aperçu de l’audience, où vous trouverez un exemple d’aperçu des profils de clients qui remplissent les critères de votre audience.

![Segmentation](./images/savedsegment.png)

Vous pouvez maintenant poursuivre l’exercice suivant et utiliser votre audience avec Adobe Target.

Étape suivante : [1.4 Action à effectuer : envoyez votre audience à Adobe Target](./ex4.md)

[Retour au flux utilisateur 1](./uc1.md)

[Revenir à tous les modules](../../overview.md)


[def]: ./images/segmentationpopup.png
