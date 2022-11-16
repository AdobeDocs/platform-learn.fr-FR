---
title: Présentation d’Apache Kafka
description: Présentation d’Apache Kafka
kt: 5342
audience: Data Engineer, Data Architect, Data Analyst
doc-type: tutorial
activity: develop
exl-id: 7b600c79-03c5-46fc-9ac9-a15599608c35
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '992'
ht-degree: 0%

---

# 15.1 Présentation d’Apache Kafka

## 15.1.1 Introduction

Chaque organisation commence de façon très simple du point de vue des données. L’écosystème de données d’une organisation commence par un système source et une cible. Le système source envoie les données au système cible, et c&#39;est tout. Facile, n&#39;est-ce pas ?
Si seulement elle restait aussi simple. Les entreprises dépassent rapidement cette configuration simple et le nombre de systèmes sources et de systèmes cibles augmente rapidement. Toutes ces sources et destinations différentes doivent échanger des données les unes avec les autres, et les choses deviennent rapidement très complexes.
Par exemple, si une entreprise dispose de 4 sources et de 6 destinations et que toutes ces applications doivent communiquer entre elles, vous devrez créer 24 intégrations.. Chacune de ces intégrations présente ses propres difficultés :

- protocole : Comment les données sont-elles transportées (TCP, HTTP, REST, FTP, etc.)
- format des données : comment les données sont-elles analysées (binaire, CSV, JSON, Parquet, etc.)
- schéma de données et évolution : quel est le modèle de données et comment évoluera-t-il ?

De plus, chaque fois que vous connectez un système source à un système de destination, la charge de ces systèmes augmente à partir de cette connexion.

Alors, comment résoudre ça ? C&#39;est là qu&#39;Apache Kafka entre en scène. Apache Kafka permet à une organisation de découpler les flux de données et les systèmes en fournissant un système de messagerie distribué, à débit élevé et commun. Les systèmes source enverront leurs données à Apache Kafka, et les systèmes de destination utiliseront les données d’Apache Kafka.

Pensez à tous les types de sources de données que les entreprises doivent gérer :

- événements de site web
- événements d’application mobile
- Événements POS
- Données CRM
- données callcenter
- historique des transactions
- ...

Pensez à tous les types de destinations que les entreprises utilisent dans leur écosystème et qui peuvent tous avoir besoin de données de ces systèmes sources :

- CRM
- lac de données
- système de messagerie électronique
- audit
- analytics
- ...

Apache Kafka a été créé par LinkedIn et est maintenant un projet open source principalement géré par Confluent.
Apache Kafka fournit une architecture répartie et résiliente qui est résistante aux défauts. Il peut s&#39;étendre horizontalement jusqu&#39;à 100 s de courtiers et s&#39;adapter à des millions de messages par seconde. Il offre des performances élevées avec des latences inférieures à 10 ms, ce qui est idéal pour les cas d’utilisation en temps réel.

Quelques exemples de cas d’utilisation :

- Système de messagerie
- Suivi des activités
- Collecte de mesures à partir de nombreux emplacements différents
- Collecte des journaux d’application
- Traitement des diffusions (avec l’API Kafka Streams ou Spark)
- Découplage des dépendances système
- Intégration avec Spark, Flink, Storm, Hadoop et de nombreuses autres technologies Big Data.

Par exemple :

- Netflix utilise Kafka pour appliquer des recommandations en temps réel pendant que vous regardez des émissions télévisées.
- Uber utilise Kafka pour rassembler en temps réel les données sur les utilisateurs, les taxis et les trajets afin de calculer et de prévoir la demande et de calculer le prix des augmentations en temps réel.
- linkedIn utilise Kafka pour prévenir les spams, collecter les interactions utilisateur afin de formuler de meilleures recommandations de connexion en temps réel.

Pour tous ces cas d&#39;utilisation, Kafka est utilisé uniquement comme mécanisme de transport. Kafka est vraiment doué pour déplacer les données entre les applications.

