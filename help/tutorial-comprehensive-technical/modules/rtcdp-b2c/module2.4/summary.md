---
title: Audience Activation à Microsoft Azure Event Hub - Résumé et avantages
description: Audience Activation à Microsoft Azure Event Hub - Résumé et avantages
kt: 5342
doc-type: tutorial
exl-id: 3b598ffc-875e-468d-b91c-882062e8203f
source-git-commit: 216914c9d97827afaef90e21ed7d4f35eaef0cd3
workflow-type: tm+mt
source-wordcount: '291'
ht-degree: 1%

---

# Résumé et avantages

Félicitations et merci d’avoir consacré votre temps à découvrir Microsoft Azure Event Hub et Adobe Experience Platform !
Dans ce module, vous avez appris à configurer une instance Azure Event Hub et à la connecter à Adobe Experience Platform.

## Avantages

Mettons en évidence les avantages de l’intégration de Adobe Experience Platform à Microsoft Azure Event Hub :

- Microsoft Azure Event Hubs as as a Adobe Experience Platform Destination vous permet de capturer la qualification de l’audience en temps réel et de les traiter à l’aide d’une fonction Azure Event Hub. Avec une telle fonction Azure Event Hub, vous pouvez créer n’importe quel type de gestionnaire d’activation d’audience personnalisé et, de ce fait, intégrer n’importe quelle destination tierce.

- Bien que les destinations ne soient déclenchées que par des audiences spécifiées, la payload d’activation inclut toutes les audiences pour lesquelles un profil donné est admissible.

- Une audience ne déclenche une activation que lorsque son état change. Par exemple, un profil qui est qualifié quatre fois pour une audience sur une période de trois mois, seuls les deux premiers seront activés. Le premier est un changement d’état de à **get**, le second est déclenché par un changement d’état de **get** à **existing**.

- Lors de l’activation d’audiences pour les profils connus, une carte d’identité complète est incluse dans la payload d’activation. Votre fonction Azure peut utiliser l’une des identités disponibles pour mapper les audiences à un profil géré dans une application tierce, tout en utilisant l’identifiant client de l’application.

- Dans ce module, la fonction de hub d’événements a été déployée localement (mode de débogage dans Visual Studio Code), ce qui vous offre de nombreuses options de dépannage et de débogage.

## Consultez cette section

- S/O

[Revenir au module 2.4](./segment-activation-microsoft-azure-eventhub.md)

[Revenir à tous les modules](./../../../overview.md)
