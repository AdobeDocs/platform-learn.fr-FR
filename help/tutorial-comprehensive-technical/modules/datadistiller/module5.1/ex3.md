---
title: Query Service - Utilisation de Query Service
description: Query Service - Utilisation de Query Service
kt: 5342
audience: Data Engineer, Data Architect, Data Analyst, BI Expert
doc-type: tutorial
exl-id: 31c14a9b-cb62-48ab-815c-caa6e832794f
source-git-commit: d9d9a38c1e160950ae755e352a54667c8a7b30f7
workflow-type: tm+mt
source-wordcount: '657'
ht-degree: 0%

---

# 5.1.3 Utilisation de Query Service

## Objectif

- Recherche et exploration de jeux de données
- Découvrez comment traiter les objets et attributs des modèles de données d’expérience dans vos requêtes

## Contexte

Dans cet article, vous apprendrez à utiliser PSQL pour récupérer des informations sur les jeux de données disponibles, à écrire des requêtes pour Experience Data Model (XDM) et à écrire vos premières requêtes de création de rapports simples à l’aide des jeux de données Query Service et Citi Signal.

## Requêtes de base

Vous y découvrirez les méthodes permettant de récupérer des informations sur les jeux de données disponibles et comment récupérer correctement des données avec une requête d’un jeu de données XDM.

Tous les jeux de données que nous avons explorés via Adobe Experience Platform au début de 1 sont également disponibles pour accès via une interface SQL sous forme de tableaux. Pour répertorier ces tables, vous pouvez utiliser la commande **show tables;** .

Exécutez `show tables;` dans votre **interface de ligne de commande PSQL**. (n’oubliez pas de terminer votre commande par un point-virgule).

Copiez la commande `show tables;` et collez-la à l’invite :

![command-prompt-show-tables.png](./images/commandpromptshowtables.png)

Le résultat suivant s’affiche :

```text
tech-insiders:all=> show tables;
                               name                               |                                                  dataSetId                                                   |                                       dataSet                                        | description |        labels        
------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------+-------------+----------------------
 ajo_bcc_feedback_event_dataset                                   | 672a07cb7728e82aefa1ec56                                                                                     | AJO BCC Feedback Event Dataset                                                       |             | 
 ajo_classification_dataset                                       | 672a07cab55b0d2aef6f9626                                                                                     | AJO Classification Dataset                                                           |             | 
 ajo_consent_service_dataset                                      | 672a07c80fd5fd2aee4155ca                                                                                     | AJO Consent Service Dataset                                                          |             | 'PROFILE'
 ajo_email_tracking_experience_event_dataset                      | 672a07c926d57d2aef020230                                                                                     | AJO Email Tracking Experience Event Dataset                  :
                               name                               |                                                  dataSetId                                                   |                                       dataSet                                        | description |        labels        
------------------------------------------------------------------+--------------------------------------------------------------------------------------------------------------+--------------------------------------------------------------------------------------+-------------+----------------------
 ajo_bcc_feedback_event_dataset                                   | 672a07cb7728e82aefa1ec56                                                                                     | AJO BCC Feedback Event Dataset                                                       |             | 
 ajo_classification_dataset                                       | 672a07cab55b0d2aef6f9626                                                                                     | AJO Classification Dataset                                                           |             | 
 ajo_consent_service_dataset                                      | 672a07c80fd5fd2aee4155ca                                                                                     | AJO Consent Service Dataset                                                          |             | 'PROFILE'
 ajo_email_tracking_experience_event_dataset                      | 672a07c926d57d2aef020230                                                                                     | AJO Email Tracking Experience Event Dataset   
```

Au niveau du deux-points, appuyez sur la barre d’espace pour afficher la page suivante du jeu de résultats ou saisissez `q` pour revenir à l’invite de commande.

Chaque jeu de données dans AEP comporte sa table Query Service correspondante. Vous pouvez trouver le tableau d’un jeu de données via l’interface utilisateur des jeux de données :

![ui-dataset-tablename.png](./images/uidatasettablename.png)

La table `demo_system_event_dataset_for_website_global_v1_1` est la table Query Service qui correspond au jeu de données `Demo System - Event Schema for Website (Global v1.1)`.

