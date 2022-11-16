---
title: Foundation - Real-time Customer Profile - De inconnu à connu sur le site web
description: Foundation - Real-time Customer Profile - De inconnu à connu sur le site web
kt: 5342
audience: Data Engineer, Data Architect, Marketer
doc-type: tutorial
activity: develop
exl-id: 065d79c5-8979-4992-afb1-4da47bbff74b
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '912'
ht-degree: 2%

---

# 3.1 De inconnu à connu sur le site web

## Contexte

Le parcours de l’inconnu au connu est l’un des sujets les plus importants parmi les marques de nos jours, tout comme le parcours client de l’acquisition à la rétention.

Adobe Experience Platform joue un rôle énorme dans ce parcours. Platform est le cerveau de la communication, le &quot;système d&#39;enregistrement de l&#39;expérience&quot;.

Platform est un environnement dans lequel le mot client est plus large que les clients connus. Un visiteur inconnu du site web est également un client du point de vue de Platform et, en tant que tel, tout le comportement en tant que visiteur inconnu est également envoyé à Platform. Grâce à cette approche, lorsque ce visiteur devient finalement un client connu, une marque peut également visualiser ce qui s’est produit avant ce moment. Cela s’avère utile du point de vue de l’attribution et de l’optimisation de l’expérience.

## Flux de parcours client

Accédez à [https://builder.adobedemo.com/projects](https://builder.adobedemo.com/projects). Une fois connecté avec votre Adobe ID, vous verrez ceci. Cliquez sur le projet de votre site web pour l’ouvrir.

![DSN](../module0/images/web8.png)

Sur le **Screens** page, cliquez sur **Exécuter**.

![DSN](../module1/images/web2.png)

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

Cliquez sur l’icône représentant un logo d’Adobe dans le coin supérieur gauche de votre écran pour ouvrir la visionneuse de profils.

![Démonstration](../module2/images/pv1.png)

Consultez le panneau Visionneuse de profils et le profil client en temps réel avec le **ID Experience Cloud** comme identifiant Principal de ce client actuellement inconnu.

![Démonstration](../module2/images/pv2.png)

Vous pouvez également voir tous les événements d’expérience collectés en fonction du comportement du client. La liste est actuellement vide, mais elle va bientôt changer.

![Démonstration](../module2/images/pv3.png)

Accédez au **Hommes** catégorie de produits. Cliquez ensuite sur le produit. **Vent de Montana**.

![Démonstration](../module2/images/pv4.png)

Vous verrez ensuite la page des détails du produit. Un événement d’expérience de type **Consultation produit** a maintenant été envoyé à Adobe Experience Platform à l’aide de l’implémentation du SDK Web que vous avez examinée dans le module 1.

![Démonstration](../module2/images/pv5.png)

Ouvrez le panneau Visionneuse de fournisseurs et examinez votre **Événements d’expérience**.

![Démonstration](../module2/images/pv6.png)

Revenez au **Femmes** page de catégorie, puis cliquez sur un autre produit. Un autre événement d’expérience a été envoyé à Adobe Experience Platform.

![Démonstration](../module2/images/pv7.png)

Ouvrez le panneau Visionneuse de profils . Vous verrez désormais deux événements d’expérience de type **Consultation produit**. Bien que le comportement soit anonyme, nous pouvons suivre chaque clic et le stocker dans Adobe Experience Platform. Une fois que le client anonyme sera connu, nous pourrons fusionner automatiquement tout comportement anonyme avec le profil de connaissance.

![Démonstration](../module2/images/pv8.png)

Accédez à la page Enregistrer/Connexion . Cliquez sur **CRÉATION D’UN COMPTE**.

![Démonstration](../module2/images/pv9.png)

Renseignez vos détails et cliquez sur **Enregistrer** après quoi vous serez redirigé vers la page précédente.

![Démonstration](../module2/images/pv10.png)

Ouvrez le panneau Visionneuse de profils et accédez à Real-time Customer Profile. Dans le panneau Visionneuse de profils, toutes vos données personnelles doivent s’afficher, comme les identifiants de téléphone et d’adresse électronique que vous venez d’ajouter.

![Démonstration](../module2/images/pv11.png)

Dans le panneau Visionneuse de profils, accédez à Événements d’expérience. Vous verrez les 2 produits que vous avez déjà consultés dans le panneau Visionneuse de profils . Ces deux événements sont désormais également connectés à votre profil &quot;connu&quot;.

![Démonstration](../module2/images/pv12.png)

Vous avez désormais ingéré des données dans Adobe Experience Platform et vous les avez liées à des identifiants tels que des ECID et des adresses électroniques. Le but est de comprendre le contexte commercial de ce que vous êtes sur le point de faire. Dans l’exercice suivant, vous allez commencer à configurer tout ce dont vous avez besoin pour rendre possible l’ingestion de données.

### Navigation dans l’application mobile

Après être devenu un client connu, il est temps de commencer à utiliser l’application mobile. Ouvrez l’application mobile sur votre iPhone, puis connectez-vous à l’application.

Si vous n’avez plus installé l’application ou si vous ne vous rappelez pas comment l’installer, veuillez consulter ce lien : [0.5 Utilisation de l’application mobile](../module0/ex5.md)

Une fois l’application installée comme indiqué, la page d’entrée de l’application avec la marque Luma chargée s’affiche. Cliquez sur l’icône de compte dans la partie supérieure gauche de votre écran.

![Démonstration](./images/app_hp.png)

Dans l’écran de connexion, connectez-vous à l’aide de l’adresse électronique que vous avez utilisée sur le site web du bureau. Cliquez sur **Ouverture de session**.

![Démonstration](./images/app_acc.png)

Accédez à l’écran d’accueil de l’application et cliquez pour ouvrir un produit.

![Démonstration](./images/app_hp.png)

Vous verrez ensuite la page des détails du produit.

![Démonstration](./images/app_carst.png)

Accédez à l’écran d’accueil de l’application et faites glisser le curseur vers la gauche de l’écran pour afficher le panneau Visionneuse de profils . Vous verrez alors le produit que vous venez de consulter dans la **Événements d’expérience** , ainsi que toutes les consultations de produits de la session de site web précédente.

![Démonstration](./images/app_after_carst.png)

Revenez à votre ordinateur de bureau et actualisez la page d’accueil, après laquelle vous verrez également le produit s’y afficher.

![Démonstration](./images/lb_x_aftermobile.png)

Vous avez désormais ingéré des données dans Adobe Experience Platform et vous les avez liées à des identifiants tels que des ECID et des adresses électroniques. Le but de cet exercice était de comprendre le contexte commercial de ce que vous êtes sur le point de faire. Vous avez désormais créé un profil client en temps réel et multi-appareils. Au cours de l’exercice suivant, vous allez visualiser votre profil dans Adobe Experience Platform.

Étape suivante : [3.2 Visualiser votre propre profil client en temps réel - interface utilisateur](./ex2.md)

[Revenir au module 3](./real-time-customer-profile.md)

[Revenir à tous les modules](../../overview.md)
