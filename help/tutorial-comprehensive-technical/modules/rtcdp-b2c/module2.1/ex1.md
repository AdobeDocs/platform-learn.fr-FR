---
title: Foundation - Real-time Customer Profile - De inconnu à connu sur le site web
description: Foundation - Real-time Customer Profile - De inconnu à connu sur le site web
kt: 5342
doc-type: tutorial
exl-id: ddbf97c2-8105-42b6-b9bf-209b1df6a3b5
source-git-commit: 3a19e88e820c63294eff38bb8f699a9f690afcb9
workflow-type: tm+mt
source-wordcount: '968'
ht-degree: 2%

---

# 2.1.1 De inconnu à connu sur le site web

## Contexte

Le parcours de l’inconnu au connu est l’un des sujets les plus importants parmi les marques de nos jours, tout comme le parcours client de l’acquisition à la rétention.

Adobe Experience Platform joue un rôle énorme dans ce parcours. Platform est le cerveau de la communication, le &quot;système d&#39;enregistrement de l&#39;expérience&quot;.

Platform est un environnement dans lequel le mot client est plus large que les clients connus. Un visiteur inconnu du site web est également un client du point de vue de Platform et, en tant que tel, tout le comportement en tant que visiteur inconnu est également envoyé à Platform. Grâce à cette approche, lorsque ce visiteur devient finalement un client connu, une marque peut également visualiser ce qui s’est produit avant ce moment. Cela s’avère utile du point de vue de l’attribution et de l’optimisation de l’expérience.

## Flux de parcours client

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

Votre site web est alors chargé dans une fenêtre de navigateur incognito. Pour chaque démonstration, vous devez utiliser une fenêtre de navigateur incognito actualisée pour charger l’URL de votre site web de démonstration.

![DSN](../../gettingstarted/gettingstarted/images/web7.png)

Cliquez sur l’icône représentant un logo d’Adobe dans le coin supérieur gauche de votre écran pour ouvrir la visionneuse de profils.

![Démonstration](../../datacollection/module1.2/images/pv1.png)

Consultez le panneau Visionneuse de profils et Real-time Customer Profile avec l’**identifiant Experience Cloud** comme identifiant principal pour ce client actuellement inconnu.

![Démonstration](../../datacollection/module1.2/images/pv2.png)

Vous pouvez également voir tous les événements d’expérience collectés en fonction du comportement du client. La liste est actuellement vide, mais elle va bientôt changer.

![Démonstration](../../datacollection/module1.2/images/pv3.png)

Accédez à la catégorie de produits **Phones &amp; devices** . Cliquez ensuite sur le produit **iPhone 15 Pro**.

![Démonstration](../../datacollection/module1.2/images/pv4.png)

Vous verrez ensuite la page des détails du produit. Un événement d’expérience de type **Consultation produit** a maintenant été envoyé à Adobe Experience Platform à l’aide de l’implémentation du SDK Web que vous avez examinée dans le module 1.

![Démonstration](../../datacollection/module1.2/images/pv5.png)

Ouvrez le panneau Fournisseur de la visionneuse et observez vos **Événements d’expérience**.

![Démonstration](../../datacollection/module1.2/images/pv6.png)

Revenez à la page de catégorie **Téléphone et appareils** et cliquez sur un autre produit. Un autre événement d’expérience a été envoyé à Adobe Experience Platform. Ouvrez le panneau Visionneuse de profils . Vous verrez désormais 2 événements d’expérience de type **Consultation produit**. Bien que le comportement soit anonyme, avec le consentement approprié en place, vous pouvez suivre chaque clic et le stocker dans Adobe Experience Platform. Une fois que le client anonyme sera connu, nous pourrons fusionner automatiquement tout comportement anonyme avec le profil de connaissance.

![Démonstration](../../datacollection/module1.2/images/pv7.png)

Accédez à la page Enregistrer/Connexion . Cliquez sur **Se connecter**.

