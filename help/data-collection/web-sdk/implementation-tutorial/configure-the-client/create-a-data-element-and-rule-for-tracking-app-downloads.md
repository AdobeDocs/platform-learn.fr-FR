---
title: Création d’un élément de données et d’une règle pour le suivi des téléchargements d’applications
description: Création d’un élément de données et d’une règle pour le suivi des téléchargements d’applications
feature: Web SDK
role: Developer
level: Intermediate
recommendations: noDisplay,noCatalog
jira: KT-10447
hide: true
hidefromtoc: true
exl-id: cb322540-e8ef-4226-b537-a67c7ca273f5
source-git-commit: 90f7621536573f60ac6585404b1ac0e49cb08496
workflow-type: tm+mt
source-wordcount: '764'
ht-degree: 3%

---

# Création d’un élément de données et d’une règle pour le suivi des téléchargements d’applications

Pour rappel, lors du suivi lorsqu’un utilisateur clique sur la variable [!UICONTROL Téléchargement de l’application] , vous avez migré vers la couche de données comme suit :

```js
window.adobeDataLayer.push({
  "event": "downloadAppClicked",
  "eventInfo": {
    "web": {
      "webInteraction": {
        "URL": "https://example.com/download",
        "name": "App Download",
        "type": "download"
      }
    }
  }
});
```

Vous avez utilisé la variable `eventInfo` qui indique à la couche de données de communiquer ces données avec l’événement, mais à _not_ conservez les données dans la couche de données. Pour un clic sur un lien, il n’est pas utile d’ajouter des informations sur le lien sur lequel l’utilisateur a cliqué à la couche de données, car elles ne s’appliquent pas à d’autres événements qui peuvent se produire ultérieurement sur la page.

Pour cette implémentation, vous enverrez un événement d’expérience à Adobe Experience Platform contenant le résultat fusionné de (1) l’état calculé de la couche de données et (2) le contenu de `eventInfo`.

Pour ce faire, vous devez d’abord créer un élément de données qui fusionne ces deux blocs d’informations.

## Créer un élément de données

Pour créer l’élément de données approprié, cliquez sur [!UICONTROL Éléments de données] dans le menu de gauche. Cliquez ensuite sur le [!UICONTROL Ajouter un élément de données] lien.

Pour le nom de l’élément de données, saisissez `computedStateAndEventInfo`. Pour le [!UICONTROL Extension] champ, sélectionnez [!UICONTROL Core] s’il n’est pas déjà sélectionné. Pour le [!UICONTROL Type d’élément de données] champ, sélectionnez [!UICONTROL Objets fusionnés]. Cet élément de données vous permet de fusionner en profondeur plusieurs objets. Le résultat fusionné est renvoyé par l’élément de données.

Pour le premier objet que vous souhaitez inclure dans la fusion, saisissez `%event.fullState%`. Lorsqu’elle est utilisée dans une règle déclenchée par une [!UICONTROL Données transférées] règle, cela fait référence à l’état calculé de la couche de données client Adobe au moment où la règle a été déclenchée.

Cliquez sur [!UICONTROL Ajouter un autre].

Pour le deuxième objet, saisissez `%event.eventInfo%`. Lorsqu’elle est utilisée dans une règle déclenchée par une [!UICONTROL Données transférées] événement de règle, qui fait référence à la variable `eventInfo` qui a été transmise à la couche de données client Adobe.

![élément de données computedStateAndEventInfo](../../../assets/implementation-strategy/computed-state-and-event-info-data-element.png)

L’élément de données est terminé. Enregistrez l’élément de données en cliquant sur le [!UICONTROL Enregistrer] bouton .

## Créer une règle

Pour créer la règle pour le suivi des clics sur le [!UICONTROL Téléchargement de l’application] lien, premier clic [!UICONTROL Règles] dans le menu de gauche.

Cliquez sur [!UICONTROL Ajouter une règle].

