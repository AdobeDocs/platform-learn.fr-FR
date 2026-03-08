---
title: Migration de Target d’at.js 2.x vers Web SDK
description: Découvrez comment migrer une implémentation Adobe Target d’at.js 2.x vers Adobe Experience Platform Web SDK. Les rubriques incluent une présentation de la bibliothèque, des différences d’implémentation et d’autres légendes importantes.
exl-id: 43b9ae91-4524-4071-9eb4-12a0a8aec242
source-git-commit: 070fc02801d3403bf65ca732323338481e25b581
workflow-type: tm+mt
source-wordcount: '400'
ht-degree: 1%

---

# Activités de rendu de Target utilisant le compositeur basé sur les formulaires

Certaines implémentations de Target peuvent utiliser des mbox régionales (désormais appelées « portées ») pour diffuser du contenu à partir d’activités qui utilisent le compositeur d’expérience d’après les formulaires. Si votre implémentation d’at.js Target utilise des mbox, procédez comme suit :

* Mettez à jour toutes les références de votre implémentation at.js qui utilisent `getOffer()` ou `getOffers()` aux méthodes de SDK Web Platform équivalentes.
* Ajoutez du code pour déclencher un événement `propositionDisplay` afin qu’une impression soit comptabilisée.

## Demander et appliquer du contenu à la demande

Les activités créées à l’aide du compositeur basé sur les formulaires de Target et diffusées aux mbox régionales ne peuvent pas être rendues automatiquement par Platform Web SDK. Tout comme at.js, les offres diffusées à des emplacements Target spécifiques doivent être rendues à la demande.


+++Exemple d’utilisation d’at.js avec `getOffer()` et `applyOffer()` :

1. Exécuter `getOffer()` pour demander une offre pour un emplacement
1. Exécutez `applyOffer()` pour rendre l’offre vers un sélecteur spécifié.
1. Une impression d’activité est automatiquement incrémentée au moment de la demande de `getOffer()`

```JavaScript
// Retrieve an offer for the homepage-hero location
adobe.target.getOffer({
  "mbox": "homepage_hero",

  // Render offer to the #hero-banner selector
  "success": function(offers) {
    adobe.target.applyOffer({
      "mbox": "homepage_hero",
      "selector": "#hero-banner",
      "offer": offers
    });
  },
  "error": {
    console.log(error);
  },
  "timeout": 3000
});
```

+++

+++Équivalent de Platform Web SDK à l’aide de la commande `applyPropositions` : 

1. Exécutez `sendEvent` commande pour demander des offres (propositions) pour un ou plusieurs emplacements (portées)
1. Exécutez `applyPropositions` commande avec l’objet de métadonnées qui fournit des instructions sur la manière d’appliquer du contenu à la page pour chaque étendue
1. Exécutez `sendEvent` commande avec eventType de `decisioning.propositionDisplay` pour suivre une impression

```JavaScript
// Retrieve propositions for homepage_hero location (scope)
alloy("sendEvent", {
  "decisionScopes": ["homepage_hero"]
}).then(function(result) {
  var retrievedPropositions = result.propositions;
    
  // Render offer (proposition) to the #hero-banner selector by supplying extra metadata
  return alloy("applyPropositions", {
    "propositions": retrievedPropositions,
    "metadata": {
      // Specify each regional mbox or scope name along with a selector and actionType
      "homepage_hero": {
        "selector": "#hero-banner",
        "actionType": "setHtml"
      }
    }
  }).then(function(applyPropositionsResult) {
    var renderedPropositions = applyPropositionsResult.propositions;

    // Send the display notifications via sendEvent command
    alloy("sendEvent", {
      "xdm": {
        "eventType": "decisioning.propositionDisplay",
        "_experience": {
          "decisioning": {
            "propositions": renderedPropositions
          }
        }
      }
    });
  });
});
```

+++

Platform Web SDK offre un meilleur contrôle pour appliquer des activités basées sur des formulaires à la page à l’aide de la commande `applyPropositions` avec un `actionType` spécifié :

| `actionType` | Description | at.js `applyOffer()` | `applyPropositions` de Platform Web SDK |
| --- | --- | --- | --- |
| `setHtml` | Effacez le contenu du conteneur, puis ajoutez l&#39;offre au conteneur | Oui (toujours utilisé) | Oui |
| `replaceHtml` | Supprimez le conteneur et remplacez-le par l’offre . | Non | Oui |
| `appendHtml` | Ajoute l’offre après le sélecteur spécifié | Non | Oui |

