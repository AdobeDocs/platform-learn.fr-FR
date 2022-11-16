---
title: Adobe Journey Optimizer - Appliquer la personnalisation à un email
description: Cet exercice explique comment utiliser la personnalisation de segment dans un contenu d’email
kt: 5342
audience: Data Engineer, Data Architect, Data Analyst
doc-type: tutorial
activity: develop
exl-id: 573ecfba-4f1d-4242-8358-1d33109aaea3
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '495'
ht-degree: 11%

---

# 10.3 Appliquer la personnalisation à un email

Connectez-vous à Adobe Experience Cloud en accédant à [Adobe Experience Cloud](https://experience.adobe.com). Cliquez sur **Adobe Journey Optimizer**.

![ACOP](../module7/images/acophome.png)

Vous serez redirigé vers le **Accueil** dans Journey Optimizer. Avant de continuer, vous devez sélectionner une **sandbox**. L’environnement de test à sélectionner est nommé ``--aepTenantId--``. Pour ce faire, cliquez sur le texte **[!UICONTROL Production Prod]** dans la ligne bleue en haut de votre écran.

![ACOP](../module7/images/acoptriglp.png)

## 10.3.1 Personnalisation basée sur les segments

Dans cet exercice, vous améliorerez votre message électronique de newsletter avec un texte personnalisé basé sur l’adhésion au segment.

Accédez à **Parcours**. Recherchez le parcours de newsletter que vous avez créé lors de l’exercice précédent. Recherchez `--demoProfileLdap-- - Newsletter`. Cliquez sur votre parcours pour l’ouvrir.

![Journey Optimizer](./images/sbp1.png)

Vous verrez alors ceci. Cliquez sur **Dupliquer**.

![Journey Optimizer](./images/sbp2.png)

Cliquez sur ** Dupliquer**.

![Journey Optimizer](./images/sbp3.png)

Sélectionnez votre **Email** action et clic **Modifier le contenu**.

![Journey Optimizer](./images/sbp3a.png)

Cliquez sur **Concepteur d&#39;email**.

![Journey Optimizer](./images/sbp4.png)

Vous verrez alors ceci.

![Journey Optimizer](./images/sbp5.png)

Ouvrir **Composants de contenu** et faites glisser un **Texte** sous le contenu actuel de la newsletter.

![Journey Optimizer](./images/sbp6.png)

Sélectionnez l’intégralité du texte par défaut et supprimez-le. Cliquez ensuite sur le bouton **Ajouter une personnalisation** dans la barre d’outils.

![Journey Optimizer](./images/sbp7.png)

Vous verrez alors :

![Journey Optimizer](./images/seg1.png)

Dans le menu de gauche, cliquez sur **Adhésions aux segments**.

![Journey Optimizer](./images/seg2.png)

>[!NOTE]
>
>Si vous ne trouvez pas votre segment dans cette liste, faites défiler la liste vers le bas pour trouver des instructions sur la manière de récupérer manuellement l’identifiant du segment.

Sélection du segment `Luma - Women's Category Interest` et cliquez sur le bouton **+** qui doit ressembler à ceci :

![Journey Optimizer](./images/seg3.png)

Vous devez ensuite laisser la première ligne telle quelle et remplacer la ligne 2 et la ligne 3 par ce code :

``
Psssst... a private sale in the women category will launch soon, we will keep you posted
{%else%}
Thanks for taking the time to read our newsletter. Here is a 10% promo code to use on the website: READER10
{%/if%}
``

Vous obtiendrez alors ce qui suit :

![Journey Optimizer](./images/seg4.png)

Cliquez sur **Valider** pour vous assurer que le code est correct. Cliquez sur **Enregistrer**.

![Journey Optimizer](./images/sbp8.png)

Vous pouvez désormais enregistrer ce message en cliquant sur le bouton **Enregistrer** dans le coin supérieur droit. Cliquez ensuite sur **Simulation du contenu**.

![Journey Optimizer](./images/sbp9.png)

Sélectionnez l’un des profils que vous avez créés dans le cadre de ce tutoriel, puis cliquez sur **Aperçu**. Vous verrez alors le résultat de votre configuration.

![Journey Optimizer](./images/sbp10.png)

Vous verrez alors ceci. Cliquez ensuite sur **Fermer**.

![Journey Optimizer](./images/sbp10fff.png)

Revenez au tableau de bord du message en cliquant sur le bouton **flèche** en regard du texte de l’objet dans le coin supérieur gauche.

![Journey Optimizer](./images/sbp11.png)

Cliquez sur la flèche dans le coin supérieur gauche pour revenir à votre parcours.

![Journey Optimizer](./images/oc79afff.png)

Cliquez sur **Ok** pour fermer votre action de courrier électronique.

![Journey Optimizer](./images/oc79bfff.png)

Modifiez votre **Planification** to **Une fois** et définir une **Date/heure**. Cliquez sur **OK**.

>[!NOTE]
>
>La date et l’heure d’envoi du message doivent être comprises dans plus d’une heure.

![Journey Optimizer](./images/sbp18.png)

Cliquez sur le bouton **Publier** dans le parcours.

![Journey Optimizer](./images/sbp19.png)

Dans la fenêtre contextuelle, cliquez sur **Publier** encore une fois.

![Journey Optimizer](./images/sbp20.png)

Votre parcours de newsletter de base est maintenant publié. Votre message électronique de newsletter sera envoyé selon votre planning et votre parcours s’arrêtera dès que le dernier email aura été envoyé.

![Journey Optimizer](./images/sbp20fff.png)

Vous avez terminé cet exercice.

Étape suivante : [10.4 Configuration et utilisation des notifications push pour iOS](./ex4.md)

[Revenir au module 10](./journeyoptimizer.md)

[Revenir à tous les modules](../../overview.md)
