---
title: Envoi de données à l’Experience Platform avec le SDK Mobile Platform
description: Découvrez comment envoyer des données à Experience Platform.
solution: Data Collection,Experience Platform
feature: Mobile SDK,Data Ingestion
jira: KT-14637
exl-id: fdd2c90e-8246-4d75-a6db-df3ef31946c4
source-git-commit: 25f0df2ea09bb7383f45a698e75bd31be7541754
workflow-type: tm+mt
source-wordcount: '1032'
ht-degree: 5%

---

# Envoi de données à l’Experience Platform

Découvrez comment envoyer des données d’application mobile à Adobe Experience Platform.

Cette leçon facultative s’applique à tous les clients de Real-Time Customer Data Platform (Real-Time CDP), Journey Optimizer et Customer Journey Analytics. Experience Platform, la base des produits Experience Cloud, est un système ouvert qui transforme toutes vos données (Adobe et non-Adobe) en profils clients fiables. Ces profils client sont mis à jour en temps réel et utilisent des insights pilotés par l’IA pour vous aider à offrir les expériences adéquates sur chaque canal.

Les données [event](events.md), [lifecycle](lifecycle-data.md) et [identity](identity.md) que vous avez collectées et envoyées à l’Edge Network Platform dans les leçons précédentes sont transférées aux services configurés dans votre flux de données, y compris Adobe Experience Platform.

![Architecture](assets/architecture-aep.png)


## Conditions préalables

Votre organisation doit être configurée et des autorisations doivent être accordées pour Adobe Experience Platform.

Si vous n&#39;y avez pas accès, vous pouvez [ignorer cette leçon](install-sdks.md).

## Objectifs d&#39;apprentissage

Dans cette leçon, vous allez :

* Créez un jeu de données Experience Platform.
* Configurez votre flux de données pour transférer des données vers Experience Platform.
* Validez les données du jeu de données.
* Activez votre schéma et votre jeu de données pour Real-time Customer Profile.
* Validation des données dans Real-time Customer Profile.
* Validez les données dans le graphique d’identités.


## Créer un jeu de données

