---
title: Utilisation de la couche de données client Adobe
description: Utilisation de la couche de données client Adobe
role: Developer
level: Intermediate
recommendations: noDisplay,noCatalog
jira: KT-10447
hide: true
hidefromtoc: true
exl-id: 33a5db8c-e49b-4073-b4d7-4abe19537fcb
source-git-commit: 90f7621536573f60ac6585404b1ac0e49cb08496
workflow-type: tm+mt
source-wordcount: '884'
ht-degree: 0%

---

# Utilisation de la couche de données client Adobe

Dans [Qu’est-ce qu’une couche de données ?](whats-a-data-layer.md), vous avez appris qu’il existe deux parties à prendre en compte lors de la discussion des couches de données : le conteneur et le contenu. La couche de données client Adobe est le conteneur. Comment tu t&#39;en fous [structurer vos données](../structuring-your-data.md) ou quelles informations vous choisissez de placer dans vos données. Les données peuvent être structurées comme [XDM](../structuring-your-data.md#xdm), comme le montrent les exemples ci-dessous, ou vous pouvez créer entièrement votre propre structure.

Idéalement, l’équipe d’ingénieurs de votre entreprise est chargée de transférer toutes les données nécessaires dans la couche de données par le biais du code sur la page. L’équipe marketing récupère ensuite les données de la couche de données, de préférence à l’aide des balises Adobe Experience Platform.

## Transmission de données vers la couche de données

La couche de données client Adobe est un tableau JavaScript. Lorsque vous créez la couche de données client Adobe, elle est vide :

```js
window.adobeDataLayer = window.adobeDataLayer || [];
```

Pour placer des données dans la couche de données, appelez la méthode `push` sur le tableau de couche de données :

```js
window.adobeDataLayer.push({
  "claims": {
    "ID": "CL10991306",
    "policyID": "IXP28113",
    "type": "automobile"
  }
});
```

Vous pouvez transférer des données supplémentaires dans la couche de données à tout moment en appelant `push` encore une fois.

```js
window.adobeDataLayer.push({
  "claims": {
    "status": "approved",
    "benefitAmount": {
      "amount": 1827.90,
      "currencyCode": "USD"
    }
  }
});
```

## Comprendre les données poussées

Si vous avez implémenté les deux `push` , vous obtiendriez deux entrées dans le tableau de couche de données. La couche de données n’est pas particulièrement utile dans cet état. En règle générale, vous souhaitez accéder à l’état fusionné de la couche de données ou, en d’autres termes, à un seul objet qui est le résultat combiné de toutes les données que vous avez transmises à la couche de données. Nous apprendrons à accéder à cet état fusionné plus loin dans le tutoriel. Pour l’instant, il suffit de comprendre que l’état calculé de la couche de données après nos deux `push` les appels sont les suivants :

```json
{
  "claims": {
    "ID": "CL10991306",
    "policyID": "IXP28113",
    "type": "automobile",
    "status": "approved",
    "benefitAmount": {
      "amount": 1827.90,
      "currencyCode": "USD"
    }
  }
}
```

## Supprimer des données

Parfois, vous devez supprimer des éléments de données de la couche de données. Cela est particulièrement courant dans les applications d’une seule page lorsque l’utilisateur navigue d’une vue à l’autre. Par exemple, si l’utilisateur navigue d’une vue de produit à une vue de contact, il peut être logique d’effacer toute donnée de produit sur la couche de données, car elle n’est plus pertinente pour la vue principale.

Vous pouvez supprimer une donnée en insérant une valeur de `undefined` pour la clé que vous souhaitez supprimer. En vous basant sur nos exemples précédents, si vous souhaitez supprimer `status` à partir de la couche de données, votre code se présenterait comme suit :

```js
window.adobeDataLayer.push({
  "claims": {
    "status": undefined
  }
});
```

L’état calculé de la couche de données n’inclut plus `status`:

