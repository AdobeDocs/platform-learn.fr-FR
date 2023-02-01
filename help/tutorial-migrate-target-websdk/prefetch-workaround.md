---
title: Solution de contournement pour la prérécupération | Migration de Target depuis at.js 2.x vers le SDK Web
description: Découvrez comment mettre en oeuvre une solution de contournement pour transférer des paramètres avec la prérécupération
source-git-commit: d061d2492d6d5e8e7a8a6e03ce63b9b6cd3793d8
workflow-type: tm+mt
source-wordcount: '502'
ht-degree: 0%

---

# Solution de contournement pour la prérécupération

Tous les clients Target qui n’étaient pas en production avec le SDK web Experience Platform avant le 1er octobre 2022 font une demande à Target à partir du réseau Edge Experience Platform à l’aide du mode &quot;prérécupération&quot;. La prérécupération permet au navigateur de précharger et de mettre en cache les offres Target afin qu’elles soient prêtes à être appliquées lorsque le visiteur atteint l’état correct de la page. Cela est avantageux pour les applications d’une seule page (SPA), car l’expérience utilisateur souhaitée peut être rendue aussi rapidement que possible, sans requêtes réseau supplémentaires. Il existe toutefois des implications importantes pour les implémentations SPA et non SPA.

Au lieu de comptabiliser un visiteur dans une activité lorsque le contenu de l’offre est diffusé dans la requête réseau, les visiteurs sont désormais comptabilisés dans les activités lorsqu’un `propositionDisplay` La demande sendEvent est effectuée par le SDK Web. Ces requêtes sont effectuées automatiquement par les activités du compositeur d’expérience visuelle (VEC) lorsque renderDecisions est défini sur true et lorsque l’expérience a été correctement rendue sur la page. Avec des portées personnalisées et lorsque renderDecisions est défini sur false, les requêtes propositionDisplay doivent être initiées intentionnellement par l’implémenteur. En outre, _tous les paramètres utilisés à des fins autres que la qualification de l’activité immédiate doivent être envoyés par le biais d’un `propositionDisplay`  event_.

## Pourquoi la solution est-elle nécessaire ?

Dans de nombreuses implémentations de Target, des demandes réseau importantes sont parfois effectuées sans attendre qu’une activité soit diffusée. Par exemple, des demandes peuvent être adressées à :

* Conversions des commandes d’enregistrement
* Définition des paramètres de profil
* Déclenchement des scripts de profil
* Envoi de paramètres d’entité pour renseigner le catalogue Recommendations

Malheureusement, en mode de prérécupération, ils ne se comportent pas comme prévu. En mode de prérécupération, ces données ne sont pas ingérées, sauf si elles font partie d’un `propositionDisplay`.

## Quelle est la solution ?

La solution se compose de trois parties :

1. Définissez une portée personnalisée dans le cadre de votre `sendEvent`
1. Utiliser la portée personnalisée dans une activité basée sur un formulaire (l’activité peut diffuser du contenu par défaut)
1. Utiliser un gestionnaire de réponse pour en créer un autre `sendEvent` pour la variable propositionDisplay et incluez les paramètres dont vous avez besoin pour capturer l’ordre, définissez les paramètres de profil, déclenchez le script de profil, envoyez les paramètres d’entité, etc.

Par exemple, voici un exemple d’utilisation de la solution pour envoyer un paramètre de profil :


```JavaScript
var data = {
    "__adobe": {
        "target": {
            "profile.gender": "male"
        }
    }
};
// Send the initial event with the data object and custom decision scope
alloy("sendEvent", {
    "renderDecisions": true,
    data,
    decisionScopes: ['profile-param-example']
}).then(function(result) {
    var propositions = result.propositions;
    var ctaProposition;
    if (propositions) {
        // Find the discount proposition, if it exists.
        for (var i = 0; i < propositions.length; i++) {
            var proposition = propositions[i];
            if (proposition.scope === "profile-param-example") {
                ctaProposition = proposition;
                break;
            }
        }
    }
    if (ctaProposition) {
        // Send a "decisioning.propositionDisplay" event signaling that the proposition has been rendered, and includes the data object again
        alloy("sendEvent", {
            xdm: {
                eventType: "decisioning.propositionDisplay",
                _experience: {
                    decisioning: {
                        propositions: [{
                            id: ctaProposition.id,
                            scope: ctaProposition.scope,
                            scopeDetails: ctaProposition.scopeDetails
                        }]
                    }
                }
            },
            data
        });
    }
});
```

Lorsque le profil est défini dans le cadre de la variable propositionDisplay, il est enregistré dans le profil du visiteur et il est disponible dans les demandes suivantes. La même approche peut être utilisée pour signaler les détails de conversion de commande et les paramètres d’entité.

Dans les balises , utilisez le type d’événement Send Event Complete pour déclencher un événement contenant l’événement sendEvent supplémentaire.

## Comment savoir si ma mise en oeuvre utilise le mode de prérécupération ?

Vous devez ouvrir un ticket auprès de l’assistance clientèle pour savoir si votre compte utilise le mode de prérécupération.


>[!NOTE]
>
>Nous nous engageons à vous aider à réussir la migration de Target d’at.js vers le SDK Web. Si vous rencontrez des obstacles lors de votre migration ou si vous pensez qu’il manque des informations essentielles dans ce guide, faites-le nous savoir en publiant sur [cette discussion communautaire](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996).