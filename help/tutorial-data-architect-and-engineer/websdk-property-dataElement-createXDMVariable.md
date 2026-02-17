---
title: Ingérer des données de flux
seo-title: Ingest streaming data | Getting Started with Adobe Experience Platform for Data Architects and Data Engineers
breadcrumb-title: Ingérer des données de flux
description: Dans cette leçon, vous allez diffuser des données dans Experience Platform à l’aide de Web SDK.
role: Data Engineer
feature: Data Ingestion
jira: KT-4348
thumbnail: 4348-ingest-streaming-data.jpg
exl-id: 09c24673-af8b-40ab-b894-b4d76ea5b112
source-git-commit: 45fec5b2a82e12bdc4a9d017664e8c11d5625cef
workflow-type: tm+mt
source-wordcount: '2966'
ht-degree: 0%

---

# Ingérer des données de flux

<!--1hr-->

Dans cette leçon, vous allez diffuser des données à l’aide de Adobe Experience Platform Web SDK.

>[!WARNING]
>
> Le site web Luma utilisé dans ce tutoriel devrait être remplacé au cours de la semaine du 16 février 2026. Le travail effectué dans le cadre de ce tutoriel peut ne pas s’appliquer au nouveau site web.

Il existe deux tâches principales :

* Implémentez Web SDK sur le site web Luma pour diffuser les événements clients vers Experience Platform Edge Network.

* Configurez un flux de données pour indiquer à Edge Network de transférer les données à notre `Luma Web Events Dataset` dans Experience Platform.

**Ingénieurs de données** devront ingérer des données de flux en dehors de ce tutoriel. Bien que les développeurs web implémentent généralement Web SDK dans un site web, il est important de savoir comment fonctionne le processus. Même si vous n’êtes pas un développeur web, vous devriez être en mesure d’effectuer cette mise en œuvre de base.

Avant de commencer les exercices, regardez ces deux courtes vidéos pour en savoir plus sur l’ingestion des données en flux continu et sur le SDK web :

