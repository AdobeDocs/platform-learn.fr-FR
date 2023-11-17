---
title: Collecte de données d’identité
description: Découvrez comment collecter des données d’identité dans une application mobile.
feature: Mobile SDK,Identities
hide: true
exl-id: e6ec9a4f-3163-47fd-8d5c-6e640af3b4ba
source-git-commit: 4a12f8261cf1fb071bc70b6a04c34f6c16bcce64
workflow-type: tm+mt
source-wordcount: '856'
ht-degree: 5%

---

# Collecte de données d’identité

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

>[!NOTE]
>
>Le SDK Mobile génère une identité unique dans son propre espace de noms, appelé ID Experience Cloud (ECID) lorsque l’application est installée. Cet ECID est stocké en mémoire persistante sur l’appareil mobile et est envoyé avec chaque accès. L’ECID est supprimé lorsque l’utilisateur désinstalle l’application ou lorsque l’utilisateur définit l’état de confidentialité global du SDK Mobile sur exclusion. Dans l’exemple d’application Luma, vous devez supprimer et réinstaller l’application pour créer un nouveau profil avec son propre ECID unique.


Pour créer un espace de noms d’identité, procédez comme suit :

1. Dans l’interface Collecte de données, sélectionnez **[!UICONTROL Identités]** à partir du rail de navigation de gauche.
1. Sélectionnez **[!UICONTROL Créer un espace de noms d’identité]**.
1. Fournissez une **[!UICONTROL Nom d’affichage]** de `Luma CRM ID` et un **[!UICONTROL Symbole d’identité]** valeur de `lumaCRMId`.
1. Sélectionner **[!UICONTROL Identifiant multi-appareils]**.
1. Sélectionnez **[!UICONTROL Créer]**.

   ![créer un espace de noms d’identité](assets/identity-create.png)




## Mise à jour des identités

Vous souhaitez mettre à jour l’identité standard (e-mail) et l’identité personnalisée (identifiant Luma CRM) lorsque l’utilisateur se connecte à l’application.

