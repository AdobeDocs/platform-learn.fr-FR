---
title: Bootcamp - Real-time Customer Profile - De inconnu à connu sur le site web
description: Bootcamp - Real-time Customer Profile - De inconnu à connu sur le site web
jira: KT-5342
audience: Data Engineer, Data Architect, Marketer
doc-type: tutorial
activity: develop
feature: Profiles
exl-id: 32a084a3-4c04-4367-947e-f7151fdad73b
source-git-commit: cd59a41f4533f18a54d80298ee9faf3a8ba3c6e7
workflow-type: tm+mt
source-wordcount: '418'
ht-degree: 1%

---

# 1.1 De inconnu à connu sur le site web

## Contexte

Le parcours de l’inconnu au connu est l’un des sujets les plus importants parmi les marques de nos jours, tout comme le parcours client de l’acquisition à la rétention.

Adobe Experience Platform joue un rôle énorme dans ce parcours. Platform est le cerveau de la communication, le **système d&#39;enregistrement d&#39;expérience**.

Platform est un environnement dans lequel le mot client est plus large que les clients connus. Un visiteur inconnu du site web est également un client du point de vue de Platform et, en tant que tel, tout le comportement en tant que visiteur inconnu est également envoyé à Platform. Grâce à cette approche, lorsque ce visiteur devient finalement un client connu, une marque peut également visualiser ce qui s’est produit avant ce moment. Cela s’avère utile du point de vue de l’attribution et de l’optimisation de l’expérience.

## Flux de parcours client

Accédez à [https://bootcamp.aepdemo.net](https://publish9122.adobedemo.com/content/aep-bootcamp-experience/language-masters/en.html). Cliquez sur **Autoriser tout**.

![DSN](./images/web8.png)

Cliquez sur l’icône représentant un logo d’Adobe dans le coin supérieur gauche de votre écran pour ouvrir la visionneuse de profils.

![Démonstration](./images/pv1.png)

Consultez le panneau Visionneuse de profils et Real-time Customer Profile avec l’**identifiant Experience Cloud** comme identifiant principal pour ce client actuellement inconnu.

![Démonstration](./images/pv2.png)

Vous pouvez également voir tous les événements d’expérience collectés en fonction du comportement du client. La liste est actuellement vide, mais elle va bientôt changer.

![Démonstration](./images/pv3.png)

Accédez à l’option de menu **Services d’application** et cliquez sur le produit **Real-Time CDP**.

![Démonstration](./images/pv4.png)

Vous verrez ensuite la page des détails du produit. Un événement d’expérience de type **Consultation produit** a maintenant été envoyé à Adobe Experience Platform à l’aide de l’implémentation du SDK Web que vous avez examinée dans le module 1. Ouvrez le panneau Visionneuse de profils et examinez vos **événements d’expérience**.

![Démonstration](./images/pv5.png)

Accédez à l’option de menu **Services d’application** et cliquez sur le produit **Adobe Journey Optimizer**. Un autre événement d’expérience a été envoyé à Adobe Experience Platform.

![Démonstration](./images/pv7.png)

Ouvrez le panneau Visionneuse de profils . Vous verrez désormais 2 événements d’expérience de type **Consultation produit**. Bien que le comportement soit anonyme, chaque clic est suivi et stocké dans Adobe Experience Platform. Une fois que le client anonyme sera connu, nous pourrons fusionner automatiquement tout comportement anonyme avec le profil de connaissance.

![Démonstration](./images/pv8.png)

Analysons maintenant votre profil client, puis utilisons votre comportement pour personnaliser votre expérience client sur le site web.

Étape suivante : [1.2 Visualisez votre propre profil client en temps réel - IU](./ex2.md)

[Retour au flux utilisateur 1](./uc1.md)

[Revenir à tous les modules](../../overview.md)
