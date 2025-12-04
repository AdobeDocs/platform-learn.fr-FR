---
title: Implémentation de Brand Concierge à l’aide de balises de collecte de données
description: Implémentation de Brand Concierge à l’aide de balises de collecte de données
kt: 5342
doc-type: tutorial
source-git-commit: 3704abb57e9fa64c2ff6d6914b6da8b46a5f44aa
workflow-type: tm+mt
source-wordcount: '433'
ht-degree: 6%

---

# 1.4.3 Implémentation de Brand Concierge à l’aide de balises de collecte de données

>[!IMPORTANT]
>
>Cet exercice est en cours de réalisation et n&#39;est pas encore terminé.

## Propriété des balises de la collecte de données

Brand Concierge doit envoyer des données à Adobe Experience Platform. Pour ce faire, Web SDK (ou alloy.js) doit être déployé sur votre site web.

Pour ce faire, vous devez maintenant créer une propriété Balises de collecte de données.

Accédez à [https://experience.adobe.com/](https://experience.adobe.com/){target="_blank"}. Ouvrez **Collecte de données**.

![Brand Concierge](./images/aep101.png)

Cliquez sur **Nouvelle propriété**.

![Brand Concierge](./images/aep102.png)

Saisissez le nom : `--aepUserLdap-- - CitiSignal Website + Brand Concierge` et saisissez également le domaine de votre site web.

Cliquez sur **Enregistrer**.

![Brand Concierge](./images/aep103.png)

Recherchez votre propriété, puis ouvrez-la.

![Brand Concierge](./images/aep104.png)

Accédez à **Extensions** puis à **Catalogue**.

![Brand Concierge](./images/aep105.png)

Recherchez `web sdk`, puis cliquez sur l’extension **Adobe Experience Platform Web SDK**. Cliquez sur **Installer**.

![Brand Concierge](./images/aep106.png)

Vous devriez alors voir ceci. Il vous suffit de fournir les détails de votre flux de données ici. Pour ce faire, faites défiler l’écran vers le bas.

![Brand Concierge](./images/aep107.png)

Pour les 3 environnements **de production**, **d’évaluation** et **de développement**, sélectionnez les éléments suivants :

- **Sandbox** : `--aepUserLdap-- - bc`
- **Flux de données** : `--aepUserLdap-- - Brand Concierge`

Cliquez sur **Enregistrer**.

![Brand Concierge](./images/aep108.png)

Vous devriez alors voir ceci. Accédez à **Règles**.

![Brand Concierge](./images/aep108a.png)

Cliquez sur **Créer une règle**.

![Brand Concierge](./images/aep109.png)

Saisissez le nom : `Homepage`. Cliquez ensuite sur **+ Ajouter** sous **ÉVÉNEMENTS**.

![Brand Concierge](./images/aep110.png)

Sélectionnez les options suivantes :

- **Extension** : **Core**
- **Type D’Événement** : **Bibliothèque Chargée (Haut De Page)**

Cliquez sur **Conserver les modifications**.

![Brand Concierge](./images/aep111.png)

Vous devriez alors voir ceci. Cliquez sur **+ Ajouter** sous **CONDITIONS**.

![Brand Concierge](./images/aep112.png)

Sélectionnez les options suivantes :

- **Type de logique** : **Standard**
- **Extension** : **Core**
- **Type De Condition** : **Chemin Sans Chaîne De Requête**
- **chemin égal à ...** : saisissez le domaine de votre site web, ici `https://vangeluw.adobedemosystem.com/`

Cliquez sur **Conserver les modifications**.

![Brand Concierge](./images/aep113.png)

Vous devriez alors voir ceci. Cliquez sur **+ Ajouter** sous **ACTIONS**.

![Brand Concierge](./images/aep114.png)

Sélectionnez les options suivantes :

- **Extension** : **Core**
- **Type d’action** : **Code personnalisé**
- **Langue** : **JavaScript**

Cliquez sur **Ouvrir l’éditeur**.

![Brand Concierge](./images/aep115.png)

Collez le code suivant :

```javascript
window["alloy"]("sendEvent", {
        conversation: {fetchConversationalExperience: true}
    }).then(result=> {
        console.log("Conversation experience fetched", result);
        window["alloy"]("bootstrapConversationalExperience", {
            selector: "#brand-concierge-mount",
						// src: "main.js",
            src: "https://experience-stage.adobe.net/solutions/experience-platform-brand-concierge-web-agent/static-assets/main.js",
            stylingConfigurations: window.styleConfiguration,
						stickySession: true
        })
    });
```

Cliquez sur **Enregistrer**.

![Brand Concierge](./images/aep116.png)

Vous devriez alors voir ceci. Cliquez sur **Conserver les modifications**.

![Brand Concierge](./images/aep117.png)

Vous devriez alors voir ceci. Cliquez sur **Enregistrer**.

![Brand Concierge](./images/aep118.png)

Accédez à **Flux de publication**. Cliquez sur **Ajouter une bibliothèque**.

![Brand Concierge](./images/aep119.png)

Saisissez le nom : `Dev`, sélectionnez **Développement (développement)** pour l’environnement, puis cliquez sur **Ajouter toutes les ressources modifiées**.

Cliquez sur **Enregistrer et générer pour le développement**.

![Brand Concierge](./images/aep120.png)

Après quelques minutes, votre bibliothèque sera construite. Attendez de voir le **point vert** à côté de **Dev**. Accédez ensuite à **Environnements**.

![Brand Concierge](./images/aep121.png)

Cliquez sur l’icône **Installer** de l’environnement **Développement**.

![Brand Concierge](./images/aep122.png)

Vous devriez alors voir ceci. Cliquez sur le bouton **copier** pour copier le chemin d’accès de votre bibliothèque. Vous devrez implémenter cette fonction sur votre site web.

Le chemin d’accès à la bibliothèque doit se présenter comme suit :
`<script src="https://assets.adobedtm.com/XXXXXXX/XXXXXXXX/launch-XXXXXXXXX-development.min.js" async></script>`

![Brand Concierge](./images/aep123.png)

Revenir à [Brand Concierge](./brandconcierge.md){target="_blank"}

[Revenir à tous les modules](./../../../overview.md){target="_blank"}