---
title: Migration de Target depuis at.js 2.x vers le SDK Web
description: Découvrez comment migrer une mise en oeuvre Adobe Target d’at.js 2.x vers le SDK Web Adobe Experience Platform. Les rubriques incluent un aperçu de la bibliothèque, des différences de mise en oeuvre et d’autres légendes dignes d’intérêt.
exl-id: 43b9ae91-4524-4071-9eb4-12a0a8aec242
source-git-commit: 4690d41f92c83fe17eda588538d397ae1fa28af0
workflow-type: tm+mt
source-wordcount: '400'
ht-degree: 1%

---

# Activités Render Target qui utilisent le compositeur basé sur les formulaires

Certaines mises en oeuvre de Target peuvent utiliser des mbox régionales (désormais appelées &quot;portées&quot;) pour diffuser du contenu à partir des activités qui utilisent le compositeur d’expérience d’après les formulaires. Si votre implémentation d’at.js Target utilise des mbox, vous devez effectuer les opérations suivantes :

* Mettez à jour toutes les références de votre implémentation at.js qui utilisent `getOffer()` ou `getOffers()` vers les méthodes SDK Web Platform équivalentes.
* Ajoutez du code pour déclencher un événement `propositionDisplay` afin de comptabiliser une impression.

## Demander et appliquer du contenu à la demande

Les activités créées à l’aide du compositeur basé sur les formulaires de Target et diffusées aux mbox régionales ne peuvent pas être rendues automatiquement par le SDK Web Platform. Tout comme at.js, les offres diffusées à des emplacements cibles spécifiques doivent être rendues à la demande.


+++Exemple d’at.js utilisant `getOffer()` et `applyOffer()` :

1. Exécutez `getOffer()` pour demander un emplacement.
1. Exécutez `applyOffer()` pour effectuer le rendu de l’offre vers un sélecteur spécifié
1. Une impression d’activité est automatiquement incrémentée au moment de la requête `getOffer()`.

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

+++Équivalent du SDK Web Platform à l’aide de la commande `applyPropositions` :

1. Exécutez la commande `sendEvent` pour demander des offres (propositions) pour un ou plusieurs emplacements (portées).
1. Exécutez la commande `applyPropositions` avec un objet de métadonnées qui fournit des instructions pour appliquer du contenu à la page pour chaque portée.
1. Exécutez la commande `sendEvent` avec eventType `decisioning.propositionDisplay` pour suivre une impression

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

Le SDK Web Platform offre un meilleur contrôle pour appliquer des activités d’après les formulaires à la page à l’aide de la commande `applyPropositions` avec un `actionType` spécifié :

| `actionType` | Description | at.js `applyOffer()` | SDK Web Platform `applyPropositions` |
| --- | --- | --- | --- |
| `setHtml` | Effacer le contenu du conteneur, puis ajouter l’offre au conteneur | Oui (toujours utilisé) | Oui |
| `replaceHtml` | Supprimer le conteneur et le remplacer par l’offre | Non | Oui |
| `appendHtml` | Ajoute l’offre après le sélecteur spécifié | Non | Oui |

Pour obtenir des exemples et des options de rendu supplémentaires, reportez-vous à la [documentation dédiée](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/rendering-personalization-content.html?lang=fr) sur le rendu de contenu à l’aide du SDK Web Platform.

## Exemple d’implémentation

L’exemple de page ci-dessous s’appuie sur l’implémentation décrite dans la section précédente. Il ajoute uniquement des portées supplémentaires à la commande `sendEvent`.

+++Exemple de SDK Web Platform avec plusieurs portées

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

Ensuite, découvrez comment [transférer des paramètres Target à l’aide du SDK Web Platform](send-parameters.md).

>[!NOTE]
>
>Nous nous engageons à vous aider à réussir la migration de Target d’at.js vers le SDK Web. Si vous rencontrez des obstacles lors de votre migration ou si vous pensez qu’il manque des informations essentielles dans ce guide, faites-le-nous savoir en publiant sur [cette discussion communautaire](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-target-from-at-js-to-web-sdk/m-p/575587?profile.language=fr#M463).
