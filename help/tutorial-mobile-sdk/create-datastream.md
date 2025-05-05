---
title: Configuration d’un flux de données pour les implémentations du SDK Platform Mobile
description: Découvrez comment créer un train de données dans Experience Platform.
feature: Mobile SDK,Datastreams
jira: KT-14625
exl-id: 7b83f834-d1fb-45d1-8bcf-bc621f94725c
source-git-commit: 25f0df2ea09bb7383f45a698e75bd31be7541754
workflow-type: tm+mt
source-wordcount: '428'
ht-degree: 7%

---

# Création dʼun flux de données

Découvrez comment créer un train de données dans Experience Platform.

Un flux de données est une configuration côté serveur sur Platform Edge Network. Le flux de données garantit que les données entrantes vers l’Edge Network Platform sont acheminées vers les applications et services Adobe Experience Cloud de manière appropriée. Pour plus d’informations, voir la [documentation](https://experienceleague.adobe.com/docs/experience-platform/datastreams/overview.html?lang=fr) ou cette [vidéo](https://experienceleague.adobe.com/docs/platform-learn/data-collection/edge-network/configure-datastreams.html?lang=fr).

![Architecture](assets/architecture.png)

## Conditions préalables

Pour créer un flux de données, votre organisation doit être configurée pour cette fonctionnalité dans l’interface de collecte de données (anciennement [!UICONTROL Launch]) et vous devez disposer des autorisations utilisateur pour gérer et afficher les flux de données.

## Objectifs d&#39;apprentissage

Dans cette leçon, vous allez :

* Savoir quand utiliser un flux de données.
* Créez un flux de données.
* Configurez un flux de données.

## Création dʼun flux de données

Les flux de données peuvent être créés dans l’interface [!UICONTROL Collecte de données] à l’aide de l’outil de configuration [!UICONTROL Datastream]. Pour créer un flux de données :

1. Assurez-vous que vous vous trouvez dans l’environnement de test Experience Platform correct, car les flux de données sont définis au niveau de l’environnement de test.
1. Sélectionnez **[!UICONTROL Datastreams]** dans le rail de gauche.
1. Sélectionnez **[!UICONTROL New Datastream]**.

   ![datastreams home](assets/datastream-new.png)

1. Fournissez un **[!UICONTROL nom]**, par exemple `Luma Mobile App` et une **[!UICONTROL description]**, par exemple `Datastream for Luma Mobile App`.

   >[!NOTE]
   >
   >Rappel final : si vous passez en revue ce tutoriel avec plusieurs personnes sur un seul environnement de test ou que vous utilisez un compte partagé, envisagez d’ajouter ou de préparer une identification dans le cadre de vos conventions de dénomination. Par exemple, utilisez `Luma Mobile App Event Dataset - Joe Smith` au lieu de `Luma Mobile App Event Dataset`. Voir également la note dans [Overview](overview.md).

1. Sélectionnez le schéma que vous avez créé lors de la leçon précédente dans la liste **Event Schema**.
1. Sélectionnez **[!UICONTROL Enregistrer]**.

   ![new datastreams](assets/datastream-name.png)


## Ajout de services

Lorsque vous suivez les leçons (facultatives) [Analytics](analytics.md) et [Experience Platform](platform.md) de ce tutoriel, vous ajoutez des services à votre flux de données afin que les données envoyées à l’Edge Network Platform soient transférées vers ces applications.

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
>L’activation de chacun des services utilisés par votre organisation garantit que les données collectées dans l’application mobile peuvent être utilisées partout. Pour plus d’informations sur les paramètres de flux de données, consultez la documentation [ici](https://experienceleague.adobe.com/docs/experience-platform/datastreams/overview.html?lang=fr).

Lors de la mise en oeuvre du SDK Mobile Platform dans votre propre application, vous devez créer trois flux de données à mapper à vos trois environnements de balises (développement, évaluation et production). Si vous utilisez le SDK Platform Mobile avec des applications basées sur Platform telles qu’Adobe Real-Time Customer Data Platform ou Adobe Journey Optimizer, vous devez veiller à créer ces flux de données dans les environnements de test appropriés.

>[!SUCCESS]
>
>Vous devez maintenant utiliser un flux de données pour le reste du tutoriel.
>
>Merci d’investir votre temps à apprendre sur le SDK Adobe Experience Platform Mobile. Si vous avez des questions, souhaitez partager des commentaires généraux ou avez des suggestions sur le contenu à venir, partagez-les sur cet [post de discussion de la communauté Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796?profile.language=fr)

Suivant : **[Configuration d’une propriété de balise](configure-tags.md)**
