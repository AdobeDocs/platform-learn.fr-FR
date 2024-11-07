---
title: Query Service - Utilisation de Query Service
description: Query Service - Utilisation de Query Service
kt: 5342
audience: Data Engineer, Data Architect, Data Analyst, BI Expert
doc-type: tutorial
source-git-commit: 2cdc145d7f3933ec593db4e6f67b60961a674405
workflow-type: tm+mt
source-wordcount: '699'
ht-degree: 0%

---

# 5.1.2 Utilisation de Query Service

## Objectif

- Recherche et exploration de jeux de données
- Découvrez comment traiter les objets et attributs des modèles de données d’expérience dans vos requêtes

## Contexte

Dans cet article, vous apprendrez à utiliser PSQL pour récupérer des informations sur les jeux de données disponibles, à écrire des requêtes pour Experience Data Model (XDM) et à écrire vos premières requêtes de création de rapports simples à l’aide des jeux de données Query Service et Citi Signal.

## 5.1.2.1 Requêtes de base

Vous y découvrirez les méthodes permettant de récupérer des informations sur les jeux de données disponibles et comment récupérer correctement des données avec une requête d’un jeu de données XDM.

Tous les jeux de données que nous avons explorés via Adobe Experience Platform au début de 1 sont également disponibles pour accès via une interface SQL sous forme de tableaux. Pour répertorier ces tables, vous pouvez utiliser la commande **show tables;** .

Exécutez **afficher les tables ;** dans votre **interface de ligne de commande PSQL**. (n’oubliez pas de terminer votre commande par un point-virgule).

Copiez la commande **show tables;** et collez-la à l’invite :

![command-prompt-show-tables.png](./images/command-prompt-show-tables.png)

Le résultat suivant s’affiche :

```text
aepenablementfy21:all=> show tables;
                            name                            |        dataSetId         |                            dataSet                             | description | resolved 
------------------------------------------------------------+--------------------------+----------------------------------------------------------------+-------------+----------
 demo_system_event_dataset_for_call_center_global_v1_1      | 5fd1a9dea30603194baeea43 | Demo System - Event Dataset for Call Center (Global v1.1)      |             | false
 demo_system_event_dataset_for_mobile_app_global_v1_1       | 5fd1a9de250e4f194bec84cd | Demo System - Event Dataset for Mobile App (Global v1.1)       |             | false
 demo_system_event_dataset_for_voice_assistants_global_v1_1 | 5fd1a9de49ee76194b85f73c | Demo System - Event Dataset for Voice Assistants (Global v1.1) |             | false
 demo_system_event_dataset_for_website_global_v1_1          | 5fd1a9dee3224d194cdfe786 | Demo System - Event Dataset for Website (Global v1.1)          |             | false
 demo_system_profile_dataset_for_loyalty_global_v1_1        | 5fd1a9de250e4f194bec84cc | Demo System - Profile Dataset for Loyalty (Global v1.1)        |             | false
 demo_system_profile_dataset_for_ml_predictions_global_v1_1 | 5fd1a9de241f58194b0cb117 | Demo System - Profile Dataset for ML Predictions (Global v1.1) |             | false
 demo_system_profile_dataset_for_mobile_app_global_v1_1     | 5fd1a9deddf353194a2e00b7 | Demo System - Profile Dataset for Mobile App (Global v1.1)     |             | false
 demo_system_profile_dataset_for_website_global_v1_1        | 5fd1a9de42a61c194dd7b810 | Demo System - Profile Dataset for Website (Global v1.1)        |             | false
 journey_step_events                                        | 5fd1a7f30268c5194bbb7e5e | Journey Step Events                                            |             | false
```

Au niveau du deux-points, appuyez sur la barre d’espace pour afficher la page suivante du jeu de résultats ou saisissez `q` pour revenir à l’invite de commande.

Chaque jeu de données de Platform comporte sa table Query Service correspondante. Vous pouvez trouver le tableau d’un jeu de données via l’interface utilisateur des jeux de données :

![ui-dataset-tablename.png](./images/ui-dataset-tablename.png)

La table `demo_system_event_dataset_for_website_global_v1_1` est la table Query Service qui correspond au jeu de données `Demo System - Event Schema for Website (Global v1.1)`.

Pour interroger certaines informations sur l’emplacement de consultation d’un produit, nous allons sélectionner les informations **geo** .

Copiez l’instruction ci-dessous et collez-la à l’invite de votre **interface de ligne de commande PSQL** et appuyez sur Entrée :

```sql
select placecontext.geo
from   demo_system_event_dataset_for_website_global_v1_1
where  eventType = 'commerce.productViews'
and placecontext.geo.countryCode <> ''
limit 1;
```

Dans le résultat de votre requête, vous remarquerez que les colonnes du modèle de données d’expérience (XDM) peuvent être des types complexes et pas seulement des types scalaires. Dans la requête ci-dessus, nous souhaitons identifier les emplacements géographiques où un **commerce.productViews** s’est produit. Pour identifier un **commerce.productViews**, nous devons parcourir le modèle XDM à l’aide de **.** (point).

