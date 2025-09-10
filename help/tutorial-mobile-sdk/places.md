---
title: Utiliser Places avec Platform Mobile SDK
description: Découvrez comment utiliser le service de géolocalisation Places dans votre application mobile.
jira: KT-14635
exl-id: adc2952f-cb01-4e06-9629-49fb95f22ca5
source-git-commit: 008d3ee066861ea9101fe9fe99ccd0a088b63f23
workflow-type: tm+mt
source-wordcount: '1825'
ht-degree: 2%

---

# Utilisation des emplacements

Découvrez comment utiliser le service de géolocalisation Places dans votre application.

Le service Places de collecte de données Adobe Experience Platform est un service de géolocalisation qui permet aux applications mobiles de comprendre le contexte de l’emplacement grâce à la connaissance de l’emplacement. Le service utilise des interfaces SDK riches et faciles à utiliser, accompagnées d’une base de données flexible de points ciblés (POI).

## Conditions préalables

* Toutes les dépendances de package sont en place dans le projet Xcode.
* Extensions enregistrées dans AppDelegate.
* MobileCore configuré pour utiliser votre appId de développement.
* SDK importés.
* L’application a été créée et exécutée avec les modifications ci-dessus.

## Objectifs d’apprentissage

Dans cette leçon, vous allez :

* Découvrez comment définir les points d’intérêt dans le service Places.
* Mettez à jour la propriété de balise avec l’extension Places.
* Mettez à jour votre schéma pour capturer les événements de géolocalisation.
* Validez la configuration dans Assurance.
* Mettez à jour votre application pour enregistrer l’extension Places.
* Implémentez le suivi de la géolocalisation à partir du service Places dans votre application.


## Configuration

Pour que le service Places fonctionne dans votre application et dans Mobile SDK, vous devez effectuer une configuration.

### Définir les emplacements

Vous définissez certains points d’intérêt dans le service Places.

