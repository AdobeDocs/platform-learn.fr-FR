---
title: Création d’une propriété de balise
description: Découvrez comment vous connecter à l’interface de collecte de données et créer une propriété de balise. Cette leçon fait partie du tutoriel Implémentation d’Experience Cloud dans les sites web .
exl-id: f83d374a-a831-4598-b9d3-6f183224b589
source-git-commit: 1fc027db2232c8c56de99d12b719ec10275b590a
workflow-type: tm+mt
source-wordcount: '562'
ht-degree: 51%

---

# Création d’une propriété de balise

Dans cette leçon, vous allez créer votre première propriété de balise.

Une propriété est essentiellement un conteneur que vous remplissez avec des extensions, des règles, des éléments de données et des bibliothèques lorsque vous déployez des balises sur votre site.


>[!WARNING]
>
> Le site web Luma utilisé dans ce tutoriel devrait être remplacé au cours de la semaine du 16 février 2026. Le travail effectué dans le cadre de ce tutoriel peut ne pas s’appliquer au nouveau site web.

## Conditions préalables

Pour suivre les leçons suivantes, vous devez disposer des autorisations de développement, d’approbation, de publication, de gestion des extensions et de gestion des environnements dans les balises. Si vous ne parvenez pas à effectuer l’une de ces étapes parce que vous n’avez pas accès aux options de l’interface utilisateur, contactez votre administrateur Experience Cloud pour demander l’accès à ces options. Pour plus d’informations sur les autorisations des utilisateurs de balises, consultez [la documentation](https://experienceleague.adobe.com/docs/experience-platform/tags/admin/user-permissions.html?lang=fr).

>[!NOTE]
>
>Adobe Experience Platform Launch est intégré à Adobe Experience Platform comme une suite de technologies destinées à la collecte de données. Plusieurs modifications terminologiques ont été déployées dans l’interface. Vous devez en être conscient lors de l’utilisation de ce contenu :
>
> * Platform Launch (côté client) est désormais **[[!DNL tags]](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html?lang=fr)**
> * Platform Launch côté serveur est désormais **[[!DNL event forwarding]](https://experienceleague.adobe.com/docs/experience-platform/tags/event-forwarding/overview.html?lang=fr)**
> * Les configurations Edge sont désormais **[[!DNL datastreams]](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/datastreams.html?lang=fr)**

## Objectifs d’apprentissage

À la fin de cette leçon, vous saurez comment :

* Connectez-vous à l’interface utilisateur de la collecte de données
* Créer une propriété de balise
* Configuration d’une propriété de balise

## Accéder à l’interface de collecte de données

**Pour accéder à Collecte de données**

1. Connectez-vous à [Adobe Experience Cloud](https://experiencecloud.adobe.com)

1. Cliquez sur l’icône ![icône du sélecteur de solutions](images/launch-solutionSwitcher.png) pour ouvrir le sélecteur d’applications

1. Sélectionnez **[!UICONTROL Launch/Collecte de données]** dans le menu ![Ouvrez le sélecteur de solutions à l’aide de l’icône et cliquez sur Launch/Collecte de données](images/launch-solutionSwitcherActivation.png)

L’écran `Tags Properties` devrait s’afficher (si aucune propriété n’a été créée pour ce compte, cet écran peut être vide) :

![Écran Propriétés](images/launch-propertiesScreen.png)

## Création d’une propriété

Une propriété est essentiellement un conteneur que vous remplissez avec des extensions, des règles, des éléments de données et des bibliothèques lorsque vous déployez des balises sur votre site. Une propriété peut être n’importe quel regroupement d’un ou de plusieurs domaines et sous-domaines. Vous pouvez gérer ces ressources et en effectuer le suivi de manière similaire. Par exemple, supposons que vous disposez de plusieurs sites web reposant sur un modèle et que vous souhaitez effectuer le suivi des mêmes ressources sur tous les sites. Vous pouvez appliquer une propriété à plusieurs domaines. Pour en savoir plus sur la création de propriétés, consultez [« Entreprises et propriétés »](https://experienceleague.adobe.com/docs/experience-platform/tags/admin/companies-and-properties.html?lang=fr) dans la documentation du produit.

**Création d’une propriété**

1. Cliquez sur le bouton **[!UICONTROL Nouvelle propriété]** :

   ![Clic sur Nouvelle propriété](images/launch-addNewProperty.png)

1. Nommez votre propriété (par ex. `Luma Tutorial` ou `Luma Tutorial - Daniel`).
1. Saisissez `enablementadobe.com` comme domaine. Il s’agit du domaine sur lequel le site de démonstration Luma est hébergé. Bien que le champ « Domaine » soit obligatoire, la propriété de balise fonctionne sur n’importe quel domaine où elle est implémentée. La fonction principale de ce champ est de préremplir les options de menu du créateur de règles.
1. Développez la section **[!UICONTROL Options avancées]** et cochez la case pour **[!UICONTROL Exécuter les composants de règle en séquence]**
1. Cliquez sur le bouton **[!UICONTROL Enregistrer]**

   ![Création d’une propriété &#x200B;](images/launch-newProperty.png)

Votre nouvelle propriété devrait s’afficher sur la page Propriétés. Notez que si vous cochez la case en regard du nom de la propriété, les options **[!UICONTROL Configurer]** ou **[!UICONTROL Supprimer]** de la propriété s’affichent au-dessus de la liste des propriétés. Cliquez sur le nom de la propriété (par exemple `Luma Tutorial`) pour ouvrir l’écran `Overview`.
![Clic sur le nom de la propriété pour l’ouvrir](images/launch-openProperty.png)

[Suite : « Ajout du code intégré » >](add-embed-code.md)
