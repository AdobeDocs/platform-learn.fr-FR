---
title: Bootcamp - Journey Optimizer Créez votre parcours
description: Bootcamp - Journey Optimizer Créez votre parcours
kt: 5342
audience: developer
doc-type: tutorial
activity: develop
exl-id: e4464502-60c8-4fba-a429-169b7a4516c8
source-git-commit: ead28f5631fc430c41e8c756b23dc69ffe19510e
workflow-type: tm+mt
source-wordcount: '220'
ht-degree: 3%

---

# 2.4 Test de votre parcours

## Flux de parcours client

Ouvrez une nouvelle fenêtre de navigateur incognito propre et accédez à [https://bootcamp.aepdemo.net](https://bootcamp.aepdemo.net). Cliquez sur **Tout autoriser**. En fonction du comportement de navigation dans le flux utilisateur précédent, vous verrez la personnalisation se produire sur la page d’accueil du site web.

![DSN](./images/web8a.png)

Cliquez sur le bouton **Profil** dans le coin supérieur droit de votre écran.

![Démonstration](./images/web8b.png)

Cliquez sur **Création d’un compte**.

![Démonstration](./images/pv5.png)

Renseignez tous les champs du formulaire. Utilisez une valeur réelle pour l’adresse email et le numéro de téléphone, car elle sera utilisée dans les exercices ultérieurs pour la diffusion des emails et des SMS.

![Démonstration](./images/pv7a.png)

Faites défiler l’écran vers le bas. Vous devez maintenant saisir l’eventID de l’événement personnalisé que vous avez créé dans l’exercice 2.2. Vous pouvez le trouver ici :

![ACOP](./images/payloadeventID.png)

L’identifiant d’événement est ce qui doit être envoyé à Adobe Experience Platform pour déclencher le parcours que vous avez créé. Il s’agit de l’eventID dans cet exemple : `19cab7852cdef99d25b6d5f1b6503da39d1f486b1d585743f97ed2d1e6b6c74f`

Remplissez l’eventID dans le champ . **Identifiant d’événement de création de compte** et cliquez sur **Enregistrer**.

![Démonstration](./images/pv8a.png)

Vous verrez alors ceci.

![Démonstration](./images/pv9.png)

Vous recevrez également cet e-mail, qui est l’e-mail que vous avez vous-même créé dans le cadre de cet exercice.

![Démonstration](./images/pv10a.png)

Vous avez maintenant terminé cet exercice.

Étape suivante : [2.5 Installation et utilisation de l’application mobile](./ex5.md)

[Retour au flux utilisateur 2](./uc2.md)

[Revenir à tous les modules](../../overview.md)