```text
aepenablementfy21:all=> select placecontext.geo
aepenablementfy21:all-> from   demo_system_event_dataset_for_website_global_v1_1
aepenablementfy21:all-> where  eventType = 'commerce.productViews'
aepenablementfy21:all-> and placecontext.geo.countryCode <> ''
aepenablementfy21:all-> limit 1;
                  geo                   
----------------------------------------
 ("(57.4694803,-3.1269422)",Tullich,GB)
(1 row)
```

Remarquez que le résultat est un objet plat plutôt qu’une seule valeur ? L’objet **placecontext.geo** contient quatre attributs : schéma, pays et ville. Et lorsqu’un objet est déclaré en tant que colonne, il renvoie l’objet entier sous la forme d’une chaîne. Le schéma XDM peut être plus complexe que ce que vous connaissez, mais il est très puissant et a été conçu pour prendre en charge de nombreuses solutions, canaux et cas d’utilisation.

Pour sélectionner les propriétés individuelles d’un objet, vous utilisez le **.** (point).

Copiez l’instruction ci-dessous et collez-la à l’invite de votre **interface de ligne de commande PSQL** :

```sql
select placecontext.geo._schema.longitude
      ,placecontext.geo._schema.latitude
      ,placecontext.geo.city
      ,placecontext.geo.countryCode
from   demo_system_event_dataset_for_website_global_v1_1
where  eventType = 'commerce.productViews'
and placecontext.geo.countryCode <> ''
limit 1;
```

Le résultat de la requête ci-dessus doit ressembler à ceci.
Le résultat est maintenant une définition de valeurs simples :

```text
aepenablementfy21:all=> select placecontext.geo._schema.longitude
aepenablementfy21:all->       ,placecontext.geo._schema.latitude
aepenablementfy21:all->       ,placecontext.geo.city
aepenablementfy21:all->       ,placecontext.geo.countryCode
aepenablementfy21:all-> from   demo_system_event_dataset_for_website_global_v1_1
aepenablementfy21:all-> where  eventType = 'commerce.productViews'
aepenablementfy21:all-> and placecontext.geo.countryCode <> ''
aepenablementfy21:all-> limit 1;
 longitude  |  latitude  |  city   | countrycode 
------------+------------+---------+-------------
 -3.1269422 | 57.4694803 | Tullich | GB
(1 row)
```

Ne vous inquiétez pas, il existe un moyen simple d’obtenir le chemin vers une propriété spécifique. Dans la partie suivante, vous allez apprendre comment.

Vous devrez modifier une requête. Ouvrez d’abord un éditeur.

Sous Windows

Cliquez sur l’icône **search** dans la barre d’outils Windows, tapez **notepad** dans le champ **search**, cliquez sur le résultat **notepad** :

![windows-start-notepad.png](./images/windows-start-notepad.png)

Sur Mac

Installez [Brackets](https://github.com/adobe/brackets/releases/download/release-1.14/Brackets.Release.1.14.dmg) ou utilisez un autre éditeur de texte de votre choix si vous ne l’avez pas installé et suivez les instructions. Après l’installation, recherchez **Brackets** via Mac et ouvrez-le.

Copiez l’instruction suivante dans un bloc-notes ou entre crochets :

```sql
select your_attribute_path_here
from   demo_system_event_dataset_for_website_global_v1_1
where  eventType = 'commerce.productViews'
and placecontext.geo.countryCode <> ''
limit 1;
```

Revenez à l’interface utilisateur de Adobe Experience Platform (doit être ouvert dans votre navigateur) ou accédez à [https://platform.adobe.com](https://platform.adobe.com).

Sélectionnez **Schémas**, saisissez `Demo System - Event Schema for Website (Global v1.1)` dans le champ **search** et sélectionnez `Demo System - Event Schema for Website (Global v1.1) Schema` dans la liste.

![browse-schema.png](./images/browse-schema.png)

Explorez le modèle XDM pour **Demo System - Event Schema for Website (Global v1.1)** en cliquant sur un objet. Développez l’arborescence pour **placecontext**, **geo** et **schema**. Lorsque vous sélectionnez l’attribut réel **longitude**, le chemin d’accès complet s’affiche dans la zone rouge mise en surbrillance. Pour copier le chemin d’accès de l’attribut, cliquez sur l’icône Copier le chemin d’accès .

![explorer-schema-for-path.png](./images/explore-schema-for-path.png)

Passez à votre notepad/crochets et supprimez **your_attribute_path_here** de la première ligne. Positionnez votre curseur après **select** sur la première ligne et collez (CTRL-V).

Copiez l’instruction modifiée depuis le bloc-notes/les crochets et collez-la à l’invite de votre **interface de ligne de commande PSQL** et appuyez sur Entrée.

Le résultat doit se présenter comme suit :

```text
aepenablementfy21:all=> select placeContext.geo._schema.longitude
aepenablementfy21:all-> from   demo_system_event_dataset_for_website_global_v1_1
aepenablementfy21:all-> where  eventType = 'commerce.productViews'
aepenablementfy21:all-> and placecontext.geo.countryCode <> ''
aepenablementfy21:all-> limit 1;
 longitude  
------------
 -3.1269422
```

Étape suivante : [5.1.3 Requêtes, requêtes, requêtes... et analyse de perte de clientèle](./ex3.md)

[Revenir au module 5.1](./query-service.md)

[Revenir à tous les modules](../../../overview.md)
