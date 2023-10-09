---
title: Collecte des données de profil
description: Découvrez comment collecter des données de profil dans une application mobile.
hide: true
exl-id: 6ce02ccc-6280-4a1f-a96e-1975f8a0220a
source-git-commit: d7410a19e142d233a6c6597de92f112b961f5ad6
workflow-type: tm+mt
source-wordcount: '597'
ht-degree: 4%

---

# Collecte des données de profil

Découvrez comment collecter des données de profil dans une application mobile.

Vous pouvez utiliser l’extension Profile pour stocker les attributs de votre utilisateur sur le client. Ces informations peuvent être utilisées ultérieurement pour cibler et personnaliser les messages lors de scénarios en ligne ou hors ligne, sans avoir à se connecter à un serveur pour des performances optimales. L’extension Profile gère le profil d’opération côté client (CSOP), permet de réagir aux API, de mettre à jour les attributs de profil utilisateur et de partager les attributs de profil utilisateur avec le reste du système en tant qu’événement généré.

Les données de profil sont utilisées par d’autres extensions pour effectuer des actions liées au profil. Par exemple, l’extension Rules Engine qui consomme les données de profil et exécute des règles basées sur les données de profil. En savoir plus sur les [Extension de profil](https://developer.adobe.com/client-sdks/documentation/profile/) dans la documentation

>[!IMPORTANT]
>
>La fonctionnalité de profil décrite dans cette leçon est différente de la fonctionnalité de profil client en temps réel dans les applications Adobe Experience Platform et basées sur Platform.


## Conditions préalables

* Création et exécution de l’application avec les SDK installés et configurés.
* Importation du SDK Profile.

  ```swift
  import AEPUserProfile
  ```

## Objectifs d&#39;apprentissage

Dans cette leçon, vous allez :

* Définir ou mettre à jour des attributs utilisateur.
* Récupérez les attributs utilisateur.


## Définition et mise à jour des attributs utilisateur

Il serait utile pour le ciblage et/ou la personnalisation dans l’application de savoir rapidement si un utilisateur a effectué un achat dans le passé ou récemment. Définissons-le dans l’application Luma.

1. Accédez à **[!DNL Luma]** > **[!DNL Luma]** > **[!DNL Utils]** >  **[!DNL MobileSDK]** dans le navigateur de projet Xcode et recherchez le `func updateUserAttribute(attributeName: String, attributeValue: String)` de la fonction Ajoutez le code suivant :

   ```swift
   // Create a profile map, add attributes to the map and update profile using the map
   var profileMap = [String: Any]()
   profileMap[attributeName] = attributeValue
   UserProfile.updateUserAttributes(attributeDict: profileMap)
   ```

   Ce code :

   1. Configure un dictionnaire vide nommé `profileMap`.

   1. Ajoute un élément au dictionnaire à l’aide de `attributeName` (par exemple `isPaidUser`), et `attributeValue` (par exemple `yes`).

   1. Utilise la variable `profileMap` comme valeur du dictionnaire `attributeDict` du paramètre [`UserProfile.updateUserAttributes`](https://developer.adobe.com/client-sdks/documentation/profile/api-reference/#updateuserattributes) appel API.

1. Accédez à **[!DNL Luma]** > **[!DNL Luma]** > **[!DNL Views]** > **[!DNL Products]** > **[!DNL ProductView]** dans le navigateur de projet Xcode et recherchez l’appel à `updateUserAttributes` (dans le code des Achats ; <img src="assets/purchase.png" width="15" /> button). Ajoutez le code suivant :

   ```swift
   // Update attributes
   MobileSDK.shared.updateUserAttribute(attributeName: "isPaidUser", attributeValue: "yes")
   ```


## Obtention des attributs utilisateur

Une fois que vous avez mis à jour l’attribut d’un utilisateur, il est disponible pour d’autres SDK d’Adobe, mais vous pouvez également récupérer explicitement les attributs pour permettre à votre application de se comporter comme vous le souhaitez.

1. Accédez à **[!DNL Luma]** > **[!DNL Luma]** > **[!DNL Views]** > **[!DNL General]** > **[!DNL HomeView]** dans le navigateur de projet Xcode et recherchez le `.onAppear` modifier. Ajoutez le code suivant :

   ```swift
   // Get attributes
   UserProfile.getUserAttributes(attributeNames: ["isPaidUser"]) { attributes, error in
       if attributes?["isPaidUser"] as! String == "yes" {
           showBadgeForUser = true
       }
       else {
           showBadgeForUser = false
       }
   }
   ```

   Ce code :

   1. Appelle le [`UserProfile.getUserAttributes`](https://developer.adobe.com/client-sdks/documentation/profile/api-reference/#getuserattributes) avec l’API `iPaidUser` nom d’attribut comme élément unique dans `attributeNames` tableau.
   1. Vérifie ensuite la valeur de la variable `isPaidUser` et quand `yes`, place un badge sur l’objet <img src="assets/paiduser.png" width="20" /> dans la barre d’outils supérieure droite.

Vous trouverez de la documentation supplémentaire [here](https://developer.adobe.com/client-sdks/documentation/profile/api-reference/#getuserattributes).

## Validation avec Assurance

1. Consultez la section [instructions de configuration](assurance.md#connecting-to-a-session) pour connecter le simulateur ou l’appareil à Assurance.
1. Exécutez l’application pour vous connecter et interagir avec un produit.

   1. Déplacez l’icône Assurance vers la gauche.
   1. Sélectionner **[!UICONTROL Accueil]** dans la barre d’onglets.
   1. Pour ouvrir la feuille de connexion, sélectionnez la <img src="assets/login.png" width="15" /> button.

      <img src="./assets/mobile-app-events-1.png" width="300">

   1. Pour insérer un e-mail aléatoire et un ID de client, sélectionnez la variable <img src="assets/insert.png" width="15" /> button .
   1. Sélectionner **[!UICONTROL Connexion]**.

      <img src="./assets/mobile-app-events-2.png" width="300">

   1. Sélectionner **[!DNL Products]** dans la barre d’onglets.
   1. Sélectionnez un produit.
   1. Sélectionner <img src="assets/saveforlater.png" width="15" />.
   1. Sélectionner <img src="assets/addtocart.png" width="20" />.
   1. Sélectionner <img src="assets/purchase.png" width="15" />.

      <img src="./assets/mobile-app-events-3.png" width="300">

   1. Revenir à **[!UICONTROL Accueil]** écran. Vous devriez voir un badge ajouté <img src="assets/person-badge-icon.png" width="15" />.

      <img src="./assets/personbadges.png" width="300">



1. Dans l’interface utilisateur d’Assurance, une **[!UICONTROL UserProfileUpdate]** et **[!UICONTROL getUserAttributes]** avec les événements mis à jour `profileMap` .
   ![valider le profil](assets/profile-validate.png)

>[!SUCCESS]
>
>Vous avez maintenant configuré votre application pour mettre à jour les attributs des profils dans le réseau Edge et (lors de la configuration) avec Adobe Experience Platform.<br/>Merci d’investir votre temps à apprendre sur le SDK Adobe Experience Platform Mobile. Si vous avez des questions, souhaitez partager des commentaires généraux ou avez des suggestions sur le contenu futur, partagez-les à ce sujet. [Article de discussion de la communauté Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796).

Suivant : **[Utiliser des emplacements](places.md)**
