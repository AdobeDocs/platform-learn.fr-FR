---
title: Collecte de données et transfert côté serveur en temps réel - Création et configuration d’une fonction cloud Google
description: Création et configuration d’une fonction cloud Google
kt: 5342
doc-type: tutorial
exl-id: bdee5a9b-2f1a-467e-9edc-a2e10a263694
source-git-commit: 3d61d91111d8693ab031fbd7b26706c02818108c
workflow-type: tm+mt
source-wordcount: '1189'
ht-degree: 1%

---

# 2.5.4 Transférer les événements au GCP Pub/Sub

>[!NOTE]
>
>Pour cet exercice, vous devez accéder à un environnement Google Cloud Platform. Si vous n&#39;avez pas encore accès à GCP, créez un compte en utilisant votre adresse e-mail personnelle.

## Création de votre publication/sous-rubrique Google Cloud

Accédez à [https://console.cloud.google.com/](https://console.cloud.google.com/). Dans la barre de recherche, saisissez `pub/sub`. Cliquez sur le résultat de la recherche **Pub/Sub - Global real-time messaging**.

![GCP](./images/gcp1.png)

Tu verras ça. Cliquez sur **CRÉER UNE RUBRIQUE**.

![GCP](./images/gcp2.png)

Tu verras ça. Pour votre ID de sujet, utilisez `--aepUserLdap---event-forwarding`. Cliquez sur **Créer**.

![GCP](./images/gcp6.png)

Votre rubrique est maintenant créée. Cliquez sur le sujet **ID d’abonnement**.

![GCP](./images/gcp7.png)

Tu verras ça. Copiez le **nom du sujet** dans le presse-papiers et enregistrez-le, car vous en aurez besoin dans les exercices suivants.

![GCP](./images/gcp8.png)

Accédons maintenant à Transfert d’événement de la collecte de données Adobe Experience Platform pour mettre à jour votre propriété Transfert d’événement afin de commencer à transférer les événements vers Pub/Sub.


## Mettez à jour votre propriété Transfert d’événement : Secrets

**Secrets** dans les propriétés de transfert d’événement sont utilisés pour stocker les informations d’identification qui seront utilisées pour s’authentifier sur les API externes. Dans cet exemple, vous devez configurer un secret pour stocker votre jeton OAuth de Google Cloud Platform, qui sera utilisé pour s’authentifier lors de l’utilisation de Pub/Sub pour diffuser des données vers GCP.

Accédez à [https://experience.adobe.com/#/data-collection/](https://experience.adobe.com/#/data-collection/) puis à **Secrets**. Cliquez sur **Créer un secret**.

![Adobe Experience Platform Data Collection SSF](./images/secret1.png)

Tu verras ça. Suivez ces instructions :

- Nom : use `--aepUserLdap---gcp-secret`
- Environnement cible : sélectionnez **Développement**
- Type : **Google OAuth 2**
- Cochez la case **Pub/Sub**

Cliquez sur **Créer un secret**.

![Adobe Experience Platform Data Collection SSF](./images/secret2.png)

Après avoir cliqué sur **Créer un secret**, une fenêtre contextuelle s’affiche pour configurer l’authentification entre le secret de votre propriété de transfert d’événement et Google. Cliquez sur **Créer et autoriser des `--aepUserLdap---gcp-secret` secrètes avec Google**.

![Adobe Experience Platform Data Collection SSF](./images/secret3.png)

Cliquez pour sélectionner votre compte Google.

![Adobe Experience Platform Data Collection SSF](./images/secret4.png)

Cliquez sur **Continuer**.

>[!NOTE]
>
>Votre message contextuel peut varier. Veuillez autoriser/autoriser l’accès demandé afin de poursuivre l’exercice.

![Adobe Experience Platform Data Collection SSF](./images/secret5.png)

Une fois l’authentification réussie, voici ce que vous verrez.

![Adobe Experience Platform Data Collection SSF](./images/secret6.png)

Votre secret est maintenant configuré avec succès et peut être utilisé dans un élément de données.

## Mettez à jour votre propriété Transfert d’événement : Élément de données

Pour utiliser votre secret dans votre propriété Transfert d’événement, vous devez créer un élément de données qui stockera la valeur du secret.

Accédez à [https://experience.adobe.com/#/data-collection/](https://experience.adobe.com/#/data-collection/) puis à **Transfert d’événement**. Recherchez votre propriété Transfert d’événement et cliquez dessus pour l’ouvrir.

![Adobe Experience Platform Data Collection SSF](./images/prop1.png)

Dans le menu de gauche, accédez à **Éléments de données**. Cliquez sur **Ajouter un élément de données**.

![Adobe Experience Platform Data Collection SSF](./images/de1gcp.png)

Configurez votre élément de données comme suit :

- Nom : **Secret GCP**
- Extension : **Core**
- Type D’Élément De Données : **Secret**
- Secret de développement : sélectionnez le secret que vous avez créé, nommé `--aepUserLdap---gcp-secret`

Cliquez sur **Enregistrer**.

![Adobe Experience Platform Data Collection SSF](./images/secret7.png)

## Mettez à jour votre propriété Transfert d’événement : Extension

Une fois votre secret et votre élément de données configurés, vous pouvez configurer l’extension de la plateforme cloud Google dans votre propriété Transfert d’événement.

Accédez à [https://experience.adobe.com/#/data-collection/](https://experience.adobe.com/#/data-collection/), accédez à **Transfert d’événement** et ouvrez votre propriété Transfert d’événement.

![Adobe Experience Platform Data Collection SSF](./images/prop1.png)

Ensuite, accédez à **Extensions**, à **Catalogue**. Cliquez sur l’extension **Google Cloud Platform**, puis sur **Installer**.

![Adobe Experience Platform Data Collection SSF](./images/gext2.png)

Tu verras ça. Cliquez sur l’icône Élément de données .

![Adobe Experience Platform Data Collection SSF](./images/gext3.png)

Sélectionnez l’élément de données que vous avez créé dans l’exercice précédent, qui est nommé **Secret GCP**. Cliquez sur **Sélectionner**.

![Adobe Experience Platform Data Collection SSF](./images/gext4.png)

Tu verras ça. Cliquez sur **Enregistrer**.

![Adobe Experience Platform Data Collection SSF](./images/gext5.png)

## Mettre à jour votre propriété Transfert d’événement : mettre à jour une règle

Maintenant que votre extension Google Cloud Platform est configurée, vous pouvez définir une règle pour commencer à transférer les données d’événement vers votre rubrique Pub/Sub. Pour ce faire, vous devez mettre à jour la règle **Toutes les pages** que vous avez créée dans l’un des exercices précédents.

Dans le menu de gauche, accédez à **Règles**. Dans l’exercice précédent, vous avez créé la règle **Toutes les pages**. Cliquez sur cette règle pour l’ouvrir.

![Adobe Experience Platform Data Collection SSF](./images/rl1gcp.png)

Tu feras ça. Cliquez sur l’icône **+** sous **Actions** pour ajouter une nouvelle action.

![Adobe Experience Platform Data Collection SSF](./images/rl2gcp.png)

Tu verras ça. Effectuez la sélection suivante :

- Sélectionnez l’**Extension** : **Google Cloud Platform**.
- Sélectionnez le **Type d’action** : **Envoyer les données à Cloud Pub/Sub**.

Cela devrait vous donner le **Nom** suivant : **Plateforme cloud Google - Envoyer les données à Cloud Pub/Sub**. Vous devriez maintenant voir ceci :

![Adobe Experience Platform Data Collection SSF](./images/rl5gcp.png)

Vous devez maintenant configurer la rubrique Pub/Sub que vous avez créée précédemment.

Vous pouvez trouver le **nom du sujet** ici, puis le copier.

![GCP](./images/gcp8.png)

Collez le **nom de la rubrique** dans votre configuration de règle. Cliquez ensuite sur l’icône de l’élément de données en regard du champ **Données (obligatoire)**.

![Adobe Experience Platform Data Collection SSF](./images/rl6gcp.png)

Sélectionnez **Événement XDM** et cliquez sur **Sélectionner**.

![Adobe Experience Platform Data Collection SSF](./images/rl7gcp.png)

Tu verras ça. Cliquez sur **Conserver les modifications**.

![Adobe Experience Platform Data Collection SSF](./images/rl8gcp.png)

Cliquez sur **Enregistrer**.

![Adobe Experience Platform Data Collection SSF](./images/rl9gcp.png)

Tu verras ça.

![Adobe Experience Platform Data Collection SSF](./images/rl10gcp.png)

## Publier vos modifications

Votre configuration est maintenant terminée. Accédez à **Flux de publication** pour publier vos modifications. Ouvrez votre bibliothèque de développement **Principal** en cliquant sur **Modifier** comme indiqué.

![Adobe Experience Platform Data Collection SSF](./images/rl12gcp.png)

Cliquez sur le bouton **Ajouter toutes les ressources modifiées**, après quoi votre règle et votre élément de données apparaîtront dans cette bibliothèque. Cliquez ensuite sur **Enregistrer et créer pour développement**. Vos modifications sont en cours de déploiement.

![Adobe Experience Platform Data Collection SSF](./images/rl13gcp.png)

Au bout de quelques minutes, vous verrez que le déploiement est terminé et prêt à être testé.

![Adobe Experience Platform Data Collection SSF](./images/rl14.png)

## Tester votre configuration

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

Basculez votre vue sur votre Google Cloud Pub/Sub et accédez à **MESSAGES**. Cliquez sur **EXTRAIRE** et au bout de quelques secondes, vous verrez des messages dans la liste. Cliquez sur un message pour visualiser son contenu.

![Configuration De La Collecte De Données Adobe Experience Platform](./images/hook3gcp.png)

Vous pouvez désormais voir la payload XDM de votre événement dans Google Pub/Sub. Vous avez maintenant envoyé avec succès les données collectées par la collecte de données Adobe Experience Platform, en temps réel, vers un point d’entrée Google Cloud Pub/Sub. De là, ces données peuvent être utilisées par n’importe quelle application Google Cloud Platform, telle que BigQuery pour le stockage et les rapports ou pour les cas d’utilisation de machine learning.

![Configuration De La Collecte De Données Adobe Experience Platform](./images/hook4gcp.png)

## Étapes suivantes

Accédez à [2.5.5 Transférer les événements vers AWS Kinesis et AWS S3](./ex5.md){target="_blank"}

Revenez à [Connexions Real-Time CDP : transfert d’événement](./aep-data-collection-ssf.md){target="_blank"}

Revenir à [Tous les modules](./../../../../overview.md){target="_blank"}
