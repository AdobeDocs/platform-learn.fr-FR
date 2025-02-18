---
title: Journey Optimizer Création de votre événement
description: Journey Optimizer Création de votre événement
kt: 5342
doc-type: tutorial
exl-id: 2c03cc8d-0106-4fa5-80c6-e25712ca2eab
source-git-commit: 3d61d91111d8693ab031fbd7b26706c02818108c
workflow-type: tm+mt
source-wordcount: '408'
ht-degree: 1%

---

# 3.1.1 Créer votre événement

Connectez-vous à Adobe Journey Optimizer en allant sur [Adobe Experience Cloud](https://experience.adobe.com?lang=fr). Cliquez sur **Journey Optimizer**.

![ACOP ](./images/acophome.png)

Vous serez redirigé vers la vue **Accueil** dans Journey Optimizer. Tout d’abord, assurez-vous d’utiliser le bon sandbox. Le sandbox à utiliser est appelé `--aepSandboxName--`.

![ACOP ](./images/acoptriglp.png)

Dans le menu de gauche, faites défiler l’écran vers le bas et cliquez sur **Configurations**. Cliquez ensuite sur le bouton **Gérer** sous **Événements**.

![ACOP ](./images/acopmenu.png)

Vous verrez ensuite un aperçu de tous les événements disponibles. Cliquez sur **Créer un événement** pour commencer à créer votre propre événement.

![ACOP ](./images/emptyevent.png)

Une nouvelle fenêtre d’événement vide s’affiche alors.

![ACOP ](./images/emptyevent1.png)

Tout d&#39;abord, donnez à votre événement un nom comme celui-ci : `--aepUserLdap--AccountCreationEvent`.
Définissez la description sur `Account Creation Event`, assurez-vous que le **Type** est défini sur **Unitaire** et, pour la sélection **Type d’identifiant d’événement**, sélectionnez **Généré par le système**.

![ACOP ](./images/eventdescription.png)

Vient ensuite la sélection du schéma . Veuillez utiliser le `Demo System - Event Schema for Website (Global v1.1) v.1` de schéma.

![ACOP ](./images/eventschema.png)

Après avoir sélectionné le schéma, vous verrez un certain nombre de champs sélectionnés dans la section **Payload**. Vous devriez maintenant pointer sur la section **Payload** et vous verrez 3 icônes s’afficher dans la fenêtre contextuelle. Cliquez sur l’icône **Modifier**.

![ACOP ](./images/eventpayload.png)

Une fenêtre contextuelle **Champs** s’affiche, dans laquelle vous devez sélectionner certains des champs dont nous avons besoin pour personnaliser l’e-mail.  Nous choisirons d’autres attributs de profil ultérieurement à l’aide des données déjà présentes dans Adobe Experience Platform.

![ACOP ](./images/eventfields.png)

Dans le `--aepTenantId--.demoEnvironment` d’objet, veillez à sélectionner les champs **brandLogo** et **brandName**.

![ACOP ](./images/eventpayloadbr.png)

Dans la `--aepTenantId--.identification.core` de l’objet, veillez à sélectionner le champ **e-mail**. Cliquez sur **Ok** pour enregistrer vos modifications.

![ACOP ](./images/eventpayloadbrid.png)

Vous devriez alors voir ceci. Définissez **Espace de noms** sur **ECID (ECID)**. Cliquez sur **Enregistrer**.

![ACOP ](./images/eventsave.png)

Votre événement est maintenant configuré et enregistré.

![ACOP ](./images/eventdone.png)

Cliquez à nouveau sur votre événement pour ouvrir à nouveau l’écran **Modifier l’événement**. Pointez à nouveau sur le champ **Payload** pour afficher à nouveau les 3 icônes. Cliquez sur l’icône **Afficher la payload**.

![ACOP ](./images/viewevent.png)

Un exemple de la payload attendue s’affiche maintenant.

![ACOP ](./images/fullpayload.png)

Votre événement possède un eventID d’orchestration unique, que vous pouvez trouver en faisant défiler cette payload jusqu’à ce que vous voyiez `_experience.campaign.orchestration.eventID`.

L’identifiant d’événement est ce qui doit être envoyé à Adobe Experience Platform afin de déclencher le parcours que vous allez créer ensuite. Mémorisez cet eventID, car vous en aurez besoin dans l’un des exercices suivants.
`"eventID": "5ae9b8d3f68eb555502b0c07d03ef71780600c4bd0373a4065c692ae0bfbd34d"`

Cliquez sur **OK**.

![ACOP ](./images/payloadeventID.png)

Cliquez sur **Annuler**.

![ACOP ](./images/payloadeventID1.png)

Vous avez maintenant terminé cet exercice.

## Étapes suivantes

Accédez à [3.1.2 Créer des fragments à utiliser dans votre message](./ex2.md){target="_blank"}

Revenez à [Adobe Journey Optimizer : Orchestration](./journey-orchestration-create-account.md){target="_blank"}

Revenir à [Tous les modules](./../../../../overview.md){target="_blank"}
