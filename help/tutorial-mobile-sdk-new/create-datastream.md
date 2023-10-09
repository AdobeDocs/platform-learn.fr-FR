---
title: Configurer un trains de données
description: Découvrez comment créer un flux de données dans Experience Platform.
feature: Mobile SDK,Datastreams
hide: true
exl-id: d8b9df3d-49ee-4578-92c6-0f920a86fe7e
source-git-commit: d7410a19e142d233a6c6597de92f112b961f5ad6
workflow-type: tm+mt
source-wordcount: '459'
ht-degree: 8%

---

# Création dʼun flux de données

Découvrez comment créer un flux de données dans Experience Platform.

Un flux de données est une configuration côté serveur sur Platform Edge Network. Le flux de données garantit que les données entrantes vers Platform Edge Network sont acheminées vers les applications et services Adobe Experience Cloud de manière appropriée. Pour plus d’informations, voir [documentation](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/datastreams.html?lang=fr) ou ceci [video](https://experienceleague.adobe.com/docs/platform-learn/data-collection/edge-network/configure-datastreams.html?lang=fr).

![Architecture](assets/architecture.png)

## Conditions préalables

Pour créer un flux de données, votre organisation doit être configurée pour cette fonctionnalité dans l’interface de collecte de données (anciennement [!UICONTROL Launch]) et vous devez disposer des autorisations utilisateur pour gérer et afficher les flux de données.

## Objectifs d&#39;apprentissage

Dans cette leçon, vous allez :

* Savoir quand utiliser un flux de données.
* Création dʼun flux de données.
* Configurer un trains de données.

## Création dʼun flux de données

Les flux de données peuvent être créés dans la variable [!UICONTROL Collecte de données] à l’aide de la fonction [!UICONTROL Datastream] de configuration. Pour créer un flux de données :

1. Assurez-vous que vous vous trouvez dans l’environnement de test Experience Platform correct, car les flux de données sont définis au niveau de l’environnement de test.
1. Sélectionner **[!UICONTROL Datastreams]** dans le rail de gauche.
1. Sélectionnez **[!UICONTROL Nouveau flux de données]**.

   ![accueil des datastreams](assets/datastream-new.png)

1. Fournissez une **[!UICONTROL Nom]**, par exemple `Luma Mobile App` et un **[!UICONTROL Description]**, par exemple `Datastream for Luma Mobile App`.

   >[!NOTE]
   >
   >Rappel final : si vous passez en revue ce tutoriel avec plusieurs personnes sur un seul environnement de test ou que vous utilisez un compte partagé, envisagez d’ajouter ou de préparer une identification dans le cadre de vos conventions de dénomination. Par exemple, utilisez `Luma Mobile App Event Dataset` plutôt que `Luma Mobile App Event Dataset - Joe Smith`. Voir également la remarque dans la section [Présentation](overview.md).

1. Sélectionnez le schéma que vous avez créé dans la leçon précédente à partir du **Schéma d’événement** liste.
1. Sélectionnez **[!UICONTROL Enregistrer]**.

   ![nouveaux flux de données](assets/datastream-name.png)


## Ajout de services

Lorsque vous exécutez le (facultatif) [Analytics](analytics.md) et [Experience Platform](platform.md) leçons de ce tutoriel, vous ajoutez des services à votre flux de données pour vous assurer que lorsque le SDK Mobile Platform envoie des données au réseau Edge, le flux de données les transfère vers les services configurés.

<!--

### Adobe Analytics

1. Select **[!UICONTROL Add Service]**.

1. Add **[!UICONTROL Adobe Analytics]** from the [!UICONTROL Service] list, 

1. Enter the name of the report site that you want to use in **[!UICONTROL Report Suite ID]**.

1. Enable the service by switching **[!UICONTROL Enabled]** on.

1. Select **[!UICONTROL Save]**.

   ![Add Adobe Analytics as datastream service](assets/datastream-service-aa.png)


### Adobe Experience Platform

You might also want to enable the Adobe Experience Platform service. 

>[!IMPORTANT]
>
>You can only enable the Adobe Experience Platform service when having created an event dataset. If you don't already have an event dataset created, follow the instructions [here](platform.md).

1. Click ![Add](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) **[!UICONTROL Add Service]** to add another service.

1. Select **[!UICONTROL Adobe Experience Platform]** from the [!UICONTROL Service] list.

1. Enable the service by switching **[!UICONTROL Enabled]** on.

1. Select the **[!UICONTROL Event Dataset]** that you created as part of the [Create a dataset](platform.md#create-a-dataset) instructions, for example **Luma Mobile App Event Dataset**

1. Select **[!UICONTROL Save]**.

   ![Add Adobe Experience Platform as a datastream service](assets/datastream-service-aep.png)
1. The final configuration should look something like this.
   
   ![datastream settings](assets/datastream-settings.png)

-->


>[!NOTE]
>
>L’activation de chacun des services utilisés par votre organisation garantit que les données collectées dans l’application mobile peuvent être utilisées partout. Pour plus d’informations sur les paramètres du flux de données, consultez la documentation [here](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/datastreams.html#adobe-experience-platform-settings).

Lors de la mise en oeuvre du SDK Mobile Platform dans votre propre application, vous devez créer trois flux de données à mapper à vos trois environnements de balises (développement, évaluation et production). Si vous utilisez le SDK Platform Mobile avec des applications basées sur Platform telles qu’Adobe Real-time Customer Data Platform ou Adobe Journey Optimizer, vous devez veiller à créer ces flux de données dans les environnements de test appropriés.

>[!SUCCESS]
>
>Vous devez maintenant utiliser un flux de données pour le reste du tutoriel.<br/>Merci d’investir votre temps à apprendre sur le SDK Adobe Experience Platform Mobile. Si vous avez des questions, souhaitez partager des commentaires généraux ou avez des suggestions sur le contenu futur, partagez-les à ce sujet. [Article de discussion de la communauté Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796)

Suivant : **[Configuration d’une propriété de balise](configure-tags.md)**
