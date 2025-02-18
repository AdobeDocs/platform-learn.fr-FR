---
title: Présentation d’Apache Kafka
description: Présentation d’Apache Kafka
kt: 5342
doc-type: tutorial
exl-id: e0209ffc-621b-4e8d-aaa7-ac92eef3f86a
source-git-commit: 3d61d91111d8693ab031fbd7b26706c02818108c
workflow-type: tm+mt
source-wordcount: '1012'
ht-degree: 0%

---

# 2.6.1 Présentation d’Apache Kafka

## 2.6.1.1 Introduction

Chaque organisation démarre d’une manière très simple du point de vue des données. L’écosystème de données d’une organisation commence par un système source et une cible. Le système source envoie les données au système cible, et c&#39;est tout. Facile, non ?
Si seulement cela restait aussi simple. Les entreprises dépassent rapidement cette configuration simple et le nombre de systèmes sources et de systèmes cibles augmente rapidement. Toutes ces différentes sources et destinations ont besoin d&#39;échanger des données entre elles, et les choses deviennent rapidement très complexes.
Par exemple, si une organisation possède 4 sources et 6 destinations et que toutes ces applications doivent communiquer entre elles, vous devrez créer 24 intégrations... Chacune de ces intégrations s’accompagne de ses propres difficultés :

- protocol : comment les données sont-elles transportées (TCP, HTTP, REST, FTP, ...)
- Format des données : comment les données sont-elles analysées (binaire, CSV, JSON, Parquet, etc.) ?
- schéma de données et évolution : qu’est-ce que le modèle de données et comment évoluera-t-il ?

En outre, chaque fois que vous connectez un système source à un système de destination, la charge de ces systèmes augmente à partir de cette connexion.

Alors, comment résoudre ça ? C&#39;est là qu&#39;Apache Kafka entre en scène. Apache Kafka permet à une organisation de découpler les flux de données et les systèmes en fournissant un système de messagerie distribué commun à haut débit. Les systèmes Source envoient leurs données à Apache Kafka et les systèmes de destination utilisent les données d’Apache Kafka.

Pensez à tous les types de sources de données que les entreprises doivent gérer :

- événements de site web
- événements d’application mobile
- Événements POS
- Données CRM
- données du centre d’appels
- historique des transactions
- …

Pensez à tous les types de destinations que les entreprises utilisent dans leur écosystème et qui peuvent tous nécessiter des données provenant de ces systèmes sources :

- Intégration des systèmes de gestion des relations clients
- lac de données
- système de messagerie
- audit
- analytics
- …

Apache Kafka a été créé par LinkedIn et est maintenant un projet open source principalement géré par Confluent.
Apache Kafka offre une architecture distribuée et résiliente qui tolère les pannes. Il peut être mis à l&#39;échelle horizontalement à des centaines de courtiers et à des millions de messages par seconde. Il offre des performances élevées avec des latences inférieures à 10 ms, ce qui est idéal pour les cas d’utilisation en temps réel.

Voici quelques exemples de cas d’utilisation :

- Système De Messagerie
- Suivi des activités
- Collecter des mesures à partir de nombreux emplacements différents
- Collecte des journaux d&#39;application
- Traitement des flux (avec l’API de flux Kafka ou Spark)
- Découplage des dépendances système
- Intégration avec Spark, Flink, Storm, Hadoop et de nombreuses autres technologies Big Data.

Par exemple :

- Netflix utilise Kafka pour appliquer des recommandations en temps réel lorsque vous regardez des émissions de télévision
- Uber utilise Kafka pour recueillir des données sur les utilisateurs, les taxis et les trajets en temps réel afin de calculer et de prévoir la demande et de calculer les prix de pointe en temps réel
- LinkedIn utilise Kafka pour prévenir le spam, collecter les interactions utilisateur pour faire de meilleures recommandations de connexion en temps réel

Pour tous ces cas d’utilisation, Kafka n’est utilisé que comme mécanisme de transport. Kafka est vraiment bon pour déplacer les données entre les applications.

