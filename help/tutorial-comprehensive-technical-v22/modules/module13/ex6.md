---
title: Activation de segment vers Microsoft Azure Event Hub - Action
description: Activation de segment vers Microsoft Azure Event Hub - Action
kt: 5342
audience: Data Engineer, Data Architect, Data Analyst
doc-type: tutorial
activity: develop
exl-id: 989dd2e4-597b-4b80-8b17-41aa6929ed64
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '560'
ht-degree: 0%

---

# 13.6 Scénario de bout en bout

## 13.6.1 Démarrage du déclencheur Azure Event Hub

Pour afficher la charge utile envoyée par la plateforme de données clients en temps réel de Adobe Experience Platform à notre hub d’événements Azure lors de la qualification du segment, nous devons démarrer notre simple fonction de déclenchement Azure Event Hub. Cette fonction &quot;décharge&quot; simplement la charge utile vers la console dans Visual Studio Code. Mais rappelez-vous que cette fonction peut être étendue de quelque manière que ce soit pour s&#39;adapter à toutes sortes d&#39;environnements à l&#39;aide d&#39;API et de protocoles dédiés.

### Lancement de Visual Studio Code et démarrage du projet

Assurez-vous que votre projet Visual Studio Code est ouvert et en cours d’exécution.

Pour démarrer/arrêter/redémarrer votre fonction Azure dans Visual Studio Code, reportez-vous aux exercices suivants :

- [Exercice 13.5.4 - Démarrage du projet Azure](./ex5.md)
- [Exercice 13.5.5 - Arrêter le projet Azure](./ex5.md)

Votre code Visual Studio **Terminal** doit mentionner quelque chose de similaire à ceci :

```code
[2022-02-23T05:03:41.429Z] Worker process started and initialized.
[2022-02-23T05:03:41.484Z] Debugger attached.
[2022-02-23T05:03:46.401Z] Host lock lease acquired by instance ID '000000000000000000000000D90C881B'.
```

![6-01-vsc-ready.png](./images/vsc31.png)

## 13.6.2 Chargement du site web Luma

Accédez à [https://builder.adobedemo.com/projects](https://builder.adobedemo.com/projects). Une fois connecté avec votre Adobe ID, vous verrez ceci. Cliquez sur le projet de votre site web pour l’ouvrir.

![DSN](../module0/images/web8.png)

Vous pouvez maintenant suivre le flux ci-dessous pour accéder au site web. Cliquez sur **Intégrations**.

![DSN](../module0/images/web1.png)

Sur le **Intégrations** , vous devez sélectionner la propriété de collecte de données qui a été créée dans l’exercice 0.1.

![DSN](../module0/images/web2.png)

Vous verrez alors votre site web de démonstration ouvert. Sélectionnez l’URL et copiez-la dans le presse-papiers.

![DSN](../module0/images/web3.png)

Ouvrez une nouvelle fenêtre de navigateur incognito.

![DSN](../module0/images/web4.png)

Collez l’URL de votre site web de démonstration, que vous avez copiée à l’étape précédente. Vous serez alors invité à vous connecter à l’aide de votre Adobe ID.

![DSN](../module0/images/web5.png)

Sélectionnez le type de compte et procédez à la connexion.

![DSN](../module0/images/web6.png)

Votre site web est alors chargé dans une fenêtre de navigateur incognito. Pour chaque démonstration, vous devez utiliser une fenêtre de navigateur incognito actualisée pour charger l’URL de votre site web de démonstration.

![DSN](../module0/images/web7.png)

## 13.6.3 Qualifier votre intérêt pour le segment Matériel

Accédez au **Matériel** une fois, et **ne pas le recharger ni l’actualiser**. Cette action doit vous permettre de `--demoProfileLdap-- - Interest in Equipment` segment.

![6-04-luma-telco-nav-sports.png](./images/luma1.png)

Pour vérifier, ouvrez le panneau Visionneuse de profils . Vous devez maintenant être membre de la fonction `--demoProfileLdap-- - Interest in Equipment`. Si les appartenances à vos segments ne sont pas encore mises à jour dans le panneau Visionneuse de profils, cliquez sur le bouton recharger .

![6-05-luma-telco-nav-broadband.png](./images/luma2.png)

Revenez à Visual Studio Code et regardez votre **TERMINAL** vous devriez voir une liste de segments pour votre **ECID**. Cette payload d’activation est diffusée vers votre centre d’événements dès que vous êtes admissible pour la `--demoProfileLdap-- - Interest in Equipment` segment.

Lorsque vous regardez de plus près la payload du segment, vous pouvez constater que `--demoProfileLdap-- - Interest in Equipment` est en état **réalisé**.

Un état de segment de **réalisé** signifie que notre profil vient de saisir le segment. Lorsque la variable **existant** status signifie que notre profil reste dans le segment.

![6-06-vsc-activation-realized.png](./images/luma3.png)

## 13.6.4 Consultez la page Matériel pour une seconde fois

Effectuez une actualisation irréversible de la variable **Matériel** page.

![6-07-back-to-sports.png](./images/luma1.png)

Maintenant, revenez à Visual Studio Code et vérifiez votre **TERMINAL** . Vous verrez que nous avons toujours votre segment, mais que celui-ci est maintenant à l’état **existant** ce qui signifie que notre profil reste dans le segment.

![6-08-vsc-activation-existing.png](./images/luma4.png)

## 13.6.5 Consultez la page Sports pour une troisième fois

Si vous revenez à la **Sports** pour la troisième fois, aucune activation n’a lieu, car aucun changement d’état n’est effectué d’un point de vue de segment.

Les activations de segment ne se produisent que lorsque l’état du segment change :

![6-09-segment-state-change.png](./images/6-09-segment-state-change.png)

Étape suivante : [Résumé et avantages](./summary.md)

[Revenir au module 13](./segment-activation-microsoft-azure-eventhub.md)

[Revenir à tous les modules](./../../overview.md)
