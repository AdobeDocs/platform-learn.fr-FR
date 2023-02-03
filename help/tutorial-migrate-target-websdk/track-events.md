---
title: Suivi des événements | Migration de Target depuis at.js 2.x vers le SDK Web
description: Découvrez comment effectuer le suivi des événements de conversion Adobe Target à l’aide du SDK Web Experience Platform.
source-git-commit: 8209b13b745dbea418003b133a6834825947950e
workflow-type: tm+mt
source-wordcount: '654'
ht-degree: 1%

---


# Suivi des événements de conversion Target à l’aide du SDK Web Platform

Il est possible d’effectuer le suivi des événements de conversion pour Target avec le SDK Web Platform, comme pour at.js. Les événements de conversion se répartissent généralement dans les catégories suivantes :

* Suivi automatique des événements qui ne nécessitent aucune configuration
* Événements de conversion d’achat qui doivent être ajustés en fonction d’une mise en oeuvre recommandée du SDK Web Platform
* Événements de conversion hors achat nécessitant des mises à jour du code

## Comparaison des objectifs

Le tableau suivant compare la manière dont at.js et le SDK Web Platform effectuent le suivi des événements de conversion.

| Objectif de l’activité | Target at.js 2.x | SDK Web de Platform |
|---|---|---|
| Conversion > A affiché une page | Suivi automatiquement. En fonction de la valeur de `context.address.url` dans le payload de la requête at.js. | Suivi automatiquement. En fonction de la valeur de `xdm.web.webPageDetails.URL` dans le `sendEvent` payload |
| Conversion > A affiché une mbox | Suivi avec la demande d’un emplacement de mbox d’affichage ou d’une notification à l’aide de `trackEvent()` ou `sendNotifications()` avec un `type` valeur de `display`. | Suivi avec un SDK Web Platform `sendEvent` avec l’appel `eventType` de `decisioning.propositionDisplay`. |
| Conversion > Cliqué sur un élément | Suivi automatiquement pour les activités basées sur le compositeur d’expérience visuelle. Apparaît comme un appel réseau at.js avec un `notifications` dans le payload de la requête et un `type` valeur de `click`. | Suivi automatiquement pour les activités basées sur le compositeur d’expérience visuelle. Apparaît comme SDK Web Platform `sendEvent` avec l’appel `eventType` de `decisioning.propositionInteract`. |
| Engagement > Pages vues | Suivi automatiquement | Suivi automatiquement |
| Engagement > Temps passé sur le site | Suivi automatiquement | Suivi automatiquement |

