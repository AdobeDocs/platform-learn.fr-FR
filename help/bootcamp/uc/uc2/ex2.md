---
title: Bootcamp - Journey Optimizer Créer votre événement
description: Bootcamp - Journey Optimizer Créer votre événement
jira: KT-5342
audience: developer
doc-type: tutorial
activity: develop
solution: Journey Optimizer
feature-set: Journey Optimizer
feature: Events
exl-id: 89db40ab-d4c5-4310-aca6-cb64828e7bc9
source-git-commit: 3c86f9b19cecf92c9a324fb6fcfcefaebf82177f
workflow-type: tm+mt
source-wordcount: '447'
ht-degree: 0%

---

# 2.2 Création de votre événement

Connectez-vous à Adobe Journey Optimizer en vous rendant à [Adobe Experience Cloud](https://experience.adobe.com?lang=fr). Cliquez sur **Journey Optimizer**.

![ACOP](./images/acophome.png)

Vous serez redirigé vers la vue **Home** dans Journey Optimizer. Tout d’abord, assurez-vous d’utiliser l’environnement de test approprié. L’environnement de test à utiliser s’appelle `Bootcamp`. Pour passer d’un environnement de test à un autre, cliquez sur **Prod** et sélectionnez l’environnement de test dans la liste. Dans cet exemple, l’environnement de test est appelé **Bootcamp**. Vous serez alors dans la vue **Home** de votre environnement de test `Bootcamp`.

![ACOP](./images/acoptriglp.png)

Dans le menu de gauche, faites défiler l’écran vers le bas et cliquez sur **Configurations**. Cliquez ensuite sur le bouton **Gérer** sous **Événements**.

![ACOP](./images/acopmenu.png)

Vous verrez ensuite un aperçu de tous les événements disponibles. Cliquez sur **Créer un événement** pour commencer à créer votre propre événement.

![ACOP](./images/emptyevent.png)

Une nouvelle fenêtre d’événement vide s’affiche alors.

![ACOP](./images/emptyevent1.png)

Tout d’abord, attribuez un nom à votre événement comme suit : `yourLastNameAccountCreationEvent` et ajoutez une description comme celle-ci `Account Creation Event`.

![ACOP](./images/eventdescription.png)

Ensuite, assurez-vous que le **Type** est défini sur **Unitary**, et pour la sélection **Event ID Type**, sélectionnez **System Generated**.

![ACOP](./images/eventidtype.png)

La sélection de schéma suivante s’affiche. Un schéma a été préparé pour cet exercice. Utilisez le schéma `Demo System - Event Schema for Website (Global v1.1) v.1`.

![ACOP](./images/eventschema.png)

Après avoir sélectionné le schéma, plusieurs champs sont sélectionnés dans la section **Champs** . Pointez maintenant sur la section **Champs** pour afficher la fenêtre contextuelle de 3 icônes. Cliquez sur l&#39;icône **Modifier** .

![ACOP](./images/eventpayload.png)

Une fenêtre contextuelle **Champs** s’affiche, dans laquelle vous devez sélectionner certains des champs dont nous avons besoin pour personnaliser l’email.  Nous choisirons d’autres attributs de profil ultérieurement, en utilisant les données déjà présentes dans Adobe Experience Platform.

![ACOP](./images/eventfields.png)

Dans l&#39;objet `_experienceplatform.demoEnvironment`, veillez à sélectionner les champs **brandLogo** et **brandName**.

![ACOP](./images/eventpayloadbr.png)

Dans l&#39;objet `_experienceplatform.identification.core`, veillez à sélectionner le champ **email**.

![ACOP](./images/eventpayloadbrid.png)

Cliquez sur **Ok** pour enregistrer vos modifications.

![ACOP](./images/saveok.png)

Vous devriez alors voir ceci. Cliquez une fois de plus sur **Enregistrer** pour enregistrer vos modifications.

![ACOP](./images/eventsave.png)

Votre événement est maintenant configuré et enregistré.

![ACOP](./images/eventdone.png)

Cliquez à nouveau sur votre événement pour ouvrir à nouveau l’écran **Modifier l’événement** . Passez de nouveau la souris sur **Fields** pour afficher à nouveau les 3 icônes. Cliquez sur l’icône **Afficher la charge utile** .

![ACOP](./images/viewevent.png)

Vous verrez maintenant un exemple de la charge utile attendue.
Votre événement a un eventID d’orchestration unique, que vous pouvez trouver en faisant défiler la page vers le bas dans cette payload jusqu’à ce que vous voyiez `_experience.campaign.orchestration.eventID`.

![ACOP](./images/payloadeventID.png)

L’identifiant d’événement est ce qui doit être envoyé à Adobe Experience Platform pour déclencher le parcours que vous allez créer dans l’un des exercices suivants. Mémorisez cet eventID, car vous en aurez peut-être besoin plus tard.
`"eventID": "19cab7852cdef99d25b6d5f1b6503da39d1f486b1d585743f97ed2d1e6b6c74f"`

Cliquez sur **Ok**, puis sur **Annuler**.

Vous avez maintenant terminé cet exercice.

Étape suivante : [2.3 Création de votre message électronique](./ex3.md)

[Retour au flux utilisateur 2](./uc2.md)

[Revenir à tous les modules](../../overview.md)
