---
title: Création dʼun flux de données
description: Création dʼun flux de données
exl-id: 4a33a7f3-8bd8-4d28-9ae4-a0609444485f
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '467'
ht-degree: 1%

---

# Création dʼun flux de données

Les données que vous envoyez à partir de votre site web avec le SDK Web de Platform atteignent un ensemble de serveurs Adobe appelés [Adobe Experience Platform Edge Network](https://business.adobe.com/products/experience-platform/experience-platform-edge-network.html). Ce réseau peut envoyer vos données au [Jeu de données Adobe Experience Platform que vous avez créé précédemment](create-a-schema.md) et d’autres produits dans Adobe Experience Cloud. Ces produits Adobe peuvent également répondre avec des données à votre page web. Par exemple, Edge Network peut renvoyer du contenu de personnalisation à partir d’Adobe Target.

Pour configurer les produits Adobe pour lesquels Edge Network interrompt les données, vous devez créer un flux de données. Lorsqu’Edge Network reçoit des données de votre page web, il consulte le flux de données que vous avez créé, lit sa configuration, puis transmet les données aux produits d’Adobe appropriés.

![Configuration du produit Datastream](../assets/datastream-diagram.png)

1. Pour créer un flux de données, vous devez d’abord accéder à l’interface utilisateur de la collecte de données. Dans le coin supérieur droit de Platform, cliquez sur le **[!UICONTROL Sélecteur d’application]** et sélectionnez **[!UICONTROL Collecte de données]** dans le menu déroulant.
   ![Menu de collecte de données](../assets/data-collection-menu.png)
1. Une fois que l’interface de collecte de données s’affiche, sélectionnez **[!UICONTROL Datastreams]** dans le volet de navigation de gauche, puis le **[!UICONTROL Nouvelle structure de données]** dans le coin supérieur droit.
1. Attribuez un nom au flux de données, puis sélectionnez [le schéma que vous avez créé précédemment ;](create-a-schema.md) comme la propriété **[!UICONTROL Jeu de données d’événement]**, puis sélectionnez **[!UICONTROL Enregistrer]** (le mappage est abordé ultérieurement).
   ![Nom et description de la structure de données](../assets/datastream-name-description.png)

## Ajout d’un service à un flux de données

L’écran suivant vous permet d’ajouter quels produits et services Adobe doivent recevoir les données que vous envoyez depuis votre site web.

1. Sélectionnez la **[!UICONTROL Ajouter un service]** . Pour les besoins de ce tutoriel, activez uniquement Adobe Experience Platform, sélectionnez [le jeu de données que vous avez créé précédemment ;](create-a-dataset.md) et sélectionnez **[!UICONTROL Enregistrer]** dans le coin supérieur droit. Votre flux de données a été créé.
   ![Configuration du produit Datastream](../assets/datastream-product-configuration.png)

## Environnements de flux de données

Les entreprises disposent généralement d’un chemin de promotion pour toutes les mises à jour de site web. Une personne de l’entreprise (un spécialiste du marketing ou un ingénieur, selon les modifications) teste généralement ses modifications dans un environnement de développement que seule cette personne utilise. Une fois que les modifications leur conviennent, elles sont promues dans un environnement d’évaluation où elles font l’objet d’autres tests. Enfin, les modifications sont publiées sur le site web de production que les utilisateurs voient. Les flux de données prennent en charge ce modèle de promotion.

Si vous prenez en charge des applications basées sur Platform telles que la plateforme de données clients en temps réel, Journey Optimizer ou Customer Journey Analytics, des flux de données supplémentaires doivent être créés dans des environnements de test Platform distincts qui correspondent à ces environnements.

Si vous n’êtes pas client Platform, vous pouvez créer plusieurs flux de données dans un seul environnement de test et utiliser la fonction de copie de flux de données pour dupliquer les paramètres.

Le serveur est maintenant entièrement configuré pour recevoir les données de votre page web.

[Suivant : ](../configure-the-client/whats-a-data-layer.md)

>[!NOTE]
>
>Merci d’avoir consacré votre temps à l’apprentissage de la collecte de données. Si vous avez des questions, souhaitez partager des commentaires généraux ou avez des suggestions sur le contenu futur, partagez-les à ce sujet. [Article de discussion de la communauté Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-use-adobe-experience-platform-data/m-p/543877)
