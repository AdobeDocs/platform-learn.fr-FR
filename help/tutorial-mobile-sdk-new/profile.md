---
title: Profile
description: Découvrez comment collecter des données de profil dans une application mobile.
hide: true
hidefromtoc: true
source-git-commit: ca83bbb571dc10804adcac446e2dba4fda5a2f1d
workflow-type: tm+mt
source-wordcount: '582'
ht-degree: 3%

---

# Profile

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


## Définir et mettre à jour

Il serait utile pour le ciblage et/ou la personnalisation de savoir rapidement si un utilisateur a déjà effectué des achats dans l’application. Définissons-le dans l’application Luma.

1. Accédez à **[!UICONTROL ProductView]** (dans **[!UICONTROL Vues]** > **[!UICONTROL Produits]**) dans le projet de l’application Xcode Luma et recherchez l’appel à `updateUserAttributes` (dans le bouton Achats ) :

   ```swift {highlight="8-9"}
   Button {
       Task {
           if ATTrackingManager.trackingAuthorizationStatus == .authorized {
               // Send purchase commerce experience event
               MobileSDK.shared.sendCommerceExperienceEvent(commerceEventType: "purchases", product: product)
               // Update attributes
               MobileSDK.shared.updateUserAttributes(attributeName: "isPaidUser", attributeValue: "yes")
           }
       }
       showPurchaseDialog.toggle()
   } label: {
       Label("", systemImage: "creditcard")
   }
   .alert(isPresented: $showPurchaseDialog, content: {
       Alert(title: Text( "Purchases"), message: Text("The selected item is purchased…"))
   })
   ```

2. Accédez à **[!UICONTROL MobileSDK]** et recherchez la variable `updateUserAttributes` de la fonction Ajoutez le code mis en surbrillance suivant :

   ```swift {highlight="2-4"}
   func updateUserAttributes(attributeName: String, attributeValue: String) {
       var profileMap = [String: Any]()
       profileMap[attributeName] = attributeValue
       UserProfile.updateUserAttributes(attributeDict: profileMap)
   }
   ```

   Ce code :

   1. Configure un dictionnaire vide nommé `profileMap`.

   1. Ajoute un élément au dictionnaire à l’aide de `attributeName` (par exemple `isPaidUser`), et `attributeValue` (par exemple `yes`).

   1. Utilise la variable `profileMap` comme valeur du dictionnaire `attributeDict` du paramètre `UserProfile.updateUserAttributes` appel API.


Additional `updateUserAttributes` La documentation est disponible [here](https://developer.adobe.com/client-sdks/documentation/profile/api-reference/#updateuserattribute).

## Obtenir

Une fois que vous avez mis à jour l’attribut d’un utilisateur, il est disponible pour d’autres SDK Adobe, mais vous pouvez également récupérer explicitement les attributs.

1. Accédez à **[!UICONTROL HomeView]** (dans **[!UICONTROL Vues]** > **[!UICONTROL Général]**) et recherchez la variable `.onAppear` modifier. Ajoutez le code suivant :

   ```swift {highlight="3-11"}
   .onAppear {
       // Track view screen
       MobileSDK.shared.sendTrackScreenEvent(stateName: "luma: content: ios: us: en: home")
       // Get attributes
       UserProfile.getUserAttributes(attributeNames: ["isPaidUser"]) { attributes, error in
           if attributes?["isPaidUser"] as! String == "yes" {
               showBadgeForUser = true
           }
           else {
               showBadgeForUser = false
           }
       }
   }
   ```

   Ce code :

   1. Appelle le `UserProfile.getUserAttributes` la fermeture de `iPaidUser` nom d’attribut comme élément unique dans `attributeNames` tableau.
   1. Vérifie ensuite la valeur de la variable `isPaidUser` et quand `yes`, place un badge sur l’icône Personne en haut à droite.

Additional `getUserAttributes` La documentation est disponible [here](https://developer.adobe.com/client-sdks/documentation/profile/api-reference/#getuserattributes).

## Validation avec Assurance

1. Consultez la section [instructions de configuration](assurance.md) .
1. Installez l’application.
1. Lancez l’application à l’aide de l’URL générée par Assurance.
1. Exécutez l’application pour vous connecter et interagir avec un produit.

   1. Déplacez l’icône Assurance vers la gauche.
   1. Sélectionner **[!UICONTROL Accueil]** dans la barre d’onglets.
   1. Pour ouvrir la feuille de connexion, sélectionnez la **[!UICONTROL Connexion]** bouton .
   1. Pour insérer un e-mail aléatoire et un ID de client, sélectionnez la variable **[!UICONTROL A|]** bouton .
   1. Sélectionner **[!UICONTROL Connexion]**.
   1. Sélectionner **[!UICONTROL Produits]** dans la barre d’onglets.
   1. Sélectionnez un produit.
   1. Sélectionner **[!UICONTROL Enregistrer ultérieurement]**.
   1. Sélectionner **[!UICONTROL Ajouter au panier]**.
   1. Sélectionner **[!UICONTROL Achat]**.
   1. Revenir à **[!UICONTROL Accueil]** écran. Vous devriez voir un bouton de connexion mis à jour.

      <img src="./assets/mobile-app-events-1.png" width="200"> <img src="./assets/mobile-app-events-2.png" width="200"> <img src="./assets/mobile-app-events-3.png" width="200"> <img src="./assets/personbadges.png" width="200">

1. Vous devriez voir une **[!UICONTROL UserProfileUpdate]** et **[!UICONTROL getUserAttributes]** dans l’interface utilisateur d’assurance avec la mise à jour `profileMap` .
   ![valider le profil](assets/profile-validate.png)

>[!SUCCESS]
>
>Vous avez maintenant configuré votre application pour mettre à jour les attributs des profils dans le réseau Edge et (lors de la configuration) avec Adobe Experience Platform.<br/>Merci d’investir votre temps à apprendre sur le SDK Adobe Experience Platform Mobile. Si vous avez des questions, souhaitez partager des commentaires généraux ou avez des suggestions sur le contenu futur, partagez-les à ce sujet. [Article de discussion de la communauté Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796)

Suivant : **[Mappage des données à Adobe Analytics](analytics.md)**