## Terminologie 2.6.1.2 Kafka

### Message

Un message est une communication envoyée par un système dans Kafka. Un message contient une payload qui, elle, contient des éléments de données. Par exemple, un événement d’expérience envoyé par un site web dans Adobe Experience Platform est considéré comme un message.

### Rubrique, partitions, décalages

Une rubrique est un flux particulier de données, semblable à un tableau dans une base de données. Vous pouvez avoir autant de rubriques que vous le souhaitez et une rubrique est identifiée par son nom. Les rubriques sont divisées en partitions. Chaque partition est classée et chaque message d’une partition reçoit un identifiant incrémentiel appelé **offset**. Les messages sont stockés dans une rubrique, sur une partition et sont référencés à l’aide d’un décalage. Les messages ne sont conservés que pendant une durée limitée (1 semaine par défaut). Une fois qu’un message est écrit dans une partition, il ne peut plus être modifié.

### Courtiers

Un courtier est semblable à un serveur. Un cluster Kafka est composé de plusieurs courtiers (serveurs). Chaque courtier est identifié par un ID et contient certaines partitions de rubrique.

### Réplication

Kafka est un système distribué. Dans un système distribué, les données sont stockées en toute sécurité et, par conséquent, la réplication est nécessaire. Après tout, lorsqu’un courtier (serveur) tombe en panne, un autre courtier (serveur) doit toujours pouvoir fournir l’accès aux messages initialement stockés sur le courtier qui est tombé en panne. La réplication crée des copies des messages sur plusieurs courtiers pour garantir qu&#39;aucune donnée n&#39;est perdue.

### Producteurs

Comment les données sont-elles envoyées à Kafka ? C&#39;est le rôle d&#39;un producteur. Un producteur se connecte à un système source et extrait les données du système source, puis écrit ces données dans des rubriques sur des partitions. En fonction de la configuration de votre cluster Kafka, les producteurs sauront automatiquement à quel courtier et à quelle partition écrire. Dans un système distribué avec plusieurs courtiers et une stratégie de réplication, un producteur stocke les données de manière aléatoire sur plusieurs courtiers, ce qui signifie qu&#39;il équilibrera automatiquement la charge.

### Clés de message

Les producteurs peuvent choisir d’envoyer une clé avec le message. Une clé peut être n’importe quelle chaîne, n’importe quel nombre, etc. Si aucune clé n&#39;est fournie, un message sera envoyé aléatoirement aux courtiers. Si une clé est envoyée, tous les messages pour cette clé seront toujours envoyés vers la même partition. Une clé de message en tant que telle est utilisée pour classer les messages en fonction d&#39;un champ spécifique.

### Consommateurs

Les consommateurs lisent des données d’une rubrique Apache Kafka, puis partagent ces données avec les systèmes de destination. Les consommateurs savent à quel courtier s&#39;adresser. Les données sont lues par un client dans l’ordre, dans chaque partition. Les consommateurs lisent des données dans des groupes de consommateurs.

### Zookeeper

ZooKeeper est essentiellement un service pour les systèmes distribués offrant un magasin de valeur-clé hiérarchique, qui est utilisé pour fournir un service de configuration distribuée, un service de synchronisation et un registre de nommage pour les systèmes distribués de grande taille. Zookeeper doit être en cours d&#39;exécution avant de pouvoir utiliser Apache Kafka, et Zookeeper est en quelque sorte le maître de cérémonie pour Kafka, gérant les services distribués en arrière-plan pendant que Kafka produit et consomme des événements.

Vous avez terminé cet exercice.

## Étapes suivantes

Accédez à [2.6.2 Installation et configuration de votre cluster Kafka](./ex2.md){target="_blank"}

Revenez à [Diffuser des données d’Apache Kafka vers Adobe Experience Platform](./aep-apache-kafka.md){target="_blank"}

Revenir à [Tous les modules](./../../../../overview.md){target="_blank"}