![Démonstration](../../datacollection/module1.2/images/pv8.png)

Cliquez sur **Créer un compte**.

![Démonstration](../../datacollection/module1.2/images/pv9.png)

Renseignez vos détails et cliquez sur **Enregistrer** après quoi vous serez redirigé vers la page précédente.

![Démonstration](../../datacollection/module1.2/images/pv10.png)

Ouvrez le panneau Visionneuse de profils et accédez à Real-time Customer Profile. Dans le panneau Visionneuse de profils, toutes vos données personnelles doivent s’afficher, comme les identifiants de téléphone et d’adresse électronique que vous venez d’ajouter.

![Démonstration](../../datacollection/module1.2/images/pv11.png)

Dans le panneau Visionneuse de profils, accédez à Événements d’expérience. Vous verrez les 2 produits que vous avez déjà consultés dans le panneau Visionneuse de profils . Ces deux événements sont désormais également connectés à votre profil &quot;connu&quot;.

![Démonstration](../../datacollection/module1.2/images/pv12.png)

Vous avez désormais ingéré des données dans Adobe Experience Platform et vous les avez liées à des identifiants tels que des ECID et des adresses électroniques. Le but est de comprendre le contexte commercial de ce que vous êtes sur le point de faire. Dans l’exercice suivant, vous allez commencer à configurer tout ce dont vous avez besoin pour rendre possible l’ingestion de données.

### Navigation dans l’application mobile

Après être devenu un client connu, il est temps de commencer à utiliser l’application mobile. Ouvrez l’application mobile sur votre iPhone, puis connectez-vous à l’application.

Si vous n’avez plus installé l’application ou si vous ne savez plus comment l’installer, veuillez consulter le lien suivant : [Utilisation de l’application mobile](../../gettingstarted/gettingstarted/ex5.md)

Après avoir installé l’application comme indiqué, la page d’entrée de l’application avec la marque Citi Signal chargée. Cliquez sur l’icône de compte dans la partie supérieure gauche de votre écran.

![Démonstration](./images/app_hp1.png)

Dans l’écran de connexion, connectez-vous à l’aide de l’adresse électronique que vous avez utilisée sur le site web du bureau. Cliquez sur **Login**.

![Démonstration](./images/app_acc.png)

Accédez à l’écran d’accueil de l’application et cliquez pour ouvrir un produit.

![Démonstration](./images/app_hp.png)

Vous verrez ensuite la page des détails du produit.

![Démonstration](./images/app_galaxy.png)

Accédez à l’écran d’accueil de l’application et faites glisser le curseur vers la gauche de l’écran pour afficher le panneau Visionneuse de profils . Vous verrez ensuite le produit que vous venez de consulter dans la section **Événements d’expérience**, ainsi que toutes les consultations de produit de la session de site web précédente.

>[!NOTE]
>
>Il peut s’écouler quelques minutes avant que l’affichage consolidé ne s’affiche dans l’application et sur le site web.

![Démonstration](./images/app_after_galaxy.png)

Revenez à votre ordinateur de bureau et actualisez la page d’accueil, après laquelle vous verrez également le produit s’y afficher.

>[!NOTE]
>
>Il peut s’écouler quelques minutes avant que l’affichage consolidé ne s’affiche dans l’application et sur le site web.

![Démonstration](./images/web_x_aftermobile.png)

Vous avez désormais ingéré des données dans Adobe Experience Platform et vous les avez liées à des identifiants tels que des ECID et des adresses électroniques. Le but de cet exercice était de comprendre le contexte commercial de ce que vous êtes sur le point de faire. Vous avez désormais créé un profil client en temps réel et multi-appareils. Au cours de l’exercice suivant, vous allez visualiser votre profil dans Adobe Experience Platform.

Étape suivante : [2.1.2 Visualiser votre propre profil client en temps réel - IU](./ex2.md)

[Revenir au module 2.1](./real-time-customer-profile.md)

[Revenir à tous les modules](../../../overview.md)