>[!VIDEO](https://video.tv.adobe.com/v/28425?learn=on&enablevpops)

>[!VIDEO](https://video.tv.adobe.com/v/34141?learn=on&enablevpops)

>[!NOTE]
>
>Bien que ce tutoriel porte sur l’ingestion par flux à partir de sites Web avec Web SDK, vous pouvez également diffuser des données à l’aide de l’[Mobile SDK](https://experienceleague.adobe.com/fr/docs/platform-learn/implement-mobile-sdk/overview), de l’[API Edge Network Server](https://experienceleague.adobe.com/fr/docs/platform-learn/data-collection/server-api/overview) et de l’[API HTTP](https://experienceleague.adobe.com/fr/docs/experience-platform/sources/connectors/streaming/http).

## Autorisations requises

Dans la leçon [Configurer les autorisations](configure-permissions.md), vous allez configurer tous les contrôles d’accès requis pour suivre cette leçon.


## Configurer le flux de données

Tout d’abord, nous allons configurer le flux de données. Un flux de données indique à Experience Platform Edge Network où envoyer les données après les avoir reçues de l’appel Web SDK. Par exemple, souhaitez-vous envoyer les données à Experience Platform, Adobe Analytics ou Adobe Target ?

![SDK web, flux de données et diagramme Edge Network](assets/dc-websdk-datastreams.png)

Pour créer votre [!UICONTROL flux de données] :

1. Vérifiez que vous êtes toujours dans le sandbox ` Luma Tutorial`
1. Sélectionnez **[!UICONTROL Flux de données]** dans le volet de navigation de gauche
1. Sélectionnez le bouton **[!UICONTROL Nouveau flux de données]** dans le coin supérieur droit

   ![Sélectionnez flux de données dans le volet de navigation de gauche](assets/websdk-datastream-newDatastream.png)


1. Pour le **[!UICONTROL Nom]**, saisissez `Luma Platform Tutorial` (ajoutez votre nom à la fin, si plusieurs personnes de votre entreprise suivent ce tutoriel)
1. Sélectionnez le bouton **[!UICONTROL Enregistrer]**

   ![Nommez le flux de données et enregistrez](assets/websdk-datastream-name.png)

Une fois que les données arrivent dans l’Edge, le [!UICONTROL flux de données] les transfère vers les [!UICONTROL services] configurés. Pour envoyer des données à Experience Platform :

1. Sélectionnez **[!UICONTROL Ajouter un service]**
   ![Ajouter un service](assets/websdk-datastream-addService.png)

1. Sélectionner un `Adobe Experience Platform`
1. Sélectionner votre `Luma Web Events Dataset`
1. Sélectionnez **[!UICONTROL Enregistrer]**

   ![Sélectionnez votre jeu de données et enregistrez](assets/websdk-datastream-addPlatformService.png)

Bien qu’il existe une option Jeu de données de profil dans la configuration du train de données, elle ne doit pas être utilisée pour envoyer des données XDM Individual Profile normales à Platform. Ce paramètre ne doit être utilisé que pour envoyer les détails de consentement, de jeton push et de zone géographique de l’activité de l’utilisateur.

Les cases à cocher pour [!UICONTROL Offer Decisioning], [!UICONTROL Segmentation Edge], [!UICONTROL Destinations Personalization] et [!UICONTROL Adobe Journey Optimizer] vous permettent d’activer des données sur Edge, mais ne sont pas utilisées dans ce tutoriel.

## Implémentation de Web SDK

### Ajouter une propriété

Tout d’abord, nous devons créer une propriété de balise (anciennement, une propriété de balise). Une propriété est un conteneur de toutes les fonctionnalités, JavaScript, règles et autres, nécessaires pour collecter des détails dans une page web et l’envoyer à différents emplacements.

Pour créer une propriété :

1. Accédez à **[!UICONTROL Balises]** dans le volet de navigation de gauche
1. Sélectionnez **[!UICONTROL Nouvelle propriété]**
   ![Ajouter une nouvelle propriété](assets/websdk-property-addNewProperty.png)
1. Dans le champ **[!UICONTROL Nom]**, saisissez `Luma Platform Tutorial` (ajoutez votre nom à la fin, si plusieurs personnes de votre entreprise suivent ce tutoriel)
1. Pour le **[!UICONTROL Domaines]**, saisissez `enablementadobe.com` (expliqué plus loin)
1. Sélectionnez **[!UICONTROL Enregistrer]**
   ![Détails de la propriété](assets/websdk-property-propertyDetails.png)


### Ajouter des extensions à la propriété

Maintenant que vous disposez d’une propriété , vous pouvez ajouter le SDK Web à l’aide d’une extension. Une extension est un package de code qui ajoute des fonctionnalités à votre propriété de balise et à votre implémentation. Pour ajouter l’extension :

1. Ouvrir la propriété de balise
1. Accédez à **[!UICONTROL Extensions]** dans le volet de navigation de gauche
1. Accédez à l’onglet **[!UICONTROL Catalogue]**
1. De nombreuses extensions sont disponibles pour les balises. Filtrer le catalogue avec le terme `Web SDK`
1. Sélectionnez l’extension **[!UICONTROL Adobe Experience Platform Web SDK]** pour ouvrir le panneau latéral
1. Sélectionnez le bouton **[!UICONTROL Installer]**
   ![Installation de l’extension Adobe Experience Platform Web SDK](assets/websdk-property-addExtension.png)
1. Plusieurs configurations sont disponibles pour l’extension Web SDK, mais nous n’en configurerons que deux pour ce tutoriel. Mettez à jour le domaine **[!UICONTROL Edge]** en `data.enablementadobe.com`. Ce paramètre vous permet de définir des cookies propriétaires avec votre implémentation de Web SDK, ce qui est recommandé. Lorsque vous implémentez Web SDK sur votre propre site Web, nous vous recommandons de créer un CNAME à des fins de collecte de données, par exemple, `data.YOUR_DOMAIN.com`
1. Dans la section **[!UICONTROL Flux de données]**, pour l’environnement de production, sélectionnez le sandbox `Luma Tutorial` et le flux de données `Luma Platform Tutorial`.
1. N’hésitez pas à consulter les autres options de configuration (mais ne les modifiez pas), puis sélectionnez **[!UICONTROL Enregistrer]**
   ![Configuration de l’extension Web SDK](assets/websdk-property-configureExtension.png)

Dans l’écran Catalogue des extensions , installez l’extension Adobe Client Data Layer (ACDL). Cette extension nous aidera à lire la couche de données du site web Luma :

![Installation de l’extension Adobe Client Data Layer](assets/websdk-property-installACDLExtension.png)

Aucune configuration n’est nécessaire dans l’extension. Il vous suffit donc de l’enregistrer dans votre bibliothèque.

## Créer une règle pour envoyer des données

Nous allons maintenant créer une règle pour envoyer des données à Platform. Une règle est une combinaison d’événements, de conditions et d’actions indiquant aux balises d’effectuer une opération. Pour créer une règle :

1. Accédez à **[!UICONTROL Règles]**
1. Sélectionnez le bouton **[!UICONTROL Créer une règle]**
   ![Créer une règle](assets/websdk-property-createRule.png)
1. Donnez à la règle le nom `adobeDataLayer event`.
1. Sous **[!UICONTROL Événements]**, sélectionnez le bouton **[!UICONTROL Ajouter]**
   ![Nommez la règle et ajoutez un événement](assets/websdk-property-nameRule.png)
1. Utilisez la **[!UICONTROL couche de données client Adobe]** **[!UICONTROL extension]** et sélectionnez **[!UICONTROL données transmises]** comme **[!UICONTROL type d’événement]**.
1. Sélectionnez **[!UICONTROL Écouter]**. **[!UICONTROL Tous les événements]**.
1. Sélectionnez **[!UICONTROL Conserver les modifications]** pour revenir à l’écran principal des règles
   ![Ajoutez l’événement Library Loaded (Bibliothèque chargée)](assets/websdk-property-addEvent.png)
1. Sous **[!UICONTROL Actions]**, sélectionnez le bouton **[!UICONTROL Ajouter]**
1. Utilisez le **[!UICONTROL SDK Web Adobe Experience Platform]** **[!UICONTROL Extension]** et sélectionnez **[!UICONTROL Envoyer l’événement]** comme **[!UICONTROL Type d’action]**
1. Sur la droite, sélectionnez **[!UICONTROL Pages vues des détails de la page web]** dans la liste déroulante **[!UICONTROL Type]**. Ceci renseigne le champ eventType de notre `Luma Web Events Schema`
1. Sélectionnez **[!UICONTROL Conserver les modifications]** pour revenir à l’écran principal des règles
   ![Ajouter l’action Envoyer l’événement](assets/websdk-property-addAction.png)
1. Sélectionnez **[!UICONTROL Enregistrer]** pour enregistrer la règle\
   ![Enregistrer la règle](assets/websdk-property-saveRule.png)

## Publication de la règle dans une bibliothèque

Ensuite, nous publierons la règle dans notre environnement de développement afin de vérifier qu’elle fonctionne.


Pour créer une bibliothèque, procédez comme suit :

1. Accédez à **[!UICONTROL Flux de publication]** dans le volet de navigation de gauche
1. Sélectionnez **[!UICONTROL Ajouter une bibliothèque]**
   ![Sélectionnez Ajouter une bibliothèque](assets/websdk-property-pubAddNewLib.png)
1. Pour le **[!UICONTROL Nom]**, saisissez `Luma Platform Tutorial`
1. Pour le **[!UICONTROL Environnement]**, sélectionnez `Development`
1. Sélectionnez le bouton **[!UICONTROL Ajouter toutes les ressources modifiées]**. (Outre l’extension [!UICONTROL Adobe Experience Platform Web SDK] et la règle `adobeDataLayer event`, vous verrez également l’extension [!UICONTROL Core] ajoutée, qui contient le JavaScript de base requis par toutes les propriétés web des balises.)
1. Sélectionnez le bouton **[!UICONTROL Enregistrer et créer pour développement]**
   ![Création et génération de la bibliothèque](assets/websdk-property-buildLibrary.png)

La création de la bibliothèque peut prendre quelques minutes et, lorsqu’elle est terminée, un point vert s’affiche à gauche du nom de la bibliothèque :
![Création terminée](assets/websdk-property-buildComplete.png)

Comme vous pouvez le voir sur l’écran [!UICONTROL Flux de publication], le processus de publication ne se limite pas au contenu de ce tutoriel. Nous allons simplement utiliser une seule bibliothèque dans notre environnement de développement.

## Valider les données de la requête

### Ajout d’Adobe Experience Platform Debugger

Experience Platform Debugger est une extension disponible pour Chrome qui vous aide à voir la technologie Adobe mise en œuvre dans vos pages web. Téléchargez la version correspondant au navigateur de votre choix :

* [Extension Chrome](https://chrome.google.com/webstore/detail/adobe-experience-platform/bfnnokhpnncpkdmbokanobigaccjkpob)

Si vous n’avez jamais utilisé Debugger auparavant, vous pouvez regarder cette vidéo de présentation de cinq minutes :

>[!VIDEO](https://video.tv.adobe.com/v/32156?learn=on&enablevpops)

### Ouvrir le site web Luma

Pour ce tutoriel, nous utilisons une version hébergée publiquement du site web de démonstration de Luma. Ouvrons-le et mettons-le en signet :

1. Dans un nouvel onglet du navigateur, ouvrez le [site web Luma](https://newluma.enablementadobe.com).
1. Ajoutez un signet à la page à utiliser tout au long du tutoriel.

C’est pour cette raison que nous avons utilisé `enablementadobe.com` dans le champ [!UICONTROL Domaines] de notre configuration initiale de propriété de balise et que nous avons utilisé `data.enablementadobe.com` comme domaine propriétaire dans l’extension [!UICONTROL Adobe Experience Platform Web SDK]. J&#39;avais un plan !

![Page d’accueil Luma](assets/websdk-luma-homepage.png)

### Utiliser Experience Platform Debugger pour mapper à votre propriété de balise

Experience Platform Debugger dispose d’une fonctionnalité pratique qui vous permet de remplacer une propriété de balise existante par une autre. Cela s’avère utile pour la validation et nous permet d’ignorer de nombreuses étapes d’implémentation dans ce tutoriel.

1. Vérifiez que le site Luma est ouvert et sélectionnez l’icône de l’extension Experience Platform Debugger .
1. Le débogueur s’ouvre et affiche certains détails de l’implémentation en codage en dur, sans rapport avec ce tutoriel (vous devrez peut-être recharger le site Luma après l’ouverture du débogueur)
1. Vérifiez que le débogueur est « **[!UICONTROL connecté à Luma]** » comme illustré ci-dessous, puis sélectionnez l’icône « **[!UICONTROL verrouiller]** » pour le verrouiller sur le site Luma.
1. Sélectionnez le bouton **[!UICONTROL Se connecter]** en haut à droite pour vous authentifier.
1. Accédez maintenant à **[!UICONTROL Experience Platform Tags]** dans le volet de navigation de gauche
1. Sélectionnez l’onglet Configuration .
1. À droite de l’emplacement où s’affiche le **[!UICONTROL Codes incorporés de la page]**, ouvrez le menu déroulant **[!UICONTROL Actions]** et sélectionnez **[!UICONTROL Remplacer]**
   ![Sélectionnez Actions > Remplacer](assets/websdk-debugger-replaceLibrary.png)
1. Puisque vous êtes authentifié, le débogueur va extraire vos propriétés et environnements de balises disponibles. Sélectionnez votre propriété `Luma Platform Tutorial`
1. Sélectionner votre environnement `Development`
1. Sélectionnez le bouton **[!UICONTROL Appliquer]**
   ![Sélectionnez la propriété de balise alternative](assets/websdk-debugger-selectProperty.png)
1. Le site web Luma va maintenant se recharger _avec votre propriété de balise_.
   ![propriété de balise remplacée](assets/websdk-debugger-propertyReplaced.png)
1. Accédez à **[!UICONTROL Résumé]** dans le volet de navigation de gauche pour afficher les détails de votre propriété [!UICONTROL balise]
   ![Onglet Résumé](assets/websdk-debugger-summary.png)
1. Accédez maintenant à **[!UICONTROL Experience Platform Web SDK]** dans le volet de navigation de gauche pour afficher les **[!UICONTROL Demandes réseau]**
1. Sélectionnez la ligne **[!UICONTROL événements]**

   ![Requête Adobe Experience Platform Web SDK](assets/websdk-debugger-platformNetwork.png)

1. Notez comment nous pouvons voir le type d’événement `web.webpagedetails.pageView` que nous avons spécifié dans notre action [!UICONTROL Envoyer l’événement]
   ![Requête Adobe Experience Platform Web SDK](assets/websdk-debugger-eventDetails.png)


1. Les détails de la requête sont également visibles dans l’onglet Outils de développement web **Réseau** du navigateur. Ouvrez-la et rechargez la page. Filtrez les appels avec des `interact` pour localiser l’appel, sélectionnez-le, puis recherchez dans la zone **En-têtes** **Payload de requête**.
   ![Onglet Réseau](assets/websdk-debugger-networkTab.png)
1. Accédez à l’onglet **Réponse** et notez comment la valeur ECID est incluse dans la réponse. Copiez cette valeur, car vous l’utiliserez pour valider les informations de profil dans l’exercice suivant.
   ![Onglet Réseau](assets/websdk-debugger-networkTab-response.png)



## Valider les données dans Experience Platform

Vous pouvez vérifier que les données arrivent dans Platform en examinant les lots de données arrivant dans le `Luma Web Events Dataset`. (Je sais, cela s’appelle l’ingestion de données par flux, mais je dis maintenant qu’elle arrive par lots ! Il diffuse en temps réel vers le profil, afin qu’il puisse être utilisé pour la segmentation et l’activation en temps réel, mais il est envoyé par lots toutes les 15 minutes au lac de données.)

Pour valider les données :

1. Dans l’interface utilisateur de Platform, accédez à **[!UICONTROL Jeux de données]** dans le volet de navigation de gauche
1. Ouvrez le `Luma Web Events Dataset` et vérifiez qu’un lot est arrivé. N’oubliez pas qu’ils sont envoyés toutes les 15 minutes. Vous devrez peut-être donc attendre que le lot s’affiche.
1. Sélectionnez le bouton **[!UICONTROL Prévisualiser le jeu de données]**
   ![Ouvrir le jeu de données](assets/websdk-platform-dataset.png)
1. Dans la boîte de dialogue modale de prévisualisation, notez que vous pouvez sélectionner différents champs du schéma à gauche pour prévisualiser ces points de données spécifiques :
   ![Prévisualiser les champs](assets/websdk-platform-datasetPreview.png)

Vous pouvez également vérifier que le nouveau profil s’affiche :

1. Dans l’interface utilisateur de Platform, accédez à **[!UICONTROL Profils]** dans le volet de navigation de gauche
1. Sélectionnez l’espace de noms **[!UICONTROL ECID]** et recherchez votre valeur ECID (copiez-la à partir de la réponse). Le profil possède son propre identifiant, distinct de l’ECID.
1. Sélectionnez l’**[!UICONTROL Identifiant de profil]** pour ouvrir le profil
   ![Rechercher et ouvrir le profil](assets/websdk-platform-openProfile.png)
1. Sélectionnez l’onglet **[!UICONTROL Événements]** pour afficher les pages que vous avez consultées
   ![Événements de profil](assets/websdk-platform-profileEvents.png)\
   <!--![](assets/websdk-platform-confirmProfile.png)-->

## Ajouter des données personnalisées à l’événement

Web SDK renseigne automatiquement de nombreux champs XDM, mais vous devrez inévitablement personnaliser votre implémentation pour collecter des champs supplémentaires à partir de votre site web. C&#39;est très important, mais voici quelques exemples simples.

### Créer un élément de données pour stocker les données XDM

1. Revenez à la propriété de balise `Luma Platform Tutorial`
1. Ouvrez la liste déroulante **[!UICONTROL Sélectionner une bibliothèque de travail]** et sélectionnez votre bibliothèque de `Luma Platform Tutorial`. Ce paramètre facilite la publication de mises à jour supplémentaires dans notre bibliothèque.
1. Accédez maintenant à **[!UICONTROL Éléments de données]** dans le volet de navigation de gauche
1. Sélectionnez le bouton **[!UICONTROL Créer un élément de données]**

   ![Créer un nouvel élément de données](assets/websdk-property-createNewDataElement.png)

Sur la page **[!UICONTROL Éléments de données]** :


1. Dans le champ **[!UICONTROL Nom]**, saisissez `XDM data`
1. Sélectionnez **[!UICONTROL Extension]**, puis `Adobe Experience Platform Web SDK`
1. Sélectionnez **[!UICONTROL comme]** Type d’élément de données`Variable`
1. En tant que **[!UICONTROL Sandbox]**, sélectionnez votre sandbox `Luma Tutorial`
1. Sélectionnez votre **[!UICONTROL en tant que]** Schéma`Luma Web Events Schema`
1. Vérifiez que `Luma Platform Tutorial` est sélectionné comme bibliothèque de travail
1. Sélectionnez **[!UICONTROL Enregistrer dans la bibliothèque]**
   ![Mappez le nom de la page à l’élément de données de l’objet XDM](assets/websdk-property-dataElement-createXDMVariable.png)

### Créer un élément de données pour le nom de page

1. Créer un nouvel élément de données
1. Dans le champ **[!UICONTROL Nom]**, saisissez `Page Name`
1. Sélectionnez **[!UICONTROL comme]** Type d’élément de données`JavaScript Variable`
1. Comme nom de variable **[!UICONTROL JavaScript]**, saisissez `adobeDataLayer.0.page.name`
1. Pour normaliser le format des valeurs, cochez les cases **[!UICONTROL Forcer les valeurs en minuscules]** et **[!UICONTROL Nettoyer le texte]**
1. Sélectionnez **[!UICONTROL Enregistrer dans la bibliothèque]**
   ![Créer un élément de données pour le nom de page](assets/websdk-property-dataElement-pageName.png)


### Ajoutez les données XDM à votre action Envoyer l’événement

Maintenant que vous avez mappé les données aux champs XDM, vous pouvez les inclure dans votre action Envoyer l’événement :

1. Accéder à l’écran **[!UICONTROL Règles]**
1. Ouvrez votre règle de `adobeDataLayer event`
1. Ouvrir l’action `Adobe Experience Platform Web SDK - Send Event`
1. En tant que **[!UICONTROL XDM]**, sélectionnez l’icône pour ouvrir la boîte de dialogue modale de sélection des éléments de données et choisissez votre `XDM data` élément de données
1. Sélectionnez **[!UICONTROL Conserver les modifications]**
   ![Ajoutez les données XDM à votre action Envoyer l’événement](assets/websdk-property-addXDMtoSendEvent.png)

1. Ajoutez une nouvelle action à votre règle
1. Sélectionnez la `Adobe Experience Platform Web SDK` **[!UICONTROL Extension]**
1. Sélectionnez le `Update Variable` **[!UICONTROL Type d’action]**
1. Renseignez votre élément de données `Page Name` en tant que `web.webPageDetails.name`
1. Sélectionnez **[!UICONTROL Conserver les modifications]**
   ![Ajoutez l’action Mettre à jour la variable à votre règle](assets/websdk-property-addUpdateVariableAction.png)

1. Réorganisez les [!UICONTROL Actions] de sorte que [!UICONTROL Mettre à jour la variable] se déclenche avant [!UICONTROL Envoyer l’événement]
1. Maintenant, puisque `Luma Platform Tutorial` a été sélectionné comme votre bibliothèque de travail pour les derniers exercices, vos modifications récentes ont été enregistrées directement dans la bibliothèque. Au lieu de devoir publier vos modifications via l’écran Flux de publication, vous pouvez simplement ouvrir la liste déroulante et sélectionner **[!UICONTROL Enregistrer dans la bibliothèque et créer]**
   ![Enregistrer dans la bibliothèque et créer](assets/websdk-property-saveAndBuildUpdatedSendEvent.png)

Cette action lance la création d’une bibliothèque de balises avec les trois modifications que vous venez d’apporter.

### Valider les données XDM

Vous devriez maintenant pouvoir recharger la page d’accueil Luma, tout en étant mappé à votre propriété de balise à l’aide du débogueur, comme vous l’avez appris précédemment, et voir que le champ du nom de page est renseigné dans la requête.
![Validation des données XDM](assets/websdk-debugger-pageName.png)

Vous pouvez également valider le nom de page pour lequel les données ont été reçues dans Platform, en prévisualisant le jeu de données et le profil.

## Envoyer des identités supplémentaires

Votre implémentation de Web SDK envoie désormais des événements avec l’Experience Cloud ID (ECID) comme identifiant principal. L’ECID est généré automatiquement par le SDK Web et est unique par appareil et navigateur. Un seul client peut avoir plusieurs ECID en fonction de l’appareil et du navigateur qu’il utilise. Comment pouvons-nous obtenir une vue unifiée de ce client et lier son activité en ligne à nos données de gestion de la relation client, de fidélité et d’achat hors ligne ? Pour ce faire, nous collectons des identités supplémentaires au cours de leur session et permettons au Service d’identités de les lier de manière déterministe.

Si vous vous souvenez, j’ai mentionné que nous utiliserions l’ECID et l’ID de gestion de la relation client comme identités pour nos données web dans la leçon [Mappage d’identités](map-identities.md). Collectons donc l’identifiant CRM avec le Web SDK !

### Ajouter un élément de données pour l’identifiant CRM

Tout d’abord, nous allons stocker l’identifiant CRM dans un élément de données :

1. Dans l’interface des balises, ajoutez un élément de données nommé `CRM Id`
1. Sélectionnez **[!UICONTROL Variable JavaScript comme]** Type d’élément de données **&#x200B;**
1. Comme nom de variable **[!UICONTROL JavaScript]**, saisissez `adobeDataLayer.0.user.id`
1. Sélectionnez le bouton **[!UICONTROL Enregistrer dans la bibliothèque]** (`Luma Platform Tutorial` doit toujours être votre bibliothèque de travail)
   ![Ajouter un élément de données pour l’ID CRM](assets/websdk-property-dataElement-crmId.png)

### Ajout de l’identifiant CRM à l’élément de données Identity Map

Maintenant que nous avons capturé la valeur de l’ID CRM, nous devons l’associer à un type d’élément de données spécial appelé l’élément de données [!UICONTROL Identity Map] :

1. Ajoutez un élément de données nommé `Identity Map`
1. Sélectionnez **[!UICONTROL Adobe Experience Platform Web SDK en tant qu’extension]**&#x200B;**&#x200B;**
1. Sélectionnez **[!UICONTROL Type d’élément de données]**, **[!UICONTROL Mappage d’identités]**
1. En tant qu’**[!UICONTROL Espace de noms]**, sélectionnez ou saisissez `Luma CRM Id`, qui est l’[!UICONTROL espace de noms] que nous avons créé dans une leçon précédente.

1. En tant qu’**[!UICONTROL ID]**, sélectionnez l’icône pour ouvrir la boîte de dialogue modale de sélection de l’élément de données et choisissez votre `CRM Id` élément de données
1. Dans le champ **[!UICONTROL État authentifié]**, sélectionnez **[!UICONTROL Authentifié]**
1. Vérifier **[!UICONTROL Principal]**

   >[!TIP]
   >
   > Adobe recommande d’envoyer les identités qui représentent une personne, telles que `Luma CRM Id`, comme identité [!UICONTROL &#x200B; principale].
   >
   > Si la carte des identités contient l’identifiant de personne (par exemple, `Luma CRM Id`), l’identifiant de personne devient l’identité [!UICONTROL principale]. Dans le cas contraire, `ECID` devient l’identité [!UICONTROL &#x200B; principale &#x200B;].

1. Sélectionnez le bouton **[!UICONTROL Enregistrer dans la bibliothèque]** (`Luma Platform Tutorial` doit toujours être votre bibliothèque de travail)
   ![Ajouter l’ID CRM à l’élément de données Mappage d’identités](assets/websdk-property-dataElement-identityMap.png)

>[!NOTE]
>
>Vous pouvez transmettre plusieurs identifiants à l’aide du type de données [!UICONTROL Mappage d’identités].

### Ajouter l’élément de données Mappage d’identités à la variable XDM

Nous devons maintenant mettre à jour l’action Variable XDM dans notre règle pour inclure le mappage d’identité. Ne vous inquiétez pas, nous avons presque fini cette leçon !

1. Ouvrez votre règle de `adobeDataLayer event`
1. Ouvrir l’action `Update variable`
1. Sélectionnez l’élément de données `Identity Map` dans le champ XDM `identityMap`.
1. Sélectionnez **[!UICONTROL Conserver les modifications]**
   ![Ajouter l’élément de données IdentityMap à l’objet XDM](assets/websdk-property-dataElement-addIdentitiesToXDMVariable.png)
1. Comme vous avez `Luma Platform Tutorial` sélectionné comme bibliothèque de travail pour les derniers exercices, sélectionnez **[!UICONTROL Enregistrer dans la bibliothèque et créer]**

   ![Enregistrer et créer la bibliothèque](assets/websdk-property-saveAndBuild.png)

<!--U1770721295408-->

### Validation de l’identité

Pour vérifier que l’identifiant CRM est maintenant envoyé par le SDK Web :

1. Ouvrez le site web [Luma](https://luma.enablementadobe.com/content/luma/us/en.html)
1. Mappez-le à votre propriété de balise à l’aide du débogueur, conformément aux instructions précédentes
1. Sélectionnez le lien **Connexion** en haut à droite du site web Luma
1. Connectez-vous à l’aide des informations d’identification `test@test.com`/`test`
1. Une fois authentifié, examinez l’appel Experience Platform Web SDK dans Debugger (**[!UICONTROL Adobe Experience Platform Web SDK]** > **[!UICONTROL Requêtes réseau]** > **[!UICONTROL événements]** de la requête la plus récente) et vous devriez voir les `lumaCrmId` :
   ![Valider l’identité dans le débogueur](assets/websdk-debugger-confirmIdentity.png)
1. Recherchez à nouveau le profil utilisateur à l’aide de l’espace de noms ECID et de la valeur . Dans le profil, vous verrez l’identifiant CRM, ainsi que l’identifiant de fidélité et les détails du profil, tels que le nom et le numéro de téléphone. Toutes les identités et les données ont été regroupées en un seul profil client en temps réel.
   ![Valider l’identité dans Platform](assets/websdk-platform-lumaCrmIdProfile.png)


## Ressources supplémentaires

* [Implémenter dʼAdobe Experience Cloud avec le SDK web](/help/tutorial-web-sdk/overview.md)
* [Documentation sur l’ingestion en flux continu](https://experienceleague.adobe.com/docs/experience-platform/ingestion/streaming/overview.html?lang=fr)
* [Référence de l’API d’ingestion en flux continu](https://developer.adobe.com/experience-platform-apis/references/streaming-ingestion/)

Très bon travail ! Il s’agissait de beaucoup d’informations sur Web SDK et les balises. Une implémentation complète implique beaucoup plus d’éléments, mais ce sont les principes de base qui vous aideront à commencer et à voir les résultats dans Platform.

>[!NOTE]
>
>Maintenant que vous avez terminé la leçon d’ingestion en flux continu, vous pouvez supprimer le sandbox [!UICONTROL Prod] de votre profil de produit `Luma Tutorial Platform`


Ingénieurs de données, si vous le souhaitez, vous pouvez passer à la leçon [exécuter des requêtes](run-queries.md).

Architectes de données, vous pouvez passer aux [&#x200B; politiques de fusion &#x200B;](create-merge-policies.md)
