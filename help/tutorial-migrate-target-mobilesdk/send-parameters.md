---
title: Envoi de paramètres - Migration d’Adobe Target vers l’extension Adobe Journey Optimizer - Prise de décision Mobile
description: Découvrez comment envoyer des paramètres de mbox, de profil et d’entité à Adobe Target à l’aide du SDK Web Experience Platform.
source-git-commit: afbc8248ad81a5d9080a4fdba1167e09bbf3b33d
workflow-type: tm+mt
source-wordcount: '658'
ht-degree: 0%

---

# Envoi de paramètres à Target à l’aide de l’extension Adobe Journey Optimizer - Decisioning Mobile

Les mises en oeuvre de Target diffèrent d’un site web à l’autre en raison de l’architecture du site, des exigences de l’entreprise et des fonctionnalités utilisées. La plupart des implémentations de Target incluent la transmission de divers paramètres pour les informations contextuelles, les audiences et les recommandations de contenu.

Utilisons une page de détails de produit simple et une page de confirmation de commande pour démontrer les différences entre les extensions lors de la transmission de paramètres à Target.


| Exemple de paramètre at.js | Option SDK Web Platform | Notes |
| --- | --- | --- |
| `at_property` | S/O | Les jetons de propriété sont configurés dans le [datastream](https://experienceleague.adobe.com/docs/experience-platform/edge/datastreams/configure.html#target) et ne peuvent pas être définis dans l’appel `sendEvent`. |
| `pageName` | `xdm.web.webPageDetails.name` | Tous les paramètres de mbox Target doivent être transmis dans le cadre de l’objet `xdm` et conformes à un schéma à l’aide de la classe XDM ExperienceEvent. Les paramètres de mbox ne peuvent pas être transmis dans le cadre de l’objet `data`. |
| `profile.gender` | `data.__adobe.target.profile.gender` | Tous les paramètres de profil Target doivent être transmis dans le cadre de l’objet `data` et précédés du préfixe `profile.` pour être mappés correctement. |
| `user.categoryId` | `data.__adobe.target.user.categoryId` | Paramètre réservé utilisé pour la fonctionnalité Affinité catégorielle de Target qui doit être transmis dans le cadre de l’objet `data`. |
| `entity.id` | `data.__adobe.target.entity.id` <br>OR<br> `xdm.productListItems[0].SKU` | Les identifiants d’entité sont utilisés pour les compteurs de comportement de Target Recommendations. Ces identifiants d’entité peuvent être transmis dans le cadre de l’objet `data` ou mappés automatiquement à partir du premier élément du tableau `xdm.productListItems` si votre implémentation utilise ce groupe de champs. |
| `entity.categoryId` | `data.__adobe.target.entity.categoryId` | Les identifiants de catégorie d’entité peuvent être transmis dans le cadre de l’objet `data`. |
| `entity.customEntity` | `data.__adobe.target.entity.customEntity` | Les paramètres d’entité personnalisés sont utilisés pour la mise à jour du catalogue de produits Recommendations. Ces paramètres personnalisés doivent être transmis dans le cadre de l’objet `data`. |
| `cartIds` | `data.__adobe.target.cartIds` | Utilisé pour les algorithmes de recommandations basés sur le panier de Target. |
| `excludedIds` | `data.__adobe.target.excludedIds` | Utilisé pour empêcher le renvoi d’ID d’entité spécifiques dans une conception de recommandations. |
| `mbox3rdPartyId` | Défini dans l’objet `xdm.identityMap` | Utilisé pour synchroniser les profils Target sur les appareils et les attributs du client. L’espace de noms à utiliser pour l’ID de client doit être spécifié dans la configuration [Target de la banque de données](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/adobe-target/using-mbox-3rdpartyid.html). |
| `orderId` | `xdm.commerce.order.purchaseID` | Utilisé pour identifier une commande unique pour le suivi de conversion de Target. |
| `orderTotal` | `xdm.commerce.order.priceTotal` | Utilisé pour le suivi des totaux des commandes pour les objectifs de conversion et d’optimisation de Target. |
| `productPurchasedId` | `data.__adobe.target.productPurchasedId` <br>OR<br> `xdm.productListItems[0-n].SKU` | Utilisé pour le suivi des conversions Target et les algorithmes de recommandations. Pour plus d’informations, reportez-vous à la section [paramètres d’entité](#entity-parameters) ci-dessous. |
| `mboxPageValue` | `data.__adobe.target.mboxPageValue` | Utilisé pour l’objectif de l’activité [score personnalisé](https://experienceleague.adobe.com/docs/target/using/activities/success-metrics/capture-score.html). |

{style="table-layout:auto"}

## Paramètres personnalisés

Les paramètres mbox personnalisés doivent être transmis en tant que XDM ou à l’aide de l’objet de données avec la commande `sendEvent`. Il est important de s’assurer que le schéma XDM inclut tous les champs requis pour votre mise en oeuvre Target.


## Paramètres de profil

Les paramètres de profil Target doivent être transmis...

## Paramètres d’entité

Les paramètres d’entité sont utilisés pour transmettre des données comportementales et des informations de catalogue supplémentaires pour Target Recommendations. Tous les [paramètres d’entité](https://experienceleague.adobe.com/docs/target/using/recommendations/entities/entity-attributes.html) pris en charge par at.js sont également pris en charge par le SDK Web Platform. Tout comme les paramètres de profil, tous les paramètres d’entité doivent être transmis sous l’objet `data.__adobe.target` dans la payload de commande du SDK Web Platform `sendEvent`.

Les paramètres d’entité d’un élément spécifique doivent comporter le préfixe `entity.` pour une capture de données correcte. Les paramètres réservés `cartIds` et `excludedIds` pour les algorithmes de recommandations ne doivent pas être précédés d’un préfixe et la valeur de chacun d’eux doit contenir une liste séparée par des virgules d’identifiants d’entité.



## Paramètres d’achat

Les paramètres d’achat sont transmis sur une page de confirmation de commande après une commande réussie et sont utilisés pour les objectifs de conversion et d’optimisation de Target. Avec une mise en oeuvre du SDK Mobile Platform à l’aide de l’extension de prise de décision, ces paramètres et sont automatiquement mappés à partir des données XDM transmises dans le cadre du groupe de champs `commerce`.


Les informations d’achat sont transmises à Target lorsque `purchases.value` est défini sur `1` pour le groupe de champs `commerce`. L’identifiant de commande et le total de la commande sont automatiquement mappés à partir de l’objet `order`. Si le tableau `productListItems` est présent, les valeurs `SKU` sont utilisées pour `productPurchasedId`.


## ID de client (mbox3rdPartyId)

Target permet la synchronisation des profils entre appareils et systèmes à l’aide d’un seul ID de client.



Ensuite, découvrez comment [suivre les événements de conversion Target](track-events.md) avec le SDK Web Platform.

>[!NOTE]
>
>Nous nous engageons à vous aider à réussir la migration de Target mobile de l’extension Target vers l’extension de prise de décision. Si vous rencontrez des obstacles lors de votre migration ou si vous pensez qu’il manque des informations essentielles dans ce guide, faites-le-nous savoir en publiant sur [cette discussion communautaire](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-target-from-at-js-to-web-sdk/m-p/575587#M463).
