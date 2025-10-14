---
title: Adobe Journey Optimizer - Sources de données externes et actions personnalisées
description: Adobe Journey Optimizer - Sources de données externes et actions personnalisées
kt: 5342
doc-type: tutorial
exl-id: 068c8be4-2e9e-4d38-9c0e-f769ac927b57
source-git-commit: c531412a2c0a5c216f49560e01fb26b9b7e71869
workflow-type: tm+mt
source-wordcount: '624'
ht-degree: 0%

---

# 3.2.5 Déclenchement du parcours

Dans cet exercice, vous allez tester et déclencher le parcours que vous avez configuré dans ce module.

## 3.2.5.1 Mettre à jour la configuration de l’événement de limite géographique

Accédez à [Collecte de données Adobe Experience Platform](https://experience.adobe.com/launch/) puis sélectionnez **Balises**.

Il s’agit de la page Propriétés de la collecte de données Adobe Experience Platform que vous avez déjà vue.

![Page Propriétés](./../../../modules/datacollection/module1.1/images/launch1.png)

Dans **Prise en main**, le système de démonstration a créé deux propriétés client pour vous : une pour le site web et une pour l’application mobile. Recherchez-les en `--aepUserLdap--` dans la zone **[!UICONTROL Rechercher]**. Cliquez pour ouvrir la propriété **Web**.

![Zone de recherche](./../../../modules/datacollection/module1.1/images/property6.png)

Tu verras ça.

![Configuration de Launch](./images/rule1.png)

Dans le menu de gauche, accédez à **Règles** et recherchez la règle **Événement de limite géographique**. Cliquez sur la règle **Événement de limite géographique** pour l’ouvrir.

![Configuration de Launch](./images/rule2.png)

Vous verrez alors les détails de cette règle. Cliquez pour ouvrir l’action **Adobe Experience Platform Web SDK - Envoyer l’événement**.

![Configuration de Launch](./images/rule3.png)

Vous constaterez ensuite que lorsque cette action est déclenchée, un élément de données spécifique est utilisé pour définir la structure de données XDM. Vous devez mettre à jour cet élément de données et définir l’**identifiant d’événement** de l’événement que vous avez configuré dans [Exercice 3.2.1](./ex1.md).

![Configuration de Launch](./images/rule4.png)

Vous devez maintenant mettre à jour l’élément de données **XDM - Événement de limite géographique**. Pour ce faire, accédez à **Éléments de données**. Recherchez **XDM - Événement de limite géographique** et cliquez pour ouvrir cet élément de données.

![Configuration de Launch](./images/rule5.png)

Vous verrez alors ceci :

![Configuration de Launch](./images/rule6.png)

Accédez au `_experience.campaign.orchestration.eventID` de champs . Supprimez la valeur actuelle et collez-y votre eventID.

Pour rappel, l’identifiant d’événement se trouve dans Adobe Journey Optimizer sous **Configurations > Événements** et vous trouverez l’identifiant d’événement dans l’exemple de payload de votre événement, qui se présente comme suit : `"eventID": "4df8dc10731eba7b0c37af83a9db38d4de7aa6aebcce38196d9d47929b9c598e"`.

![ACOP &#x200B;](./images/payloadeventID.png)

Définissez ensuite votre ville dans cet élément de données. Accédez à **placeContext > geo > city** et saisissez la ville de votre choix. Cliquez ensuite sur **Enregistrer** ou **Enregistrer dans la bibliothèque**.

![ACOP &#x200B;](./images/payloadeventIDgeo.png)

Enfin, vous devez publier vos modifications. Accédez à **Flux de publication** dans le menu de gauche, puis cliquez sur **Man** pour ouvrir votre bibliothèque.

![Configuration de Launch](./images/rule8.png)

Cliquez sur **Ajouter toutes les ressources modifiées** puis sur **Enregistrer et créer dans le développement**.

![Configuration de Launch](./images/rule9.png)

## 3.2.5.2 Déclencher votre parcours

Accédez à [https://dsn.adobe.com](https://dsn.adobe.com). Après vous être connecté avec votre Adobe ID, voici ce que vous verrez. Cliquez sur le **de 3 points...** sur le projet de votre site web, puis cliquez sur **Exécuter** pour l’ouvrir.

![DSN &#x200B;](./../../datacollection/module1.1/images/web8.png)

Vous verrez ensuite votre site web de démonstration s’ouvrir. Sélectionnez l’URL et copiez-la dans le presse-papiers.

![DSN &#x200B;](../../gettingstarted/gettingstarted/images/web3.png)

Ouvrez une nouvelle fenêtre de navigateur en mode privé.

![DSN &#x200B;](../../gettingstarted/gettingstarted/images/web4.png)

Collez l’URL de votre site web de démonstration, que vous avez copiée à l’étape précédente. Il vous sera ensuite demandé de vous connecter à l’aide de votre Adobe ID.

![DSN &#x200B;](../../gettingstarted/gettingstarted/images/web5.png)

Sélectionnez votre type de compte et terminez le processus de connexion.

![DSN &#x200B;](../../gettingstarted/gettingstarted/images/web6.png)

Votre site web est alors chargé dans une fenêtre de navigateur en mode privé. Pour chaque exercice, vous devrez utiliser une nouvelle fenêtre de navigateur en mode privé pour charger l’URL de votre site web de démonstration.

![DSN &#x200B;](../../gettingstarted/gettingstarted/images/web7.png)

Cliquez sur l’icône du logo Adobe dans le coin supérieur gauche de l’écran pour ouvrir la visionneuse de profils.

![Démonstration](./../../../modules/datacollection/module1.2/images/pv1.png)

Ouvrez le panneau Visionneuse de profils et accédez au profil client en temps réel. Dans le panneau Visionneuse de profil, toutes vos données personnelles doivent s’afficher, comme vos nouveaux identifiants d’e-mail et de téléphone ajoutés.

![Démonstration](./images/pv2.png)

Dans le panneau Visionneuse de profils, cliquez sur **UTILITAIRES**. Saisissez `geofenceevent` et cliquez sur **Envoyer**.

>[!NOTE]
>
>Si vous ne disposez pas de la possibilité d’envoyer un événement d’appel direct dans le panneau de la visionneuse de profil, vous pouvez en envoyer un manuellement en ouvrant la vue Développeur de votre navigateur et en accédant à **Console**, puis coller et envoyer cette commande : `_satellite.track('geofenceevent')`.

Quelques secondes plus tard, le message de Adobe Journey Optimizer s’affichera dans le canal du Slack.

![Démonstration](./images/smsdemo4.png)

Étape suivante : [Résumé et avantages](./summary.md)

[Retour au module 3.2](journey-orchestration-external-weather-api-sms.md)

[Revenir à tous les modules](../../../overview.md)
