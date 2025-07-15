---
title: Récupération des activités Target - Migrez l’implémentation d’Adobe Target dans votre application mobile vers l’extension Offer Decisioning et Target
description: Découvrez comment récupérer les activités Adobe Target lors de la migration d’Adobe Target vers l’extension Offer Decisioning et Target Mobile.
exl-id: 39569088-a254-4e64-9956-0c6e1a8ed2a5
source-git-commit: 876e664a213aec954105bf2d5547baab5d8a84ea
workflow-type: tm+mt
source-wordcount: '317'
ht-degree: 0%

---

# Récupération des activités Target

Les implémentations mobiles de Target utilisent des mbox régionales (désormais appelées « portées ») pour diffuser du contenu à partir d’activités qui utilisent le compositeur d’expérience basé sur les formulaires de Target. Vous devez mettre à jour votre application mobile pour inclure des portées dans vos appels réseau.

Le contenu renvoyé par Target, également appelé « offres », se compose généralement de texte ou de code json que vous devez utiliser dans votre application pour effectuer le rendu de l’expérience client finale. Les offres de Target sont souvent utilisées pour :

* Activer les indicateurs de fonctionnalité dans votre application
* Diffuser du texte secondaire ou des images

Si vous avez des activités qui doivent s’exécuter à la fois dans les versions de l’extension Target et de l’extension Offer Decisioning et Target de votre application, veillez à effectuer un test approfondi. Si vous devez utiliser des offres différentes pour différentes versions de votre application, pensez à utiliser les options de ciblage dans l’interface pour diffuser des offres différentes aux différentes versions.

Veillez toujours à inclure la gestion des erreurs pour afficher les expériences appropriées dans des conditions d’erreur.


## Demander et appliquer du contenu à la demande

>[!IMPORTANT]
>
>Après avoir appliqué du contenu à l’application, il est impératif de déclencher `displayed` API pour informer Target que le visiteur a vu le contenu secondaire ou par défaut spécifié dans l’activité. Consultez la page [Suivi des événements de conversion Target](track-events.md) pour plus d’informations.


+++ Exemple Android

>[!BEGINTABS]

>[!TAB Optimisation de SDK]

```Java
// Mboxes for Target activities
final DecisionScope decisionScope1 = DecisionScope("myTargetMbox1");
final DecisionScope decisionScope2 = new DecisionScope("myTargetMbox2");
 
final List<DecisionScope> decisionScopes = new ArrayList<>();
decisionScopes.add(decisionScope1);
decisionScopes.add(decisionScope2);
 
// Prefetch the Target mboxes
Optimize.updatePropositions(decisionScopes,
                            new HashMap<String, Object>() {
                                {
                                    put("xdmKey", "xdmValue");
                                }
                            },
                            new HashMap<String, Object>() {
                                {
                                    put("dataKey", "dataValue");
                                }
                            },
                            new AdobeCallbackWithOptimizeError<Map<DecisionScope, OptimizeProposition>>() {
                                @Override
                                public void fail(AEPOptimizeError optimizeError) {
                                    // Log in case of error
                                    Log.d("Target Prefetch error", optimizeError.title);
                                }
 
                                @Override
                                public void call(Map<DecisionScope, OptimizeProposition> propositionsMap) {
                                    // Retrieve cached propositions if prefetch succeeds
                                    Optimize.getPropositions(scopes, new AdobeCallbackWithError<Map<DecisionScope, OptimizeProposition>>() {
                                        @Override
                                      public void fail(final AdobeError adobeError) {
                                              // handle error
                                        }
 
                                        @Override
                                        public void call(Map<DecisionScope, OptimizeProposition> propositionsMap) {
                                              if (propositionsMap != null && !propositionsMap.isEmpty()) {
                                                // get the propositions for the given decision scopes
                                                if (propositionsMap.contains(decisionScope1)) {
                                                      final OptimizeProposition proposition1 = propsMap.get(decisionScope1)
                                                      // read proposition1 offers and display them
                                                }
                                                if (propositionsMap.contains(decisionScope2)) {
                                                      final OptimizeProposition proposition2 = propsMap.get(decisionScope2)
                                                      // read proposition2 offers and display them
                                                }
                                              }
                                        }
                                      });
                                }
                            });
```

>[!ENDTABS]

+++

+++ Exemple iOS

>[!BEGINTABS]

>[!TAB Optimisation de SDK]

```Swift
// Mboxes for Target activities
let decisionScope1 = DecisionScope(name: "myTargetMbox1")
let decisionScope2 = DecisionScope(name: "myTargetMbox2")
 
// Prefetch the Target mboxes
Optimize.updatePropositions(for: [decisionScope1, decisionScope2]
                            withXdm: ["xdmKey": "xdmValue"]
                            andData: ["dataKey": "dataValue"]) { data, error in
            if let error = error as? AEPOptimizeError {
                // handle error
                return
            }
            // Retrieve cached propositions if prefetch succeeds
            Optimize.getPropositions(for: [decisionScope1, decisionScope2]) { propositionsDict, error in
                if let error = error {
                    // handle error
                    return
                }
 
                if let propositionsDict = propositionsDict {
                    // get the propositions for the given decision scopes
 
                    if let proposition1 = propositionsDict[decisionScope1] {
                        // read proposition1 offers and display them
                    }
 
                    if let proposition2 = propositionsDict[decisionScope2] {
                        // read proposition2 offers and display them
                    }
                }
            }
        }
```

>[!ENDTABS]

+++



Découvrez ensuite comment [transmettre des paramètres Target à l’aide de l’extension Offer Decisioning et Target](send-parameters.md).

>[!NOTE]
>
>Nous nous engageons à vous aider à réussir votre migration mobile de Target vers l’extension Offer Decisioning et Target. Si vous rencontrez des obstacles avec votre migration ou si vous pensez qu&#39;il manque des informations essentielles dans ce guide, veuillez nous le faire savoir en postant dans [cette discussion communautaire](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-adobe-target-to-mobile-sdk-on-edge/m-p/747484#M625).
