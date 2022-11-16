---
title: Création d’un schéma
description: Création d’un schéma
role: Developer
level: Intermediate
recommendations: noDisplay,noCatalog
kt: 10447
hide: true
hidefromtoc: true
exl-id: 25d77367-046d-46bd-9640-60fbcea263da
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '451'
ht-degree: 3%

---

# Création d’un schéma

Comme décrit dans [Structuration de vos données](../structuring-your-data.md), les données envoyées à Adobe Experience Platform doivent être dans XDM. Plus précisément, vos données doivent correspondre à un _schema_. Un schéma est essentiellement une description de ce à quoi les données doivent ressembler. Il décrit les noms des champs et leur emplacement dans les données. Il décrit également le type de valeur que chaque champ doit avoir (par exemple, une valeur booléenne, une chaîne de longueur de 12 caractères, un tableau de nombres).

Adobe Experience Platform fournit quelques blocs de création prêts à l’emploi, appelés groupes de champs, communs à l’industrie. Par exemple, pour le secteur des services financiers, il existe des groupes de champs pour les transferts d&#39;équilibre et les demandes de prêts. Pour l&#39;industrie du voyage et de l&#39;hôtellerie, il existe des groupes sur le terrain pour les réservations d&#39;avion et de logement.

Dans la mesure du possible, nous vous recommandons d’utiliser les groupes de champs intégrés lors de la création de votre schéma. Nous comprenons également que vous avez peut-être besoin de champs spécifiques à votre propre entreprise. C’est pourquoi vous pouvez créer vos propres groupes de champs personnalisés à utiliser dans les schémas que vous créez.

Examinons la création d’un schéma pour un site web d’e-commerce classique.

Tout d’abord, accédez au [!UICONTROL Schémas] dans Adobe Experience Platform.

![Vue Schémas](../../../assets/implementation-strategy/schemas-view.png)

Sélectionner [!UICONTROL Créer un schéma] dans le coin supérieur droit. Un menu s’affiche. Sélectionner [!UICONTROL XDM ExperienceEvent].

À ce stade, une boîte de dialogue s’affiche pour vous demander quels groupes de champs vous souhaitez ajouter à votre schéma. Le premier groupe de champs que vous devez sélectionner est le groupe de champs nommé [!UICONTROL ExperienceEvent du SDK Web AEP]. Ce groupe de champs ajoute un ensemble de champs qui prend en charge les données automatiquement collectées par le SDK Web de Adobe Experience Platform.

![Mixin SDK Web AEP](../../../assets/implementation-strategy/aep-web-sdk-mixin.png)

Comme le site web de ce tutoriel est un site web de commerce électronique, vous devez également sélectionner la variable [!UICONTROL Détails du commerce] groupe de champs. Ce groupe vous permet d’envoyer des données commerciales standard, telles que les produits affichés, ajoutés au panier et achetés.

![Mixin Détails du commerce](../../../assets/implementation-strategy/commerce-details-mixin.png)

Cliquez sur le bouton [!UICONTROL Ajouter des groupes de champs] en haut à droite de la boîte de dialogue. À ce stade, vous devriez voir la structure de votre schéma.

![Schéma avec mixins](../../../assets/implementation-strategy/schema-with-mixins.png)

Les groupes de champs que vous avez ajoutés sont répertoriés à gauche. La sélection d’un groupe de champs met en surbrillance les champs de droite fournis par ce groupe. Prenez quelques instants pour explorer les champs disponibles.

Enfin, sélectionnez [!UICONTROL Schéma sans titre] dans la partie gauche de l’écran, saisissez un nom et une description à droite de l’écran, puis cliquez sur [!UICONTROL Enregistrer].

![Schéma avec nom et description](../../../assets/implementation-strategy/schema-name-description.png)

Votre schéma a été créé. Apprenons ensuite comment créer un jeu de données destiné à contenir vos données.

Pour plus d’informations sur la création de schémas, voir [Création d’un schéma (interface utilisateur)](https://experienceleague.adobe.com/docs/experience-platform/xdm/tutorials/create-schema-ui.html?lang=fr).
