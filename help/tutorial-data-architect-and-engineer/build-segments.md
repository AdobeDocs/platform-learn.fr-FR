---
title: Créer des segments
seo-title: Build segments | Getting Started with Adobe Experience Platform for Data Architects and Data Engineers
breadcrumb-title: Créer des segments
description: Dans cette leçon, nous allons créer certains segments en fonction des données de profil que nous avons ingérées dans les leçons précédentes.
role: Data Architect
feature: Data Governance
jira: KT-4348
thumbnail: 4348-build-segments.jpg
exl-id: cd05e814-1ea7-48ba-adf6-1a71504c623e
source-git-commit: 90f7621536573f60ac6585404b1ac0e49cb08496
workflow-type: tm+mt
source-wordcount: '904'
ht-degree: 2%

---

# Créer des segments

<!-- 30 min-->
Dans cette leçon, nous allons créer certains segments en fonction des données de profil que nous avons ingérées dans les leçons précédentes.

Une fois que vous disposez de profils clients en temps réel, vous pouvez créer des segments d’individus qui partagent des caractéristiques similaires et qui peuvent répondre de la même manière aux stratégies marketing. Les blocs de création de ces segments sont les champs XDM que vous avez créés précédemment.

**Architectes de données** Vous devrez créer des segments en dehors de ce tutoriel et prendre en charge leurs collègues dans cette tâche.

