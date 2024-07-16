---
title: Bootcamp - Fusion physique et numérique - Testez votre parcours
description: Bootcamp - Fusion physique et numérique - Testez votre parcours
jira: KT-5342
audience: developer
doc-type: tutorial
activity: develop
solution: Journey Optimizer
feature-set: Journey Optimizer
feature: Events
exl-id: 45c77177-9ea9-4c3d-a40e-c04a747938eb
source-git-commit: 3c86f9b19cecf92c9a324fb6fcfcefaebf82177f
workflow-type: tm+mt
source-wordcount: '193'
ht-degree: 0%

---

# 3.4 Test de votre parcours

Pour tester votre parcours, vous devez utiliser l’identifiant d’événement que vous avez créé dans l’exercice 3.2, qui ressemble à ceci.

![ACOP](./images/payloadeventID.png)

L’identifiant d’événement est ce qui doit être envoyé à Adobe Experience Platform pour déclencher le parcours. Dans cet exemple, eventID est :
`e76c0bf0c77c3517e5b6f4c457a0754ebaf5f1f6b9357d74e0d8e13ae517c3d5`.

Ouvrez l’application mobile et accédez à la page d’accueil. Cliquez sur l’icône **Paramètres** .

![DSN](./images/appsett.png)

Collez votre eventID dans le champ **Beacon EventID** et cliquez sur **Enregistrer**.

![DSN](./images/beacon1.png)

Avant de poursuivre, ouvrez cette page web sur votre ordinateur : [https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/screen.html](https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/screen.html)

Vous verrez alors :

![DSN](./images/screen1.png)

Ensuite, revenez à la page d’accueil. Cliquez sur l’icône **balise** .

![DSN](./images/app23.png)

Vous verrez alors ceci. Sélectionnez tout d&#39;abord **Bootcamp Screen Beacon** , puis cliquez sur le bouton **entry** . Vous pourrez ainsi simuler une entrée de balise.

![DSN](./images/app21.png)

Maintenant, regardez l&#39;écran du magasin. Le dernier produit que vous avez consulté s’affiche dans les 5 secondes qui suivent.

![DSN](./images/beacon3.png)

Vous avez également reçu votre notification push.

![DSN](./images/beacon2.png)

Vous avez maintenant terminé cet exercice.

[Retour au flux utilisateur 3](./uc3.md)

[Revenir à tous les modules](../../overview.md)
