---
title: Création d’un schéma
description: Création d’un schéma
exl-id: 0256b358-0c2c-4c59-ab23-5fe0d38880d6
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '467'
ht-degree: 3%

---

# Création d’un schéma

Comme décrit dans [Structuration de vos données](../structuring-your-data.md), les données envoyées à Adobe Experience Platform doivent être dans XDM. Plus précisément, vos données doivent correspondre à un _schema_. Un schéma est essentiellement une description de ce à quoi les données doivent ressembler. Il décrit les noms des champs et leur emplacement dans les données. Il décrit également le type de valeur que chaque champ doit avoir (par exemple, une valeur booléenne, une chaîne de longueur de 12 caractères, un tableau de nombres).

Adobe Experience Platform fournit quelques blocs de création prêts à l’emploi, appelés groupes de champs, communs à l’industrie. Par exemple, pour le secteur des services financiers, il existe des groupes de champs pour les transferts d&#39;équilibre et les demandes de prêts. Pour l&#39;industrie du voyage et de l&#39;hôtellerie, il existe des groupes sur le terrain pour les réservations d&#39;avion et de logement.

Dans la mesure du possible, nous vous recommandons d’utiliser les groupes de champs intégrés lors de la création de votre schéma. Nous comprenons également que vous avez peut-être besoin de champs spécifiques à votre propre entreprise. C’est pourquoi vous pouvez créer vos propres groupes de champs personnalisés à utiliser dans les schémas que vous créez.

Examinons la création d’un schéma pour un site web d’e-commerce classique.

1. Sélectionner **[!UICONTROL Schémas]** under [!UICONTROL Data Management] dans le menu de gauche de l’interface de Adobe Experience Platform.
1. Sélectionner **[!UICONTROL Créer un schéma]** dans le coin supérieur droit, et **[!UICONTROL XDM ExperienceEvent]** dans le menu déroulant.

Vous vous trouvez maintenant sur le canevas du créateur de schémas.
![Vue Schémas](../assets/schemas-view.png)

## Ajouter des groupes de champs

1. Dans le **[!UICONTROL Groupes de champs]** sur le côté gauche de la **[!UICONTROL Structure]** , sélectionnez la zone **[!UICONTROL + Ajouter]** lien. À ce stade, un modal s’affiche pour sélectionner les groupes de champs à ajouter à votre schéma.
1. Tout d’abord, sélectionnez le groupe de champs nommé **[!UICONTROL ExperienceEvent du SDK Web AEP]**. Ce groupe de champs ajoute un ensemble de champs qui prend en charge les données automatiquement collectées par le SDK Web de Adobe Experience Platform.
   ![Mixin SDK Web AEP](../assets/aep-web-sdk-mixin.png)
1. Ensuite, comme le site web de ce tutoriel est un site web de commerce électronique, sélectionnez la variable **[!UICONTROL Détails du commerce]** groupe de champs. Ce groupe de champs vous permet d’envoyer des données commerciales standard, telles que les produits affichés, ajoutés au panier et achetés.
1. Sélectionnez la **[!UICONTROL Ajouter des groupes de champs]** en haut à droite de la boîte de dialogue.
   ![Mixin Détails du commerce](../assets/commerce-details-mixin.png)
1. À ce stade, vous devriez voir la structure de votre schéma.
   ![Schéma avec mixins](../assets/schema-with-mixins.png)

## Enregistrement du schéma

1. Indiquez enfin un nom et une description à droite de l’écran, puis sélectionnez **[!UICONTROL Enregistrer]**.
   ![Schéma avec nom et description](../assets/schema-name-description.png)

Votre schéma a été créé. Apprenons ensuite comment créer un jeu de données pour stocker vos données.

Pour plus d’informations sur la création de schémas, voir [Création de schémas](/help/platform/schemas/create-schemas.md).

[Suivant : ](create-a-dataset.md)

>[!NOTE]
>
>Merci d’avoir consacré votre temps à l’apprentissage de la collecte de données. Si vous avez des questions, souhaitez partager des commentaires généraux ou avez des suggestions sur le contenu futur, partagez-les à ce sujet. [Article de discussion de la communauté Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-use-adobe-experience-platform-data/m-p/543877)
