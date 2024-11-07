---
title: Mise à jour de votre ID de configuration et test de votre Parcours
description: Mise à jour de votre ID de configuration et test de votre Parcours
kt: 5342
doc-type: tutorial
source-git-commit: 2cdc145d7f3933ec593db4e6f67b60961a674405
workflow-type: tm+mt
source-wordcount: '618'
ht-degree: 0%

---

# 3.1.3 Mise à jour de la propriété Collecte de données et test de votre parcours

## 3.1.3.1 Mise à jour de la propriété Collecte de données

Accédez à [Adobe Experience Platform Data Collection](https://experience.adobe.com/launch/) et sélectionnez **Balises**.

Il s’agit de la page Propriétés de la collecte de données Adobe Experience Platform que vous avez déjà vue.

![Page Propriétés](./../../../modules/datacollection/module1.1/images/launch1.png)

Dans le module 0, Demo System a créé deux propriétés Client pour vous : une pour le site web et une pour l’application mobile. Recherchez-les en recherchant `--demoProfileLdap--` dans la zone **[!UICONTROL Rechercher]**. Cliquez pour ouvrir la propriété **Web**.

![Zone de recherche](./../../../modules/datacollection/module1.1/images/property6.png)

Vous verrez alors ceci.

![Configuration de Launch](./images/rule1.png)

Dans le menu de gauche, accédez à **Règles** et recherchez la règle **Enregistrer le profil**. Cliquez sur la règle **Enregistrer le profil** pour l’ouvrir.

![Configuration de Launch](./images/rule2.png)

Vous verrez alors les détails de cette règle. Cliquez pour ouvrir l’action **Envoyer un événement d’enregistrement à AEP - déclencher JO**.

![Configuration de Launch](./images/rule3.png)

Vous verrez ensuite que lorsque cette action est déclenchée, un élément de données spécifique est utilisé pour définir la structure de données XDM. Vous devez mettre à jour cet élément de données et définir l’**ID d’événement** de l’événement que vous avez configuré dans l’ [exercice 7.1](./ex1.md).

![Configuration de Launch](./images/rule4.png)

Vous devez maintenant mettre à jour l’élément de données **XDM - Enregistrement de l’événement**. Pour ce faire, accédez à **Data Elements**. Recherchez **XDM - Registration Event** et cliquez pour ouvrir cet élément de données.

![Configuration de Launch](./images/rule5.png)

Vous verrez alors :

![Configuration de Launch](./images/rule6.png)

Accédez au champ `_experience.campaign.orchestration.eventID`. Supprimez la valeur actuelle et collez-y votre eventID.

Pour rappel, l’ID d’événement se trouve dans Adobe Journey Optimizer sous **Configurations > Événements** et vous trouverez l’ID d’événement dans l’exemple de charge utile de votre événement, qui ressemble à ceci : `"eventID": "227402c540eb8f8855c6b2333adf6d54d7153d9d7d56fa475a6866081c574736"`.

![ACOP](./images/payloadeventID.png)

Après avoir collé votre eventID, votre écran doit ressembler à celui-ci. Cliquez ensuite sur **Enregistrer** ou **Enregistrer dans la bibliothèque**.

![Configuration de Launch](./images/rule7.png)

Enfin, vous devez publier vos modifications. Accédez à **Flux de publication** dans le menu de gauche.

![Configuration de Launch](./images/rule8.png)

Cliquez sur **Ajouter toutes les ressources modifiées**, puis sur **Enregistrer et créer dans le développement**.

![Configuration de Launch](./images/rule9.png)

Votre bibliothèque sera alors mise à jour. Au bout de 1 à 2 minutes, vous pourrez ensuite poursuivre et tester votre configuration.

## 3.1.3.2 Test de votre Parcours

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

1 minute après avoir créé votre compte, vous recevrez de Adobe Journey Optimizer l’e-mail de création de votre compte.

![Configuration de Launch](./images/email.png)

Étape suivante : [Résumé et avantages](./summary.md)

[Revenir au module 3.1](./journey-orchestration-create-account.md)

[Revenir à tous les modules](../../../overview.md)
