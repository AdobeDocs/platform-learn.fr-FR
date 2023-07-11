---
title: Configuration d’Assurance
description: Découvrez comment mettre en oeuvre l’extension Assurance dans une application mobile.
feature: Mobile SDK,Assurance
exl-id: e15774b2-2f52-400f-9313-bb4338a88918
source-git-commit: adbe8f4476340abddebbf9231e3dde44ba328063
workflow-type: tm+mt
source-wordcount: '585'
ht-degree: 5%

---

# Assurance

Découvrez comment configurer Adobe Experience Platform Assurance dans une application mobile.

L’assurance, officiellement appelée Projet Griffon, est conçue pour vous aider à inspecter, tester, simuler et valider la manière dont vous collectez des données ou diffusez des expériences dans votre application mobile.

Assurance vous aide à inspecter les événements SDK bruts générés par le SDK Mobile Adobe Experience Platform. Tous les événements collectés par le SDK sont disponibles pour inspection. Les événements du SDK sont chargés en mode Liste, triés par heure. Chaque événement dispose d’une vue détaillée qui fournit des détails supplémentaires. Des vues supplémentaires sur la configuration du SDK, les éléments de données, les états partagés et les versions de l’extension du SDK sont également fournies. En savoir plus sur les [Assurance](https://experienceleague.adobe.com/docs/experience-platform/assurance/home.html?lang=fr) dans la documentation du produit.


## Conditions préalables

* Création et exécution réussie de l’exemple d’application avec les SDK installés et configurés.

## Objectifs d&#39;apprentissage

Dans cette leçon, vous allez :

* Vérifiez que votre entreprise a accès à (et demandez-le si ce n’est pas le cas).
* Configurez votre URL de base.
* Ajoutez le code spécifique à iOS requis.
* Connectez-vous à une session.

## Confirmer l’accès

Vérifiez que votre entreprise a accès à Assurance en procédant comme suit :

1. Visite [https://experience.adobe.com/#/assurance](https://experience.adobe.com/griffon){target="_blank"}
1. Connectez-vous à l’aide de vos informations d’identification Adobe ID pour l’Experience Cloud.
1. Si vous êtes amené à la variable **[!UICONTROL Sessions]** puis vous avez accès. Si vous accédez à la page d’accès bêta, sélectionnez **[!UICONTROL Enregistrer]**.

## Implémenter

Outre le [Installation du SDK](install-sdks.md) Si vous avez terminé la leçon précédente, iOS requiert également l’ajout suivant. Ajoutez le code suivant au `AppDelegate.swift` fichier :

```swift
func application(_ app: UIApplication, open url: URL, options: [UIApplication.OpenURLOptionsKey: Any] = [:]) -> Bool {
    Assurance.startSession(url: url)
    return true
}
```

L’exemple de Luma fourni pour ce tutoriel utilise iOS 12.0. Si vous suivez votre propre application basée sur les scènes à l’aide d’iOS 13 et versions ultérieures, utilisez le `UISceneDelegate's scene(_:openURLContexts:)` comme suit :

```swift
func scene(_ scene: UIScene, openURLContexts URLContexts: Set<UIOpenURLContext>) {
    // Called when the app in background is opened with a deep link.
    if let deepLinkURL = URLContexts.first?.url {
        Assurance.startSession(url: deepLinkURL)
    }
}
```

Vous trouverez plus d’informations [ici](https://developer.adobe.com/client-sdks/documentation/platform-assurance-sdk/api-reference/){target="_blank"}.

## Configuration d’une URL de base

1. Ouvrez XCode et sélectionnez le nom du projet.
1. Accédez au **Infos** .
1. Faites défiler jusqu’à **Types d’URL** et sélectionnez la variable **+** pour en ajouter un nouveau.
1. Définir **Identifiant** et **Modèles d’URL** à &quot;lumadeeplink&quot;.
1. Créez et exécutez l’application.

![url d&#39;assurance](assets/mobile-assurance-url-type.png)

Pour en savoir plus sur les schémas d’URL dans iOS, consultez [Documentation Apple](https://developer.apple.com/documentation/xcode/defining-a-custom-url-scheme-for-your-app){target="_blank"}.

L’assurance s’exécute en ouvrant une URL, soit via un navigateur, soit via le code QR, cette URL commence par l’URL de base qui ouvre l’application et contient des paramètres supplémentaires. Ces paramètres uniques sont utilisés pour connecter la session.

## Connexion à une session

1. Accédez au [Interface utilisateur d’Assurance](https://experience.adobe.com/griffon){target="_blank"}.
1. Sélectionner **[!UICONTROL Créer une session]**.
1. Fournir **[!UICONTROL Nom de la session]** par exemple `Luma App QA` et le **[!UICONTROL URL de base]** `lumadeeplink://default`
1. Sélectionnez **[!UICONTROL Suivant]**.
   ![création d’une session d’assurance](assets/mobile-assurance-create-session.png)
1. **[!UICONTROL Analyser le code QR]** si vous utilisez un appareil physique. Si vous utilisez le simulateur, alors **[!UICONTROL Copier le lien]** et ouvrez-le avec Safari dans le simulateur.
   ![code qa d’assurance](assets/mobile-assurance-qr-code.png)
1. Lorsque l’application se charge, un modal vous demande de saisir votre code PIN à l’étape précédente.
   ![point d’entrée d’assurance](assets/mobile-assurance-enter-pin.png)
1. Si la connexion a réussi, des événements s’affichent dans l’interface utilisateur web d’assurance et une icône Assurance flottante s’affiche dans l’application.
   * Icône Assurance flottante.
     ![modal d’assurance](assets/mobile-assurance-modal.png)
   * Événements Experience Cloud provenant de l’interface utilisateur web.
     ![événements d’assurance](assets/mobile-assurance-events.png)

Si vous rencontrez des défis, veuillez consulter la section [technique](https://developer.adobe.com/client-sdks/documentation/platform-assurance-sdk/){target="_blank"} and [general documentation](https://experienceleague.adobe.com/docs/experience-platform/assurance/home.html?lang=fr){target="_blank"}.

Suivant : **[Consentement](consent.md)**

>[!NOTE]
>
>Merci d’avoir consacré votre temps à l’apprentissage du SDK Adobe Experience Platform Mobile. Si vous avez des questions, souhaitez partager des commentaires généraux ou avez des suggestions sur le contenu futur, partagez-les à ce sujet. [Article de discussion de la communauté Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796)
