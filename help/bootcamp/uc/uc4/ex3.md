---
title: Bootcamp - Customer Journey Analytics - Création d’une vue de données
description: 'Customer Journey Analytics : création d’une vue de données'
jira: KT-5342
audience: Data Engineer, Data Architect, Data Analyst
doc-type: tutorial
activity: develop
solution: Customer Journey Analytics
feature-set: Customer Journey Analytics
feature: Data Views
exl-id: e634876c-2b1c-4f7f-99e5-1940f6c87d80
source-git-commit: 3c86f9b19cecf92c9a324fb6fcfcefaebf82177f
workflow-type: tm+mt
source-wordcount: '1627'
ht-degree: 3%

---

# 4.3 Création d’une vue de données

## Objectifs

- Présentation de l’interface utilisateur de la vue de données
- Présentation des paramètres de base de la définition de visite
- Présentation de l’attribution et de la persistance dans une vue de données

## 4.3.1 Affichage des données

Une fois votre connexion établie, vous pouvez maintenant influencer la visualisation. Une différence entre Adobe Analytics et CJA réside dans le fait que CJA a besoin d’une vue de données afin de nettoyer et de préparer les données avant la visualisation.

Une vue de données est similaire au concept de suites de rapports virtuelles dans Adobe Analytics, où vous définissez des définitions de visite basées sur le contexte, le filtrage, ainsi que la manière dont les composants sont appelés.

Vous aurez besoin d’au moins une vue de données par connexion. Cependant, dans certains cas d’utilisation, il est conseillé d’avoir plusieurs vues de données pour la même connexion, dans le but de fournir des informations différentes à différentes équipes.
Si vous souhaitez que votre entreprise soit axée sur les données, vous devez adapter la manière dont les données sont vues dans chaque équipe. Quelques exemples :

- Mesures UX uniquement pour l’équipe de conception de l’expérience utilisateur
- Utilisez les mêmes noms pour les indicateurs de performance clés et les mesures pour les Google Analytics que pour les Customer Journey Analytics afin que l’équipe d’analyse numérique ne parle qu’une seule langue.
- Vue des données filtrée afin d’afficher, par exemple, les données d’un seul marché ou d’une seule marque, ou uniquement pour les périphériques mobiles.

Sur l’écran **Connexions**, cochez la case en regard de la connexion que vous venez de créer. Cliquez sur **Créer une vue de données**.

![demo](./images/exta.png)

Vous serez redirigé vers le workflow **Créer une vue de données**.

![demo](./images/0-v2.png)

## 4.3.2 Définition de la vue des données

Vous pouvez maintenant configurer les définitions de base de votre vue de données.

![demo](./images/0-v2.png)

La **connexion** que vous avez créée dans l’exercice précédent est déjà sélectionnée. Votre connexion est nommée `yourLastName – Omnichannel Data Connection`.

![demo](./images/ext5.png)

Attribuez ensuite un nom à votre vue de données en suivant cette convention d’affectation des noms : `yourLastName – Omnichannel Data View`.

Saisissez la même valeur pour la description : `yourLastName – Omnichannel Data View`.

| Nom | Description |
| ----------------- |-------------| 
| `yourLastName – Omnichannel Data View` | `yourLastName – Omnichannel Data View` |

![demo](./images/1-v2.png)

Pour le **Fuseau horaire**, sélectionnez le fuseau horaire **Berlin, Stockholm, Rome, Berne, Bruxelles, Vienne, Amsterdam GMT+01:00**. C&#39;est un cadre vraiment intéressant car certaines entreprises opèrent dans différents pays et régions. Allouer le bon fuseau horaire pour chaque pays évitera les erreurs de données typiques, comme par exemple croire qu&#39;au Pérou, la majorité des gens achètent des T-shirts à 4 heures du matin.

![demo](./images/ext7.png)