## 15.1.2 Terminologie kafka

### Message

Un message est une communication envoyée par un système à Kafka. Un message contient une payload et une payload contient des éléments de données. Par exemple, un événement d’expérience envoyé par un site web à Adobe Experience Platform est considéré comme un message.

### Rubrique, partitions, décalages

Une rubrique est un flux de données particulier, similaire à un tableau dans une base de données. Vous pouvez avoir autant de rubriques que vous le souhaitez et une rubrique est identifiée par son nom. Les rubriques sont fractionnées en partitions. Chaque partition est ordonnée et chaque message d’une partition reçoit un identifiant incrémentiel, appelé **offset**. Les messages sont stockés dans une rubrique, sur une partition et sont référencés à l’aide d’un décalage. Les messages ne sont conservés que pendant une durée limitée (la durée par défaut est d’une semaine). Une fois qu&#39;un message est écrit sur une partition, il ne peut plus être modifié.

### Brodeurs

Un courtier est similaire à un serveur. Un groupe Kafka est composé de plusieurs courtiers (serveurs). Chaque courtier est identifié avec un identifiant et contient certaines partitions de rubrique.

### Réplication

Kafka est un système distribué. L’un des aspects importants d’un système distribué est que les données sont stockées en toute sécurité et qu’une réplication est donc nécessaire. Après tout, lorsqu’un courtier (serveur) tombe en panne, un autre courtier (serveur) doit toujours être en mesure de fournir l’accès aux messages qui étaient initialement stockés sur le courtier qui a chuté. La réplication crée des copies des messages entre plusieurs courtiers afin de garantir qu’aucune donnée n’est perdue.

### Producteurs

Comment les données sont-elles envoyées à Kafka ? C&#39;est le rôle d&#39;un producteur. Un producteur se connecte à un système source et récupère les données du système source, puis écrit ces données sur des rubriques sur des partitions. Selon la configuration de votre grappe Kafka, les producteurs sauront automatiquement à quel courtier et à quelle partition écrire. Dans un système distribué avec plusieurs courtiers et une stratégie de réplication, un producteur stockera les données de manière aléatoire sur plusieurs courtiers, ce qui signifie qu’il effectuera automatiquement l’équilibrage de charge.

### Clés de message

Les producteurs peuvent choisir d’envoyer une clé avec le message. Une clé peut être n’importe quelle chaîne, n’importe quel nombre, etc. Si aucune clé n’est fournie, un message sera envoyé de manière aléatoire aux courtiers. Si une clé est envoyée, tous les messages de cette clé seront toujours envoyés vers la même partition. Une clé de message en tant que telle est utilisée pour classer les messages en fonction d’un champ spécifique.

### Consommateurs

Les clients lisent les données d’une rubrique Apache Kafka, puis partagent ces données avec les systèmes de destination. Les consommateurs savent de quel courtier ils ont besoin pour lire. Les données sont lues par un consommateur dans l&#39;ordre, au sein de chaque partition. Les consommateurs lisent les données dans des groupes de consommateurs.

### Zookeeper

ZooKeeper est essentiellement un service pour les systèmes distribués offrant un magasin de valeurs de clé hiérarchique qui sert à fournir un service de configuration distribué, un service de synchronisation et un registre d’affectation des noms pour les systèmes distribués volumineux. Zookeeper doit être en cours d&#39;exécution avant de pouvoir utiliser Apache Kafka, et Zookeeper est en quelque sorte le maître de la cérémonie pour Kafka, gérant les services distribués sur le serveur principal pendant que Kafka produit et consomme des événements.

Vous avez terminé cet exercice.

Étape suivante : [15.2 Installation et configuration de votre grappe Kafka](./ex2.md)

[Revenir au module 15](./aep-apache-kafka.md)

[Revenir à tous les modules](../../overview.md)
