---
title: Bootcamp - Real-time Customer Profile - Création d’un segment - interface utilisateur
description: Bootcamp - Real-time Customer Profile - Création d’un segment - interface utilisateur
jira: KT-5342
audience: Data Engineer, Data Architect, Marketer
doc-type: tutorial
activity: develop
feature: Segments
exl-id: 37d4a5e8-e2bc-4c8c-a74f-09f74ea79962
source-git-commit: ee5c0af17c12f1d90774a3a4150c9788e2368e39
workflow-type: tm+mt
source-wordcount: '496'
ht-degree: 3%

---

# 1.3 Création d’un segment - IU

Dans cet exercice, vous allez créer un segment à l’aide du créateur de segments de Adobe Experience Platform.

## Histoire

Accédez à [Adobe Experience Platform](https://experience.adobe.com/platform). Une fois connecté, vous accédez à la page d’accueil de Adobe Experience Platform.

![Ingestion des données](./images/home.png)

Avant de continuer, vous devez sélectionner une **sandbox**. L’environnement de test à sélectionner est nommé ``Bootcamp``. Pour ce faire, cliquez sur le texte **[!UICONTROL Production Prod]** dans la ligne bleue en haut de votre écran. Après avoir sélectionné le [!UICONTROL sandbox], vous verrez le changement d’écran et vous êtes maintenant dans votre [!UICONTROL sandbox].

![Ingestion des données](./images/sb1.png)

Dans le menu de gauche, accédez à **Segments**. Sur cette page, vous pouvez voir un aperçu de tous les segments existants. Cliquez sur le bouton **+ Créer un segment** pour commencer à créer un segment.

![Segmentation](./images/menuseg.png)

Une fois que vous êtes dans le nouveau créateur de segments, vous constatez immédiatement que la variable **Attributs** et l’option **XDM Individual Profile** référence.

![Segmentation](./images/segmentationui.png)

Étant donné que XDM est le langage qui alimente les activités d’expérience, XDM est également la base du créateur de segments. Toutes les données ingérées dans Platform doivent être mappées sur XDM. Par conséquent, toutes les données font partie du même modèle de données, quel que soit l’endroit d’où elles proviennent. Cela vous offre un grand avantage lors de la création de segments. Comme dans cette interface utilisateur du créateur de segments, vous pouvez combiner des données provenant de n’importe quelle origine dans le même workflow. Les segments créés dans le créateur de segments peuvent être envoyés à des solutions telles qu’Adobe Target, Adobe Campaign et Adobe Audience Manager pour activation.

Vous devez maintenant créer un segment de tous les clients qui ont consulté le produit. **Real-Time CDP**.

Pour créer ce segment, vous devez ajouter un événement d’expérience. Vous pouvez trouver tous les événements d’expérience en cliquant sur la variable **Événements** dans le **Champs** de la barre de menus.

![Segmentation](./images/findee.png)

Ensuite, vous verrez le niveau supérieur, **XDM ExperienceEvents** noeud . Cliquez sur **XDM ExperienceEvent**.

![Segmentation](./images/see.png)

Accédez à **Éléments de liste de produits**.

![Segmentation](./images/plitems.png)

Sélectionner **Nom** et faites glisser et déposez le **Nom** du menu de gauche sur le canevas du créateur de segments dans la **Événements** . Vous verrez alors :

![Segmentation](./images/eewebpdtlname.png)

Le paramètre de comparaison doit être **est égal à** et dans le champ de saisie, saisissez **CDP en temps réel**.

![Segmentation](./images/pv.png)

Chaque fois que vous ajoutez un élément au créateur de segments, vous pouvez cliquer sur le **Actualiser l’estimation** pour obtenir une nouvelle estimation de la population de votre segment.

![Segmentation](./images/refreshest.png)

As **Méthode d’évaluation**, sélectionnez **Edge**.

![Segmentation](./images/evedge.png)

Enfin, attribuons un nom à votre segment et enregistrez-le.

Pour définir une convention d’affectation des noms, utilisez :

- `yourLastName - Interest in Real-Time CDP`

Cliquez ensuite sur le bouton **Enregistrer et fermer** pour enregistrer votre segment.

![Segmentation](./images/segmentname.png)

Revenez maintenant à la page d’aperçu des segments, où vous trouverez un exemple d’aperçu des profils de clients qui remplissent les critères de votre segment.

![Segmentation](./images/savedsegment.png)

Vous pouvez maintenant passer à l’exercice suivant et utiliser votre segment avec Adobe Target.

Étape suivante : [1.4 Agir : envoyer votre segment à Adobe Target ;](./ex4.md)

[Retour au flux utilisateur 1](./uc1.md)

[Revenir à tous les modules](../../overview.md)
