---
title: Configuration d’un parcours avec des messages push
description: Configuration d’un parcours avec des messages push
kt: 5342
doc-type: tutorial
exl-id: 63d7ee24-b6b5-4503-b104-a345c2b26960
source-git-commit: fb14ba45333bdd5834ff0c6c2dc48dda35cfe85f
workflow-type: tm+mt
source-wordcount: '770'
ht-degree: 3%

---

# 3.3.2 Configuration d’un parcours avec des messages push

Connectez-vous à Adobe Journey Optimizer en allant sur [Adobe Experience Cloud](https://experience.adobe.com?lang=fr). Cliquez sur **Journey Optimizer**.

![ACOP &#x200B;](./../../../../modules/delivery-activation/ajo-b2c/ajob2c-1/images/acophome.png)

Vous serez redirigé vers la vue **Accueil** dans Journey Optimizer. Tout d’abord, assurez-vous d’utiliser le bon sandbox. Le sandbox à utiliser est appelé `--aepSandboxName--`. Vous serez alors dans la vue **Accueil** de votre `--aepSandboxName--` sandbox.

![ACOP &#x200B;](./../../../../modules/delivery-activation/ajo-b2c/ajob2c-1/images/acoptriglp.png)

## 3.3.2.1 Créer un événement

Dans le menu de gauche, accédez à **Configurations**, puis cliquez sur **Gérer** sous **Événements**.

![ACOP &#x200B;](./images/acopmenu.png)

Sur l’écran **Événements**, une vue similaire à celle-ci s’affiche. Cliquez sur **Créer un événement**.

![ACOP &#x200B;](./images/add.png)

Une configuration d’événement vide s’affiche alors.
Tout d’abord, donnez à votre Événement un Nom comme celui-ci : `--aepUserLdap--StoreEntryEvent` et définissez la description sur `Store Entry Event`.
La sélection suivante est **Type d’événement**. Sélectionnez **Unitaire**.
La sélection suivante est **Type d’identifiant d’événement**. Sélectionnez **Système généré**.

![ACOP &#x200B;](./images/eventname.png)

Vient ensuite la sélection du schéma . Un schéma a été préparé pour cet exercice. Veuillez utiliser le `Demo System - Event Schema for Mobile App (Global v1.1) v.1` de schéma.

Après avoir sélectionné le schéma, vous verrez un certain nombre de champs sélectionnés dans la section **Payload**. Vérifiez que le champ **Espace de noms** est défini sur **ECID**. Votre événement est maintenant entièrement configuré.

Cliquez sur **Enregistrer**.

![ACOP &#x200B;](./images/eventschema.png)

Votre événement est maintenant configuré et enregistré. Cliquez à nouveau sur votre événement pour ouvrir à nouveau l’écran **Modifier l’événement**.

![ACOP &#x200B;](./images/eventdone.png)

Pointez sur le champ **Payload** et cliquez sur l’icône **Afficher la payload**.

![ACOP &#x200B;](./images/hover.png)

Un exemple de la payload attendue s’affiche maintenant.

Votre événement possède un eventID d’orchestration unique, que vous pouvez trouver en faisant défiler cette payload jusqu’à ce que vous voyiez `_experience.campaign.orchestration.eventID`.

L’identifiant d’événement est ce qui doit être envoyé à Adobe Experience Platform afin de déclencher le Parcours que vous allez créer à l’étape suivante. Notez cet eventID, car vous en aurez besoin à l’étape suivante.
`"eventID": "aa895251f76831e6440f169f1bb9d2a4388f0696d8e2782cfab192a275817dfa"`

Cliquez sur **OK**.

![ACOP &#x200B;](./images/payloadeventID.png)

Cliquez sur **Annuler**.

![ACOP &#x200B;](./images/payloadeventIDa.png)

## 3.3.2.2 Créer un parcours

Dans le menu de gauche, accédez à **Parcours** puis cliquez sur **Créer un Parcours**.

![DSN &#x200B;](./images/sjourney1.png)

Tu verras ça. Donnez un nom à votre parcours : `--aepUserLdap-- - Store Entry journey`. Cliquez sur **Enregistrer**.

![DSN &#x200B;](./images/sjourney3.png)

Tout d’abord, vous devez ajouter votre événement comme point de départ de votre parcours. Recherchez le `--aepUserLdap--StoreEntryEvent` de votre événement et glissez-déposez-le sur la zone de travail. Cliquez sur **Enregistrer**.

![DSN &#x200B;](./images/sjourney4.png)

Ensuite, sous **Actions**, recherchez l’action **Push**. Faites glisser et déposez l’action **Push** sur la zone de travail.

Définissez la **Catégorie** sur **Marketing** et sélectionnez une surface push qui vous permet d’envoyer des notifications push. Dans ce cas, la surface d’email à sélectionner est **Push-iOS-Android**.

>[!NOTE]
>
>Un canal dans Journey Optimizer utilisant la **surface d’application** comme vérifié précédemment doit exister.

![ACOP &#x200B;](./images/journeyactions1push.png)

L’étape suivante consiste à créer votre message. Pour ce faire, cliquez sur **Modifier le contenu**.

![ACOP &#x200B;](./images/journeyactions2push.png)

Tu verras ça. Cliquez sur l’icône **personnalisation** pour le champ **Titre**.

![Notification push](./images/bp5.png)

Tu verras ça. Vous pouvez désormais sélectionner directement n’importe quel attribut de profil du profil client en temps réel.

Recherchez le champ **Prénom**, puis cliquez sur l’icône **+** en regard du champ **Prénom**. Le jeton de personnalisation du prénom ajouté s’affiche alors : **{{profile.person.name.firstName}}**.

![Notification push](./images/bp9.png)

Ensuite, ajoutez le texte **, bienvenue dans notre boutique !** derrière **{{profile.person.name.firstName}}**.

Cliquez sur **Enregistrer**.

![Notification push](./images/bp10.png)

Vous l&#39;avez maintenant. Cliquez sur l’icône **personnalisation** du champ **Corps**.

![Notification push](./images/bp11.png)

Entrez ce texte **Cliquez ici pour obtenir une réduction de 10 % lorsque vous achetez aujourd&#39;hui !** et cliquez sur **Enregistrer**.

![Notification push](./images/bp12.png)

Tu auras alors ceci. Cliquez sur la flèche dans le coin supérieur gauche pour revenir au parcours.

![Journey Optimizer](./images/bp12a.png)

Cliquez sur **Enregistrer** pour fermer votre action push.

![DSN &#x200B;](./images/sjourney8.png)

Cliquez sur **Publier**.

![DSN &#x200B;](./images/sjourney10.png)

Cliquez de nouveau sur **Publier**.

![DSN &#x200B;](./images/sjourney10a.png)

Votre parcours est maintenant publié.

![DSN &#x200B;](./images/sjourney11.png)

## 3.3.2.3 Mettre à jour la propriété de collecte de données pour mobile

Dans **Prise en main**, le système de démonstration a ensuite créé pour vous des propriétés de balises : une pour le site web et une pour l’application mobile. Recherchez-les en `--aepUserLdap--` dans la zone **Rechercher**. Cliquez pour ouvrir la propriété **Mobile**.

![DSN &#x200B;](./images/pushpoi1.png)

Vous devriez alors voir ceci.

![DSN &#x200B;](./images/pushpoi2.png)

Dans le menu de gauche, accédez à **Règles** et cliquez pour ouvrir la règle **Entrée d’emplacement**.

![DSN &#x200B;](./images/pushpoi3.png)

Vous devriez alors voir ceci. Cliquez sur l’action **Mobile Core - Joindre des données**.

![DSN &#x200B;](./images/pushpoi4.png)

Vous devriez alors voir ceci.

![DSN &#x200B;](./images/pushpoi5.png)

Collez l’eventID de votre `--aepUserLdap--StoreEntryEvent` d’événement dans la fenêtre **Payload JSON**. Cliquez sur **Conserver les modifications**.

![DSN &#x200B;](./images/pushpoi6.png)

Cliquez sur **Enregistrer** ou **Enregistrer dans la bibliothèque**.

![DSN &#x200B;](./images/pushpoi7.png)

Accédez à **Flux de publication** et cliquez pour ouvrir la bibliothèque **Principal**.

![DSN &#x200B;](./images/pushpoi8.png)

Cliquez sur **Ajouter toutes les ressources modifiées** puis sur **Enregistrer et créer dans le développement**.

![DSN &#x200B;](./images/pushpoi9.png)

## 3.3.2.4 Tester votre parcours et votre message push

Ouvrez l&#39;application **DSN Mobile**.

![DSN &#x200B;](./images/dxdemo1.png)

Accédez à la page **Localisateur de magasin**.

![DSN &#x200B;](./images/dxdemo2.png)

Cliquez sur **Simuler une entrée de point d’intérêt**.

![DSN &#x200B;](./images/dxdemo3.png)

Au bout de quelques secondes, la notification push s’affiche.

![DSN &#x200B;](./images/dxdemo4.png)

## Étapes suivantes

Accédez à [3.3.3 Configuration d’une campagne avec des messages in-app](./ex3.md){target="_blank"}

Revenez à [Adobe Journey Optimizer : messages push et in-app](ajopushinapp.md){target="_blank"}

Revenir à [Tous les modules](./../../../../overview.md){target="_blank"}