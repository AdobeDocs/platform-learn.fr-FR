---
title: Installer et configurer votre cluster Kafka
description: Installer et configurer votre cluster Kafka
kt: 5342
audience: Data Engineer, Data Architect, Data Analyst
doc-type: tutorial
activity: develop
exl-id: 563cd836-fb71-40dc-b696-ad97f107a3d9
source-git-commit: 3d61d91111d8693ab031fbd7b26706c02818108c
workflow-type: tm+mt
source-wordcount: '770'
ht-degree: 0%

---

# 2.6.2 Installation et configuration de votre cluster Kafka

## Télécharger Apache Kafka

Accédez à [https://kafka.apache.org/downloads](https://kafka.apache.org/downloads) et téléchargez la dernière version publiée. Sélectionnez la dernière version binaire, dans ce cas **3.9.0**. Votre téléchargement va commencer.

![ Kafka ](./images/kafka1.png)

Créez un dossier nommé **Kafka_AEP** sur votre bureau et placez le fichier téléchargé dans ce répertoire.

![ Kafka ](./images/kafka3.png)

Ouvrez une fenêtre **Terminal** en cliquant avec le bouton droit sur votre dossier et en cliquant sur **Nouveau terminal dans le dossier**.

![ Kafka ](./images/kafka4.png)

Exécutez cette commande dans la fenêtre de votre terminal pour décompresser le fichier téléchargé :

`tar -xvf kafka_2.13-3.9.0.tgz`

>[!NOTE]
>
>Vérifiez que la commande ci-dessus correspond à la version du fichier que vous avez téléchargé. Si votre version est plus récente, vous devrez mettre à jour la commande ci-dessus pour qu’elle corresponde à cette version.

![ Kafka ](./images/kafka5.png)

Vous verrez alors ceci :

![ Kafka ](./images/kafka6.png)

Après avoir décompressé ce fichier, vous disposez désormais d’un répertoire comme celui-ci :

![ Kafka ](./images/kafka7.png)

Et dans ce répertoire, vous verrez les sous-répertoires suivants :

![ Kafka ](./images/kafka8.png)

Revenez à la fenêtre Terminal. Saisissez la commande suivante :

`cd kafka_2.13-3.9.0`

>[!NOTE]
>
>Vérifiez que la commande ci-dessus correspond à la version du fichier que vous avez téléchargé. Si votre version est plus récente, vous devrez mettre à jour la commande ci-dessus pour qu’elle corresponde à cette version.

![ Kafka ](./images/kafka9.png)

Saisissez ensuite la `bin/kafka-topics.sh` de commande.

![ Kafka ](./images/kafka10a.png)

Vous devriez alors voir cette réponse. Cela signifie que Kafka est correctement installé et que Java fonctionne correctement. (Rappel : pour que cela fonctionne, Java 23 JDK doit être installé. Vous pouvez voir quelle version Java vous avez installée à l’aide de la commande `java -version`.)

![ Kafka ](./images/kafka10.png)

## Démarrer Kafka

Pour démarrer Kafka, vous devez démarrer Kafka Zookeeper et Kafka, dans cet ordre.

Ouvrez une fenêtre **Terminal** en cliquant avec le bouton droit sur votre dossier **kafka_2.13-3.9.0** et en cliquant sur **Nouveau terminal dans le dossier**.

![ Kafka ](./images/kafka11.png)

Saisissez la commande suivante :

`bin/zookeeper-server-start.sh config/zookeeper.properties`

![ Kafka ](./images/kafka12.png)

Vous verrez alors ceci :

![ Kafka ](./images/kafka13.png)

Gardez cette fenêtre ouverte pendant que vous faites ces exercices !

Ouvrez une autre fenêtre **Terminal** en cliquant avec le bouton droit sur votre dossier **kafka_2.13-3.9.0** et en cliquant sur **Nouveau terminal dans le dossier**.

![ Kafka ](./images/kafka11.png)

Saisissez la commande suivante :

`bin/kafka-server-start.sh config/server.properties`

![ Kafka ](./images/kafka14.png)

Vous verrez alors ceci :

![ Kafka ](./images/kafka15.png)

Gardez cette fenêtre ouverte pendant que vous faites ces exercices !

## Créer une rubrique Kafka

Ouvrez une fenêtre **Terminal** en cliquant avec le bouton droit sur votre dossier **kafka_2.13-3.9.0** et en cliquant sur **Nouveau terminal dans le dossier**.

![ Kafka ](./images/kafka11.png)

Saisissez cette commande pour créer une nouvelle rubrique Kafka nommée **aeptest**. Cette rubrique sera utilisée à des fins de test dans cet exercice.

`bin/kafka-topics.sh --create --topic aeptest --bootstrap-server localhost:9092`

Une confirmation s’affiche ensuite :

![ Kafka ](./images/kafka17a.png)

Saisissez cette commande pour créer une nouvelle rubrique Kafka nommée **aep**. Cette rubrique sera utilisée par le connecteur de récepteur Adobe Experience Platform que vous allez configurer dans les exercices suivants.

`bin/kafka-topics.sh --create --topic aep --bootstrap-server localhost:9092`

Une confirmation similaire s’affiche ensuite :

![ Kafka ](./images/kafka17.png)

## Produire des événements

Revenez à la fenêtre Terminal dans laquelle vous avez créé votre première rubrique Kafka et saisissez la commande suivante :

`bin/kafka-console-producer.sh --broker-list 127.0.0.1:9092 --topic aeptest`

![ Kafka ](./images/kafka18.png)

Tu verras ça. Chaque nouvelle ligne suivie du bouton Entrée entraîne l’envoi d’un nouveau message dans la rubrique **aeptest**.

![ Kafka ](./images/kafka19.png)

Saisissez `Hello AEP` et appuyez sur Entrée. Votre premier événement a maintenant été envoyé à votre instance Kafka locale, dans la rubrique **aeptest**.

![ Kafka ](./images/kafka20.png)

Saisissez `Hello AEP again.` et appuyez sur Entrée.

Saisissez `AEP Data Collection is the best.` et appuyez sur Entrée.

Vous avez maintenant produit 3 événements dans le sujet **aeptest**. Ces événements peuvent désormais être utilisés par une application qui peut avoir besoin de ces données.

![ Kafka ](./images/kafka21.png)

Sur votre clavier, cliquez sur `Control` et `C` en même temps pour fermer votre producteur.

![ Kafka ](./images/kafka22.png)

## Consommer des événements

Dans la même fenêtre Terminal que celle utilisée pour générer les événements, saisissez la commande suivante :

`bin/kafka-console-consumer.sh --bootstrap-server 127.0.0.1:9092 --topic aeptest --from-beginning`

Tous les messages générés dans l’exercice précédent pour le sujet **aeptest** s’affichent alors dans l’écran du client. Voici comment fonctionne Apache Kafka : un producteur crée des événements dans un pipeline et un consommateur consomme ces événements.

![ Kafka ](./images/kafka23.png)

Sur votre clavier, cliquez sur `Control` et `C` en même temps pour fermer votre producteur.

![ Kafka ](./images/kafka24.png)

Dans cet exercice, vous avez parcouru toutes les bases pour configurer un cluster Kafka local, créer un sujet Kafka, produire des événements et consommer des événements.

L’objectif de ce module est de simuler ce qui se passerait si une organisation réelle avait déjà implémenté un cluster Apache Kafka et souhaitait diffuser des données de son cluster Kafka vers Adobe Experience Platform.

Pour faciliter une telle implémentation, un connecteur de récepteur Adobe Experience Platform a été créé, qui peut être implémenté à l’aide de Kafka Connect. Vous trouverez la documentation de ce connecteur de récepteur Adobe Experience Platform ici : [https://github.com/adobe/experience-platform-streaming-connect](https://github.com/adobe/experience-platform-streaming-connect).

Dans les exercices suivants, vous implémenterez tout ce dont vous avez besoin pour utiliser ce connecteur de récepteur Adobe Experience Platform à partir de votre propre cluster Kafka local.

Fermez la fenêtre de votre terminal.

Vous avez terminé cet exercice.

## Étapes suivantes

Accédez à [2.6.3 Configuration du point d’entrée de l’API HTTP dans Adobe Experience Platform](./ex3.md){target="_blank"}

Revenez à [Diffuser des données d’Apache Kafka vers Adobe Experience Platform](./aep-apache-kafka.md){target="_blank"}

Revenir à [Tous les modules](./../../../../overview.md){target="_blank"}
