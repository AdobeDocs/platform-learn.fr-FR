---
title: Création de politiques de fusion
seo-title: Create merge policies | Getting Started with Adobe Experience Platform for Data Architects and Data Engineers
breadcrumb-title: Création de politiques de fusion
description: Dans cette leçon, vous allez créer des politiques de fusion pour déterminer comment les données fusionnent en profils.
role: Data Architect, Data Engineer
feature: Profiles
jira: KT-4348
audience: data architect
doc-type: tutorial
activity: implement
thumbnail: 4348-create-merge-policies.jpg
exl-id: ec862bb2-7aa2-4157-94eb-f5af3a94295f
source-git-commit: 48a38fd96ea9072d207173a1b51153c6498090e0
workflow-type: tm+mt
source-wordcount: '991'
ht-degree: 0%

---

# Création de politiques de fusion

<!--20 min-->

Dans cette leçon, vous allez créer des politiques de fusion pour donner la priorité à la manière dont plusieurs sources de données fusionnent en profils.

Adobe Experience Platform vous permet de rassembler des données issues de plusieurs sources et de les combiner pour obtenir une vue complète de chaque client. Lors du regroupement de ces données, les politiques de fusion déterminent la priorité des données et les données combinées pour créer cette vue unifiée.

Nous nous en tiendrons à l’interface utilisateur pour cette leçon, mais il existe également des options d’API pour créer des politiques de fusion.

**Architectes de données** devront créer des politiques de fusion en dehors de ce tutoriel.

