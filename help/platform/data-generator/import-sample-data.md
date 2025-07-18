---
title: Importer des données d’exemple dans Adobe Experience Platform
description: Découvrez comment configurer un environnement sandbox Experience Platform avec des exemples de données.
feature: API
role: Developer
level: Experienced
jira: KT-7349
last-substantial-update: 2023-06-21T00:00:00Z
exl-id: da94f4bd-0686-4d6a-a158-506f2e401b4e
source-git-commit: 1836e80bbf3d38b600f120d83d6628a9cb3c257b
workflow-type: tm+mt
source-wordcount: '1776'
ht-degree: 6%

---

# Importer des données d’exemple dans Adobe Experience Platform

Découvrez comment configurer un environnement sandbox Experience Platform avec des données d’exemple. À l’aide d’une collection Postman, vous pouvez créer des groupes de champs, des schémas, des jeux de données, puis importer des données d’exemple dans Experience Platform.

## Exemple de cas d’utilisation de données

Les utilisateurs professionnels d’Experience Platform doivent souvent passer par une série d’étapes comprenant l’identification des groupes de champs, la création de schémas, la préparation des données, la création de jeux de données, puis l’ingestion de données avant de pouvoir explorer les fonctionnalités marketing offertes par Experience Platform. Ce tutoriel automatise certaines des étapes afin que vous puissiez obtenir des données dans un sandbox Platform le plus rapidement possible.

Ce tutoriel se concentre sur une marque fictive de vente au détail appelée Luma. Ils investissent dans Adobe Experience Platform pour combiner les données de fidélité, de gestion de la relation client (CRM), de catalogue de produits et d’achat hors ligne dans des profils clients en temps réel et activer ces profils pour faire passer leur marketing au niveau supérieur. Nous avons généré des exemples de données pour Luma. Dans la suite de ce tutoriel, vous importerez ces données dans l’un de vos environnements de sandbox Experience Platform.

