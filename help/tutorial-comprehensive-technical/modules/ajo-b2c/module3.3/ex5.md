---
title: Offer decisioning - Utilisez votre décision dans un email
description: Utiliser votre décision dans un email
kt: 5342
doc-type: tutorial
source-git-commit: 6962a0d37d375e751a05ae99b4f433b0283835d0
workflow-type: tm+mt
source-wordcount: '381'
ht-degree: 11%

---

# 3.3.5 Utiliser votre décision dans un email

Dans cet exercice, vous utiliserez votre décision pour personnaliser la diffusion d’un email et d’un SMS.

Accédez à **Parcours**. Recherchez le parcours que vous avez créé dans l’exercice 7.2, intitulé `--aepUserLdap-- - Account Creation Journey`. Cliquez sur votre parcours pour l’ouvrir.

![Journey Optimizer](./images/emailoffer1.png)

Vous verrez alors ceci. Cliquez sur **Créer une version**.

![Journey Optimizer](./images/journey1.png)

Cliquez sur **Créer une version**.

![Journey Optimizer](./images/journey2.png)

Cliquez sur l&#39;action **Email**, puis sur **Modifier le contenu**.

![Journey Optimizer](./images/journey3.png)

Le tableau de bord du message s’affiche alors. Cliquez sur **Email Designer**.

![Journey Optimizer](./images/emailoffer2.png)

Vous verrez alors ceci.

![Journey Optimizer](./images/emailoffer5.png)

Vous verrez alors ceci. Faites glisser un nouveau composant de structure **1:1 column** sur la zone de travail.

![Journey Optimizer](./images/emailoffer6.png)

Dans le menu, accédez à **Composants du contenu**. Sélectionnez le composant **Offer Decision** et faites glisser et déposez ce composant dans l’espace réservé de l’offre de contenu du courrier électronique comme indiqué. Cliquez ensuite sur **Ajouter**.

![Journey Optimizer](./images/emailoffer7.png)

Sélectionnez le type d’emplacement que vous souhaitez inclure dans le courrier électronique. Dans le menu déroulant **Emplacements**, sélectionnez **Email - Image**, puis sélectionnez votre décision `--aepUserLdap-- - Luma Decision`. Cliquez sur **Ajouter**.

![Journey Optimizer](./images/emailoffer8.png)

Vous voyez maintenant toutes les offres personnalisées et l’offre de secours en cours de visualisation dans le concepteur d’email. Cliquez sur **Simuler le contenu** pour prévisualiser le message électronique avec un profil client réel.

![Journey Optimizer](./images/emailoffer9.png)

Commencez par identifier le profil que vous souhaitez utiliser pour la prévisualisation. Sélectionnez l’espace de noms **email** et saisissez l’adresse électronique d’un profil client que vous avez créé sur le site web de démonstration. Cliquez ensuite sur **Aperçu**.

![Journey Optimizer](./images/emailoffer10.png)

Une fois l&#39;email affiché et l&#39;offre correctement affichée, cliquez sur le bouton **Fermer** .

![Journey Optimizer](./images/emailoffer11.png)

Enfin, cliquez sur **Enregistrer**.

![Journey Optimizer](./images/emailoffer12.png)

Cliquez maintenant sur la flèche pour revenir à l’écran précédent.

![Journey Optimizer](./images/emailoffer13.png)

Vous verrez alors ceci. Cliquez sur la flèche dans le coin supérieur gauche pour revenir à votre parcours.

![Journey Optimizer](./images/emailoffer14.png)

Cliquez sur **Ok** pour fermer votre action **Email**.

![Journey Optimizer](./images/emailoffer14a.png)

Cliquez sur **Publish** pour publier votre parcours mis à jour.

![Journey Optimizer](./images/emailoffer14b.png)

Confirmez en cliquant de nouveau sur **Publish**.

![Journey Optimizer](./images/emailoffer15.png)

Votre message est maintenant publié.

![Journey Optimizer](./images/emailoffer16.png)

Lorsque vous créez un compte sur le site web de démonstration, vous obtenez maintenant cet e-mail :

![Journey Optimizer](./images/emailoffer17.png)

Vous avez terminé cet exercice.

Étape suivante : [3.3.6 Test de votre décision à l’aide de l’API](./ex6.md)

[Revenir au module 3.3](./offer-decisioning.md)

[Revenir à tous les modules](./../../../overview.md)
