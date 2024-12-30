---
title: Adobe Journey Optimizer - Application d’une personnalisation dans un e-mail
description: Cet exercice explique comment utiliser la personnalisation de segment dans un contenu d’e-mail
kt: 5342
doc-type: tutorial
exl-id: bb5f8130-0237-4381-bc1e-f6b62950b1fc
source-git-commit: c531412a2c0a5c216f49560e01fb26b9b7e71869
workflow-type: tm+mt
source-wordcount: '483'
ht-degree: 11%

---

# 3.4.3 Appliquer une personnalisation dans un e-mail

Connectez-vous à Adobe Experience Cloud en allant sur [Adobe Experience Cloud](https://experience.adobe.com?lang=fr). Cliquez sur **Adobe Journey Optimizer**.

![ACOP ](./../../../modules/ajo-b2c/module3.1/images/acophome.png)

Vous serez redirigé vers la vue **Accueil** dans Journey Optimizer. Avant de continuer, vous devez sélectionner un **sandbox**. Le sandbox à sélectionner est nommé ``--aepTenantId--``.

![ACOP ](./../../../modules/ajo-b2c/module3.1/images/acoptriglp.png)

## 3.4.3.1 la personnalisation basée sur les segments

Dans cet exercice, vous allez améliorer votre e-mail de newsletter avec un texte personnalisé basé sur l’appartenance à un segment.

Accédez à **Parcours**. Recherchez le parcours de newsletter que vous avez créé dans l’exercice précédent. Recherchez `--aepUserLdap-- - Newsletter`. Cliquez sur votre parcours pour l’ouvrir.

![Journey Optimizer](./images/sbp1.png)

Tu verras ça. Cliquez sur **Dupliquer**.

![Journey Optimizer](./images/sbp2.png)

Cliquez sur **Dupliquer**.

![Journey Optimizer](./images/sbp3.png)

Sélectionnez votre action **E-mail** et cliquez sur **Modifier le contenu**.

![Journey Optimizer](./images/sbp3a.png)

Cliquez sur **Email Designer**.

![Journey Optimizer](./images/sbp4.png)

Tu verras ça.

![Journey Optimizer](./images/sbp5.png)

Ouvrez **Composants de contenu** et faites glisser un composant **Texte** sous le contenu actuel de la newsletter.

![Journey Optimizer](./images/sbp6.png)

Sélectionnez l’intégralité du texte par défaut et supprimez-le. Cliquez ensuite sur le bouton **Ajouter une personnalisation** dans la barre d’outils.

![Journey Optimizer](./images/sbp7.png)

Vous verrez alors ceci :

![Journey Optimizer](./images/seg1.png)

Dans le menu de gauche, cliquez sur **Abonnements aux segments**.

![Journey Optimizer](./images/seg2.png)

>[!NOTE]
>
>Si vous ne trouvez pas votre segment dans cette liste, faites défiler la liste vers le bas pour trouver des instructions sur la manière de récupérer manuellement l’identifiant du segment.

Sélectionnez l’`Luma - Women's Category Interest` du segment et cliquez sur l’icône **+**, qui doit se présenter comme suit :

![Journey Optimizer](./images/seg3.png)

Vous devez ensuite laisser la première ligne telle quelle et remplacer les lignes 2 et 3 par ce code :

``
    Psssst... a private sale in the women category will launch soon, we will keep you posted
{%else%}
    Thanks for taking the time to read our newsletter. Here is a 10% promo code to use on the website: READER10
{%/if%}
``

Voici ce que vous obtiendrez :

![Journey Optimizer](./images/seg4.png)

Cliquez sur **Valider** pour vous assurer que le code est correct. Cliquez sur **Enregistrer**.

![Journey Optimizer](./images/sbp8.png)

Vous pouvez maintenant enregistrer ce message en cliquant sur le bouton **Enregistrer** dans le coin supérieur droit. Cliquez ensuite sur **Simuler du contenu**.

![Journey Optimizer](./images/sbp9.png)

Sélectionnez l’un des profils que vous avez créés dans le cadre de ce tutoriel et cliquez sur **Aperçu**. Le résultat de votre configuration s’affiche ensuite.

![Journey Optimizer](./images/sbp10.png)

Tu verras ça. Cliquez ensuite sur **Fermer**.

![Journey Optimizer](./images/sbp10fff.png)

Revenez au tableau de bord des messages en cliquant sur la **flèche** en regard du texte de l’objet dans le coin supérieur gauche.

![Journey Optimizer](./images/sbp11.png)

Cliquez sur la flèche dans le coin supérieur gauche pour revenir au parcours.

![Journey Optimizer](./images/oc79afff.png)

Cliquez sur **Ok** pour fermer l’action de l’e-mail.

![Journey Optimizer](./images/oc79bfff.png)

Remplacez votre **Planification** par **Une fois** et définissez une **Date/Heure**. Cliquez sur **OK**.

>[!NOTE]
>
>La date et l’heure d’envoi du message doivent être comprises dans plus d’une heure.

![Journey Optimizer](./images/sbp18.png)

Cliquez sur le bouton **Publish** dans le parcours.

![Journey Optimizer](./images/sbp19.png)

Dans la fenêtre pop-up, cliquez de nouveau sur **Publish**.

![Journey Optimizer](./images/sbp20.png)

Votre parcours de newsletter de base est maintenant publié. Votre newsletter sera envoyée par e-mail selon votre calendrier et votre parcours s’arrêtera dès que le dernier e-mail aura été envoyé.

![Journey Optimizer](./images/sbp20fff.png)

Vous avez terminé cet exercice.

Étape suivante : [3.4.4 Configurer et utiliser des notifications push pour iOS](./ex4.md)

[Retour au module 3.4](./journeyoptimizer.md)

[Revenir à tous les modules](../../../overview.md)