>[!NOTE]
>
>Le résultat final de ce tutoriel est un sandbox contenant des données similaires au tutoriel [Prise en main de Adobe Experience Platform pour les architectes et ingénieurs de données](https://experienceleague.adobe.com/docs/platform-learn/getting-started-for-data-architects-and-data-engineers/overview.html?lang=fr). Elle a été mise à jour en avril 2023 pour prendre en charge les [défis de Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer-learn/challenges/introduction-and-prerequisites.html?lang=fr). Elle a été mise à jour en juin 2023 pour passer la méthode d’authentification à OAuth.


## Conditions préalables

* Vous avez accès aux API d’Experience Platform et savez comment vous authentifier. Sinon, consultez ce [tutoriel](https://experienceleague.adobe.com/docs/platform-learn/tutorials/platform-api-authentication.html?lang=fr).
* Vous avez accès à un sandbox de développement Experience Platform.
* Vous connaissez votre identifiant client Experience Platform. Vous pouvez l’obtenir en effectuant une requête [API](https://experienceleague.adobe.com/docs/experience-platform/xdm/api/getting-started.html?lang=fr#know-your-tenant_id) authentifiée
ou en l’extrayant de l’URL lorsque vous vous connectez à votre compte Platform. Par exemple, dans l’URL suivante, le client est « `techmarketingdemos` » `https://experience.adobe.com/#/@techmarketingdemos/sname:prod/platform/home`.

## Utilisation de [!DNL Postman] {#postman}

### Configuration des variables d’environnement

Avant de suivre les étapes, vérifiez que vous avez téléchargé l’application [Postman](https://www.postman.com/downloads/). C’est parti !

1. Téléchargez le fichier [platform-utils-main.zip](../assets/data-generator/platform-utils-main.zip), qui contient tous les fichiers requis pour ce tutoriel.

   >[!NOTE]
   >
   >Les données utilisateur contenues dans le fichier [platform-utils-main.zip](../assets/data-generator/platform-utils-main.zip) sont fictives et ne doivent être utilisées qu’à des fins de démonstration.

1. Dans votre dossier de téléchargements, déplacez le fichier `platform-utils-main.zip` vers l’emplacement souhaité sur votre ordinateur, puis décompressez-le.
1. Dans le dossier `luma-data`, ouvrez tous les fichiers `json` dans un éditeur de texte et remplacez toutes les instances de `_yourTenantId` par votre propre ID client, précédé d’un trait de soulignement.
1. Ouvrez `luma-offline-purchases.json`, `luma-inventory-events.json` et `luma-web-events.json` dans un éditeur de texte et mettez à jour toutes les dates et heures afin que les événements se produisent le mois dernier (par exemple, recherchez `"timestamp":"2022-11` et remplacez l’année et le mois)
1. Notez l’emplacement du dossier décompressé, car vous en aurez besoin ultérieurement lors de la configuration de la variable d’environnement `FILE_PATH` [!DNL Postman] :

   >[!NOTE]
   > Pour obtenir le chemin d’accès au fichier sur votre Mac, accédez au dossier `platform-utils-main`, cliquez avec le bouton droit de la souris sur le dossier et sélectionnez l’option **Obtenir des informations**.
   >
   > ![Chemin du fichier MAC](../assets/data-generator/images/mac-file-path.png)

   >[!NOTE]
   > Pour obtenir le chemin d&#39;accès au fichier sous Windows, cliquez pour ouvrir le dossier désiré, puis cliquez avec le bouton droit de la souris à droite du chemin d&#39;accès dans la barre d&#39;adresse. Copiez l’adresse pour obtenir le chemin d’accès au fichier.
   > 
   > ![Chemin d’accès au fichier Windows](../assets/data-generator/images/windows-file-path.png)

1. Ouvrez [!DNL Postman] et créez un espace de travail à partir du menu déroulant **Espaces de travail** :\
   ![Créer un espace de travail](../assets/data-generator/images/create-workspace.png)
1. Saisissez un **Nom** et un **Résumé** facultatifs pour votre espace de travail, puis cliquez sur **Créer un Workspace**. [!DNL Postman] passera à votre nouvel espace de travail lorsque vous le créerez.
   ![Enregistrer l’espace de travail](../assets/data-generator/images/save-workspace.png)
1. Ajustez maintenant certains paramètres pour exécuter les collections de [!DNL Postman] dans cet espace de travail. Dans l’en-tête de [!DNL Postman], cliquez sur l’icône d’engrenage et sélectionnez **Paramètres** pour ouvrir la boîte de dialogue modale des paramètres. Vous pouvez également utiliser le raccourci clavier (CMD/Ctrl + ,) pour ouvrir la boîte de dialogue modale.
1. Sous l’onglet `General` , mettez à jour le délai d’expiration de la requête en ms pour `5000 ms` et activer `allow reading file outside this directory`
   ![Paramètres](../assets/data-generator/images/settings.png)

   >[!NOTE]
   > Si les fichiers sont chargés à partir du répertoire de travail, il s&#39;exécutera sans problème sur les périphériques si les mêmes fichiers sont stockés sur les autres périphériques. Cependant, si vous souhaitez exécuter des fichiers situés en dehors du répertoire de travail, un paramètre doit être activé pour indiquer la même intention. Si votre `FILE_PATH` n’est pas identique au chemin d’accès au répertoire de travail du [!DNL Postman], cette option doit être activée.

1. Fermez le panneau **Paramètres**.
1. Sélectionnez le **Environnements** puis sélectionnez **Importer** :
   ![Import d’environnement](../assets/data-generator/images/env-import.png)
1. Importez le fichier d’environnement json téléchargé, `DataInExperiencePlatform.postman_environment`
1. Dans Postman, sélectionnez votre environnement dans le menu déroulant du coin supérieur droit, puis cliquez sur l’icône représentant un œil pour afficher les variables d’environnement :
   ![Sélection de l’environnement](../assets/data-generator/images/env-selection.png)

1. Assurez-vous que les variables d’environnement suivantes sont renseignées. Pour savoir comment obtenir la valeur des variables d’environnement, consultez le tutoriel [S’authentifier auprès des API Experience Platform](/help/platform/api/platform-api-authentication.md) pour obtenir des instructions détaillées.

   * `CLIENT_SECRET`
   * `API_KEY` : `Client ID` dans Adobe Developer Console
   * `SCOPES`
   * `TECHNICAL_ACCOUNT_ID`
   * `IMS`
   * `IMS_ORG` : `Organization ID` dans Adobe Developer Console
   * `SANDBOX_NAME`
   * `TENANT_ID` : veillez à commencer par un trait de soulignement, par exemple `_techmarketingdemos`
   * `CONTAINER_ID`
   * `platform_end_point`
   * `FILE_PATH` : utilisez le chemin d&#39;accès au dossier local dans lequel vous avez décompressé le fichier `platform-utils-main.zip`. Veillez à inclure le nom du dossier, par exemple `/Users/dwright/Desktop/platform-utils-main`

1. **Enregistrer** l’environnement mis à jour

### Importer des collections Postman

Vous devez ensuite importer les collections dans Postman.

1. Sélectionnez **Collections** puis choisissez l’option d’importation :

   ![Collections](../assets/data-generator/images/collections.png)

1. Importez les collections suivantes :

   * `0-Authentication.postman_collection.json`
   * `1-Luma-Loyalty-Data.postman_collection.json`
   * `2-Luma-CRM-Data.postman_collection.json`
   * `3-Luma-Product-Catalog.postman_collection.json`
   * `4-Luma-Offline-Purchase-Events.postman_collection.json`
   * `5-Luma-Product-Inventory-Events.postman_collection.json`
   * `6-Luma-Test-Profiles.postman_collection.json`
   * `7-Luma-Web-Events.postman_collection.json`

   ![Importation des collections](../assets/data-generator/images/collection-files.png)

### Authentifier

Vous devez ensuite vous authentifier et générer un jeton d’utilisateur. N’oubliez pas que les méthodes de génération de jetons utilisées dans ce tutoriel ne conviennent qu’à une utilisation hors production. La signature locale charge une bibliothèque JavaScript à partir d’un hôte tiers et la signature à distance envoie la clé privée à un service web détenu et exploité par Adobe. Bien qu’Adobe ne stocke pas cette clé privée, les clés de production ne doivent jamais être partagées avec qui que ce soit.

1. Ouvrez la collection de `0-Authentication`, sélectionnez la requête de `OAuth: Request Access Token`, puis cliquez sur `SEND` pour vous authentifier et obtenir le jeton d’accès.

   ![Importation des collections](../assets/data-generator/images/authentication.png)

1. Passez en revue les variables d’environnement et notez que la `ACCESS_TOKEN` est maintenant renseignée.

### Importer des données

Vous pouvez maintenant préparer et importer les données dans votre sandbox Platform. Les collections Postman que vous avez importées vous chargeront de tout le travail !

1. Ouvrez la collection de `1-Luma-Loyalty-Data` et cliquez sur **Exécuter** dans l’onglet d’aperçu pour démarrer un exécuteur de collections.

   ![Importation des collections](../assets/data-generator/images/loyalty.png)

1. Dans la fenêtre de l’exécuteur de collections, veillez à sélectionner l’environnement dans la liste déroulante, à mettre à jour le **Délai** en `4000ms`, à vérifier l’option **Enregistrer les réponses** et à vérifier que l’ordre d’exécution est correct. Cliquez sur le bouton **Exécuter les données de fidélité Luma**

   ![Importation des collections](../assets/data-generator/images/loyalty-run.png)

   >[!NOTE]
   >
   >**1-Luma-Loyalty-Data** crée un schéma pour les données de fidélité des clients. Le schéma est basé sur la classe XDM Individual Profile, le groupe de champs standard, ainsi qu’un groupe de champs et un type de données personnalisés. La collection crée un jeu de données à l’aide du schéma et charge des exemples de données de fidélité des clients dans Adobe Experience Platform.

   >[!NOTE]
   >
   >Si des requêtes de collection échouent pendant l’exécution de la collection Postman, arrêtez l’exécution et exécutez les requêtes de collection une par une.

1. Si tout se passe bien, toutes les requêtes de la collection `Luma-Loyalty-Data` doivent être transmises.

   ![Résultat Fidélité](../assets/data-generator/images/loyalty-result.png)

1. Maintenant, connectons-nous à l’interface de [Adobe Experience Platform](https://platform.adobe.com/) et accédons aux jeux de données.
1. Ouvrez le jeu de données `Luma Loyalty Dataset` et, sous la fenêtre d’activité du jeu de données, vous pouvez afficher une exécution par lots réussie qui a ingéré 1 000 enregistrements. Vous pouvez également cliquer sur l’option Prévisualiser le jeu de données pour vérifier les enregistrements ingérés. Vous devrez peut-être attendre plusieurs minutes pour confirmer que 1 000 [!UICONTROL nouveaux fragments de profil] ont été créés.
   ![Jeu de données de fidélité](../assets/data-generator/images/loyalty-dataset.png)
1. Répétez les étapes 1 à 3 pour exécuter les autres collections :
   * `2-Luma-CRM-Data.postman_collection.json` crée un schéma et un jeu de données renseigné pour les données CRM des clients. Le schéma est basé sur la classe Profil individuel XDM qui comprend des détails démographiques, des détails de contact personnels, des détails de préférences et un groupe de champs d’identité personnalisée.
   * `3-Luma-Product-Catalog.postman_collection.json` crée un schéma et un jeu de données renseigné pour les informations du catalogue de produits. Le schéma est basé sur une classe de catalogue de produits personnalisée et utilise un groupe de champs de catalogue de produits personnalisé.
   * `4-Luma-Offline-Purchase-Events.postman_collection.json` crée un schéma et un jeu de données renseigné pour les données d’événement d’achat hors ligne des clients . Le schéma est basé sur la classe XDM ExperienceEvent et comprend une identité personnalisée et des groupes de champs Détails du Commerce .
   * `5-Luma-Product-Inventory-Events.postman_collection.json` crée un schéma et un jeu de données renseigné pour les événements liés aux produits en stock et en rupture de stock. Le schéma est basé sur une classe d’événement métier personnalisée et un groupe de champs personnalisés.
   * `6-Luma-Test-Profiles.postman_collection.json` crée un schéma et un jeu de données renseigné avec des profils de test à utiliser dans Adobe Journey Optimizer
   * `7-Luma-Web-Events.postman_collection.json` crée un schéma et un jeu de données rempli avec des données web historiques simples.


## Validation

Les exemples de données ont été conçus de sorte que lorsque les collections ont été exécutées, des profils clients en temps réel sont créés pour combiner des données provenant de plusieurs systèmes. Le premier enregistrement des jeux de données de fidélité, de gestion de la relation client et d’achat hors ligne en est un bon exemple. Recherchez ce profil pour confirmer que les données ont été ingérées. Dans l’interface de [Adobe Experience Platform ](https://experience.adobe.com/platform/) :

1. Accédez à **[!UICONTROL Profils]** > **[!UICONTROL Parcourir]**
1. Sélectionnez `Luma Loyalty Id` comme **[!UICONTROL Espace de noms d’identité]**
1. Recherchez `5625458` comme valeur **[!UICONTROL Identity]**
1. Ouvrir le profil de `Daniel Wright`

>[!TIP]
>
>Si le profil ne s’affiche pas, vérifiez la page [!UICONTROL Jeux de données] pour vous assurer que tous les jeux de données ont bien été créés et que les données ont bien été ingérées. Si tout semble correct, patientez quinze minutes et vérifiez si le profil est disponible dans la visionneuse.  En cas de problèmes lors de l’ingestion des données, vérifiez les messages d’erreur pour essayer de localiser le problème. Vous pouvez également essayer d’activer les diagnostics d’erreur sur la page [!UICONTROL Jeux de données] et faire glisser et déposer le fichier de données json pour réingérer les données.


![Ouverture d’un profil](../assets/data-generator/images/validation-profile-open.png)

En parcourant les données dans les onglets **[!UICONTROL Attributs]** et **[!UICONTROL Événements]**, vous devriez voir que le profil contient des données provenant des différents fichiers de données :
![Données d’événement du fichier d’événements d’achat hors ligne](../assets/data-generator/images/validation-profile-events.png)

## Étapes suivantes

Si vous souhaitez en savoir plus sur Adobe Journey Optimizer, cette sandbox contient tout ce dont vous avez besoin pour relever les [défis de Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer-learn/challenges/introduction-and-prerequisites.html?lang=fr)

Si vous souhaitez en savoir plus sur les politiques de fusion, la gouvernance des données, le service de requête et le créateur de segments, passez à la leçon [11 dans le tutoriel Prise en main pour les architectes et ingénieurs de données](https://experienceleague.adobe.com/docs/platform-learn/getting-started-for-data-architects-and-data-engineers/create-merge-policies.html?lang=fr). Les premières leçons de cet autre tutoriel vous ont permis de créer manuellement tout ce qui vient d’être renseigné par ces collections Postman, profitez d’un bon départ !

Si vous souhaitez créer un exemple d’implémentation de Web SDK à lier à ce sandbox, parcourez le
[Tutoriel sur l’implémentation de Adobe Experience Cloud avec Web SDK](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/overview.html?lang=fr). Après avoir configuré les leçons « Configuration initiale », « Configuration des balises » et « Configuration d’Experience Platform » du tutoriel Web SDK, connectez-vous au site web de Luma à l’aide des dix premières adresses e-mail du fichier `luma-crm.json` à l’aide du mot de passe `test` pour voir les fragments de profil fusionner avec les données chargées dans ce tutoriel.

Si vous souhaitez créer un exemple d’implémentation de Mobile SDK à lier à ce sandbox, parcourez le
[Tutoriel sur l’implémentation de Adobe Experience Cloud dans les applications mobiles](https://experienceleague.adobe.com/docs/platform-learn/implement-mobile-sdk/overview.html?lang=fr). Après avoir configuré les leçons « Configuration initiale », « Implémentation de l’application » et « Experience Platform » du tutoriel Web SDK, connectez-vous au site web de Luma à l’aide des premières adresses e-mail du fichier `luma-crm.json` pour voir un fragment de profil fusionner avec les données chargées dans ce tutoriel.

## Réinitialiser l’environnement Sandbox {#reset-sandbox}

La réinitialisation d’un sandbox hors production supprime toutes les ressources associées à ce sandbox (schémas, jeux de données, etc.) tout en conservant le nom et les autorisations associés du sandbox. Ce sandbox « propre » reste disponible avec le même nom auprès des utilisateurs qui y ont accès.

Suivez les étapes [ici](https://experienceleague.adobe.com/docs/experience-platform/sandbox/ui/user-guide.html?lang=fr#reset-a-sandbox) pour réinitialiser un environnement sandbox.
