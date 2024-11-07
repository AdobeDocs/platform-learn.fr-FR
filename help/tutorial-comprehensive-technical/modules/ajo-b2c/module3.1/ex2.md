---
title: Journey Optimizer Créer votre parcours et votre message électronique
description: Journey Optimizer Créer votre email
kt: 5342
doc-type: tutorial
source-git-commit: 2cdc145d7f3933ec593db4e6f67b60961a674405
workflow-type: tm+mt
source-wordcount: '1413'
ht-degree: 6%

---

# 3.1.2 Création de votre parcours et de votre message électronique

Dans cet exercice, vous allez configurer le parcours et le message qui doivent être déclenchés lorsqu’une personne crée un compte sur le site web de démonstration.

Connectez-vous à Adobe Journey Optimizer en vous rendant à [Adobe Experience Cloud](https://experience.adobe.com?lang=fr). Cliquez sur **Journey Optimizer**.

![ACOP](./images/acophome.png)

Vous serez redirigé vers la vue **Home** dans Journey Optimizer. Tout d’abord, assurez-vous d’utiliser l’environnement de test approprié. L’environnement de test à utiliser s’appelle `--aepSandboxId--`. Pour passer d’un environnement de test à un autre, cliquez sur **Production Prod (VA7)** et sélectionnez l’environnement de test dans la liste. Dans cet exemple, l’environnement de test est nommé **AEP Enablement FY22**. Vous serez alors dans la vue **Home** de votre environnement de test `--aepSandboxId--`.

![ACOP](./images/acoptriglp.png)

## 3.1.2.1 Création de votre parcours

Dans le menu de gauche, cliquez sur **Parcours**. Cliquez ensuite sur **Créer un Parcours** pour créer un parcours.

![ACOP](./images/createjourney.png)

Vous verrez alors un écran de parcours vide.

![ACOP](./images/journeyempty.png)

Dans l’exercice précédent, vous avez créé un **événement**. Vous l’avez appelé comme suit `ldapAccountCreationEvent` et remplacé `ldap` par votre ldap. Il s’agit du résultat de la création de l’événement :

![ACOP](./images/eventdone.png)

Vous devez maintenant considérer cet événement comme le début de ce Parcours. Pour ce faire, accédez au côté gauche de l’écran et recherchez votre événement dans la liste des événements.

![ACOP](./images/eventlist.png)

Sélectionnez votre événement, faites-le glisser et déposez-le sur le canevas de Parcours. Votre Parcours ressemble maintenant à ceci :

![ACOP](./images/journeyevent.png)

Pour la deuxième étape du parcours, vous devez ajouter une étape **Wait** courte. Accédez à la section **Orchestration** sur le côté gauche de votre écran pour trouver ceci. Vous utiliserez les attributs de profil et devez vous assurer qu’ils sont renseignés dans le profil client en temps réel.

![ACOP](./images/journeywait.png)

Votre parcours ressemble maintenant à ceci. Dans la partie droite de l’écran, vous devez configurer le temps d’attente. Définissez-le sur 1 minute. Cela donnera beaucoup de temps aux attributs de profil qui seront disponibles après le déclenchement de l’événement.

![ACOP](./images/journeywait1.png)

Cliquez sur **Ok** pour enregistrer vos modifications.

Comme troisième étape du parcours, vous devez ajouter une action **Email**. Accédez au côté gauche de votre écran à **Actions**, sélectionnez l’action **Email**, puis faites-la glisser sur le deuxième noeud de votre parcours. Vous voyez maintenant ceci.

![ACOP](./images/journeyactions.png)

Définissez la **catégorie** sur **Marketing** et sélectionnez une surface d&#39;email qui vous permet d&#39;envoyer des emails. Dans ce cas, la surface de l&#39;email à sélectionner est **Email**. Assurez-vous que les cases à cocher des **clics sur l’email** et des **ouvertures d’email** sont toutes deux activées.

![ACOP](./images/journeyactions1.png)

L’étape suivante consiste à créer votre message. Pour ce faire, cliquez sur **Modifier le contenu**.

![ACOP](./images/journeyactions2.png)

## 3.1.2.2 Créer votre message

Pour créer votre message, cliquez sur **Modifier le contenu**.

![ACOP](./images/journeyactions2.png)

Vous voyez maintenant ceci.

![ACOP](./images/journeyactions3.png)

Cliquez sur le champ de texte **Objet** .

![Journey Optimizer](./images/msg5.png)

Dans la zone de texte, commencez à écrire **Hi**

![Journey Optimizer](./images/msg6.png)

L’objet n’est pas encore terminé. Vous devez ensuite importer le jeton de personnalisation pour le champ **Prénom** stocké sous `profile.person.name.firstName`. Dans le menu de gauche, faites défiler l’écran vers le bas pour trouver l’élément **Person** et cliquez sur la flèche pour aller plus loin.

![Journey Optimizer](./images/msg7.png)

Recherchez maintenant l’élément **Nom complet** et cliquez sur la flèche pour aller plus loin.

![Journey Optimizer](./images/msg8.png)

Enfin, recherchez le champ **Prénom** et cliquez sur le signe **+** situé à côté. Le jeton de personnalisation apparaît alors dans le champ de texte.

![Journey Optimizer](./images/msg9.png)

Ajoutez ensuite le texte **, merci de vous être inscrit !**. Cliquez sur **Enregistrer**.

![Journey Optimizer](./images/msg10.png)

Vous serez alors de retour ici. Cliquez sur **Email Designer** pour créer le contenu de l’email.

![Journey Optimizer](./images/msg11.png)

Dans l’écran suivant, vous serez invité à utiliser 3 méthodes différentes pour fournir le contenu de l’email :

- **Conception à partir de zéro** : commencez par un canevas vierge et utilisez l’éditeur WYSIWYG pour faire glisser et déposer la structure et les composants de contenu afin de créer visuellement le contenu de l’email.
- **Codez votre propre** : créez votre propre modèle d&#39;email en le codant à l&#39;aide de HTML
- **Importer un HTML** : importez un modèle d’HTML existant que vous pourrez modifier.

Cliquez sur **Conception à partir de zéro**.

![Journey Optimizer](./images/msg12.png)

Dans le menu de gauche, vous trouverez les composants de structure que vous pouvez utiliser pour définir la structure de l&#39;email (lignes et colonnes).

![Journey Optimizer](./images/msg13.png)

Faites glisser et déposez une colonne **1:2 Left** du menu dans la zone de travail. Il s’agit de l’espace réservé de l’image du logo.

![Journey Optimizer](./images/msg14.png)

Faites glisser et déposez une **colonne 1:1** sous le composant précédent. Ce sera le bloc de bannière.

![Journey Optimizer](./images/msg15.png)

Faites glisser et déposez une colonne **1:2 Left** sous le composant précédent. Il s’agit du contenu réel avec une image sur le côté gauche et du texte sur le côté droit.

![Journey Optimizer](./images/msg16.png)

Faites ensuite glisser et déposez une **colonne 1:1** sous le composant précédent. Il s’agit du pied de page de l’email. Votre zone de travail doit maintenant ressembler à ceci :

![Journey Optimizer](./images/msg17.png)

Utilisons ensuite les composants de contenu pour ajouter du contenu à l’intérieur de ces blocs. Cliquez sur l’option de menu **Composants du contenu**

![Journey Optimizer](./images/msg18.png)

Faites glisser et déposez un composant **Image** dans la première cellule de la première ligne. Cliquez sur **Parcourir**.

![Journey Optimizer](./images/msg19.png)

Vous verrez alors ceci. Accédez au dossier **enablement-assets** et sélectionnez le fichier **luma-logo.png**. Cliquez sur **Sélectionner**.

![Journey Optimizer](./images/msg21.png)

Vous êtes maintenant de retour ici :

![Journey Optimizer](./images/msg25.png)

Accédez à **Composants du contenu** et faites glisser et déposez un composant **Image** dans la première cellule de la première ligne. Cliquez sur **Parcourir**.

![Journey Optimizer](./images/msg26.png)

Dans la fenêtre contextuelle **Assets**, accédez au dossier **enablement-assets**. Dans ce dossier, vous trouverez toutes les ressources précédemment préparées et chargées par l’équipe créative. Sélectionnez **module23-thankyou-new.png** et cliquez sur **Sélectionner**.

![Journey Optimizer](./images/msg28.png)

Vous obtiendrez alors ce qui suit :

![Journey Optimizer](./images/msg30.png)

Sélectionnez votre image et, dans le menu de droite, faites défiler l’écran vers le bas jusqu’à ce que le composant de curseur de largeur **Size** s’affiche. Utilisez le curseur pour définir la largeur sur f.i. **60%**.

![Journey Optimizer](./images/msg31.png)

Ensuite, accédez à **Composants du contenu** et faites glisser et déposez un composant **Texte** dans le composant de structure sur la quatrième ligne.

![Journey Optimizer](./images/msg33.png)

Sélectionnez le texte par défaut **Veuillez saisir votre texte ici.** comme vous le feriez avec tout éditeur de texte. Écrivez **Cher** à la place. La barre d’outils de texte s’affiche lorsque vous êtes en mode texte.

![Journey Optimizer](./images/msg34.png)

Dans la barre d’outils, cliquez sur l’icône **Ajouter une personnalisation** .

![Journey Optimizer](./images/msg35.png)

Ensuite, vous devez importer le jeton de personnalisation **Prénom** stocké sous `profile.person.name.firstName`. Dans le menu, recherchez l’élément **Person** , recherchez l’élément **Full Name** , puis cliquez sur l’icône **+** pour ajouter le champ First Name à l’éditeur d’expression.

Cliquez sur **Enregistrer**.

![Journey Optimizer](./images/msg36.png)

Vous remarquerez maintenant comment le champ de personnalisation a été ajouté à votre texte.

![Journey Optimizer](./images/msg37.png)

Dans le même champ de texte, appuyez deux fois sur **Entrée** pour ajouter deux lignes et écrivez **Merci d’avoir créé votre compte avec Luma !**.

![Journey Optimizer](./images/msg38.png)

La dernière vérification à effectuer pour vous assurer que votre email est prêt est de le prévisualiser, cliquez sur le bouton **Simuler le contenu** .

![Journey Optimizer](./images/msg50.png)

Commencez par identifier le profil que vous souhaitez utiliser pour la prévisualisation. Sélectionnez l’espace de noms **email** en cliquant sur l’icône en regard du champ **Entrer l’espace de noms d’identité** .

Dans la liste des espaces de noms d’identité, sélectionnez l’espace de noms **Email**.

Dans le champ **Valeur d’identité**, saisissez l’adresse électronique d’un précédent profil de démonstration qui est déjà stocké dans Real-time Customer Profile. Par exemple, **woutervangeluwe+06022022-01@gmail.com** et cliquez sur le bouton **Rechercher un profil de test**

![Journey Optimizer](./images/msg53.png)

Une fois votre profil affiché dans le tableau, cliquez sur l’onglet **Aperçu** pour accéder à l’écran de prévisualisation.

Lorsque l’aperçu est prêt, vérifiez que la personnalisation est correcte dans la ligne d’objet. Le texte du corps ainsi que le lien de désinscription sont mis en surbrillance sous la forme d’un lien hypertexte.

Cliquez sur **Fermer** pour fermer l’aperçu.

![Journey Optimizer](./images/msg54.png)

Cliquez sur **Enregistrer** pour enregistrer votre message.

![Journey Optimizer](./images/msg55.png)

Revenez au tableau de bord des messages en cliquant sur la **flèche** en regard de l’objet du texte dans le coin supérieur gauche.

![Journey Optimizer](./images/msg56.png)

Vous avez maintenant terminé de créer votre email d’enregistrement. Cliquez sur la flèche dans le coin supérieur gauche pour revenir à votre parcours.

![Journey Optimizer](./images/msg57.png)

Cliquez sur **OK**.

![Journey Optimizer](./images/msg57a.png)

## 3.1.2.3 Publish votre parcours

Vous devez toujours donner un nom à votre parcours. Pour ce faire, cliquez sur l’icône **Propriétés** dans le coin supérieur droit de votre écran.

![ACOP](./images/journeyname.png)

Vous pouvez ensuite y saisir le nom du parcours. Veuillez utiliser `--demoProfileLdap-- - Account Creation Journey`. Cliquez sur **OK** pour enregistrer vos modifications.

![ACOP](./images/journeyname1.png)

Vous pouvez maintenant publier votre parcours en cliquant sur **Publish**.

![ACOP](./images/publishjourney.png)

Cliquez de nouveau sur **Publish**.

![ACOP](./images/publish1.png)

Une barre de confirmation verte s’affiche alors, indiquant que votre parcours est désormais Publié.

![ACOP](./images/published.png)

Vous avez maintenant terminé cet exercice.

Étape suivante : [3.1.3 Mettre à jour votre propriété de collecte de données et tester votre parcours](./ex3.md)

[Revenir au module 3.1](./journey-orchestration-create-account.md)

[Revenir à tous les modules](../../../overview.md)
