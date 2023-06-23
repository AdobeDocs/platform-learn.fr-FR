---
title: Bootcamp - Fusion physique et numérique - Utilisez l’application mobile et déclenchez une entrée de balise.
description: Bootcamp - Fusion physique et numérique - Utilisez l’application mobile et déclenchez une entrée de balise.
jira: KT-5342
audience: Data Engineer, Data Architect, Marketer
doc-type: tutorial
activity: develop
exl-id: c33c973b-db8a-49ce-bd6c-a6c4fbe579a0
source-git-commit: 90f7621536573f60ac6585404b1ac0e49cb08496
workflow-type: tm+mt
source-wordcount: '533'
ht-degree: 0%

---

# 3.1 Utilisation de l’application mobile et déclenchement d’une entrée de balise

## Installation de l’application mobile

Avant d’installer l’application, vous devez activer **Tracking** sur votre appareil iOS. Pour ce faire, accédez à **Paramètres** > **Confidentialité et sécurité** > **Tracking** et assurez-vous que l’option **Autoriser les applications à demander pour effectuer le suivi**.

![DSN](./../uc3/images/app4.png)

Accédez à Apple App Store et recherchez `aepmobile-bootcamp`. Cliquez sur **Installer** ou **Télécharger**.

![DSN](./../uc3/images/app1.png)

Une fois l’application installée, cliquez sur **Ouvrir**.

![DSN](./../uc3/images/app2.png)

Cliquez sur **OK**.

![DSN](./../uc3/images/app9.png)

Cliquez sur **Autoriser**.

![DSN](./../uc3/images/app3.png)

Cliquez sur **Je suis d&#39;accord.**.

![DSN](./../uc3/images/app7.png)

Cliquez sur **Autoriser lors de l’utilisation de l’application**.

![DSN](./../uc3/images/app8.png)

Cliquez sur **Autoriser**.

![DSN](./../uc3/images/app5.png)

Vous êtes maintenant dans l’application, sur la page d’accueil, prêt à passer par le parcours client.

![DSN](./../uc3/images/app12.png)

## Flux de parcours client

Tout d&#39;abord, vous devez vous connecter. Cliquez sur **Ouverture de session**.

![DSN](./images/app13.png)

Après avoir créé votre compte dans les exercices précédents, vous l’avez vu sur le site web. Vous devez maintenant réutiliser l’adresse électronique du compte que vous avez créé dans l’application pour vous connecter.

![Démonstration](./images/pv1.png)

Saisissez ici l&#39;adresse email que vous avez utilisée sur le site web et cliquez sur **Connexion**.

![DSN](./images/app14.png)

Vous obtiendrez alors une confirmation de connexion et vous recevrez une notification push.

![DSN](./images/app15.png)

Revenez à la page d’accueil de l’application et d’autres fonctionnalités s’affichent.

![DSN](./images/app17.png)

Tout d’abord, accédez à **Produits**. Cliquez sur n’importe quel produit, dans cet exemple **Café à emporter**.

![DSN](./images/app19.png)

Vous verrez le **Café à emporter** page produit dans l’application.

![DSN](./images/app20.png)

Vous allez maintenant simuler un événement d’entrée de balise dans un emplacement de magasin hors ligne. L’objectif de la simulation est de personnaliser l’expérience client sur les écrans du magasin. Pour visualiser l’expérience en magasin, une page a été créée afin d’afficher dynamiquement les informations pertinentes pour le client qui vient d’entrer dans le magasin.

Avant de poursuivre, ouvrez cette page web sur votre ordinateur : [https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/screen.html](https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/screen.html)

Vous verrez alors :

![DSN](./images/screen1.png)

Ensuite, revenez à la page d’accueil. Cliquez sur le bouton **beacon** icône .

![DSN](./images/app23.png)

Vous verrez alors ceci. Tout d’abord, sélectionnez **Balise d’écran Bootcamp** puis cliquez sur le bouton **entrée** bouton . Vous pourrez ainsi simuler une entrée de balise.

![DSN](./images/app21.png)

Maintenant, regardez l&#39;écran du magasin. Le dernier produit que vous avez consulté s’affiche dans les 5 secondes qui suivent.

![DSN](./images/screen2.png)

Ensuite, revenez à **Produits**. Cliquez sur n’importe quel produit, dans cet exemple **Plage Tan**.

![DSN](./images/app22.png)

Ensuite, revenez à la page d’accueil. Cliquez sur le bouton **beacon** icône .

![DSN](./images/app23.png)

Vous verrez alors ceci. Tout d’abord, sélectionnez **Balise d’écran Bootcamp** puis cliquez sur le bouton **entrée** à nouveau. Vous pourrez ainsi simuler une entrée de balise.

![DSN](./images/app21.png)

Maintenant, regardez de nouveau l&#39;écran en magasin. Le dernier produit que vous avez consulté s’affiche dans les 5 secondes qui suivent.

![DSN](./images/screen3.png)

Jetons également un coup d’oeil à votre Visionneuse de profils sur le site web. De nombreux événements y ont été ajoutés, simplement pour montrer que toute interaction avec un client est collectée et stockée dans Adobe Experience Platform.

![DSN](./images/screen4.png)

Dans les exercices suivants, vous allez configurer et tester votre propre parcours d’entrée de balise.

Étape suivante : [3.2 Création de votre événement](./ex2.md)

[Retour au flux utilisateur 3](./uc3.md)

[Revenir à tous les modules](../../overview.md)
