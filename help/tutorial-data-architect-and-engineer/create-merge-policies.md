---
title: Création de stratégies de fusion
seo-title: Create merge policies | Getting Started with Adobe Experience Platform for Data Architects and Data Engineers
breadcrumb-title: Création de stratégies de fusion
description: Dans cette leçon, vous allez créer des stratégies de fusion afin de déterminer comment les données sont fusionnées en profils.
role: Data Architect, Data Engineer
feature: Profiles
jira: KT-4348
audience: data architect
doc-type: tutorial
activity: implement
thumbnail: 4348-create-merge-policies.jpg
exl-id: ec862bb2-7aa2-4157-94eb-f5af3a94295f
source-git-commit: 915502e54365eedb09b12a92aa3b1af71f6de1f4
workflow-type: tm+mt
source-wordcount: '984'
ht-degree: 0%

---

# Création de stratégies de fusion

<!--20 min-->

Dans cette leçon, vous allez créer des stratégies de fusion afin de prioriser la manière dont plusieurs sources de données fusionnent en profils.

Adobe Experience Platform vous permet de rassembler des données provenant de plusieurs sources et de les combiner pour obtenir une vue complète de chaque client. Lorsque vous rassemblez ces données, les stratégies de fusion déterminent la priorité des données et les données combinées pour créer cette vue unifiée.

Nous allons nous en tenir à l’interface utilisateur pour cette leçon, mais des options d’API existent également pour créer des stratégies de fusion.

**Les architectes de données** devront créer des stratégies de fusion en dehors de ce tutoriel.

