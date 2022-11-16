---
title: Adobe Journey Optimizer - Événements commerciaux
description: Cette section explique comment utiliser la fonctionnalité d’événements professionnels pour réaliser un cas pratique "article en stock".
kt: 5342
audience: Data Engineer, Data Architect, Data Analyst
doc-type: tutorial
activity: develop
exl-id: cc06d847-a405-4223-836c-c22ad6c9caca
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '1187'
ht-degree: 8%

---

# 10.5 Création d’un parcours d’événement professionnel

Connectez-vous à Adobe Journey Optimizer en accédant à [Adobe Experience Cloud](https://experience.adobe.com). Cliquez sur **Journey Optimizer**.

![ACOP](../module7/images/acophome.png)

Vous serez redirigé vers le **Accueil**  dans Journey Optimizer. Tout d’abord, assurez-vous d’utiliser l’environnement de test approprié. L’environnement de test à utiliser est appelé `--aepSandboxId--`. Pour passer d’un environnement de test à un autre, cliquez sur **Production (VA7)** et sélectionnez l’environnement de test dans la liste. Dans cet exemple, l’environnement de test est nommé **Activation AEP FY22**. Vous serez alors dans le **Accueil** affichage de votre environnement de test `--aepSandboxId--`.

![ACOP](../module7/images/acoptriglp.png)

## 10.5.1 Création d’un événement commercial

Dans le menu de gauche, cliquez sur **Configurations**. Cliquez sur le bouton **Gérer** à l’intérieur du bouton **Événements** carte.

![Journey Optimizer](./images/be1.png)

Les événements professionnels sont un nouveau type d’événement que vous pouvez créer dans Journey Optimizer. Contrairement au **Unitaire** que vous avez créés dans les modules précédents, les événements métier ne sont pas déclenchés par le client, mais par l’organisation. Vous allez maintenant créer votre événement professionnel.

Cliquez sur **Créer un événement**.

![Journey Optimizer](./images/be2.png)

Saisissez les valeurs suivantes dans le formulaire de création d&#39;un événement :

- **Nom**: `--demoProfileLdap--ItemBackInStock`. Par exemple : **vangeluwItemBackInStock**
- **Description**: Cet événement est déclenché lorsqu’un produit est de nouveau en stock.
- **Type**: select **Entreprises** dans la liste déroulante

![Journey Optimizer](./images/evde.png)

Pour le schéma, sélectionnez **Système de démonstration - Schéma d’événement pour les événements métier JO (Global v1.1) v.1**. Vous devez maintenant sélectionner les champs du schéma dont vous avez besoin pour notre cas d’utilisation.

![Journey Optimizer](./images/evdes.png)

Procédez de la façon suivante :

Cliquez sur le bouton **crayon** sur le champ où il indique **1 champ sélectionné**.

![Journey Optimizer](./images/23.8-4.png)

Sélectionnez tous les champs disponibles dans le schéma, puis cliquez sur **OK**.

![Journey Optimizer](./images/23.8-5.png)

Pour la condition : vous devez spécifier les enregistrements de ce schéma qui déclencheront l’événement d’entreprise.

Procédez de la façon suivante :

Cliquez sur le bouton **crayon** sur le champ où il indique **Ajouter une condition**.

![Journey Optimizer](./images/23.8-6.png)

Sur le côté gauche, développez la variable `--aepTenantId--` , développez l’objet **joBusinessEvents** et effectuez un glisser-déposer du champ. **eventName** sur la zone de travail.

![Journey Optimizer](./images/23.8-7.png)

Pour le champ **eventName**, saisissez la valeur suivante : `--demoProfileLdap--ItemBackInStock`. Par exemple : vangeluwItemBackInStock.
Cliquez sur **OK**.

![Journey Optimizer](./images/23.8-8.png)

Cliquez sur **OK**.

![Journey Optimizer](./images/23.8-9.png)

Enfin, votre formulaire de création d’événement doit ressembler à ceci. Cliquez sur **Enregistrer** pour enregistrer votre événement professionnel.

![Journey Optimizer](./images/23.8-10.png)

## 10.5.2 Création d’un parcours d’événement commercial

Vous pouvez désormais exploiter cet événement professionnel et le message dans un parcours. Accédez à **Parcours**. Cliquez sur **Créer un Parcours**.

![Journey Optimizer](./images/bej10.png)

Sur le côté droit se trouve un formulaire dans lequel vous devez spécifier le nom et la description du parcours. Saisissez les valeurs suivantes :

- **Nom**: `--demoProfileLdap-- - Item back in stock journey`. Par exemple : vangeluw - Article de retour en stock
- **Description**: Ce parcours envoie un SMS lorsqu’un article est de nouveau en stock à un visiteur qui a manifesté de l’intérêt.

Cliquez sur **OK**.

![Journey Optimizer](./images/bej11.png)

Dans le menu de gauche, sous **Événements**, recherchez votre ldap. Vous trouverez l’événement professionnel créé précédemment. `--demoProfileLdap--ItemBackInStock`. Faites glisser et déposez cet événement sur la zone de travail, car il s’agira du point de départ du parcours.

![Journey Optimizer](./images/bej12.png)

Comme vous pouvez le voir, une **Lecture de segment** l’activité a été automatiquement ajoutée à la zone de travail. Cela est dû au fait que les événements professionnels envoient uniquement un déclencheur pour que le parcours lise un segment spécifique, qui récupère ensuite la liste des profils pour ce parcours.

Cliquez sur le bouton **Lecture de segment** activité.
Le **Lecture de segment** La configuration s’attend à ce que vous sélectionniez le segment que vous souhaitez avertir de l’événement commercial qui vient d’avoir lieu. Cliquez sur le bouton **Sélection d’un segment** champ .

![Journey Optimizer](./images/bej13.png)

Dans le **Sélection d’un segment** , recherchez votre ldap et sélectionnez le segment que vous avez créé dans [Module 6 - CDP en temps réel - Création d’un segment et action](../module6/real-time-cdp-build-a-segment-take-action.md) named `--demoProfileLdap-- - Interest in PROTEUS FITNESS JACKSHIRT`. par exemple : vangeluw - L&#39;intérêt pour PROTEUS FITNESS JACKSHIRT. Cliquez sur **Enregistrer**.

![Journey Optimizer](./images/bej14.png)

Cliquez ensuite sur **Ok**.

![Journey Optimizer](./images/bej15.png)

L’étape suivante consiste à faire glisser et déposer l’action que nous voulons exécuter dans ce parcours. Sélectionner l’action **SMS**, puis effectuez un glisser-déposer après la condition que vous venez d’ajouter.

![Démonstration](./images/jop9.png)

Définissez la variable **Catégorie** to **Marketing** et sélectionnez une surface sms permettant d&#39;envoyer des sms. Dans ce cas, la surface de l&#39;email à sélectionner est **SMS**.

![ACOP](./images/journeyactions1x.png)

L’étape suivante consiste à créer votre message. Pour ce faire, cliquez sur **Modifier le contenu**.

![ACOP](./images/journeyactions2x.png)

Le tableau de bord des messages s’affiche maintenant. Vous pouvez y configurer le texte de votre SMS. Cliquez sur le bouton **Composer le message** pour créer votre message.

![Journey Optimizer](./images/sms3.png)

Saisissez le texte suivant : `Hi {{profile.person.name.firstName}}, the Proteus Fitness Jackshirt is back in stock at Luma.`. Cliquez sur **Enregistrer**.

![Journey Optimizer](./images/sms4.png)

Revenez au tableau de bord du message en cliquant sur le bouton **flèche** en regard du texte de l’objet dans le coin supérieur gauche.

![Journey Optimizer](./images/oc79xx.png)

Vous verrez maintenant votre action SMS terminée. Cliquez sur **OK**.

![Journey Optimizer](./images/oc79xxy.png)

Votre parcours est maintenant prêt à être publié. Cliquez sur **Publier**.

![Journey Optimizer](./images/jop13.png)

Cliquez sur **Publier** encore une fois.

![Journey Optimizer](./images/jop14.png)

Votre parcours est maintenant publié, vous pouvez le tester !

![Journey Optimizer](./images/jop15.png)

## 10.5.3 Test de votre parcours d’événement professionnel

Vous allez à présent simuler la réévaluation d’un produit en ingérant un nouvel événement sur le **Système de démonstration - Schéma d’événement pour les événements métier JO (Global v1.1) v.1** à l’aide de Postman.

Dans le menu de gauche, cliquez sur **Sources** puis cliquez sur le bouton **Comptes** .

![Journey Optimizer](./images/s1.png)

Sur le **Comptes** , le compte nommé **Événements commerciaux Journey Optimizer**. Cliquez dessus pour l’ouvrir.

![Journey Optimizer](./images/s2.png)

Ce compte ne comporte qu’un seul flux de données. Cliquez sur le nom du flux de données pour le sélectionner.

![Journey Optimizer](./images/s3.png)

Cliquez sur **Copie de la payload de schéma** dans le menu de droite. Cette option copie l’intégralité de la variable **curl** pour insérer un enregistrement par rapport à la fonction **Système de démonstration - Schéma d’événement pour les événements métier JO (Global v1.1) v.1** dans le presse-papiers.

![Journey Optimizer](./images/s4.png)

Coller la commande Curl dans un éditeur de texte

![Journey Optimizer](./images/s5.png)

Regardons de plus près cette demande,

- La demande du POST est envoyée à l’ID d’ingestion du serveur de collecte de données.
- La requête fait référence au schéma, au jeu de données et à l’ID d’organisation.
- Enfin, il contient le noeud xdmEntity qui représente les données que nous voulons créer dans le jeu de données.

Vous devez maintenant remplacer ce qui suit : `xdmEntity` ligne...

```json
"xdmEntity": {
  "_experienceplatform": {
    "joBusinessEvents": {
      "eventDescription": "string",
      "eventName": "string",
      "stockEventId": "string"
    }
  },
  "_id": "/uri-reference",
  "eventType": "advertising.completes",
  "timestamp": "2018-11-12T20:20:39+00:00"
}
```

...sur cette ligne, veillez à vérifier le champ eventName comme il doit le dire. `--demoProfileLdap--ItemBackInStock`, qui représente la condition que vous avez spécifiée dans votre événement professionnel pour déclencher votre parcours.

```json
"xdmEntity": {
  "_experienceplatform": {
    "joBusinessEvents": {
      "eventDescription": "Product Proteus Fitness Jackshirt is back in stock",
      "eventName": "--demoProfileLdap--ItemBackInStock",
      "stockEventId": "1"
    }
  },
  "_id": "/uri-reference",
  "eventType": "productBackInStock",
  "timestamp": "2021-04-19T15:25:39+00:00"
}
```

La mise à jour **curl** doit se présenter comme suit :

![Journey Optimizer](./images/s6.png)

Sélectionnez-la et copiez-la dans le presse-papiers.

Ouvrez Postman. Sur le côté gauche de Postman, cliquez sur **Importer**.

![Journey Optimizer](./images/23.8-46.png)

Sélectionnez la **Texte brut** et collez la commande précédemment copiée ici. Cliquez sur **Continuer**.

![Journey Optimizer](./images/s7.png)

Cliquez sur **Importer**.

![Journey Optimizer](./images/23.8-50.png)

Postman a automatiquement converti la variable **curl** dans une commande REST prête à être déclenchée, appuyez simplement sur la touche **Envoyer** pour demander la création de cet enregistrement dans le jeu de données.

![Journey Optimizer](./images/23.8-51.png)

Vérifiez que votre demande a bien été reçue. Recherchez un **200 OK** statut dans postman.

![Journey Optimizer](./images/s8.png)

Le SMS peut prendre quelques minutes pour arriver sur votre téléphone portable. Si ce n’est pas le cas, votre **L&#39;intérêt pour le maillot de sport de Proteus** peut ne pas contenir de profil avec un téléphone portable correct. Si tel est le cas, rendez-vous sur le site web de Luma en accédant à la **Veste Fitness de Proteus** et enregistrez-vous tout en veillant à fournir le numéro de téléphone portable correct.

![Journey Optimizer](./images/s9.png)

Vous avez maintenant terminé cet exercice.

Étape suivante : [Résumé et avantages](./summary.md)

[Revenir au module 10](./journeyoptimizer.md)

[Revenir à tous les modules](../../overview.md)
