---
title: Consentement
description: Découvrez comment mettre en oeuvre le consentement dans une application mobile.
exl-id: 08042569-e16e-4ed9-9b5a-864d8b7f0216
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '373'
ht-degree: 2%

---

# Consentement

Découvrez comment mettre en oeuvre le consentement dans une application mobile.

L’extension mobile de consentement Adobe Experience Platform permet la collecte des préférences de consentement de votre application mobile lors de l’utilisation du SDK Mobile Adobe Experience Platform et de l’extension Edge Network. En savoir plus sur les [Extension de consentement](https://aep-sdks.gitbook.io/docs/foundation-extensions/consent-for-edge-network), dans la documentation.

## Conditions préalables

* Création et exécution de l’application avec les SDK installés et configurés.

## Objectifs d&#39;apprentissage

Dans cette leçon, vous allez :

* Demandez à l’utilisateur son consentement.
* Mettez à jour l’extension en fonction de la réponse de l’utilisateur.
* Découvrez comment obtenir l’état actuel du consentement.

## Demander le consentement

Si vous avez suivi le tutoriel à partir du début, vous vous souviendrez de la définition de la variable **[!UICONTROL Niveau de consentement par défaut]** à &quot;En attente&quot;. Pour commencer à collecter des données, vous devez obtenir le consentement de l’utilisateur. Dans ce tutoriel, obtenez le consentement en demandant simplement une alerte, dans une application réelle, vous souhaiterez consulter les bonnes pratiques en matière de consentement pour votre région.

1. Vous ne souhaitez demander à l’utilisateur qu’une seule fois. Une façon simple de gérer cela consiste à simplement utiliser `UserDefaults`.
1. Accédez à `Home.swift`.
1. Ajoutez le code suivant à `viewDidLoad()`.

   ```swift
   let defaults = UserDefaults.standard
   let consentKey = "askForConsentYet"
   let hidePopUp = defaults.bool(forKey: consentKey)
   ```

1. Si l’utilisateur n’a pas encore vu l’alerte, affichez-la et mettez à jour le consentement en fonction de sa réponse. Ajoutez le code suivant à `viewDidLoad()`.

   ```swift
   if(hidePopUp == false){
       //Consent Alert
       let alert = UIAlertController(title: "Allow Data Collection?", message: "Selecting Yes will begin data collection", preferredStyle: .alert)
       alert.addAction(UIAlertAction(title: "Yes", style: .default, handler: { action in
           //Update Consent -> "yes"
           let collectConsent = ["collect": ["val": "y"]]
           let currentConsents = ["consents": collectConsent]
           Consent.update(with: currentConsents)
           defaults.set(true, forKey: consentKey)
       }))
       alert.addAction(UIAlertAction(title: "No", style: .cancel, handler: { action in
           //Update Consent -> "no"
           let collectConsent = ["collect": ["val": "n"]]
           let currentConsents = ["consents": collectConsent]
           Consent.update(with: currentConsents)
           defaults.set(true, forKey: consentKey)
       }))
       self.present(alert, animated: true)
   }
   ```


## Obtention de l’état du consentement actuel

L’extension mobile Consent supprimera/mettra/autorisera automatiquement le suivi en fonction de la valeur de consentement actuelle. Vous pouvez également accéder vous-même à l’état actuel du consentement :

1. Accédez à `Home.swift`.
1. Ajoutez le code suivant à `viewDidLoad()`.

```swift
Consent.getConsents{ consents, error in
    guard error == nil, let consents = consents else { return }
    guard let jsonData = try? JSONSerialization.data(withJSONObject: consents, options: .prettyPrinted) else { return }
    guard let jsonStr = String(data: jsonData, encoding: .utf8) else { return }
    print("Consent getConsents: ",jsonStr)
}
```

Dans l’exemple ci-dessus, vous imprimez simplement l’état du consentement sur la console. Dans un scénario réel, vous pouvez l’utiliser pour modifier les menus ou options affichés à l’utilisateur.

## Validation avec Assurance

1. Consultez la section [Assurance](assurance.md) leçon.
1. Installez l’application.
1. Lancez l’application à l’aide de l’URL générée par Assurance.
1. Si vous avez correctement ajouté le code ci-dessus, vous serez invité à fournir votre consentement. Sélectionner **Oui**.
   ![fenêtre contextuelle de consentement](assets/mobile-consent-validate.png)
1. Vous devriez voir une **[!UICONTROL Préférences de consentement mises à jour]** dans l’interface utilisateur d’Assurance.
   ![valider le consentement](assets/mobile-consent-update.png)

Suivant : **[Collecter les données du cycle de vie](lifecycle-data.md)**

>[!NOTE]
>
>Merci d’avoir consacré votre temps à l’apprentissage du SDK Adobe Experience Platform Mobile. Si vous avez des questions, souhaitez partager des commentaires généraux ou avez des suggestions sur le contenu futur, partagez-les à ce sujet. [Article de discussion de la communauté Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-in-mobile/td-p/443796)