Avant de commencer les exercices, regardez cette courte vidéo pour en savoir plus sur la création de segments :
>[!VIDEO](https://video.tv.adobe.com/v/27254?quality=12&learn=on)


## Autorisations requises

Dans le [Configuration des autorisations](configure-permissions.md) leçon, vous configurez tous les contrôles d’accès requis pour terminer cette leçon, en particulier :

* Éléments d’autorisation **[!UICONTROL Gestion des profils]** > **[!UICONTROL Gestion des segments]**, **[!UICONTROL Affichage de segments]**, et **[!UICONTROL Exportation du segment d’audience]**
* Éléments d’autorisation **[!UICONTROL Gestion des profils]** > **[!UICONTROL Afficher les profils]**, et **[!UICONTROL Gestion des profils]**
* Élément d’autorisation **[!UICONTROL Environnements de test]** > `Luma Tutorial`
* Accès des rôles utilisateur à la variable `Luma Tutorial Platform` profil de produits
* Accès des développeurs au `Luma Tutorial Platform` profil de produit (pour l’API)

## Création d’un segment de base

Créons un segment simple pour les clients du programme de fidélité ayant un statut Gold ou Platine.

1. Dans l’interface utilisateur de Platform, accédez à **[!UICONTROL Segments]** dans le volet de navigation de gauche
1. Sélectionnez la **[!UICONTROL Créer un segment]** button
1. À gauche du créateur de schémas se trouvent trois onglets pour les attributs (données d’enregistrement), les événements (données de série temporelle) et les audiences.
1. Sélectionnez l’icône d’engrenage pour noter que le créateur de segments affiche par défaut uniquement les champs contenant des données et vous permet de modifier la stratégie de fusion.
1. Dans l’onglet Attributs , accédez à la **XDM Individual Profile > Loyalty** dossier (vous pouvez également rechercher &quot;loyalty&quot;)
1. Effectuez un glisser-déposer, `Tier` du menu des champs d’attribut au canevas du créateur de segments
1. Sélectionner `Tier` est égal à `Gold` ou `Platinum`
1. Sélectionner **[!UICONTROL Actualiser l’estimation]** pour déterminer le nombre de profils qualifiés pour votre segment
1. Comme la variable **[!UICONTROL Nom]**, saisissez `Luma customers with level Gold or Above`
1. Sélectionnez **[!UICONTROL Enregistrer]**
   ![Segment](assets/segment-goldOrAbove.png)

<!--## Build a sequential segment-->

## Création d’un segment dynamique

Au cours de cet exercice, nous allons créer un segment pour les clients qui ont acheté le même produit deux fois dans les 30 jours. Les segments dynamiques vous permettent de mettre à l’échelle votre segmentation à l’aide de champs en tant que variables.

1. Accédez à **[!UICONTROL Segments]** dans le volet de navigation de gauche
1. Sélectionnez la **[!UICONTROL Créer un segment]** button
1. Sélectionnez la **[!UICONTROL Événements]** tab
1. Filtrez la liste sur `purchases`
1. Faites glisser le **[!UICONTROL Achats]** type d’événement sur la zone de travail _deux fois distinctes_
1. Sélectionner l’icône de l’horloge entre les deux **[!UICONTROL Achats]** et sélectionnez &quot;dans les 30 jours&quot;
1. Confirmez que votre définition de segment à ce stade se lit comme suit : **&quot;Inclure l’audience qui comporte au moins 1 événement Achats puis au moins 1 événement Achats dans les 30 jours&quot;**
   ![Deux achats dans les 30 jours](assets/segment-twoPurchases.png)
1. Maintenant, remplacez le filtre d’événement par `sku`
1. Faites glisser le champ SKU vers le deuxième événement d’achat
   ![Deux achats dans les 30 jours avec le SKU](assets/segment-twoPurchases-addSku.png)
1. Désormais, effacez le filtre d’événement.
1. Vous devriez voir dans la **[!UICONTROL Parcourir les variables]** , il existe des dossiers pour les deux événements d’achat. Cliquez pour explorer **[!UICONTROL Achats 1]**\
   ![Deux achats dans les 30 jours avec le SKU, parcourez le premier achat](assets/segment-twoPurchases-browsePurchaseOne.png)
1. Explorez les **[!UICONTROL Éléments de la liste de produits]** , sélectionnez **[!UICONTROL SKU]** et faites-le glisser à droite du champ **[!UICONTROL est égal à]** opérande. Lorsque vous survolez la zone, déposez-la dans la section &quot;Ajouter pour comparer les opérandes&quot;.
1. Nommer votre segment `Bought same product within 30 days`
1. Confirmez que votre définition d’audience est **&quot;Inclure l’audience qui comporte au moins 1 événement Achats puis, dans les 30 jours, au moins 1 événement Achats où ((SKU = Achats1 SKU)&quot;**
1. Sélectionnez la **[!UICONTROL Enregistrer]** button

   ![Achat du même produit dans le segment des 30 derniers jours](assets/segment-boughtSameProduct.png)

## Création d’un segment d’entités multiples

Rappelez-vous comment nous avons créé la relation entre le `Luma Offline Purchase Events Schema` et le `Luma Product Catalog Schema` dans les leçons précédentes ? Nous l’avons fait pour pouvoir utiliser la relation dans notre schéma à l’aide de la segmentation d’entités multiples.

Grâce à la fonction de segmentation d’entités multiples avancée, vous pouvez créer des segments à l’aide de plusieurs classes XDM pour étendre vos schémas. Par conséquent, le créateur de segments peut accéder à des champs supplémentaires comme s’ils étaient natifs de l’entrepôt de données de profil.

Vous allez créer le segment suivant en appliquant la relation que vous avez créée entre vos `Luma Product Catalog Schema` et votre `Luma Offline Purchase Events Schema`.

1. Accédez à **[!UICONTROL Segments]** dans le volet de navigation de gauche
1. Sélectionnez la **[!UICONTROL Créer un segment]** button
1. Sélectionnez la **[!UICONTROL Événements]** tab
1. Filtrez la liste sur `purchases`
1. Faites glisser le **[!UICONTROL Achats]** type d’événement sur la zone de travail
1. Sélectionnez la liste déroulante de l’horloge au-dessus de l’événement et choisissez **[!UICONTROL dans les 30 derniers jours]**
1. Filtrez les **[!UICONTROL Événements]** à `category` puis faites glisser le **[!UICONTROL Catégorie de produits]** champ sur **[!UICONTROL Achats]**
1. Modifiez l’opérateur en **[!UICONTROL commence par]** et saisissez `men` dans la zone de texte
1. Comme la variable **[!UICONTROL Nom]**, saisissez `Purchased a Men's product in the last 30 days`
1. Confirmation de la définition de l’audience `(Include audience who have at least 1 Purchases event where ((Product Category starts with men)) ) and occurs in last 30 day(s)`
1. Sélectionnez la **[!UICONTROL Enregistrer]** button

   ![Achat du même produit dans le segment des 30 derniers jours](assets/segment-purchasedMens.png)

## Segmentation par lots et par flux

Cliquez sur **[!UICONTROL Segments]** dans le volet de navigation de gauche, prenons quelques instants pour passer en revue nos trois segments :

* Deux de nos segments sont des segments par lot et l’autre est un segment par flux.
* Platform opte par défaut pour la segmentation par flux chaque fois que cela est possible, ce qui qualifie le client pour un segment dès qu’il répond aux critères. Lorsque les définitions de segment sont trop complexes pour la diffusion en continu, elles sont automatiquement converties en lot. Dans ce cas, les deux segments étaient par défaut par lot, car la période d’analyse des événements d’achat était supérieure à sept jours. Pour obtenir la liste complète et actuelle des limites de diffusion en continu, voir [la documentation](https://experienceleague.adobe.com/docs/experience-platform/segmentation/ui/streaming-segmentation.html).
* Les tâches par lots s’exécutent selon un calendrier quotidien, qui peut être désactivé.

![Achat du même produit dans le segment des 30 derniers jours](assets/segment-review.png)

## Ressources supplémentaires

* [Documentation de Segmentation Service](https://experienceleague.adobe.com/docs/experience-platform/segmentation/home.html?lang=fr)
* [Référence de l’API Segmentation Service](https://www.adobe.io/experience-platform-apis/references/segmentation/)

La segmentation comporte d’autres avantages, en particulier l’activation des segments. Ces sujets seront abordés dans un autre tutoriel.

Vous avez réussi à travers tous les exercices ! Veuillez passer à la [Conclusion](conclusion.md).
