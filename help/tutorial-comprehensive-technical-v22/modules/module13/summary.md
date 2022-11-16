---
title: Activation des segments vers Microsoft Azure Event Hub - Résumé et avantages
description: Activation des segments vers Microsoft Azure Event Hub - Résumé et avantages
kt: 5342
audience: Data Engineer, Data Architect, Data Analyst
doc-type: tutorial
activity: develop
exl-id: 2174ac52-b5dd-4bc8-ab5f-4d84ae9ef19b
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '290'
ht-degree: 1%

---

# Résumé et avantages

Félicitations et merci d’avoir consacré votre temps à découvrir Microsoft Azure Event Hub et Adobe Experience Platform !
Dans ce module, vous avez appris à configurer une instance Azure Event Hub et à la connecter à Adobe Experience Platform.

## Avantages

Mettons en évidence les avantages de l’intégration de Adobe Experience Platform à Microsoft Azure Event Hub :

- Microsoft Azure Event Hubs as as a Adobe Experience Platform Destination vous permet de capturer la qualification de segment en temps réel et de les traiter à l’aide d’une fonction Azure Event Hub. Avec une telle fonction Azure Event Hub, vous pouvez créer n’importe quel type de gestionnaire d’activation de segment personnalisé et, de ce fait, intégrer n’importe quelle destination tierce.

- Bien que les destinations ne soient déclenchées que par des segments spécifiés, la charge utile d’activation inclut tous les segments pour lesquels un profil donné est admissible.

- Un segment déclenche une activation uniquement lorsque son état change. Par exemple, un profil qui est qualifié quatre fois pour un segment sur une période de trois mois, seuls les deux premiers seront activés. Le premier est un changement d’état de à **réalisé**, la seconde est déclenchée par un changement d’état de **réalisé** to **existant**.

- Lors de l’activation de segments pour les profils connus, une carte d’identité complète est incluse dans la payload d’activation. Votre fonction Azure peut utiliser l’une des identités disponibles pour mapper les segments à un profil géré dans une application tierce, tout en utilisant l’identifiant client de l’application.

- Dans ce module, la fonction de hub d’événements a été déployée localement (mode de débogage dans Visual Studio Code), ce qui vous offre de nombreuses options de dépannage et de débogage.

## Consultez cette section

- S/O

[Revenir au module 13](./segment-activation-microsoft-azure-eventhub.md)

[Revenir à tous les modules](./../../overview.md)