Toutes les données correctement ingérées dans Adobe Experience Platform sont conservées sous la forme de jeux de données dans le lac de données. Un jeu de données est une structure de stockage et de gestion pour une collecte de données (généralement sous la forme d’un tableau) contenant un schéma (des colonnes) et des champs (des lignes). Les jeux de données contiennent également des métadonnées qui décrivent divers aspects des données stockées. Pour plus d’informations, consultez la [documentation](https://experienceleague.adobe.com/docs/experience-platform/catalog/datasets/overview.html?lang=fr) .

1. Accédez à l’interface de l’Experience Platform en la sélectionnant dans le menu Applications ![Apps](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Apps_18_N.svg) en haut à droite.


1. Sélectionnez **[!UICONTROL Jeux de données]** dans le menu de navigation de gauche.

1. Sélectionnez ![Ajouter](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) **[!UICONTROL Créer un jeu de données]**.

1. Sélectionnez **[!UICONTROL Créer un jeu de données à partir d&#39;un schéma]**.
   ![accueil du jeu de données](assets/dataset-create.png)

1. Recherchez votre schéma. par exemple, en utilisant `Luma Mobile` dans le champ de recherche.
1. Sélectionnez votre schéma, par exemple **[!DNL Luma Mobile App Event Schema]**.

1. Sélectionnez **[!UICONTROL Suivant]**.
   ![configuration du jeu de données](assets/dataset-configure.png)

1. Fournissez un **[!UICONTROL nom]**, par exemple `Luma Mobile App Events Dataset` et une **[!UICONTROL description]**.

1. Sélectionnez **[!UICONTROL Terminer]**.
   ![finition du jeu de données](assets/dataset-finish.png)


## Ajout du service Adobe Experience Platform datastream

Pour envoyer vos données XDM de l’Edge Network vers Adobe Experience Platform, ajoutez le service Adobe Experience Platform à la banque de données que vous avez configurée dans le cadre de la [création d’une banque de données](create-datastream.md).

>[!IMPORTANT]
>
>Vous ne pouvez activer le service Adobe Experience Platform que lorsque vous avez créé un jeu de données d’événement.

1. Dans l’interface utilisateur de la collecte de données, sélectionnez **[!UICONTROL Datastreams]** et votre flux de données.

1. Sélectionnez ensuite ![Ajouter](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) **[!UICONTROL Ajouter un service]**.

1. Sélectionnez **[!UICONTROL Adobe Experience Platform]** dans la liste [!UICONTROL Service].

1. Activez le service en activant **[!UICONTROL Enabled]**.

1. Sélectionnez le **[!UICONTROL jeu de données d’événement]** que vous avez créé précédemment, par exemple **[!DNL Luma Mobile App Event Dataset]**.

1. Sélectionnez **[!UICONTROL Enregistrer]**.

   ![Ajouter Adobe Experience Platform en tant que service de flux de données](assets/datastream-service-aep.png)
1. La configuration finale devrait ressembler à ceci.

   ![paramètres du flux de données](assets/datastream-settings.png)


## Validation des données dans le jeu de données

Maintenant que vous avez créé un jeu de données et mis à jour votre flux de données pour envoyer des données à l’Experience Platform, toutes les données XDM envoyées à l’Edge Network Platform sont transférées vers Platform et arrivent dans le jeu de données.

Ouvrez l’application et accédez aux écrans dans lesquels vous effectuez le suivi des événements. Vous pouvez également déclencher des mesures de cycle de vie.

Ouvrez votre jeu de données dans l’interface de Platform. Vous devriez voir les données arriver par lots au jeu de données. Les données arrivent généralement par microlots toutes les 15 minutes. Il se peut donc que vos données ne s’affichent pas immédiatement.

![valider les lots de jeux de données de la plateforme d’entrée de données](assets/platform-dataset-batches.png)

Vous devriez également pouvoir voir des exemples d’enregistrements et de champs à l’aide de la fonctionnalité **[!UICONTROL Preview dataset]** :
![valider le cycle de vie envoyé au jeu de données Platform](assets/lifecycle-platform-dataset.png)

Le [service de requête](https://experienceleague.adobe.com/docs/platform-learn/tutorials/queries/explore-data.html?lang=fr) de Platform constitue un outil plus robuste de validation des données.

## Activation de Real-time Customer Profile

Le profil client en temps réel de l’Experience Platform vous permet de créer une vue d’ensemble de chaque client qui combine des données issues de plusieurs canaux, notamment des données en ligne, hors ligne, CRM et tierces. Le profil vous permet de consolider vos diverses données client en une vue unifiée offrant un compte horodaté et exploitable de chaque interaction client.

### Activation du schéma

1. Ouvrez votre schéma, par exemple **[!DNL Luma Mobile App Event Schema]**.
1. Activez **[!UICONTROL Profile]**.
1. Sélectionnez **[!UICONTROL Les données de ce schéma contiendront une identité principale dans le champ identityMap .]** dans la boîte de dialogue.
1. **[!UICONTROL Enregistrez]** le schéma.

   ![activation du schéma pour profile](assets/platform-profile-schema.png)

### Activer le jeu de données

1. Ouvrez votre jeu de données, par exemple **[!DNL Luma Mobile App Event Dataset]**.
1. Activez **[!UICONTROL Profile]**.

   ![activation du jeu de données pour profile](assets/platform-profile-dataset.png)

### Validation des données dans Profile

Ouvrez l’application et accédez aux écrans où vous effectuez le suivi des événements, par exemple : connectez-vous à l’application Luma et effectuez un achat.

Utilisez Assurance pour trouver l’une des identités transmises dans identityMap (Email, lumaCrmId ou ECID), par exemple l’identifiant CRM.

![saisir une valeur d’identité](assets/platform-identity.png)

Dans l’interface de Platform,

1. Accédez à **[!UICONTROL Profils]** et sélectionnez **[!UICONTROL Parcourir]** dans la barre supérieure.
1. Indiquez les détails de l’identité que vous venez de saisir, par exemple `Luma CRM ID` pour **[!UICONTROL Identity namespace]** et la valeur que vous avez copiée pour **[!UICONTROL Identity Value]**. Sélectionnez ensuite **[!UICONTROL Affichage]**.
1. Pour afficher les détails, sélectionnez le profil.

![rechercher une valeur d’identité](assets/platform-profile-lookup.png)

Sur l’écran **[!UICONTROL Detail]**, vous pouvez voir des informations de base sur l’utilisateur, y compris les **[!UICONTROL **&#x200B; identités liées &#x200B;**]** :
![détails du profil](assets/platform-profile-details.png)

Sur les **[!UICONTROL Événements]**, vous pouvez voir les événements collectés à partir de la mise en oeuvre de votre application mobile pour cet utilisateur :

![événements de profil](assets/platform-profile-events.png)


Dans l’écran des détails du profil :

1. Pour afficher le graphique d’identités, cliquez sur le lien ou accédez à **[!UICONTROL Identités]**, puis sélectionnez **[!UICONTROL Graphique d’identités]** dans la barre supérieure.
1. Pour rechercher la valeur d’identité, spécifiez `Luma CRM ID` comme **[!UICONTROL espace de noms d’identité]** et la valeur copiée comme **[!UICONTROL valeur d’identité]**. Sélectionnez ensuite **[!UICONTROL Affichage]**.

   Cette visualisation vous présente toutes les identités liées entre elles dans un profil et leur origine. Voici un exemple de graphique d’identités constitué des données collectées à la fois à partir de ce tutoriel sur le SDK Mobile (Data Source 2) et du [tutoriel sur le SDK Web](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/overview.html?lang=fr) (Data Source 1) :

   ![saisir une valeur d’identité](assets/platform-profile-identitygraph.png)


## Étapes suivantes

Les spécialistes du marketing et de l’analyse peuvent en faire bien plus avec les données capturées dans Experience Platform, notamment en les analysant dans Customer Journey Analytics et en créant des segments dans Real-Time Customer Data Platform. Vous partez pour un bon départ !


>[!SUCCESS]
>
>Vous avez maintenant configuré votre application pour envoyer des données non seulement à l’Edge Network, mais également à Adobe Experience Platform.<br>Merci d’investir votre temps dans l’apprentissage du SDK Adobe Experience Platform Mobile. Si vous avez des questions, souhaitez partager des commentaires généraux ou avez des suggestions sur le contenu à venir, partagez-les sur cet [post de discussion de la communauté Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796).

Suivant : **[Créer et envoyer des notifications push](journey-optimizer-push.md)**
