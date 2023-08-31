---
title: Exécution de tests A/B avec Target
description: Découvrez comment utiliser un test A/B Target dans votre application mobile avec le SDK Mobile Platform et Adobe Target.
solution: Data Collection,Target
feature-set: Target
feature: A/B Tests
hide: true
source-git-commit: 593dcce7d1216652bb0439985ec3e7a45fc811de
workflow-type: tm+mt
source-wordcount: '1418'
ht-degree: 3%

---


# Exécution de tests A/B avec Target

Découvrez comment effectuer des tests A/B dans vos applications mobiles avec le SDK Mobile Platform et Adobe Target.

Target fournit tout ce dont vous avez besoin pour personnaliser les expériences de vos clients. Target vous aide à optimiser les recettes de vos sites web et mobiles, de vos applications, de vos médias sociaux et d’autres canaux numériques. Ce tutoriel se concentre sur la fonctionnalité de test A/B de Target. Voir [Présentation des tests A/B](https://experienceleague.adobe.com/docs/target/using/activities/abtest/test-ab.html?lang=en) pour plus d’informations.

Avant de pouvoir effectuer des tests A/B avec Target, vous devez vous assurer que les configurations et intégrations appropriées sont en place.

>[!NOTE]
>
>Cette leçon est facultative et s’applique uniquement aux utilisateurs d’Adobe Target qui souhaitent effectuer des tests A/B.


## Conditions préalables

* Création et exécution de l’application avec les SDK installés et configurés.
* Accès à Adobe Target Premium avec autorisations, rôles, espaces de travail et propriétés correctement configurés, comme décrit [here](https://experienceleague.adobe.com/docs/target/using/administer/manage-users/enterprise/property-channel.html?lang=fr).
Vous devriez également pouvoir utiliser Target Standard, mais le tutoriel utilise certains concepts avancés (par exemple, les propriétés de Target) qui sont propres à Target Premium.


## Objectifs d&#39;apprentissage

Dans cette leçon, vous allez

* Mettez à jour votre configuration Edge pour l’intégration de Target.
* Mettez à jour votre propriété de balise avec l’extension Journey Optimizer - Decisioning.
* Mettez à jour votre schéma pour capturer les événements de proposition.
* Validez la configuration dans Assurance.
* Créez un test A/B simple dans Target.
* Mettez à jour votre application pour inclure l’extension Optimizer.
* Mettez en oeuvre le test A/B dans votre application.
* Validez l’implémentation dans Assurance.


## Configuration de votre application

>[!TIP]
>
>Si vous avez déjà configuré votre application dans le cadre de la [Offres Journey Optimizer](journey-optimizer-offers.md) tutoriel,

### Mise à jour de la configuration Edge

Pour vous assurer que les données envoyées de votre application mobile vers le réseau Edge sont transférées vers Adobe Target, vous devez mettre à jour votre configuration Experience Edge.

1. Dans l’interface utilisateur de la collecte de données, sélectionnez **[!UICONTROL Datastreams]**, puis sélectionnez votre flux de données, par exemple **[!UICONTROL Application mobile Luma]**.
1. Sélectionner **[!UICONTROL Ajouter un service]** et sélectionnez **[!UICONTROL Adobe Target]** de la **[!UICONTROL Service]** liste.
1. Saisissez la cible **[!UICONTROL Jeton de propriété]** que vous souhaitez utiliser pour cette intégration.

   Vous trouverez vos propriétés dans l’interface utilisateur de Target, dans **[!UICONTROL Administration]** > **[!UICONTROL Propriétés]**. Sélectionner ![Code](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Code_18_N.svg) pour afficher le jeton de propriété de la propriété que vous souhaitez utiliser. Le jeton de propriété a un format semblable à `"at_property": "xxxxxxxx-xxxx-xxxxx-xxxx-xxxxxxxxxxxx"`; vous ne devez saisir que la valeur `xxxxxxxx-xxxx-xxxxx-xxxx-xxxxxxxxxxxx`.

1. Sélectionnez **[!UICONTROL Enregistrer]**.

   ![Ajout de Target à un flux de données](assets/edge-datastream-target.png)


### Installer Adobe Journey Optimizer - Extension des balises de prise de décision

1. Accédez à **[!UICONTROL Balises]** et recherchez la propriété de balise mobile et ouvrez-la.
1. Sélectionner **[!UICONTROL Extensions]**.
1. Sélectionner **[!UICONTROL Catalogue]**.
1. Recherchez le **[!UICONTROL Adobe Journey Optimizer - Prise de décision]** extension .
1. Installation l’extension. L’extension ne nécessite pas de configuration supplémentaire.

   ![Ajout de l’extension de prise de décision](assets/tag-add-decisioning-extension.png)


### Mettre à jour votre schéma

1. Accédez à l’interface utilisateur de la collecte de données et sélectionnez Schémas dans le rail de gauche.
1. Sélectionner **[!UICONTROL Parcourir]** dans la barre supérieure.
1. Sélectionnez votre schéma pour l’ouvrir.
1. Dans l’éditeur de schéma, sélectionnez ![Ajouter](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) **[!UICONTROL Ajouter]** en regard de **[!UICONTROL Groupes de champs]**.
1. Dans la boîte de dialogue Ajouter des groupes de champs, recherchez `proposition`, sélectionnez **[!UICONTROL Événement d’expérience - Interactions de propositions]** et sélectionnez **[!UICONTROL Ajouter des groupes de champs]**.
   ![Proposition](assets/schema-fieldgroup-proposition.png)
1. pour enregistrer les modifications apportées à votre schéma, sélectionnez **[!UICONTROL Enregistrer]** .


### Validation de la configuration dans Assurance

Pour valider votre configuration dans Assurance :

1. Accédez à l’interface utilisateur d’assurance.
1. Sélectionner **[!UICONTROL Configurer]** dans le rail de gauche et sélectionnez ![Ajouter](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) en regard de **[!UICONTROL Validation de la configuration]** underneath **[!UICONTROL PRISE DE DÉCISION ADOBE JOURNEY OPTIMIZER]**.
1. Sélectionnez **[!UICONTROL Enregistrer]**.
1. Sélectionner **[!UICONTROL Validation de la configuration]** dans le rail de gauche. La configuration du flux de données est validée et celle du SDK dans votre application.
   ![Validation de la prise de décision AJO](assets/ajo-decisioning-validation.png)

## Création d’un test A/B

1. Dans l’interface utilisateur de Target, sélectionnez **[!UICONTROL Activités]** dans la barre supérieure.
1. Sélectionner **[!UICONTROL Créer une activité]** et **[!UICONTROL Test A/B]** dans le menu contextuel.
1. Dans le **[!UICONTROL Créer une activité de test A/B]** modal, sélectionnez **[!UICONTROL Mobile]** comme la propriété **[!UICONTROL Type]**, sélectionnez un espace de travail dans la **[!UICONTROL Choisir Workspace]** et sélectionnez votre propriété dans la liste **[!UICONTROL Choisir la propriété]** liste.
1. Sélectionnez **[!UICONTROL Créer]**.
   ![Activité Créer Target](assets/target-create-activity1.png)

1. Dans le **[!UICONTROL Activité sans titre]** , au niveau de l’écran **[!UICONTROL Expériences]** étape :

   1. Entrée `luma-mobileapp-abtest` in **[!UICONTROL Sélectionner un emplacement]** sous L**[!UICONTROL OCATION 1]**.
   1. Sélectionner ![Chrevron vers le bas](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ChevronDown_18_N.svg) en regard de **[!UICONTROL Contenu par défaut]** et sélectionnez **[!UICONTROL Création d’une offre JSON]** dans le menu contextuel.
   1. Copiez le fichier JSON suivant dans **[!UICONTROL Saisie d’un objet JSON valide]**.

      ```json
      { 
          "title": "Luma Anaolog Watch",
          "text": "Designed to stand up to your active lifestyle, this women's Luma Analog Watch features a tasteful brushed chrome finish and a stainless steel, water-resistant construction for lasting durability.", 
          "image": "https://luma.enablementadobe.com/content/dam/luma/en/products/gear/watches/Luma_Analog_Watch.jpg" 
      }
      ```

   1. Sélectionner **[!UICONTROL + Ajouter une expérience]**.

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

      ![Expérience B](assets/target-create-activity-experienceB.png)

1. Dans le **[!UICONTROL Ciblage]** passez en revue la configuration de votre test A/B. Par défaut, les deux offres sont réparties de manière égale entre tous les visiteurs. Sélectionnez **[!UICONTROL Suivant]** pour continuer.

   ![Ciblage](assets/taget-targeting.png)

1. Dans le **[!UICONTROL Objectifs et paramètres]** étape :

   1. Renommez votre activité sans titre, par exemple en `Luma Mobile SDK Tutorial - A/B Test Example`.
   1. Saisissez un **[!UICONTROL Objectif]** pour votre test A/B, par exemple `A/B Test for Luma mobile app tutorial`.
   1. Sélectionner **[!UICONTROL Conversion]**, **[!UICONTROL Cliqué sur la mbox]** dans le **[!UICONTROL Mesure de l’objectif]** > **[!UICONTROL MON OBJECTIF DE PRINCIPAL]** et saisissez votre nom d’emplacement (mbox, par exemple). `luma-mobileapp-abtest`.
   1. Sélectionnez **[!UICONTROL Enregistrer et fermer]**.

      ![Paramètres des objectifs](assets/target-goals.png)

1. De retour dans le **[!UICONTROL Toutes les activités]** écran :

   1. Sélectionner ![Plus](https://spectrum.adobe.com/static/icons/workflow_18/Smock_MoreSmallList_18_N.svg) dans votre activité.
   1. Sélectionner ![Play](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Play_18_N.svg) **[!UICONTROL Activer]** pour activer votre test A/B.

   ![Activer](assets/target-activate.png)


## Implémentation de Target dans votre application

Comme indiqué dans les leçons précédentes, l’installation d’une extension de balise mobile fournit uniquement la configuration. Vous devez ensuite installer et enregistrer le SDK Optimiser. Si ces étapes ne sont pas claires, passez en revue la [Installation des SDK](install-sdks.md) .

>[!NOTE]
>
>Si vous avez terminé la [Installation des SDK](install-sdks.md) , le SDK est déjà installé et vous pouvez ignorer cette étape.
>

1. Dans Xcode, assurez-vous que [Optimisation AEP](https://github.com/adobe/aepsdk-messaging-ios.git) est ajouté à la liste des modules dans les dépendances de modules. Voir [Swift Package Manager](install-sdks.md#swift-package-manager).
1. Accédez à **[!UICONTROL Luma]** > **[!UICONTROL Luma]** > **[!UICONTROL AppDelegate]** dans le navigateur de projet Xcode.
1. Assurez-vous que `AEPOptimize` fait partie de votre liste d’importations.

   `import AEPOptimize`

1. Assurez-vous que `Optimize.self` fait partie du tableau des extensions que vous enregistrez.

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

1. Accédez à **[!UICONTROL Luma]** > **[!UICONTROL Luma]** > **[!UICONTROL Utils]** > **[!UICONTROL MobileSDK]** dans le navigateur de projet Xcode. Recherchez le ` func updatePropositionAT(ecid: String, location: String) async` de la fonction Inspect du code qui configure
   * dictionnaire XDM `xdmData`, contenant l’ECID pour identifier le profil pour lequel vous devez présenter le test A/B, et
   * la valeur `decisionScope`, un tableau d’emplacements sur lequel présenter le test A/B.

   La fonction appelle ensuite deux API : [`Optimize.clearCachePropositions`](https://support.apple.com/en-ie/guide/mac-help/mchlp1015/mac)  et [`Optimize.updatePropositions`](https://developer.adobe.com/client-sdks/documentation/adobe-journey-optimizer-decisioning/api-reference/#updatepropositions). Ces fonctions effacent toutes les propositions mises en cache et mettent à jour les propositions de ce profil.

1. Accédez à **[!UICONTROL Luma]** > **[!UICONTROL Luma]** > **[!UICONTROL Vues]** > **[!UICONTROL Personnalisation]** > **[!UICONTROL TargetOffersView]** dans le navigateur de projet Xcode. Recherchez le `func getPropositionAT(location: String) async` et examinez le code de cette fonction. La partie la plus importante de cette fonction est la fonction  [`Optimize.getPropositions`](https://developer.adobe.com/client-sdks/documentation/adobe-journey-optimizer-decisioning/api-reference/#getpropositions) appel API, qui
   * récupère les propositions du profil actuel en fonction de la portée de la décision (c’est-à-dire l’emplacement que vous avez défini dans le test A/B) et
   * libère le résultat du contenu qui peut être affiché correctement dans l’application.

1. Toujours dans **[!UICONTROL TargetOffersView]**, recherchez le f`unc updatePropositions(location: String) async` et ajoutez le code suivant :

   ```swift
       Task {
           await self.updatePropositionAT(
               ecid: currentEcid,
               location: location
           )
       }
       try? await Task.sleep(seconds: 2.0)
       Task {
           await self.getPropositionAT(
               location: location
           )
       }
   ```

   Ce code permet de mettre à jour les propositions, puis de récupérer les résultats à l&#39;aide des fonctions décrites dans les étapes 5 et 6.


## Validation à l’aide de l’application

1. Ouvrez votre application sur un appareil ou dans le simulateur.

1. Accédez au **[!UICONTROL Personnalisation]** .

1. Sélectionner **[!UICONTROL Personnalisation d’Edge]**.

1. Faites défiler l’écran jusqu’en bas pour voir l’une des deux offres que vous avez définies dans votre test A/B affichée dans la **[!UICONTROL TARGET]** mosaïque.

   <img src="assets/target-app-offer.png" width="300">


## Validation de la mise en oeuvre dans Assurance

Pour valider le test A/B dans Assurance :

1. Accédez à l’interface utilisateur d’assurance.
1. Sélectionner **[!UICONTROL Configurer]** dans le rail de gauche et sélectionnez ![Ajouter](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) en regard de **[!UICONTROL Révision et simulation]** underneath **[!UICONTROL PRISE DE DÉCISION ADOBE JOURNEY OPTIMIZER]**.
1. Sélectionnez **[!UICONTROL Enregistrer]**.
1. Sélectionner **[!UICONTROL Révision et simulation]** dans le rail de gauche. La configuration du flux de données est validée et celle du SDK dans votre application.
1. Sélectionner **[!UICONTROL Demandes]** dans la barre supérieure. Vous voyez votre **[!UICONTROL Cible]** requêtes.
   ![Validation de la prise de décision AJO](assets/assurance-decisioning-requests.png)

1. Vous pouvez explorer les onglets Simuler et Liste d’événements pour découvrir d’autres fonctionnalités permettant de vérifier votre configuration pour les offres Target.

## Étapes suivantes

Vous devez maintenant disposer de tous les outils pour commencer à ajouter d’autres tests A/B ou d’autres activités Target (comme le ciblage d’expérience, le test multivarié), le cas échéant et selon le cas, à l’application Luma.

>[!SUCCESS]
>
>Vous avez activé l’application pour les tests A/B et affiché les résultats d’un test A/B à l’aide d’Adobe Target et de l’extension Adobe Journey Optimizer - Prise de décision pour le SDK Mobile Adobe Experience Platform.<br/>Merci d’investir votre temps à apprendre sur le SDK Adobe Experience Platform Mobile. Si vous avez des questions, souhaitez partager des commentaires généraux ou avez des suggestions sur le contenu futur, partagez-les à ce sujet. [Article de discussion de la communauté Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796).

Suivant : **[Conclusion et prochaines étapes](conclusion.md)**
