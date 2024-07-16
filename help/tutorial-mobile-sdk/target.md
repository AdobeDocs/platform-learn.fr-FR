---
title: Exécution de tests A/B dans les applications mobiles avec le SDK Mobile Target et Platform
description: Découvrez comment utiliser un test A/B Target dans votre application mobile avec le SDK Mobile Platform et Adobe Target.
solution: Data Collection,Target
feature-set: Target
feature: A/B Tests
jira: KT-14641
exl-id: 87546baa-2d8a-4cce-b531-bec3782d2e90
source-git-commit: 25f0df2ea09bb7383f45a698e75bd31be7541754
workflow-type: tm+mt
source-wordcount: '1745'
ht-degree: 1%

---

# Optimisation et personnalisation avec Adobe Target

Découvrez comment optimiser et personnaliser les expériences dans vos applications mobiles avec le SDK Mobile Platform et Adobe Target.

Target fournit tout ce dont vous avez besoin pour personnaliser les expériences de vos clients. Target vous aide à optimiser les recettes de vos sites web et mobiles, de vos applications, de vos médias sociaux et d’autres canaux numériques. Target peut effectuer des tests A/B, des tests multivariés, recommander des produits et du contenu, cibler du contenu, personnaliser automatiquement le contenu à l’aide de l’IA, etc. Cette leçon porte principalement sur la fonctionnalité de test A/B de Target. Pour plus d’informations, consultez la [présentation du test A/B](https://experienceleague.adobe.com/docs/target/using/activities/abtest/test-ab.html?lang=en) .

![Architecture](assets/architecture-at.png)

Avant de pouvoir effectuer des tests A/B avec Target, vous devez vous assurer que les configurations et intégrations appropriées sont en place.

>[!NOTE]
>
>Cette leçon est facultative et s’applique uniquement aux utilisateurs d’Adobe Target qui souhaitent effectuer des tests A/B.


## Conditions préalables

* Création et exécution de l’application avec les SDK installés et configurés.
* Accès à Adobe Target avec des autorisations, des rôles, des espaces de travail et des propriétés correctement configurés, comme décrit [ici](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/enterprise/property-channel.html?lang=fr).


## Objectifs d&#39;apprentissage

Dans cette leçon, vous allez :

* Mettez à jour votre flux de données pour l’intégration de Target.
* Mettez à jour votre propriété de balise avec l’extension Journey Optimizer - Decisioning.
* Mettez à jour votre schéma pour capturer les événements de proposition.
* Validez la configuration dans Assurance.
* Créez un test A/B simple dans Target.
* Mettez à jour votre application pour enregistrer l’extension Optimizer.
* Mettez en oeuvre le test A/B dans votre application.
* Validez l’implémentation dans Assurance.


## Configuration

>[!TIP]
>
>Si vous avez déjà configuré votre application dans le cadre de la leçon [Offres Journey Optimizer](journey-optimizer-offers.md), vous avez peut-être déjà effectué certaines étapes de cette section de configuration.

### Mise à jour de la configuration des flux de données

#### Adobe Target

Pour vous assurer que les données envoyées de votre application mobile à l’Edge Network Experience Platform sont transférées vers Adobe Target, vous devez mettre à jour la configuration de la banque de données.

1. Dans l’interface utilisateur de la collecte de données, sélectionnez **[!UICONTROL Datastreams]**, puis sélectionnez votre flux de données, par exemple **[!DNL Luma Mobile App]**.
1. Sélectionnez **[!UICONTROL Ajouter un service]** et **[!UICONTROL Adobe Target]** dans la liste **[!UICONTROL Service]**.
1. Si vous êtes client Target Premium et souhaitez utiliser des jetons de propriété, saisissez la valeur Target **[!UICONTROL Property Token]** que vous souhaitez utiliser pour cette intégration. Les utilisateurs de Target Standard peuvent ignorer cette étape.

   Vous trouverez vos propriétés dans l’interface utilisateur de Target, sous **[!UICONTROL Administration]** > **[!UICONTROL Propriétés]**. Sélectionnez ![Code](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Code_18_N.svg) pour afficher le jeton de propriété de la propriété que vous souhaitez utiliser. Le jeton de propriété a un format de type `"at_property": "xxxxxxxx-xxxx-xxxxx-xxxx-xxxxxxxxxxxx"` ; vous ne devez saisir que la valeur `xxxxxxxx-xxxx-xxxxx-xxxx-xxxxxxxxxxxx`.

   Vous pouvez éventuellement spécifier un ID d’environnement cible. Target utilise des environnements pour organiser vos sites et environnements de préproduction afin de faciliter la gestion et la création de rapports. Les environnements prédéfinis incluent Production, Test et Développement. Pour plus d’informations, voir [Environments](https://experienceleague.adobe.com/docs/target/using/administer/environments.html?lang=en) et [Target Environment ID](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/applications-setup/setup-target.html?lang=en#target-environment-id) .

   Vous pouvez éventuellement spécifier un espace de noms d’identifiant tiers Target pour prendre en charge la synchronisation des profils sur un espace de noms d’identité (par exemple, un identifiant CRM). Pour plus d’informations, voir [Espace de noms d’ID tiers Target](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/applications-setup/setup-target.html?lang=en#target-third-party-id-namespace) .

1. Sélectionnez **[!UICONTROL Enregistrer]**.

   ![Ajouter Target à la banque de données](assets/edge-datastream-target.png)


#### Adobe Journey Optimizer

Pour vous assurer que les données envoyées de votre application mobile à l’Edge Network sont transférées vers Journey Optimizer - Gestion des décisions, mettez à jour votre configuration de flux de données.

1. Dans l’interface utilisateur de la collecte de données, sélectionnez **[!UICONTROL Datastreams]**, puis sélectionnez votre flux de données, par exemple **[!DNL Luma Mobile App]**.
1. Sélectionnez ![Plus](https://spectrum.adobe.com/static/icons/workflow_18/Smock_MoreSmallList_18_N.svg) pour **[!UICONTROL Experience Platform]** et ![Modifier](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Edit_18_N.svg) **[!UICONTROL Modifier]** dans le menu contextuel.
1. Dans l’écran **[!UICONTROL Datastreams]** > ![Folder](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Folder_18_N.svg) > **[!UICONTROL Adobe Experience Platform]**, assurez-vous que **[!UICONTROL Offer decisioning]**, **[!UICONTROL Segmentation Edge]** et **[!UICONTROL Destinations Personalization]** sont sélectionnés. Si vous suivez également les leçons Journey Optimizer, vous sélectionnez **[!UICONTROL Adobe Journey Optimizer]**. Voir [Paramètres Adobe Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/datastreams/configure.html?lang=en#aep) pour plus d’informations.
1. Pour enregistrer votre configuration de flux de données, sélectionnez **[!UICONTROL Enregistrer]** .

   ![ {configuration de flux de données AEP](assets/datastream-aep-configuration-target.png)


### Installer Adobe Journey Optimizer - Extension des balises de prise de décision

1. Accédez à **[!UICONTROL Balises]**, recherchez votre propriété de balise mobile, puis ouvrez la propriété .
1. Sélectionnez **[!UICONTROL Extensions]**.
1. Sélectionnez **[!UICONTROL Catalog]**.
1. Recherchez l’extension **[!UICONTROL Adobe Journey Optimizer - Decisioning]**.
1. Installez l’extension . L’extension ne nécessite pas de configuration supplémentaire.

   ![Ajouter l’extension de prise de décision](assets/tag-add-decisioning-extension.png)


### Mettre à jour votre schéma

1. Accédez à l’interface de collecte de données et sélectionnez **[!UICONTROL Schémas]** dans le rail de gauche.
1. Sélectionnez **[!UICONTROL Parcourir]** dans la barre supérieure.
1. Sélectionnez votre schéma pour l’ouvrir.
1. Dans l’éditeur de schéma, sélectionnez ![Ajouter](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) **[!UICONTROL Ajouter]** en regard de **[!UICONTROL Groupes de champs]**.
1. Dans la boîte de dialogue **[!UICONTROL Ajouter des groupes de champs]**, recherchez `proposition`, sélectionnez **[!UICONTROL Événement d’expérience - Interactions de propositions]** et sélectionnez **[!UICONTROL Ajouter des groupes de champs]**.
   ![Proposition](assets/schema-fieldgroup-proposition.png)
1. Pour enregistrer les modifications apportées à votre schéma, sélectionnez **[!UICONTROL Enregistrer]**.


### Validation de la configuration dans Assurance

Pour valider votre configuration dans Assurance :

1. Accédez à l’interface utilisateur d’assurance.
1. Sélectionnez **[!UICONTROL Configurer]** dans le rail gauche et sélectionnez ![Ajouter](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) en regard de **[!UICONTROL Valider la configuration]** sous **[!UICONTROL ADOBE JOURNEY OPTIMIZER DECISIONING]**.
1. Sélectionnez **[!UICONTROL Enregistrer]**.
1. Sélectionnez **[!UICONTROL Valider la configuration]** dans le rail de gauche. La configuration du flux de données est validée et celle du SDK dans votre application.
   ![Validation de prise de décision AJO](assets/ajo-decisioning-validation.png)

## Création d’un test A/B

Il existe de nombreux types d’activités que vous pouvez créer dans Adobe Target et mettre en oeuvre dans une application mobile, comme indiqué dans l’introduction. Pour cette leçon, vous allez mettre en oeuvre un test A/B.

1. Dans l’interface utilisateur de Target, sélectionnez **[!UICONTROL Activités]** dans la barre supérieure.
1. Sélectionnez **[!UICONTROL Créer l’activité]** et **[!UICONTROL Test A/B]** dans le menu contextuel.
1. Dans la boîte de dialogue **[!UICONTROL Créer une activité de test A/B]**, sélectionnez **[!UICONTROL Mobile]** comme **[!UICONTROL Type]**, sélectionnez un espace de travail dans la liste **[!UICONTROL Choisir Workspace]**, puis sélectionnez votre propriété dans la liste **[!UICONTROL Choisir la propriété]** si vous êtes un client Target Premium et avez spécifié un jeton de propriété dans le flux de données.
1. Sélectionnez **[!UICONTROL Créer]**.
   ![Créer une activité Target](assets/target-create-activity1.png)

1. Dans l’écran **[!UICONTROL Activité sans titre]**, à l’étape **[!UICONTROL Expériences]** :

   1. Saisissez `luma-mobileapp-abtest` dans **[!UICONTROL Select Location]** sous **[!UICONTROL LOCATION 1]**. Ce nom d’emplacement (souvent appelé mbox) est utilisé ultérieurement dans la mise en oeuvre de l’application.
   1. Sélectionnez ![Chrevron down](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ChevronDown_18_N.svg) en regard de **[!UICONTROL Contenu par défaut]** et sélectionnez **[!UICONTROL Créer une offre JSON]** dans le menu contextuel.
   1. Copiez le fichier JSON suivant dans **[!UICONTROL Saisissez un objet JSON valide]**.

      ```json
      { 
          "title": "Luma Anaolog Watch",
          "text": "Designed to stand up to your active lifestyle, this women's Luma Analog Watch features a tasteful brushed chrome finish and a stainless steel, water-resistant construction for lasting durability.", 
          "image": "https://luma.enablementadobe.com/content/dam/luma/en/products/gear/watches/Luma_Analog_Watch.jpg" 
      }
      ```

   1. Sélectionnez **[!UICONTROL + Ajouter une expérience]**.

      ![Expérience A](assets/target-create-activity-experienceA.png)

   1. Répétez les étapes b et c pour l’expérience B, mais utilisez plutôt le fichier JSON suivant :

      ```json
      { 
          "title": "Aim Analog Watch",
          "text": "The flexible, rubberized strap is contoured to conform to the shape of your wrist for a comfortable all-day fit. The face features three illuminated hands, a digital read-out of the current time, and stopwatch functions.", 
          "image": "https://luma.enablementadobe.com/content/dam/luma/en/products/gear/watches/Aim_Watch.jpg" 
      }
      ```

   1. Sélectionnez **[!UICONTROL Suivant]**.

      ![Expérience B](assets/target-create-activity-experienceB.png)

1. À l’étape **[!DNL Targeting]**, passez en revue la configuration de votre test A/B. Par défaut, les deux offres sont réparties de manière égale entre tous les visiteurs. Sélectionnez **[!UICONTROL Suivant]** pour continuer.

   ![Ciblage](assets/taget-targeting.png)

1. À l’étape **[!UICONTROL Objectifs et paramètres]** :

   1. Renommez votre activité sans titre, par exemple `Luma Mobile SDK Tutorial - A/B Test Example`.
   1. Saisissez un **[!UICONTROL objectif]** pour votre test A/B, par exemple `A/B Test for Luma mobile app tutorial`.
   1. Sélectionnez **[!UICONTROL Conversion]**, **[!UICONTROL A affiché une mbox]** dans la mosaïque **[!UICONTROL Mesure de l’objectif]** > **[!UICONTROL MY PRINCIPAL GOAL]** et saisissez votre nom d’emplacement (mbox), par exemple `luma-mobileapp-abtest`.
   1. Sélectionnez **[!UICONTROL Enregistrer et fermer]**.

      ![Paramètres des objectifs](assets/target-goals.png)

1. De retour dans l’écran **[!UICONTROL Toutes les activités]** :

   1. Sélectionnez ![Plus](https://spectrum.adobe.com/static/icons/workflow_18/Smock_MoreSmallList_18_N.svg) dans votre activité.
   1. Sélectionnez ![Play](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Play_18_N.svg) **[!UICONTROL Activer]** pour activer votre test A/B.

   ![Activer](assets/target-activate.png)


## Implémentation de Target dans votre application

Comme indiqué dans les leçons précédentes, l’installation d’une extension de balise mobile fournit uniquement la configuration. Vous devez ensuite installer et enregistrer le SDK Optimiser. Si ces étapes ne sont pas claires, consultez la section [Installer les SDK](install-sdks.md) .

>[!NOTE]
>
>Si vous avez terminé la section [Installer les SDK](install-sdks.md) , le SDK est déjà installé et vous pouvez ignorer cette étape.
>

1. Dans Xcode, assurez-vous que [AEP Optimize](https://github.com/adobe/aepsdk-messaging-ios) est ajouté à la liste des modules dans les dépendances de modules. Voir [Swift Package Manager](install-sdks.md#swift-package-manager).
1. Accédez à **[!DNL Luma]** > **[!DNL Luma]** > **[!DNL AppDelegate]** dans le navigateur de projet Xcode.
1. Assurez-vous que `AEPOptimize` fait partie de votre liste d’importations.

   `import AEPOptimize`

1. Vérifiez que `Optimize.self` fait partie du tableau des extensions que vous enregistrez.

   ```swift
   let extensions = [
       AEPIdentity.Identity.self,
       Lifecycle.self,
       Signal.self,
       Edge.self,
       AEPEdgeIdentity.Identity.self,
       Consent.self,
       UserProfile.self,
       Places.self,
       Messaging.self,
       Optimize.self,
       Assurance.self
   ]
   ```

1. Accédez à **[!DNL Luma]** > **[!DNL Luma]** > **[!DNL Utils]** > **[!DNL MobileSDK]** dans le navigateur de projet Xcode. Recherchez la fonction ` func updatePropositionAT(ecid: String, location: String) async` . Ajoutez le code suivant :

   ```swift
   // set up the XDM dictionary, define decision scope and call update proposition API
   Task {
       let ecid = ["ECID" : ["id" : ecid, "primary" : true] as [String : Any]]
       let identityMap = ["identityMap" : ecid]
       let xdmData = ["xdm" : identityMap]
       let decisionScope = DecisionScope(name: location)
       Optimize.clearCachedPropositions()
       Optimize.updatePropositions(for: [decisionScope], withXdm: xdmData)
   }
   ```

   Cette fonction :

   * configure un dictionnaire XDM `xdmData`, contenant l’ECID pour identifier le profil pour lequel vous devez présenter le test A/B, et
   * définit un `decisionScope`, un tableau d’emplacements où présenter le test A/B.

   Ensuite, la fonction appelle deux API : [`Optimize.clearCachedPropositions`](https://developer.adobe.com/client-sdks/documentation/adobe-journey-optimizer-decisioning/api-reference/#clearpropositions) et [`Optimize.updatePropositions`](https://developer.adobe.com/client-sdks/documentation/adobe-journey-optimizer-decisioning/api-reference/#updatepropositions). Ces fonctions effacent toutes les propositions mises en cache et mettent à jour les propositions de ce profil. Dans ce contexte, une proposition est l’expérience (offre) sélectionnée dans l’activité Target (votre test A/B) et que vous avez définie dans [Créer un test A/B](#create-an-ab-test).

1. Accédez à **[!DNL Luma]** > **[!DNL Luma]** > **[!DNL Views]** > **[!DNL Personalization]** > **[!DNL TargetOffersView]** dans le navigateur de projet Xcode. Recherchez la fonction `func onPropositionsUpdateAT(location: String) async {` et examinez le code de cette fonction. La partie la plus importante de cette fonction est l’appel API [`Optimize.onPropositionsUpdate`](https://developer.adobe.com/client-sdks/documentation/adobe-journey-optimizer-decisioning/api-reference/#onpropositionsupdate), qui :
   * récupère les propositions du profil actuel en fonction de la portée de la décision (qui est l’emplacement que vous avez défini dans le test A/B),
   * récupère l&#39;offre à partir de la proposition,
   * libère le contenu de l’offre afin qu’elle puisse s’afficher correctement dans l’application ; et
   * déclenche l’action `displayed()` sur l’offre qui renvoie un événement à l’Edge Network Platform pour informer l’affichage de l’offre.

1. Toujours dans **[!DNL TargetOffersView]**, ajoutez le code suivant au modificateur `.onFirstAppear`. Ce code garantit que le rappel pour la mise à jour des offres n’est enregistré qu’une seule fois.

   ```swift
   // Invoke callback for offer updates
   Task {
       await self.onPropositionsUpdateAT(location: location)
   }
   ```

1. Toujours dans **[!DNL TargetOffersView]**, ajoutez le code suivant au modificateur `.task`. Ce code met à jour les offres lorsque la vue est actualisée.

   ```swift
   // Clear and update offers
   await self.updatePropositionsAT(ecid: currentEcid, location: location)
   ```

Vous pouvez envoyer des paramètres Target supplémentaires (comme des paramètres de mbox, de profil, de produit ou de commande) dans une requête de personnalisation au réseau Experience Edge, en les ajoutant dans un dictionnaire de données lors de l’appel de l’API [`Optimize.updatePropositions`](https://developer.adobe.com/client-sdks/documentation/adobe-journey-optimizer-decisioning/api-reference/#updatepropositions). Voir pour plus d’informations [Paramètres Target](https://developer.adobe.com/client-sdks/documentation/adobe-journey-optimizer-decisioning/#target-parameters).


## Validation à l’aide de l’application

1. Recréez et exécutez l’application dans le simulateur ou sur un appareil physique à partir de Xcode, en utilisant ![Play](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Play_18_N.svg).

1. Accédez à l&#39;onglet **[!UICONTROL Personnalisation]**.

1. Faites défiler l’écran jusqu’en bas pour voir l’une des deux offres que vous avez définies dans votre test A/B affichée dans la mosaïque **[!UICONTROL TARGET]**.

   <img src="assets/target-app-offer.png" width="300">


## Validation de la mise en oeuvre dans Assurance

Pour valider le test A/B dans Assurance :

1. Consultez la section [instructions de configuration](assurance.md#connecting-to-a-session) pour connecter votre simulateur ou périphérique à Assurance.
1. Sélectionnez **[!UICONTROL Configurer]** dans le rail gauche et sélectionnez ![Ajouter](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) en regard de **[!UICONTROL Réviser et simuler]** sous **[!UICONTROL ADOBE JOURNEY OPTIMIZER DECISIONING]**.
1. Sélectionnez **[!UICONTROL Enregistrer]**.
1. Sélectionnez **[!UICONTROL Réviser et simuler]** dans le rail de gauche. La configuration du flux de données est validée et celle du SDK dans votre application.
1. Sélectionnez **[!UICONTROL Demandes]** dans la barre supérieure. Vos requêtes **[!DNL Target]** s’affichent.
   ![Validation de prise de décision AJO](assets/assurance-decisioning-requests.png)

1. Vous pouvez explorer les onglets **[!UICONTROL Simuler]** et **[!UICONTROL Liste d’événements]** pour découvrir d’autres fonctionnalités qui vérifient votre configuration pour les offres Target.

## Étapes suivantes

Vous devez maintenant disposer de tous les outils pour commencer à ajouter d’autres tests A/B ou d’autres activités Target (comme le ciblage d’expérience, le test multivarié), le cas échéant, à votre application. Des informations plus détaillées sont disponibles dans le [référentiel GitHub pour l’extension Optimize](https://github.com/adobe/aepsdk-optimize-ios) où vous pouvez également trouver un lien vers un [tutoriel](https://opensource.adobe.com/aepsdk-optimize-ios/#/tutorials/README) dédié sur la manière de suivre les offres Adobe Target.

>[!SUCCESS]
>
>Vous avez activé l’application pour les tests A/B et affiché les résultats d’un test A/B avec Adobe Target et l’extension Adobe Journey Optimizer - Prise de décision pour le SDK Mobile Adobe Experience Platform.
>
>Merci d’investir votre temps à apprendre sur le SDK Adobe Experience Platform Mobile. Si vous avez des questions, souhaitez partager des commentaires généraux ou avez des suggestions sur le contenu à venir, partagez-les sur cet [post de discussion de la communauté Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796).

Suivant : **[Conclusion et étapes suivantes](conclusion.md)**
