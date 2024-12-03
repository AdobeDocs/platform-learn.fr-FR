---
title: Service de requête
description: Service de requête
kt: 5342
doc-type: tutorial
exl-id: 6eb65de3-d0e8-49d4-a702-5c9d6a1952b7
source-git-commit: b53ee64ae8438b8f48f842ed1f44ee7ef3e813fc
workflow-type: tm+mt
source-wordcount: '547'
ht-degree: 1%

---

# 5.1 Query Service

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
>N’oubliez pas d’installer, de configurer et d’utiliser l’extension Chrome comme référencé dans [Installation de l’extension Chrome pour la documentation Experience League](../../gettingstarted/gettingstarted/ex1.md)

## Exercices

[5.1.1 Conditions préalables](./ex1.md)

Vous devrez installer PSQL pour exécuter les requêtes dans cet exercice d’activation. Selon votre système d’exploitation, vous devrez installer Microsoft Power BI ou Tableau. Les utilisateurs de Windows peuvent choisir entre Power BI ou Tableau. Les utilisateurs de Mac doivent installer Tableau.

[5.1.2 Prise en main](./ex2.md)

Dans cet exercice, vous allez explorer l’interface utilisateur de Adobe Experience Platform Query Service, en apprendre davantage sur les jeux de données, trouver vos requêtes et enfin configurer une connexion à partir de PSQL.

[5.1.3 Utilisation de Query Service](./ex3.md)

Au cours de cet exercice, vous en apprendrez davantage sur la syntaxe de base de Query Service et vous pourrez identifier les attributs du schéma XDM dans votre requête.

[5.1.4 Requêtes, requêtes, requêtes.. et analyse de perte de clientèle](./ex4.md)

Au cours de cet exercice, vous allez effectuer des requêtes. Vous allez découvrir les fonctions définies par l’Adobe tout en effectuant une analyse de perte de clientèle. À la fin de cette opération, vous allez écrire une requête pour préparer un jeu de données à utiliser dans Microsoft Power BI.

[5.1.5 Génération d’un jeu de données à partir d’une requête](./ex5.md)

Dans cet exercice, vous allez générer un jeu de données à partir d’une requête exécutée dans le précédent et vous utiliserez ce jeu de données dans les exercices suivants.

[5.1.6 Query Service et Power BI](./ex6.md)

Dans cet exercice, vous allez connecter Power BI à Adobe Experience Platform et Query Service pour effectuer l’analyse de l’interaction Callcenter.

[5.1.7 Query Service et Tableau](./ex7.md)

Dans cet exercice, vous allez connecter Tableau à Adobe Experience Platform et Query Service pour effectuer l’analyse de l’interaction Callcenter.

[5.1.8 API Query Service](./ex8.md)

Dans cet exercice, vous utiliserez l’API Query Service pour gérer les modèles de requête et les plannings de requête.

[Résumé et avantages](./summary.md)

Résumé de ce module et aperçu des avantages.

>[!NOTE]
>
>Merci d’investir votre temps à apprendre tout ce qu’il y a à savoir sur Adobe Experience Platform et ses applications. Si vous avez des questions, si vous souhaitez partager les commentaires généraux d’avoir des suggestions sur le contenu futur, contactez directement les initiés de technologie, en envoyant un email à **techinsiders@adobe.com**.

[Revenir à tous les modules](../../../overview.md)
