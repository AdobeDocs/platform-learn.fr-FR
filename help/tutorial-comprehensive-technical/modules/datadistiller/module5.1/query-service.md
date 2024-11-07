---
title: Query Service
description: Query Service
kt: 5342
doc-type: tutorial
source-git-commit: 7d2f5f842559b2d6d9f115f3993268a4b36a0fe0
workflow-type: tm+mt
source-wordcount: '556'
ht-degree: 1%

---

# 5.1 Query Service

**Auteurs : [Marc Meewis](https://www.linkedin.com/in/marcmeewis/), [Wouter Van Geluwe](https://www.linkedin.com/in/woutervangeluwe/)**

Dans ce module, vous obtiendrez un aperçu pratique de Adobe Experience Platform Query Service. Query Service vous permet d’exécuter des requêtes omnicanal sur toutes les données d’application Adobe Experience Cloud, de joindre et d’analyser des données dans Adobe Campaign, Analytics, Audience Manager, Target et Advertising Cloud, ainsi que d’autres données client chargées/insérées dans Adobe Experience Platform.

Query Service est un outil sans serveur. Il prend en charge les requêtes SQL et la connectivité de plusieurs applications clientes via sa compatibilité PostgreSQL.
Nous utiliserons les données qui ont été injectées dans la plateforme à l’aide des données d’interaction web, des interactions avec le centre d’appels, en association avec les données de fidélité de la clientèle transférées dans la plateforme.

## Objectifs d’apprentissage

- Familiarisez-vous avec l’interface utilisateur Adobe Experience Platform
- Connexion à Query Service et exécution de vos requêtes SQL
- Exploration des jeux de données dans Adobe Experience Platform
- Connexion de Tableau ou de Power BI au service de requête Adobe Experience Platform pour créer des visualisations et des rapports

## Conditions préalables

- Une certaine familiarité avec SQL est préférable, mais elle n’est pas requise.
- Accès à Adobe Experience Platform : [https://experience.adobe.com/platform](https://experience.adobe.com/platform)
- Jeux de données (jeu de données utilisé pendant le laboratoire, préchargé pour vous)
- PostgreSQL
- Tableau ou Microsoft Power BI Desktop
- **Téléchargez ces ressources** :
   - [JSON - Exemple de données : interactions avec des sites web](./../../../assets/json/ee.json)
   - [JSON - Exemples de données : interactions avec le centre d’appels](./../../../assets/json/callcenter.json)
   - [JSON - Exemple de données : Loyalty](./../../../assets/json/loyalty.json)

>[!NOTE]
>
>N’oubliez pas d’installer, de configurer et d’utiliser l’extension Chrome comme référencé dans [0.1 - Installation de l’extension Chrome pour la documentation Experience League](../../gettingstarted/gettingstarted/ex1.md)

## Exercices

[5.1.0 Conditions préalables](./ex0.md)

Vous devrez installer PSQL pour exécuter les requêtes dans cet exercice d’activation. Selon votre système d’exploitation, vous devrez installer Microsoft Power BI ou Tableau. Les utilisateurs de Windows peuvent choisir entre Power BI ou Tableau. Les utilisateurs de Mac doivent installer Tableau.

[5.1.1 Prise en main](./ex1.md)

Dans cet exercice, vous allez explorer l’interface utilisateur de Adobe Experience Platform Query Service, en apprendre davantage sur les jeux de données, trouver vos requêtes et enfin configurer une connexion à partir de PSQL.

[5.1.2 Utilisation de Query Service](./ex2.md)

Au cours de cet exercice, vous en apprendrez davantage sur la syntaxe de base de Query Service et vous pourrez identifier les attributs du schéma XDM dans votre requête.

[5.1.3 Requêtes, requêtes, requêtes.. et analyse de perte de clientèle](./ex3.md)

Au cours de cet exercice, vous allez effectuer des requêtes. Vous allez découvrir les fonctions définies par l’Adobe tout en effectuant une analyse de perte de clientèle. À la fin de cette opération, vous allez écrire une requête pour préparer un jeu de données à utiliser dans Microsoft Power BI.

[5.1.4 Génération d’un jeu de données à partir d’une requête](./ex4.md)

Dans cet exercice, vous allez générer un jeu de données à partir d’une requête exécutée dans le précédent et vous utiliserez ce jeu de données dans les exercices suivants.

[5.1.5 Query Service et Power BI](./ex5.md)

Dans cet exercice, vous allez connecter Power BI à Adobe Experience Platform et Query Service pour effectuer l’analyse de l’interaction Callcenter.

[5.1.6 Query Service et Tableau](./ex6.md)

Dans cet exercice, vous allez connecter Tableau à Adobe Experience Platform et Query Service pour effectuer l’analyse de l’interaction Callcenter.

[5.1.7 API Query Service](./ex7.md)

Dans cet exercice, vous utiliserez l’API Query Service pour gérer les modèles de requête et les plannings de requête.

[Résumé et avantages](./summary.md)

Résumé de ce module et aperçu des avantages.

>[!NOTE]
>
>Merci d’investir votre temps à apprendre tout ce qu’il y a à savoir sur Adobe Experience Platform et ses applications. Si vous avez des questions, si vous souhaitez partager les commentaires généraux d’avoir des suggestions sur le contenu futur, contactez directement les initiés de technologie, en envoyant un email à **techinsiders@adobe.com**.

[Revenir à tous les modules](../../../overview.md)
