---
title: Collecte de données de profil avec le SDK Platform Mobile
description: Découvrez comment collecter des données de profil dans une application mobile.
jira: KT-14634
exl-id: 97717611-04d9-45e3-a443-ea220a13b57c
source-git-commit: 25f0df2ea09bb7383f45a698e75bd31be7541754
workflow-type: tm+mt
source-wordcount: '573'
ht-degree: 1%

---

# Collecte des données de profil

Découvrez comment collecter des données de profil dans une application mobile.

Vous pouvez utiliser l’extension Profile pour stocker les attributs de votre utilisateur sur le client. Ces informations peuvent être utilisées ultérieurement pour cibler et personnaliser les messages lors de scénarios en ligne ou hors ligne, sans avoir à se connecter à un serveur pour des performances optimales. L’extension Profile gère le profil d’opération côté client (CSOP), permet de réagir aux API, de mettre à jour les attributs de profil utilisateur et de partager les attributs de profil utilisateur avec le reste du système en tant qu’événement généré.

Les données de profil sont utilisées par d’autres extensions pour effectuer des actions liées au profil. Par exemple, l’extension Rules Engine qui consomme les données de profil et exécute des règles basées sur les données de profil. Pour en savoir plus sur l’ [extension de profil](https://developer.adobe.com/client-sdks/documentation/profile/) dans la documentation

>[!IMPORTANT]
>
>La fonctionnalité de profil décrite dans cette leçon est différente de la fonctionnalité de profil client en temps réel dans les applications Adobe Experience Platform et basées sur Platform.


## Conditions préalables

* Création et exécution de l’application avec les SDK installés et configurés.

## Objectifs d&#39;apprentissage

Dans cette leçon, vous allez :

* Définir ou mettre à jour des attributs utilisateur.
* Récupérez les attributs utilisateur.


## Définition et mise à jour des attributs utilisateur

Il serait utile pour le ciblage et/ou la personnalisation dans l’application de savoir rapidement si un utilisateur a effectué un achat dans le passé ou récemment. Définissons-le dans l’application Luma.

1. Accédez à **[!DNL Luma]** > **[!DNL Luma]** > **[!DNL Utils]** > **[!DNL MobileSDK]** dans le navigateur de projet Xcode et recherchez la fonction `func updateUserAttribute(attributeName: String, attributeValue: String)` . Ajoutez le code suivant :

   ```swift
   // Create a profile map, add attributes to the map and update profile using the map
   var profileMap = [String: Any]()
   profileMap[attributeName] = attributeValue
   UserProfile.updateUserAttributes(attributeDict: profileMap)
   ```

   Ce code :

   1. Configure un dictionnaire vide nommé `profileMap`.

   1. Ajoute un élément au dictionnaire en utilisant `attributeName` (par exemple `isPaidUser`) et `attributeValue` (par exemple `yes`).

   1. Utilise le dictionnaire `profileMap` comme valeur du paramètre `attributeDict` de l’appel API [`UserProfile.updateUserAttributes`](https://developer.adobe.com/client-sdks/documentation/profile/api-reference/#updateuserattributes).

1. Accédez à **[!DNL Luma]** > **[!DNL Luma]** > **[!DNL Views]** > **[!DNL Products]** > **[!DNL ProductView]** dans le navigateur de projet Xcode et recherchez l’appel à `updateUserAttributes` (dans le code pour les achats). bouton <img src="assets/purchase.png" width="15" />). Ajoutez le code suivant :

   ```swift
   // Update attributes
   MobileSDK.shared.updateUserAttribute(attributeName: "isPaidUser", attributeValue: "yes")
   ```


## Obtention des attributs utilisateur

Une fois que vous avez mis à jour l’attribut d’un utilisateur, il est disponible pour d’autres SDK d’Adobe, mais vous pouvez également récupérer explicitement les attributs pour permettre à votre application de se comporter comme vous le souhaitez.

1. Accédez à **[!DNL Luma]** > **[!DNL Luma]** > **[!DNL Views]** > **[!DNL General]** > **[!DNL HomeView]** dans le navigateur de projet Xcode et recherchez le modificateur `.onAppear`. Ajoutez le code suivant :

   ```swift
   // Get attributes
   UserProfile.getUserAttributes(attributeNames: ["isPaidUser"]) { attributes, error in
       if attributes?.count ?? 0 > 0 {
           if attributes?["isPaidUser"] as? String == "yes" {
               showBadgeForUser = true
           }
           else {
               showBadgeForUser = false
           }
       }
   }
   ```

   Ce code :

   1. Appelle l’API [`UserProfile.getUserAttributes`](https://developer.adobe.com/client-sdks/documentation/profile/api-reference/#getuserattributes) avec le nom d’attribut `isPaidUser` comme élément unique dans le tableau `attributeNames`.
   1. Ensuite, vérifie la valeur de l’attribut `isPaidUser` et, lorsque `yes`, place un badge sur l’attribut icône <img src="assets/paiduser.png" width="20" /> dans la barre d’outils en haut à droite.

Vous trouverez plus de documentation [ici](https://developer.adobe.com/client-sdks/documentation/profile/api-reference/#getuserattributes).

## Valider avec Assurance

1. Consultez la section [instructions de configuration](assurance.md#connecting-to-a-session) pour connecter votre simulateur ou périphérique à Assurance.
1. Exécutez l’application pour vous connecter et interagir avec un produit.

   1. Déplacez l’icône Assurance vers la gauche.
   1. Sélectionnez **[!UICONTROL Home]** dans la barre d’onglets.
   1. Pour ouvrir la feuille de connexion, sélectionnez la Bouton <img src="assets/login.png" width="15" />.

      <img src="./assets/mobile-app-events-1.png" width="300">

   1. Pour insérer un e-mail aléatoire et un ID de client, sélectionnez la variable Bouton <img src="assets/insert.png" width="15" /> .
   1. Sélectionnez **[!UICONTROL Login]**.

      <img src="./assets/mobile-app-events-2.png" width="300">

   1. Sélectionnez **[!DNL Products]** dans la barre d’onglets.
   1. Sélectionnez un produit.
   1. Sélectionner <img src="assets/saveforlater.png" width="15" />.
   1. Sélectionner <img src="assets/addtocart.png" width="20" />.
   1. Sélectionner <img src="assets/purchase.png" width="15" />.

      <img src="./assets/mobile-app-events-3.png" width="300">

   1. Revenez à l’écran **[!UICONTROL Home]** . Vous devriez constater qu’un badge a été ajouté. <img src="assets/person-badge-icon.png" width="15" />.

      <img src="./assets/personbadges.png" width="300">



1. Dans l’interface utilisateur d’Assurance, vous devriez voir des événements **[!UICONTROL UserProfileUpdate]** et **[!UICONTROL getUserAttributes]** avec la valeur `profileMap` mise à jour.
   ![valider le profil](assets/profile-validate.png)

>[!SUCCESS]
>
>Vous avez maintenant configuré votre application pour mettre à jour les attributs des profils dans l’Edge Network et (lors de la configuration) avec Adobe Experience Platform.
>
>Merci d’investir votre temps à apprendre sur le SDK Adobe Experience Platform Mobile. Si vous avez des questions, souhaitez partager des commentaires généraux ou avez des suggestions sur le contenu à venir, partagez-les sur cet [post de discussion de la communauté Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796).

Suivant : **[Utiliser des espaces](places.md)**