```json
{
  "claims": {
    "ID": "CL10991306",
    "policyID": "IXP28113",
    "type": "automobile",
    "benefitAmount": {
      "amount": 1827.90,
      "currencyCode": "USD"
    }
  }
}
```

## Purge des événements dans la couche de données

La couche de données client Adobe est non seulement utilisée pour le stockage des données, mais également pour la communication des événements qui se produisent sur la page. En fait, vous poussez généralement les données dans la couche de données. _par résultat_ d’un événement se produisant sur la page. Ces événements comprennent (1) des événements d’interaction, comme l’ouverture d’un robot de chat ou la saisie d’un terme de recherche dans une barre de recherche ou (2) des événements de non-interaction, comme l’impression d’une publicité ou la fin des calculs de performances d’une page web.

Pour signaler qu’un événement s’est produit sur la page, incluez une `event` dans l’objet que vous poussez vers la couche de données. Vous pouvez par exemple indiquer qu’un utilisateur a saisi une requête dans un champ de recherche.

```js
window.adobeDataLayer.push({
  "event": "searchQueryEntered"
});
```

Vous apprendrez ensuite comment déclencher des règles dans les balises Adobe Experience Platform lorsqu’un événement particulier est envoyé à la couche de données. Notez également que la variable `event` key is _not_ inclus dans l’état calculé. Il reçoit un traitement particulier de la couche de données.

## Transmission d’événements et de données à la couche de données

Il est utile d’avertir les écouteurs que l’utilisateur a entré une requête de recherche, mais que se passe-t-il si vous souhaitez fournir des informations supplémentaires sur l’événement ? Par exemple, vous souhaitez peut-être inclure la requête de recherche de l’utilisateur. Vous pouvez fournir ces données de deux manières :

1. Fournir des données pour qu’elles **est conservé** dans la couche de données dans le cadre de l’état calculé de la couche de données.
2. Fournir des données pour qu’elles **n’est pas conservé** dans la couche de données dans le cadre de l’état calculé de la couche de données.

La conservation ou non des données dans la couche de données dépend généralement du fait que vous prévoyez de les référencer tout au long de la durée de la présence de l’utilisateur sur la page. Si ce n’est pas le cas, la conservation des données dans la couche de données peut simplement entraîner une couche de données encombrée.

Voici un exemple de transfert d’un événement avec des données supplémentaires qui **est conservé** dans la couche de données :

```js
window.adobeDataLayer.push({
  "event": "searchQueryEntered",
  "siteKnowledge": {
    "supportSiteSearch": {
      "term": "roller",
      "locationInPage": "topSearchBar"
    }
  }
});
```

Après cela `push` a lieu, `siteKnowledge` s’affichera toujours à l’état calculé de la couche de données jusqu’à ce que la page soit déchargée (sauf si vous supprimez ou remplacez intentionnellement la page). `siteKnowledge`).

En revanche, voici un exemple de transfert d’un événement avec des données supplémentaires qui **n’est pas conservé** dans la couche de données :

```js
window.adobeDataLayer.push({
  "event": "searchQueryEntered",
  "eventInfo": {
    "siteKnowledge": {
      "supportSiteSearch": {
        "term": "roller",
        "locationInPage": "topSearchBar"
      }
    }
  }
});
```

Dans cet exemple, notez que `siteKnowledge` est enveloppé dans `eventInfo`. Le `eventInfo` la clé reçoit un traitement spécial de la couche de données. Elle indique à la couche de données que ces données _should_ être inclus avec l’événement qui est envoyé aux écouteurs, mais il _should not_ être conservée dans la couche de données. Une fois que les écouteurs (comme les balises Adobe Experience Platform) ont été informés de l’événement, ces données sont essentiellement oubliées. Le `siteKnowledge` ne s’affichera jamais dans l’état calculé de la couche de données.

Chaque fois que vous appelez `push`, la couche de données client Adobe avertit tous les écouteurs. Plus tard, nous apprendrons à écouter ces notifications des balises Adobe Experience Platform et à déclencher des règles en conséquence.
