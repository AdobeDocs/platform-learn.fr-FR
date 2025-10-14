---
title: Audience Activation vers Microsoft Azure Event Hub - Action
description: Audience Activation vers Microsoft Azure Event Hub - Action
kt: 5342
doc-type: tutorial
exl-id: bff4d2ee-eaff-4b56-9fa0-4ffc3c368141
source-git-commit: 3d61d91111d8693ab031fbd7b26706c02818108c
workflow-type: tm+mt
source-wordcount: '427'
ht-degree: 0%

---

# 2.4.7 Scénario de bout en bout

## Démarrer le déclencheur Azure Event Hub

Pour afficher la payload envoyée par Adobe Experience Platform Real-time CDP à notre Azure Event Hub lors de la qualification de l’audience, nous devons démarrer notre simple fonction de déclenchement Azure Event Hub. Cette fonction va simplement « vider » la payload dans la console dans Visual Studio Code. Mais souvenez-vous que cette fonction peut être étendue de quelque manière que ce soit pour s’interfacer avec toutes sortes d’environnements à l’aide d’API et de protocoles dédiés.

### Lancer Visual Studio Code et démarrer le projet

Assurez-vous que votre projet Visual Studio Code est ouvert et en cours d’exécution

Pour démarrer/arrêter/redémarrer votre fonction Azure dans Visual Studio Code, reportez-vous à l’exercice précédent.

Le **Terminal** de votre Visual Studio Code devrait mentionner quelque chose de similaire à ceci :

```code
[2024-11-20T20:07:12.316Z] Debugger listening on ws://127.0.0.1:9229/86c8e251-8e2f-4c65-a063-cda77edbf2ca
[2024-11-20T20:07:12.318Z] For help, see: https://nodejs.org/en/docs/inspector
[2024-11-20T20:07:12.343Z] Worker process started and initialized.
[2024-11-20T20:07:12.359Z] Debugger attached.

Functions:

        vangeluw-aep-event-hub-trigger: eventHubTrigger

For detailed output, run func with --verbose flag.
[2024-11-20T20:07:18.150Z] Host lock lease acquired by instance ID '000000000000000000000000000C19D8'.
```

## Charger votre site Citi Signal

Accédez à [https://dsn.adobe.com](https://dsn.adobe.com). Après vous être connecté avec votre Adobe ID, voici ce que vous verrez. Cliquez sur le **de 3 points...** sur le projet de votre site web, puis cliquez sur **Exécuter** pour l’ouvrir.

![DSN &#x200B;](./../../datacollection/dc1.1/images/web8.png)

Vous verrez ensuite votre site web de démonstration s’ouvrir. Sélectionnez l’URL et copiez-la dans le presse-papiers.

![DSN &#x200B;](../../../getting-started/gettingstarted/images/web3.png)

Ouvrez une nouvelle fenêtre de navigateur en mode privé.

![DSN &#x200B;](../../../getting-started/gettingstarted/images/web4.png)

Collez l’URL de votre site web de démonstration, que vous avez copiée à l’étape précédente. Il vous sera ensuite demandé de vous connecter à l’aide de votre Adobe ID.

![DSN &#x200B;](../../../getting-started/gettingstarted/images/web5.png)

Sélectionnez votre type de compte et terminez le processus de connexion.

![DSN &#x200B;](../../../getting-started/gettingstarted/images/web6.png)

Votre site web est alors chargé dans une fenêtre de navigateur en mode privé. Pour chaque exercice, vous devrez utiliser une nouvelle fenêtre de navigateur en mode privé pour charger l’URL de votre site web de démonstration.

![DSN &#x200B;](../../../getting-started/gettingstarted/images/web7.png)

## Qualifier pour votre audience

Accédez à la page **Plans**. Cette action vous qualifiera pour l’audience `--aepUserLdap-- - Interest in Plans`.

![6-04-luma-telco-nav-sports.png](./images/cs1.png)

Pour vérifier, ouvrez le panneau Visionneuse de profils. Vous devriez maintenant être membre du `--aepUserLdap-- - Interest in Plans`. Si les appartenances à votre audience ne sont pas encore mises à jour dans le panneau Visionneuse de profils, cliquez sur le bouton recharger .

![6-05-luma-telco-nav-haut débit.png](./images/cs2.png)

Revenez à Visual Studio Code et consultez votre onglet **TERMINAL**. Vous devriez voir une liste d’audiences pour votre **ECID** spécifique. Cette payload d’activation est diffusée à votre centre d’événements dès que vous remplissez les conditions pour l’audience `--aepUserLdap-- - Interest in Plans`.

![6-06-vsc-activation-alized.png](./images/cs3.png)

Lorsque vous regardez de plus près la payload de l’audience, vous pouvez voir que `--aepUserLdap-- - Interest in Plans`’est en statut **réalisé**.

```json
{
  "identityMap": {
    "ecid": [
      {
        "id": "36281682065771928820739672071812090802"
      }
    ]
  },
  "segmentMembership": {
    "ups": {
      "94db5aed-b90e-478d-9637-9b0fad5bba11": {
        "createdAt": 1732129904025,
        "lastQualificationTime": "2024-11-21T07:33:52Z",
        "mappingCreatedAt": 1732130611000,
        "mappingUpdatedAt": 1732130611000,
        "name": "vangeluw - Interest in Plans",
        "status": "realized",
        "updatedAt": 1732129904025
      }
    }
  }
}
```

Le statut d’audience **réalisé** signifie que votre profil fait partie de l’audience, tandis que le statut **sorti** signifie que votre profil a été supprimé de l’audience.

## Étapes suivantes

Accédez à [&#x200B; Résumé et avantages &#x200B;](./summary.md){target="_blank"}

Revenez à [Real-Time CDP : Audience Activation vers Microsoft Azure Event Hub](./segment-activation-microsoft-azure-eventhub.md){target="_blank"}

Revenir à [Tous les modules](./../../../../overview.md){target="_blank"}