Vous pouvez également modifier le nom des mesures principales (Personne, Session et Événement). Cela n’est pas obligatoire, mais certains clients aiment utiliser Personnes, Visites et Accès au lieu de Personne, Session et Événements (convention de dénomination par défaut de Customer Journey Analytics).

Les paramètres suivants doivent maintenant être configurés :

![demo](./images/1-v2.png)

Cliquez sur **Enregistrer et continuer**.

![demo](./images/12-v2.png)

## 4.3.3 Composants de la vue de données

Dans cet exercice, vous allez configurer les composants dont vous avez besoin pour analyser les données et les visualiser à l’aide d’Analysis Workspace. Dans cette interface utilisateur, il existe trois zones principales :

- Côté gauche : composants disponibles des jeux de données sélectionnés
- Milieu : ajout de composants à la vue de données
- Côté droit : paramètres des composants

![demo](./images/2-v2.png)

>[!IMPORTANT]
>
>Si vous ne trouvez pas de mesure ou de dimension spécifique, vérifiez si le champ `Contains data` est supprimé de votre vue de données. Dans le cas contraire, supprimez ce champ.
>
>![demo](./images/2-v2a.png)

Vous devez maintenant faire glisser les composants dont vous avez besoin pour l’analyse vers les **Composants ajoutés**. Pour ce faire, vous devez sélectionner les composants dans le menu de gauche et les faire glisser sur la zone de travail au milieu.

Commençons par le premier composant : **Name (web.webPageDetails.name)**. Recherchez ce composant, puis faites-le glisser sur la zone de travail.

![demo](./images/3-v2.png)

Ce composant est le nom de page, car vous pouvez dériver de la lecture du champ de schéma `(web.webPageDetails.name)`.

Cependant, l’utilisation de **Name** comme nom n’est pas la meilleure convention d’affectation des noms pour un utilisateur chargé de la conception de entreprise afin de comprendre rapidement cette dimension.

Modifions le nom en **Nom de page**. Cliquez sur le composant et renommez-le dans la zone **Paramètres du composant**.

![demo](./images/3-0-v2.png)

Les **paramètres de persistance** comptent vraiment. Le concept d’evars et de prop n’existe pas dans CJA, mais les paramètres de persistance rendent possible un comportement similaire.

![demo](./images/3-0-v21.png)

Si vous ne modifiez pas ces paramètres, CJA interprète la dimension comme **Prop** (niveau accès). Nous pouvons également modifier la Persistance pour que la dimension soit **eVar** (conserver la valeur sur l’ensemble du parcours).

