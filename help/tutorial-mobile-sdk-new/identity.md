---
title: Identité
description: Découvrez comment collecter des données d’identité dans une application mobile.
feature: Mobile SDK,Identities
hide: true
hidefromtoc: true
source-git-commit: ca83bbb571dc10804adcac446e2dba4fda5a2f1d
workflow-type: tm+mt
source-wordcount: '626'
ht-degree: 6%

---

# Identité

Découvrez comment collecter des données d’identité dans une application mobile.

Adobe Experience Platform Identity Service vous permet de mieux connaître vos clients et leurs comportements en rapprochant des identités entre appareils et systèmes, ce qui vous permet de proposer des expériences numériques personnelles et percutantes en temps réel. Les champs d’identité et les espaces de noms sont la colle qui relie différentes sources de données pour créer le profil client en temps réel à 360 degrés.

En savoir plus sur les [Extension Identity](https://developer.adobe.com/client-sdks/documentation/identity-for-edge-network/) et la variable [service d’identité](https://experienceleague.adobe.com/docs/experience-platform/identity/home.html?lang=fr) dans la documentation.

## Conditions préalables

* Création et exécution de l’application avec les SDK installés et configurés.

## Objectifs d&#39;apprentissage

Dans cette leçon, vous allez :

* Configurez un espace de noms d’identité personnalisé.
* Mise à jour des identités.
* Validez le graphique d’identités.
* Obtenez l’ECID et d’autres identités.


## Configuration d’un espace de noms d’identité personnalisé

Les espaces de noms d’identité sont des composants de [Identity Service](https://experienceleague.adobe.com/docs/experience-platform/identity/home.html?lang=fr) qui servent d’indicateurs du contexte auquel une identité se rapporte. Par exemple, ils distinguent une valeur `name@email.com` comme adresse e-mail ou `443522` comme identifiant CRM numérique.

1. Dans l’interface Collecte de données, sélectionnez **[!UICONTROL Identités]** à partir du rail de navigation de gauche.
1. Sélectionnez **[!UICONTROL Créer un espace de noms d’identité]**.
1. Fournissez une **[!UICONTROL Nom d’affichage]** de `Luma CRM ID` et un **[!UICONTROL Symbole d’identité]** valeur de `lumaCRMId`.
1. Sélectionner **[!UICONTROL Identifiant multi-appareils]**.
1. Sélectionnez **[!UICONTROL Créer]**.

   ![créer un espace de noms d’identité](assets/identity-create.png)




## Mise à jour des identités

Vous souhaitez mettre à jour l’identité standard (e-mail) et l’identité personnalisée (identifiant Luma CRM) lorsque l’utilisateur se connecte à l’application.

1. Accédez à **[!UICONTROL LoginSheet]** (dans **[!UICONTROL Vues]** > **[!UICONTROL Général]**) dans le projet de l’application Xcode Luma et recherchez l’appel à `updateIdentities`:

   ```swift {highlight="3,4"}
   Button("Login") {
       // call updaeIdentities
       MobileSDK.shared.updateIdentities(emailAddress: currentEmailId, crmId: currentCRMId)
   
       // Send app interaction event
       MobileSDK.shared.sendAppInteractionEvent(actionName: "login")
       dismiss()
   }
   .disabled(currentEmailId.isValidEmail == false)
   .buttonStyle(.bordered)
   ```

1. Accédez au `updateIdentities` implémentation des fonctions dans **[!UICONTROL MobileSDK]** (dans **[!UICONTROL Utils]**) dans le projet de l’application Xcode Luma. Ajoutez le code en surbrillance suivant à la fonction .

   ```swift {highlight="2-12"}
   func updateIdentities(emailAddress: String, crmId: String) {
       let identityMap: IdentityMap = IdentityMap()
       // Add identity items
       let emailIdentity = IdentityItem(id: emailAddress, authenticatedState: AuthenticatedState.authenticated)
       let crmIdentity = IdentityItem(id: crmId, authenticatedState: AuthenticatedState.authenticated)
       identityMap.add(item:emailIdentity, withNamespace: "Email")
       identityMap.add(item: crmIdentity, withNamespace: "lumaCRMId")
   
       // Update identities
       Identity.updateIdentities(with: identityMap)
   }
   ```

   Ce code :

   1. Crée une `IdentityMap` .

      ```swift
      let identityMap: IdentityMap = IdentityMap()
      ```

   1. Configuration `IdentityItem` pour l’e-mail et l’identifiant CRM.

      ```swift
      let emailIdentity = IdentityItem(id: emailAddress, authenticatedState: AuthenticatedState.authenticated)
      let crmIdentity = IdentityItem(id: crmId, authenticatedState: AuthenticatedState.authenticated)
      ```

   1. Ajoute ces `IdentityItem` aux objets `IdentityMap` .

      ```swift
      identityMap.add(item:emailIdentity, withNamespace: "Email")
      identityMap.add(item: crmIdentity, withNamespace: "lumaCRMId")
      ```

   1. Envoie le `IdentityItem` dans le cadre de l’objet `Identity.updateIdentities` Appel API au réseau Edge.

      ```swift
      Identity.updateIdentities(with: identityMap) 
      ```


>[!NOTE]
>
>Vous pouvez envoyer plusieurs identités en une seule `updateIdentities` appelez . Vous pouvez également modifier les identités envoyées précédemment.


## Suppression d’une identité

Vous pouvez utiliser `removeIdentity` pour supprimer l’identité de la carte d’identité côté client stockée. L’extension Identity cesse d’envoyer l’identifiant au réseau Edge. L’utilisation de cette API ne supprime pas l’identifiant du graphique de profil utilisateur ou d’identité côté serveur.

1. Accédez à **[!UICONTROL LoginSheet]** (dans **[!UICONTROL Vues]** > **[!UICONTROL Général]**) dans le projet de l’application Xcode Luma et recherchez l’appel à `removeIdentities`:

   ```swift {highlight="3"}
   Button("Logout", role: .destructive) {
       // call removeIdentities
       MobileSDK.shared.removeIdentities(emailAddress: currentEmailId, crmId: currentCRMId)
       dismiss()                   
   }
   .buttonStyle(.bordered)
   ```

1. Ajoutez le code suivant au `removeIdentities` fonction dans `MobileSDK`:

   ```swift {highlight="2-8"}
   func removeIdentities(emailAddress: String, crmId: String) {
       Identity.removeIdentity(item: IdentityItem(id: emailAddress), withNamespace: "Email")
       Identity.removeIdentity(item: IdentityItem(id: crmId), withNamespace: "lumaCRMId")
       // reset email and CRM Id to their defaults
       currentEmailId = "testUser@gmail.com"
       currentCRMId = "112ca06ed53d3db37e4cea49cc45b71e"
   }
   ```


## Validation avec Assurance

1. Consultez la section [instructions de configuration](assurance.md) et connectez votre simulateur ou votre appareil à Assurance.
1. Dans l’application Luma
   1. Sélectionnez la variable **[!UICONTROL Accueil]** .
   1. Sélectionnez la variable **[!UICONTROL Connexion]** en haut à droite.
   1. fournir une adresse électronique et un identifiant CRM ; ou
   1. Sélectionnez A| pour générer de manière aléatoire une **[!UICONTROL Email]** et **[!UICONTROL Identifiant CRM]**.
   1. Sélectionner **[!UICONTROL Connexion]**.

      <img src="./assets/identity1.png" width="300"> <img src="./assets/identity2.png" width="300">


1. Recherchez dans l’interface utilisateur web d’assurance le **[!UICONTROL Identités de mise à jour d’identité Edge]**de la variable **[!UICONTROL com.adobe.griffon.mobile]** fournisseur.
1. Sélectionnez l’événement et passez en revue les données de la variable **[!UICONTROL ACPExtensionEventData]** . Vous devriez voir les identités que vous avez mises à jour.
   ![mise à jour des identités de validation](assets/identity-validate-assurance.png)

## Validation avec le graphique d’identités

Une fois que vous avez terminé les étapes de la section [leçon Experience Platform](platform.md), vous pouvez confirmer la capture d’identité dans la visionneuse de graphiques d’identités de Platform :

1. Sélectionner **[!UICONTROL Identités]** dans l’interface utilisateur de la collecte de données.
1. Sélectionner **[!UICONTROL Graphique d’identités]** dans la barre supérieure.
1. Entrée `Luma CRM ID` comme la propriété **[!UICONTROL Espace de noms d’identité]** et votre identifiant CRM (par exemple, `24e620e255734d8489820e74f357b5c8`) en tant que **[!UICONTROL Valeur d’identité]**.
1. Vous voyez le **[!UICONTROL Identités]** répertorié.

   ![validation du graphique d’identités](assets/identity-validate-graph.png)


>[!SUCCESS]
>
>Vous avez maintenant configuré votre application pour mettre à jour les identités dans le réseau Edge et (lors de la configuration) avec Adobe Experience Platform.<br/>Merci d’investir votre temps à apprendre sur le SDK Adobe Experience Platform Mobile. Si vous avez des questions, souhaitez partager des commentaires généraux ou avez des suggestions sur le contenu futur, partagez-les à ce sujet. [Article de discussion de la communauté Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796)

Suivant : **[Profil](profile.md)**
