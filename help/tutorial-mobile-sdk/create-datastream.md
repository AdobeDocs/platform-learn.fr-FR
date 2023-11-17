---
title: Configurer un trains de données
description: Découvrez comment créer un flux de données dans Experience Platform.
feature: Mobile SDK,Datastreams
exl-id: 7b83f834-d1fb-45d1-8bcf-bc621f94725c
source-git-commit: bc53cb5926f708408a42aa98a1d364c5125cb36d
workflow-type: tm+mt
source-wordcount: '425'
ht-degree: 8%

---

# Création dʼun flux de données

Découvrez comment créer un flux de données dans Experience Platform.

>[!INFO]
>
> Ce tutoriel sera remplacé par un nouveau tutoriel utilisant un nouvel exemple d’application mobile à la fin novembre 2023.

Un flux de données est une configuration côté serveur sur Platform Edge Network.  Le flux de données garantit que les données entrantes vers Platform Edge Network sont acheminées vers les applications et services Adobe Experience Cloud de manière appropriée. Pour plus d’informations, voir [documentation](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/datastreams.html?lang=fr) ou ceci [video](https://experienceleague.adobe.com/docs/platform-learn/data-collection/edge-network/configure-datastreams.html?lang=fr).

## Conditions préalables

Pour créer un flux de données, votre organisation doit être configurée pour cette fonctionnalité dans l’interface de collecte de données (anciennement [!UICONTROL Launch]) et que vous devez disposer des autorisations utilisateur pour [!UICONTROL Experience Platform] > [!UICONTROL Collecte de données] > **[!UICONTROL Gestion des flux de données]** et **[!UICONTROL Affichage des flux de données]**.

## Objectifs d&#39;apprentissage

Dans cette leçon, vous allez :

* Savoir quand utiliser un flux de données.
* Création dʼun flux de données.
* Configurer un trains de données.

## Création dʼun flux de données

Les flux de données peuvent être créés dans la variable [!UICONTROL Collecte de données] à l’aide de la fonction [!UICONTROL Datastream] de configuration. Pour créer un flux de données :

1. Assurez-vous que vous vous trouvez dans le bon environnement de test Platform.
1. Sélectionnez **[!UICONTROL Nouveau flux de données]**.

   ![accueil des datastreams](assets/mobile-datastream-new.png)

1. Attribuez un nom, par exemple `Luma App`.
1. Sélectionnez le schéma que vous avez créé dans la leçon précédente.
1. Sélectionnez **[!UICONTROL Enregistrer]**.

   ![nouveaux flux de données](assets/mobile-datastream-name.png)


## Ajout de services

Vous pouvez ensuite connecter vos services Experience Cloud à votre flux de données. Lorsque le SDK Mobile Platform envoie des données à Edge Network, le flux de données envoie les données à ces services :

1. Ajouter **[!UICONTROL Adobe Analytics]** et fournissez une suite de rapports.

1. Activer **[!UICONTROL Adobe Audience Manager]** (facultatif).

1. Activer **[!UICONTROL Adobe Experience Platform]** et fournissez une **[!UICONTROL dataset]** (facultatif).
   * Si vous n’avez pas encore créé de jeu de données, suivez les instructions. [here](platform.md).

1. La configuration finale devrait ressembler à ceci.
   ![paramètres du flux de données](assets/mobile-datastream-settings.png)


>[!NOTE]
>
>L’activation de chacun des services utilisés par votre organisation garantit que les données collectées dans l’application mobile peuvent être utilisées partout. Pour plus d’informations sur les paramètres du flux de données, consultez la documentation [here](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/datastreams.html#adobe-experience-platform-settings).

Lors de l’implémentation du SDK Mobile Platform sur votre propre site web, vous devez créer trois flux de données à mapper à vos trois environnements de balises (développement, évaluation et production). Si vous utilisez le SDK Platform Mobile avec des applications basées sur Platform telles qu’Adobe Real-time Customer Data Platform ou Adobe Journey Optimizer, vous devez veiller à créer ces flux de données dans les environnements de test Platform appropriés.

Suivant : **[Configuration des balises](configure-tags.md)**

>[!NOTE]
>
>Merci d’investir votre temps à apprendre sur le SDK Adobe Experience Platform Mobile. Si vous avez des questions, souhaitez partager des commentaires généraux ou avez des suggestions sur le contenu futur, partagez-les à ce sujet. [Article de discussion de la communauté Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796)
