---
title: Paramètres d’envoi - Migration d’Adobe Target vers l’extension Adobe Journey Optimizer - Prise de décision pour mobile
description: Découvrez comment envoyer des paramètres de mbox, de profil et d’entité à Adobe Target à l’aide d’Experience Platform Web SDK.
exl-id: 927d83f9-c019-4a6b-abef-21054ce0991b
source-git-commit: 314f0279ae445f970d78511d3e2907afb9307d67
workflow-type: tm+mt
source-wordcount: '777'
ht-degree: 1%

---

# Envoi de paramètres à Target à l’aide de l’extension Adobe Journey Optimizer - Decisioning Mobile

Les implémentations de Target varient d’un site web à l’autre en fonction de l’architecture, des exigences commerciales et des fonctionnalités utilisées. La plupart des implémentations de Target incluent la transmission de divers paramètres pour les informations contextuelles, les audiences et les recommandations de contenu.

Avec l’extension Target, tous les paramètres Target étaient transmis à l’aide de la fonction `TargetParameters`.

Avec l’extension Decisioning :

* Les paramètres destinés à plusieurs applications Adobe peuvent être transmis dans l’objet XDM
* Les paramètres destinés uniquement à Target peuvent être transmis dans l’objet `data.__adobe.target`


>[!IMPORTANT]
>
> Avec l’extension Decisioning, les paramètres envoyés dans une requête s’appliquent à toutes les portées de la requête. Si vous devez définir des paramètres différents pour différentes portées, vous devez effectuer des requêtes supplémentaires.

## Paramètres personnalisés

Les paramètres de mbox personnalisés sont la méthode la plus simple pour transmettre des données à Target et peuvent être transmis dans les objets XDM ou `data.__adobe.target`.

## Paramètres de profil

Les paramètres de profil stockent des données pendant une période prolongée dans le profil Target de l’utilisateur et doivent être transmis à l’objet `data.__adobe.target`.

## Paramètres de l’entité

