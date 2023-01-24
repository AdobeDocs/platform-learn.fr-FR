---
title: Bootcamp - Customer Journey Analytics - Visualisation avec Customer Journey Analytics - Brésil
description: Bootcamp - Customer Journey Analytics - Visualisation avec Customer Journey Analytics - Brésil
kt: 5342
audience: Data Engineer, Data Architect, Data Analyst
doc-type: tutorial
activity: develop
source-git-commit: 75a878ba596078e6d013b65062606931402302dd
workflow-type: tm+mt
source-wordcount: '1502'
ht-degree: 1%

---

# 4.5 Visualisation avec Customer Journey Analytics

## Objectifs

- Présentation de l’interface utilisateur d’Analysis Workspace
- Découvrez certaines fonctionnalités qui rendent Analysis Workspace si différent.
- Découvrez comment analyser dans CJA à l’aide d’Analysis Workspace

## Contexte

Au cours de cet exercice, vous utiliserez Analysis Workspace dans CJA pour analyser les consultations de produits, les entonnoirs de produits, la perte de clientèle, etc.

Utilisons le projet que vous avez créé dans [4.4 Préparation des données dans Analysis Workspace](./ex4.md), alors accédez à [https://analytics.adobe.com](https://analytics.adobe.com).

![demo](./images/prohome.png)

Ouvrez votre projet `yourLastName - Omnichannel Analysis`.

Une fois le projet ouvert et la vue des données `yourLastName - Omnichannel Analysis` sélectionné, vous êtes prêt à commencer à créer vos premières visualisations.

![demo](./images/prodataView1.png)

## Combien de consultations de produits y a-t-il quotidiennement ?

Tout d&#39;abord, nous devons sélectionner les dates appropriées pour analyser les données. Accédez au menu déroulant du calendrier sur le côté droit de la zone de travail. Cliquez dessus et sélectionnez la période applicable.

>[!IMPORTANT]
>
>Sélectionnez une période comme **Cette semaine** ou **Ce mois-ci**. Les données les plus récentes ont été ingérées le 19 septembre 2022.

![demo](./images/pro1.png)

Dans le menu de gauche (zone Composants), recherchez la mesure calculée. **Consultations produits**. Sélectionnez-la et faites-la glisser sur la zone de travail, en haut à droite du tableau à structure libre.

![demo](./images/pro2.png)

Automatiquement la dimension **Jour** sera ajouté pour créer votre premier tableau. Maintenant, vous pouvez voir que votre question a reçu une réponse instantanément.

![demo](./images/pro3.png)

Cliquez ensuite avec le bouton droit de la souris sur le résumé de la mesure.

![demo](./images/pro4.png)

Cliquez sur **Visualiser** puis sélectionnez **Ligne** comme visualisation.

![demo](./images/pro5.png)

Vous verrez vos consultations de produits par jour.

![demo](./images/pro6.png)

Vous pouvez modifier la plage horaire au jour le jour en cliquant sur **Paramètres** dans la visualisation.

![demo](./images/pro7.png)

Cliquez sur le point en regard de **Ligne** to **Gestion de la source de données**.

![demo](./images/pro7a.png)

Cliquez ensuite sur **Verrouiller la sélection** et sélectionnez **Éléments sélectionnés** pour verrouiller cette visualisation afin qu’elle affiche toujours une chronologie des consultations de produits.

![demo](./images/pro7b.png)

## Les 5 produits les plus consultés

Quels sont les 5 premiers produits consultés ?

N’oubliez pas d’enregistrer le projet de temps à autre.

| Système d’exploitation | Court |
| ----------------- |-------------| 
| Windows | Ctrl + S |
| Mac | Commande + S |

Commençons à trouver les 5 premiers produits consultés. Dans le menu de gauche, recherchez le **Nom du produit** - Dimension.

![demo](./images/pro8.png)

Maintenant, faites glisser et déposez **Nom du produit** pour remplacer la fonction **Jour** dimension :

Le résultat sera le suivant :

![demo](./images/pro10a.png)

Essayez ensuite de ventiler l’un des produits par nom de marque. Rechercher **brandName** et faites-le glisser sous le premier nom du produit.

![demo](./images/pro13.png)

Effectuez ensuite une ventilation à l’aide de l’agent utilisateur. Rechercher **Agent utilisateur** et faites-le glisser sous le nom de la marque.

![demo](./images/pro15.png)

Vous verrez alors :

![demo](./images/pro15a.png)

Enfin, vous pouvez ajouter d’autres visualisations. Sur le côté gauche, sous Visualisations, recherchez `Donut`. Take `Donut`, faites-le glisser sur la zone de travail sous le **Ligne** visualisation.

![demo](./images/pro18.png)

Ensuite, dans le tableau, sélectionnez les 5 premières **Agent utilisateur**  lignes de la ventilation que nous avons réalisée sous **Smartphone noir Google Pixel XL 32 Go** > **Signal Citi**. Lorsque vous sélectionnez les 5 lignes, conservez la propriété **CTRL** (sous Windows) ou le bouton **Commande** (sur Mac).

![demo](./images/pro20.png)

Le graphique en anneau est alors modifié :

![demo](./images/pro21.png)

Vous pouvez même adapter la conception pour la rendre plus lisible, en effectuant les deux **Ligne** et la variable **Anneau** graphique un peu plus petit pour s’adapter l’un à côté de l’autre :

![demo](./images/pro22.png)

Cliquez sur le point en regard de **Anneau** to **Gestion de la source de données**.
Cliquez ensuite sur **Verrouiller la sélection** pour verrouiller cette visualisation afin qu’elle affiche toujours une chronologie des consultations de produits.

![demo](./images/pro22b.png)

Pour en savoir plus sur les visualisations à l’aide d’Analysis Workspace, cliquez ici :

- [https://experienceleague.adobe.com/docs/analytics/analyze/analysis-workspace/visualizations/freeform-analysis-visualizations.html?lang=fr](https://experienceleague.adobe.com/docs/analytics/analyze/analysis-workspace/visualizations/freeform-analysis-visualizations.html?lang=fr)
- [https://experienceleague.adobe.com/docs/analytics/analyze/analysis-workspace/visualizations/t-sync-visualization.html](https://experienceleague.adobe.com/docs/analytics/analyze/analysis-workspace/visualizations/t-sync-visualization.html)

## Entonnoir d’interaction de produit, de l’affichage à l’achat

Il y a de nombreuses façons de résoudre cette question. L’une d’elles consiste à utiliser le type d’interaction du produit et à l’utiliser sur un tableau à structure libre. Une autre méthode consiste à utiliser une **Visualisation Abandons**. Utilisons la dernière comme nous voulons visualiser et analyser en même temps.

Fermez le panneau actuel en cliquant ici :

![demo](./images/pro23.png)

Ajoutez maintenant un nouveau panneau vierge en cliquant sur **+ Ajouter un panneau vierge**.

![demo](./images/pro24.png)

Clic sur la visualisation **Abandon**.

![demo](./images/pro25.png)

Sélectionnez la même période que dans l’exercice précédent.

![demo](./images/prodatef.png)

Vous verrez alors ceci.

![demo](./images/prodatefa.png)

Recherche de la dimension **Type d’événement** sous les composants sur le côté gauche :

![demo](./images/pro26.png)

Cliquez sur la flèche pour ouvrir la dimension :

![demo](./images/pro27.png)

Vous verrez tous les types d’événement disponibles.

![demo](./images/pro28.png)

Sélectionner l’élément **commerce.productViews** et faites-le glisser sur le **Ajouter un point de contact** dans le champ **Visualisation Abandons**.

![demo](./images/pro29.png)

Faites de même avec **commerce.productListAdds** et **commerce.purchases** et les déposer sur le **Ajouter un point de contact** dans le champ **Visualisation Abandons**. Votre visualisation se présente désormais comme suit :

![demo](./images/props1.png)

Vous pouvez faire beaucoup de choses ici. Quelques exemples : comparer au fil du temps, comparer chaque étape par appareil ou comparer par fidélité. Cependant, si nous voulons analyser des éléments intéressants comme les raisons pour lesquelles les clients n’achètent pas après avoir ajouté un article à leur panier, nous pouvons utiliser le meilleur outil dans CJA : cliquez avec le bouton droit de la souris.

Clic droit sur le point de contact **commerce.productListAdds**. Cliquez ensuite sur **Ventiler les abandons à ce point de contact**.

![demo](./images/pro32.png)

Un nouveau tableau à structure libre sera créé pour analyser les actions des personnes qui n’ont pas effectué d’achat.

![demo](./images/pro33.png)

Modifiez la variable **Type d’événement** par **Nom de la page**, dans le nouveau tableau à structure libre, pour voir les pages qu’ils consultent au lieu de la page de confirmation d’achat.

![demo](./images/pro34.png)

## Que font les visiteurs sur le site avant d’accéder à la page Annuler le service ?

Encore une fois, il existe de nombreuses façons d’effectuer cette analyse. Utilisons l’analyse de flux pour commencer la partie découverte.

Fermez le panneau actuel en cliquant ici :

![demo](./images/pro0.png)

Ajoutez maintenant un nouveau panneau vierge en cliquant sur **+ Ajouter un panneau vierge**.

![demo](./images/pro0a.png)

Clic sur la visualisation **Flux**.

![demo](./images/pro35.png)

Vous verrez alors :

![demo](./images/pro351.png)

Sélectionnez la même période que dans l’exercice précédent.

![demo](./images/pro0b.png)

Recherche de la dimension **Nom de la page** sous les composants sur le côté gauche :

![demo](./images/pro36.png)

Cliquez sur la flèche pour ouvrir la dimension :

![demo](./images/pro37.png)

Vous trouverez toutes les pages consultées. Recherchez le nom de la page : **Annuler le service**.
Glisser-déposer **Annuler le service** dans le champ Visualisation du flux au milieu :

![demo](./images/pro38.png)

Vous verrez alors :

![demo](./images/pro40.png)

Analysons maintenant si les clients qui ont visité le **Annuler le service** sur le site web a également appelé callcenter, et quel a été le résultat.

Sous les dimensions, revenez en arrière, puis recherchez **Type d’interaction d’appel**.
Glisser-déposer **Type d’interaction d’appel** pour remplacer la première interaction à droite dans la fonction **Visualisation du flux**.

![demo](./images/pro43.png)

Vous voyez maintenant le ticket d’assistance des clients qui ont appelé le centre d’appel après avoir visité le **Annuler le service** page.

![demo](./images/pro44.png)

Ensuite, sous les dimensions, recherchez **Raisonnement des appels**.  Faites-la glisser et déposez-la pour remplacer la première interaction à droite dans le **Visualisation du flux**.

![demo](./images/pro46.png)

Vous verrez alors :

![demo](./images/flow.png)

Comme vous pouvez le voir, nous avons exécuté une analyse omnicanal à l’aide de la visualisation Flux. Grâce à cela, nous avons trouvé que certains clients qui pensaient annuler leur service, avaient un sentiment positif après avoir appelé le centre d&#39;appel. Avons-nous peut-être changé d&#39;avis avec une promotion ?


## Comment les clients avec un contact Callcenter positif se comportent-ils par rapport aux indicateurs clés de performance principaux ?

Commençons par segmenter les données pour obtenir uniquement les utilisateurs avec **positive** appels . Dans CJA, les segments sont appelés filtres. Accédez aux filtres dans la zone de composant (sur le côté gauche) et cliquez sur **+**.

![demo](./images/pro58.png)

Dans le créateur de filtres, attribuez un nom au filtre.

| Nom | Description |
| ----------------- |-------------| 
| Sentiment d’appel - positif | Sentiment d’appel - positif |

![demo](./images/pro47.png)

Sous les composants (dans le Créateur de filtres), recherchez **Raisonnement des appels** et faites-le glisser dans la définition du Créateur de filtres.

![demo](./images/pro48.png)

Maintenant, sélectionnez **positive** comme valeur du filtre.

![demo](./images/pro49.png)

Modifier la portée à définir **Personne** niveau.

![demo](./images/pro50.png)

Pour terminer, cliquez simplement sur **Enregistrer**.

![demo](./images/pro51.png)

Vous serez alors de retour ici. Si ce n’est pas encore fait, fermez le panneau précédent.

![demo](./images/pro0c.png)

Ajoutez maintenant un nouveau panneau vierge en cliquant sur **+ Ajouter un panneau vierge**.

![demo](./images/pro24c.png)

Sélectionnez la même période que dans l’exercice précédent.

![demo](./images/pro24d.png)

Cliquez sur **Tableau à structure libre**.

![demo](./images/pro52.png)

Déposez maintenant le filtre que vous venez de créer.

![demo](./images/pro53.png)

Temps nécessaire pour ajouter certaines mesures. Commencer par **Consultations produits**. Effectuez un glisser-déposer dans le tableau à structure libre. Vous pouvez également supprimer la variable **Événements** mesure.

![demo](./images/pro54.png)

Faites de même avec **Personnes**,  **Ajouter au panier** et **Achats**. Vous finirez avec une table comme celle-ci.

![demo](./images/pro55.png)

Grâce à la première analyse de flux, une nouvelle question est venue à l&#39;esprit. Nous avons donc décidé de créer ce tableau et de vérifier certains indicateurs de performance clés par rapport à un segment pour répondre à cette question. Comme vous pouvez le constater, le temps d’accès aux informations est beaucoup plus rapide que l’utilisation de SQL ou d’autres solutions de BI.

## Customer Journey Analytics et Analysis Workspace recap

Comme vous l’avez appris dans ce laboratoire, Analysis Workspace assemble les données de tous les canaux afin d’analyser l’ensemble du parcours client. N’oubliez pas également que vous pouvez importer des données dans le même espace de travail qui n’est pas assemblé au parcours.
Il peut être très utile d’importer des données déconnectées dans votre analyse pour donner un contexte au parcours. Certains exemples incluent des données NPS, des enquêtes, des événements Facebook Ads ou des interactions hors ligne (non identifiées).

Étape suivante : [4.6 D’insights à l’action](./ex6.md)

[Retour au flux utilisateur 4](./uc4.md)

[Revenir à tous les modules](./../../overview.md)
