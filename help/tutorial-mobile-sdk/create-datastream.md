---
title: Configurer un flux de données pour les implémentations de Platform Mobile SDK
description: Découvrez comment créer un train de données dans Experience Platform.
feature: Mobile SDK,Datastreams
jira: KT-14625
exl-id: 7b83f834-d1fb-45d1-8bcf-bc621f94725c
source-git-commit: 008d3ee066861ea9101fe9fe99ccd0a088b63f23
workflow-type: tm+mt
source-wordcount: '425'
ht-degree: 7%

---

# Création dʼun flux de données

Découvrez comment créer un train de données dans Experience Platform.

Un flux de données est une configuration côté serveur sur Platform Edge Network. Le flux de données garantit que les données entrantes vers Platform Edge Network sont acheminées correctement vers les applications et services Adobe Experience Cloud. Pour plus d’informations, consultez la [documentation](https://experienceleague.adobe.com/fr/docs/experience-platform/datastreams/overview) ou cette [vidéo](https://experienceleague.adobe.com/fr/docs/platform-learn/data-collection/edge-network/configure-datastreams).

![Architecture](assets/architecture.png){zoomable="yes"}

## Conditions préalables

Pour créer un flux de données, votre organisation doit être configurée pour cette fonctionnalité dans l’interface de collecte de données (anciennement [!UICONTROL Launch]) et vous devez disposer des autorisations utilisateur pour gérer et afficher les flux de données.

## Objectifs d’apprentissage

Dans cette leçon, vous allez :

* Savoir quand utiliser un flux de données.
* Créez un flux de données.
* Configurez un flux de données.

## Création dʼun flux de données

Les flux de données peuvent être créés dans l’interface [!UICONTROL Collecte de données] à l’aide de l’outil de configuration [!UICONTROL Flux de données]. Pour créer un flux de données :

1. Assurez-vous que vous vous trouvez dans le bon sandbox Experience Platform, car les flux de données sont définis au niveau du sandbox.
1. Sélectionnez **[!UICONTROL Flux de données]** dans le rail de gauche.
1. Sélectionnez **[!UICONTROL Nouveau flux de données]**.

   ![page de départ flux de données](assets/datastream-new.png){zoomable="yes"}

1. Fournissez un **[!UICONTROL Nom]** par exemple `Luma Mobile App` et un **[!UICONTROL Description]** par exemple `Datastream for Luma Mobile App`.

   >[!NOTE]
   >
   >Dernier rappel : si vous suivez ce tutoriel avec plusieurs personnes sur un seul sandbox ou que vous utilisez un compte partagé, pensez à ajouter ou à ajouter une identification comme partie intégrante de vos conventions de nommage. Par exemple, au lieu de `Luma Mobile App Event Dataset`, utilisez `Luma Mobile App Event Dataset - Joe Smith`. Consultez également la remarque dans [Présentation](overview.md).

1. Sélectionnez le schéma que vous avez créé dans la leçon précédente dans la liste **Schéma d’événement**.
1. Sélectionnez **[!UICONTROL Enregistrer]**.

   ![nouveaux flux de données](assets/datastream-name.png){zoomable="yes"}


## Ajouter des services

Lorsque vous parcourez les leçons [Analytics](analytics.md) et [Experience Platform](platform.md) (facultatives) de ce tutoriel, vous ajoutez des services à votre flux de données afin que les données envoyées à Platform Edge Network soient transférées vers ces applications.

<!--

### Adobe Analytics

1. Select **[!UICONTROL Add Service]**.

1. Add **[!UICONTROL Adobe Analytics]** from the [!UICONTROL Service] list, 

1. Enter the name of the report site that you want to use in **[!UICONTROL Report Suite ID]**.

1. Enable the service by switching **[!UICONTROL Enabled]** on.

1. Select **[!UICONTROL Save]**.

   ![Add Adobe Analytics as datastream service](assets/datastream-service-aa.png){zoomable="yes"}


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

   ![Add Adobe Experience Platform as a datastream service](assets/datastream-service-aep.png){zoomable="yes"}
1. The final configuration should look something like this.
   
   ![datastream settings](assets/datastream-settings.png){zoomable="yes"}

-->


>[!NOTE]
>
>L’activation de chacun des services utilisés par votre organisation garantit que les données collectées dans l’application mobile peuvent être utilisées partout. Pour plus d’informations[ voir ](https://experienceleague.adobe.com/fr/docs/experience-platform/datastreams/overview) Paramètres de flux de données .

Lors de l’implémentation de Platform Mobile SDK dans votre propre application, vous devez créer trois flux de données à mapper à vos trois environnements de balises (développement, évaluation et production). Si vous utilisez Platform Mobile SDK avec des applications basées sur Platform, telles qu’Adobe Real-Time Customer Data Platform ou Adobe Journey Optimizer, vous devez veiller à créer ces flux de données dans les sandbox appropriés.

>[!SUCCESS]
>
>Vous disposez désormais d’un flux de données à utiliser pour la suite du tutoriel.
>
>Merci d’avoir consacré votre temps à découvrir Adobe Experience Platform Mobile SDK. Si vous avez des questions, souhaitez partager des commentaires généraux ou des suggestions sur le contenu futur, partagez-les dans ce [article de discussion de la communauté Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796?profile.language=fr)

Suivant : **[Configurer une propriété de balise](configure-tags.md)**
