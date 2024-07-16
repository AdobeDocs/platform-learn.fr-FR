---
title: Configuration de Developer Console et Postman
seo-title: Set up Developer Console and Postman | Getting Started with Adobe Experience Platform for Data Architects and Data Engineers
breadcrumb-title: Configuration de Developer Console et Postman
description: Dans cette leçon, vous allez configurer un projet dans Adobe Developer Console et vous fournir  [!DNL Postman] Collections afin que vous puissiez commencer à utiliser les API Platform.
role: Data Architect, Data Engineer
feature: API
jira: KT-4348
thumbnail: 4348-set-up-developer-console-and-postman.jpg
exl-id: 72b541fa-3ea1-4352-b82b-c5b79ff98491
source-git-commit: 90f7621536573f60ac6585404b1ac0e49cb08496
workflow-type: tm+mt
source-wordcount: '1259'
ht-degree: 0%

---

# Configuration de Developer Console et [!DNL Postman]

<!--30min-->

Dans cette leçon, vous allez configurer un projet dans Adobe Developer Console et télécharger [!DNL Postman] collections afin de pouvoir commencer à utiliser les API Platform.

Pour terminer les exercices d’API dans ce tutoriel, [téléchargez l’application Postman pour votre système d’exploitation.](https://www.postman.com/downloads/) Bien que cela ne soit pas nécessaire pour utiliser les API Experience Platform, Postman facilite les workflows API et Adobe Experience Platform fournit des dizaines de collections Postman pour vous aider à exécuter des appels API et à découvrir comment ils fonctionnent. Le reste de ce tutoriel suppose des connaissances pratiques de Postman. Pour obtenir de l’aide, reportez-vous à la [documentation Postman](https://learning.postman.com/).

Platform est une API d’abord créée. Bien que des options d’interface existent également pour toutes les tâches principales, vous pouvez utiliser l’API Platform à un moment donné. Par exemple, pour ingérer des données, déplacez des éléments entre des environnements de test, automatisez les tâches de routine ou utilisez de nouvelles fonctionnalités de Platform avant la création de l’interface utilisateur.

**Les architectes de données** et les **ingénieurs de données** peuvent avoir besoin d’utiliser l’API Platform en dehors de ce tutoriel.

## Autorisations requises

Dans la leçon [Configurer les autorisations](configure-permissions.md) , vous configurez tous les contrôles d’accès requis pour terminer cette leçon.

<!--
* Permission item Sandboxes > `Luma Tutorial`
* Developer-role access to the `Luma Tutorial Platform` product profile
-->

## Configuration de Adobe Developer Console

Adobe Developer Console est la destination des développeurs pour accéder aux API et SDK d’Adobe, écouter des événements en temps quasi réel, exécuter des fonctions sur Runtime ou créer des modules externes ou des applications App Builder. Vous l’utiliserez pour accéder à l’API Experience Platform. Pour plus d’informations, voir la [documentation Adobe Developer Console](https://www.adobe.io/apis/experienceplatform/console/docs.html)

1. Créez un dossier sur votre ordinateur local nommé `Luma Tutorial Assets` pour les fichiers utilisés dans le tutoriel.

1. Ouvrez le [Adobe Developer Console](https://console.adobe.io){target="_blank"}

1. Connectez-vous et vérifiez que vous vous trouvez dans l’organisation appropriée.

1. Sélectionnez **[!UICONTROL Créer un nouveau projet]** dans le menu [!UICONTROL Démarrage rapide] .

   ![Créer un projet](assets/adobeio-createNewProject.png)


1. Dans le projet nouvellement créé, cliquez sur le bouton **[!UICONTROL Modifier le projet]**
1. Remplacez le **[!UICONTROL titre du projet]** par `Luma Tutorial API Project` (ajoutez votre nom à la fin si plusieurs personnes de votre société suivent ce tutoriel).
1. Sélectionnez **[!UICONTROL Save]**

   ![Configuration de l’API de projet Adobe Developer Console](assets/adobeio-renameProject.png)


1. Sélectionnez **[!UICONTROL Ajouter une API]**

   ![Configuration de l’API de projet Adobe Developer Console](assets/adobeio-addAPI.png)

1. Filtrez la liste en sélectionnant **[!UICONTROL Adobe Experience Platform]**

1. Dans la liste des API disponibles, sélectionnez **[!UICONTROL API Experience Platform]** et **[!UICONTROL Suivant]**.

   ![Configuration de l’API de projet Adobe Developer Console](assets/adobeio-AEPAPI.png)

1. Sélectionnez **[!UICONTROL OAuth Server-to-Server]** comme informations d’identification et sélectionnez **[!UICONTROL Next]**.
   ![Sélectionnez OAuth Server-to-Server](assets/adobeio-choose-auth.png)

1. Sélectionnez le profil de produit `AEP-Default-All-Users` et sélectionnez **[!UICONTROL Save Configured API]**

   ![Sélectionner un profil de produit](assets/adobeio-selectProductProfile.png)

1. Maintenant, votre projet Developer Console a été créé.

1. Dans la section **[!UICONTROL Essayez-le]** de la page, sélectionnez **[!UICONTROL Télécharger pour Postman]**, puis sélectionnez **[!UICONTROL OAuth Server-to-Server]** pour télécharger le fichier json d’environnement [!DNL Postman]. Enregistrez le `oauth_server_to_server.postman_environment.json` dans votre dossier `Luma Tutorial Assets`.


   ![Configuration de l’API de projet Adobe Developer Console](assets/adobeio-io-api.png)

## Demander à un administrateur système d’ajouter les informations d’identification de l’API au rôle

Pour utiliser les informations d’identification de l’API pour interagir avec l’Experience Platform, un administrateur système doit affecter les informations d’identification de l’API au rôle créé dans la leçon précédente.  Si vous n’êtes pas administrateur système, envoyez-les :

1. [!UICONTROL Nom] de vos informations d’identification API (`Credential in Luma Tutorial API Project`)
1. L’ [!UICONTROL e-mail du compte technique] de vos informations d’identification (l’administrateur système peut ainsi trouver les informations d’identification)

   ![[!UICONTROL Nom] et [!UICONTROL Adresse électronique du compte technique] de vos informations d’identification](assets/postman-credentialDetails.png)

Voici les instructions pour l’administrateur système :

1. Connectez-vous à [Adobe Experience Platform](https://platform.adobe.com)
1. Sélectionnez **[!UICONTROL Autorisations]** dans le volet de navigation de gauche qui vous mènera à l’écran [!UICONTROL Rôles]
1. Ouvrez le rôle `Luma Tutorial Platform`
   ![Ouvrez le rôle](assets/postman-openRole.png)
1. Sélectionnez l’onglet **[!UICONTROL Informations d’identification de l’API]**
1. Sélectionnez **[!UICONTROL Ajouter des informations d’identification d’API]**
   ![Ajouter des informations d’identification](assets/postman-addCredential.png)
1. Recherchez les informations d’identification `Credential in Luma Tutorial API Project`, en filtrant avec le [!UICONTROL courrier électronique du compte technique] fourni par le participant au tutoriel, si la liste est longue.
1. Sélection des informations d’identification
1. Sélectionnez **[!UICONTROL Save]**


   ![Ajouter des informations d’identification](assets/postman-findCredential.png)

## Configuration de Postman

>[!CAUTION]
>
>L’interface de Postman est régulièrement mise à jour. Les captures d’écran de ce tutoriel ont été effectuées avec Postman v10.15.1 pour Mac, mais les options de l’interface ont peut-être changé.


1. Télécharger et installer [[!DNL Postman]](https://www.postman.com/downloads/)
1. Ouvrez [!DNL Postman] et créez un espace de travail.
   ![Environnement d’importation](assets/postman-createWorkspace.png)

1. Importez le fichier d’environnement json téléchargé, `oauth_server_to_server.postman_environment.json`
   ![Environnement d’importation](assets/postman-importEnvironment.png)
1. Dans [!DNL Postman], sélectionnez votre environnement dans la liste déroulante

1. Sélectionnez l&#39;icône pour afficher les variables d&#39;environnement :

   ![Changement d’environnement](assets/postman-changeEnvironment.png)


### Ajout du nom de l’environnement de test et de l’identifiant du client

Les variables `SANDBOX_NAME` et `TENANT_ID` et `CONTAINER_ID` ne sont pas incluses dans l’exportation Adobe Developer Console. Nous les ajoutons donc manuellement :

1. Dans [!DNL Postman], ouvrez les **variables d’environnement**
1. Sélectionnez le lien **Modifier** à droite du nom de l&#39;environnement.
1. Dans le **champ Ajouter une nouvelle variable**, saisissez `SANDBOX_NAME`
1. Dans les deux champs de valeur, saisissez `luma-tutorial`, le nom que nous avons donné à notre environnement de test dans la leçon précédente. Si vous avez utilisé un nom différent pour votre environnement de test, par exemple luma-tutorial-ignatiusjreilly, veillez à utiliser cette valeur.
1. Dans le **champ Ajouter une nouvelle variable**, saisissez `TENANT_ID`
1. Passez à votre navigateur web et recherchez l’ID de client de votre société en accédant à l’interface de l’Experience Platform et en extrayant la partie de l’URL *après le signe @*. Par exemple, mon identifiant de tenant est `techmarketingdemos`, mais le vôtre est différent :

   ![Obtention de l’identifiant du client à partir de l’URL de l’interface de Platform](assets/postman-getTenantId.png)

1. Copiez cette valeur et revenez à l’écran [!DNL Postman] Gérer les environnements
1. Collez l’identifiant du client dans les deux champs de valeur
1. Dans le **champ Ajouter une nouvelle variable**, saisissez `CONTAINER_ID`
1. Entrez `global` dans les deux champs de valeur

   >[!NOTE]
   >
   >`CONTAINER_ID` est un champ dont la valeur a été modifiée plusieurs fois au cours du tutoriel. Lorsque `global` est utilisé, l’API interagit avec les éléments fournis par l’Adobe dans votre compte Platform. Lorsque `tenant` est utilisé, l’API interagit avec vos propres éléments personnalisés.

1. Sélectionnez **Save**

   ![Champs SANDBOX_NAME, TENANT_ID et CONTAINER_ID ajoutés en tant que variables d’environnement](assets/postman-addEnvFields.png)



## Lancer des appels API

### Récupération d’un jeton d’accès

Adobe fournit un riche ensemble de [!DNL Postman] collections pour vous aider à explorer l’API de l’Experience Platform. Ces collections se trouvent dans le [référentiel GitHub d’exemples Adobe Experience Platform Postman](https://github.com/adobe/experience-platform-postman-samples). Vous devez marquer ce référentiel comme vous l’utiliserez de nombreuses fois tout au long de ce tutoriel et plus tard lorsque vous implémenterez Experience Platform pour votre propre société.

La première collection fonctionne avec les API Adobe Identity Management Service (IMS). Il s’agit d’un moyen pratique de récupérer un jeton d’accès dans Postman.

Pour générer le jeton d’accès :

1. Téléchargez la [collection des API de service Identity Management](https://github.com/adobe/experience-platform-postman-samples/blob/master/apis/ims/Identity%20Management%20Service.postman_collection.json) vers votre dossier `Luma Tutorial Assets`
1. Importez la collection dans [!DNL Postman]
1. Sélectionnez la requête **oAuth: Request Access Token** et sélectionnez **Send**
1. Vous devriez obtenir une réponse `200 OK` avec un jeton d’accès dans la réponse.

   ![Demander les jetons](assets/postman-requestToken.png)

1. Le jeton d’accès doit être automatiquement stocké en tant que variable d’environnement **ACCESS_TOKEN** de votre environnement [!DNL Postman].

   ![Postman](assets/postman-config.png)


### Interaction avec une API Platform

Maintenant, lançons un appel API Platform pour confirmer que nous avons tout correctement configuré.

Ouvrez les collections [Experience Platform [!DNL Postman] dans GitHub](https://github.com/adobe/experience-platform-postman-samples/tree/master/apis/experience-platform). Cette page contient de nombreuses collections, pour diverses API Platform. Je recommande vivement de le mettre en signet.

Faisons maintenant notre premier appel API :

1. Téléchargez la [ collection d’API Schema Registry](https://raw.githubusercontent.com/adobe/experience-platform-postman-samples/master/apis/experience-platform/Schema%20Registry%20API.postman_collection.json) dans votre dossier `Luma Tutorial Assets`.
1. Importer dans [!DNL Postman]
1. Ouvrez **API Schema Registry > Schémas > Schémas de liste**
1. Examinez les onglets **Params** et **Headers** et notez comment ils incluent certaines des variables d’environnement que nous avons saisies précédemment.
1. Notez que le **champ En-têtes > Valeur d’acceptation** est défini sur `application/vnd.adobe.xed-id+json`. Les API Schema Registry nécessitent l’une de ces [valeurs d’en-tête Accept spécifiées](https://experienceleague.adobe.com/docs/experience-platform/xdm/api/getting-started.html?lang=en#accept) qui fournissent différents formats dans la réponse.
1. Sélectionnez **Send** pour effectuer votre premier appel API Platform !

Espérons que vous obteniez une réponse `200 OK` réussie contenant une liste des schémas XDM fournis par l’Adobe dans votre environnement de test, comme illustré ci-dessous.

![Premier appel API dans Postman](assets/postman-firstAPICall.png)

Si votre appel n’a pas réussi, prenez quelques instants pour déboguer à l’aide des détails de réponse d’erreur de l’appel API et passez en revue les étapes ci-dessus. Si vous êtes bloqué, demandez de l’aide sur le [forum de la communauté](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform/ct-p/adobe-experience-platform-community?profile.language=fr) ou utilisez le lien situé à droite de cette page pour &quot;consigner un problème&quot;.

Avec vos autorisations Platform, sandbox et [!DNL Postman] configurées, vous êtes prêt à [modéliser les données dans les schémas](model-data-in-schemas.md) !
