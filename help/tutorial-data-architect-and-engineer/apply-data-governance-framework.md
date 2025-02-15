---
title: Application du cadre de gouvernance des données
seo-title: Apply the data governance framework | Getting Started with Adobe Experience Platform for Data Architects and Data Engineers
breadcrumb-title: Application du cadre de gouvernance des données
description: Dans cette leçon, vous allez appliquer le cadre de gouvernance des données aux données que vous avez ingérées dans votre sandbox.
role: Data Architect
feature: Data Governance
jira: KT-4348
thumbnail: 4348-apply-data-governance-framework.jpg
exl-id: 3cc3c794-5ffd-41bf-95d8-be5bca2e3a0f
source-git-commit: 286c85aa88d44574f00ded67f0de8e0c945a153e
workflow-type: tm+mt
source-wordcount: '621'
ht-degree: 5%

---

# Application du cadre de gouvernance des données

<!--15min-->

Dans cette leçon, vous allez appliquer le cadre de gouvernance des données aux données que vous avez ingérées dans votre sandbox.

La gouvernance des données d’Adobe Experience Platform vous permet de gérer les données clients et de garantir la conformité aux réglementations, aux restrictions et aux politiques applicables à l’utilisation des données. Elle joue un rôle essentiel dans Experience Platform à différents niveaux, notamment dans le contrôle de l’utilisation des données.

Avant de commencer les exercices, regardez ces courtes vidéos sur la gouvernance des données :
>[!VIDEO](https://video.tv.adobe.com/v/36653?learn=on&enablevpops)

>[!VIDEO](https://video.tv.adobe.com/v/29708?learn=on&enablevpops)

<!--
## Permissions required

In the [Configure Permissions](configure-permissions.md) lesson, you set up all the access controls required to complete this lesson, specifically:

* Permission items **[!UICONTROL Data Governance]** > **[!UICONTROL Manage Usage Labels]**, **[!UICONTROL Manage Data Usage Policies]** and **[!UICONTROL View Data Usage Policies]**
* Permission items **[!UICONTROL Data Management]** > **[!UICONTROL View Datasets]** and **[!UICONTROL Manage Datasets]**
* Permission item **[!UICONTROL Sandboxes]** > `Luma Tutorial`
* User-role access to the `Luma Tutorial Platform` Product Profile
-->

## Scénario d’entreprise

Luma promet aux membres de son programme de fidélité que les données de fidélité ne seront partagées avec aucun tiers. Nous allons mettre en œuvre ce scénario dans la suite de la leçon.

## Application de libellés de gouvernance des données

La première étape du processus de gouvernance des données consiste à appliquer des libellés de gouvernance à vos données. Avant de procéder, jetons un coup d’œil aux étiquettes disponibles :

1. Dans l’interface utilisateur de Platform, sélectionnez **[!UICONTROL Politiques]** dans le volet de navigation de gauche
1. Accédez à l’onglet **[!UICONTROL Libellés]** pour afficher tous les libellés du compte.

Il existe de nombreux libellés d’usine, et vous pouvez créer les vôtres à l’aide du bouton [!UICONTROL Créer un libellé]. Il existe trois types principaux : [!UICONTROL libellés Contrat], [!UICONTROL libellés Identité] et [!UICONTROL libellés Sensible] qui correspondent à des raisons courantes de restriction des données. Chacune des étiquettes comporte un [!UICONTROL Nom convivial] et un court [!UICONTROL Nom] qui est simplement une abréviation du type et un nombre. Par exemple, le libellé [!DNL C1] est pour « Aucune exportation vers des tiers », ce qui est ce dont nous avons besoin pour notre politique de fidélité.

![Libellé de gouvernance des données](assets/governance-policies.png)

Il est maintenant temps d’étiqueter les données dont nous voulons restreindre l’utilisation :

1. Dans l’interface utilisateur de Platform, sélectionnez **[!UICONTROL Jeux de données]** dans le volet de navigation de gauche
1. Ouvrir le `Luma Loyalty Dataset`
1. Accédez à l’onglet **[!UICONTROL Gouvernance des données]**
1. Vous pouvez appliquer des libellés à des champs individuels ou les appliquer à l’ensemble du jeu de données. Nous appliquerons le libellé à l’ensemble du jeu de données. Cliquez sur l’icône en forme de crayon. Si vous ne voyez pas l’icône, essayez d’élargir votre navigateur ou faites défiler le panneau central vers la droite.
   ![Gouvernance des données](assets/governance-dataset.png)
1. Dans la boîte de dialogue modale, développez la section **[!UICONTROL Libellés de contrat]** et cochez le libellé **[!UICONTROL C2]**
1. Sélectionnez le bouton **[!UICONTROL Enregistrer les modifications]**
   ![Gouvernance des données](assets/governance-applyLabel.png)
1. En revenant à l’écran principal [!UICONTROL Gouvernance des données], lorsque le bouton (bascule) **[!UICONTROL Afficher les libellés hérités]** est activé, vous pouvez voir comment le libellé a été appliqué à tous les champs du jeu de données.
   ![Gouvernance des données](assets/governance-labelsAdded.png)


<!--adding extra, unnecessary fields from field groups makes it harder to see which fields really need labels-->
<!--Are there any best practices for applying governance labels-->

## Créer des politiques de gouvernance des données

Maintenant que nos données sont étiquetées, nous pouvons créer une politique.

1. Dans l’interface utilisateur de Platform, sélectionnez **[!UICONTROL Politiques]** dans le volet de navigation de gauche
1. Dans l’onglet Parcourir , il existe déjà une politique prête à l’emploi appelée « Restriction d’exportation tierce » qui associe le libellé C2 à l’action marketing [!UICONTROL Exporter vers un tiers], exactement ce dont nous avons besoin !
1. Sélectionnez la politique, puis activez-la à l’aide du bouton (bascule) **[!UICONTROL Statut de la politique]**
   ![Gouvernance des données](assets/governance-enablePolicy.png)

Vous pouvez créer vos propres politiques à l’aide du bouton **[!UICONTROL Créer une politique]**. Un assistant s’ouvre, qui vous permet de combiner plusieurs libellés et restrictions d’action marketing.

## Application des politiques de gouvernance

L&#39;application des politiques de gouvernance est évidemment un élément clé du cadre. L’application se produit en aval lorsque les données sont activées et envoyées hors de Platform, en particulier avec le Real-Time Customer Data Platform, que vous possédez peut-être sous licence ou non. Quoi qu’il en soit, cela n’entre pas dans le cadre de ce tutoriel. Mais pour ne pas vous laisser traîner, vous pouvez en savoir plus sur la façon dont les politiques sont appliquées dans cette vidéo, que j&#39;ai mise en file d&#39;attente jusqu&#39;à la partie pertinente. Elle vous indique également ce qui se produit lorsqu’une politique est enfreinte.

>[!VIDEO](https://video.tv.adobe.com/v/33631/?t=151&quality=12&learn=on&enablevpops)


## Ressources supplémentaires

* [Documentation sur la gouvernance des données](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html?lang=fr)
* [Référence de l’API Dataset Service](https://www.adobe.io/experience-platform-apis/references/dataset-service/)
* [Référence de l’API Governance Policy Service](https://www.adobe.io/experience-platform-apis/references/policy-service/)

Passons maintenant à [query service](run-queries.md).
