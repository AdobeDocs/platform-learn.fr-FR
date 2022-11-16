---
title: Création de stratégies de fusion
seo-title: Create merge policies | Getting Started with Adobe Experience Platform for Data Architects and Data Engineers
breadcrumb-title: Création de stratégies de fusion
description: Dans cette leçon, vous allez créer des stratégies de fusion afin de déterminer comment les données sont fusionnées en profils.
role: Data Architect, Data Engineer
feature: Profiles
kt: 4348
audience: data architect
doc-type: tutorial
activity: implement
thumbnail: 4348-create-merge-policies.jpg
exl-id: ec862bb2-7aa2-4157-94eb-f5af3a94295f
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '996'
ht-degree: 0%

---

# Création de stratégies de fusion

<!--20 min-->

Dans cette leçon, vous allez créer des stratégies de fusion afin de prioriser la manière dont plusieurs sources de données fusionnent en profils.

Adobe Experience Platform vous permet de rassembler des données provenant de plusieurs sources et de les combiner pour obtenir une vue complète de chaque client. Lorsque vous rassemblez ces données, les stratégies de fusion déterminent la priorité des données et les données combinées pour créer cette vue unifiée.

Nous allons nous en tenir à l’interface utilisateur pour cette leçon, mais des options d’API existent également pour créer des stratégies de fusion.

**Architectes de données** Vous devrez créer des stratégies de fusion en dehors de ce tutoriel.

