---
title: Profile
description: Découvrez comment collecter des données de profil dans une application mobile.
exl-id: 97717611-04d9-45e3-a443-ea220a13b57c
source-git-commit: cf0193e3aae4d6536c868f078f4773ee14e90408
workflow-type: tm+mt
source-wordcount: '441'
ht-degree: 2%

---

# Profile

Découvrez comment collecter des données de profil dans une application mobile.

Vous pouvez utiliser l’extension Profile pour stocker les attributs de votre utilisateur sur le client. Ces informations peuvent être utilisées ultérieurement pour cibler et personnaliser les messages lors de scénarios en ligne ou hors ligne, sans avoir à se connecter à un serveur pour des performances optimales. L’extension Profile gère le profil d’opération côté client (CSOP), permet de réagir aux API, de mettre à jour les attributs de profil utilisateur et de partager les attributs de profil utilisateur avec le reste du système en tant qu’événement généré.

Les données de profil sont utilisées par d’autres extensions pour effectuer des actions liées au profil. Par exemple, l’extension Rules Engine qui consomme les données de profil et exécute des règles basées sur les données de profil. En savoir plus sur les [Extension de profil](https://aep-sdks.gitbook.io/docs/foundation-extensions/profile) dans la documentation

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

1. Accédez à `Cart.swift`

1. Ajoutez le code ci-dessous à la variable `processOrder() `fonction .

   ```swift
   var profileMap = [String: Any]()
   profileMap["isPaidUser"] = "yes"
   UserProfile.updateUserAttributes(attributeDict: profileMap)
   ```

L’équipe de personnalisation peut également souhaiter effectuer un ciblage en fonction du niveau de fidélité de l’utilisateur. Définissons-le dans l’application Luma.

1. Accédez à `Account.swift`

1. Ajoutez le code ci-dessous à la variable `showUserInfo()` fonction .

   ```swift
   var profileMap = [String: Any]()
   profileMap["loyaltyLevel"] = loyaltyLevel
   UserProfile.updateUserAttributes(attributeDict: profileMap)
   ```

Additional `updateUserAttributes` documentation disponible [here](https://aep-sdks.gitbook.io/docs/foundation-extensions/profile/profile-api-references#update-user-attributes).

## Obtenir

Une fois que vous avez mis à jour l’attribut d’un utilisateur, il sera disponible pour d’autres SDK Adobe, mais vous pouvez également récupérer explicitement les attributs.

```swift
UserProfile.getUserAttributes(attributeNames: ["isPaidUser","loyaltyLevel"]){
    attributes, error in
    print("Profile: getUserAttributes: ",attributes as Any)
}
```

Additional `getUserAttributes` documentation disponible [here](https://aep-sdks.gitbook.io/docs/foundation-extensions/profile/profile-api-references#get-user-attributes).

## Validation avec Assurance

1. Consultez la section [instructions de configuration](assurance.md) .
1. Installez l’application.
1. Lancez l’application à l’aide de l’URL générée par Assurance.
1. Cliquez sur l’icône Compte , puis sélectionnez Connexion. Remarque : vous n&#39;avez pas d&#39;informations d&#39;identification.
1. Fermez les menus de connexion, puis sélectionnez à nouveau l’icône Compte . Vous accédez alors à l’écran des détails du compte où `loyaltyLevel` est définie.
1. Vous devriez voir une **[!UICONTROL UserProfileUpdate]** dans l’interface utilisateur d’assurance avec la mise à jour `profileMap` .
   ![valider le profil](assets/mobile-profile-validate.png)

Suivant : **[Mappage des données à Adobe Analytics](analytics.md)**

>[!NOTE]
>
>Merci d’avoir consacré votre temps à l’apprentissage du SDK Adobe Experience Platform Mobile. Si vous avez des questions, souhaitez partager des commentaires généraux ou avez des suggestions sur le contenu futur, partagez-les à ce sujet. [Article de discussion de la communauté Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796)