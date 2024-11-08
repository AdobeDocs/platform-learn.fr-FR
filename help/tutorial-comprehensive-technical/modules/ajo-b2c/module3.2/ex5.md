---
title: Adobe Journey Optimizer - API météorologique externe, action SMS, etc. - Déclenchez votre Parcours client orchestré
description: Adobe Journey Optimizer - API météorologique externe, action SMS, etc. - Déclenchez votre Parcours client orchestré
kt: 5342
doc-type: tutorial
source-git-commit: 6962a0d37d375e751a05ae99b4f433b0283835d0
workflow-type: tm+mt
source-wordcount: '635'
ht-degree: 1%

---

# 3.2.5 Déclencher votre parcours

Dans cet exercice, vous allez tester et déclencher le parcours que vous avez configuré dans ce module.

## 3.2.5.1 Mise à jour de la configuration des événements de géobarrière

Accédez à [Adobe Experience Platform Data Collection](https://experience.adobe.com/launch/) et sélectionnez **Balises**.

Il s’agit de la page Propriétés de la collecte de données Adobe Experience Platform que vous avez déjà vue.

![Page Propriétés](./../../../modules/datacollection/module1.1/images/launch1.png)

Dans le module 0, Demo System a créé deux propriétés Client pour vous : une pour le site web et une pour l’application mobile. Recherchez-les en recherchant `--aepUserLdap--` dans la zone **[!UICONTROL Rechercher]**. Cliquez pour ouvrir la propriété **Web**.

![Zone de recherche](./../../../modules/datacollection/module1.1/images/property6.png)

Vous verrez alors ceci.

![Configuration de Launch](./images/rule1.png)

Dans le menu de gauche, accédez à **Rules** et recherchez la règle **Geofence event**. Cliquez sur la règle **Evénement de géolocalisation** pour l’ouvrir.

![Configuration de Launch](./images/rule2.png)

Vous verrez alors les détails de cette règle. Cliquez pour ouvrir l’action **Envoyer un événement de géobence à AEP - déclencher JO**.

![Configuration de Launch](./images/rule3.png)

Vous verrez ensuite que lorsque cette action est déclenchée, un élément de données spécifique est utilisé pour définir la structure de données XDM. Vous devez mettre à jour cet élément de données et définir l’**ID d’événement** de l’événement que vous avez configuré dans l’ [exercice 8.1](./ex1.md).

![Configuration de Launch](./images/rule4.png)

Vous devez maintenant mettre à jour l’élément de données **XDM - Événement de géofence**. Pour ce faire, accédez à **Data Elements**. Recherchez **XDM - Événement de géo-barrière** et cliquez pour ouvrir cet élément de données.

![Configuration de Launch](./images/rule5.png)

Vous verrez alors :

![Configuration de Launch](./images/rule6.png)

Accédez au champ `_experience.campaign.orchestration.eventID`. Supprimez la valeur actuelle et collez-y votre eventID.

Pour rappel, l’ID d’événement se trouve dans Adobe Journey Optimizer sous **Configurations > Événements** et vous trouverez l’ID d’événement dans l’exemple de charge utile de votre événement, qui ressemble à ceci : `"eventID": "fa42ab7982ba55f039eacec24c1e32e5c51b310c67f0fa559ab49b89b63f4934"`.

![ACOP](./images/payloadeventID.png)

Vous devez ensuite définir votre ville dans cet élément de données. Accédez à **placeContext > geo > city** et saisissez une ville de votre choix. Cliquez ensuite sur **Enregistrer** ou **Enregistrer dans la bibliothèque**.

![ACOP](./images/payloadeventIDgeo.png)

Enfin, vous devez publier vos modifications. Accédez à **Flux de publication** dans le menu de gauche.

![Configuration de Launch](./images/rule8.png)

Cliquez sur **Ajouter toutes les ressources modifiées**, puis sur **Enregistrer et créer dans le développement**.

![Configuration de Launch](./images/rule9.png)

## 3.2.5.2 Déclencher votre parcours

Accédez à [https://builder.adobedemo.com/projects](https://builder.adobedemo.com/projects). Une fois connecté avec votre Adobe ID, vous verrez ceci. Cliquez sur le projet de votre site web pour l’ouvrir.

![DSN](./../../../modules/gettingstarted/gettingstarted/images/web8.png)

Sur la page **Screens**, cliquez sur **Exécuter**.

![DSN](./../../../modules/datacollection/module1.1/images/web2.png)

Vous verrez alors votre site web de démonstration ouvert. Sélectionnez l’URL et copiez-la dans le presse-papiers.

![DSN](./../../../modules/gettingstarted/gettingstarted/images/web3.png)

Ouvrez une nouvelle fenêtre de navigateur incognito.

![DSN](./../../../modules/gettingstarted/gettingstarted/images/web4.png)

Collez l’URL de votre site web de démonstration, que vous avez copiée à l’étape précédente. Vous serez alors invité à vous connecter à l’aide de votre Adobe ID.

![DSN](./../../../modules/gettingstarted/gettingstarted/images/web5.png)

Sélectionnez le type de compte et procédez à la connexion.

![DSN](./../../../modules/gettingstarted/gettingstarted/images/web6.png)

Votre site web est alors chargé dans une fenêtre de navigateur incognito. Pour chaque démonstration, vous devez utiliser une fenêtre de navigateur incognito actualisée pour charger l’URL de votre site web de démonstration.

![DSN](./../../../modules/gettingstarted/gettingstarted/images/web7.png)

Cliquez sur l’icône représentant un logo d’Adobe dans le coin supérieur gauche de votre écran pour ouvrir la visionneuse de profils.

![Démonstration](./../../../modules/datacollection/module1.2/images/pv1.png)

Consultez le panneau Visionneuse de profils et Real-time Customer Profile avec l’**identifiant Experience Cloud** comme identifiant principal pour ce client actuellement inconnu.

![Démonstration](./../../../modules/datacollection/module1.2/images/pv2.png)

Accédez à la page Enregistrer/Connexion . Cliquez sur **CRÉER UN COMPTE**.

![Démonstration](./../../../modules/datacollection/module1.2/images/pv9.png)

Renseignez vos détails et cliquez sur **Enregistrer** après quoi vous serez redirigé vers la page précédente.

![Démonstration](./../../../modules/datacollection/module1.2/images/pv10.png)

Ouvrez le panneau Visionneuse de profils et accédez à Real-time Customer Profile. Dans le panneau Visionneuse de profils, toutes vos données personnelles doivent s’afficher, comme les identifiants de téléphone et d’adresse électronique que vous venez d’ajouter.

![Démonstration](./../../../modules/datacollection/module1.2/images/pv11.png)

Dans le panneau Visionneuse de profils, cliquez sur **UTILITIES**. Saisissez `geofenceevent` et cliquez sur **Send**.

![Démonstration](./images/smsdemo1.png)

Quelques secondes plus tard, vous recevrez un SMS de Adobe Journey Optimizer.

![Démonstration](./images/smsdemo4.png)

Étape suivante : [Résumé et avantages](./summary.md)

[Revenir au module 3.2](journey-orchestration-external-weather-api-sms.md)

[Revenir à tous les modules](../../../overview.md)
