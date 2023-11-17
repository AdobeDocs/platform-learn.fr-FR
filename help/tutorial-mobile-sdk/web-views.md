---
title: Gestion des WebViews
description: Découvrez comment gérer la collecte de données avec WebViews dans une application mobile.
jira: KT-6987
exl-id: 9b3c96fa-a1b8-49d2-83fc-ece390b9231c
source-git-commit: bc53cb5926f708408a42aa98a1d364c5125cb36d
workflow-type: tm+mt
source-wordcount: '414'
ht-degree: 0%

---

# Gestion des WebViews

Découvrez comment gérer la collecte de données avec WebViews dans une application mobile.

>[!INFO]
>
> Ce tutoriel sera remplacé par un nouveau tutoriel utilisant un nouvel exemple d’application mobile à la fin novembre 2023.

## Conditions préalables

* Création et exécution de l’application avec les SDK installés et configurés.

## Objectifs d&#39;apprentissage

Dans cette leçon, vous allez :

* Comprenez pourquoi vous devez prendre en compte des considérations spéciales pour les WebViews.
* Comprendre le code requis pour éviter les problèmes de suivi.

## Problèmes de suivi potentiels

Si vous envoyez des données depuis la partie native de l’application et un WebView, chacun génère son propre ID d’Experience Cloud (ECID). Cela se traduit par des accès déconnectés et une augmentation des données sur les visites/visiteurs. Vous trouverez plus d’informations sur l’ECID dans la section [Présentation d’ECID](https://experienceleague.adobe.com/docs/experience-platform/identity/ecid.html?lang=en).

Pour résoudre cette situation indésirable, il est important de transmettre l’ECID de l’utilisateur de la partie native à WebView.

L’extension JavaScript du service d’ID Experience Cloud dans WebView extrait l’ECID de l’URL au lieu d’envoyer une demande d’Adobe d’un nouvel ID. Le service d’ID utilise cet ECID pour effectuer le suivi du visiteur.

## Mise en œuvre

Dans l’exemple d’application Luma, recherchez le `TermsOfService.swift` (dans la variable `Intro-Login_SignUp` ) et recherchez le code suivant :

```swift
// Show tou.html
let url = Bundle.main.url(forResource: "tou", withExtension: "html")
let myRequest = URLRequest(url: url!)
self.webView.load(myRequest)
```

Il s’agit d’un moyen simple de charger un WebView. Dans ce cas, il s’agit d’un fichier local, mais les mêmes concepts s’appliquent aux pages distantes.

Refactorisez le code webview comme illustré ci-dessous :

```swift
let url = Bundle.main.url(forResource: "tou", withExtension: "html")
if var urlString = url?.absoluteString {
    // Adobe Experience Platform - Handle Web View
    AEPEdgeIdentity.Identity.getUrlVariables {(urlVariables, error) in
        if let error = error {
            self.simpleAlert("\(error.localizedDescription)")
            return;
        }

        if let urlVariables: String = urlVariables {
            urlString.append("?" + urlVariables)
        }

        DispatchQueue.main.async {
            self.webView.load(URLRequest(url: URL(string: urlString)!))
        }
        print("Successfully retrieved urlVariables for WebView, final URL: \(urlString)")
    }
} else {
    self.simpleAlert("Failed to create URL for webView")
}
```

Vous pouvez en savoir plus sur les `Identity.getUrlVariables` de l’API [Guide de référence de l’API d’extension Identity for Edge Network](https://developer.adobe.com/client-sdks/documentation/identity-for-edge-network/api-reference/#geturlvariables).

## Validation

Après avoir examiné la variable [instructions de configuration](assurance.md) et connectez votre simulateur ou votre périphérique à Assurance, chargez le WebView et recherchez le `Edge Identity Response URL Variables` de l’événement `com.adobe.griffon.mobile` fournisseur.

Pour charger le WebView, accédez à l’écran d’accueil de l’application Luma, sélectionnez l’icône &quot;Compte&quot;, suivie des &quot;Conditions d’utilisation&quot; dans le pied de page.

Après avoir chargé WebView, sélectionnez l’événement et passez en revue la variable `urlvariables` dans le champ `ACPExtensionEventData` , confirmant que les paramètres suivants sont présents dans l’URL : `adobe_mc`, `mcmid`, et `mcorgid`.

![validation de webview](assets/mobile-webview-validation.png)

Un exemple `urvariables` est visible ci-dessous :

```html
// Original (with escaped characters)
adobe_mc=TS%3D1636526122%7CMCMID%3D79076670946787530005526183384271520749%7CMCORGID%3D7ABB3E6A5A7491460A495D61%40AdobeOrg

// Beautified
adobe_mc=TS=1636526122|MCMID=79076670946787530005526183384271520749|MCORGID=7ABB3E6A5A7491460A495D61@AdobeOrg
```

>[!NOTE]
>
>L’assemblage de visiteurs via ces paramètres d’URL est actuellement pris en charge dans le SDK Web Platform (versions 2.11.0 ou ultérieures) et `VisitorAPI.js`.


Suivant : **[Identité](identity.md)**

>[!NOTE]
>
>Merci d’investir votre temps à apprendre sur le SDK Adobe Experience Platform Mobile. Si vous avez des questions, souhaitez partager des commentaires généraux ou avez des suggestions sur le contenu futur, partagez-les à ce sujet. [Article de discussion de la communauté Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796)