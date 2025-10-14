---
title: Service de requête
description: Service de requête
kt: 5342
doc-type: tutorial
exl-id: 881dcff5-3637-4b67-9e61-88690babe83b
source-git-commit: 1e3a8d585503eddad4c642a3b13d2b5f7ddc9943
workflow-type: tm+mt
source-wordcount: '549'
ht-degree: 1%

---

# 2.1 Query Service

Dans ce module, vous obtiendrez un aperçu pratique de Adobe Experience Platform Query Service. Query Service vous permet d’effectuer des requêtes omnicanales sur toutes les données de l’application Adobe Experience Cloud, en joignant et en analysant les données d’Adobe Campaign, d’Analytics, d’Audience Manager, de Target et d’Advertising Cloud ainsi que d’autres données client chargées/insérées dans Adobe Experience Platform.

Query Service est un outil sans serveur. Il prend en charge les requêtes SQL et la connectivité à partir de plusieurs applications clientes via sa compatibilité PostgreSQL.
Nous utiliserons les données qui ont été injectées dans Platform à l’aide des données d’interaction web, des interactions du centre d’appels en combinaison avec les données de fidélité du client chargées dans Platform.

## Objectifs d’apprentissage

- Se familiariser avec l’interface utilisateur de Adobe Experience Platform
- Connexion à Query Service et exécution de vos requêtes SQL
- Explorer des jeux de données dans Adobe Experience Platform
- Connectez Tableau ou Power BI à Adobe Experience Platform Query Service pour créer des visualisations et des rapports

## Conditions préalables

- Il est préférable de posséder des connaissances en SQL, mais cela n’est pas obligatoire
- Accès à Adobe Experience Platform : [https://experience.adobe.com/platform](https://experience.adobe.com/platform)
- Jeux de données (jeu de données utilisé pendant l’atelier, préchargé pour vous)
- PostgreSQL
- Tableau ou Microsoft Power BI Desktop
- **Téléchargez ces ressources** :
   - [JSON - Exemples de données : interactions de site web](./../../../../assets/json/ee.json)
   - [JSON - Exemples de données : interactions du centre d’appels](./../../../../assets/json/callcenter.json)
   - [JSON - Exemples de données : fidélité](./../../../../assets/json/loyalty.json)

>[!NOTE]
>
>N’oubliez pas d’installer, de configurer et d’utiliser l’extension Chrome, comme indiqué dans [Installation de l’extension Chrome pour la documentation Experience League](../../../getting-started/gettingstarted/ex1.md)

## Exercices

[2.1.1 Conditions préalables](./ex1.md)

Vous devrez installer PSQL pour exécuter les requêtes dans cet exercice d’activation. En fonction de votre système d&#39;exploitation, vous devrez installer Microsoft Power BI ou Tableau. Les utilisateurs de Windows peuvent choisir entre Power BI ou Tableau. Les utilisateurs de Mac doivent installer Tableau.

[2.1.2 Prise En Main](./ex2.md)

Dans cet exercice, vous allez explorer l’interface utilisateur de Adobe Experience Platform Query Service, en savoir plus sur les jeux de données, rechercher vos requêtes et enfin configurer une connexion à partir de PSQL.

[2.1.3 Utilisation de Query Service](./ex3.md)

Dans cet exercice, vous découvrirez la syntaxe de base de Query Service et vous pourrez identifier les attributs du schéma XDM dans votre requête.

[2.1.4 Requêtes, requêtes, requêtes... et analyse de perte de clientèle](./ex4.md)

Dans cet exercice, vous allez effectuer des requêtes, vous découvrirez les fonctions définies par Adobe tout en réalisant une analyse de l’attrition. À la fin de cette opération, vous allez écrire une requête pour préparer un jeu de données à utiliser dans Microsoft Power BI.

[2.1.5 Générer un jeu de données à partir d’une requête](./ex5.md)

Dans cet exercice, vous allez générer un jeu de données à partir d’une requête exécutée dans l’exercice précédent et vous utiliserez ce jeu de données dans les exercices suivants.

[2.1.6 Query Service et Power BI](./ex6.md)

Dans cet exercice, vous allez connecter Power BI à Adobe Experience Platform et à Query Service pour effectuer une analyse des interactions Callcenter.

[2.1.7 Query Service et Tableau](./ex7.md)

Dans cet exercice, vous allez connecter Tableau à Adobe Experience Platform et à Query Service pour effectuer une analyse des interactions Callcenter.

[2.1.8 API Query Service](./ex8.md)

Dans cet exercice, vous allez utiliser l’API Query Service pour gérer les modèles et les plannings de requête.

[Résumé et avantages](./summary.md)

Résumé de ce module et aperçu des avantages.

![Insiders de la technologie &#x200B;](./../../../../assets/images/techinsiders.png){width="50px" align="left"}

>[!NOTE]
>
>Merci d’avoir consacré votre temps à apprendre tout ce qu’il y a à savoir sur Adobe Experience Platform et ses applications. Si vous avez des questions, si vous souhaitez partager des commentaires généraux ou si vous avez des suggestions sur le contenu futur, veuillez contacter directement les initiés techniques, en envoyant un e-mail à **techinsiders@adobe.com**.

[Revenir à tous les modules](./../../../../overview.md)
