---
title: Offer decisioning - Utiliser votre décision dans un e-mail
description: Utiliser votre décision dans un e-mail
kt: 5342
doc-type: tutorial
source-git-commit: 91dbf1aac923c26608528b163bbd68218d45425b
workflow-type: tm+mt
source-wordcount: '310'
ht-degree: 11%

---

# 3.3.5 Utiliser votre décision dans un e-mail

Dans cet exercice, vous allez utiliser votre décision pour personnaliser la diffusion d’un e-mail et d’un SMS.

Accédez à **Parcours**. Recherchez le parcours que vous avez créé dans l’exercice 3.1.3, qui est nommé `--aepUserLdap-- - Registration Journey`. Cliquez sur votre parcours pour l’ouvrir.

![Journey Optimizer](./images/emailoffer1.png)

Tu verras ça. Cliquez sur **... Plus** puis cliquez sur **Créer une nouvelle version**.

![Journey Optimizer](./images/journey1.png)

Cliquez sur **Créer une version**.

![Journey Optimizer](./images/journey2.png)

Cliquez sur l’action **E-mail**, puis sur **Modifier le contenu**.

![Journey Optimizer](./images/journey3.png)

Le tableau de bord des messages s’affiche alors. Cliquez sur **Modifier le corps de l’e-mail**.

![Journey Optimizer](./images/emailoffer2.png)

Tu verras ça. Faites glisser un nouveau composant de structure de colonne **1:1** sur la zone de travail.

![Journey Optimizer](./images/emailoffer6.png)

Dans le menu, accédez à **Contenu**. Sélectionnez le composant **Décision d’offre** et faites glisser et déposez ce composant dans l’espace réservé de l’offre de contenu de l’e-mail, comme indiqué. Cliquez ensuite sur **Ajouter**.

![Journey Optimizer](./images/emailoffer7.png)

Sélectionnez le type d’emplacement à inclure dans l’e-mail. Dans le menu déroulant **Emplacements**, sélectionnez **E-mail - Image**, puis sélectionnez votre `--aepUserLdap-- - CitiSignal Decision` de décision. Cliquez sur **Ajouter**.

![Journey Optimizer](./images/emailoffer8.png)

Vous pouvez maintenant parcourir toutes les offres personnalisées et l&#39;offre de secours, toutes visualisées dans le Concepteur d&#39;email. Cliquez sur **Enregistrer**.

![Journey Optimizer](./images/emailoffer9.png)

Cliquez maintenant sur la flèche pour revenir à l’écran précédent.

![Journey Optimizer](./images/emailoffer13.png)

Cliquez sur la flèche dans le coin supérieur gauche pour revenir au parcours.

![Journey Optimizer](./images/emailoffer14.png)

Cliquez sur **Enregistrer** pour fermer l’action **E-mail**.

![Journey Optimizer](./images/emailoffer14a.png)

Cliquez sur **Publish** pour publier votre parcours mis à jour.

![Journey Optimizer](./images/emailoffer14b.png)

Confirmez en cliquant de nouveau sur **Publish**.

![Journey Optimizer](./images/emailoffer15.png)

Votre message est maintenant publié.

![Journey Optimizer](./images/emailoffer16.png)

Lorsque vous créez un compte sur le site web de démonstration, vous recevez désormais cet e-mail :

![Journey Optimizer](./images/emailoffer17.png)

Vous avez terminé cet exercice.

Étape suivante : [3.3.6 Tester votre décision à l’aide de l’API](./ex6.md)

[Retour au module 3.3](./offer-decisioning.md)

[Revenir à tous les modules](./../../../overview.md)
