---
title: Bootcamp - Fusion physique et numérique - Journey Optimizer Créez votre parcours et votre notification push
description: Bootcamp - Fusion physique et numérique - Journey Optimizer Créez votre parcours et votre notification push
jira: KT-5342
audience: developer
doc-type: tutorial
activity: develop
solution: Journey Optimizer
feature-set: Journey Optimizer
feature: Events
exl-id: be8c23ec-c5f8-4abc-849f-994446072a84
source-git-commit: cd59a41f4533f18a54d80298ee9faf3a8ba3c6e7
workflow-type: tm+mt
source-wordcount: '839'
ht-degree: 4%

---

# 3.3 Création de votre parcours et de votre notification push

Dans cet exercice, vous allez configurer le parcours et le message qui doivent être déclenchés lorsqu’une personne entre dans une balise à l’aide de l’application mobile.

Connectez-vous à Adobe Journey Optimizer en vous rendant à [Adobe Experience Cloud](https://experience.adobe.com?lang=fr). Cliquez sur **Journey Optimizer**.

![ACOP](./images/acophome.png)

Vous serez redirigé vers la vue **Home** dans Journey Optimizer. Tout d’abord, assurez-vous d’utiliser l’environnement de test approprié. L’environnement de test à utiliser s’appelle `Bootcamp`. Pour passer d’un environnement de test à un autre, cliquez sur **Prod** et sélectionnez l’environnement de test dans la liste. Dans cet exemple, l’environnement de test est appelé **Bootcamp**. Vous serez alors dans la vue **Home** de votre environnement de test `Bootcamp`.

![ACOP](./images/acoptriglp.png)

## 3.3.1 Création de votre parcours

Dans le menu de gauche, cliquez sur **Parcours**. Cliquez ensuite sur **Créer un Parcours** pour créer un parcours.

![ACOP](./images/createjourney.png)

Vous verrez alors un écran de parcours vide.

![ACOP](./images/journeyempty.png)

Dans l’exercice précédent, vous avez créé un **événement**. Vous l&#39;avez appelé comme suit `yourLastNameBeaconEntryEvent` et remplacé `yourLastName` par votre nom de famille. Il s’agit du résultat de la création de l’événement :

![ACOP](./images/eventdone.png)

Vous devez maintenant considérer cet événement comme le début de ce Parcours. Pour ce faire, accédez au côté gauche de l’écran et recherchez votre événement dans la liste des événements.

![ACOP](./images/eventlist.png)

Sélectionnez votre événement, faites-le glisser et déposez-le sur le canevas de parcours. Votre parcours ressemble maintenant à ceci. Cliquez sur **Ok** pour enregistrer vos modifications.

![ACOP](./images/journeyevent.png)

Pour la deuxième étape du parcours, vous devez ajouter une action **Push**. Accédez au côté gauche de votre écran à **Actions**, sélectionnez l’action **Push**, puis faites-la glisser sur le deuxième noeud de votre parcours.

![ACOP](./images/journeyactions.png)

Sur le côté droit de l’écran, vous devez maintenant créer votre notification push.

Définissez la **catégorie** sur **Marketing** et sélectionnez une surface push qui vous permet d’envoyer des notifications push. Dans ce cas, la surface push à sélectionner est **mmeeewis-app-mobile-bootcamp**.

![ACOP](./images/journeyactions1.png)

## 3.3.2 Création de votre message

Cliquez sur **Modifier le contenu**.

![ACOP](./images/emptymsg.png)

Vous verrez alors :

![ACOP](./images/emailmsglist.png)

Définissons le contenu de la notification push.

Cliquez sur le champ de texte **Titre** .

![Journey Optimizer](./images/msg5.png)

Dans la zone de texte, commencez à écrire **Hi**. Cliquez sur l&#39;icône de personnalisation.

![Journey Optimizer](./images/msg6.png)

Vous devez maintenant importer le jeton de personnalisation pour le champ **Prénom** qui est stocké sous `profile.person.name.firstName`. Dans le menu de gauche, sélectionnez **Attributs de profil**, faites défiler l’écran vers le bas/accédez à l’élément **Personne** et cliquez sur la flèche pour aller plus loin jusqu’à atteindre le champ `profile.person.name.firstName`. Cliquez sur l’icône **+** pour ajouter le champ à la zone de travail. Cliquez sur **Enregistrer**.

![Journey Optimizer](./images/msg7.png)

Vous serez alors de retour ici. Cliquez sur l’icône de personnalisation en regard du champ **Body**.

![Journey Optimizer](./images/msg11.png)

Dans la zone de texte, écrivez `Welcome at the `.

![Journey Optimizer](./images/msg12.png)

Cliquez ensuite sur **Attributs contextuels**, puis sur **Journey Orchestration**.

![ACOP](./images/jomsg3.png)

Cliquez sur **Events**.

![ACOP](./images/jomsg4.png)

Cliquez sur le nom de votre événement, qui doit ressembler à ceci : **yourLastNameBeaconEntryEvent**.

![ACOP](./images/jomsg5.png)

Cliquez sur **Placer le contexte**.

![ACOP](./images/jomsg6.png)

Cliquez sur **Interaction POI**.

![ACOP](./images/jomsg7.png)

Cliquez sur **Détails du point ciblé**.

![ACOP](./images/jomsg8.png)

Cliquez sur l’icône **+** sur **Nom du point ciblé**.
Vous verrez alors ceci. Cliquez sur **Enregistrer**.

![ACOP](./images/jomsg9.png)

Votre message est maintenant prêt. Cliquez sur la flèche dans le coin supérieur gauche pour revenir à votre parcours.

![ACOP](./images/jomsg11.png)

Cliquez sur **OK**.

![ACOP](./images/jomsg14.png)

## 3.3.2 Envoi d’un message à un écran

Comme troisième étape du parcours, vous devez ajouter une action **sendMessageToScreen**. Accédez au côté gauche de votre écran à **Actions**, sélectionnez l’action **sendMessageToScreen**, puis faites-la glisser sur le troisième noeud de votre parcours. Vous verrez alors ceci.

![ACOP](./images/jomsg15.png)

L’action **sendMessageToScreen** est une action personnalisée qui publiera un message sur le point de terminaison utilisé par l’affichage en magasin. L’action **sendMessageToScreen** exige la définition de plusieurs variables. Vous pouvez voir ces variables en faisant défiler l’écran jusqu’à ce que **Paramètres d’action** s’affiche.

![ACOP](./images/jomsg16.png)

Vous devez maintenant définir les valeurs de chaque paramètre d’action. Suivez ce tableau pour déterminer les valeurs requises à quel emplacement.

| Paramètre | valeur |
|:-------------:| :---------------:|
| DIFFUSION | `'image'` |
| ECID | `@{yourLastNameBeaconEntryEvent._experienceplatform.identification.core.ecid}` |
| PREMIER NOM | `#{ExperiencePlatform.ProfileFieldGroup.profile.person.name.firstName}` |
| EVENTSUBJECT | `#{ExperiencePlatform.ProductListItems.experienceevent.first(currentDataPackField.eventType == "commerce.productViews").productListItems.first().name}` |
| EVENTSUBJECTURL | `#{ExperiencePlatform.ProductListItems.experienceevent.first(currentDataPackField.eventType == "commerce.productViews").productListItems.first()._experienceplatform.core.imageURL}` |
| ENVIRONNEMENT DE TEST | `'bootcamp'` |
| CONTAINERID | `''` |
| ACTIVITYID | `''` |
| PLACEMENTID | `''` |

{style="table-layout:auto"}

Pour définir ces valeurs, cliquez sur l&#39;icône **Modifier** .

![ACOP](./images/jomsg17.png)

Sélectionnez ensuite **Mode avancé**.

![ACOP](./images/jomsg18.png)

Ensuite, collez la valeur en fonction du tableau ci-dessus. Cliquez sur **OK**.

![ACOP](./images/jomsg19.png)

Répétez cette procédure pour ajouter des valeurs pour chaque champ.

>[!IMPORTANT]
>
>Pour le champ ECID, il existe une référence à l’événement `yourLastNameBeaconEntryEvent`. Veillez à remplacer `yourLastName` par votre nom de famille.

Le résultat final doit ressembler à ceci :

![ACOP](./images/jomsg20.png)

Faites défiler la page vers le haut et cliquez sur **Ok**.

![ACOP](./images/jomsg21.png)

Vous devez toujours donner un nom à votre parcours. Pour ce faire, cliquez sur l’icône **Crayon** dans le coin supérieur gauche de votre écran.

![ACOP](./images/journeyname.png)

Vous pouvez ensuite y saisir le nom du parcours. Veuillez utiliser `yourLastName - Beacon Entry Journey`. Cliquez sur **OK** pour enregistrer vos modifications.

![ACOP](./images/journeyname1.png)

Vous pouvez maintenant publier votre parcours en cliquant sur **Publish**.

![ACOP](./images/publishjourney.png)

Cliquez de nouveau sur **Publish**.

![ACOP](./images/publish1.png)

Une barre de confirmation verte s’affiche alors, indiquant que votre parcours est désormais Publié.

![ACOP](./images/published.png)

Votre parcours est maintenant en ligne et peut être déclenché.

Vous avez maintenant terminé cet exercice.

Étape suivante : [3.4 Test de votre parcours](./ex4.md)

[Retour au flux utilisateur 3](./uc3.md)

[Revenir à tous les modules](../../overview.md)