1. Accédez à **[!DNL Luma]** > **[!DNL Luma]** > **[!DNL Utils]** > **[!UICONTROL MobileSDK]** dans le navigateur de projet Xcode et recherchez le `func updateIdentities(emailAddress: String, crmId: String)` implémentation de la fonction . Ajoutez le code suivant à la fonction .

   ```swift
   // Set up identity map, add identities to map and update identities
   let identityMap: IdentityMap = IdentityMap()
   
   let emailIdentity = IdentityItem(id: emailAddress, authenticatedState: AuthenticatedState.authenticated)
   let crmIdentity = IdentityItem(id: crmId, authenticatedState: AuthenticatedState.authenticated)
   identityMap.add(item:emailIdentity, withNamespace: "Email")
   identityMap.add(item: crmIdentity, withNamespace: "lumaCRMId")
   
   Identity.updateIdentities(with: identityMap)
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

1. Accédez à **[!DNL Luma]** > **[!DNL Luma]** > **[!DNL Views]** > **[!DNL General]** > **[!UICONTROL LoginSheet]** dans le navigateur de projet Xcode et recherchez le code à exécuter lors de la sélection de la variable **[!UICONTROL Connexion]** bouton . Ajoutez le code suivant :

   ```swift
   // Update identities
   MobileSDK.shared.updateIdentities(emailAddress: currentEmailId, crmId: currentCRMId)                             
   ```


>[!NOTE]
>
>Vous pouvez envoyer plusieurs identités en une seule `updateIdentities` appelez . Vous pouvez également modifier les identités envoyées précédemment.


## Suppression d’une identité

Vous pouvez utiliser la variable [`Identity.removeIdentity`](https://developer.adobe.com/client-sdks/documentation/identity-for-edge-network/api-reference/#removeidentity) API pour supprimer l’identité de la carte d’identité côté client stockée. L’extension Identity cesse d’envoyer l’identifiant au réseau Edge. L’utilisation de cette API ne supprime pas l’identifiant du graphique d’identités côté serveur. Voir [Affichage des graphiques d’identités](https://experienceleague.adobe.com/docs/platform-learn/tutorials/identities/view-identity-graphs.html?lang=en) pour plus d’informations sur les graphiques d’identités.

1. Accédez à **[!DNL Luma]** > **[!DNL Luma]** > **[!DNL Utils]** > **[!UICONTROL MobileSDK]** dans le navigateur de projet Xcode et ajoutez le code suivant au `func removeIdentities(emailAddress: String, crmId: String)` function:

   ```swift
   // Remove identities and reset email and CRM Id to their defaults
   Identity.removeIdentity(item: IdentityItem(id: emailAddress), withNamespace: "Email")
   Identity.removeIdentity(item: IdentityItem(id: crmId), withNamespace: "lumaCRMId")
   currentEmailId = "testUser@gmail.com"
   currentCRMId = "112ca06ed53d3db37e4cea49cc45b71e"
   ```

1. Accédez à **[!DNL Luma]** > **[!DNL Luma]** > **[!DNL Views]** > **[!DNL General]** > **[!UICONTROL LoginSheet]** dans le navigateur de projet Xcode et recherchez le code à exécuter lors de la sélection de la variable **[!UICONTROL Déconnexion]** bouton . Ajoutez le code suivant :

   ```swift
   // Remove identities
   MobileSDK.shared.removeIdentities(emailAddress: currentEmailId, crmId: currentCRMId)                  
   ```


## Validation avec Assurance

1. Consultez la section [instructions de configuration](assurance.md#connecting-to-a-session) pour connecter le simulateur ou l’appareil à Assurance.
1. Dans l’application Luma
   1. Sélectionnez la variable **[!UICONTROL Accueil]** et déplacez l’icône Assurance vers la gauche.
   1. Sélectionnez le <img src="assets/login.png" width="15" /> en haut à droite.

      <img src="./assets/identity1.png" width="300">

   1. fournir une adresse électronique et un identifiant CRM ; ou
   1. Sélectionner <img src="assets/insert.png" width="15" /> pour générer de manière aléatoire une **[!UICONTROL Email]** et **[!UICONTROL Identifiant CRM]**.
   1. Sélectionner **[!UICONTROL Connexion]**.

      <img src="./assets/identity2.png" width="300">


1. Recherchez dans l’interface web d’Assurance le **[!UICONTROL Identités de mise à jour d’identité Edge]** de l’événement **[!UICONTROL com.adobe.griffon.mobile]** fournisseur.
1. Sélectionnez l’événement et passez en revue les données de la variable **[!UICONTROL ACPExtensionEventData]** . Vous devriez voir les identités que vous avez mises à jour.
   ![mise à jour des identités de validation](assets/identity-validate-assurance.png)

## Validation avec le graphique d’identités

Une fois que vous avez terminé les étapes de la section [leçon Experience Platform](platform.md), vous pouvez confirmer la capture d’identité dans la visionneuse de graphiques d’identités Platform :

1. Sélectionner **[!UICONTROL Identités]** dans l’interface utilisateur de la collecte de données.
1. Sélectionner **[!UICONTROL Graphique d’identités]** dans la barre supérieure.
1. Entrée `Luma CRM ID` comme la propriété **[!UICONTROL Espace de noms d’identité]** et votre identifiant CRM (par exemple, `24e620e255734d8489820e74f357b5c8`) en tant que **[!UICONTROL Valeur d’identité]**.
1. Vous voyez le **[!UICONTROL Identités]** répertorié.

   ![validation du graphique d’identités](assets/identity-validate-graph.png)

>[!INFO]
>
>Il n’existe pas de code dans l’application pour réinitialiser l’ECID, ce qui signifie que vous pouvez uniquement réinitialiser l’ECID (et créer effectivement un profil avec un nouvel ECID) par le biais d’une désinstallation et d’une réinstallation de l’application. Pour mettre en oeuvre la réinitialisation des identifiants, voir la section [`Identity.resetIdentities`](https://developer.adobe.com/client-sdks/documentation/mobile-core/identity/api-reference/#resetidentities) et [`MobileCore.resetIdentities`](https://developer.adobe.com/client-sdks/documentation/mobile-core/api-reference/#resetidentities) Appels API. Soyez toutefois prudent lors de l’utilisation d’un identifiant de notification push (voir [Envoi de notifications push](journey-optimizer-push.md)), cet identifiant devient un autre identifiant de profil &quot;attractif&quot; sur l’appareil.


>[!SUCCESS]
>
>Vous avez maintenant configuré votre application pour mettre à jour les identités dans le réseau Edge et (lors de la configuration) avec Adobe Experience Platform.
>
>Merci d’investir votre temps à apprendre sur le SDK Adobe Experience Platform Mobile. Si vous avez des questions, souhaitez partager des commentaires généraux ou avez des suggestions sur le contenu futur, partagez-les à ce sujet. [Article de discussion de la communauté Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796)

Suivant : **[Collecte des données de profil](profile.md)**
