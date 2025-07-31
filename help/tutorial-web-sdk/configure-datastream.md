---
title: Configurer un flux de données pour Platform Web SDK
description: Découvrez comment activer un flux de données et configurer des solutions Experience Cloud. Cette leçon fait partie du tutoriel Implémentation d’Adobe Experience Cloud avec le SDK web.
feature: Web SDK,Datastreams
jira: KT-15399
exl-id: 20f770d1-eb0f-41a9-b451-4069a0a91fc4
source-git-commit: 7ccbaaf4db43921f07c971c485e1460a1a7f0334
workflow-type: tm+mt
source-wordcount: '535'
ht-degree: 8%

---

# Configurer un trains de données

Découvrez comment configurer un flux de données pour le SDK web d’Adobe Experience Platform.

[Flux de données](https://experienceleague.adobe.com/fr/docs/experience-platform/datastreams/overview) indiquez à Adobe Experience Platform Edge Network où envoyer les données collectées par Platform Web SDK. Dans la configuration des flux de données, vous activez vos applications Experience Cloud, votre compte Experience Platform et le transfert d’événement.

![SDK web, flux de données et diagramme Edge Network](assets/dc-websdk-datastreams.png)

## Objectifs d’apprentissage

À la fin de cette leçon, vous saurez comment :

* Création dʼun flux de données
* Prise en main des remplacements de trains de données

## Conditions préalables

Avant de configurer votre flux de données, vous devez avoir déjà suivi les leçons suivantes :

* [Configuration d’un schéma](configure-schemas.md)
* [Configuration d’un espace de noms d’identité](configure-identities.md)

## Création dʼun flux de données

Vous pouvez désormais créer un flux de données pour indiquer à Platform Edge Network où envoyer les données collectées par Web SDK.

**Pour créer un flux de données, procédez comme suit**

1. Ouvrez l’interface [Collecte de données](https://experience.adobe.com/data-collection/){target="_blank"}
1. Vérifiez que vous vous trouvez dans le bon sandbox

   >[!NOTE]
   >
   >Si vous êtes client d’une application basée sur Platform telle que Real-Time CDP ou Journey Optimizer, nous vous recommandons d’utiliser un sandbox de développement pour ce tutoriel. Si ce n’est pas le cas, utilisez le sandbox **[!UICONTROL Prod]**.

1. Accédez à **[!UICONTROL Flux de données]** dans le volet de navigation de gauche
1. Sélectionnez **[!UICONTROL Nouveau flux de données]**
1. Saisissez `Luma Web SDK: Development Environment` comme **[!UICONTROL Nom]**. Ce nom est référencé ultérieurement lorsque vous configurez l’extension Web SDK dans votre propriété de balise.
1. Sélectionnez **[!UICONTROL Enregistrer]**

   ![Créer le flux de données](assets/datastream-create-new-datastream.png)

   >[!NOTE]
   >
   >Il n’est pas nécessaire de sélectionner un schéma. Une sélection de schéma n’est nécessaire que si vous utilisez la fonctionnalité [Préparation des données pour la collecte de données](/help/data-collection/edge/data-prep.md).

Sur l’écran suivant, vous pouvez ajouter des services tels que des applications Adobe au flux de données, mais vous ne pourrez pas ajouter de services à ce stade. Vous le ferez ultérieurement dans les leçons [Configuration d’Experience Platform](setup-experience-platform.md), [Configuration d’Analytics](setup-analytics.md), [Configuration d’Audience Manager](setup-audience-manager.md), [Configuration de Target](setup-target.md) ou [Transfert d’événement](setup-event-forwarding.md).

>[!NOTE]
>
>Lors de l’implémentation de Platform Web SDK sur votre propre site Web, vous devez créer trois flux de données à mapper à vos trois environnements de balises (développement, évaluation et production). Si vous utilisez Platform Web SDK avec des applications basées sur Platform telles qu’Adobe Real-Time Customer Data Platform ou Adobe Journey Optimizer, vous devez veiller à créer ces flux de données dans les sandbox Platform appropriés.

## Remplacer un flux de données

[Remplacements de train de données](https://experienceleague.adobe.com/en/docs/experience-platform/datastreams/overrides) vous permettent de définir des configurations supplémentaires pour votre train de données, puis de remplacer votre configuration par défaut sous certaines conditions.

Le remplacement de la configuration des trains de données est un processus en deux étapes :

1. Tout d’abord, vous définissez les remplacements de train de données dans la configuration du service de train de données. Par exemple, vous pouvez définir d’autres suites de rapports Analytics, des espaces de travail Target ou des jeux de données Platform à utiliser comme remplacements.
1. Ensuite, vous envoyez les remplacements à Edge Network avec une action d’événement d’envoi Web SDK ou par une configuration dans l’extension de balise Web SDK.

Dans la leçon [Configurer Adobe Analytics](setup-analytics.md), vous allez remplacer la suite de rapports d’une page à l’aide de l’action d’envoi d’événement Platform Web SDK.

Vous êtes maintenant prêt à installer l’extension Platform Web SDK dans votre propriété de balise.

>[!NOTE]
>
>Merci d’avoir investi votre temps dans votre apprentissage de Adobe Experience Platform Web SDK. Si vous avez des questions, souhaitez partager des commentaires généraux ou avez des suggestions sur le contenu futur, veuillez les partager dans ce [article de discussion de la communauté Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996)