Pour le nom de la règle, saisissez _Lien de l’application de téléchargement cliqué_.

## Ajout d’un événement

Cliquez sur le bouton [!UICONTROL Ajouter] sous [!UICONTROL Événements]. Vous affichez maintenant la vue d’événement. Pour le [!UICONTROL Extension] champ, sélectionnez [!UICONTROL Adobe de la couche de données client]. Pour le [!UICONTROL Type d’événement] champ, sélectionnez [!UICONTROL Données transférées].

Parce que vous souhaitez que cette règle soit déclenchée uniquement lorsque la variable `downloadAppClicked` est envoyé à la couche de données, sélectionnez l’événement [!UICONTROL Evénement spécifique] radio sous [!UICONTROL Écoute] et type _downloadAppClicked_ dans la [!UICONTROL Événement/Clé à enregistrer pour]  Champ de texte affiché.

![Télécharger l’événement sur lequel l’application a cliqué](../../../assets/implementation-strategy/download-app-clicked-event.png)

Cliquez sur [!UICONTROL Conserver les modifications].

## Ajouter une action

Maintenant que vous êtes de retour à l’affichage des règles, cliquez sur le bouton [!UICONTROL Ajouter] sous [!UICONTROL Actions]. Vous devriez maintenant être dans la vue d’action. Pour le [!UICONTROL Extension] champ, sélectionnez [!UICONTROL SDK Web Adobe Experience Platform]. Pour le [!UICONTROL Type d’action] champ, sélectionnez [!UICONTROL Envoyer un événement].

Dans la partie droite de l’écran, recherchez le [!UICONTROL Type] champ et sélectionnez `web.webinteraction.linkClicks`.

Pour le [!UICONTROL Données XDM] , cliquez sur le bouton sélecteur d’élément de données et sélectionnez [!UICONTROL computedStateAndEventInfo]. Il s’agit de l’élément de données que vous venez de créer.

Pour cette règle (contrairement aux autres règles que vous avez créées), vous allez vérifier la variable [!UICONTROL Le document sera déchargé.] . Cela indique essentiellement au SDK que l’utilisateur quitte la page lorsqu’il clique sur le lien. Ceci est important, car cela permet au SDK d’effectuer la requête de manière à ce que, même si l’utilisateur quitte la page, la requête continue à s’exécuter en arrière-plan et atteigne le serveur. Si cette case n’est pas cochée, la demande ne sera pas faite de cette manière et sera donc probablement annulée lors du déchargement du document actif.

Vous vous demandez peut-être : &quot;Ça a l&#39;air sympa. Pourquoi cette option n’est-elle pas toujours activée alors ?&quot;

Eh bien, c’est un peu compliqué, mais lorsque vous utilisez cette fonctionnalité, le SDK utilise une méthode de navigateur appelée [`sendBeacon`](https://developer.mozilla.org/fr-FR/docs/Web/API/Navigator/sendBeacon) pour envoyer la demande. Lors de l’envoi d’une requête à l’aide de `sendBeacon`, le navigateur n’autorise pas le SDK (ni rien d’autre) à accéder aux données renvoyées par le serveur. Si le SDK devait utiliser cette fonctionnalité pour chaque demande, il ne serait jamais en mesure de recevoir des données du serveur. Pour cette raison, il est important de vérifier la variable [!UICONTROL Le document sera déchargé.] uniquement lorsque le document actif est déchargé, auquel cas les données de réponse peuvent être ignorées.

![Case à cocher Le document va se décharger](../../../assets/implementation-strategy/document-will-unload.png)

Enregistrez l’action en cliquant sur le bouton [!UICONTROL Conserver les modifications] bouton .

## Enregistrez la règle

Votre règle doit maintenant être terminée.

![Règle de clic sur le lien de l’application de téléchargement](../../../assets/implementation-strategy/download-app-link-clicked-rule.png)

Enregistrez la règle en cliquant sur [!UICONTROL Enregistrer].
