---
title: Collecte de données Adobe Experience Platform et transfert côté serveur en temps réel - Créer et configurer un webhook personnalisé
description: Création et configuration d’un webhook personnalisé
kt: 5342
doc-type: tutorial
exl-id: bb712980-5910-4f01-976b-b7fcf03f5407
source-git-commit: b4a7144217a68bc0b1bc70b19afcbc52e226500f
workflow-type: tm+mt
source-wordcount: '1107'
ht-degree: 1%

---

# 2.5.3 Création et configuration d’un webhook personnalisé

## Créer votre webhook personnalisé

Accédez à [https://pipedream.com/requestbin](https://pipedream.com/requestbin). Vous avez déjà utilisé cette application dans le [SDK d’exercice 2.3.7 Destinations](./../../../modules/rtcdp-b2c/module2.3/ex7.md)

Si vous n’avez pas encore utilisé ce service, créez un compte, puis créez un espace de travail. Une fois l’espace de travail créé, vous verrez quelque chose de similaire.

Cliquez sur **copy** pour copier l’URL. Vous devrez spécifier cette URL lors de l’exercice suivant. L’URL dans cet exemple est `https://eodts05snjmjz67.m.pipedream.net`.

![demo](./images/webhook1.png)

Ce site web a maintenant créé ce webhook pour vous et vous pourrez configurer ce webhook dans votre **[!DNL Event Forwarding property]** pour commencer à tester le transfert des événements.

## Mettre à jour la propriété Event Forwarting : créer un élément de données

Accédez à [https://experience.adobe.com/#/data-collection/](https://experience.adobe.com/#/data-collection/) et à **Transfert d’événement**. Recherchez la propriété Event Forwarding et cliquez dessus pour l’ouvrir.

![Adobe Experience Platform Data Collection SSF](./images/prop1.png)

Dans le menu de gauche, accédez à **Data Elements**. Cliquez sur **Créer un élément de données**.

![Adobe Experience Platform Data Collection SSF](./images/de1.png)

Un nouvel élément de données à configurer s’affiche.

![Adobe Experience Platform Data Collection SSF](./images/de2.png)

Effectuez la sélection suivante :

- En tant que **Nom**, saisissez **Événement XDM**.
- En tant que **Extension**, sélectionnez **Core**.
- En tant que **Type d’élément de données**, sélectionnez **Chemin**.
- En tant que **Chemin**, sélectionnez **Lecture de données à partir de XDM (arc.event.xdm)**. En sélectionnant ce chemin, vous allez filtrer la section **XDM** de la payload d’événement envoyée par le site web ou l’application mobile dans Adobe Edge.

![Adobe Experience Platform Data Collection SSF](./images/de3.png)

Vous allez maintenant avoir ceci. Cliquez sur **Enregistrer**.

![Adobe Experience Platform Data Collection SSF](./images/de3a.png)

>[!NOTE]
>
>Dans le chemin ci-dessus, une référence est faite à **arc**. **arc** signifie Adobe Resource Context et **arc** signifie toujours l’objet disponible le plus élevé disponible dans le contexte côté serveur. Des enrichissements et des transformations peuvent être ajoutés à cet objet **arc** à l’aide des fonctions du serveur de collecte de données Adobe Experience Platform.
>
>Dans le chemin ci-dessus, une référence est faite à **event**. **event** correspond à un événement unique et le serveur de collecte de données Adobe Experience Platform évalue toujours chaque événement individuellement. Parfois, vous pouvez voir une référence à **events** dans la payload envoyée par le SDK Web côté client, mais dans le serveur de collecte de données Adobe Experience Platform, chaque événement est évalué individuellement.

## Mettre à jour la propriété du serveur de collecte de données Adobe Experience Platform : créer une règle

Dans le menu de gauche, accédez à **Règles**. Cliquez sur **Créer une règle**.

![Adobe Experience Platform Data Collection SSF](./images/rl1.png)

Vous verrez alors une nouvelle règle à configurer. Saisissez le **Nom** : **Toutes les pages**. Pour cet exercice, il n’est pas nécessaire de configurer une condition. À la place, vous allez configurer une action. Cliquez sur le bouton **+ Ajouter** sous **Actions**.

![Adobe Experience Platform Data Collection SSF](./images/rl2.png)

Vous verrez alors ceci. Effectuez la sélection suivante :

- Sélectionnez l’ **extension** : **Adobe Cloud Connector**.
- Sélectionnez le **Type d’action** : **Lancer l’appel de récupération**.

Cela devrait vous donner ce **Nom** : **Connecteur Adobe Cloud - Lancer l’appel de récupération**. Vous devriez maintenant voir ceci :

![Adobe Experience Platform Data Collection SSF](./images/rl4.png)

Configurez ensuite les éléments suivants :

- Remplacez la méthode de requête de GET par **POST**
- Saisissez l&#39;URL du webhook personnalisé que vous avez créé lors de l&#39;une des étapes précédentes, qui ressemble à ceci : `https://eodts05snjmjz67.m.pipedream.net`

Vous devriez maintenant avoir ceci. Ensuite, accédez à **Body**.

![Adobe Experience Platform Data Collection SSF](./images/rl6.png)

Vous verrez alors ceci. Cliquez sur l’icône d’élément de données comme indiqué ci-dessous.

![Adobe Experience Platform Data Collection SSF](./images/rl7.png)

Dans la fenêtre contextuelle, sélectionnez l’élément de données **XDM Event** que vous avez créé à l’étape précédente. Cliquez sur **Sélectionner**.

![Adobe Experience Platform Data Collection SSF](./images/rl8.png)

Vous verrez alors ceci. Cliquez sur **Conserver les modifications**.

![Adobe Experience Platform Data Collection SSF](./images/rl9.png)

Vous verrez alors ceci. Cliquez sur **Enregistrer**.

![Adobe Experience Platform Data Collection SSF](./images/rl10.png)

Vous avez maintenant configuré votre première règle dans une propriété Event Forwarding. Accédez à **Flux de publication** pour publier vos modifications.
Ouvrez votre bibliothèque de développement **Main** en cliquant sur **Modifier** comme indiqué.

![Adobe Experience Platform Data Collection SSF](./images/rl11.png)

Cliquez sur le bouton **Ajouter toutes les ressources modifiées**, après lequel votre règle et votre élément de données apparaîtront dans cette bibliothèque. Cliquez ensuite sur **Enregistrer et créer pour le développement**. Vos modifications sont en cours de déploiement.

![Adobe Experience Platform Data Collection SSF](./images/rl13.png)

Au bout de quelques minutes, vous verrez que le déploiement est terminé et prêt à être testé.

![Adobe Experience Platform Data Collection SSF](./images/rl14.png)

## Tester votre configuration

Accédez à [https://dsn.adobe.com](https://dsn.adobe.com). Une fois connecté avec votre Adobe ID, vous verrez ceci. Cliquez sur les 3 points **...** dans le projet de votre site web, puis cliquez sur **Exécuter** pour l’ouvrir.

![DSN](./../../datacollection/module1.1/images/web8.png)

Vous verrez alors votre site web de démonstration ouvert. Sélectionnez l’URL et copiez-la dans le presse-papiers.

![DSN](../../gettingstarted/gettingstarted/images/web3.png)

Ouvrez une nouvelle fenêtre de navigateur incognito.

![DSN](../../gettingstarted/gettingstarted/images/web4.png)

Collez l’URL de votre site web de démonstration, que vous avez copiée à l’étape précédente. Vous serez alors invité à vous connecter à l’aide de votre Adobe ID.

![DSN](../../gettingstarted/gettingstarted/images/web5.png)

Sélectionnez le type de compte et procédez à la connexion.

![DSN](../../gettingstarted/gettingstarted/images/web6.png)

Votre site web est alors chargé dans une fenêtre de navigateur incognito. Pour chaque exercice, vous devrez utiliser une fenêtre de navigateur incognito actualisée pour charger l’URL de votre site web de démonstration.

![DSN](../../gettingstarted/gettingstarted/images/web7.png)

Lorsque vous ouvrez la vue Développeur de votre navigateur, vous pouvez examiner les demandes réseau comme indiqué ci-dessous. Lorsque vous utilisez le filtre **interagit**, vous verrez les requêtes réseau envoyées par le client de collecte de données Adobe Experience Platform à Adobe Edge.

![Configuration de la collecte de données Adobe Experience Platform](./images/hook1.png)

Si vous sélectionnez la charge utile brute, accédez à [https://jsonformatter.org/json-pretty-print](https://jsonformatter.org/json-pretty-print) et collez la charge utile. Cliquez sur **Minify / Beautify**. Vous verrez ensuite la charge utile JSON, l’objet **events** et l’objet **xdm** . Lors de l’une des étapes précédentes, lorsque vous avez défini l’élément de données, vous avez utilisé la référence **arc.event.xdm**, ce qui vous permettra d’analyser l’objet **xdm** de cette payload.

![Configuration de la collecte de données Adobe Experience Platform](./images/hook2.png)

Basculez votre vue vers votre webhook personnalisé [https://webhook.site/](https://webhook.site/) que vous avez utilisé lors de l’une des étapes précédentes. Vous devriez maintenant avoir une vue similaire à celle-ci, avec les requêtes réseau affichées dans le menu de gauche. Vous voyez la charge utile **xdm** qui a été filtrée hors de la requête réseau qui a été affichée ci-dessus.

![Configuration de la collecte de données Adobe Experience Platform](./images/hook3.png)

Faites défiler la page vers le bas pour trouver le nom de la page, qui est dans ce cas **home**.

![Configuration de la collecte de données Adobe Experience Platform](./images/hook4.png)

Si vous parcourez désormais le site web, d’autres requêtes réseau seront disponibles en temps réel sur ce webhook personnalisé.

![Configuration de la collecte de données Adobe Experience Platform](./images/hook5.png)

Vous avez maintenant configuré le transfert côté serveur des événements des payloads Web SDK/XDM vers un webhook personnalisé externe. Dans les exercices suivants, vous allez configurer une approche similaire, et vous enverrez ces mêmes données vers les environnements Google et AWS.

Étape suivante : [2.5.4 Création et configuration d’une fonction cloud Google](./ex4.md)

[Revenir au module 2.5](./aep-data-collection-ssf.md)

[Revenir à tous les modules](./../../../overview.md)
