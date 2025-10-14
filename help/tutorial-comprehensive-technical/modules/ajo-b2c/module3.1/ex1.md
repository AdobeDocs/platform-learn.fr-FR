---
title: Journey Optimizer Création de votre événement
description: Journey Optimizer Création de votre événement
kt: 5342
doc-type: tutorial
exl-id: b132ad78-aaa3-458d-9895-0935f8ba88bb
source-git-commit: f843c50af04d744a7d769f320b5b55a5e6d25ffd
workflow-type: tm+mt
source-wordcount: '404'
ht-degree: 1%

---

# 3.1.1 Créer votre événement

Connectez-vous à Adobe Journey Optimizer en allant sur [Adobe Experience Cloud](https://experience.adobe.com?lang=fr). Cliquez sur **Journey Optimizer**.

![ACOP &#x200B;](./images/acophome.png)

Vous serez redirigé vers la vue **Accueil** dans Journey Optimizer. Tout d’abord, assurez-vous d’utiliser le bon sandbox. Le sandbox à utiliser est appelé `--aepSandboxName--`.

![ACOP &#x200B;](./images/acoptriglp.png)

Dans le menu de gauche, faites défiler l’écran vers le bas et cliquez sur **Configurations**. Cliquez ensuite sur le bouton **Gérer** sous **Événements**.

![ACOP &#x200B;](./images/acopmenu.png)

Vous verrez ensuite un aperçu de tous les événements disponibles. Cliquez sur **Créer un événement** pour commencer à créer votre propre événement.

![ACOP &#x200B;](./images/emptyevent.png)

Une nouvelle fenêtre d’événement vide s’affiche alors.

![ACOP &#x200B;](./images/emptyevent1.png)

Tout d&#39;abord, donnez à votre événement un nom comme celui-ci : `--aepUserLdap--AccountCreationEvent`.
Définissez la description sur `Account Creation Event`, assurez-vous que le **Type** est défini sur **Unitaire** et, pour la sélection **Type d’identifiant d’événement**, sélectionnez **Généré par le système**.

![ACOP &#x200B;](./images/eventdescription.png)

Vient ensuite la sélection du schéma . Veuillez utiliser le `Demo System - Event Schema for Website (Global v1.1) v.1` de schéma.

![ACOP &#x200B;](./images/eventschema.png)

Après avoir sélectionné le schéma, vous verrez un certain nombre de champs sélectionnés dans la section **Payload**. Vous devriez maintenant pointer sur la section **Payload** et vous verrez 3 icônes s’afficher dans la fenêtre contextuelle. Cliquez sur l’icône **Modifier**.

![ACOP &#x200B;](./images/eventpayload.png)

Une fenêtre contextuelle **Champs** s’affiche, dans laquelle vous devez sélectionner certains des champs dont nous avons besoin pour personnaliser l’e-mail.  Nous choisirons d’autres attributs de profil ultérieurement à l’aide des données déjà présentes dans Adobe Experience Platform.

![ACOP &#x200B;](./images/eventfields.png)

Dans le `--aepTenantId--.demoEnvironment` d’objet, veillez à sélectionner les champs **brandLogo** et **brandName**.

![ACOP &#x200B;](./images/eventpayloadbr.png)

Dans la `--aepTenantId--.identification.core` de l’objet, veillez à sélectionner le champ **e-mail**. Cliquez sur **Ok** pour enregistrer vos modifications.

![ACOP &#x200B;](./images/eventpayloadbrid.png)

Vous devriez alors voir ceci. Définissez **Espace de noms** sur **ECID (ECID)**. Cliquez sur **Enregistrer**.

![ACOP &#x200B;](./images/eventsave.png)

Votre événement est maintenant configuré et enregistré.

![ACOP &#x200B;](./images/eventdone.png)

Cliquez à nouveau sur votre événement pour ouvrir à nouveau l’écran **Modifier l’événement**. Pointez à nouveau sur le champ **Payload** pour afficher à nouveau les 3 icônes. Cliquez sur l’icône **Afficher la payload**.

![ACOP &#x200B;](./images/viewevent.png)

Un exemple de la payload attendue s’affiche maintenant.

![ACOP &#x200B;](./images/fullpayload.png)

Votre événement possède un eventID d’orchestration unique, que vous pouvez trouver en faisant défiler cette payload jusqu’à ce que vous voyiez `_experience.campaign.orchestration.eventID`.

L’identifiant d’événement est ce qui doit être envoyé à Adobe Experience Platform afin de déclencher le parcours que vous allez créer ensuite. Mémorisez cet eventID, car vous en aurez besoin dans l’un des exercices suivants.
`"eventID": "5ae9b8d3f68eb555502b0c07d03ef71780600c4bd0373a4065c692ae0bfbd34d"`

Cliquez sur **OK**.

![ACOP &#x200B;](./images/payloadeventID.png)

Cliquez sur **Annuler**.

![ACOP &#x200B;](./images/payloadeventID1.png)

Vous avez maintenant terminé cet exercice.

Étape suivante : [3.1.2 Créer des fragments à utiliser dans votre message](./ex2.md)

[Retour au module 3.1](./journey-orchestration-create-account.md)

[Revenir à tous les modules](../../../overview.md)
