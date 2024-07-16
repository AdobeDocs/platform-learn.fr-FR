---
title: Collecte de données d’identité dans une application mobile avec SDK Mobile
description: Découvrez comment collecter des données d’identité dans une application mobile.
feature: Mobile SDK,Identities
jira: KT-14633
exl-id: cbcd1708-29e6-4d74-be7a-f75c917ba2fa
source-git-commit: 25f0df2ea09bb7383f45a698e75bd31be7541754
workflow-type: tm+mt
source-wordcount: '815'
ht-degree: 1%

---

# Collecte de données d’identité

Découvrez comment collecter des données d’identité dans une application mobile.

Adobe Experience Platform Identity Service vous permet de mieux connaître vos clients et leurs comportements en rapprochant des identités entre appareils et systèmes, ce qui vous permet de proposer des expériences numériques personnelles et percutantes en temps réel. Les champs d’identité et les espaces de noms sont la colle qui relie différentes sources de données pour créer le profil client en temps réel à 360 degrés.

Pour en savoir plus sur l’ [extension d’identité](https://developer.adobe.com/client-sdks/documentation/identity-for-edge-network/) et le [service d’identité](https://experienceleague.adobe.com/docs/experience-platform/identity/home.html?lang=fr) dans la documentation.

## Conditions préalables

* Création et exécution de l’application avec les SDK installés et configurés.

## Objectifs d&#39;apprentissage

Dans cette leçon, vous allez :

* Configurez un espace de noms d’identité personnalisé.
* Mise à jour des identités.
* Validez le graphique d’identités.
* Obtenez l’ECID et d’autres identités.


## Configuration d’un espace de noms d’identité personnalisé

Les espaces de noms d’identité sont des composants d’ [Identity Service](https://experienceleague.adobe.com/docs/experience-platform/identity/home.html?lang=fr) qui servent d’indicateurs du contexte auquel une identité se rapporte. Par exemple, ils distinguent une valeur de `name@email.com` comme adresse électronique ou de `443522` comme identifiant CRM numérique.

>[!NOTE]
>
>Le SDK Mobile génère une identité unique dans son propre espace de noms, appelé ID Experience Cloud (ECID) lorsque l’application est installée. Cet ECID est stocké en mémoire persistante sur l’appareil mobile et est envoyé avec chaque accès. L’ECID est supprimé lorsque l’utilisateur désinstalle l’application ou lorsque l’utilisateur définit l’état de confidentialité global du SDK Mobile sur exclusion. Dans l’exemple d’application Luma, vous devez supprimer et réinstaller l’application pour créer un nouveau profil avec son propre ECID unique.


Pour créer un espace de noms d’identité, procédez comme suit :

1. Dans l’interface Collecte de données, sélectionnez **[!UICONTROL Identités]** dans le volet de navigation de gauche.
1. Sélectionnez **[!UICONTROL Créer un espace de noms d’identité]**.
1. Fournissez un **[!UICONTROL nom d’affichage]** de `Luma CRM ID` et une valeur **[!UICONTROL symbole d’identité]** de `lumaCRMId`.
1. Sélectionnez **[!UICONTROL ID multi-appareils]**.
1. Sélectionnez **[!UICONTROL Créer]**.

   ![créer un espace de noms d’identité](assets/identity-create.png)




## Mise à jour des identités

Vous souhaitez mettre à jour l’identité standard (e-mail) et l’identité personnalisée (identifiant Luma CRM) lorsque l’utilisateur se connecte à l’application.

1. Accédez à **[!DNL Luma]** > **[!DNL Luma]** > **[!DNL Utils]** > **[!UICONTROL MobileSDK]** dans le navigateur de projet Xcode et recherchez l’implémentation de la fonction `func updateIdentities(emailAddress: String, crmId: String)`. Ajoutez le code suivant à la fonction .

   ```swift
   // Set up identity map, add identities to map and update identities
   let identityMap: IdentityMap = IdentityMap()
   
   let emailIdentity = IdentityItem(id: emailAddress, authenticatedState: AuthenticatedState.authenticated)
   let crmIdentity = IdentityItem(id: crmId, authenticatedState: AuthenticatedState.authenticated)
   identityMap.add(item:emailIdentity, withNamespace: "Email")
   identityMap.add(item: crmIdentity, withNamespace: "lumaCRMId")
   
   Identity.updateIdentities(with: identityMap)
   ```

   Ce code :

   1. Crée un objet `IdentityMap` vide.

      ```swift
      let identityMap: IdentityMap = IdentityMap()
      ```

   1. Configure `IdentityItem` objets pour l’e-mail et l’identifiant CRM.

      ```swift
      let emailIdentity = IdentityItem(id: emailAddress, authenticatedState: AuthenticatedState.authenticated)
      let crmIdentity = IdentityItem(id: crmId, authenticatedState: AuthenticatedState.authenticated)
      ```

   1. Ajoute ces objets `IdentityItem` à l’objet `IdentityMap`.

      ```swift
      identityMap.add(item:emailIdentity, withNamespace: "Email")
      identityMap.add(item: crmIdentity, withNamespace: "lumaCRMId")
      ```

   1. Envoie l’objet `IdentityItem` dans le cadre de l’appel d’API `Identity.updateIdentities` à l’Edge Network.

      ```swift
      Identity.updateIdentities(with: identityMap) 
      ```

1. Accédez à **[!DNL Luma]** > **[!DNL Luma]** > **[!DNL Views]** > **[!DNL General]** > **[!UICONTROL LoginSheet]** dans le navigateur de projet Xcode et recherchez le code à exécuter lors de la sélection du bouton **[!UICONTROL Login]**. Ajoutez le code suivant :

   ```swift
   // Update identities
   MobileSDK.shared.updateIdentities(emailAddress: currentEmailId, crmId: currentCRMId)                             
   ```


>[!NOTE]
>
>Vous pouvez envoyer plusieurs identités dans un seul appel `updateIdentities`. Vous pouvez également modifier les identités envoyées précédemment.


## Suppression d’une identité

Vous pouvez utiliser l’API [`Identity.removeIdentity`](https://developer.adobe.com/client-sdks/documentation/identity-for-edge-network/api-reference/#removeidentity) pour supprimer l’identité de la carte d’identité côté client stockée. L’extension Identity cesse d’envoyer l’identifiant à l’Edge Network. L’utilisation de cette API ne supprime pas l’identifiant du graphique d’identités côté serveur. Pour plus d’informations sur les graphiques d’identités, voir [Affichage des graphiques d’identités](https://experienceleague.adobe.com/docs/platform-learn/tutorials/identities/view-identity-graphs.html?lang=en) .

1. Accédez à **[!DNL Luma]** > **[!DNL Luma]** > **[!DNL Utils]** > **[!UICONTROL MobileSDK]** dans le navigateur de projet Xcode et ajoutez le code suivant à la fonction `func removeIdentities(emailAddress: String, crmId: String)` :

   ```swift
   // Remove identities and reset email and CRM Id to their defaults
   Identity.removeIdentity(item: IdentityItem(id: emailAddress), withNamespace: "Email")
   Identity.removeIdentity(item: IdentityItem(id: crmId), withNamespace: "lumaCRMId")
   currentEmailId = "testUser@gmail.com"
   currentCRMId = "112ca06ed53d3db37e4cea49cc45b71e"
   ```

1. Accédez à **[!DNL Luma]** > **[!DNL Luma]** > **[!DNL Views]** > **[!DNL General]** > **[!UICONTROL LoginSheet]** dans le navigateur de projet Xcode et recherchez le code à exécuter lors de la sélection du bouton **[!UICONTROL Logout]**. Ajoutez le code suivant :

   ```swift
   // Remove identities
   MobileSDK.shared.removeIdentities(emailAddress: currentEmailId, crmId: currentCRMId)                  
   ```


## Valider avec Assurance

1. Consultez la section [instructions de configuration](assurance.md#connecting-to-a-session) pour connecter votre simulateur ou périphérique à Assurance.
1. Dans l’application Luma
   1. Sélectionnez l’onglet **[!UICONTROL Accueil]** et déplacez l’icône Assurance vers la gauche.
   1. Sélectionnez la variable Icône <img src="assets/login.png" width="15" /> en haut à droite.

      <img src="./assets/identity1.png" width="300">

   1. fournir une adresse électronique et un identifiant CRM ; ou
   1. Sélectionner <img src="assets/insert.png" width="15" /> pour générer de manière aléatoire un **[!UICONTROL email]** et un **[!UICONTROL identifiant CRM]**.
   1. Sélectionnez **[!UICONTROL Login]**.

      <img src="./assets/identity2.png" width="300">


1. Recherchez dans l’interface web d’assurance l’événement **[!UICONTROL Identités de mise à jour d’identité Edge]** du fournisseur **[!UICONTROL com.adobe.griffon.mobile]** .
1. Sélectionnez l’événement et passez en revue les données dans l’objet **[!UICONTROL ACPExtensionEventData]** . Vous devriez voir les identités que vous avez mises à jour.
   ![valider la mise à jour des identités](assets/identity-validate-assurance.png)

## Validation avec le graphique d’identités

Une fois que vous avez terminé les étapes de la [leçon Experience Platform](platform.md), vous pouvez confirmer la capture d’identité dans la visionneuse de graphiques d’identités Platform :

1. Sélectionnez **[!UICONTROL Identités]** dans l’interface utilisateur de collecte de données.
1. Sélectionnez **[!UICONTROL Graphique d’identités]** dans la barre supérieure.
1. Saisissez `Luma CRM ID` comme **[!UICONTROL espace de noms d’identité]** et votre ID de gestion de la relation client (par exemple `24e620e255734d8489820e74f357b5c8`) comme **[!UICONTROL valeur d’identité]**.
1. Les **[!UICONTROL identités]** sont répertoriées.

   ![valider le graphique d’identités](assets/identity-validate-graph.png)

>[!INFO]
>
>Il n’existe pas de code dans l’application pour réinitialiser l’ECID, ce qui signifie que vous pouvez uniquement réinitialiser l’ECID (et créer effectivement un profil avec un nouvel ECID) par le biais d’une désinstallation et d’une réinstallation de l’application. Pour mettre en oeuvre la réinitialisation des identifiants, voir les appels API [`Identity.resetIdentities`](https://developer.adobe.com/client-sdks/documentation/mobile-core/identity/api-reference/#resetidentities) et [`MobileCore.resetIdentities`](https://developer.adobe.com/client-sdks/documentation/mobile-core/api-reference/#resetidentities) . Notez cependant que, lors de l’utilisation d’un identifiant de notification push (voir [Envoi de notifications push](journey-optimizer-push.md)), cet identifiant devient un autre identifiant de profil &quot;attractif&quot; sur l’appareil.


>[!SUCCESS]
>
>Vous avez maintenant configuré votre application pour mettre à jour les identités dans l’Edge Network et (lors de la configuration) avec Adobe Experience Platform.
>
>Merci d’investir votre temps à apprendre sur le SDK Adobe Experience Platform Mobile. Si vous avez des questions, souhaitez partager des commentaires généraux ou avez des suggestions sur le contenu à venir, partagez-les sur cet [post de discussion de la communauté Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796)

Suivant : **[Collecter les données de profil](profile.md)**
