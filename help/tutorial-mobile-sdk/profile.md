---
title: Collecter des données de profil avec Platform Mobile SDK
description: Découvrez comment collecter des données de profil dans une application mobile.
jira: KT-14634
exl-id: 97717611-04d9-45e3-a443-ea220a13b57c
source-git-commit: 4a0fa85c76c00fd505118692ea4b6cbe410f5839
workflow-type: tm+mt
source-wordcount: '786'
ht-degree: 1%

---

# Collecter des données de profil

Découvrez comment collecter des données de profil dans une application mobile.

Vous pouvez utiliser l’extension de profil pour stocker des attributs sur votre utilisateur sur le client. Ces informations peuvent être utilisées ultérieurement pour cibler et personnaliser des messages lors de scénarios en ligne ou hors ligne, sans avoir à se connecter à un serveur pour des performances optimales.

L’extension de profil gère le profil d’opération côté client (CSOP), permet de réagir aux API, met à jour les attributs de profil utilisateur et partage les attributs de profil utilisateur avec le reste du système en tant qu’événement généré.

Les données de profil sont utilisées par d’autres extensions pour effectuer des actions liées aux profils. Exemple : l’extension du moteur de règles qui utilise les données de profil et exécute les règles en fonction des données de profil. En savoir plus sur l’extension [Profile](https://developer.adobe.com/client-sdks/documentation/profile/) dans la documentation

>[!IMPORTANT]
>
>La fonctionnalité de profil décrite dans cette leçon est distincte de la fonctionnalité de profil client en temps réel dans les applications Adobe Experience Platform et basées sur Platform.


## Conditions préalables

* Application créée et exécutée avec succès avec les SDK installés et configurés.

## Objectifs d’apprentissage

Dans cette leçon, vous allez :

* Définissez ou mettez à jour les attributs utilisateur.
* Récupérez les attributs utilisateur.


## Définition et mise à jour des attributs utilisateur

Il serait utile pour le ciblage et la personnalisation dans l’application de savoir rapidement si un utilisateur a effectué un achat dans le passé ou récemment. Configurez-le dans l’application Luma.

>[!BEGINTABS]

>[!TAB iOS]

1. Accédez à **[!DNL Luma]** > **[!DNL Luma]** > **[!DNL Utils]** > **[!DNL MobileSDK]** dans le navigateur de projet Xcode et recherchez la fonction `func updateUserAttribute(attributeName: String, attributeValue: String)`. Ajoutez le code suivant :

   ```swift
   // Create a profile map, add attributes to the map and update profile using the map
   var profileMap = [String: Any]()
   profileMap[attributeName] = attributeValue
   UserProfile.updateUserAttributes(attributeDict: profileMap)
   ```

   Ce code :

   1. Configure un dictionnaire vide nommé `profileMap`.

   1. Ajoute un élément au dictionnaire en utilisant `attributeName` (par exemple, `isPaidUser`) et `attributeValue` (par exemple, `yes`).

   1. Utilise le dictionnaire de `profileMap` comme valeur du paramètre `attributeDict` de l’appel API [`UserProfile.updateUserAttributes`](https://developer.adobe.com/client-sdks/documentation/profile/api-reference/#updateuserattributes).

1. Accédez à **[!DNL Luma]** > **[!DNL Luma]** > **[!DNL Views]** > **[!DNL Products]** > **[!DNL ProductView]** dans le navigateur de projet Xcode et recherchez l’appel à `updateUserAttributes` (dans le code du bouton Achats ![Carte de crédit](/help/assets/icons/CreditCard.svg)). Ajoutez le code suivant :

   ```swift
   // Update attributes
   MobileSDK.shared.updateUserAttribute(attributeName: "isPaidUser", attributeValue: "yes")
   ```

>[!TAB Android]

1. Accédez à **[!UICONTROL Android]** ![ChevronDown](/help/assets/icons/ChevronDown.svg) > **[!DNL app]** > **[!DNL kotlin+java]** > **[!DNL com.adobe.luma.tutorial.android]** > **[!UICONTROL models]** > **[!UICONTROL MobileSDK]** dans le navigateur d’Android Studio et recherchez la fonction `func updateUserAttribute(attributeName: String, attributeValue: String)`. Ajoutez le code suivant :

   ```kotlin
   // Create a profile map, add attributes to the map and update profile using the map
   val profileMap = mapOf(attributeName to attributeValue)
   UserProfile.updateUserAttributes(profileMap)
   ```

   Ce code :

   1. Configure un mappage vide nommé `profileMap`.

   1. Ajoute un élément au mappage à l’aide des `attributeName` (par exemple, `isPaidUser`) et `attributeValue` (par exemple, `yes`).

   1. Utilise le mappage `profileMap` comme valeur du paramètre `attributeDict` de l’appel API [`UserProfile.updateUserAttributes`](https://developer.adobe.com/client-sdks/documentation/profile/api-reference/#updateuserattributes).

1. Accédez à **[!UICONTROL Android]** ![ChevronDown](/help/assets/icons/ChevronDown.svg) > **[!DNL app]** > **[!DNL kotlin+java]** > **[!DNL com.adobe.luma.tutorial.android]** > **[!UICONTROL views]** > **[!UICONTROL ProductView.kt]** et recherchez l’appel à `updateUserAttributes` (dans le code du bouton Achats ![Carte de crédit](/help/assets/icons/CreditCard.svg)). Ajoutez le code suivant :

   ```kotlin
   // Update attributes
   MobileSDK.shared.updateUserAttribute("isPaidUser", "yes")
   ```

>[!ENDTABS]

## Obtenir les attributs utilisateur

Une fois que vous avez mis à jour l’attribut d’un utilisateur, il est disponible pour d’autres SDK Adobe, mais vous pouvez également récupérer les attributs explicitement, pour permettre à votre application de se comporter comme vous le souhaitez.

>[!BEGINTABS]

>[!TAB iOS]

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

   1. Appelle l’API [`UserProfile.getUserAttributes`](https://developer.adobe.com/client-sdks/documentation/profile/api-reference/#getuserattributes) avec le nom d’attribut `isPaidUser` comme élément unique dans le tableau `attributeNames` .
   1. Recherche ensuite la valeur de l’attribut `isPaidUser` et, lorsqu’il est `yes`, place un badge sur l’icône ![UserCheckedOut](/help/assets/icons/UserCheckedOut.svg) dans la barre d’outils supérieure droite.

>[!TAB Android]

1. Accédez à **[!UICONTROL Android]** ![ChevronDown](/help/assets/icons/ChevronDown.svg) > **[!DNL app]** > **[!DNL kotlin+java]** > **[!DNL com.adobe.luma.tutorial.androi]** > **[!DNL views]** > **[!DNL HomeView.kt]** dans le navigateur de projet Android Studio et recherchez le modificateur `.onAppear`. Ajoutez le code suivant :

   ```kotlin
   // Get attributes
   UserProfile.getUserAttributes(listOf("isPaidUser")) { attributes ->
       showBadgeForUser = attributes?.get("isPaidUser") == "yes"
   }
   ```

   Ce code :

   1. Appelle l’API [`UserProfile.getUserAttributes`](https://developer.adobe.com/client-sdks/documentation/profile/api-reference/#getuserattributes) avec le nom d’attribut `isPaidUser` comme élément unique dans le tableau `attributeNames` .
   1. Recherche ensuite la valeur de l’attribut `isPaidUser`. Lorsqu’il est `yes`, le code remplace l’icône de personne par une icône de badge dans la barre d’outils supérieure droite.

>[!ENDTABS]

Pour plus d’informations, consultez la [référence de l’API](https://developer.adobe.com/client-sdks/documentation/profile/api-reference/#getuserattributes).

## Valider avec Assurance

1. Consultez la section [instructions de configuration](assurance.md#connecting-to-a-session) pour connecter votre simulateur ou votre appareil à Assurance.
1. Exécutez l’application pour vous connecter et interagir avec un produit.

>[!BEGINTABS]

>[!TAB iOS]

1. Sélectionnez **[!UICONTROL Accueil]** dans la barre d’onglets.
1. Déplacez l’icône Assurance vers la gauche.
1. Pour ouvrir la feuille de connexion, sélectionnez le bouton ![Utilisateur](/help/assets/icons/User.svg).

   <img src="./assets/mobile-app-events-1.png" width="300">

1. Pour insérer un e-mail et un identifiant client aléatoires, sélectionnez le bouton > .
1. Sélectionnez **[!UICONTROL Connexion]**.

   <img src="./assets/mobile-app-events-2.png" width="300">

1. Sélectionnez **[!DNL Products]** dans la barre d’onglets.
1. Sélectionnez un produit.
1. Sélectionnez ![ Cœur ](/help/assets/icons/Heart.svg).
1. Sélectionnez ![Panier](/help/assets/icons/ShoppingCart.svg).
1. Sélectionnez ![ Carte de crédit ](/help/assets/icons/CreditCard.svg).

   <img src="./assets/mobile-app-events-3.png" width="300">

1. Revenez à l’écran **[!UICONTROL Accueil]**. Vous devriez constater qu’un badge a été ajouté ![UserCheckedOut](/help/assets/icons/UserCheckedOut.svg).

   <img src="./assets/personbadges.png" width="300">


>[!TAB Android]

1. Sélectionnez **[!UICONTROL Accueil]** dans la barre d’onglets.
1. Déplacez l’icône Assurance vers la gauche.
1. Pour ouvrir la feuille de connexion, sélectionnez le bouton ![Utilisateur](/help/assets/icons/User.svg).

   <img src="./assets/mobile-app-events-1-android.png" width="300">

1. Pour insérer un e-mail aléatoire et un ID de client, sélectionnez **[!UICONTROL Générer un e-mail aléatoire]** .
1. Sélectionnez **[!UICONTROL Connexion]**.

   <img src="./assets/mobile-app-events-2-android.png" width="300">

1. Sélectionnez **[!DNL Products]** dans la barre d’onglets.
1. Sélectionnez un produit.
1. Sélectionnez ![Pouce levé](/help/assets/icons/ThumbUp.svg)
1. Sélectionnez ![Panier](/help/assets/icons/ShoppingCart.svg).
1. Sélectionnez ![ Carte de crédit ](/help/assets/icons/CreditCard.svg).

   <img src="./assets/mobile-app-events-3-android.png" width="300">

1. Revenez à l’écran **[!UICONTROL Accueil]**. Vous devriez voir que l’icône de personne est mise à jour.

   <img src="./assets/personbadges-android.png" width="300">

>[!ENDTABS]


Dans l’interface utilisateur d’Assurance, vous devriez voir un événement **[!UICONTROL UserProfileUpdate]** et **[!UICONTROL getUserAttributes]** avec la valeur de `profileMap` mise à jour.

![valider le profil](assets/profile-validate.png){zoomable="yes"}

>[!SUCCESS]
>
>Vous avez maintenant configuré votre application pour mettre à jour les attributs des profils dans Edge Network et (lorsqu’elle est configurée) avec Adobe Experience Platform.
>
>Merci d’avoir consacré votre temps à découvrir Adobe Experience Platform Mobile SDK. Si vous avez des questions, souhaitez partager des commentaires généraux ou des suggestions sur le contenu futur, partagez-les dans ce [article de discussion de la communauté Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796).

Suivant : **[Utiliser des endroits](places.md)**
