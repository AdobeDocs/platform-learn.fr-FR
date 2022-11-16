---
title: Bootcamp - Fusion physique et numérique - Journey Optimizer Créez votre parcours et votre notification push
description: Bootcamp - Fusion physique et numérique - Journey Optimizer Créez votre parcours et votre notification push
kt: 5342
audience: developer
doc-type: tutorial
activity: develop
exl-id: be8c23ec-c5f8-4abc-849f-994446072a84
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '834'
ht-degree: 4%

---

# 3.3 Création de votre parcours et de votre notification push

Dans cet exercice, vous allez configurer le parcours et le message qui doivent être déclenchés lorsqu’une personne entre dans une balise à l’aide de l’application mobile.

Connectez-vous à Adobe Journey Optimizer en accédant à [Adobe Experience Cloud](https://experience.adobe.com). Cliquez sur **Journey Optimizer**.

![ACOP](./images/acophome.png)

Vous serez redirigé vers le **Accueil**  dans Journey Optimizer. Tout d’abord, assurez-vous d’utiliser l’environnement de test approprié. L’environnement de test à utiliser est appelé `Bootcamp`. Pour passer d’un environnement de test à un autre, cliquez sur **Prod** et sélectionnez l’environnement de test dans la liste. Dans cet exemple, l’environnement de test est nommé **Bootcamp**. Vous serez alors dans le **Accueil** affichage de votre environnement de test `Bootcamp`.

![ACOP](./images/acoptriglp.png)

## 3.3.1 Création de votre parcours

Dans le menu de gauche, cliquez sur **Parcours**. Cliquez ensuite sur **Créer un Parcours** pour créer un parcours.

![ACOP](./images/createjourney.png)

Vous verrez alors un écran de parcours vide.

![ACOP](./images/journeyempty.png)

Dans l’exercice précédent, vous avez créé une **Événement**. Vous l’avez appelé comme suit : `yourLastNameBeaconEntryEvent` et remplacé `yourLastName` par votre nom de famille. Il s’agit du résultat de la création de l’événement :

![ACOP](./images/eventdone.png)

Vous devez maintenant considérer cet événement comme le début de ce Parcours. Pour ce faire, accédez au côté gauche de l’écran et recherchez votre événement dans la liste des événements.

![ACOP](./images/eventlist.png)

Sélectionnez votre événement, faites-le glisser et déposez-le sur le canevas de parcours. Votre parcours ressemble maintenant à ceci. Cliquez sur **Ok** pour enregistrer vos modifications.

![ACOP](./images/journeyevent.png)

Pour la deuxième étape du parcours, vous devez ajouter une **Push** action. Accédez au côté gauche de l’écran pour **Actions**, sélectionnez la variable **Push** puis faites-la glisser sur le deuxième noeud de votre parcours.

![ACOP](./images/journeyactions.png)

Sur le côté droit de l’écran, vous devez maintenant créer votre notification push.

Définissez la variable **Catégorie** to **Marketing** et sélectionnez une surface push qui permet d&#39;envoyer des notifications push. Dans ce cas, la surface push à sélectionner est **mmeeewis-app-mobile-bootcamp**.

![ACOP](./images/journeyactions1.png)

## 3.3.2 Création de votre message

Cliquez sur **Modifier le contenu**.

![ACOP](./images/emptymsg.png)

Vous verrez alors :

![ACOP](./images/emailmsglist.png)

Définissons le contenu de la notification push.

Cliquez sur le bouton **Titre** Champ de texte.

![Journey Optimizer](./images/msg5.png)

Dans la zone de texte, commencez à écrire. **Bonjour**. Cliquez sur l&#39;icône de personnalisation.

![Journey Optimizer](./images/msg6.png)

Vous devez maintenant importer le jeton de personnalisation pour le champ. **Prénom** qui est stocké sous `profile.person.name.firstName`. Dans le menu de gauche, sélectionnez **Attributs de profil**, faites défiler l’écran vers le bas/accédez au **Personne** et cliquez sur la flèche pour atteindre un niveau plus profond jusqu’au champ. `profile.person.name.firstName`. Cliquez sur le bouton **+** pour ajouter le champ à la zone de travail. Cliquez sur **Enregistrer**.

![Journey Optimizer](./images/msg7.png)

Vous serez alors de retour ici. Cliquez sur l’icône de personnalisation en regard du champ. **Corps**.

![Journey Optimizer](./images/msg11.png)

Dans la zone de texte, écrivez `Welcome at the `.

![Journey Optimizer](./images/msg12.png)

Cliquez ensuite sur **Attributs contextuels** puis **Journey Orchestration**.

![ACOP](./images/jomsg3.png)

Cliquez sur **Événements**.

![ACOP](./images/jomsg4.png)

Cliquez sur le nom de votre événement, qui doit se présenter comme suit : **yourLastNameBeaconEntryEvent**.

![ACOP](./images/jomsg5.png)

Cliquez sur **Contexte de l’emplacement**.

![ACOP](./images/jomsg6.png)

Cliquez sur **Interaction du point ciblé**.

![ACOP](./images/jomsg7.png)

Cliquez sur **Détails des points ciblés**.

![ACOP](./images/jomsg8.png)

Cliquez sur le bouton **+** icône **Nom du point ciblé**.
Vous verrez alors ceci. Cliquez sur **Enregistrer**.

![ACOP](./images/jomsg9.png)

Votre message est maintenant prêt. Cliquez sur la flèche dans le coin supérieur gauche pour revenir à votre parcours.

![ACOP](./images/jomsg11.png)

Cliquez sur **OK**.

![ACOP](./images/jomsg14.png)

## 3.3.2 Envoi d’un message à un écran

Pour la troisième étape du parcours, vous devez ajouter une **sendMessageToScreen** action. Accédez au côté gauche de l’écran pour **Actions**, sélectionnez la variable **sendMessageToScreen** puis faites-la glisser sur le troisième noeud de votre parcours. Vous verrez alors ceci.

![ACOP](./images/jomsg15.png)

Le **sendMessageToScreen** action est une action personnalisée qui publie un message sur le point de terminaison utilisé par l’affichage en magasin. Le **sendMessageToScreen** attend la définition de plusieurs variables. Vous pouvez afficher ces variables en faisant défiler la page vers le bas jusqu’à ce que vous voyiez **Paramètres d’action**.

![ACOP](./images/jomsg16.png)

Vous devez maintenant définir les valeurs de chaque paramètre d’action. Suivez ce tableau pour déterminer les valeurs requises.

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

{style=&quot;table-layout:auto&quot;}

Pour définir ces valeurs, cliquez sur le bouton **Modifier** icône .

![ACOP](./images/jomsg17.png)

Ensuite, sélectionnez **Mode avancé**.

![ACOP](./images/jomsg18.png)

Ensuite, collez la valeur en fonction du tableau ci-dessus. Cliquez sur **OK**.

![ACOP](./images/jomsg19.png)

Répétez cette procédure pour ajouter des valeurs pour chaque champ.

>[!IMPORTANT]
>
>Pour le champ ECID, il existe une référence à l’événement . `yourLastNameBeaconEntryEvent`. Veillez à remplacer `yourLastName` par votre nom de famille.

Le résultat final doit ressembler à ceci :

![ACOP](./images/jomsg20.png)

Faites défiler la page vers le haut et cliquez sur **Ok**.

![ACOP](./images/jomsg21.png)

Vous devez toujours donner un nom à votre parcours. Pour ce faire, cliquez sur le bouton **Propriétés** en haut à droite de l’écran.

![ACOP](./images/journeyname.png)

Vous pouvez ensuite y saisir le nom du parcours. Veuillez utiliser `yourLastName - Beacon Entry Journey`. Cliquez sur **OK** pour enregistrer vos modifications.

![ACOP](./images/journeyname1.png)

Vous pouvez maintenant publier votre parcours en cliquant sur **Publier**.

![ACOP](./images/publishjourney.png)

Cliquez sur **Publier** encore une fois.

![ACOP](./images/publish1.png)

Une barre de confirmation verte s’affiche alors, indiquant que votre parcours est désormais Publié.

![ACOP](./images/published.png)

Votre parcours est maintenant en ligne et peut être déclenché.

Vous avez maintenant terminé cet exercice.

Étape suivante : [3.4 Test de votre parcours](./ex4.md)

[Retour au flux utilisateur 3](./uc3.md)

[Revenir à tous les modules](../../overview.md)
