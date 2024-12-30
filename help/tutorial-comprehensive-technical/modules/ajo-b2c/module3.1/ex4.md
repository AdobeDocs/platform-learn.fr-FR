---
title: Mettre à jour votre ID de configuration et tester votre Parcours
description: Mettre à jour votre ID de configuration et tester votre Parcours
kt: 5342
doc-type: tutorial
source-git-commit: 2bd4249d96eb697da66db68895761f8b0bd6e638
workflow-type: tm+mt
source-wordcount: '628'
ht-degree: 1%

---

# 3.1.3 Mettre à jour la propriété de collecte de données et tester le parcours

## 3.1.3.1 Mettre à jour la propriété de la collecte de données

Accédez à [Collecte de données Adobe Experience Platform](https://experience.adobe.com/launch/) puis sélectionnez **Balises**.

![Page Propriétés](./../../../modules/datacollection/module1.1/images/launch1.png)

Dans **Prise en main**, le système de démonstration a créé deux propriétés client pour vous : une pour le site web et une pour l’application mobile. Recherchez-les en `--aepUserLdap--` dans la zone **[!UICONTROL Rechercher]**. Cliquez pour ouvrir la propriété **Web**.

![Zone de recherche](./../../../modules/datacollection/module1.1/images/property6.png)

Tu verras ça.

![Configuration de Launch](./images/rule1.png)

Dans le menu de gauche, accédez à **Règles** et recherchez la règle **Créer un compte**. Cliquez sur la règle **Créer un compte** pour l’ouvrir.

![Configuration de Launch](./images/rule2.png)

Vous verrez alors les détails de cette règle. Cliquez pour ouvrir l’action **Envoyer l’événement d’expérience « Événement d’enregistrement »**.

![Configuration de Launch](./images/rule3.png)

Vous constaterez ensuite que lorsque cette action est déclenchée, un élément de données spécifique est utilisé pour définir la structure de données XDM. Vous devez mettre à jour cet élément de données et définir l’**identifiant d’événement** de l’événement que vous avez configuré dans [Exercice 3.1.1](./ex1.md).

![Configuration de Launch](./images/rule4.png)

Vous devez maintenant procéder à la mise à jour de l’élément de données **XDM - Événement d’enregistrement**. Pour ce faire, accédez à **Éléments de données**. Recherchez **XDM - Enregistrement** et cliquez pour ouvrir cet élément de données.

![Configuration de Launch](./images/rule5.png)

Vous verrez alors ceci :

![Configuration de Launch](./images/rule6.png)

Accédez au `_experience.campaign.orchestration.eventID` de champs . Supprimez la valeur actuelle et collez-y votre eventID.

Pour rappel, l’identifiant d’événement se trouve dans Adobe Journey Optimizer sous **Configurations > Événements** et vous trouverez l’identifiant d’événement dans l’exemple de payload de votre événement, qui se présente comme suit : `"eventID": "5ae9b8d3f68eb555502b0c07d03ef71780600c4bd0373a4065c692ae0bfbd34d"`.

![ACOP ](./images/payloadeventID.png)

Après avoir collé votre eventID, l’écran doit se présenter comme suit : Cliquez ensuite sur **Enregistrer** ou **Enregistrer dans la bibliothèque**.

![Configuration de Launch](./images/rule7.png)

Enfin, vous devez publier vos modifications. Accédez à **Flux de publication** dans le menu de gauche, puis cliquez pour ouvrir votre bibliothèque **principale**.

![Configuration de Launch](./images/rule8.png)

Cliquez sur **Ajouter toutes les ressources modifiées** puis sur **Enregistrer et créer dans le développement**.

![Configuration de Launch](./images/rule9.png)

Votre bibliothèque sera alors mise à jour et, au bout de 1 à 2 minutes, vous pourrez tester votre configuration.

## 3.1.3.2 Tester votre Parcours

Accédez à [https://dsn.adobe.com](https://dsn.adobe.com). Après vous être connecté avec votre Adobe ID, voici ce que vous verrez. Cliquez sur le **de 3 points...** sur le projet de votre site web, puis cliquez sur **Exécuter** pour l’ouvrir.

![DSN ](./../../datacollection/module1.1/images/web8.png)

Vous verrez ensuite votre site web de démonstration s’ouvrir. Sélectionnez l’URL et copiez-la dans le presse-papiers.

![DSN ](../../gettingstarted/gettingstarted/images/web3.png)

Ouvrez une nouvelle fenêtre de navigateur en mode privé.

![DSN ](../../gettingstarted/gettingstarted/images/web4.png)

Collez l’URL de votre site web de démonstration, que vous avez copiée à l’étape précédente. Il vous sera ensuite demandé de vous connecter à l’aide de votre Adobe ID.

![DSN ](../../gettingstarted/gettingstarted/images/web5.png)

Sélectionnez votre type de compte et terminez le processus de connexion.

![DSN ](../../gettingstarted/gettingstarted/images/web6.png)

Votre site web est alors chargé dans une fenêtre de navigateur en mode privé. Pour chaque exercice, vous devrez utiliser une nouvelle fenêtre de navigateur en mode privé pour charger l’URL de votre site web de démonstration.

![DSN ](../../gettingstarted/gettingstarted/images/web7.png)

Cliquez sur l’icône du logo Adobe dans le coin supérieur gauche de l’écran pour ouvrir la visionneuse de profils.

![Démonstration](./../../../modules/datacollection/module1.2/images/pv1.png)

Affichez le panneau Visionneuse de profils et le profil client en temps réel avec l’ID **Experience Cloud** comme identifiant principal pour ce client actuellement inconnu. Cliquez sur **Se connecter**.

![Démonstration](./../../../modules/datacollection/module1.2/images/pv2.png)

Cliquez sur **CRÉER UN COMPTE**.

![Démonstration](./../../../modules/datacollection/module1.2/images/pv9.png)

Renseignez vos informations et cliquez sur **S’inscrire** après quoi vous serez redirigé vers la page précédente.

![Démonstration](./../../../modules/datacollection/module1.2/images/pv10.png)

Ouvrez le panneau Visionneuse de profils et accédez au profil client en temps réel. Dans le panneau Visionneuse de profil, toutes vos données personnelles doivent s’afficher, comme vos nouveaux identifiants d’e-mail et de téléphone ajoutés.

![Démonstration](./../../../modules/datacollection/module1.2/images/pv11.png)

1 minute après la création de votre compte, vous recevrez un e-mail de création de compte de Adobe Journey Optimizer.

![Configuration de Launch](./images/email.png)

Vous verrez également l’entrée du parcours et la progression à travers le parcours sur le tableau de bord du parcours dans Journey Optimizer.

![Configuration de Launch](./images/emaildash.png)

Étape suivante : [Résumé et avantages](./summary.md)

[Retour au module 3.1](./journey-orchestration-create-account.md)

[Revenir à tous les modules](../../../overview.md)
