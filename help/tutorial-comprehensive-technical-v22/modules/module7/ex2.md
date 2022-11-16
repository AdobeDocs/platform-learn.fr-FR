---
title: Journey Optimizer Créer votre parcours et votre message électronique
description: Journey Optimizer Créer votre email
kt: 5342
audience: developer
doc-type: tutorial
activity: develop
exl-id: 2b7333c3-5b6a-41c5-a7a7-b048d1579ddd
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '1395'
ht-degree: 6%

---

# 7.2 Création de votre parcours et de votre message électronique

Dans cet exercice, vous allez configurer le parcours et le message qui doivent être déclenchés lorsqu’une personne crée un compte sur le site web de démonstration.

Connectez-vous à Adobe Journey Optimizer en accédant à [Adobe Experience Cloud](https://experience.adobe.com). Cliquez sur **Journey Optimizer**.

![ACOP](./images/acophome.png)

Vous serez redirigé vers le **Accueil**  dans Journey Optimizer. Tout d’abord, assurez-vous d’utiliser l’environnement de test approprié. L’environnement de test à utiliser est appelé `--aepSandboxId--`. Pour passer d’un environnement de test à un autre, cliquez sur **Production (VA7)** et sélectionnez l’environnement de test dans la liste. Dans cet exemple, l’environnement de test est nommé **Activation AEP FY22**. Vous serez alors dans le **Accueil** affichage de votre environnement de test `--aepSandboxId--`.

![ACOP](./images/acoptriglp.png)

## 7.2.1 Création de votre parcours

Dans le menu de gauche, cliquez sur **Parcours**. Cliquez ensuite sur **Créer un Parcours** pour créer un parcours.

![ACOP](./images/createjourney.png)

Vous verrez alors un écran de parcours vide.

![ACOP](./images/journeyempty.png)

Dans l’exercice précédent, vous avez créé une **Événement**. Vous l’avez appelé comme suit : `ldapAccountCreationEvent` et remplacé `ldap` avec votre ldap. Il s’agit du résultat de la création de l’événement :

![ACOP](./images/eventdone.png)

Vous devez maintenant considérer cet événement comme le début de ce Parcours. Pour ce faire, accédez au côté gauche de l’écran et recherchez votre événement dans la liste des événements.

![ACOP](./images/eventlist.png)

Sélectionnez votre événement, faites-le glisser et déposez-le sur le canevas de Parcours. Votre Parcours ressemble maintenant à ceci :

![ACOP](./images/journeyevent.png)

Pour la deuxième étape du parcours, vous devez ajouter une **Attente** étape . Accédez au côté gauche de l’écran au **Orchestration** pour le trouver. Vous utiliserez les attributs de profil et devez vous assurer qu’ils sont renseignés dans le profil client en temps réel.

![ACOP](./images/journeywait.png)

Votre parcours ressemble maintenant à ceci. Dans la partie droite de l’écran, vous devez configurer le temps d’attente. Définissez-le sur 1 minute. Cela donnera beaucoup de temps aux attributs de profil qui seront disponibles après le déclenchement de l’événement.

![ACOP](./images/journeywait1.png)

Cliquez sur **Ok** pour enregistrer vos modifications.

Pour la troisième étape du parcours, vous devez ajouter une **Email** action. Accédez au côté gauche de l’écran pour **Actions**, sélectionnez la variable **Email** puis faites-la glisser sur le deuxième noeud de votre parcours. Vous voyez maintenant ceci.

![ACOP](./images/journeyactions.png)

Définissez la variable **Catégorie** to **Marketing** et sélectionnez une surface d&#39;email permettant d&#39;envoyer des emails. Dans ce cas, la surface de l&#39;email à sélectionner est **Email**. Assurez-vous que les cases à cocher de **Clics sur l&#39;email** et **ouvertures de courrier électronique** sont toutes deux activées.

![ACOP](./images/journeyactions1.png)

L’étape suivante consiste à créer votre message. Pour ce faire, cliquez sur **Modifier le contenu**.

![ACOP](./images/journeyactions2.png)

## 7.2.2 Création de votre message

Pour créer votre message, cliquez sur **Modifier le contenu**.

![ACOP](./images/journeyactions2.png)

Vous voyez maintenant ceci.

![ACOP](./images/journeyactions3.png)

Cliquez sur le bouton **Objet** Champ de texte.

![Journey Optimizer](./images/msg5.png)

Dans la zone de texte, commencez à écrire. **Bonjour**

![Journey Optimizer](./images/msg6.png)

L’objet n’est pas encore terminé. Vous devez ensuite importer le jeton de personnalisation pour le champ. **Prénom** qui est stocké sous `profile.person.name.firstName`. Dans le menu de gauche, faites défiler l’écran vers le bas pour trouver le **Personne** et cliquez sur la flèche pour aller plus loin.

![Journey Optimizer](./images/msg7.png)

Maintenant, trouvez la variable **Nom complet** et cliquez sur la flèche pour aller plus loin.

![Journey Optimizer](./images/msg8.png)

Enfin, recherchez la **Prénom** et cliquez sur le champ **+** signe à côté. Le jeton de personnalisation apparaît alors dans le champ de texte.

![Journey Optimizer](./images/msg9.png)

Ajoutez ensuite le texte. **, merci de vous être inscrit !**. Cliquez sur **Enregistrer**.

![Journey Optimizer](./images/msg10.png)

Vous serez alors de retour ici. Cliquez sur **Concepteur d&#39;email** pour créer le contenu de l&#39;email.

![Journey Optimizer](./images/msg11.png)

Dans l’écran suivant, vous serez invité à utiliser 3 méthodes différentes pour fournir le contenu de l’email :

- **Conception à partir de zéro**: Commencez par un canevas vierge et utilisez l’éditeur WYSIWYG pour faire glisser et déposer la structure et les composants de contenu afin de créer visuellement le contenu de l’email.
- **Codez vos propres**: Créez votre propre modèle d&#39;email en le codant à l&#39;aide de HTML
- **HTML d’importation**: Importez un modèle de HTML existant que vous pourrez éditer.

Cliquez sur **Conception à partir de zéro**.

![Journey Optimizer](./images/msg12.png)

Dans le menu de gauche, vous trouverez les composants de structure que vous pouvez utiliser pour définir la structure de l&#39;email (lignes et colonnes).

![Journey Optimizer](./images/msg13.png)

Faites glisser et déposez un **Colonne 1:2 gauche** du menu vers la zone de travail. Il s’agit de l’espace réservé de l’image du logo.

![Journey Optimizer](./images/msg14.png)

Faites glisser et déposez un **Colonne 1:1** sous le composant précédent. Ce sera le bloc de bannière.

![Journey Optimizer](./images/msg15.png)

Faites glisser et déposez un **Colonne 1:2 gauche** sous le composant précédent. Il s’agit du contenu réel avec une image sur le côté gauche et du texte sur le côté droit.

![Journey Optimizer](./images/msg16.png)

Ensuite, effectuez un glisser-déposer d’une **Colonne 1:1** sous le composant précédent. Il s’agit du pied de page de l’email. Votre zone de travail doit maintenant ressembler à ceci :

![Journey Optimizer](./images/msg17.png)

Utilisons ensuite les composants de contenu pour ajouter du contenu à l’intérieur de ces blocs. Cliquez sur le bouton **Composants de contenu** élément de menu

![Journey Optimizer](./images/msg18.png)

Faites glisser et déposez un **Image** dans la première cellule de la première ligne. Cliquez sur **Parcourir**.

![Journey Optimizer](./images/msg19.png)

Vous verrez alors ceci. Accédez au dossier **enablement-assets** et sélectionnez le fichier **luma-logo.png**. Cliquez sur **Sélectionner**.

![Journey Optimizer](./images/msg21.png)

Vous êtes maintenant de retour ici :

![Journey Optimizer](./images/msg25.png)

Accédez à **Composants de contenu** et faites glisser un **Image** dans la première cellule de la première ligne. Cliquez sur **Parcourir**.

![Journey Optimizer](./images/msg26.png)

Dans le **Ressources** , accédez à la **enablement-assets** dossier. Dans ce dossier, vous trouverez toutes les ressources précédemment préparées et chargées par l’équipe créative. Sélectionner **module23-thankyou-new.png** et cliquez sur **Sélectionner**.

![Journey Optimizer](./images/msg28.png)

Vous obtiendrez alors ce qui suit :

![Journey Optimizer](./images/msg30.png)

Sélectionnez votre image, puis, dans le menu de droite, faites défiler l’écran vers le bas jusqu’à ce que le **Taille** composant de curseur de largeur. Utilisez le curseur pour définir la largeur sur f.i. **60 %**.

![Journey Optimizer](./images/msg31.png)

Ensuite, accédez à **Composants de contenu** et faites glisser un **Texte** dans le composant de structure sur la quatrième ligne.

![Journey Optimizer](./images/msg33.png)

Sélectionner le texte par défaut **Veuillez saisir votre texte ici.** comme vous le feriez avec n’importe quel éditeur de texte. Write **Cher** au lieu de . La barre d’outils de texte s’affiche lorsque vous êtes en mode texte.

![Journey Optimizer](./images/msg34.png)

Dans la barre d’outils, cliquez sur le bouton **Ajouter une personnalisation** icône .

![Journey Optimizer](./images/msg35.png)

Ensuite, vous devez apporter le **Prénom** jeton de personnalisation stocké sous `profile.person.name.firstName`. Dans le menu, recherchez le **Personne** élément, accédez au **Nom complet** , puis cliquez sur le bouton **+** pour ajouter le champ Prénom à l’éditeur d’expression.

Cliquez sur **Enregistrer**.

![Journey Optimizer](./images/msg36.png)

Vous remarquerez maintenant comment le champ de personnalisation a été ajouté à votre texte.

![Journey Optimizer](./images/msg37.png)

Dans le même champ de texte, appuyez sur **Entrée** deux fois pour ajouter deux lignes et écrire **Merci d’avoir créé votre compte avec Luma !**.

![Journey Optimizer](./images/msg38.png)

La dernière vérification à effectuer pour vous assurer que votre email est prêt consiste à le prévisualiser, cliquez sur l’icône **Simulation du contenu** bouton .

![Journey Optimizer](./images/msg50.png)

Commencez par identifier le profil que vous souhaitez utiliser pour la prévisualisation. Sélectionnez la **email** espace de noms en cliquant sur l’icône en regard de **Saisir l’espace de noms d’identité** champ .

Dans la liste des espaces de noms d’identité, sélectionnez le **Email** espace de noms.

Dans le **Valeur d’identité** , saisissez l’adresse électronique d’un précédent profil de démonstration déjà stocké dans Real-time Customer Profile. Par exemple **woutervangeluwe+06022022-01@gmail.com** et cliquez sur le bouton **Rechercher un profil de test** button

![Journey Optimizer](./images/msg53.png)

Une fois votre profil affiché dans le tableau, cliquez sur le **Aperçu** pour accéder à l’écran de prévisualisation.

Lorsque l’aperçu est prêt, vérifiez que la personnalisation est correcte dans la ligne d’objet. Le texte du corps ainsi que le lien de désinscription sont mis en surbrillance sous la forme d’un lien hypertexte.

Cliquez sur **Fermer** pour fermer l’aperçu.

![Journey Optimizer](./images/msg54.png)

Cliquez sur **Enregistrer** pour enregistrer votre message.

![Journey Optimizer](./images/msg55.png)

Revenez au tableau de bord du message en cliquant sur le bouton **flèche** en regard du texte de l’objet dans le coin supérieur gauche.

![Journey Optimizer](./images/msg56.png)

Vous avez maintenant terminé de créer votre email d’enregistrement. Cliquez sur la flèche dans le coin supérieur gauche pour revenir à votre parcours.

![Journey Optimizer](./images/msg57.png)

Cliquez sur **OK**.

![Journey Optimizer](./images/msg57a.png)

## 7.2.3 Publication du parcours

Vous devez toujours donner un nom à votre parcours. Pour ce faire, cliquez sur le bouton **Propriétés** en haut à droite de l’écran.

![ACOP](./images/journeyname.png)

Vous pouvez ensuite y saisir le nom du parcours. Veuillez utiliser `--demoProfileLdap-- - Account Creation Journey`. Cliquez sur **OK** pour enregistrer vos modifications.

![ACOP](./images/journeyname1.png)

Vous pouvez maintenant publier votre parcours en cliquant sur **Publier**.

![ACOP](./images/publishjourney.png)

Cliquez sur **Publier** encore une fois.

![ACOP](./images/publish1.png)

Une barre de confirmation verte s’affiche alors, indiquant que votre parcours est désormais Publié.

![ACOP](./images/published.png)

Vous avez maintenant terminé cet exercice.

Étape suivante : [7.3 Mise à jour de la propriété Collecte de données et test de votre parcours](./ex3.md)

[Revenir au module 7](./journey-orchestration-create-account.md)

[Revenir à tous les modules](../../overview.md)