1. Dans l’interface utilisateur de collecte de données, sélectionnez **[!UICONTROL Emplacements]**.
1. Sélectionnez ![Plus](https://spectrum.adobe.com/static/icons/workflow_18/Smock_MoreSmallList_18_N.svg).
1. Dans le menu contextuel, sélectionnez **[!UICONTROL Gérer les bibliothèques]**.
   ![Gestion des bibliothèques](assets/places-manage-libraries.png){zoomable="yes"}
1. Dans la boîte de dialogue **[!UICONTROL Gérer les bibliothèques]**, sélectionnez **[!UICONTROL Nouveau]**.
1. Dans la boîte de dialogue **[!UICONTROL Créer une bibliothèque]** saisissez un **[!UICONTROL Nom]**, par exemple `Luma`.
1. Sélectionnez **[!UICONTROL Confirmer]**.
   ![Créer une bibliothèque](assets/places-create-library.png){zoomable="yes"}
1. Pour fermer la boîte de dialogue **[!UICONTROL Gérer les bibliothèques]**, sélectionnez **[!UICONTROL Fermer]**.
1. De retour dans **[!UICONTROL Gestion des POI]**, sélectionnez **[!UICONTROL Importer des POI]**.
1. Sélectionnez **[!UICONTROL Démarrer]** dans la boîte de dialogue **[!UICONTROL Importer des emplacements]**.
1. Sélectionnez **[!DNL Luma]** dans la liste des bibliothèques,
1. Sélectionnez **[!UICONTROL Suivant]**.
   ![Sélectionner une bibliothèque](assets/places-import-select-library.png){zoomable="yes"}
1. Téléchargez le fichier ZIP des points d’intérêt [Luma](assets/luma_pois.csv.zip) et extrayez-le à un emplacement de votre ordinateur.
1. Dans la boîte de dialogue **[!UICONTROL Importer des emplacements]**, faites glisser et déposez le fichier `luma_pois.csv` extrait sur **[!UICONTROL Choisir un fichier CSV - Faites glisser et déposez votre fichier]**. Vous devriez voir **[!UICONTROL Succès de la validation]** - **[!UICONTROL Le fichier CSV a été validé avec succès]**.
1. Sélectionnez **[!UICONTROL Démarrer l’importation]**. Vous devriez voir **[!UICONTROL Succès]** - **[!UICONTROL 6 nouveaux points d’intérêt ajoutés avec succès]**.
1. Sélectionnez **[!UICONTROL Terminé]**.
1. Dans **[!UICONTROL Gestion des points d’intérêt]**, vous devriez voir que six nouveaux magasins Luma sont ajoutés à la liste. Vous pouvez basculer entre la vue de carte ![Liste](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ViewList_18_N.svg) et ![Carte](https://spectrum.adobe.com/static/icons/workflow_18/Smock_MapView_18_N.svg).
   ![Liste des lieux](assets/places-list.png){zoomable="yes"}.


### Installer l’extension Places

1. Accédez à **[!UICONTROL Balises]** recherchez la propriété de balise mobile et ouvrez la propriété.
1. Sélectionnez **[!UICONTROL Extensions]**.
1. Sélectionnez **[!UICONTROL Catalogue]**.
1. Recherchez l’extension **[!UICONTROL Places]**.
1. Installez l’extension .

   ![Ajouter des emplacements](assets/tag-places-extension.png)

1. Dans la boîte de dialogue **[!UICONTROL Installer l’extension]** :
   1. Sélectionnez **[!DNL Luma]** dans la liste **[!UICONTROL Sélectionner une bibliothèque]**.
   1. Assurez-vous d’avoir choisi votre bibliothèque de travail, par exemple **[!UICONTROL Version initiale]**.
   1. Sélectionnez **[!UICONTROL Enregistrer dans la bibliothèque et créer]** dans **[!UICONTROL Enregistrer dans la bibliothèque]**.
      ![Installer l’extension Places](assets/places-install-extension.png){zoomable="yes"}.

1. Votre bibliothèque est reconstruite.


### Vérification du schéma

Vérifiez si votre schéma, tel que défini dans [Créer un schéma](create-schema.md), incorpore les groupes et classes de champs nécessaires pour collecter les données de point d’intérêt et de géolocalisation.

1. Accédez à l’interface de collecte de données et sélectionnez **[!UICONTROL Schémas]** dans le rail de gauche.
1. Sélectionnez **[!UICONTROL Parcourir]** dans la barre supérieure.
1. Sélectionnez votre schéma pour l’ouvrir.
1. Dans l’éditeur de schémas, sélectionnez **[!UICONTROL Événement d’expérience client]**.
1. Un objet **[!UICONTROL placeContext]** contenant l’objet et les champs permettant de capturer les données d’interaction avec le point d’intérêt et de géolocalisation s’affiche.
   ![Emplacements du schéma](assets/schema-places-context.png){zoomable="yes"}.


### Mettre à jour la propriété de balise

L’extension Places pour les balises offre la fonctionnalité de surveillance des événements de géolocalisation et vous permet de déclencher des actions en fonction de ces événements. Vous pouvez utiliser cette fonctionnalité pour minimiser le codage d’API que vous devez implémenter dans l’application.

**Éléments de données**

Vous devez d’abord créer plusieurs éléments de données.

1. Accédez à la propriété de balise dans l’interface utilisateur de collecte de données.
1. Sélectionnez **[!UICONTROL Éléments de données]** dans le rail de gauche.
1. Sélectionnez **[!UICONTROL Ajouter un élément de données]**.
1. Dans l’écran **[!UICONTROL Créer un élément de données]**, saisissez un nom, par exemple `Name - Entered`.
1. Sélectionnez **[!UICONTROL Places]** dans la liste **[!UICONTROL Extension]**.
1. Sélectionnez **[!UICONTROL Nom]** dans la liste **[!UICONTROL Type d’élément de données]**.
1. Sélectionnez **[!UICONTROL POI actuel]** sous **[!UICONTROL TARGET]**.
1. Sélectionnez **[!UICONTROL Enregistrer dans la bibliothèque]**.
   ![Élément de données](assets/tags-create-data-element.png){zoomable="yes"}

1. Répétez les étapes 4 à 8 à l’aide des informations du tableau ci-dessous, pour créer des éléments de données supplémentaires.

   | Nom | Extension | Type d’élément de données | CIBLE |
   |---|---|---|---|
   | `Name - Exited` | Places | Nom | Dernier POI quitté |
   | `Category - Current` | Places | Catégorie | Point ciblé actuel |
   | `Category - Exited` | Places | Catégorie | Dernier POI quitté |
   | `City - Current` | Places | Ville | Point ciblé actuel |
   | `City - Exited` | Places | Ville | Dernier POI quitté |

   Vous devriez disposer de la liste suivante d’éléments de données.

   ![Liste des éléments de données](assets/tags-data-elements-list.png){zoomable="yes"}

**Règles**

Vous allez maintenant définir des règles pour travailler avec ces éléments de données.

1. Dans la propriété de balise, sélectionnez **[!UICONTROL Règles]** dans le rail de gauche.
1. Sélectionnez **[!UICONTROL Ajouter une règle]**.
1. Dans l’écran **[!UICONTROL Créer une règle]**, saisissez le nom de la règle, par exemple `POI - Entry`.
1. Sélectionnez ![Ajouter](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) sous **[!UICONTROL ÉVÉNEMENTS]**.
   1. Sélectionnez **[!UICONTROL Places]** dans la liste **[!UICONTROL Extension]** et sélectionnez **[!UICONTROL Saisir un point d’intérêt]** dans la liste **[!UICONTROL Type d’événement]**.
   1. Sélectionnez **[!UICONTROL Conserver les modifications]**.
      ![Événement de balise](assets/tags-event-mobile-core.png).
1. Sélectionnez ![Ajouter](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) sous **[!UICONTROL ACTIONS]**.
   1. Sélectionnez **[!UICONTROL Mobile Core]** dans la liste **[!UICONTROL Extension]**, sélectionnez **[!UICONTROL Joindre les données]** dans **[!UICONTROL Type d’action]**. Cette action joint des données de payload.
   1. Dans la **[!UICONTROL Payload JSON]**, collez la payload suivante :

      ```json
      {
          "xdm": {
              "eventType": "location.entry",
              "placeContext": {
                  "geo": {
                      "city": "{%%City - Current%%}"
                  },
                  "POIinteraction": {
                      "poiDetail": {
                          "name": "{%%Name - Current%%}",
                          "category": "{%%Category - Current%%}"
                      },
                      "poiEntries": {
                          "value": 1
                      }
                  }
              }
          }
      }
      ```

      Vous pouvez également insérer `{%% ... %%}` valeurs d’espace réservé d’élément de données dans le fichier JSON en sélectionnant le ![Data](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Data_18_N.svg). Une boîte de dialogue contextuelle vous permet de sélectionner n’importe quel élément de données que vous avez créé.

   1. Sélectionnez **[!UICONTROL Conserver les modifications]**.
      ![Action des balises](assets/tags-action-mobile-core.png){zoomable="yes"}

1. Sélectionnez ![Ajouter](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) en regard de l’action **[!UICONTROL Mobile Core - Joindre des données]**.
   1. Sélectionnez **[!UICONTROL Adobe Experience Platform Edge Network]** dans la liste **[!UICONTROL Extension]** et sélectionnez **[!UICONTROL Transférer l’événement vers Edge Network]**. Cette action garantit que l’événement et les données de payload supplémentaires sont transférés vers Platform Edge Network.
   1. Sélectionnez **[!UICONTROL Conserver les modifications]**.

1. Pour enregistrer la règle, sélectionnez **[!UICONTROL Enregistrer dans la bibliothèque]**.

   ![Règle ](assets/tags-rule-poi-entry.png){zoomable="yes"}

Créons une autre règle

1. Dans l’écran **[!UICONTROL Créer une règle]**, saisissez le nom de la règle, par exemple `POI - Exit`.
1. Sélectionnez ![Ajouter](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) sous **[!UICONTROL ÉVÉNEMENTS]**.
   1. Sélectionnez **[!UICONTROL Places]** dans la liste **[!UICONTROL Extension]**, puis sélectionnez **[!UICONTROL Quitter le POI]** dans la liste **[!UICONTROL Type d’événement]**.
   1. Sélectionnez **[!UICONTROL Conserver les modifications]**.
1. Sélectionnez ![Ajouter](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) sous **[!UICONTROL ACTIONS]**.
   1. Sélectionnez **[!UICONTROL Mobile Core]** dans la liste **[!UICONTROL Extension]**, sélectionnez **[!UICONTROL Joindre les données]** dans la liste **[!UICONTROL Type d’action]**.
   1. Dans la **[!UICONTROL Payload JSON]**, collez la payload suivante :

      ```json
      {
          "xdm": {
              "eventType": "location.exit",
              "placeContext": {
                  "geo": {
                      "city": "{%%City - Exited%%}"
                  },
                  "POIinteraction": {
                      "poiExits": {
                          "value": 1
                      },
                      "poiDetail": {
                          "name": "{%%Name - Exited%%}",
                          "category": "{%%Category - Exited%%}"
                      }
                  }
              }
          }
      }
      ```

   1. Sélectionnez **[!UICONTROL Conserver les modifications]**.

1. Sélectionnez ![Ajouter](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) en regard de l’action **[!UICONTROL Mobile Core - Joindre des données]**.
   1. Sélectionnez **[!UICONTROL Adobe Experience Platform Edge Network]** dans la liste **[!UICONTROL Extension]** et sélectionnez **[!UICONTROL Transférer l’événement vers Edge Network]**.
   1. Sélectionnez **[!UICONTROL Conserver les modifications]**.

1. Pour enregistrer la règle, sélectionnez **[!UICONTROL Enregistrer dans la bibliothèque]**.

   ![Règle ](assets/tags-rule-poi-exit.png){zoomable="yes"}


Pour vous assurer que toutes les modifications apportées à votre balise sont publiées :

1. Sélectionnez **[!UICONTROL Version initiale]** comme bibliothèque à créer.
1. Sélectionnez **[!UICONTROL Créer]**.
   ![Bibliothèque de build](assets/tags-build-library.png){zoomable="yes"}




## Validation de la configuration dans Assurance

Pour valider votre configuration dans Assurance :

1. Accédez à l’interface utilisateur d’Assurance.
1. S’il n’est pas déjà disponible dans le rail de gauche, sélectionnez **[!UICONTROL Configurer]** dans le rail de gauche et sélectionnez ![Ajouter](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) en regard de **[!UICONTROL Événements]** et **[!UICONTROL Mapper et simuler]** sous **[!UICONTROL SERVICE PLACES]**.
1. Sélectionnez **[!UICONTROL Enregistrer]**.
1. Sélectionnez **[!UICONTROL Mapper et simuler]** dans le rail de gauche.
1. Déplacez la carte vers un emplacement de l’un de vos points d’intérêt.
1. Sélectionnez ![Engrenage](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Gears_18_N.svg) Simuler des points d’intérêt de chargement. Votre point d’intérêt est identifié à l’aide d’un cercle et d’une épingle.
1. Sélectionnez votre point d’intérêt.
1. Dans la fenêtre contextuelle, sélectionnez ![Engrenage](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Gears_18_N.svg) **[!UICONTROL Simuler un événement d’entrée]**.

   ![Simuler un événement d’entrée](assets/places-simulate.png){zoomable="yes"}

1. Sélectionnez **[!UICONTROL Événements]** dans le rail de gauche pour afficher les événements que vous avez simulés.

   ![Validation d&#39;AJO Decisioning](assets/places-events.png){zoomable="yes"}


## Implémentation de Places dans votre application

Comme nous l’avons vu dans les leçons précédentes, l’installation d’une extension de balise mobile fournit uniquement la configuration . Vous devez ensuite installer et enregistrer Places SDK. Si ces étapes ne sont pas claires, consultez la section [Installation des SDK](install-sdks.md).

>[!NOTE]
>
>Si vous avez terminé la section [Installation des SDK](install-sdks.md), Places SDK est déjà installé et vous pouvez ignorer cette étape.
>

>[!IMPORTANT]
>
>Pour configurer Maps SDK pour Android dans votre application, vous devez configurer la facturation en fonction des coûts d’acquisition liés à l’utilisation. Vous pouvez limiter les coûts à l’aide de votre ID d’application unique et d’une clé SHA-1. Pour plus d’informations, voir [Mappage de SDK pour Android](https://developers.google.com/maps/documentation/android-sdk/overview). Si vous ne souhaitez pas configurer de facturation ni engager de coûts, ignorez cette leçon.

>[!BEGINTABS]

>[!TAB iOS]

1. Dans Xcode, assurez-vous que [AEP Places](https://github.com/adobe/aepsdk-places-ios) est ajouté à la liste des packages dans les dépendances de packages. Voir [Gestionnaire de packages Swift](install-sdks.md#swift-package-manager).
1. Accédez à **[!DNL Luma]** > **[!DNL Luma]** > **[!DNL AppDelegate]** dans le navigateur de projet Xcode.
1. Assurez-vous que `AEPPlaces` fait partie de votre liste d’importations.

   ```swift
   import AEPPlaces
   ```

1. Assurez-vous que `Places.self` fait partie du tableau d’extensions que vous enregistrez.

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

1. Accédez à **[!DNL Luma]** > **[!DNL Luma]** > **[!DNL Utils]** > **[!UICONTROL MobileSDK]** dans le navigateur de projet Xcode et recherchez la fonction `func processRegionEvent(regionEvent: PlacesRegionEvent, forRegion region: CLRegion) async`. Ajoutez le code suivant :

   ```swift
   // Process geolocation event
   Places.processRegionEvent(regionEvent, forRegion: region)
   ```

   Cette API [`Places.processRegionEvent`](https://developer.adobe.com/client-sdks/documentation/places/api-reference/#processregionevent) communique les informations de géolocalisation au service Places.

1. Accédez à **[!DNL Luma]** > **[!DNL Luma]** > **[!DNL Views]** > **[!DNL Location]** > **[!DNL GeofenceSheet]** dans le navigateur de projet de Xcode.

   1. Pour le bouton Entrée , saisissez le code suivant :

      ```swift
      // Simulate geofence entry event
      Task {
          await MobileSDK.shared.processRegionEvent(regionEvent: .entry, forRegion: region)
      }
      ```

   1. Pour le bouton Quitter , saisissez le code suivant :

      ```swift
      // Simulate geofence exit event
      Task {
          await MobileSDK.shared.processRegionEvent(regionEvent: .exit, forRegion: region)
      }
      ```

>[!TAB Android]

1. Dans Android Studio, assurez-vous que [aepsdk-places-android](https://github.com/adobe/aepsdk-places-android) fait partie des dépendances dans **[!UICONTROL build.gradle.kts (module :app)]** dans **[!UICONTROL Android]** ![ChevronDown](/help/assets/icons/ChevronDown.svg) **[!UICONTROL Scripts Gradle]**. Voir [Gradle](install-sdks.md#gradle).
1. Accédez à **[!UICONTROL Android]** ![ChevronDown](/help/assets/icons/ChevronDown.svg) > **[!DNL app]** > **[!DNL kotlin+java]** > **[!UICONTROL com.adobe.luma.tutorial.android]** > **[!UICONTROL LumaApplication]** dans le navigateur de projet Android Studio.
1. Assurez-vous que `com.adobe.marketing.mobile.Messaging` fait partie de votre liste d’importations.

   `import import com.adobe.marketing.mobile.Places`

1. Assurez-vous que `Places.EXTENSION` fait partie du tableau d’extensions que vous enregistrez.

   ```kotlin
   val extensions = listOf(
       Identity.EXTENSION,
       Lifecycle.EXTENSION,
       Signal.EXTENSION,
       Edge.EXTENSION,
       Consent.EXTENSION,
       UserProfile.EXTENSION,
       Places.EXTENSION,
       Messaging.EXTENSION,
       Optimize.EXTENSION,
       Assurance.EXTENSION
   )
   ```

1. Accédez à **[!UICONTROL Android]** ![ChevronDown](/help/assets/icons/ChevronDown.svg) > **[!DNL app]** > **[!DNL kotlin+java]** > **[!UICONTROL com.adobe.luma.tutorial.android]** > **[!UICONTROL models]** > **[!UICONTROL MobileSDK]** dans le navigateur de projet Android Studio. Recherchez la fonction `suspend fun processGeofence(geofence: Geofence?, transitionType: Int)`. Ajoutez le code suivant :

   ```kotlin
   // Process geolocation event
   Places.processGeofence(geofence, transitionType)
   ```

   Cette API [`Places.processRegionEvent`](https://developer.adobe.com/client-sdks/documentation/places/api-reference/#processregionevent) communique les informations de géolocalisation au service Places.


1. Accédez à **[!UICONTROL Android]** ![ChevronDown](/help/assets/icons/ChevronDown.svg) > **[!DNL app]** > **[!DNL kotlin+java]** > **[!UICONTROL com.adobe.luma.tutorial.android]** > **[!UICONTROL views]** > **[!UICONTROL LocationView.k]** dans le navigateur de projet Android Studio.

   1. Pour le bouton Entrée , saisissez le code suivant :

      ```kotlin
      // Simulate geofence entry event
      coroutineScope.launch {
          MobileSDK.shared.processGeofence(
             region,
             Geofence.GEOFENCE_TRANSITION_ENTER
          )
      }
      ```

   1. Pour le bouton Quitter , saisissez le code suivant :

      ```kotlin
      // Simulate geofence entry event
      coroutineScope.launch {
          MobileSDK.shared.processGeofence(
              region,
              Geofence.GEOFENCE_TRANSITION_EXIT
          )
      }
      ```

>[!ENDTABS]

## Validation à l’aide de l’application

Pour valider les fonctionnalités de géolocalisation dans votre application :

>[!BEGINTABS]

>[!TAB iOS]

1. Ouvrez votre application sur un appareil ou dans le simulateur.

1. Accédez à l’onglet **[!UICONTROL Emplacement]**.

1. Déplacez (faites glisser) la carte pour vous assurer que le cercle bleu du milieu se trouve au-dessus de l’un de vos points d’intérêt, par exemple Londres.

1. Appuyer <img src="assets/geobutton.png" width="20" /> jusqu’à ce que la catégorie et le nom apparaissent dans l’étiquette à l’emplacement rouge avec l’épingle.

1. Appuyez sur l’étiquette du point d’intérêt, ce qui ouvre la feuille **[!UICONTROL Point d’intérêt voisin]**.

   <img src="assets/appgeolocation.png" width="300" />

1. Appuyez sur les boutons **[!UICONTROL Entrée]** ou **[!UICONTROL Sortie]** pour simuler des événements d’entrée et de sortie de limite géographique à partir de l’application.

   <img src="assets/appentryexit.png" width="300" />

1. Vous devriez voir les événements dans l’interface utilisateur d’Assurance. À la fois dans les événements et dans les événements du service Places.

>[!TAB Android]

1. Accédez à l’onglet **[!UICONTROL Emplacement]**.

1. Sélectionnez **[!UICONTROL Utiliser et/ou simuler des limites géographiques]**.

1. Appuyez quelque part dans le cercle rouge qui s’affiche.

   <img src="assets/appgeolocation-android.png" width="300" />


1. Appuyez sur les boutons **[!UICONTROL Entrée]** ou **[!UICONTROL Sortie]** pour simuler des événements d’entrée et de sortie de limite géographique à partir de l’application.

   <img src="assets/appentryexit-android.png" width="300" />

1. Vous devriez voir les événements dans l’interface utilisateur d’Assurance.


>[!ENDTABS]



## Étapes suivantes

Vous devriez maintenant disposer de tous les outils nécessaires pour commencer à ajouter d’autres fonctionnalités à votre fonctionnalité de géolocalisation dans l’application. Après avoir transféré les événements vers Edge Network, une fois que vous avez configuré l’application pour [Experience Platform](platform.md), les événements d’expérience doivent apparaître pour le profil utilisé dans l’application.

Dans la section Journey Optimizer de ce tutoriel, vous pouvez voir que les événements d’expérience peuvent être utilisés pour déclencher des parcours (voir [notification push](journey-optimizer-inapp.md) et [messagerie in-app](journey-optimizer-push.md) avec Journey Optimizer). Par exemple, l’exemple habituel d’envoi d’une notification push à l’utilisateur de votre application avec une promotion de produit lorsque cet utilisateur accède à la limite géographique d’un magasin physique.

Cette implémentation de la fonctionnalité de géolocalisation de votre application réduit le code. Le service Places, les éléments de données et les règles que vous avez définis dans la propriété de balise fournissent la plupart des fonctionnalités. Vous pouvez également implémenter la même fonctionnalité directement dans votre application à l’aide de l’API [`Edge.sendEvent`](https://developer.adobe.com/client-sdks/documentation/edge-network/api-reference/#sendevent) (voir [Événements](events.md) pour plus d’informations) avec une payload XDM contenant un objet `placeContext` renseigné.

>[!SUCCESS]
>
>Vous avez maintenant activé l’application pour les services de géolocalisation à l’aide de l’extension Places dans Experience Platform Mobile SDK.
>
>Merci d’avoir consacré votre temps à découvrir Adobe Experience Platform Mobile SDK. Si vous avez des questions, souhaitez partager des commentaires généraux ou des suggestions sur le contenu futur, partagez-les dans ce [article de discussion de la communauté Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796).

Suivant : **[Mapper des données à Adobe Analytics](analytics.md)**