Avant de commencer les exercices, regardez cette courte vidéo pour en savoir plus sur les politiques de fusion :
>[!VIDEO](https://video.tv.adobe.com/v/345076?captions=fre_fr&learn=on&enablevpops)

## Autorisations requises

Dans la leçon [Configurer les autorisations](configure-permissions.md), vous allez configurer tous les contrôles d’accès requis pour suivre cette leçon.

<!--* Permission items **[!UICONTROL Profile Management]** > **[!UICONTROL View Merge Policies]** and **[!UICONTROL Manage Merge Policies]**
* Permission item **[!UICONTROL Profile Management]** > **[!UICONTROL View Profiles]** and **[!UICONTROL Manage Profiles]**
* Permission item **[!UICONTROL Sandboxes]** > `Luma Tutorial`
* User-role access to the `Luma Tutorial Platform` product profile
-->

## À propos des politiques de fusion et du schéma d’union

Vous vous souvenez peut-être que dans la leçon sur l’ingestion par lots, nous avons chargé deux enregistrements avec des informations légèrement différentes pour le même client. Dans les données [!DNL Loyalty], le prénom du client était `Daniel` et il vivait en `New York City`, mais dans les données CRM, le prénom du client était `Danny` et il vivait en `Portland`. Les données clients changent au fil du temps. Peut-être est-il passé de `Portland` à `New York City`. D’autres éléments changent également, tels que les numéros de téléphone et les adresses e-mail. Les politiques de fusion vous aident à décider comment gérer ces types de conflits lorsque deux sources de données fournissent des informations différentes pour le même utilisateur.

Alors, pourquoi `Danny` a-t-il gagné comme prénom ? Jetons un coup d’œil :

1. Dans l’interface utilisateur de Platform, sélectionnez **[!UICONTROL Profils]** dans le volet de navigation de gauche
1. Accédez à l’onglet **[!UICONTROL Politiques de fusion]**
1. La politique de fusion par défaut utilise un horodatage ordonné. Comme vous avez chargé les données CRM après les données de fidélité, `Danny` a été choisi comme prénom dans le profil :

![Écran Politique de fusion](assets/mergepolicies-default.png)

Lorsque plusieurs schémas sont activés pour le profil, un [!UICONTROL schéma d’union] est automatiquement créé pour tous les schémas d’enregistrement compatibles avec le profil et partageant une classe de base. Vous pouvez afficher les [!UICONTROL Schémas d’union] en accédant à l’onglet **[!UICONTROL Schéma d’union]**.

![Écran Politique de fusion](assets/mergepolicies-unionSchema.png)

Notez qu’il n’existe pas de schéma d’union pour la classe ExperienceEvent. Bien que les données ExperienceEvent soient toujours conservées dans le profil, car elles sont basées sur des séries temporelles, chaque événement inclut une date et une heure, ainsi qu’un identifiant, et les collisions ne posent pas de problème.

Que se passe-t-il si vous n’aimez pas cette politique de fusion par défaut ? Que se passe-t-il si Luma décide que son système de fidélité doit être la source de vérité en cas de conflit ? Pour cela, nous allons créer une politique de fusion.

## Créer une politique de fusion dans l’interface utilisateur

1. Sur l’écran Politiques de fusion, cliquez sur le bouton **[!UICONTROL Créer une politique de fusion]** en haut à droite
1. Dans le champ **[!UICONTROL Nom]**, saisissez `Loyalty Prioritized`
1. En tant que **[!UICONTROL Schéma]**, sélectionnez **[!UICONTROL Profil XDM]** (notez que votre classe personnalisée, puisqu’il s’agit de données d’enregistrement, est également disponible pour les politiques de fusion)
1. Pour **[!UICONTROL Assemblage des identifiants]**, sélectionnez **[!UICONTROL Graphique privé]**
1. Pour **[!UICONTROL Fusion d’attributs]**, sélectionnez **[!UICONTROL Priorité du jeu de données]**
1. Faites glisser et déposez des `Luma Loyalty Dataset` et des `Luma CRM Dataset` dans le panneau **[!UICONTROL Jeu de données]**.
1. Assurez-vous que `Luma Loyalty Dataset` est au-dessus en le faisant glisser et en le déposant au-dessus de la `Luma CRM Dataset`
1. Sélectionnez le bouton **[!UICONTROL Enregistrer]**
   <!--do i need to explain Private Graph? Is that GA?-->
   ![&#x200B; Politique de fusion &#x200B;](assets/mergepolicies-newPolicy.png)

## Validation de la politique de fusion

Voyons si la politique de fusion fonctionne comme prévu :

1. Accédez à l’onglet **[!UICONTROL Parcourir]**
1. Modifiez la **[!UICONTROL politique de fusion]** en votre nouvelle politique de `Loyalty Prioritized`
1. Utilisez votre **[!UICONTROL en tant qu’espace de noms]** Identity`Luma CRM Id`
1. Comme **[!UICONTROL valeur d’identité]** utilisez `f660ab912ec121d1b1e928a0bb4bc61b`
1. Sélectionnez le bouton **[!UICONTROL Afficher le profil]**
1. `Daniel` est de retour !

![Affichage d’un profil avec une politique de fusion différente](assets/mergepolicies-lookupProfileWithMergePolicy.png)

## Créer une politique de fusion avec des jeux de données limités

Lors de la création de politiques de fusion à l’aide de la priorité du jeu de données, seuls les jeux de données de la même classe de base que celle que vous incluez à droite sont inclus dans le profil. Configurez une autre politique de fusion

1. Sur l’écran Politiques de fusion, cliquez sur le bouton **[!UICONTROL Créer une politique de fusion]** en haut à droite
1. Dans le champ **[!UICONTROL Nom]**, saisissez `Loyalty Only`
1. Sélectionnez **[!UICONTROL Schéma]**, puis **[!UICONTROL Profil XDM]**
1. Pour **[!UICONTROL Combinaison d’ID]**, sélectionnez **[!UICONTROL Aucun]**
1. Pour **[!UICONTROL Fusion d’attributs]**, sélectionnez **[!UICONTROL Priorité du jeu de données]**
1. Glissez-déposez uniquement le `Luma Loyalty Dataset` dans le panneau **[!UICONTROL Jeu de données sélectionné]**.
1. Sélectionnez le bouton **[!UICONTROL Enregistrer]**

![Politique de fusion Fidélité uniquement](assets/mergepolicies-loyaltyOnly.png)

## Validation de la politique de fusion

Examinons maintenant l’effet de cette politique de fusion :

1. Accédez à l’onglet **[!UICONTROL Parcourir]**
1. Modifiez la **[!UICONTROL politique de fusion]** en votre nouvelle politique de `Loyalty Only`
1. Utilisez votre **[!UICONTROL en tant qu’espace de noms]** Identity`Luma CRM Id`
1. Comme **[!UICONTROL valeur d’identité]** utilisez `f660ab912ec121d1b1e928a0bb4bc61b`
1. Sélectionnez le bouton **[!UICONTROL Afficher le profil]**
1. Vérifiez qu’aucun profil n’a été trouvé :
   ![Fidélité uniquement pas de recherche d’ID CRM.](assets/mergepolicies-loyaltyOnly-noCrmLookup.png)

L’identifiant CRM est un champ d’identité de la `Luma Loyalty Dataset`, mais seules les identités principales peuvent être utilisées pour rechercher des profils. Recherchons donc le profil à l’aide de l’identité principale, `Luma Loyalty Id` »

1. Remplacez **[!UICONTROL Espace de noms d’identité]** par `Luma Loyalty Id`
1. Comme **[!UICONTROL valeur d’identité]** utilisez `5625458`
1. Sélectionnez le bouton **[!UICONTROL Afficher le profil]**
1. Sélectionnez l’ID du profil pour ouvrir le profil
1. Accédez à l’onglet **[!UICONTROL Attributs]**
1. Notez que d’autres détails du profil du jeu de données CRM, tels que le numéro de téléphone mobile et l’adresse e-mail, ne sont pas disponibles, car notre politique de fusion `Loyalty Only` n’inclut pas le jeu de données CRM.
   ![Les données CRM ne sont pas visibles dans la politique Fidélité uniquement](assets/mergepolicies-loyaltyOnly-attributes.png)
1. Accédez à l’onglet **[!UICONTROL Événements]**
1. Les données ExperienceEvent sont disponibles bien qu’elles ne soient pas explicitement incluses dans les jeux de données de la politique de fusion :
   ![Les événements sont visibles dans la politique Fidélité uniquement](assets/mergepolicies-loyaltyOnly-events.png)

## En savoir plus sur les politiques de fusion

Dans la recherche de profil, redéfinissez la politique de fusion utilisée sur `Default Timebased` et sélectionnez le bouton **[!UICONTROL Afficher le profil]**. Danny est de retour !

![Affichage d’un profil avec une politique de fusion différente](assets/mergepolicies-backToDanny.png)

Que se passe-t-il ici ? Eh bien, la fusion de profils n&#39;est pas une chose unique. Les profils clients en temps réel sont assemblés à la volée, en fonction de divers facteurs, y compris la politique de fusion utilisée. Vous pouvez créer plusieurs politiques de fusion à utiliser dans différents contextes, en fonction de la vue du client que vous souhaitez.

Un cas d’utilisation clé des politiques de fusion concerne la gouvernance des données. Supposons, par exemple, que vous ingériez des données tierces dans Platform qui ne peuvent pas être utilisées pour les cas d’utilisation de la personnalisation, mais _peuvent_ être utilisées pour les cas d’utilisation de la publicité. Vous pouvez créer une politique de fusion qui exclut ce jeu de données tiers et utiliser cette politique de fusion pour créer des segments pour vos cas d’utilisation publicitaire.

## Ressources supplémentaires

* [Documentation sur les politiques de fusion](https://experienceleague.adobe.com/docs/experience-platform/profile/merge-policies/overview.html?lang=fr)
* [Référence de l’API Merge Policies (faisant partie de l’API Real-Time Customer Profile)](https://www.adobe.io/experience-platform-apis/references/profile/#tag/Merge-policies)

Passons maintenant au [cadre de gouvernance des données](apply-data-governance-framework.md).
