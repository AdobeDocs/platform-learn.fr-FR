---
title: Foundation - Profil client en temps réel - Création d’un segment - interface utilisateur
description: Foundation - Profil client en temps réel - Création d’un segment - interface utilisateur
kt: 5342
audience: Data Engineer, Data Architect, Marketer
doc-type: tutorial
activity: develop
exl-id: 2462addc-6123-44e6-991c-0e5c21256448
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '723'
ht-degree: 3%

---

# 3.4 Création d’un segment - IU

Dans cet exercice, vous allez créer un segment à l’aide du créateur de segments de Adobe Experience Platform.

## Histoire

Accédez à [Adobe Experience Platform](https://experience.adobe.com/platform). Une fois connecté, vous accédez à la page d’accueil de Adobe Experience Platform.

![Ingestion des données](../module2/images/home.png)

Avant de continuer, vous devez sélectionner une **sandbox**. L’environnement de test à sélectionner est nommé ``--aepSandboxId--``. Pour ce faire, cliquez sur le texte **[!UICONTROL Production Prod]** dans la ligne bleue en haut de votre écran. Après avoir sélectionné le [!UICONTROL sandbox], vous verrez le changement d’écran et vous êtes maintenant dans votre [!UICONTROL sandbox].

![Ingestion des données](../module2/images/sb1.png)

Dans le menu de gauche, accédez à **Segments**. Sur cette page, vous pouvez voir un aperçu de tous les segments existants. Cliquez sur le bouton **+ Créer un segment** pour commencer à créer un segment.

![Segmentation](./images/menuseg.png)

Une fois que vous êtes dans le nouveau créateur de segments, vous constatez immédiatement que la variable **Attributs** et l’option **XDM Individual Profile** référence.

![Segmentation](./images/segmentationui.png)

Étant donné que XDM est le langage qui alimente les activités d’expérience, XDM est également la base du créateur de segments. Toutes les données ingérées dans Platform doivent être mappées sur XDM. Par conséquent, toutes les données font partie du même modèle de données, quel que soit l’endroit d’où elles proviennent. Cela vous offre un grand avantage lors de la création de segments. Comme dans cette interface utilisateur du créateur de segments, vous pouvez combiner des données provenant de n’importe quelle origine dans le même workflow. Les segments créés dans le créateur de segments peuvent être envoyés à des solutions telles qu’Adobe Target, Adobe Campaign et Adobe Audience Manager pour activation.

Créons un segment qui comprend tous les **male** clients.

Pour accéder à l’attribut gender , vous devez comprendre et connaître XDM.

Le genre est un attribut de Personne, qui se trouve sous Attributs. Pour y arriver, cliquez sur **XDM Individual Profile**. Vous verrez alors ceci. Dans la **XDM Individual Profile** fenêtre, sélectionnez **Personne**.

![Segmentation](./images/person.png)

Vous verrez alors ceci. Dans **Personne**, vous pouvez trouver la variable **Genre** attribut. Faites glisser l’attribut Genre sur le créateur de segments.

![Segmentation](./images/gender.png)

Vous pouvez désormais choisir le genre spécifique parmi les options préremplies. Dans ce cas, choisissons **Masculin**.

![Segmentation](./images/genderselection.png)

Après avoir sélectionné **Masculin**, vous pouvez obtenir une estimation de la population du segment en poussant la variable **Actualiser l’estimation** bouton . Cela s’avère très utile pour un utilisateur chargé de la conception de parcours, de sorte qu’il puisse voir l’impact de certains attributs sur la taille du segment obtenue.

![Segmentation](./images/segmentpreview.png)

Vous verrez ensuite une estimation comme celle-ci :

![Segmentation](./images/segmentpreviewest.png)

Ensuite, vous devez affiner un peu votre segment. Vous devez créer un segment de tous les clients masculins qui ont consulté le produit. **Veste de sport Proteus (orange)**.

Pour créer ce segment, vous devez ajouter un événement d’expérience. Vous pouvez trouver tous les événements d’expérience en cliquant sur la variable **Événements** dans le **Champs** de la barre de menus.

![Segmentation](./images/findee.png)

Ensuite, vous verrez le niveau supérieur, **XDM ExperienceEvents** noeud . Cliquez sur **XDM ExperienceEvent**.

![Segmentation](./images/see.png)

Accédez à **Éléments de liste de produits**.

![Segmentation](./images/plitems.png)

Sélectionner **Nom** et faites glisser et déposez le **Nom** du menu de gauche sur le canevas du créateur de segments dans la **Événements** .

![Segmentation](./images/eeweb.png)

Vous verrez alors :

![Segmentation](./images/eewebpdtlname.png)

Le paramètre de comparaison doit être **est égal à** et dans le champ de saisie, saisissez **JACKET ÉOLIEN DE MONTANA**.

![Segmentation](./images/pv.png)

Chaque fois que vous ajoutez un élément au créateur de segments, vous pouvez cliquer sur le **Actualiser l’estimation** pour obtenir une nouvelle estimation de la population de votre segment.

Jusqu’à présent, vous avez uniquement utilisé l’interface utilisateur pour créer votre segment, mais il existe également une option de code pour créer un segment.

Lors de la création d’un segment, vous composez en fait une requête PQL (Profile Query Language). Pour visualiser le code PQL, vous pouvez cliquer sur le **Affichage du code** sélecteur dans le coin supérieur droit du créateur de segments.

![Segmentation](./images/codeview.png)

Vous pouvez maintenant voir l’instruction PQL complète :

```sql
person.gender in ["male"] and CHAIN(xEvent, timestamp, [C0: WHAT(productListItems.exists(name.equals("MONTANA WIND JACKET", false)))])
```

Vous pouvez également prévisualiser un exemple des profils client qui font partie de ce segment, en cliquant sur **Afficher les profils**.

![Segmentation](./images/previewprofiles.png)

![Segmentation](./images/previewprofilesdtl.png)

Enfin, attribuons un nom à votre segment et enregistrez-le.

Pour définir une convention d’affectation des noms, utilisez :

- `--demoProfileLdap-- - Male customers with interest in Montana Wind Jacket`

![Segmentation](./images/segmentname.png)

Cliquez ensuite sur le bouton **Enregistrer et fermer** pour enregistrer votre segment, puis revenir à la page d’aperçu du segment .

![Segmentation](./images/savedsegment.png)

Vous pouvez maintenant poursuivre l’exercice suivant et créer un segment via l’API.

Étape suivante : [3.5 Création d’un segment - API](./ex5.md)

[Revenir au module 3](./real-time-customer-profile.md)

[Revenir à tous les modules](../../overview.md)
