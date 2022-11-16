---
title: Journey Optimizer Créer votre événement
description: Journey Optimizer Créer votre événement
kt: 5342
audience: developer
doc-type: tutorial
activity: develop
exl-id: e35d2357-21f9-4566-b2a1-cc0cf0c64956
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '449'
ht-degree: 0%

---

# 7.1 Création de votre événement

Connectez-vous à Adobe Journey Optimizer en accédant à [Adobe Experience Cloud](https://experience.adobe.com). Cliquez sur **Journey Optimizer**.

![ACOP](./images/acophome.png)

Vous serez redirigé vers le **Accueil**  dans Journey Optimizer. Tout d’abord, assurez-vous d’utiliser l’environnement de test approprié. L’environnement de test à utiliser est appelé `--aepSandboxId--`. Pour passer d’un environnement de test à un autre, cliquez sur **Production (VA7)** et sélectionnez l’environnement de test dans la liste. Dans cet exemple, l’environnement de test est nommé **Activation AEP FY22**. Vous serez alors dans le **Accueil** affichage de votre environnement de test `--aepSandboxId--`.

![ACOP](./images/acoptriglp.png)

Dans le menu de gauche, faites défiler l’écran vers le bas et cliquez sur **Configurations**. Cliquez ensuite sur le **Gérer** sous **Événements**.

![ACOP](./images/acopmenu.png)

Vous verrez ensuite un aperçu de tous les événements disponibles. Cliquez sur **Créer un événement** pour commencer à créer votre propre événement.

![ACOP](./images/emptyevent.png)

Une nouvelle fenêtre d’événement vide s’affiche alors.

![ACOP](./images/emptyevent1.png)

Tout d’abord, attribuez un nom à votre événement comme suit : `--demoProfileLdap--AccountCreationEvent`.

![ACOP](./images/eventname.png)

Ajoutez ensuite une description de ce type : `Account Creation Event`.

![ACOP](./images/eventdescription.png)

Ensuite, assurez-vous que la variable **Type** est défini sur **Unitaire**, et pour le **Type d’identifiant d’événement** sélection, sélectionnez **Généré par le système**.

![ACOP](./images/eventidtype.png)

La sélection de schéma suivante s’affiche. Un schéma a été préparé pour cet exercice. Veuillez utiliser le schéma `Demo System - Event Schema for Website (Global v1.1) v.1`.

![ACOP](./images/eventschema.png)

Après avoir sélectionné le schéma, plusieurs champs sont sélectionnés dans la variable **Payload** . Vous devez maintenant pointer sur le **Payload** et 3 icônes s’affichent. Cliquez sur le bouton **Modifier** icône .

![ACOP](./images/eventpayload.png)

Vous verrez une **Champs** fenêtre contextuelle dans laquelle vous devez sélectionner certains des champs dont nous avons besoin pour personnaliser l&#39;email.  Nous choisirons d’autres attributs de profil ultérieurement, en utilisant les données déjà présentes dans Adobe Experience Platform.

![ACOP](./images/eventfields.png)

Dans l’objet `--aepTenantId--.demoEnvironment`, veillez à sélectionner les champs **brandLogo** et **brandName**.

![ACOP](./images/eventpayloadbr.png)

Dans l’objet `--aepTenantId--.identification.core`, veillez à sélectionner le champ . **email**.

![ACOP](./images/eventpayloadbrid.png)

Cliquez sur **Ok** pour enregistrer vos modifications.

![ACOP](./images/saveok.png)

Vous devriez alors voir ceci :

![ACOP](./images/eventsave.png)

Cliquez sur **Enregistrer** une fois de plus pour enregistrer vos modifications.

![ACOP](./images/save1.png)

Votre événement est maintenant configuré et enregistré.

![ACOP](./images/eventdone.png)

Cliquez à nouveau sur l’événement pour ouvrir la **Modifier l’événement** à nouveau. Passez la souris sur le **Payload** pour afficher à nouveau les 3 icônes. Cliquez sur le bouton **Afficher la charge utile** icône .

![ACOP](./images/viewevent.png)

Vous verrez maintenant un exemple de la charge utile attendue.

![ACOP](./images/fullpayload.png)

Votre événement comporte un eventID d’orchestration unique, que vous pouvez trouver en faisant défiler la page vers le bas dans cette payload jusqu’à ce que vous voyiez `_experience.campaign.orchestration.eventID`.

![ACOP](./images/payloadeventID.png)

L’identifiant d’événement est ce qui doit être envoyé à Adobe Experience Platform pour déclencher le Parcours que vous allez créer dans l’exercice 7.2. Mémorisez cet eventID, car vous en aurez besoin dans l’exercice 7.3.
`"eventID": "227402c540eb8f8855c6b2333adf6d54d7153d9d7d56fa475a6866081c574736"`

Cliquez sur **Ok**, puis cliquez sur **Annuler**.

Vous avez maintenant terminé cet exercice.

Étape suivante : [7.2 Journey Optimizer : Créer votre parcours et votre email](./ex2.md)

[Revenir au module 7](./journey-orchestration-create-account.md)

[Revenir à tous les modules](../../overview.md)