Pour interroger certaines informations sur l’emplacement de consultation d’un produit, nous allons sélectionner les informations **geo** .

Copiez la requête ci-dessous et collez-la à l’invite de votre **interface de ligne de commande PSQL** et appuyez sur Entrée :

```sql
select placecontext.geo
from   demo_system_event_dataset_for_website_global_v1_1
where  eventType = 'commerce.productViews'
and placecontext.geo.countryCode <> ''
limit 1;
```

Dans le résultat de votre requête, vous remarquerez que les colonnes du modèle de données d’expérience (XDM) peuvent être des types complexes et pas seulement des types scalaires. Dans la requête ci-dessus, nous souhaitons identifier les emplacements géographiques où un **commerce.productViews** s’est produit. Pour identifier un **commerce.productViews**, nous devons parcourir le modèle XDM à l’aide de **.** (point).

```text
tech-insiders:all=> select placecontext.geo
from   demo_system_event_dataset_for_website_global_v1_1
where  eventType = 'commerce.productViews'
and placecontext.geo.countryCode <> ''
limit 1;
                 geo                  
--------------------------------------
 ("(51.59119,-1.407848)",Charlton,GB)
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
tech-insiders:all=> select placecontext.geo._schema.longitude
      ,placecontext.geo._schema.latitude
      ,placecontext.geo.city
      ,placecontext.geo.countryCode
from   demo_system_event_dataset_for_website_global_v1_1
where  eventType = 'commerce.productViews'
and placecontext.geo.countryCode <> ''
limit 1;
 longitude | latitude |   city   | countrycode 
-----------+----------+----------+-------------
 -1.407848 | 51.59119 | Charlton | GB
(1 row)
```

Ne vous inquiétez pas, il existe un moyen simple d’obtenir le chemin vers une propriété spécifique. Dans la partie suivante, vous allez apprendre comment.

Vous devrez modifier une requête. Ouvrez d’abord un éditeur.

Sous Windows : utilisez **Notepad**

Sous Mac : installez toute application de l’éditeur de texte de votre choix et ouvrez-la.

Copiez l’instruction suivante dans votre éditeur de texte :

```sql
select your_attribute_path_here
from   demo_system_event_dataset_for_website_global_v1_1
where  eventType = 'commerce.productViews'
and placecontext.geo.countryCode <> ''
limit 1;
```

Revenez à l’interface utilisateur de Adobe Experience Platform (doit être ouvert dans votre navigateur) ou accédez à [Adobe Experience Platform](https://experience.adobe.com/platform).

Sélectionnez **Schémas**, entrez `Demo System - Event Schema for Website` dans le champ **search** et cliquez pour ouvrir le schéma `Demo System - Event Schema for Website (Global v1.1) Schema`.

![browse-schema.png](./images/browseschema.png)

Explorez le modèle XDM pour **Demo System - Event Schema for Website (Global v1.1)** en cliquant sur un objet. Développez l’arborescence pour **placecontext**, **geo** et **schema**. Lorsque vous sélectionnez l’attribut réel **longitude**, le chemin d’accès complet s’affiche dans la zone rouge mise en surbrillance. Pour copier le chemin d’accès de l’attribut, cliquez sur l’icône Copier le chemin d’accès .

![explorer-schema-for-path.png](./images/exploreschemaforpath.png)

Passez à votre notepad/crochets et supprimez **your_attribute_path_here** de la première ligne. Positionnez votre curseur après **select** sur la première ligne et collez (CTRL-V).

![explorer-schema-for-path.png](./images/exploreschemaforpath1.png)

Copiez l’instruction modifiée et collez-la à l’invite de votre **interface de ligne de commande PSQL** et appuyez sur Entrée.

Le résultat doit se présenter comme suit :

```text
tech-insiders:all=> select placeContext.geo._schema.longitude
from   demo_system_event_dataset_for_website_global_v1_1
where  eventType = 'commerce.productViews'
and placecontext.geo.countryCode <> ''
limit 1;
 longitude 
-----------
 -1.407848
(1 row)
```

Étape suivante : [5.1.4 Requêtes, requêtes, requêtes... et analyse de perte de clientèle](./ex4.md)

[Revenir au module 5.1](./query-service.md)

[Revenir à tous les modules](../../../overview.md)
