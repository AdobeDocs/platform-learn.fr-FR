---
title: Bootcamp - Customer Journey Analytics - Connectez des jeux de données Adobe Experience Platform en Customer Journey Analytics - Brésil
description: Bootcamp - Customer Journey Analytics - Connectez des jeux de données Adobe Experience Platform en Customer Journey Analytics - Brésil
kt: 5342
audience: Data Engineer, Data Architect, Data Analyst
doc-type: tutorial
activity: develop
source-git-commit: 75a878ba596078e6d013b65062606931402302dd
workflow-type: tm+mt
source-wordcount: '679'
ht-degree: 3%

---

# 4.2 Connexion des jeux de données Adobe Experience Platform dans Customer Journey Analytics

## Objectifs

- Présentation de l’interface utilisateur de connexion aux données
- Intégration des données Adobe Experience Platform dans CJA
- Présentation de l’ID de personne et de la combinaison de données
- Découvrez le concept de diffusion de données en continu dans Customer Journey Analytics

## 4.2.1 Connexion

Accédez à [analytics.adobe.com](https://analytics.adobe.com) pour accéder à Customer Journey Analytics.

Sur la page d’accueil du Customer Journey Analytics, accédez à **Connexions**.

![demo](./images/cja2.png)

Ici, vous pouvez voir toutes les différentes connexions établies entre CJA et Platform. Ces connexions ont le même objectif que les suites de rapports dans Adobe Analytics. Cependant, la collecte des données est totalement différente. Toutes les données proviennent des jeux de données Adobe Experience Platform.

Créons votre première connexion. Cliquez sur **Créer une connexion**.

![demo](./images/cja4.png)

Vous verrez alors le **Créer une connexion** Interface utilisateur.

![demo](./images/cja5.png)

Vous pouvez maintenant donner un nom à votre connexion.

Utilisez cette convention d’affectation des noms : `yourLastName – Omnichannel Data Connection`.

Exemple : `vangeluw - Omnichannel Data Connection`

Vous devez également sélectionner l’environnement de test correct à utiliser. Dans le menu des environnements de test, sélectionnez votre environnement de test, qui doit être `Bootcamp`. Dans cet exemple, l’environnement de test à utiliser est **Bootcamp**. Et vous devez également définir la variable **Nombre moyen d’événements quotidiens** to **moins de 1 million**.

![demo](./images/cjasb.png)

Après avoir sélectionné votre environnement de test, vous pouvez commencer à ajouter des jeux de données à cette connexion. Cliquez sur **Ajout de jeux de données**.

![demo](./images/cjasb1.png)

## 4.2.2 Sélection de jeux de données Adobe Experience Platform

Recherche du jeu de données `Demo System - Event Dataset for Website (Global v1.1)`. Cliquez sur **+** pour ajouter le jeu de données à cette connexion.

![demo](./images/cja7.png)

Désormais, recherchez et cochez les cases correspondant à `Demo System - Event Dataset for Voice Assistants (Global v1.1)` et `Demo System - Event Dataset for Call Center (Global v1.1)`.

Vous aurez alors ceci. Cliquez sur **Suivant**.

![demo](./images/cja9.png)

## 4.2.3 Identifiant de personne et assemblage de données

### ID de personne

L’objectif est maintenant de rejoindre ces jeux de données. Pour chaque jeu de données sélectionné, un champ appelé **ID de personne**. Chaque jeu de données possède son propre champ ID de personne.

![demo](./images/cja11.png)

Comme vous pouvez le constater, l’ID de personne est automatiquement sélectionné pour la plupart d’entre eux. En effet, un identifiant Principal est sélectionné dans chaque schéma de Adobe Experience Platform. Par exemple, voici le schéma pour `Demo System - Event Schema for Call Center (Global v1.1)`, où vous pouvez voir que l’identifiant de Principal est défini sur `phoneNumber`.

![demo](./images/cja13.png)

Cependant, vous pouvez toujours influencer l’identifiant qui sera utilisé pour assembler des jeux de données pour votre connexion. Vous pouvez utiliser n’importe quel identifiant configuré dans le schéma lié à votre jeu de données. Cliquez sur la liste déroulante pour explorer les identifiants disponibles pour chaque jeu de données.

![demo](./images/cja14.png)

Comme mentionné, vous pouvez définir différents ID de personne pour chaque jeu de données. Cela vous permet de rassembler différents jeux de données provenant de plusieurs origines dans CJA. Imaginez que vous introduisiez des NPS ou des données d&#39;enquête qui seraient très intéressantes et utiles pour comprendre le contexte et pourquoi quelque chose s&#39;est passé.

Le nom du champ ID de personne n’est pas important tant que la valeur des champs ID de personne correspond. Disons que nous `email` dans un jeu de données et `emailAddress` dans un autre jeu de données défini comme ID de personne. If `delaigle@adobe.com` est la même valeur pour le champ ID de personne des deux jeux de données. CJA sera en mesure de regrouper les données.

Il existe actuellement d&#39;autres limitations telles que l&#39;assemblage du comportement anonyme à connu. Consultez les questions fréquentes ici : [FAQ](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-overview/cja-faq.html?lang=fr).

### Assemblage des données à l’aide de l’ID de personne

Maintenant que vous comprenez le concept de regroupement de jeux de données à l’aide de l’ID de personne, nous allons choisir `email` comme ID de personne pour chaque jeu de données.

![demo](./images/cja15.png)

Accédez à chaque jeu de données pour mettre à jour l’ID de personne.

![demo](./images/cja12a.png)

Renseignez maintenant le champ ID de personne en choisissant la variable `email` dans la liste déroulante.

![demo](./images/cja17.png)

Une fois que vous avez assemblé les trois jeux de données, nous sommes prêts à continuer.

| jeu de données | ID de personne |
| ----------------- |-------------| 
| Système de démonstration - Jeu de données d’événement pour le site web (Global v1.1) | adresse e-mail |
| Système de démonstration - Jeu de données d’événement pour les assistants vocaux (Global v1.1) | adresse e-mail |
| Système de démonstration - Jeu de données d’événement pour le centre d’appels (Global v1.1) | adresse e-mail |

Vous devez également vous assurer que pour chaque jeu de données, ces options sont activées :

- Importer toutes les nouvelles données
- Renvoi de toutes les données existantes

Cliquez sur **Ajout de jeux de données**.

![demo](./images/cja16.png)

Cliquez sur **Enregistrer** et passez à l’exercice suivant.
Après avoir créé votre **Connexion** il peut s’écouler quelques heures avant que vos données ne soient disponibles dans CJA.

![demo](./images/cja20.png)

Étape suivante : [4.3 Création d’une vue de données](./ex3.md)

[Retour au flux utilisateur 4](./uc4.md)

[Revenir à tous les modules](./../../overview.md)