Les [paramètres d’entité](https://experienceleague.adobe.com/docs/target/using/recommendations/entities/entity-attributes.html) sont utilisés pour transmettre des données comportementales et des informations de catalogue supplémentaires pour Target Recommendations. Tout comme les paramètres de profil, tous les paramètres d’entité doivent être transmis sous l’objet `data.__adobe.target`.

Les paramètres d&#39;entité pour un élément spécifique doivent être précédés de `entity.` pour une capture de données correcte. Les paramètres `cartIds` et `excludedIds` réservés aux algorithmes de recommandations ne doivent pas être précédés de préfixes et la valeur de chaque doit contenir une liste d’identifiants d’entité séparés par des virgules.

## Paramètres d’achat

Les paramètres d’achat sont transmis sur une page de confirmation de commande après une commande réussie et sont utilisés pour les objectifs de conversion et d’optimisation de Target. Avec une implémentation de Platform Mobile SDK utilisant l’extension Decisioning, ces paramètres et sont automatiquement mappés à partir des données XDM transmises dans le cadre du groupe de champs `commerce`.

Les informations d’achat sont transmises à Target lorsque le groupe de champs `commerce` a `purchases.value` défini sur `1`. L’ID de commande et le total de la commande sont automatiquement mappés à partir de l’objet `order`. Si le tableau `productListItems` est présent, les valeurs `SKU` sont utilisées pour la `productPurchasedId`.

Si vous ne transmettez pas `commerce` champs dans l’objet XDM, vous pouvez transmettre les détails de la commande à Target à l’aide des champs `data.__adobe.target.orderId`, `data.__adobe.target.orderTotal` et `data.__adobe.target.productPurchasedId`.

## Identifiant client (mbox3rdPartyId)

Target permet de synchroniser les profils sur plusieurs appareils et systèmes à l’aide d’un seul identifiant client. Cet ID de client doit être transmis dans le champ `identityMap` de l’objet XDM et mappé au champ ID de tiers cible dans le flux de données.

## Tableau

| Exemple de paramètre at.js | Option de Platform Web SDK | Notes |
| --- | --- | --- |
| `at_property` | S/O | Les jetons de propriété sont configurés dans le [flux de données](https://experienceleague.adobe.com/docs/experience-platform/edge/datastreams/configure.html#target) et ne peuvent pas être définis dans l’appel `sendEvent`. |
| `pageName` | `xdm.web.webPageDetails.name` | Tous les paramètres de mbox cible doivent être transmis dans le cadre de l’objet `xdm` et être conformes à un schéma à l’aide de la classe XDM ExperienceEvent. Les paramètres de mbox ne peuvent pas être transmis dans le cadre de l’objet `data`. |
| `profile.gender` | `data.__adobe.target.profile.gender` | Tous les paramètres de profil Target doivent être transmis dans le cadre de l’objet `data` et précédés du préfixe `profile.` pour être mappés correctement. |
| `user.categoryId` | `data.__adobe.target.user.categoryId` | Paramètre réservé utilisé pour la fonction Affinité catégorielle de Target qui doit être transmis dans le cadre de l’objet `data`. |
| `entity.id` | `data.__adobe.target.entity.id` <br>OU<br> `xdm.productListItems[0].SKU` | Les identifiants d’entité sont utilisés pour les compteurs comportementaux de Target Recommendations. Ces ID d’entité peuvent être transmis dans le cadre de l’objet `data` ou mappés automatiquement à partir du premier élément du tableau de `xdm.productListItems` si votre implémentation utilise ce groupe de champs. |
| `entity.categoryId` | `data.__adobe.target.entity.categoryId` | Les identifiants de catégorie d’entité peuvent être transmis dans le cadre de l’objet `data`. |
| `entity.customEntity` | `data.__adobe.target.entity.customEntity` | Les paramètres d’entité personnalisés sont utilisés pour mettre à jour le catalogue de produits Recommendations. Ces paramètres personnalisés doivent être transmis dans le cadre de l’objet `data`. |
| `cartIds` | `data.__adobe.target.cartIds` | Utilisé pour les algorithmes de recommandations basés sur le panier de Target. |
| `excludedIds` | `data.__adobe.target.excludedIds` | Utilisé pour empêcher le renvoi d’ID d’entité spécifiques dans une conception Recommendations. |
| `mbox3rdPartyId` | Définir dans l’objet `xdm.identityMap` | Utilisé pour synchroniser les profils Target sur les appareils et les attributs du client. L’espace de noms à utiliser pour l’ID de client doit être spécifié dans la [configuration cible du flux de données](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/adobe-target/using-mbox-3rdpartyid.html). |
| `orderId` | `xdm.commerce.order.purchaseID`<br> (lorsque `commerce.purchases.value` est défini sur `1`) | Utilisé pour identifier une commande unique pour le suivi des conversions dans Target. |
| `orderTotal` | `xdm.commerce.order.priceTotal`<br> (lorsque `commerce.purchases.value` est défini sur `1`) | Utilisé pour le suivi des totaux des ordres pour les objectifs de conversion et d’optimisation de Target. |
| `productPurchasedId` | `xdm.productListItems[0-n].SKU`<br> (lorsque `commerce.purchases.value` est défini sur `1`) <br>OU<br> `data.__adobe.target.productPurchasedId` | Utilisé pour le suivi des conversions de Target et les algorithmes de recommandations. Pour plus d’informations](#entity-parameters) reportez-vous à la section [paramètres d’entité ci-dessous. |
| `mboxPageValue` | `data.__adobe.target.mboxPageValue` | Utilisé pour l’objectif de l’activité [notation personnalisée](https://experienceleague.adobe.com/docs/target/using/activities/success-metrics/capture-score.html). |

{style="table-layout:auto"}


## Exemples de transmission de paramètres

Prenons un exemple simple pour démontrer les différences entre les extensions lors de la transmission de paramètres à Target.

### Android

>[!BEGINTABS]

>[!TAB SDK Target]

```Java
Map<String, String> mboxParameters = new HashMap<String, String>();
mboxParameters1.put("status", "platinum");
 
Map<String, String> profileParameters = new HashMap<String, String>();
profileParameters1.put("gender", "male");
 
List<String> purchasedProductIds = new ArrayList<String>();
purchasedProductIds.add("ppId1");
TargetOrder targetOrder = new TargetOrder("id1", 1.0, purchasedProductIds);
 
TargetProduct targetProduct = new TargetProduct("pId1", "cId1");
 
TargetParameters targetParameters = new TargetParameters.Builder()
                                    .parameters(mboxParameters)
                                    .profileParameters(profileParameters)
                                    .product(targetProduct)
                                    .order(targetOrder)
                                    .build();
```

>[!ENDTABS]

### iOS

>[!BEGINTABS]

>[!TAB SDK Target]

```Swift
let mboxParameters = [
                        "status": "platinum"
                     ]
 
let profileParameters = [
                            "gender": "male"
                        ]
 
let order = TargetOrder(id: "id1", total: 1.0, purchasedProductIds: ["ppId1"])
 
let product = TargetProduct(productId: "pId1", categoryId: "cId1")
 
let targetParameters = TargetParameters(parameters: mboxParameters, profileParameters: profileParameters, order: order, product: product))
```


>[!ENDTABS]






Ensuite, découvrez comment [suivre les événements de conversion Target](track-events.md) avec le SDK web de Platform.

>[!NOTE]
>
>Nous nous engageons à vous aider à réussir votre migration mobile de Target de l’extension Target vers l’extension Decisioning. Si vous rencontrez des obstacles avec votre migration ou si vous pensez qu&#39;il manque des informations essentielles dans ce guide, veuillez nous le faire savoir en postant dans [cette discussion communautaire](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-target-from-at-js-to-web-sdk/m-p/575587#M463).
