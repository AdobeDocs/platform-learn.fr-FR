---
title: Adobe Journey Optimizer - Configuration d’un parcours basé sur les lots
description: Dans cette section, vous allez configurer un parcours de messagerie par lots pour envoyer une newsletter.
kt: 5342
doc-type: tutorial
source-git-commit: 6962a0d37d375e751a05ae99b4f433b0283835d0
workflow-type: tm+mt
source-wordcount: '794'
ht-degree: 8%

---

# 3.4.2 Configuration d’un parcours de newsletter par lots

Connectez-vous à Adobe Journey Optimizer en vous rendant à [Adobe Experience Cloud](https://experience.adobe.com?lang=fr). Cliquez sur **Journey Optimizer**.

![ACOP](./../../../modules/ajo-b2c/module3.2/images/acophome.png)

Vous serez redirigé vers la vue **Home** dans Journey Optimizer. Tout d’abord, assurez-vous d’utiliser l’environnement de test approprié. L’environnement de test à utiliser s’appelle `--aepSandboxName--`. Pour passer d’un environnement de test à un autre, cliquez sur **Production Prod (VA7)** et sélectionnez l’environnement de test dans la liste. Dans cet exemple, l’environnement de test est nommé **AEP Enablement FY22**. Vous serez alors dans la vue **Home** de votre environnement de test `--aepSandboxName--`.

![ACOP](./../../../modules/ajo-b2c/module3.2/images/acoptriglp.png)

## 3.4.2.1 Création d’un parcours de newsletter

Vous allez maintenant créer un parcours basé sur les lots. Contrairement à l’parcours basé sur les événements de l’exercice précédent qui repose sur les événements d’expérience entrants, les entrées de segment ou les sorties pour déclencher un parcours pour 1 client spécifique, les parcours basés sur des lots ciblent un segment entier une fois avec un contenu unique comme les newsletters, les promotions ponctuelles ou les informations génériques ou avec des contenus similaires envoyés régulièrement, comme par exemple des campagnes d’anniversaire et des rappels.

Dans le menu, accédez à **Parcours** et cliquez sur **Créer un Parcours**.

![Journey Optimizer](./images/oc43.png)

Sur le côté droit se trouve un formulaire dans lequel vous devez spécifier le nom et la description du parcours. Saisissez les valeurs suivantes :

- **Nom** : `--aepUserLdap-- - Newsletter Journey`. Par exemple : **vangeluw - Newsletter Parcours**.
- **Description** : Newsletter mensuelle

Cliquez sur **OK**.

![Journey Optimizer](./images/batchj2.png)

Sous **Orchestration**, placez **Lecture de segment** sur la zone de travail. Cela signifie qu’une fois publié, le parcours commence par récupérer l’audience de segment entière, qui devient ensuite l’audience cible du parcours et du message. Cliquez sur **Sélectionner un segment**.

![Journey Optimizer](./images/batchj3.png)

Dans la fenêtre contextuelle **Choisir un segment**, recherchez votre LDAP et sélectionnez le segment que vous avez créé dans [Module 2.3 - CDP en temps réel - Créer un segment et entreprendre l’action ](./../../../modules/rtcdp-b2c/module2.3/real-time-cdp-build-a-segment-take-action.md) nommée `--aepUserLdap-- - Interest in PROTEUS FITNESS JACKSHIRT`. par exemple : vangeluw - Intérêt pour PROTEUS FITNESS JACKSHIRT. Cliquez sur **Enregistrer**.

![Journey Optimizer](./images/batchj5.png)

Cliquez sur **OK**.

![Journey Optimizer](./images/batchj6.png)

Dans le menu de gauche, recherchez la section **Actions** et faites glisser une action **Email** sur la zone de travail.

![Journey Optimizer](./images/batchj7.png)

Définissez la **catégorie** sur **Marketing** et sélectionnez une surface d&#39;email qui vous permet d&#39;envoyer des emails. Dans ce cas, la surface de l&#39;email à sélectionner est **Email**. Assurez-vous que les cases à cocher des **clics sur l’email** et des **ouvertures d’email** sont toutes deux activées.

![ACOP](./images/journeyactions1eee.png)

L’étape suivante consiste à créer votre message. Pour ce faire, cliquez sur **Modifier le contenu**.

![ACOP](./images/journeyactions2.png)

Vous voyez maintenant ceci. Cliquez sur le champ de texte **Objet** .

![Journey Optimizer](./images/batch4.png)

Saisissez ce texte pour l’objet : `Luma Newsletter - your monthly update has arrived.`. Cliquez sur **Enregistrer**.

![Journey Optimizer](./images/batch5.png)

Vous serez alors de retour ici. Cliquez sur **Designer email** pour commencer à créer le contenu de l&#39;email.

![Journey Optimizer](./images/batch6.png)

Vous verrez alors ceci. Cliquez sur **Importer l’HTML**.

![Journey Optimizer](./images/batch7.png)

Dans l’écran contextuel, vous devez faire glisser et déposer le fichier d’HTML de l’email. Vous trouverez le modèle d’HTML [ici](./../../../assets/html/ajo-newsletter.html.zip). Téléchargez le fichier zip avec le modèle d’HTML sur votre ordinateur local et décompressez-le sur votre bureau.

![Journey Optimizer](./images/html1.png)

Faites glisser et déposez le fichier **ajo-newsletter.html** pour le charger dans Journey Optimizer. Cliquez sur **Importer**.

![Journey Optimizer](./images/batch8.png)

Ce contenu d’email est prêt à l’emploi, car il contient toute la personnalisation, l’imagerie et le texte attendus. Seul l’espace réservé de l’offre est laissé vide.

Un message d’erreur peut s’afficher : **Erreur lors de la récupération des ressources**. Il est lié à l’image dans l’email.

![Journey Optimizer](./images/errorfetch.png)

Si vous obtenez cette erreur, sélectionnez l’image et cliquez sur le bouton **Modifier l’image** .

![Journey Optimizer](./images/errorfetch1.png)

Cliquez sur **Assets Essentials** pour revenir à votre bibliothèque AEM Assets Essentials.

![Journey Optimizer](./images/errorfetch2.png)

Vous verrez alors cette fenêtre contextuelle. Accédez au dossier **enablement-assets** et sélectionnez l’image **luma-newsletterContent.png**. Cliquez sur **Sélectionner**.

![Journey Optimizer](./images/errorfetch3.png)

Votre message électronique de newsletter de base est maintenant prêt. Cliquez sur **Enregistrer**.

![Journey Optimizer](./images/ready.png)

Revenez au tableau de bord des messages en cliquant sur la **flèche** en regard de l’objet du texte dans le coin supérieur gauche.

![Journey Optimizer](./images/batch9.png)

Cliquez sur la flèche dans le coin supérieur gauche pour revenir à votre parcours.

![Journey Optimizer](./images/oc79aeee.png)

Cliquez sur **Ok** pour fermer votre action de courrier électronique.

![Journey Optimizer](./images/oc79beee.png)

Votre parcours de newsletter est maintenant prêt à être publié. Avant de procéder, remarquez la section **Planning** où vous pouvez passer de ce parcours unique à une campagne récurrente. Cliquez sur le bouton **Schedule** .

![Journey Optimizer](./images/batchj12.png)

Vous verrez alors ceci. Sélectionnez **Once**.

![Journey Optimizer](./images/sch1.png)

Sélectionnez une date et une heure dans l’heure suivante afin de pouvoir tester votre parcours. Cliquez sur **OK**.

>[!NOTE]
>
>La date et l’heure d’envoi du message doivent être comprises dans plus d’une heure.

Cliquez sur **Publier**.

![Journey Optimizer](./images/batchj13.png)

Cliquez de nouveau sur **Publish**.

![Journey Optimizer](./images/batchj14.png)

Votre parcours de newsletter de base est maintenant publié. Votre message électronique de newsletter sera envoyé tel que vous l’avez défini dans votre planning, et votre parcours s’arrêtera dès que le dernier email aura été envoyé.

![Journey Optimizer](./images/batchj14eee.png)

Vous avez terminé cet exercice.

Étape suivante : [3.4.3 Appliquer la personnalisation dans un message électronique](./ex3.md)

[Revenir au module 3.4](./journeyoptimizer.md)

[Revenir à tous les modules](../../../overview.md)
