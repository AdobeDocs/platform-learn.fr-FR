---
title: offer decisioning - Utilisez votre décision dans un email
description: Utiliser votre décision dans un email
kt: 5342
audience: Data Engineer, Data Architect, Orchestration Engineer, Marketer
doc-type: tutorial
activity: develop
exl-id: 0fb8c244-1025-479f-b82e-374d1aa5e4dc
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '373'
ht-degree: 11%

---

# 9.5 Utiliser votre décision dans un email

Dans cet exercice, vous utiliserez votre décision pour personnaliser la diffusion d’un email et d’un SMS.

Accédez à **Parcours**. Recherchez le parcours que vous avez créé dans l’exercice 7.2, qui est nommé `--demoProfileLdap-- - Account Creation Journey`. Cliquez sur votre parcours pour l’ouvrir.

![Journey Optimizer](./images/emailoffer1.png)

Vous verrez alors ceci. Cliquez sur **Création d’une version**.

![Journey Optimizer](./images/journey1.png)

Cliquez sur **Création d’une version**.

![Journey Optimizer](./images/journey2.png)

Cliquez sur le bouton **Email** puis cliquez sur **Modifier le contenu**.

![Journey Optimizer](./images/journey3.png)

Le tableau de bord du message s’affiche alors. Cliquez sur **Concepteur d&#39;email**.

![Journey Optimizer](./images/emailoffer2.png)

Vous verrez alors ceci.

![Journey Optimizer](./images/emailoffer5.png)

Vous verrez alors ceci. Faites glisser un nouveau **Colonne 1:1** composant de structure sur la zone de travail.

![Journey Optimizer](./images/emailoffer6.png)

Dans le menu, accédez à **Composants de contenu**. Sélectionnez la **Décision sur l’offre** et faites glisser et déposez ce composant dans l’espace réservé de l’offre de contenu de l’email comme indiqué. Cliquez ensuite sur **Ajouter**.

![Journey Optimizer](./images/emailoffer7.png)

Sélectionnez le type d’emplacement que vous souhaitez inclure dans le courrier électronique. Dans le **Emplacements** menu déroulant, sélectionnez **Email - Image**, puis sélectionnez votre décision `--demoProfileLdap-- - Luma Decision`. Cliquez sur **Ajouter**.

![Journey Optimizer](./images/emailoffer8.png)

Toutes les offres personnalisées et l’offre de secours sont désormais visibles dans le concepteur d’email. Cliquez sur  **Simulation du contenu** pour prévisualiser le message électronique avec un profil client réel.

![Journey Optimizer](./images/emailoffer9.png)

Commencez par identifier le profil que vous souhaitez utiliser pour la prévisualisation. Sélectionnez la **email** et saisissez l’adresse électronique d’un profil client que vous avez créé sur le site web de démonstration. Cliquez ensuite sur **Aperçu**.

![Journey Optimizer](./images/emailoffer10.png)

Une fois l&#39;email affiché et l&#39;offre correctement affichée, cliquez sur la **Fermer** bouton .

![Journey Optimizer](./images/emailoffer11.png)

Enfin, cliquez sur **Enregistrer**.

![Journey Optimizer](./images/emailoffer12.png)

Cliquez maintenant sur la flèche pour revenir à l’écran précédent.

![Journey Optimizer](./images/emailoffer13.png)

Vous verrez alors ceci. Cliquez sur la flèche dans le coin supérieur gauche pour revenir à votre parcours.

![Journey Optimizer](./images/emailoffer14.png)

Cliquez sur **Ok** pour fermer votre **Email** action.

![Journey Optimizer](./images/emailoffer14a.png)

Cliquez sur **Publier** pour publier votre parcours mis à jour.

![Journey Optimizer](./images/emailoffer14b.png)

Confirmer en cliquant sur **Publier** encore une fois.

![Journey Optimizer](./images/emailoffer15.png)

Votre message est maintenant publié.

![Journey Optimizer](./images/emailoffer16.png)

Lorsque vous créez un compte sur le site web de démonstration, vous obtenez maintenant cet e-mail :

![Journey Optimizer](./images/emailoffer17.png)

Vous avez terminé cet exercice.

Étape suivante : [9.6 Test de votre décision à l’aide de l’API](./ex6.md)

[Revenir au module 9](./offer-decisioning.md)

[Revenir à tous les modules](./../../overview.md)