Si vous ne connaissez pas les eVars et les props, vous pouvez [en savoir plus à leur sujet dans la documentation](https://experienceleague.adobe.com/docs/analytics/landing/an-key-concepts.html).

Laissez le Nom de page comme Prop. Par conséquent, vous n’avez pas besoin de modifier les **paramètres de persistance**.

| Nom du composant à rechercher | Nouveau nom | Paramètres de persistance |
| ----------------- |-------------| --------------------| 
| Nom (web.webPageDetails.name) | Nom de la page |          |

Ensuite, sélectionnez la dimension **phoneNumber** et déposez-la sur la zone de travail. Le nouveau nom doit être **Numéro de téléphone**.

![demo](./images/3-1-v2.png)

Enfin, changeons les paramètres de persistance, car le numéro de mobile doit persister au niveau de l’utilisateur.

Pour modifier la Persistance, faites défiler l’écran vers le bas dans le menu de droite et ouvrez l’onglet **Persistance** :

![demo](./images/5-v2.png)

Cochez la case pour modifier les paramètres de persistance. Sélectionnez **Le plus récent** et la portée **Personne (fenêtre de création de rapports)**, car nous nous soucions uniquement du dernier numéro de mobile de cette personne. Si le client ne remplit pas le mobile lors de futures visites, cette valeur sera toujours renseignée.

![demo](./images/6-v2.png)

| Nom du composant à rechercher | Nouveau nom | Paramètres de persistance |
| ----------------- |-------------| --------------------| 
| phoneNumber | Numéro de téléphone | Le plus récent, Personne (fenêtre de reporting) |

Le composant suivant est `web.webPageDetails.pageViews.value`.

Dans le menu de gauche, recherchez `web.webPageDetails.pageViews.value`. Faites glisser cette mesure et déposez-la sur la zone de travail.

Modifiez le nom en **Pages vues** sous les **paramètres de composant**.

| Nom du composant à rechercher | Nouveau nom | Paramètres d’attribution |
| ----------------- |-------------| --------------------| 
| web.webPageDetails.pageViews.value | Pages vues |         |

![demo](./images/7-v2.png)

Pour les paramètres d’attribution, laissez ce champ vide.

Remarque : les paramètres de persistance des mesures peuvent également être modifiés dans Analysis Workspace. Dans certains cas, vous pouvez choisir de le définir ici pour éviter que les utilisateurs professionnels n’aient à penser quel est le meilleur modèle de persistance.

Vous devrez ensuite configurer de nombreuses Dimensions et mesures, comme indiqué dans le tableau ci-dessous.

### DIMENSIONS


| Nom du composant à rechercher | Nouveau nom | Paramètres de persistance |
| ----------------- |-------------| --------------------| 
| brandName | Nom de la marque | Session la plus récente |
| callentiment | Raisonnement des appels |          |
| ID d’appel | Type d’interaction d’appel |          |
| callTopic | Rubrique d’appel | Session la plus récente |
| ecid | ECID | Le plus récent, Personne (fenêtre de reporting) |
| adresse e-mail | Email ID | Le plus récent, Personne (fenêtre de reporting) |
| Type de paiement | Type de paiement |          |
| Méthode d’ajout du produit | Méthode d’ajout du produit | Session la plus récente |
| Type d’événement | Type d’événement |         |
| Nom (productListItems.name) | Nom du produit |         |
| SKU | SKU (session) | Session la plus récente |
| Identifiant de transaction | Identifiant de transaction |         |
| URL (web.webPageDetails.URL) | URL |         |
| Agent utilisateur | Agent utilisateur | Session la plus récente |
| level | Niveau de fidélité |          |
| points | Valeur de durée de vie du client |          |

### MESURES

| Nom du composant à rechercher | Nouveau nom | Paramètres d’attribution |
| ----------------- |-------------| --------------------| 
| Quantité | Quantité |          |
| commerce.order.priceTotal | Recettes |         |

Votre configuration doit alors se présenter comme suit :

![demo](./images/11-v2.png)

N’oubliez pas de **Enregistrer** votre vue de données. Cliquez maintenant sur **Enregistrer**.

![demo](./images/12-v2s.png)

## 4.3.4 Mesures calculées

Bien que nous ayons organisé tous les composants dans la vue de données, vous devez tout de même en adapter certains, afin que les utilisateurs professionnels soient prêts à commencer leur analyse.

Si vous vous souvenez, nous n’avons pas incorporé de mesures spécifiques telles que Ajout au panier, Consultation produit ou Achats dans la Vue des données.
Cependant, nous avons une dimension appelée : **Type d’événement**. Dériver ces types d’interactions en créant 3 mesures calculées.

Commençons par la première mesure : **Consultations produits**.

Sur le côté gauche, recherchez **Type d’événement** et sélectionnez la dimension. Faites ensuite glisser et déposez-le dans le canevas **Composants inclus**.

![demo](./images/calcmetr1.png)

Cliquez pour sélectionner la nouvelle mesure **Type d’événement**.

![demo](./images/calcmetr2.png)

Remplacez maintenant le nom et la description du composant par les valeurs suivantes :

| Nom du composant | Description du composant |
| ----------------- |-------------| 
| Consultations produits | Consultations produits |

![demo](./images/calcmetr3.png)

Désormais, comptabilise uniquement les événements **Consultations produits**. Pour ce faire, faites défiler l’écran vers le bas jusqu’à ce que vous voyiez **Inclure les valeurs d’exclusion**. **&#x200B;**&#x200B;Veillez à activer l’option **Définir les valeurs d’inclusion/exclusion**.

![demo](./images/calcmetr4.png)

Puisque nous ne voulons compter que **Consultations de produit**, spécifiez **commerce.productViews** sous les critères.

![demo](./images/calcmetr5.png)

Votre mesure calculée est maintenant prête !

Répétez ensuite le même processus pour les événements **Ajouter au panier** et **Achat** .

### Ajouter au panier

Faites d’abord glisser et déposez la même dimension **Type d’événement**.

![demo](./images/calcmetr1.png)

Une alerte contextuelle d’un champ dupliqué s’affiche, car nous utilisons la même variable. Veuillez cliquer sur **Ajouter tout** :

![demo](./images/calcmetr6.png)

Suivez maintenant la même procédure que pour la mesure Consultations produits :
- Modifiez d’abord le nom et la description.
- Ajoutez enfin **commerce.productListAdds** comme critère pour ne comptabiliser que l’ajout au panier.

| Nom | Description | Critères |
| ----------------- |-------------| -------------|
| Ajouter au panier | Ajouter au panier | commerce.productListAdds |

![demo](./images/calcmetr6a.png)

### Achats

Faites d’abord glisser et déposez la même dimension **Type d’événement** que pour les deux mesures précédentes.

![demo](./images/calcmetr1.png)

Une alerte contextuelle d’un champ dupliqué s’affiche, car nous utilisons la même variable. Veuillez cliquer sur **Ajouter tout** :

![demo](./images/calcmetr7.png)

Suivez maintenant la même procédure que pour les mesures Consultations produits et Ajouter au panier :
- Modifiez d’abord le nom et la description.
- Ajoutez enfin **commerce.purchase** comme critère pour ne comptabiliser que les achats

| Nom | Description | Critères |
| ----------------- |-------------| -------------|
| Achats | Achats | commerce.purchases |

![demo](./images/calcmetr7a.png)

Votre configuration finale doit alors ressembler à celle-ci. Cliquez sur **Enregistrer et continuer**.

![demo](./images/calcmetr8.png)

## 4.3.5 Paramètres de vue des données

Vous devez être redirigé vers cet écran :

![demo](./images/8-v2.png)

Dans cet onglet, vous pouvez modifier certains paramètres importants afin de modifier le mode de traitement des données. Commençons par définir le **délai d’expiration de la session** sur 30 minutes. Grâce à l’horodatage de chaque événement d’expérience, vous pouvez étendre le concept de session sur tous les canaux. Par exemple, que se passe-t-il si un client appelle le centre d’appel après avoir visité le site web ? L’utilisation de délais d’expiration de session personnalisés offre une grande flexibilité pour décider ce qu’est une session et comment cette session fusionnera les données.

![demo](./images/ext8.png)

Dans cet onglet, vous pouvez modifier d’autres éléments tels que le filtrage des données à l’aide d’un segment/filtre. Vous n&#39;aurez pas besoin de le faire dans cet exercice.

![demo](./images/10-v2.png)

Une fois que vous avez terminé, cliquez sur **Enregistrer et terminer**.

![demo](./images/13-v2.png)

>[!NOTE]
>
>Vous pouvez revenir à cette vue de données par la suite et modifier les paramètres et les composants à tout moment. Les modifications affectent la manière dont les données historiques sont affichées.

Vous pouvez maintenant poursuivre la partie Visualisation et analyse !

Étape suivante : [4.4 Data Preparation in Customer Journey Analytics](./ex4.md)

[Retour au flux utilisateur 4](./uc4.md)

[Revenir à tous les modules](./../../overview.md)