Avant de commencer les exercices, regardez cette courte vidéo pour en savoir plus sur les stratégies de fusion :
>[!VIDEO](https://video.tv.adobe.com/v/330433?quality=12&learn=on)

## Autorisations requises

Dans le [Configuration des autorisations](configure-permissions.md) leçon, vous configurez tous les contrôles d’accès requis pour terminer cette leçon.

<!--* Permission items **[!UICONTROL Profile Management]** > **[!UICONTROL View Merge Policies]** and **[!UICONTROL Manage Merge Policies]**
* Permission item **[!UICONTROL Profile Management]** > **[!UICONTROL View Profiles]** and **[!UICONTROL Manage Profiles]**
* Permission item **[!UICONTROL Sandboxes]** > `Luma Tutorial`
* User-role access to the `Luma Tutorial Platform` product profile
-->

## À propos des stratégies de fusion et du schéma d’union

Vous vous souvenez peut-être que, dans la leçon sur l’ingestion par lots, nous avons chargé deux enregistrements avec des informations légèrement différentes pour le même client. Dans le [!DNL Loyalty] data, prénom du client `Daniel` et il vivait à `New York City`, mais dans les données CRM, le prénom du client était `Danny` et il vivait à `Portland`. Les données client changent au fil du temps. Peut-être qu&#39;il a déménagé `Portland` to `New York City`. D’autres éléments changent également, tels que les numéros de téléphone et les adresses électroniques. Les stratégies de fusion vous aident à décider comment gérer ces types de conflits lorsque deux sources de données donnent des informations différentes pour un même utilisateur.

Alors, pourquoi ? `Danny` win comme prénom ? Jetons un coup d&#39;oeil :

1. Dans l’interface utilisateur de Platform, sélectionnez **[!UICONTROL Profils]** dans le volet de navigation de gauche
1. Accédez au **[!UICONTROL Stratégies de fusion]** tab
1. La stratégie de fusion par défaut est horodatée. Puisque vous avez chargé les données CRM après les données de fidélité, `Danny` a été sélectionné comme prénom dans le profil :

![Écran Stratégie de fusion](assets/mergepolicies-default.png)

Lorsque plusieurs schémas sont activés pour le profil, une [!UICONTROL Schéma d’union] est automatiquement créé pour tous les schémas d’enregistrement activés pour les profils partageant une classe de base. Vous pouvez afficher la variable [!UICONTROL Schémas d’union] en accédant à la fonction **[!UICONTROL Schéma d’union]** .

![Écran Stratégie de fusion](assets/mergepolicies-unionSchema.png)

Notez qu’il n’existe pas de schéma d’union pour la classe ExperienceEvent. Bien que les données ExperienceEvent se trouvent toujours dans le profil, puisqu’elles sont basées sur des séries temporelles, chaque événement comprend un horodatage et les identifiants et les collisions ne posent pas problème.

Maintenant, que se passe-t-il si vous n’aimez pas cette stratégie de fusion par défaut ? Que se passe-t-il si Luma décide que son système de gestion de la relation client devrait être la source de vérité en cas de conflit ? Pour cela, nous allons créer une stratégie de fusion.

## Création d’une stratégie de fusion dans l’interface utilisateur

1. Dans l’écran Stratégies de fusion, sélectionnez la variable **[!UICONTROL Créer une stratégie de fusion]** dans le coin supérieur droit
1. Comme la variable **[!UICONTROL Nom]**, saisissez `Loyalty Prioritized`
1. Comme la variable **[!UICONTROL Schéma]**, sélectionnez **[!UICONTROL Profil XDM]** (notez que votre classe personnalisée, puisqu’il s’agit de données d’enregistrement, est également disponible pour les stratégies de fusion).
1. Pour **[!UICONTROL Assemblage D’Id]**, sélectionnez **[!UICONTROL Graphique privé]**
1. Pour **[!UICONTROL Fusion d’attributs]**, sélectionnez **[!UICONTROL Priorité du jeu de données]**
1. Glisser-déposer `Luma Loyalty Dataset` et `Luma CRM Dataset` au **[!UICONTROL Jeu de données]** du panneau.
1. Assurez-vous de `Luma Loyalty Dataset` est en haut en le faisant glisser au-dessus de la balise `Luma CRM Dataset`
1. Sélectionnez la **[!UICONTROL Enregistrer]** button
<!--do i need to explain Private Graph? Is that GA?-->
![Stratégie de fusion](assets/mergepolicies-newPolicy.png)

## Validation de la stratégie de fusion

Voyons si la stratégie de fusion fait ce à quoi nous nous attendons :

1. Accédez au **[!UICONTROL Parcourir]** tab
1. Modifiez la variable **[!UICONTROL Stratégie de fusion]** à votre nouvelle `Loyalty Prioritized` policy
1. Comme la variable **[!UICONTROL Espace de noms d’identité]**, utilisez `Luma CRM Id`
1. Comme la variable **[!UICONTROL Valeur d’identité]** use `112ca06ed53d3db37e4cea49cc45b71e`
1. Sélectionnez la **[!UICONTROL Afficher le profil]** button
1. `Daniel` est de retour !

![Affichage d’un profil avec une stratégie de fusion différente](assets/mergepolicies-lookupProfileWithMergePolicy.png)

## Création d’une stratégie de fusion avec des jeux de données limités

Lors de la création de stratégies de fusion utilisant la priorité du jeu de données, seuls les jeux de données de la même classe de base que celle que vous incluez à droite sont inclus dans le profil. Configuration d’une autre stratégie de fusion

1. Dans l’écran Stratégies de fusion, sélectionnez la variable **[!UICONTROL Créer une stratégie de fusion]** dans le coin supérieur droit
1. Comme la variable **[!UICONTROL Nom]**, saisissez  `Loyalty Only`
1. Comme la variable **[!UICONTROL Schéma]**, sélectionnez **[!UICONTROL Profil XDM]**
1. Pour **[!UICONTROL Assemblage D’Id]**, sélectionnez **[!UICONTROL Aucun]**
1. Pour **[!UICONTROL Fusion d’attributs]**, sélectionnez **[!UICONTROL Priorité du jeu de données]**
1. Faites glisser et déposez uniquement le `Luma Loyalty Dataset` to **[!UICONTROL Jeu de données sélectionné]** du panneau.
1. Sélectionnez la **[!UICONTROL Enregistrer]** button

![Stratégie de fusion Loyalty Only](assets/mergepolicies-loyaltyOnly.png)

## Validation de la stratégie de fusion

Examinons maintenant ce que cette stratégie de fusion fait :

1. Accédez au **[!UICONTROL Parcourir]** tab
1. Modifiez la variable **[!UICONTROL Stratégie de fusion]** à votre nouvelle `Loyalty Only` policy
1. Comme la variable **[!UICONTROL Espace de noms d’identité]**, utilisez `Luma CRM Id`
1. Comme la variable **[!UICONTROL Valeur d’identité]** use `112ca06ed53d3db37e4cea49cc45b71e`
1. Sélectionnez la **[!UICONTROL Afficher le profil]** button
1. Vérifiez qu’aucun profil n’est trouvé :
   ![Fidélité Uniquement aucune recherche d’identifiant CRM.](assets/mergepolicies-loyaltyOnly-noCrmLookup.png)

L’identifiant CRM est un champ d’identité dans la variable `Luma Loyalty Dataset`, mais seules les identités Principales peuvent être utilisées pour rechercher des profils. Donc, recherchons le profil à l&#39;aide de la Principale identité, `Luma Loyalty Id`&quot;

1. Modifiez la variable **[!UICONTROL Espace de noms d’identité]** to `Luma Loyalty Id`
1. Comme la variable **[!UICONTROL Valeur d’identité]** use `5625458`
1. Sélectionnez la **[!UICONTROL Afficher le profil]** button
1. Sélectionner l’identifiant du profil pour ouvrir le profil
1. Accédez au **[!UICONTROL Attributs]** tab
1. Notez que d’autres détails de profil du jeu de données CRM, tels que le numéro de téléphone mobile et l’adresse électronique, ne sont pas disponibles, car nous ne faisons que
   ![Les données de gestion de la relation client ne sont pas visibles dans la stratégie de fidélité uniquement](assets/mergepolicies-loyaltyOnly-attributes.png)
1. Accédez au **[!UICONTROL Événements]** tab
1. Les données ExperienceEvent sont disponibles même si elles ne sont pas explicitement incluses dans les jeux de données de stratégie de fusion :
   ![Les événements sont visibles dans la stratégie de fidélité uniquement](assets/mergepolicies-loyaltyOnly-events.png)

## En savoir plus sur les stratégies de fusion

Dans la recherche de profil, modifiez la stratégie de fusion utilisée en `Default Timebased` et sélectionnez la variable **[!UICONTROL Afficher le profil]** bouton . Danny est de retour !

![Affichage d’un profil avec une stratégie de fusion différente](assets/mergepolicies-backToDanny.png)

Que se passe-t-il ici ? Eh bien, la fusion des profils n&#39;est pas une chose unique. Les profils client en temps réel sont assemblés à la volée, en fonction de divers facteurs, y compris la stratégie de fusion utilisée. Vous pouvez créer plusieurs stratégies de fusion à utiliser dans différents contextes, selon la vue du client que vous souhaitez.

La gouvernance des données est un cas d’utilisation clé des stratégies de fusion. Par exemple, supposons que vous ingériez des données tierces dans Platform qui ne peuvent pas être utilisées pour des cas d’utilisation de personnalisation, mais _can_ à utiliser pour des cas d’utilisation publicitaire ; Vous pouvez créer une stratégie de fusion qui exclut ce jeu de données tiers et utiliser cette stratégie de fusion pour créer des segments pour vos cas d’utilisation publicitaire.

## Ressources supplémentaires

* [Documentation sur les stratégies de fusion](https://experienceleague.adobe.com/docs/experience-platform/profile/merge-policies/overview.html)
* [Référence de l’API Stratégies de fusion (partie intégrante de l’API Real-time Customer Profile)](https://www.adobe.io/experience-platform-apis/references/profile/#tag/Merge-policies)

Passons maintenant au [cadre de gouvernance des données](apply-data-governance-framework.md).
