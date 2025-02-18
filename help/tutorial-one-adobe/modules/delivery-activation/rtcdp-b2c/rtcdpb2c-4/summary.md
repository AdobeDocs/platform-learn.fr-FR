---
title: Audience Activation vers Microsoft Azure Event Hub - Résumé et avantages
description: Audience Activation vers Microsoft Azure Event Hub - Résumé et avantages
kt: 5342
doc-type: tutorial
exl-id: f081af11-3ea0-47cc-ae74-24a0e0231d66
source-git-commit: 3d61d91111d8693ab031fbd7b26706c02818108c
workflow-type: tm+mt
source-wordcount: '300'
ht-degree: 1%

---

# Résumé et avantages

Félicitations et merci d’avoir investi votre temps dans votre apprentissage de Microsoft Azure Event Hub et de Adobe Experience Platform !
Dans ce module, vous avez appris à configurer une instance Azure Event Hub et à la connecter à Adobe Experience Platform.

## Avantages

Examinons les avantages de l’intégration de Adobe Experience Platform à Microsoft Azure Event Hub :

- Microsoft Azure Event Hubs as a Adobe Experience Platform Destination vous permet de capturer la qualification des audiences en temps réel et de la traiter à l’aide d’une fonction Azure Event Hub. Avec une telle fonction Azure Event Hub, vous pouvez créer n’importe quel type de gestionnaire d’activation d’audience personnalisé et intégrer à ce titre n’importe quel type de destination tierce.

- Bien que les destinations soient déclenchées uniquement par des audiences spécifiées, la payload d’activation inclut toutes les audiences pour lesquelles un profil donné se qualifie.

- Une audience ne déclenche une activation que lorsque son statut change. Par exemple, un profil qui se qualifie quatre fois pour une audience sur une période de trois mois, seuls les deux premiers seront activés. La première est un changement d’état de à **réalisé**, la seconde est déclenchée par un changement d’état de **réalisé** à **existant**.

- Lors de l’activation des audiences pour les profils connus, un mappage d’identité complet est inclus dans le payload d’activation. Votre fonction Azure peut utiliser n’importe quelle identité disponible pour mapper les audiences à un profil géré dans une application tierce, tout en utilisant l’identifiant client de l’application.

- Dans ce module, la fonction de hub d’événements a été déployée localement (mode débogage dans Visual Studio Code), ce qui vous offre de nombreuses options de dépannage et de débogage.

## Consulter ceci

- S/O

## Étapes suivantes

Revenez à [Real-Time CDP : Audience Activation vers Microsoft Azure Event Hub](./segment-activation-microsoft-azure-eventhub.md){target="_blank"}

Revenir à [Tous les modules](./../../../../overview.md){target="_blank"}