Reportez-vous à la [documentation dédiée](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/rendering-personalization-content.html?lang=fr) sur le rendu du contenu à l’aide du SDK web de Platform pour obtenir des options de rendu supplémentaires et des exemples.

## Exemple d’implémentation

L’exemple de page ci-dessous s’appuie sur l’implémentation décrite dans la section précédente, mais il ajoute des portées supplémentaires à la commande `sendEvent` .

+++Exemple Platform Web SDK avec plusieurs portées

```HTML
<!doctype html>
<html>
<head>
  <title>Example page</title>
  <!--Data Layer to enable rich data collection and targeting-->
  <script>
    var digitalData = { 
      // Data layer information goes here
    };
  </script>

  <!--Third party libraries that may be used by Target offers and modifications-->
  <script src="https://ajax.googleapis.com/ajax/libs/jquery/3.6.1/jquery.min.js"></script>

  <!--Prehiding snippet for Target with asynchronous deployment-->
  <script>
    !function(e,a,n,t){var i=e.head;if(i){
    if (a) return;
    var o=e.createElement("style");
    o.id="alloy-prehiding",o.innerText=n,i.appendChild(o),setTimeout(function(){o.parentNode&&o.parentNode.removeChild(o)},t)}}
    (document, document.location.href.indexOf("mboxEdit") !== -1, ".body { opacity: 0 !important }", 3000);
  </script>

  <!--Platform Web SDK base code-->
  <script>
    !function(n,o){o.forEach(function(o){n[o]||((n.__alloyNS=n.__alloyNS||
    []).push(o),n[o]=function(){var u=arguments;return new Promise(
    function(i,l){n[o].q.push([i,l,u])})},n[o].q=[])})}
    (window,["alloy"]);
  </script>

  <!--Platform Web SDK loaded asynchonously. Change the src to use the latest supported version.-->
  <script src="https://cdn1.adoberesources.net/alloy/2.6.4/alloy.min.js" async></script>
  
  <!--Configure Platform Web SDK then send event-->
  <script>
    alloy("configure", {
      "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
      "orgId":"ADB3LETTERSANDNUMBERS@AdobeOrg"
    });
    alloy("sendEvent", {
      // Request and render VEC-based activities
      "renderDecisions": true,
      // Request content for form-based activities using the "homepage_hero" scope
      "decisionScopes": ["homepage_hero"]
    }).then(function(result) {
      var retrievedPropositions = result.propositions;
        
      // Render offer (proposition) to the #hero-banner selector by supplying extra metadata
      return alloy("applyPropositions", {
        "propositions": retrievedPropositions,
        "metadata": {
          // Specify each regional mbox or scope name along with a selector and actionType
          "homepage_hero": {
            "selector": "#hero-banner",
            "actionType": "setHtml"
          }
        }
      }).then(function(applyPropositionsResult) {
        var renderedPropositions = applyPropositionsResult.propositions;

        // Send the display notifications via sendEvent command
        alloy("sendEvent", {
          "xdm": {
            "eventType": "decisioning.propositionDisplay",
            "_experience": {
              "decisioning": {
                "propositions": renderedPropositions
              }
            }
          }
        });
      });
    });
  </script>
</head>
<body>
  <h1 id="title">Home Page</h1><br><br>
  <p id="bodyText">Navigation</p><br><br>
  <a id="home" class="navigationLink" href="#">Home</a><br>
  <a id="pageA" class="navigationLink" href="#">Page A</a><br>
  <a id="pageB" class="navigationLink" href="#">Page B</a><br>
  <a id="pageC" class="navigationLink" href="#">Page C</a><br>
  <div id="homepage-hero">Homepage Hero Banner Content</div>
</body>
</html>
```

+++

Découvrez ensuite comment [transmettre des paramètres Target à l’aide de Platform Web SDK](send-parameters.md).

>[!NOTE]
>
>Nous nous engageons à vous aider à réussir la migration de Target d’at.js vers Web SDK. Si vous rencontrez des obstacles avec votre migration ou si vous pensez qu&#39;il manque des informations essentielles dans ce guide, veuillez nous le faire savoir en postant dans [cette discussion communautaire](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-target-from-at-js-to-web-sdk/m-p/575587?profile.language=fr#M463).
