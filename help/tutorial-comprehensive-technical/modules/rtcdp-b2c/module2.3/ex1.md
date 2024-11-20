---
title: CDP en temps réel - Créer une audience et agir - Créer une audience
description: CDP en temps réel - Créer une audience et agir - Créer une audience
kt: 5342
doc-type: tutorial
exl-id: a46b1640-769d-4fb3-97e6-beaf9706efbf
source-git-commit: acb941e4ee668248ae0767bb9f4f42e067c181ba
workflow-type: tm+mt
source-wordcount: '611'
ht-degree: 3%

---

# 2.3.1 Création d’une audience

Dans cet exercice, vous allez créer une audience en utilisant le créateur d’audiences de Adobe Experience Platform.

## Contexte

Répondre aux intérêts d’un client doit être en temps réel. L’utilisation d’une audience, à condition que l’audience soit admissible en temps réel, constitue l’un des moyens de répondre au comportement des clients en temps réel. Dans cet exercice, vous devez créer une audience, en tenant compte de l’activité réelle sur le site web que nous avons utilisé.

## Identifier le comportement auquel vous souhaitez réagir

Accédez à [https://dsn.adobe.com](https://dsn.adobe.com). Une fois connecté avec votre Adobe ID, vous verrez ceci. Cliquez sur les 3 points **...** dans le projet de votre site web, puis cliquez sur **Exécuter** pour l’ouvrir.

![DSN](./../../datacollection/module1.1/images/web8.png)

Vous verrez alors votre site web de démonstration ouvert. Sélectionnez l’URL et copiez-la dans le presse-papiers.

![DSN](../../gettingstarted/gettingstarted/images/web3.png)

Ouvrez une nouvelle fenêtre de navigateur incognito.

![DSN](../../gettingstarted/gettingstarted/images/web4.png)

Collez l’URL de votre site web de démonstration, que vous avez copiée à l’étape précédente. Vous serez alors invité à vous connecter à l’aide de votre Adobe ID.

![DSN](../../gettingstarted/gettingstarted/images/web5.png)

Sélectionnez le type de compte et procédez à la connexion.

![DSN](../../gettingstarted/gettingstarted/images/web6.png)

Votre site web est alors chargé dans une fenêtre de navigateur incognito. Pour chaque exercice, vous devrez utiliser une fenêtre de navigateur incognito actualisée pour charger l’URL de votre site web de démonstration.

![DSN](../../gettingstarted/gettingstarted/images/web7.png)

Dans cet exemple, vous souhaitez répondre à un client spécifique qui consulte un produit spécifique.
Sur la page d&#39;accueil de **Citi Signal**, accédez à **Phones &amp; devices** et cliquez sur le produit **Galaxy S24**.

![Ingestion des données](./images/homegalaxy.png)

Ainsi, lorsque quelqu’un visite la page du produit pour **Galaxy S24**, vous souhaitez pouvoir agir. La première chose à faire est de définir une audience.

![Ingestion des données](./images/homegalaxy1.png)

## Créer l’audience

Accédez à [Adobe Experience Platform](https://experience.adobe.com/platform). Une fois connecté, vous accédez à la page d’accueil de Adobe Experience Platform.

![Ingestion des données](./../../../modules/datacollection/module1.2/images/home.png)

Avant de continuer, vous devez sélectionner un **sandbox**. L’environnement de test à sélectionner est nommé ``--aepSandboxName--``. Après avoir sélectionné l’[!UICONTROL sandbox] approprié, vous verrez le changement d’écran et vous êtes désormais dans votre [!UICONTROL sandbox] dédié.

![Ingestion des données](./../../../modules/datacollection/module1.2/images/sb1.png)

Dans le menu de gauche, accédez à **Audiences**, puis à **Parcourir** où vous pouvez voir un aperçu de toutes les audiences existantes. Cliquez sur le bouton **Créer une audience** pour commencer à créer une audience.

![Segmentation](./images/menuseg.png)

Sélectionnez **Créer la règle** et cliquez sur **Créer**.

![Segmentation](./images/menuseg1.png)

Comme mentionné ci-dessus, vous devez créer une audience parmi tous les clients qui ont consulté le produit **Galaxy S24**.

Pour créer cette audience, vous devez ajouter un événement. Vous pouvez trouver tous les événements en cliquant sur l’icône **Événements** dans la barre de menus **Audiences**.

Vous verrez ensuite le noeud de niveau supérieur **XDM ExperienceEvent**.

Pour rechercher les clients qui ont visité le produit **Galaxy S24**, cliquez sur **XDM ExperienceEvent**.

![Segmentation](./images/findee.png)

Faites défiler l’écran jusqu’à **Éléments de liste de produits** et cliquez dessus.

![Segmentation](./images/see.png)

Sélectionnez **Nom** et faites glisser et déposez l’objet **Nom** du menu de gauche **Éléments de liste de produits** sur le canevas du créateur d’audiences dans la section **Événements**.

![Segmentation](./images/eewebpdtlname1.png)

Le paramètre de comparaison doit être **equals** et, dans le champ de saisie, saisissez `Galaxy S24`.

![Segmentation](./images/pv.png)

Vos **règles d’événement** doivent maintenant ressembler à ceci. Chaque fois que vous ajoutez un élément au créateur d’audiences, vous pouvez cliquer sur le bouton **Actualiser l’estimation** pour obtenir une nouvelle estimation de la population de votre audience.

![Segmentation](./images/ldap4.png)

Donnez un nom à votre audience et définissez la **Méthode d’évaluation** sur **Edge**.

Pour définir une convention d’affectation des noms, utilisez :

- `--aepUserLdap-- - Interest in Galaxy S24`

Cliquez ensuite sur le bouton **Publish** pour enregistrer votre audience.

![Segmentation](./images/segmentname.png)

Vous revenez alors à la page d’aperçu de l’audience.

![Segmentation](./images/savedsegment.png)

Étape suivante : [2.3.2 Passez en revue la configuration de la destination DV360 à l’aide des destinations](./ex2.md)

[Revenir au module 2.3](./real-time-cdp-build-a-segment-take-action.md)

[Revenir à tous les modules](../../../overview.md)
