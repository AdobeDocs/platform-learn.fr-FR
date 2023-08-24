---
title: Configurer un train de données
description: Découvrez comment créer un flux de données dans Experience Platform.
feature: Mobile SDK,Datastreams
hide: true
source-git-commit: 7de7c7e13ea6d02f1193620e0cc35299e07d59e5
workflow-type: tm+mt
source-wordcount: '552'
ht-degree: 9%

---


# Création dʼun flux de données

Découvrez comment créer un flux de données dans Experience Platform.

Un flux de données est une configuration côté serveur sur Platform Edge Network. Le flux de données garantit que les données entrantes vers Platform Edge Network sont acheminées vers les applications et services Adobe Experience Cloud de manière appropriée. Pour plus d’informations, voir [documentation](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/datastreams.html?lang=fr) ou ceci [video](https://experienceleague.adobe.com/docs/platform-learn/data-collection/edge-network/configure-datastreams.html?lang=fr).

## Conditions préalables

Pour créer un flux de données, votre organisation doit être configurée pour cette fonctionnalité dans l’interface de collecte de données (anciennement [!UICONTROL Launch]) et que vous devez disposer des autorisations utilisateur pour [!UICONTROL Experience Platform] > [!UICONTROL Collecte de données] > **[!UICONTROL Gestion des flux de données]** et **[!UICONTROL Affichage des flux de données]**.

## Objectifs d&#39;apprentissage

Dans cette leçon, vous allez :

* Savoir quand utiliser un flux de données.
* Création dʼun flux de données.
* Configurer un train de données.

## Création dʼun flux de données

Les flux de données peuvent être créés dans la variable [!UICONTROL Collecte de données] à l’aide de la fonction [!UICONTROL Datastream] de configuration. Pour créer un flux de données :

1. Assurez-vous que vous vous trouvez dans l’environnement de test Experience Platform correct, car les flux de données sont définis au niveau de l’environnement de test.
1. Sélectionner **[!UICONTROL Datastreams]** dans le rail de gauche.
1. Sélectionnez **[!UICONTROL Nouveau flux de données]**.

   ![accueil des datastreams](assets/datastream-new.png)

1. Fournissez une **[!UICONTROL Nom]**, par exemple `Luma Mobile App` et un **[!UICONTROL Description]**, par exemple `Datastream for Luma Mobile App`.
1. Sélectionnez le schéma que vous avez créé dans la leçon précédente à partir du **Schéma d’événement** une liste.
1. Sélectionnez **[!UICONTROL Enregistrer]**.

   ![nouveaux flux de données](assets/datastream-name.png)


## Ajout de services

Ensuite, vous connectez vos services Experience Cloud à votre flux de données. Lorsque le SDK Mobile Platform envoie des données à Edge Network, le flux de données envoie les données à ces services :

1. Sélectionnez **[!UICONTROL Ajouter un service]**.

1. Ajouter **[!UICONTROL Adobe Analytics]** de la [!UICONTROL Service] list,

1. Entrez le nom du site de rapports dans lequel vous souhaitez utiliser **[!UICONTROL Identifiant de suite de rapports]**.

1. Activez le service en basculant **[!UICONTROL Activé]** sur .

1. Sélectionnez **[!UICONTROL Enregistrer]**.

   ![Ajout d’Adobe Analytics en tant que service de flux de données](assets/datastream-service-aa.png)

Vous pouvez également activer le service Adobe Experience Platform.

>[!IMPORTANT]
>
>Vous ne pouvez activer le service Adobe Experience Platform que lorsque vous avez créé un jeu de données d’événement. Si vous n’avez pas encore créé de jeu de données d’événement, suivez les instructions. [here](platform.md).

1. Cliquez sur ![Ajouter](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) **[!UICONTROL Ajouter un service]** pour ajouter un autre service.

1. Sélectionnez **[!UICONTROL Adobe Experience Platform]** dans la liste [!UICONTROL Service].

1. Activez le service en basculant **[!UICONTROL Activé]** sur .

1. Sélectionnez la variable **[!UICONTROL Jeu de données d’événement]** que vous avez créé dans le cadre de la [Création d’un jeu de données](platform.md#create-a-dataset) par exemple, **Jeu de données d’événement d’application mobile Luma**

1. Sélectionnez **[!UICONTROL Enregistrer]**.

   ![Ajout de Adobe Experience Platform en tant que service de flux de données](assets/datastream-service-aep.png)
1. La configuration finale devrait ressembler à ceci.

   ![paramètres du flux de données](assets/datastream-settings.png)


>[!NOTE]
>
>L’activation de chacun des services utilisés par votre organisation garantit que les données collectées dans l’application mobile peuvent être utilisées partout. Pour plus d’informations sur les paramètres du flux de données, consultez la documentation [here](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/datastreams.html#adobe-experience-platform-settings).

Lors de l’implémentation du SDK Mobile Platform dans votre propre application, vous devez créer trois flux de données à mapper à vos trois environnements de balises (développement, évaluation et production). Si vous utilisez le SDK Platform Mobile avec des applications basées sur Platform telles qu’Adobe Real-time Customer Data Platform ou Adobe Journey Optimizer, vous devez veiller à créer ces flux de données dans les environnements de test Platform appropriés.

>[!SUCCESS]
>
>Vous devez maintenant utiliser un flux de données pour le reste du tutoriel.<br/>Merci d’investir votre temps à apprendre sur le SDK Adobe Experience Platform Mobile. Si vous avez des questions, souhaitez partager des commentaires généraux ou avez des suggestions sur le contenu futur, partagez-les à ce sujet. [Article de discussion de la communauté Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796)

Suivant : **[Configuration des balises](configure-tags.md)**
