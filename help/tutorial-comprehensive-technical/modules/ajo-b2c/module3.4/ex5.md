---
title: Adobe Journey Optimizer - Événements commerciaux
description: Cette section explique comment utiliser la fonctionnalité d’événements professionnels pour réaliser un cas pratique "article en stock".
kt: 5342
doc-type: tutorial
source-git-commit: 6962a0d37d375e751a05ae99b4f433b0283835d0
workflow-type: tm+mt
source-wordcount: '1195'
ht-degree: 8%

---

# 3.4.5 Création d’un parcours d’événement commercial

Connectez-vous à Adobe Journey Optimizer en vous rendant à [Adobe Experience Cloud](https://experience.adobe.com?lang=fr). Cliquez sur **Journey Optimizer**.

![ACOP](./../../../modules/ajo-b2c/module3.2/images/acophome.png)

Vous serez redirigé vers la vue **Home** dans Journey Optimizer. Tout d’abord, assurez-vous d’utiliser l’environnement de test approprié. L’environnement de test à utiliser s’appelle `--aepSandboxName--`. Pour passer d’un environnement de test à un autre, cliquez sur **Production Prod (VA7)** et sélectionnez l’environnement de test dans la liste. Dans cet exemple, l’environnement de test est nommé **AEP Enablement FY22**. Vous serez alors dans la vue **Home** de votre environnement de test `--aepSandboxName--`.

![ACOP](./../../../modules/ajo-b2c/module3.2/images/acoptriglp.png)

## 3.4.5.1 Création d’un événement commercial

Dans le menu de gauche, cliquez sur **Configurations**. Cliquez sur le bouton **Gérer** dans la carte **Événements** .

![Journey Optimizer](./images/be1.png)

Les événements professionnels sont un nouveau type d’événement que vous pouvez créer dans Journey Optimizer. Contrairement aux événements **Unitary** que vous avez créés dans les modules précédents, les événements métier ne sont pas déclenchés par le client mais par l’organisation. Vous allez maintenant créer votre événement professionnel.

Cliquez sur **Créer un événement**.

![Journey Optimizer](./images/be2.png)

Saisissez les valeurs suivantes dans le formulaire de création d&#39;un événement :

- **Nom** : `--aepUserLdap--ItemBackInStock`. Par exemple : **vangeluwItemBackInStock**
- **Description** : cet événement est déclenché lorsqu’un produit est de nouveau en stock.
- **Type** : sélectionnez **Business** dans la liste déroulante

![Journey Optimizer](./images/evde.png)

Pour le schéma, sélectionnez **Demo System - Event Schema for JO Business Events (Global v1.1) v.1**. Vous devez maintenant sélectionner les champs du schéma dont vous avez besoin pour notre cas d’utilisation.

![Journey Optimizer](./images/evdes.png)

Procédez de la façon suivante :

Cliquez sur l&#39;icône **crayon** dans le champ où il est indiqué **1 champ sélectionné**.

![Journey Optimizer](./images/23.8-4.png)

Sélectionnez tous les champs disponibles dans le schéma, puis cliquez sur **OK**.

![Journey Optimizer](./images/23.8-5.png)

Pour la condition : vous devez spécifier les enregistrements de ce schéma qui déclencheront l’événement d’entreprise.

Procédez de la façon suivante :

Cliquez sur l&#39;icône **crayon** dans le champ où il est indiqué **Ajouter une condition**.

![Journey Optimizer](./images/23.8-6.png)

Sur le côté gauche, développez l’objet `--aepTenantId--`, développez l’objet **joBusinessEvents** et faites glisser le champ **eventName** sur la zone de travail.

![Journey Optimizer](./images/23.8-7.png)

Pour le champ **eventName**, saisissez la valeur suivante : `--aepUserLdap--ItemBackInStock`. Par exemple : vangeluwItemBackInStock.
Cliquez sur **OK**.

![Journey Optimizer](./images/23.8-8.png)

Cliquez sur **OK**.

![Journey Optimizer](./images/23.8-9.png)

Enfin, votre formulaire de création d’événement doit ressembler à ceci. Cliquez sur **Enregistrer** pour enregistrer votre événement professionnel.

![Journey Optimizer](./images/23.8-10.png)

## 3.4.5.2 Création d’un parcours d’événement commercial

Vous pouvez désormais exploiter cet événement professionnel et le message dans un parcours. Accédez à **Parcours**. Cliquez sur **Créer un Parcours**.

![Journey Optimizer](./images/bej10.png)

Sur le côté droit se trouve un formulaire dans lequel vous devez spécifier le nom et la description du parcours. Saisissez les valeurs suivantes :

- **Nom** : `--aepUserLdap-- - Item back in stock journey`. Par exemple : vangeluw - Article en parcours de stock
- **Description** : ce parcours envoie un SMS lorsqu’un article est de nouveau en stock à un visiteur qui a manifesté son intérêt.

Cliquez sur **OK**.

![Journey Optimizer](./images/bej11.png)

Dans le menu de gauche, sous **Events**, recherchez votre ldap. Vous trouverez l&#39;événement professionnel `--aepUserLdap--ItemBackInStock` créé précédemment. Faites glisser et déposez cet événement sur la zone de travail, car il s’agira du point de départ du parcours.

![Journey Optimizer](./images/bej12.png)

Comme vous pouvez le constater, une activité **Lecture de segment** a été automatiquement ajoutée à la zone de travail. Cela est dû au fait que les événements professionnels envoient uniquement un déclencheur pour que le parcours lise un segment spécifique, qui récupère ensuite la liste des profils pour ce parcours.

Cliquez sur l’activité **Lecture de segment** .
La configuration **Lecture de segment** exige que vous sélectionniez le segment que vous souhaitez avertir de l’événement commercial qui vient d’avoir lieu. Cliquez sur le champ **Sélectionner un segment** .

![Journey Optimizer](./images/bej13.png)

Dans la fenêtre contextuelle **Choisir un segment**, recherchez votre LDAP et sélectionnez le segment que vous avez créé dans [Module 2.3 - CDP en temps réel - Créer un segment et entreprendre l’action ](./../../../modules/rtcdp-b2c/module2.3/real-time-cdp-build-a-segment-take-action.md) nommée `--aepUserLdap-- - Interest in PROTEUS FITNESS JACKSHIRT`. par exemple : vangeluw - Intérêt pour PROTEUS FITNESS JACKSHIRT. Cliquez sur **Enregistrer**.

![Journey Optimizer](./images/bej14.png)

Cliquez ensuite sur **Ok**.

![Journey Optimizer](./images/bej15.png)

L’étape suivante consiste à faire glisser et déposer l’action que nous voulons exécuter dans ce parcours. Sélectionnez l’action **SMS**, puis faites-la glisser après la condition que vous venez d’ajouter.

![Démonstration](./images/jop9.png)

Définissez la **catégorie** sur **Marketing** et sélectionnez une surface SMS qui vous permet d&#39;envoyer des SMS. Dans ce cas, la surface d&#39;email à sélectionner est **SMS**.

![ACOP](./images/journeyactions1x.png)

L’étape suivante consiste à créer votre message. Pour ce faire, cliquez sur **Modifier le contenu**.

![ACOP](./images/journeyactions2x.png)

Le tableau de bord des messages s’affiche maintenant. Vous pouvez y configurer le texte de votre SMS. Cliquez sur la zone **Composer le message** pour créer votre message.

![Journey Optimizer](./images/sms3.png)

Saisissez le texte suivant : `Hi {{profile.person.name.firstName}}, the Proteus Fitness Jackshirt is back in stock at Luma.`. Cliquez sur **Enregistrer**.

![Journey Optimizer](./images/sms4.png)

Revenez au tableau de bord des messages en cliquant sur la **flèche** en regard de l’objet du texte dans le coin supérieur gauche.

![Journey Optimizer](./images/oc79xx.png)

Vous verrez maintenant votre action SMS terminée. Cliquez sur **OK**.

![Journey Optimizer](./images/oc79xxy.png)

Votre parcours est maintenant prêt à être publié. Cliquez sur **Publier**.

![Journey Optimizer](./images/jop13.png)

Cliquez de nouveau sur **Publish**.

![Journey Optimizer](./images/jop14.png)

Votre parcours est maintenant publié, vous pouvez le tester !

![Journey Optimizer](./images/jop15.png)

## 3.4.5.3 Test de votre parcours d’événements professionnels

Vous allez maintenant simuler la réévaluation d’un produit en ingérant un nouvel événement par rapport au **système de démonstration - schéma d’événement pour JO Business Events (Global v1.1) v.1** à l’aide de Postman.

Dans le menu de gauche, cliquez sur **Sources** , puis sur l’onglet **Comptes** .

![Journey Optimizer](./images/s1.png)

Dans l’onglet **Comptes**, vous trouverez le compte nommé **Journey Optimizer Business Events**. Cliquez dessus pour l’ouvrir.

![Journey Optimizer](./images/s2.png)

Ce compte ne comporte qu’un seul flux de données. Cliquez sur le nom du flux de données pour le sélectionner.

![Journey Optimizer](./images/s3.png)

Cliquez sur **Copier la payload du schéma** dans le menu de droite. Cette option copie la commande **curl** entière pour insérer un enregistrement dans le presse-papiers de **Demo System - Event Schema for JO Business Events (Global v1.1) v.1**.

![Journey Optimizer](./images/s4.png)

Coller la commande Curl dans un éditeur de texte

![Journey Optimizer](./images/s5.png)

Regardons de plus près cette demande,

- La demande du POST est envoyée à l’ID d’ingestion du serveur de collecte de données.
- La requête fait référence au schéma, au jeu de données et à l’ID d’organisation.
- Enfin, il contient le noeud xdmEntity qui représente les données que nous voulons créer dans le jeu de données.

Vous devez maintenant remplacer la ligne `xdmEntity` suivante...

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

...sur cette ligne, veillez à vérifier le champ eventName comme il doit être appelé `--aepUserLdap--ItemBackInStock`, qui représente la condition que vous avez spécifiée dans votre événement professionnel pour déclencher votre parcours.

```json
"xdmEntity": {
  "_experienceplatform": {
    "joBusinessEvents": {
      "eventDescription": "Product Proteus Fitness Jackshirt is back in stock",
      "eventName": "--aepUserLdap--ItemBackInStock",
      "stockEventId": "1"
    }
  },
  "_id": "/uri-reference",
  "eventType": "productBackInStock",
  "timestamp": "2021-04-19T15:25:39+00:00"
}
```

La commande **curl** mise à jour doit se présenter comme suit :

![Journey Optimizer](./images/s6.png)

Sélectionnez-la et copiez-la dans le presse-papiers.

Ouvrez Postman. Sur le côté gauche de Postman, cliquez sur **Importer**.

![Journey Optimizer](./images/23.8-46.png)

Sélectionnez l&#39;onglet **Texte brut** et collez la commande précédemment copiée ici. Cliquez sur **Continuer**.

![Journey Optimizer](./images/s7.png)

Cliquez sur **Importer**.

![Journey Optimizer](./images/23.8-50.png)

Postman a automatiquement converti la commande **curl** en une commande REST prête à être déclenchée. Appuyez simplement sur le bouton **Send** pour demander la création de cet enregistrement dans le jeu de données.

![Journey Optimizer](./images/23.8-51.png)

Vérifiez que votre demande a bien été reçue. Recherchez un état **200 OK** dans Postman.

![Journey Optimizer](./images/s8.png)

Le SMS peut prendre quelques minutes pour arriver sur votre téléphone portable. Si ce n’est pas le cas, votre segment **Centre d’intérêt de Proteus Fitness Jackshirt** peut ne pas contenir de profil avec un téléphone portable correct. Si tel est le cas, rendez-vous sur le site web de Luma, rendez-vous sur le produit **Proteus Fitness Jackshirt** et inscrivez-vous tout en vous assurant que vous fournissez le numéro de téléphone portable correct.

![Journey Optimizer](./images/s9.png)

Vous avez maintenant terminé cet exercice.

Étape suivante : [Résumé et avantages](./summary.md)

[Revenir au module 3.4](./journeyoptimizer.md)

[Revenir à tous les modules](../../../overview.md)
