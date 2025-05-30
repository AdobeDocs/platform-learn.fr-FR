---
title: Création d’un schéma XDM pour les implémentations du SDK Platform Mobile
description: Découvrez comment créer un schéma XDM pour les événements d’application mobile.
feature: Mobile SDK,Schemas
jira: KT-14624
exl-id: c6b0d030-437a-4afe-b7d5-5a7831877983
source-git-commit: 63987fb652a653283a05a5f35f7ce670127ae905
workflow-type: tm+mt
source-wordcount: '1414'
ht-degree: 14%

---

# Créer un schéma XDM

Découvrez comment créer un schéma XDM pour les événements d’application mobile.

La normalisation et l’interopérabilité sont les concepts clés d’Adobe Experience Platform. Le modèle de données d’expérience (XDM), optimisé par Adobe, vise à normaliser les données d’expérience client et à définir des schémas pour la gestion de l’expérience client.

## Que sont les schémas XDM ?

XDM est une spécification documentée publiquement conçue pour améliorer la puissance des expériences digitales. Il fournit des structures et des définitions communes qui permettent à toute application de communiquer avec les services Platform. L’adhésion aux normes XDM permet d’intégrer toutes les données d’expérience client dans une représentation commune afin de fournir des informations de manière plus rapide et intégrée. Vous obtenez des informations précieuses à partir des actions des clients, définissez les audiences des clients par le biais de segments et utilisez les attributs du client à des fins de personnalisation.

Experience Platform utilise des schémas pour décrire la structure des données de manière cohérente et réutilisable. En définissant les données de manière cohérente sur l’ensemble des systèmes, il est plus simple de leur donner du sens et donc d’en tirer profit.

Avant que les données puissent être ingérées dans Platform, il est nécessaire de composer un schéma pour décrire la structure des données et fournir des contraintes au type de données pouvant être contenues dans chaque champ. Les schémas se composent d’une classe de base et de zéro ou plusieurs groupes de champs.