<!--
| Revenue > RPV, AOV, or Total Sales | Tracked based on the `orderTotal` parameter values for the specified mbox(es) | Tracked based on the `xdm.commerce.order.priceTotal` values. Its best to use the "any mbox" option in the goal setup. |
| Revenue > Orders | Tracked based on the unique `orderId` parameter values for the specified mbox(es) | Tracked based on the unique values for `xdm.commerce.order.purchaseID`. Its best to use the "any mbox" option in the goal setup. |
| Engagement > Custom Scoring | Tracked with the `mboxPageValue` parameter. Refer to the [dedicated documentation](https://experienceleague.adobe.com/docs/target/using/activities/success-metrics/capture-score.html) for more details. | Tracked with `data.__adobe.target.mboxPageValue` in the `sendEvent` payload |
-->

## Événements automatiquement suivis

Les objectifs de conversion suivants ne nécessitent aucun ajustement spécifique à votre mise en oeuvre :

* Conversion > A affiché une page
* Conversion > Cliqué sur un élément
* Engagement > Pages vues
* Engagement > Temps passé sur le site

>[!NOTE]
>
>Le SDK Web Platform permet un meilleur contrôle des valeurs transmises dans le payload de requête. Pour vous assurer que les fonctionnalités de Target telles que les URL AQ et les objectifs de conversion &quot;A affiché une page&quot; fonctionnent correctement, vérifiez que la variable `xdm.web.webPageDetails.URL` contient l’URL de la page entière avec la casse de caractères appropriée.

<!--
## Purchase conversion events

The following conversion goals are based on the order details information passed in the Platform Web SDK `sendEvent` payload:

* Revenue > Revenue per Visit (RPV)
* Revenue > Average Order Value (AOV)
* Revenue > Total Sales
* Revenue > Orders

Target at.js implementations typically use an order confirmation mbox with the `trackEvent()` or `sendNotifications()` functions to pass the order ID, order total, and a list of product IDs purchased. These methods are specific to Target.

The Platform Web SDK is a shared library for all Adobe applications and you may have other applications such as Adobe Analytics to consider. Because of this shared nature, its best send a single order confirmation call using the appropriate commerce XDM field group.

For more information and an example, refer to the tutorial section about [sending purchase parameters to Target](send-parameters.md#purchase-parameters). 
-->

## Événements suivis personnalisés

Les implémentations de Target utilisent généralement des événements de conversion personnalisés pour effectuer le suivi des clics pour les activités d’après les formulaires, indiquer une conversion dans un flux ou transmettre des paramètres sans demander de nouveau contenu.

Le tableau ci-dessous décrit l’approche d’at.js et l’équivalent du SDK Web Platform pour quelques cas d’utilisation de suivi de conversion courants.

| Cas d’utilisation | Target at.js 2.x | SDK Web de Platform |
|---|---|---|
| Suivi d’un événement de conversion de clics pour un emplacement de mbox (portée) | Exécuter `trackEvent()` ou `sendNotifications()` avec un `type` valeur de `click` pour un emplacement de mbox spécifique | Exécuter une `sendEvent` avec un type d’événement `decisioning.propositionInteract` |
| Suivi d’un événement de conversion personnalisé qui peut également inclure des données supplémentaires, telles que des paramètres de profil Target | Exécuter `trackEvent()` ou `sendNotifications()` avec un `type` valeur de `display` pour un emplacement de mbox spécifique | Exécuter une `sendEvent` avec un type d’événement `decisioning.propositionDisplay` |

>[!NOTE]
>
>Bien que `decisioning.propositionDisplay` est le plus souvent utilisé pour incrémenter les impressions pour des portées spécifiques ; il doit également être utilisé comme remplacement direct d’at.js. `trackEvent()` habituellement. Le `trackEvent()` par défaut d’un type de `display` si non spécifié. Vérifiez votre mise en oeuvre pour vous assurer d’utiliser le type d’événement correct pour toutes les conversions personnalisées que vous avez définies.

Pour plus d’informations sur l’utilisation de , reportez-vous à la documentation dédiée d’at.js . [`trackEvent()`](https://developer.adobe.com/target/implement/client-side/atjs/atjs-functions/adobe-target-trackevent/) et [`sendNotifications()`](https://developer.adobe.com/target/implement/client-side/atjs/atjs-functions/adobe-target-sendnotifications-atjs-21/) pour effectuer le suivi des événements Target.

Exemple d’at.js avec `trackEvent()` pour effectuer le suivi d’un clic sur un emplacement de mbox :

```JavaScript
adobe.target.trackEvent({
  "type": "click",
  "mbox": "homepage_hero"
});
```

Avec une mise en oeuvre du SDK Web Platform, vous pouvez effectuer le suivi des événements et des actions de l’utilisateur en appelant le `sendEvent` , renseigner la variable `_experience.decisioning.propositions` Groupe de champs XDM et définition de la variable `eventType` à l’une des deux valeurs suivantes :

* `decisioning.propositionDisplay`: Indique le rendu de l’activité Target.
* `decisioning.propositionInteract`: Indique une interaction de l’utilisateur avec l’activité, comme un clic de souris.

Le `_experience.decisioning.propositions` Le groupe de champs XDM est un tableau d’objets. Les propriétés de chaque objet sont dérivées de la propriété `result.propositions` qui est renvoyé dans la variable `sendEvent` command : `{ id, scope, scopeDetails }`

```JavaScript
alloy("sendEvent", {
  xdm: { ...},
  decisionScopes: ["hero-banner"]
}).then(function (result) {
  var propositions = result.propositions;

  if (propositions) {
    // Find the discount proposition, if it exists.
    for (var i = 0; i < propositions.length; i++) {
      var proposition = propositions[i];
      for (var j = 0; j < proposition.items; j++) {
        var item = proposition.items[j];

        if (item.schema === "https://ns.adobe.com/personalization/measurement") {
          // add metric to the DOM element
          const button = document.getElementById("form-based-click-metric");

          button.addEventListener("click", event => {
            const executedPropositions = [
              {
                id: proposition.id,
                scope: proposition.scope,
                scopeDetails: proposition.scopeDetails
              }
            ];
            // send the click track event
            alloy("sendEvent", {
              "xdm": {
                "eventType": "decisioning.propositionInteract",
                "_experience": {
                  "decisioning": {
                    "propositions": executedPropositions
                  }
                }
              }
            });
          });
        }
      }
    }
  }
});
```

Ensuite, apprenez à [activer le partage d’identifiants entre domaines ;](cross-domain.md) pour des profils de visiteur cohérents.

>[!NOTE]
>
>Nous nous engageons à vous aider à réussir la migration de Target d’at.js vers le SDK Web. Si vous rencontrez des obstacles lors de votre migration ou si vous pensez qu’il manque des informations essentielles dans ce guide, faites-le nous savoir en publiant sur [cette discussion communautaire](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996).