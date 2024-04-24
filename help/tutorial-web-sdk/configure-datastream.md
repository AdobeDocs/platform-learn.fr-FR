---
title: Configurer un trains de données
description: Découvrez comment activer un flux de données et configurer des solutions Experience Cloud. Cette leçon fait partie du tutoriel Mise en oeuvre de Adobe Experience Cloud avec le SDK Web .
feature: Web SDK,Datastreams
exl-id: 20f770d1-eb0f-41a9-b451-4069a0a91fc4
source-git-commit: d81e7df36807778967bc0350735aec008fb1a55e
workflow-type: tm+mt
source-wordcount: '547'
ht-degree: 5%

---

# Configurer un trains de données

Découvrez comment activer un flux de données et configurer des applications Experience Cloud.

Les flux de données indiquent à Adobe Experience Platform Edge Network où envoyer les données collectées par le SDK Web Platform. Dans la configuration des flux de données, vous activez les applications Experience Cloud, votre compte Experience Platform et le transfert des événements. Voir [Principes de base de la configuration d’un flux de données](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/datastreams.html?lang=fr) pour plus d’informations.


![SDK Web, flux de données et diagramme Edge Network](assets/dc-websdk-datastreams.png)

## Objectifs d&#39;apprentissage

À la fin de cette leçon, vous saurez comment :

* Création dʼun flux de données
* Prise en main des remplacements de flux de données

## Conditions préalables

Avant de configurer votre flux de données, vous devez avoir terminé les leçons suivantes :

* [Configuration d’un schéma](configure-schemas.md)
* [Configuration d’un espace de noms d’identité](configure-identities.md)

## Création dʼun flux de données

Vous pouvez maintenant créer un flux de données pour indiquer à Platform Edge Network où envoyer les données collectées par le SDK Web.

**Pour créer un flux de données :**

1. Ouvrez le [Interface de collecte de données](https://launch.adobe.com/){target="_blank"}
1. Assurez-vous que vous vous trouvez dans le bon environnement de test.

   >[!NOTE]
   >
   >Si vous êtes client d’une application basée sur Platform telle que Real-Time CDP ou Journey Optimizer, nous vous recommandons d’utiliser un environnement de test de développement pour ce tutoriel. Si ce n’est pas le cas, utilisez le **[!UICONTROL Prod]** sandbox.

1. Accédez à **[!UICONTROL Datastreams]** dans la navigation de gauche
1. Sélectionner **[!UICONTROL Nouvelle structure de données]** sur le côté droit de l’écran.
1. Entrée `Luma Web SDK: Development Environment` comme la propriété **[!UICONTROL Nom]**. Ce nom est référencé ultérieurement lorsque vous configurez l’extension SDK Web dans la propriété de balise.
1. Sélectionnez votre `Luma Web Event Data` comme la propriété **[!UICONTROL Schéma d’événement]**
1. Sélectionnez **[!UICONTROL Enregistrer]**.

   ![Création du flux de données](assets/datastream-create-new-datastream.png)

Sur l’écran suivant, vous pouvez ajouter des services tels que des applications d’Adobe à la banque de données, mais vous n’ajouterez aucun service à ce stade du tutoriel. Vous le ferez plus tard dans les leçons. [Configuration d’un Experience Platform](setup-experience-platform.md), [Configuration d’Analytics](setup-analytics.md), [Configuration de l’Audience Manager](setup-audience-manager.md), [Configuration de Target](setup-target.md), ou [Transfert d’événement](setup-event-forwarding.md).

>[!NOTE]
>
>Lors de l’implémentation du SDK Web Platform sur votre propre site web, vous devez créer trois flux de données à mapper à vos trois environnements de balises (développement, évaluation et production). Si vous utilisez le SDK Web Platform avec des applications basées sur Platform telles qu’Adobe Real-time Customer Data Platform ou Adobe Journey Optimizer, vous devez veiller à créer ces flux de données dans les environnements de test Platform appropriés.

## Remplacement d’un flux de données

Les remplacements de flux de données vous permettent de définir des configurations supplémentaires pour vos flux de données, puis de remplacer votre configuration par défaut sous certaines conditions de votre mise en oeuvre.


Le remplacement de la configuration du flux de données est un processus en deux étapes :

1. Tout d’abord, vous définissez vos remplacements de flux de données dans la configuration de flux de données. Cette opération doit être effectuée par application par Adobe que vous souhaitez remplacer.
1. Ensuite, vous envoyez les remplacements à l’Edge Network soit par une action Envoyer l’événement au SDK Web, soit par une configuration dans l’extension de balise du SDK Web.

Dans le [Configuration d’Adobe Analytics](setup-analytics.md) leçon Vous remplacez la suite de rapports pour une page à l’aide de l’action Envoyer l’événement du SDK Web Platform.

Voir [la configuration du flux de données remplace la documentation](https://experienceleague.adobe.com/docs/experience-platform/datastreams/overrides.html?lang=en) pour obtenir des instructions détaillées sur la façon de remplacer les configurations datastream.

Vous êtes maintenant prêt à installer l’extension SDK Web Platform dans votre propriété de balise !

[Suivant : ](install-web-sdk.md)

>[!NOTE]
>
>Merci d’avoir consacré du temps à l’apprentissage du SDK Web Adobe Experience Platform. Si vous avez des questions, souhaitez partager des commentaires généraux ou avez des suggestions sur le contenu futur, partagez-les à ce sujet. [Article de discussion de la communauté Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996)
