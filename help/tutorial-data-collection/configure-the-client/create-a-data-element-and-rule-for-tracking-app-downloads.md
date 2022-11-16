---
title: Création d’un élément de données et d’une règle pour le suivi des téléchargements d’applications
description: Création d’un élément de données et d’une règle pour le suivi des téléchargements d’applications
feature: Web SDK
exl-id: 8012ba48-38ac-4fb5-9876-8f57d1c5da5d
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '812'
ht-degree: 4%

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

Pour cette implémentation, vous envoyez un événement d’expérience à Adobe Experience Platform contenant le résultat fusionné de (1) l’état calculé de la couche de données et (2) le contenu de `eventInfo`.

Pour ce faire, vous devez créer un élément de données qui fusionne ces deux blocs d’informations.

## Créer un élément de données

Pour créer l’élément de données approprié :

1. Cliquez sur [!UICONTROL Éléments de données] dans le menu de gauche.
1. Cliquez ensuite sur le [!UICONTROL Créer un élément de données] lien.
1. Saisissez le nom de l’élément de données, `computedStateAndEventInfo`.
1. Pour le [!UICONTROL Extension] champ, sélectionnez [!UICONTROL Core] s’il n’est pas déjà sélectionné.
1. Pour le [!UICONTROL Type d’élément de données] champ, sélectionnez **[!UICONTROL Objets fusionnés]**. Cet élément de données vous permet de fusionner plusieurs objets. Le résultat fusionné est renvoyé par l’élément de données.
1. Ajoutez le premier objet que vous souhaitez inclure dans la fusion. Entrée `%event.fullState%` dans le [!UICONTROL Object(obligatoire)] champ . Lorsqu’elle est utilisée dans une règle déclenchée par une [!UICONTROL Données transférées] règle, cela fait référence à l’état calculé de la couche de données client Adobe au moment où la règle a été déclenchée.
1. Cliquez sur le bouton  **[!UICONTROL Ajouter un autre]** .
1. Ajoutez le deuxième objet. Entrée `%event.eventInfo%` dans le [!UICONTROL Object(obligatoire)] champ . Lorsqu’elle est utilisée dans une règle déclenchée par une [!UICONTROL Données transférées] événement de règle, qui fait référence à la variable `eventInfo` qui a été transmise à la couche de données client Adobe.
1. Enregistrez l’élément de données en cliquant sur le [!UICONTROL Enregistrer] bouton .
   ![élément de données computedStateAndEventInfo](../assets/computed-state-and-event-info-data-element.png)

L’élément de données est terminé.

## Créer une règle

Pour créer la règle pour le suivi des clics sur le [!UICONTROL Téléchargement de l’application] link:

1. Cliquez sur **[!UICONTROL Règles]** dans le menu de gauche.
1. Cliquez sur **[!UICONTROL Ajouter une règle]**.
1. Entrée **_Lien de l’application de téléchargement cliqué_** dans le [!UICONTROL Nom] champ .

## Ajout d’un événement

1. Cliquez sur le bouton **[!UICONTROL Ajouter]** sous [!UICONTROL Événements]. Vous affichez maintenant la vue d’événement.
1. Pour le [!UICONTROL Extension] champ, sélectionnez **[!UICONTROL Adobe de la couche de données client]**.
1. Pour le [!UICONTROL Type d’événement] champ, sélectionnez **[!UICONTROL Données transférées]**.
1. Cliquez sur **[!UICONTROL Conserver les modifications]**.
   ![Télécharger l’événement sur lequel l’application a cliqué](../assets/download-app-clicked-event.png)
Parce que vous souhaitez que cette règle soit déclenchée uniquement lorsque la variable `downloadAppClicked` est envoyé à la couche de données, sélectionnez l’événement **[!UICONTROL Evénement spécifique]** radio sous [!UICONTROL Écoute] et type **_downloadAppClicked_** dans la [!UICONTROL Événement/Clé à enregistrer pour]  Champ de texte affiché.

## Ajouter une action

Maintenant que vous revenez à la vue de règle :

1. Cliquez sur le bouton **[!UICONTROL Ajouter]** sous [!UICONTROL Actions].
1. Vous devriez maintenant être dans la vue d’action. Pour le [!UICONTROL Extension] champ, sélectionnez **[!UICONTROL SDK Web Adobe Experience Platform]**. Pour le [!UICONTROL Type d’action] champ, sélectionnez **[!UICONTROL Envoyer un événement]**.
1. Dans le [!UICONTROL Type] à droite, sélectionnez `web.webinteraction.linkClicks`.
1. Pour le [!UICONTROL Données XDM] , cliquez sur le bouton du sélecteur d’élément de données à droite et sélectionnez **[!UICONTROL computedStateAndEventInfo]**. Il s’agit de l’élément de données que vous avez récemment créé.
1. Pour cette règle (contrairement aux autres règles que vous avez créées), cochez la case **[!UICONTROL Le document sera déchargé.]** .
   ![Case à cocher Le document va se décharger](../assets/document-will-unload.png)
1. Enregistrez l’action en cliquant sur le bouton **[!UICONTROL Conserver les modifications]** bouton .

>[!TIP]
>
>Le [!UICONTROL Fonctionnalité de déchargement du document] indique au SDK que l’utilisateur quitte la page lorsqu’il clique sur le lien. Ceci est important, car cela permet au SDK d’effectuer la requête même si l’utilisateur quitte la page, car la requête continue de s’exécuter en arrière-plan et d’atteindre le serveur. Si cette case n’est pas cochée, la demande ne sera pas faite de cette manière et sera donc probablement annulée lors du déchargement du document actif.
>
>Vous vous demandez peut-être : &quot;Ça a l&#39;air sympa. Pourquoi cette option n’est-elle pas toujours activée alors ?&quot;
>
>Eh bien, c’est un peu compliqué, mais lorsque vous utilisez cette fonctionnalité, le SDK utilise une méthode de navigateur appelée [`sendBeacon`](https://developer.mozilla.org/en-US/docs/Web/API/Navigator/sendBeacon) pour envoyer la demande. Lors de l’envoi d’une requête à l’aide de `sendBeacon`, le navigateur n’autorise pas le SDK (ni rien d’autre) à accéder aux données renvoyées par le serveur. Si le SDK devait utiliser cette fonctionnalité pour chaque demande, il ne serait jamais en mesure de recevoir des données du serveur. Pour cette raison, il est important de vérifier la variable [!UICONTROL Le document sera déchargé.] uniquement lorsque le document actif est déchargé, auquel cas les données de réponse peuvent être ignorées.

## Enregistrez la règle

Votre règle doit maintenant être terminée.

1. Cliquez sur **[!UICONTROL Enregistrer]** dans le coin supérieur droit.
   ![Règle de clic sur le lien de l’application de téléchargement](../assets/download-app-link-clicked-rule.png)

[Suivant : ](publish-the-library.md)

>[!NOTE]
>
>Merci d’avoir consacré votre temps à l’apprentissage de la collecte de données. Si vous avez des questions, souhaitez partager des commentaires généraux ou avez des suggestions sur le contenu futur, partagez-les à ce sujet. [Article de discussion de la communauté Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-use-adobe-experience-platform-data/m-p/543877)