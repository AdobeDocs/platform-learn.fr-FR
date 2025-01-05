---
title: Adobe Journey Optimizer - Application d’une personnalisation dans un e-mail
description: Cet exercice explique comment utiliser la personnalisation de segment dans un contenu d’e-mail
kt: 5342
doc-type: tutorial
exl-id: bb5f8130-0237-4381-bc1e-f6b62950b1fc
source-git-commit: 9865b5697abe2d344fb530636a1afc3f152a9e8f
workflow-type: tm+mt
source-wordcount: '399'
ht-degree: 9%

---

# 3.4.3 Appliquer une personnalisation basée sur les segments dans un e-mail

Connectez-vous à Adobe Experience Cloud en allant sur [Adobe Experience Cloud](https://experience.adobe.com?lang=fr). Cliquez sur **Adobe Journey Optimizer**.

![ACOP ](./../../../modules/ajo-b2c/module3.1/images/acophome.png)

Vous serez redirigé vers la vue **Accueil** dans Journey Optimizer. Avant de continuer, vous devez sélectionner un **sandbox**. Le sandbox à sélectionner est nommé ``--aepTenantId--``.

![ACOP ](./../../../modules/ajo-b2c/module3.1/images/acoptriglp.png)

## 3.4.3.1 la personnalisation basée sur les segments

Dans cet exercice, vous allez améliorer l’e-mail de newsletter que vous avez créé dans l’exercice précédent avec un texte personnalisé basé sur l’appartenance à un segment.

Accédez à **Campagnes**. Recherchez le parcours de newsletter que vous avez créé dans l’exercice précédent. Recherchez `--aepUserLdap-- - CitiSignal Newsletter`. Cliquez avec le bouton droit de la souris sur le **de 3 points...**, puis cliquez sur **Dupliquer**.

![Journey Optimizer](./images/sbp1.png)

Tu verras ça. Utilisez ceci pour le **Titre** : `--aepUserLdap-- - CitiSignal Newsletter (SBP)`. Cliquez sur **Dupliquer**.

![Journey Optimizer](./images/sbp2.png)

Cliquez sur la campagne dupliquée pour l’ouvrir.

![Journey Optimizer](./images/sbp3.png)

Cliquez sur **Modifier** pour modifier le contenu.

![Journey Optimizer](./images/sbp3a.png)

Cliquez sur **Modifier le corps de l’e-mail**.

![Journey Optimizer](./images/sbp4.png)

Tu verras ça.

![Journey Optimizer](./images/sbp5.png)

Ouvrez **Composants de contenu** et faites glisser une colonne **1:1** au-dessus de l’offre AirPods.

![Journey Optimizer](./images/sbp6.png)

Faites glisser et déposez un composant **Texte** dans cette colonne 1:1.

![Journey Optimizer](./images/sbp6a.png)

Sélectionnez l’intégralité du texte par défaut et supprimez-le. Cliquez ensuite sur le bouton **Ajouter une personnalisation** dans la barre d’outils.

![Journey Optimizer](./images/sbp7.png)

Tu verras ça. Dans le menu de gauche, cliquez sur **Audiences**.

![Journey Optimizer](./images/seg1.png)

Sélectionnez la `--aepUserLdap-- - Interest in Plans` du segment et cliquez sur l’icône **+** pour l’ajouter à la zone de travail.

![Journey Optimizer](./images/seg3.png)

Vous devez ensuite laisser la première ligne telle quelle et remplacer les lignes 2 et 3 par ce code :

``
    PS: It may be a good idea to check if your plan still meets your needs! Click here to be contacted by one of our experts!
{%else%}
    PS: Thanks for taking the time to read our newsletter. Here is a 10% promo code to use on the website: NEWSLETTER10
{%/if%}
``

Tu auras alors ceci. Cliquez sur **Enregistrer**.

![Journey Optimizer](./images/seg4.png)

Remplacez l’alignement du texte par **Alignement centré**.

![Journey Optimizer](./images/sbp9.png)

Vous pouvez maintenant enregistrer ce message en cliquant sur le bouton **Enregistrer** dans le coin supérieur droit. Cliquez ensuite sur **flèche** en regard du texte de l’objet dans le coin supérieur gauche.

![Journey Optimizer](./images/sbp9a.png)

Cliquez sur **Vérifier pour activer**.

![Journey Optimizer](./images/oc79afff.png)

Cliquez sur **Activer**.

![Journey Optimizer](./images/oc79bfff.png)

Votre newsletter avec la personnalisation basée sur les segments est maintenant publiée. Votre newsletter sera envoyée par e-mail selon votre calendrier et votre parcours s’arrêtera dès que le dernier e-mail aura été envoyé.

Si vous remplissez les critères pour le segment qui a été utilisé, vous verrez ceci dans l’e-mail que vous recevrez :

![Journey Optimizer](./images/sbp20fff.png)

Vous avez terminé cet exercice.

Étape suivante : [3.4.4 Configurer et utiliser des notifications push pour iOS](./ex4.md)

[Retour au module 3.4](./journeyoptimizer.md)

[Revenir à tous les modules](../../../overview.md)