Avant de commencer les exercices, regardez cette courte vidéo pour en savoir plus sur les stratégies de fusion :
>[!VIDEO](https://video.tv.adobe.com/v/330433?learn=on)

## Autorisations requises

Dans la leçon [Configurer les autorisations](configure-permissions.md) , vous configurez tous les contrôles d’accès requis pour terminer cette leçon.

<!--* Permission items **[!UICONTROL Profile Management]** > **[!UICONTROL View Merge Policies]** and **[!UICONTROL Manage Merge Policies]**
* Permission item **[!UICONTROL Profile Management]** > **[!UICONTROL View Profiles]** and **[!UICONTROL Manage Profiles]**
* Permission item **[!UICONTROL Sandboxes]** > `Luma Tutorial`
* User-role access to the `Luma Tutorial Platform` product profile
-->

## À propos des stratégies de fusion et du schéma d’union

Vous vous souvenez peut-être que, dans la leçon sur l’ingestion par lots, nous avons chargé deux enregistrements avec des informations légèrement différentes pour le même client. Dans les données [!DNL Loyalty], le prénom du client était `Daniel` et il vivait dans `New York City`, mais dans les données CRM, le prénom du client était `Danny` et il vivait dans `Portland`. Les données client changent au fil du temps. Peut-être est-il passé de `Portland` à `New York City`. D’autres éléments changent également, tels que les numéros de téléphone et les adresses électroniques. Les stratégies de fusion vous aident à décider comment gérer ces types de conflits lorsque deux sources de données donnent des informations différentes pour un même utilisateur.

Alors, pourquoi `Danny` a-t-il gagné comme prénom ? Jetons un coup d&#39;oeil :

1. Dans l’interface utilisateur de Platform, sélectionnez **[!UICONTROL Profils]** dans le volet de navigation de gauche.
1. Accédez à l’onglet **[!UICONTROL Stratégies de fusion]**
1. La stratégie de fusion par défaut est horodatée. Puisque vous avez chargé les données CRM après les données de fidélité, `Danny` a obtenu le prénom dans le profil :

![Écran Stratégie de fusion](assets/mergepolicies-default.png)

Lorsque plusieurs schémas sont activés pour le profil, un [!UICONTROL schéma d’union] est automatiquement créé pour tous les schémas activés pour le profil et qui enregistrent le partage d’une classe de base. Vous pouvez afficher les [!UICONTROL schémas d’union] en accédant à l’onglet **[!UICONTROL Schéma d’union]**.

![Écran Stratégie de fusion](assets/mergepolicies-unionSchema.png)

Notez qu’il n’existe pas de schéma d’union pour la classe ExperienceEvent. Bien que les données ExperienceEvent se trouvent toujours dans le profil, puisqu’elles sont basées sur des séries temporelles, chaque événement comprend un horodatage et les identifiants et les collisions ne posent pas problème.

Maintenant, que se passe-t-il si vous n’aimez pas cette stratégie de fusion par défaut ? Et si Luma décide que leur système de fidélité devrait être la source de vérité en cas de conflit ? Pour ce faire, nous allons créer une stratégie de fusion.

## Créer une stratégie de fusion dans l’interface utilisateur

1. Dans l’écran Stratégies de fusion, cliquez sur le bouton **[!UICONTROL Créer une stratégie de fusion]** en haut à droite.
1. En tant que **[!UICONTROL Name]**, saisissez `Loyalty Prioritized`
1. En tant que **[!UICONTROL schéma]**, sélectionnez **[!UICONTROL Profil XDM]** (notez que votre classe personnalisée, puisqu’il s’agit de données d’enregistrement, est également disponible pour les stratégies de fusion).
1. Pour **[!UICONTROL Id Stitching]**, sélectionnez **[!UICONTROL Private Graph]**
1. Pour **[!UICONTROL Fusion d’attributs]**, sélectionnez **[!UICONTROL Priorité du jeu de données]**
1. Faites glisser `Luma Loyalty Dataset` et `Luma CRM Dataset` vers le panneau **[!UICONTROL Jeu de données]**.
1. Assurez-vous que `Luma Loyalty Dataset` se trouve en haut en le faisant glisser au-dessus de `Luma CRM Dataset`
1. Sélectionnez le bouton **[!UICONTROL Enregistrer]**
   <!--do i need to explain Private Graph? Is that GA?-->
   ![Stratégie de fusion](assets/mergepolicies-newPolicy.png)

## Validation de la stratégie de fusion

Voyons si la stratégie de fusion fait ce à quoi nous nous attendons :

1. Accédez à l’onglet **[!UICONTROL Parcourir]**
1. Remplacez la **[!UICONTROL stratégie de fusion]** par la nouvelle `Loyalty Prioritized` stratégie
1. En tant que **[!UICONTROL espace de noms d’identité]**, utilisez votre `Luma CRM Id`
1. En tant que **[!UICONTROL valeur d’identité]**, utilisez `112ca06ed53d3db37e4cea49cc45b71e`
1. Sélectionnez le bouton **[!UICONTROL Afficher le profil]**
1. `Daniel` est de retour !

![Affichage d’un profil avec une stratégie de fusion différente](assets/mergepolicies-lookupProfileWithMergePolicy.png)

## Création d’une stratégie de fusion avec des jeux de données limités

Lors de la création de stratégies de fusion utilisant la priorité du jeu de données, seuls les jeux de données de la même classe de base que celle que vous incluez à droite sont inclus dans le profil. Configuration d’une autre stratégie de fusion

1. Dans l’écran Stratégies de fusion, cliquez sur le bouton **[!UICONTROL Créer une stratégie de fusion]** en haut à droite.
1. En tant que **[!UICONTROL Name]**, saisissez `Loyalty Only`
1. En tant que **[!UICONTROL schéma]**, sélectionnez **[!UICONTROL Profil XDM]**
1. Pour **[!UICONTROL Assemblage d’identités]**, sélectionnez **[!UICONTROL Aucun]**
1. Pour **[!UICONTROL Fusion d’attributs]**, sélectionnez **[!UICONTROL Priorité du jeu de données]**
1. Faites glisser uniquement le panneau `Luma Loyalty Dataset` vers le **[!UICONTROL jeu de données sélectionné]**.
1. Sélectionnez le bouton **[!UICONTROL Enregistrer]**

![ {Loyalty Only Merge Policy](assets/mergepolicies-loyaltyOnly.png)

## Validation de la stratégie de fusion

Examinons maintenant ce que cette stratégie de fusion fait :

1. Accédez à l’onglet **[!UICONTROL Parcourir]**
1. Remplacez la **[!UICONTROL stratégie de fusion]** par la nouvelle `Loyalty Only` stratégie
1. En tant que **[!UICONTROL espace de noms d’identité]**, utilisez votre `Luma CRM Id`
1. En tant que **[!UICONTROL valeur d’identité]**, utilisez `112ca06ed53d3db37e4cea49cc45b71e`
1. Sélectionnez le bouton **[!UICONTROL Afficher le profil]**
1. Vérifiez qu’aucun profil n’est trouvé :
   ![Loyalty Uniquement aucune recherche d’identifiant CRM.](assets/mergepolicies-loyaltyOnly-noCrmLookup.png)

L’identifiant CRM est un champ d’identité dans `Luma Loyalty Dataset`, mais seules les identités primaires peuvent être utilisées pour rechercher des profils. Donc, recherchons le profil à l&#39;aide de l&#39;identité principale, `Luma Loyalty Id`&quot;

1. Remplacez **[!UICONTROL Identity Namespace]** par `Luma Loyalty Id`
1. En tant que **[!UICONTROL valeur d’identité]**, utilisez `5625458`
1. Sélectionnez le bouton **[!UICONTROL Afficher le profil]**
1. Sélectionner l’identifiant du profil pour ouvrir le profil
1. Accédez à l’onglet **[!UICONTROL Attributs]**
1. Notez que d’autres détails de profil du jeu de données CRM, tels que le numéro de téléphone mobile et l’adresse électronique, ne sont pas disponibles, car nous ne faisons que
   ![Les données CRM ne sont pas visibles dans la stratégie Loyalty Only](assets/mergepolicies-loyaltyOnly-attributes.png)
1. Accédez à l’onglet **[!UICONTROL Events]**
1. Les données ExperienceEvent sont disponibles même si elles ne sont pas explicitement incluses dans les jeux de données de stratégie de fusion :
   ![Les événements sont visibles dans la stratégie Loyalty Only](assets/mergepolicies-loyaltyOnly-events.png)

## En savoir plus sur les stratégies de fusion

Dans la recherche de profil, modifiez la stratégie de fusion utilisée en `Default Timebased` et sélectionnez le bouton **[!UICONTROL Afficher le profil]** . Danny est de retour !

![Affichage d’un profil avec une stratégie de fusion différente](assets/mergepolicies-backToDanny.png)

Que se passe-t-il ici ? Eh bien, la fusion des profils n&#39;est pas une chose unique. Les profils client en temps réel sont assemblés à la volée, en fonction de divers facteurs, y compris la stratégie de fusion utilisée. Vous pouvez créer plusieurs stratégies de fusion à utiliser dans différents contextes, selon la vue du client que vous souhaitez.

La gouvernance des données est un cas d’utilisation clé des stratégies de fusion. Par exemple, supposons que vous ingériez des données tierces dans Platform qui ne peuvent pas être utilisées pour des cas d’utilisation de personnalisation, mais _peut_ être utilisé pour des cas d’utilisation publicitaire. Vous pouvez créer une stratégie de fusion qui exclut ce jeu de données tiers et utiliser cette stratégie de fusion pour créer des segments pour vos cas d’utilisation publicitaire.

## Ressources supplémentaires

* [Documentation sur les stratégies de fusion](https://experienceleague.adobe.com/docs/experience-platform/profile/merge-policies/overview.html)
* [Référence de l’API Stratégies de fusion (partie intégrante de l’API Real-time Customer Profile)](https://www.adobe.io/experience-platform-apis/references/profile/#tag/Merge-policies)

Passons maintenant à la [structure de gouvernance des données](apply-data-governance-framework.md).
