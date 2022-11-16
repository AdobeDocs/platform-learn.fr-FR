---
title: CDP en temps réel - Création d’un segment et action - Création d’un segment
description: CDP en temps réel - Création d’un segment et action - Création d’un segment
kt: 5342
audience: Data Architect, Orchestration Engineer, Marketer
doc-type: tutorial
activity: develop
exl-id: c0778e81-4282-433d-9e02-37e32bf370ef
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '660'
ht-degree: 2%

---

# 6.1 Création d’un segment

Dans cet exercice, vous allez créer un segment en utilisant le créateur de segments de Adobe Experience Platform.

## 6.1.1 Contexte

Dans le monde d&#39;aujourd&#39;hui, répondre au comportement d&#39;un client doit être en temps réel. L’utilisation d’un segment, à condition que le segment soit admissible en temps réel, constitue l’une des façons de répondre au comportement des clients en temps réel. Dans cet exercice, vous devez créer un segment, en tenant compte de l’activité réelle sur le site web que nous avons utilisé.

## 6.1.2 Identifier le comportement auquel vous souhaitez réagir

Accédez à [https://builder.adobedemo.com/projects](https://builder.adobedemo.com/projects). Une fois connecté avec votre Adobe ID, vous verrez ceci. Cliquez sur le projet de votre site web pour l’ouvrir.

![DSN](../module0/images/web8.png)

Vous pouvez maintenant suivre le flux ci-dessous pour accéder au site web. Cliquez sur **Intégrations**.

![DSN](../module0/images/web1.png)

Sur le **Intégrations** , vous devez sélectionner la propriété de collecte de données qui a été créée dans l’exercice 0.1.

![DSN](../module0/images/web2.png)

Vous verrez alors votre site web de démonstration ouvert. Sélectionnez l’URL et copiez-la dans le presse-papiers.

![DSN](../module0/images/web3.png)

Ouvrez une nouvelle fenêtre de navigateur incognito.

![DSN](../module0/images/web4.png)

Collez l’URL de votre site web de démonstration, que vous avez copiée à l’étape précédente. Vous serez alors invité à vous connecter à l’aide de votre Adobe ID.

![DSN](../module0/images/web5.png)

Sélectionnez le type de compte et procédez à la connexion.

![DSN](../module0/images/web6.png)

Votre site web est alors chargé dans une fenêtre de navigateur incognito. Pour chaque démonstration, vous devez utiliser une fenêtre de navigateur incognito actualisée pour charger l’URL de votre site web de démonstration.

![DSN](../module0/images/web7.png)

Dans cet exemple, vous souhaitez répondre à un client spécifique qui consulte un produit spécifique.
Dans la **Luma** homepage, accédez à **Hommes**, puis cliquez sur le produit **PROTÉGER UN JACKSHIRT D&#39;AFFICHAGE**.

![Ingestion des données](./images/homenadia.png)

Ainsi, lorsque quelqu’un visite la page de produit pour **PROTÉGER UN JACKSHIRT D&#39;AFFICHAGE**, vous voulez pouvoir agir. La première chose à faire est de définir un segment.

![Ingestion des données](./images/homenadiapp.png)

## 6.1.3 Création du segment

Accédez à [Adobe Experience Platform](https://experience.adobe.com/platform). Une fois connecté, vous accédez à la page d’accueil de Adobe Experience Platform.

![Ingestion des données](../module2/images/home.png)

Avant de continuer, vous devez sélectionner une **sandbox**. L’environnement de test à sélectionner est nommé ``--aepSandboxId--``. Pour ce faire, cliquez sur le texte **[!UICONTROL Production Prod]** dans la ligne bleue en haut de votre écran. Après avoir sélectionné le [!UICONTROL sandbox], vous verrez le changement d’écran et vous êtes maintenant dans votre [!UICONTROL sandbox].

![Ingestion des données](../module2/images/sb1.png)

Dans le menu de gauche, accédez à **Segments** puis accédez à **Parcourir** où vous pouvez voir un aperçu de tous les segments existants. Cliquez sur le bouton **Créer un segment** pour commencer à créer un segment.

![Segmentation](./images/menuseg.png)

Comme mentionné ci-dessus, vous devez créer un segment parmi tous les clients qui ont consulté le produit. **PROTÉGER UN JACKSHIRT D&#39;AFFICHAGE**.

Pour créer ce segment, vous devez ajouter un événement . Vous pouvez trouver tous les événements en cliquant sur la variable **Événements** dans le **Segments** de la barre de menus.

Ensuite, vous verrez le niveau supérieur **XDM ExperienceEvent** noeud .

Pour rechercher des clients qui ont consulté la variable **PROTÉGER UN JACKSHIRT D&#39;AFFICHAGE** produit, cliquez sur **XDM ExperienceEvent**.

![Segmentation](./images/findee.png)

Faites défiler jusqu’à **Éléments de liste de produits** et cliquez dessus.

![Segmentation](./images/see.png)

Sélectionner **Nom** et faites glisser et déposez le **Nom** à partir de la gauche **Éléments de liste de produits** sur le canevas du créateur de segments dans la **Événements** .

![Segmentation](./images/eewebpdtlname1.png)

Le paramètre de comparaison doit être **est égal à** et dans le champ de saisie, saisissez `PROTEUS FITNESS JACKSHIRT`.

![Segmentation](./images/pv.png)

Votre **Règles d’événement** devrait maintenant ressembler à ceci. Chaque fois que vous ajoutez un élément au créateur de segments, vous pouvez cliquer sur le **Actualiser l’estimation** pour obtenir une nouvelle estimation de la population de votre segment.

![Segmentation](./images/ldap4.png)

Enfin, attribuons un nom à votre segment et enregistrez-le.

Pour définir une convention d’affectation des noms, utilisez :

- `--demoProfileLdap-- - Interest in PROTEUS FITNESS JACKSHIRT`

Le nom de votre segment doit se présenter comme suit :
`vangeluw - Interest in PROTEUS FITNESS JACKSHIRT`

Cliquez ensuite sur le **Enregistrer et fermer** pour enregistrer votre segment.

![Segmentation](./images/segmentname.png)

Vous allez maintenant revenir à la page d’aperçu du segment.

![Segmentation](./images/savedsegment.png)

Étape suivante : [6.2 Découvrez comment configurer une destination DV360 à l’aide de destinations](./ex2.md)

[Revenir au module 11](./real-time-cdp-build-a-segment-take-action.md)

[Revenir à tous les modules](../../overview.md)
