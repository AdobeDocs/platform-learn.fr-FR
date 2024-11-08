---
title: Journey Optimizer Créer votre événement
description: Journey Optimizer Créer votre événement
kt: 5342
doc-type: tutorial
source-git-commit: 6962a0d37d375e751a05ae99b4f433b0283835d0
workflow-type: tm+mt
source-wordcount: '457'
ht-degree: 0%

---

# 3.1.1 Création de votre événement

Connectez-vous à Adobe Journey Optimizer en vous rendant à [Adobe Experience Cloud](https://experience.adobe.com?lang=fr). Cliquez sur **Journey Optimizer**.

![ACOP](./images/acophome.png)

Vous serez redirigé vers la vue **Home** dans Journey Optimizer. Tout d’abord, assurez-vous d’utiliser l’environnement de test approprié. L’environnement de test à utiliser s’appelle `--aepSandboxName--`. Pour passer d’un environnement de test à un autre, cliquez sur **Production Prod (VA7)** et sélectionnez l’environnement de test dans la liste. Dans cet exemple, l’environnement de test est nommé **AEP Enablement FY22**. Vous serez alors dans la vue **Home** de votre environnement de test `--aepSandboxName--`.

![ACOP](./images/acoptriglp.png)

Dans le menu de gauche, faites défiler l’écran vers le bas et cliquez sur **Configurations**. Cliquez ensuite sur le bouton **Gérer** sous **Événements**.

![ACOP](./images/acopmenu.png)

Vous verrez ensuite un aperçu de tous les événements disponibles. Cliquez sur **Créer un événement** pour commencer à créer votre propre événement.

![ACOP](./images/emptyevent.png)

Une nouvelle fenêtre d’événement vide s’affiche alors.

![ACOP](./images/emptyevent1.png)

Tout d’abord, attribuez un nom à votre événement comme ceci : `--aepUserLdap--AccountCreationEvent`.

![ACOP](./images/eventname.png)

Ajoutez ensuite une description de ce type `Account Creation Event`.

![ACOP](./images/eventdescription.png)

Ensuite, assurez-vous que le **Type** est défini sur **Unitary**, et pour la sélection **Event ID Type**, sélectionnez **System Generated**.

![ACOP](./images/eventidtype.png)

La sélection de schéma suivante s’affiche. Un schéma a été préparé pour cet exercice. Utilisez le schéma `Demo System - Event Schema for Website (Global v1.1) v.1`.

![ACOP](./images/eventschema.png)

Après avoir sélectionné le schéma, plusieurs champs sont sélectionnés dans la section **Payload**. Pointez maintenant sur la section **Payload** pour afficher 3 icônes. Cliquez sur l&#39;icône **Modifier** .

![ACOP](./images/eventpayload.png)

Une fenêtre contextuelle **Champs** s’affiche, dans laquelle vous devez sélectionner certains des champs dont nous avons besoin pour personnaliser l’email.  Nous choisirons d’autres attributs de profil ultérieurement, en utilisant les données déjà présentes dans Adobe Experience Platform.

![ACOP](./images/eventfields.png)

Dans l&#39;objet `--aepTenantId--.demoEnvironment`, veillez à sélectionner les champs **brandLogo** et **brandName**.

![ACOP](./images/eventpayloadbr.png)

Dans l&#39;objet `--aepTenantId--.identification.core`, veillez à sélectionner le champ **email**.

![ACOP](./images/eventpayloadbrid.png)

Cliquez sur **Ok** pour enregistrer vos modifications.

![ACOP](./images/saveok.png)

Vous devriez alors voir ceci :

![ACOP](./images/eventsave.png)

Cliquez une fois de plus sur **Enregistrer** pour enregistrer vos modifications.

![ACOP](./images/save1.png)

Votre événement est maintenant configuré et enregistré.

![ACOP](./images/eventdone.png)

Cliquez à nouveau sur votre événement pour ouvrir à nouveau l’écran **Modifier l’événement** . Passez la souris sur le champ **Payload** pour afficher à nouveau les 3 icônes. Cliquez sur l’icône **Afficher la charge utile** .

![ACOP](./images/viewevent.png)

Vous verrez maintenant un exemple de la charge utile attendue.

![ACOP](./images/fullpayload.png)

Votre événement comporte un eventID d’orchestration unique, que vous pouvez trouver en faisant défiler la page vers le bas dans cette payload jusqu’à ce que vous voyiez `_experience.campaign.orchestration.eventID`.

![ACOP](./images/payloadeventID.png)

L’identifiant d’événement est ce qui doit être envoyé à Adobe Experience Platform pour déclencher le Parcours que vous allez créer dans l’exercice 7.2. Souvenez-vous de cet eventID, car vous en aurez besoin dans l’exercice 7.3.
`"eventID": "227402c540eb8f8855c6b2333adf6d54d7153d9d7d56fa475a6866081c574736"`

Cliquez sur **Ok**, puis sur **Annuler**.

Vous avez maintenant terminé cet exercice.

Étape suivante : [3.1.2 Journey Optimizer : créer votre parcours et votre message électronique](./ex2.md)

[Revenir au module 3.1](./journey-orchestration-create-account.md)

[Revenir à tous les modules](../../../overview.md)