Pour plus d’informations sur le modèle de composition de schémas, y compris sur les principes de conception et les bonnes pratiques, consultez les [ principes de base de la composition de schémas](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/composition.html?lang=fr) ou la liste de lecture [Modèle de vos données d’expérience client avec XDM](https://experienceleague.adobe.com/fr/playlists/experience-platform-model-your-customer-experience-data-with-xdm).

>[!TIP]
>
>Si vous connaissez les DTS (Solution Design Reference) d’Analytics, vous pouvez considérer un schéma comme un DTS plus robuste. Pour plus d’informations, voir [Création et gestion d’un document de référence de conception de solution (SDR)](https://experienceleague.adobe.com/docs/analytics-learn/tutorials/implementation/implementation-basics/creating-and-maintaining-an-sdr.html?lang=fr) .

## Conditions préalables

Pour terminer la leçon, vous devez disposer des autorisations nécessaires pour créer un schéma Experience Platform.

## Objectifs d&#39;apprentissage

Dans cette leçon, vous allez :

* Création d’un schéma dans l’interface de collecte de données
* Ajouter un groupe de champs standard au schéma
* Création et ajout d’un groupe de champs personnalisé au schéma

## Accès aux schémas

1. Connectez-vous à Adobe Experience Cloud.

1. Vérifiez que vous vous trouvez dans l’environnement de test Experience Platform que vous utilisez pour ce tutoriel.

1. Ouvrez le sélecteur d’applications ![sélecteur d’applications](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Apps_18_N.svg) (en haut à droite),

1. Sélectionnez **[!UICONTROL Collecte de données]** dans le menu.

   ![Connexion à l’Experience Cloud](assets/experiencecloud-login.png)

   >[!NOTE]
   >
   > Les clients d’applications basées sur Platform telles que Real-Time CDP doivent utiliser un environnement de test de développement pour ce tutoriel. D’autres clients utilisent l’environnement de test de production par défaut.


1. Sélectionnez **[!UICONTROL Schémas]** sous **[!UICONTROL Data Management]** dans le rail de gauche.

   ![Écran d’accueil des balises](assets/mobile-schema-navigate.png)

Vous vous trouvez maintenant sur la page des schémas principaux et une liste des schémas existants s’affiche. Vous pouvez également voir les onglets correspondant aux blocs de création principaux d’un schéma :

* **Les groupes de champs** sont des composants réutilisables qui définissent un ou plusieurs champs pour capturer des données spécifiques, telles que des détails personnels, des préférences d’hôtel ou une adresse.
* **Classes** définissent les aspects comportementaux des données contenues dans le schéma. Par exemple : `XDM ExperienceEvent` capture des séries temporelles, des données d’événement et `XDM Individual Profile` capture des données d’attribut sur un individu.
* **Les types de données** sont utilisés comme types de champs de référence dans des classes ou des groupes de champs de la même manière que les champs littéraux de base.

Les descriptions ci-dessus constituent un aperçu général. Pour plus d’informations, visionnez la vidéo [Blocs de création de schémas](https://experienceleague.adobe.com/docs/platform-learn/tutorials/schemas/schema-building-blocks.html?lang=fr) ou lisez [Principes de base de la composition de schémas](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/composition.html?lang=fr) dans la documentation du produit.

Dans ce tutoriel, vous utilisez le groupe de champs Événement d’expérience client et créez un groupe personnalisé pour démontrer le processus.

>[!NOTE]
>
>Adobe continue d’ajouter davantage de groupes de champs standard et ils doivent être utilisés chaque fois que cela est possible, car ces champs sont implicitement compris par les services Experience Platform et offrent une plus grande cohérence lorsqu’ils sont utilisés dans les composants Platform. L’utilisation de groupes de champs standard offre des avantages tangibles, tels que le mappage automatique dans les fonctionnalités Analytics et AI dans Platform.

## Architecture du schéma de l’application Luma

Dans un scénario réel, le processus de conception de schéma peut se présenter comme suit :

* Rassemblez les besoins de l’entreprise.
* Recherchez des groupes de champs prédéfinis pour répondre au plus grand nombre d’exigences possible.
* Créez des groupes de champs personnalisés pour les espaces.

À des fins d’apprentissage, vous utilisez des groupes de champs prédéfinis et personnalisés.

* **Événement d’expérience client** : groupe de champs prédéfini qui contient de nombreux champs communs.
* **Informations sur l’application** : groupe de champs personnalisé conçu pour imiter les concepts TrackState/TrackAction Analytics.

<!--Later in the tutorial, you can [update the schema](lifecycle-data.md) to include the **[!UICONTROL AEP Mobile Lifecycle Details]** field group.-->

## Créer un schéma

1. Sélectionnez **[!UICONTROL Créer un schéma]**.

1. À l’étape **[!UICONTROL Sélectionner une classe]** de l’assistant **[!UICONTROL Créer un schéma]**, sélectionnez **[!UICONTROL Experience Event]** sous **[!UICONTROL Sélectionner une classe de base pour ce schéma]**.

1. Sélectionnez **[!UICONTROL Suivant]**.

   ![Classe de base de l’assistant de schéma](assets/schema-wizard-base-class.png)

1. À l’étape **[!UICONTROL Nom et révision]** de l’assistant **[!UICONTROL Créer un schéma]**, saisissez un **[!UICONTROL nom d’affichage de schéma]**, par exemple `Luma Mobile Event Schema` et une [!UICONTROL description], par exemple `Schema for Luma mobile app experience events`.

   >[!NOTE]
   >
   >Si vous passez par ce tutoriel avec plusieurs personnes sur un seul environnement de test ou que vous utilisez un compte partagé, envisagez d’ajouter ou de préparer une identification dans le cadre de vos conventions d’appellation. Par exemple, utilisez `Luma Mobile App Event Schema - Joe Smith` au lieu de `Luma Mobile App Event Schema`. Voir également la note dans [Overview](overview.md).

1. Sélectionnez **[!UICONTROL Terminer]** pour terminer l’assistant.

   ![Nom du schéma et révision](assets/schema-wizard-name-and-review.png)


1. Sélectionnez ![Plus](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) **&#x200B;**&#x200B;en regard de **[!UICONTROL Groupes de champs]**.

   ![Ajout d’un groupe de champs.](assets/add-field-group.png)

1. Recherchez `Consumer Experience Event`.

1. Sélectionnez ![Aperçu](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Preview_18_N.svg) pour prévisualiser les champs et/ou lire la description pour plus de détails avant de sélectionner un groupe de champs.

1. Sélectionnez **Événement d’expérience client**.

1. Sélectionnez **[!UICONTROL Ajouter des groupes de champs]**.

   ![Sélectionner un groupe de champs](assets/schema-select-field-groups.png)

   Vous revenez à l’écran principal de composition de schéma où vous pouvez voir tous les champs disponibles.

1. Sélectionnez **[!UICONTROL Enregistrer]**.

>[!NOTE]
>
>Gardez à l’esprit que vous n’avez pas à utiliser tous les champs d’un groupe. Vous pouvez également supprimer des champs pour que le schéma reste concis et compréhensible. Si cela s’avère utile, vous pouvez considérer un schéma comme une couche de données vide. Dans votre application, vous renseignez les valeurs appropriées au moment approprié.

Le groupe de champs [!UICONTROL &#x200B; Consumer Experience Event] a un type de données appelé [!UICONTROL Web information], qui décrit des événements tels que des pages vues et des clics sur les liens. Au moment de la rédaction de cet article, il n’existe pas de parité d’application mobile pour cette fonctionnalité. Vous allez donc créer la vôtre.

## Créer un type de données personnalisé

Vous commencez par créer un type de données personnalisé décrivant les deux événements :

* Affichage d’écran
* Interaction de l’application

1. Sélectionnez l’onglet **[!UICONTROL Types de données]** .

1. Sélectionnez **[!UICONTROL Créer un type de données]**.

   ![Menu de type de données sélectionné](assets/schema-datatype-create.png)

1. Fournissez un **[!UICONTROL nom d’affichage]** et **[!UICONTROL Description]**, par exemple `App Information` et `Custom data type describing "Screen Views" & "App Actions"`

   ![Fournir le nom et la description](assets/schema-datatype-name.png)

   >[!TIP]
   >
   > Utilisez toujours des [!UICONTROL noms d’affichage] lisibles et descriptifs pour vos champs personnalisés, car cette pratique les rend plus accessibles aux marketeurs lorsque les champs apparaissent dans des services en aval comme le créateur de segments.


1. Pour ajouter un champ, cliquez sur le bouton ![Plus](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) .


1. Ce champ est un objet conteneur pour l’interaction de l’application. Par conséquent, fournissez un **[!UICONTROL nom du champ]** `appInteraction`, **[!UICONTROL nom d’affichage]** `App Interaction` et sélectionnez `Object` dans la liste **[!UICONTROL Type]**.

1. Sélectionnez **[!UICONTROL Appliquer]**.

   ![Ajout d’un nouvel événement d’action d’application](assets/schema-datatype-app-action.png)

1. Pour mesurer la fréquence d’une action, ajoutez un champ en sélectionnant le bouton ![Plus](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) en regard de l’objet **[!UICONTROL appInteraction]** que vous avez créé.

1. Donnez-lui un **[!UICONTROL nom de champ]** `appAction`, **[!UICONTROL nom d’affichage]** de `App Action` et **[!UICONTROL type]** `Measure`.

   Cette étape serait l’équivalent d’un événement de succès dans Adobe Analytics.

1. Sélectionnez **[!UICONTROL Appliquer]**.

   ![Ajout d’un champ de nom d’action](assets/schema-datatype-action-name.png)

1. Ajoutez un champ décrivant le type d&#39;interaction en sélectionnant le bouton ![Plus](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) en regard de l&#39;objet **[!UICONTROL appInteraction]** .

1. Donnez-lui un **[!UICONTROL nom du champ]** `name`, **[!UICONTROL nom d’affichage]** de `Name` et **[!UICONTROL type]** `String`.

   Cette étape équivaut à une dimension dans Adobe Analytics.

   ![Sélectionner appliquer](assets/schema-datatype-apply.png)

1. Faites défiler l’écran jusqu’au bas du rail droit et sélectionnez **[!UICONTROL Appliquer]**.

1. Pour créer un objet `appStateDetails` contenant un champ **[!UICONTROL Mesure]** appelé `screenView` et deux champs **[!UICONTROL Chaîne]** appelés `screenName` et `screenType`, procédez comme vous l&#39;avez fait lors de la création de l&#39;objet **[!UICONTROL appInteraction]**.

1. Sélectionnez **[!UICONTROL Enregistrer]**.

   ![État final du type de données](assets/schema-datatype-final.png)

## Ajouter un groupe de champs personnalisé

Ajoutez maintenant un groupe de champs personnalisé à l’aide de votre type de données personnalisé :

1. Ouvrez le schéma que vous avez créé précédemment dans cette leçon.

1. Sélectionnez ![Plus](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) **&#x200B;**&#x200B;en regard de **[!UICONTROL Groupes de champs]**.

   ![Ajout d’un nouveau groupe de champs](assets/schema-fieldgroup-add.png)

1. Sélectionnez **[!UICONTROL Créer un groupe de champs]**.

1. Fournissez un **[!UICONTROL nom d’affichage]** et une **[!UICONTROL description]**, par exemple, `App Interactions` et `Fields for app interactions`.

1. Sélectionnez **Ajouter des groupes de champs**.

   ![Fournir le nom et la description](assets/schema-fieldgroup-name.png)

1. Dans l’écran de composition principal, sélectionnez **[!UICONTROL Interactions de l’application**].

1. Ajoutez un champ à la racine du schéma en sélectionnant le bouton ![Plus](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) en regard du nom du schéma.

1. Dans le rail de droite, indiquez un **[!UICONTROL nom du champ]** de `appInformation`, un **[!UICONTROL nom d’affichage]** de `App Information` et un **[!UICONTROL type]** de `App Information`.

1. Sélectionnez **[!UICONTROL Interactions avec l’application]** dans la liste déroulante **[!UICONTROL Groupe de champs]** pour affecter les champs à votre nouveau groupe de champs.

1. Sélectionnez **[!UICONTROL Appliquer]**.

1. Sélectionnez **[!UICONTROL Enregistrer]**.

   ![Sélectionner appliquer](assets/schema-fieldgroup-apply.png)

>[!NOTE]
>
>Les groupes de champs personnalisés sont toujours placés sous l’identifiant de votre organisation Experience Cloud.


>[!SUCCESS]
>
>Vous devez maintenant utiliser un schéma pour le reste du tutoriel.
>
>Merci d’investir votre temps à apprendre sur le SDK Adobe Experience Platform Mobile. Si vous avez des questions, souhaitez partager des commentaires généraux ou avez des suggestions sur le contenu à venir, partagez-les sur cet [post de discussion de la communauté Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796?profile.language=fr).

Suivant : **[Créez un [!UICONTROL flux de données]](create-datastream.md)**
