---
title: Configuration de Developer Console et de Postman
seo-title: Set up Developer Console and Postman | Getting Started with Adobe Experience Platform for Data Architects and Data Engineers
breadcrumb-title: Configuration de Developer Console et de Postman
description: Dans cette leçon, vous allez configurer un projet dans la console Adobe Developer et vous fournir [!DNL Postman] Collections pour pouvoir commencer à utiliser les API de Platform.
role: Data Architect, Data Engineer
feature: API
kt: 4348
thumbnail: 4348-set-up-developer-console-and-postman.jpg
exl-id: 72b541fa-3ea1-4352-b82b-c5b79ff98491
source-git-commit: 35242a037bc79f18e90399c47e47064634d26a37
workflow-type: tm+mt
source-wordcount: '1320'
ht-degree: 2%

---

# Configuration de Developer Console et [!DNL Postman]

<!--30min-->

Dans cette leçon, vous allez configurer un projet dans la console Adobe Developer et le télécharger. [!DNL Postman] collections afin que vous puissiez commencer à utiliser les API de Platform.

Pour terminer les exercices d’API dans ce tutoriel, [téléchargez l’application Postman pour votre système d’exploitation.](https://www.postman.com/downloads/) Bien que cela ne soit pas nécessaire pour utiliser les API Experience Platform, Postman facilite les processus d’API et Adobe Experience Platform fournit des dizaines de collections Postman pour vous aider à exécuter des appels API et à découvrir comment ils fonctionnent. Le reste de ce tutoriel suppose des connaissances pratiques de Postman. Pour obtenir de l’aide, reportez-vous à la section [Documentation Postman](https://learning.postman.com/).

Platform est une API d’abord créée. Bien que des options d’interface existent également pour toutes les tâches principales, vous pouvez utiliser l’API Platform à un moment donné. Par exemple, pour ingérer des données, déplacez des éléments entre des environnements de test, automatisez les tâches de routine ou utilisez de nouvelles fonctionnalités de Platform avant la création de l’interface utilisateur.

**Architectes de données** et **Ingénieurs de données** Vous devrez peut-être utiliser l’API Platform en dehors de ce tutoriel.

## Autorisations requises

Dans le [Configuration des autorisations](configure-permissions.md) leçon, vous configurez tous les contrôles d’accès requis pour terminer cette leçon.

<!--
* Permission item Sandboxes > `Luma Tutorial`
* Developer-role access to the `Luma Tutorial Platform` product profile
-->

## Configuration de la console Adobe Developer

La console Adobe Developer est la destination des développeurs pour accéder aux API et SDK d’Adobe, écouter des événements en temps quasi réel, exécuter des fonctions sur Runtime ou créer des modules externes ou des applications App Builder. Vous l’utiliserez pour accéder à l’API Experience Platform. Pour plus d’informations, voir [Documentation de la console Adobe Developer](https://www.adobe.io/apis/experienceplatform/console/docs.html)

1. Créez un dossier sur votre ordinateur local nommé `Luma Tutorial Assets` pour les fichiers utilisés dans le tutoriel.

1. Ouvrez le [Console Adobe Developer](https://console.adobe.io){target="_blank"}

1. Connectez-vous et vérifiez que vous vous trouvez dans l’organisation appropriée.

1. Sélectionner **[!UICONTROL Créer un projet]** in [!UICONTROL Démarrage rapide] .

   ![Créer un projet](assets/adobeio-createNewProject.png)


1. Dans le projet nouvellement créé, sélectionnez la **[!UICONTROL Modifier le projet]** button
1. Modifiez la variable **[!UICONTROL Titre du projet]** to `Luma Tutorial API Project` (ajoutez votre nom à la fin, si plusieurs personnes de votre société suivent ce tutoriel)
1. Sélectionnez **[!UICONTROL Enregistrer]**

   ![Configuration de l’API de projet de la console Adobe Developer](assets/adobeio-renameProject.png)


1. Sélectionner **[!UICONTROL Ajout d’une API]**

   ![Configuration de l’API de projet de la console Adobe Developer](assets/adobeio-addAPI.png)

1. Filtrez la liste en sélectionnant **[!UICONTROL Adobe Experience Platform]**

1. Dans la liste des API disponibles, sélectionnez **[!UICONTROL API Experience Platform]** et sélectionnez **[!UICONTROL Suivant]**.

   ![Configuration de l’API de projet de la console Adobe Developer](assets/adobeio-AEPAPI.png)

1. Sélectionner **[!UICONTROL OAuth serveur à serveur]** comme informations d’identification et sélectionnez **[!UICONTROL Suivant]**.
   ![Sélectionnez OAuth Server-to-Server](assets/adobeio-choose-auth.png)

1. Sélectionnez la `AEP-Default-All-Users` profil de produit et sélectionnez **[!UICONTROL Enregistrer l’API configurée]**

   ![Sélectionner le profil de produit](assets/adobeio-selectProductProfile.png)

1. Votre projet Developer Console a maintenant été créé.

1. Dans le **[!UICONTROL Essayez-le]** de la page, sélectionnez **[!UICONTROL Téléchargement pour Postman]** puis sélectionnez **[!UICONTROL OAuth serveur à serveur]** pour télécharger le [!DNL Postman] fichier json d’environnement. Enregistrez le `oauth_server_to_server.postman_environment.json` dans votre `Luma Tutorial Assets` dossier.


   ![Configuration de l’API de projet de la console Adobe Developer](assets/adobeio-io-api.png)

## Demander à un administrateur système d’ajouter les informations d’identification de l’API au rôle

Pour utiliser les informations d’identification de l’API pour interagir avec l’Experience Platform, un administrateur système doit affecter les informations d’identification de l’API au rôle créé dans la leçon précédente.  Si vous n’êtes pas administrateur système, envoyez-les :

1. Le [!UICONTROL Nom] de vos informations d’identification d’API (`Credential in Luma Tutorial API Project`)
1. Le [!UICONTROL Adresse électronique du compte technique] de vos informations d’identification (cela aidera l’administrateur système à trouver les informations d’identification).

   ![[!UICONTROL Nom] et [!UICONTROL Adresse électronique du compte technique] de vos informations d’identification](assets/postman-credentialDetails.png)

Voici les instructions pour l’administrateur système :

1. Se connecter [Adobe Experience Platform](https://platform.adobe.com)
1. Sélectionner **[!UICONTROL Autorisations]** dans le volet de navigation de gauche qui vous mènera au [!UICONTROL Rôles] écran
1. Ouvrez le `Luma Tutorial Platform` rôle
   ![Ouvrir le rôle](assets/postman-openRole.png)
1. Sélectionnez la **[!UICONTROL Informations d’identification de l’API]** tab
1. Sélectionner **[!UICONTROL Ajout des informations d’identification API]**
   ![Ajouter des informations d’identification](assets/postman-addCredential.png)
1. Recherchez le `Credential in Luma Tutorial API Project` informations d’identification, filtrage à l’aide de la variable [!UICONTROL Adresse électronique du compte technique] fourni par le participant au tutoriel, si la liste est longue
1. Sélection des informations d’identification
1. Sélectionnez **[!UICONTROL Enregistrer]**


   ![Ajouter des informations d’identification](assets/postman-findCredential.png)

## Configuration de Postman

>[!CAUTION]
>
>L’interface de Postman est régulièrement mise à jour. Les captures d’écran de ce tutoriel ont été effectuées avec Postman v10.15.1 pour Mac, mais les options de l’interface ont peut-être changé.


1. Télécharger et installer [[!DNL Postman]](https://www.postman.com/downloads/)
1. Ouvrir [!DNL Postman] et créer un espace de travail
   ![Environnement d’import](assets/postman-createWorkspace.png)

1. Importez le fichier d’environnement json téléchargé, `oauth_server_to_server.postman_environment.json`
   ![Environnement d’import](assets/postman-importEnvironment.png)
1. Dans [!DNL Postman], sélectionnez votre environnement dans la liste déroulante

1. Sélectionnez l&#39;icône pour afficher les variables d&#39;environnement :

   ![Changement d’environnement](assets/postman-changeEnvironment.png)


### Ajout du nom de l’environnement de test et de l’identifiant du client

Le `SANDBOX_NAME` et `TENANT_ID` et `CONTAINER_ID` ne sont pas incluses dans l’exportation vers la console Adobe Developer. Nous les ajoutons donc manuellement :

1. Dans [!DNL Postman], ouvrez le **Variables d’environnement**
1. Sélectionnez la **Modifier** lien vers la droite du nom de l&#39;environnement
1. Dans le **Ajouter un nouveau champ de variable**, saisissez `SANDBOX_NAME`
1. Dans les deux champs de valeur, saisissez `luma-tutorial`, le nom que nous avons donné à notre environnement de test dans la leçon précédente. Si vous avez utilisé un nom différent pour votre environnement de test, par exemple luma-tutorial-ignatiusjreilly, veillez à utiliser cette valeur.
1. Dans le **Ajouter un nouveau champ de variable**, saisissez `TENANT_ID`
1. Passez à votre navigateur web et recherchez l’ID de tenant de votre société en accédant à l’interface de l’Experience Platform et en extrayant la partie de l’URL. *après le signe @*. Par exemple, mon identifiant de tenant est `techmarketingdemos` mais la vôtre est différente :

   ![Obtention de l’identifiant du client à partir de l’URL de l’interface de Platform](assets/postman-getTenantId.png)

1. Copiez cette valeur et revenez à la variable [!DNL Postman] Écran Gestion des environnements
1. Collez votre identifiant de client dans les deux champs de valeur
1. Dans le **Ajouter un nouveau champ de variable**, saisissez `CONTAINER_ID`
1. Entrée `global` dans les deux champs de valeur

   >[!NOTE]
   >
   >`CONTAINER_ID` est un champ dont la valeur est modifiée plusieurs fois au cours du tutoriel. When `global` est utilisée, l’API interagit avec les éléments fournis par Adobe dans votre compte Platform. When `tenant` est utilisée, l’API interagit avec vos propres éléments personnalisés.

1. Sélectionnez **Enregistrer**

   ![Champs SANDBOX_NAME, TENANT_ID et CONTAINER_ID ajoutés en tant que variables d’environnement](assets/postman-addEnvFields.png)



## Lancer des appels API

### Récupération d’un jeton d’accès

Adobe fournit un riche ensemble de [!DNL Postman] collections pour vous aider à explorer l’API d’Experience Platform. Ces collections se trouvent dans la variable [Adobe Experience Platform Postman Exemples de référentiel GitHub](https://github.com/adobe/experience-platform-postman-samples). Vous devez marquer ce référentiel comme vous l’utiliserez de nombreuses fois tout au long de ce tutoriel et plus tard lorsque vous implémenterez Experience Platform pour votre propre société.

La première collection fonctionne avec les API Adobe Identity Management Service (IMS). Il s’agit d’un moyen pratique de récupérer un jeton d’accès dans Postman.

Pour générer le jeton d’accès :

1. Téléchargez la [Collection des API du service Identity Management](https://github.com/adobe/experience-platform-postman-samples/blob/master/apis/ims/Identity%20Management%20Service.postman_collection.json) à `Luma Tutorial Assets` folder
1. Importez la collection dans [!DNL Postman]
1. Sélectionner la requête **oAuth : Demander le jeton d’accès** request et select **Envoyer**
1. Vous devriez avoir une `200 OK` réponse avec un jeton d’accès dans la réponse

   ![Demander les jetons](assets/postman-requestToken.png)

1. Le jeton d’accès doit être automatiquement stocké en tant que **ACCESS_TOKEN** de votre variable d’environnement [!DNL Postman] environnement.

   ![Postman](assets/postman-config.png)


### Interaction avec une API Platform

Maintenant, lançons un appel API Platform pour confirmer que nous avons tout correctement configuré.

Ouvrez le [Experience Platform [!DNL Postman] collections dans GitHub](https://github.com/adobe/experience-platform-postman-samples/tree/master/apis/experience-platform). Cette page contient de nombreuses collections, pour diverses API Platform. Je recommande vivement de le mettre en signet.

Faisons maintenant notre premier appel API :

1. Téléchargez la [Collecte de l’API Schema Registry](https://raw.githubusercontent.com/adobe/experience-platform-postman-samples/master/apis/experience-platform/Schema%20Registry%20API.postman_collection.json) à `Luma Tutorial Assets` folder
1. Importez-le dans [!DNL Postman]
1. Ouvrir **API Schema Registry > Schémas > Schémas de liste**
1. Consultez la **Paramètres** et **En-têtes** et notez comment ils incluent certaines des variables d’environnement que nous avons saisies précédemment.
1. Notez que la variable **En-têtes > Champ de valeur Accepter** est défini sur `application/vnd.adobe.xed-id+json`. Les API Schema Registry nécessitent l’une de ces [valeurs d’en-tête Accept spécifiées](https://experienceleague.adobe.com/docs/experience-platform/xdm/api/getting-started.html?lang=en#accept) qui fournissent différents formats dans la réponse.
1. Sélectionner **Envoyer** pour effectuer votre premier appel API Platform !

Espérons que vous avez réussi `200 OK` réponse contenant une liste des schémas XDM fournis par l’Adobe dans votre environnement de test, comme illustré ci-dessous.

![Premier appel API dans Postman](assets/postman-firstAPICall.png)

Si votre appel n’a pas réussi, prenez quelques instants pour déboguer à l’aide des détails de réponse d’erreur de l’appel API et passez en revue les étapes ci-dessus. Si vous êtes bloqué, veuillez demander de l’aide dans la variable [Forum de la communauté](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform/ct-p/adobe-experience-platform-community?profile.language=fr) ou utilisez le lien situé dans la partie droite de cette page pour &quot;Signaler un problème&quot;.

Avec vos autorisations Platform, sandbox et [!DNL Postman] configuré, vous êtes prêt à [données de modèle dans les schémas](model-data-in-schemas.md)!
