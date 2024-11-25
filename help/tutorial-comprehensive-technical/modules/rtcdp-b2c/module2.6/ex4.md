---
title: Installation et configuration de Kafka Connect et du connecteur Adobe Experience Platform Sink
description: Installation et configuration de Kafka Connect et du connecteur Adobe Experience Platform Sink
kt: 5342
doc-type: tutorial
exl-id: 93ded4f9-0179-4186-9601-52f479350075
source-git-commit: 6485bfa1c75c43bb569f77c478a273ace24a61d4
workflow-type: tm+mt
source-wordcount: '1071'
ht-degree: 0%

---

# 2.6.4 Installation et configuration de Kafka Connect et Adobe Experience Platform Sink Connector

## Téléchargement du connecteur Adobe Experience Platform Sink

Accédez à [https://github.com/adobe/experience-platform-streaming-connect/releases](https://github.com/adobe/experience-platform-streaming-connect/releases) et téléchargez la dernière version officielle du connecteur Adobe Experience Platform Sink.

![Kafka](./images/kc1.png)

Téléchargez le fichier **streaming-connect-sink-0.0.27-java-11.jar**.

![Kafka](./images/kc1a.png)

Placez le fichier de téléchargement, **streaming-connect-sink-0.0.27-java-11.jar**, sur votre bureau.

![Kafka](./images/kc2.png)

## Configuration de Kafka Connect

Accédez au dossier de votre bureau nommé **Kafka_AEP** et accédez au dossier `kafka_2.13-3.9.0/config`.
Dans ce dossier, ouvrez le fichier **connect-distribué.properties** à l’aide de n’importe quel éditeur de texte.

![Kafka](./images/kc3a.png)

Dans votre éditeur de texte, accédez aux lignes 34 et 35 et assurez-vous de définir les champs `key.converter.schemas.enable` et `value.converter.schemas.enable` sur `false`.

```json
key.converter.schemas.enable=false
value.converter.schemas.enable=false
```

Enregistrez vos modifications dans ce fichier.

![Kafka](./images/kc3.png)

Ensuite, revenez au dossier `kafka_2.13-3.1.0` et créez manuellement un nouveau dossier et nommez-le `connectors`.

![Kafka](./images/kc4.png)

Cliquez avec le bouton droit sur le nouveau dossier et cliquez sur **Nouveau terminal dans le dossier**.

![Kafka](./images/kc5.png)

Vous verrez alors ceci. Saisissez la commande `pwd` pour récupérer le chemin d’accès complet à ce dossier. Sélectionnez le chemin complet et copiez-le dans le presse-papiers.

![Kafka](./images/kc6.png)

Revenez à votre éditeur de texte, au fichier **connect-Distributed.properties** et faites défiler l’écran jusqu’à la dernière ligne (ligne 89 dans la capture d’écran). Vous devez annuler la mise en commentaire de la ligne (supprimer `#`) commençant par `# plugin.path=` et vous devez coller le chemin d’accès complet au dossier nommé `connectors`. Le résultat doit ressembler à ceci :

`plugin.path=/Users/woutervangeluwe/Desktop/Kafka_AEP/kafka_2.13-3.9.0/connectors`

Enregistrez vos modifications dans le fichier **connect-distribué.properties** et fermez votre éditeur de texte.

![Kafka](./images/kc7.png)

Copiez ensuite la dernière version officielle du connecteur Adobe Experience Platform Sink que vous avez téléchargé dans le dossier nommé `connectors`. Le fichier que vous avez téléchargé précédemment est nommé **streaming-connect-sink-0.0.27-java-11.jar**. Vous pouvez simplement le déplacer dans le dossier `connectors`.

![Kafka](./images/kc8.png)

Ouvrez ensuite une nouvelle fenêtre Terminal au niveau du dossier **kafka_2.13-3.9.0** . Cliquez avec le bouton droit de la souris sur ce dossier et cliquez sur **New Terminal at Folder**.

Dans la fenêtre Terminal, collez la commande suivante : `bin/connect-distributed.sh config/connect-distributed.properties` et cliquez sur **Entrée**. Cette commande démarre Kafka Connect et charge la bibliothèque de Adobe Experience Platform Sink Connector.

![Kafka](./images/kc9.png)

Au bout de quelques secondes, vous verrez quelque chose comme ceci :

![Kafka](./images/kc10.png)

## Création de votre connecteur Adobe Experience Platform Sink à l’aide de Postman

Vous pouvez désormais interagir avec Kafka Connect à l’aide de Postman. Pour ce faire, téléchargez [cette collection Postman](./../../../assets/postman/postman_kafka.zip) et décompressez-la sur votre ordinateur local sur le bureau. Vous aurez alors un fichier appelé `Kafka_AEP.postman_collection.json`.

![Kafka](./images/kc11a.png)

Vous devez importer ce fichier dans Postman. Pour ce faire, ouvrez Postman, cliquez sur **Importer**, faites glisser et déposez le fichier `Kafka_AEP.postman_collection.json` dans la fenêtre contextuelle, puis cliquez sur **Importer**.

![Kafka](./images/kc11b.png)

Vous trouverez ensuite cette collection dans le menu de gauche de Postman. Cliquez sur la première requête, **Connecteurs Kafka Connect disponibles** pour l’ouvrir.

![Kafka](./images/kc11c.png)

Vous verrez alors ceci. Cliquez sur le bouton bleu **Send** , après lequel vous devriez voir une réponse vide `[]`. La réponse vide est due au fait qu’aucun connecteur Kafka Connect n’est actuellement défini.

![Kafka](./images/kc11.png)

Pour créer un connecteur, cliquez pour ouvrir la seconde requête dans la collection Kafka, **POST Create AEP Sink Connector** et accédez à **Body**. Vous verrez alors ceci. Sur la ligne 11, où il est indiqué **&quot;aep.endpoint&quot;: &quot;&quot;**, vous devez coller dans l’URL du point de terminaison de diffusion en flux continu de l’API HTTP que vous avez reçue à la fin de l’un des exercices précédents. L’URL du point d’entrée de diffusion en continu de l’API HTTP ressemble à ceci : `https://dcs.adobedc.net/collection/63751d0f299eeb7aa48a2f22acb284ed64de575f8640986d8e5a935741be9067`.

![Kafka](./images/kc12a.png)

Après l’avoir collé, le corps de votre requête doit ressembler à ceci. Cliquez sur le bouton bleu **Send** pour créer votre connecteur. Vous obtiendrez une réponse immédiate à la création de votre connecteur.

![Kafka](./images/kc12.png)

Cliquez sur la première requête, **Connecteurs Kafka Connect disponibles** pour l’ouvrir à nouveau et cliquez de nouveau sur le bouton bleu **Envoyer** . vous verrez maintenant qu&#39;il existe un connecteur Kafka Connect.

![Kafka](./images/kc13.png)

Ouvrez ensuite la troisième requête dans la collection Kafka, **GET Check Kafka Connect Connector Status**. Cliquez sur le bouton bleu **Envoyer** . Une réponse similaire à celle ci-dessous s’affiche, indiquant que le connecteur est en cours d’exécution.

![Kafka](./images/kc14.png)

## Génération d’un événement d’expérience

Ouvrez une nouvelle fenêtre **Terminal** en cliquant avec le bouton droit de la souris sur votre dossier **kafka_2.13-3.9.0** et en cliquant sur **Nouveau terminal dans le dossier**.

![Kafka](./images/kafka11.png)

Saisissez la commande suivante :

`bin/kafka-console-producer.sh --broker-list 127.0.0.1:9092 --topic aep`

Vous verrez alors ceci. Chaque nouvelle ligne suivie d’un bouton Entrée entraîne l’envoi d’un nouveau message dans la rubrique **aep**.

![Kafka](./images/kc16.png)

Vous pouvez maintenant envoyer un message qui sera consommé par Adobe Experience Platform Sink Connector et ingéré dans Adobe Experience Platform en temps réel.

Prenez l’exemple de payload d’événement d’expérience ci-dessous et copiez-le dans un éditeur de texte.

```json
{
  "header": {
    "datasetId": "61fe23fd242870194a6d779c",
    "imsOrgId": "--aepImsOrgID--",
    "source": {
      "name": "Launch"
    },
    "schemaRef": {
      "id": "https://ns.adobe.com/experienceplatform/schemas/b0190276c6e1e1e99cf56c99f4c07a6e517bf02091dcec90",
      "contentType": "application/vnd.adobe.xed-full+json;version=1"
    }
  },
  "body": {
    "xdmMeta": {
      "schemaRef": {
        "id": "https://ns.adobe.com/experienceplatform/schemas/b0190276c6e1e1e99cf56c99f4c07a6e517bf02091dcec90",
        "contentType": "application/vnd.adobe.xed-full+json;version=1"
      }
    },
    "xdmEntity": {
      "eventType": "callCenterInteractionKafka",
      "_id": "",
      "timestamp": "2024-11-25T09:54:12.232Z",
      "_experienceplatform": {
        "identification": {
          "core": {
            "phoneNumber": ""
          }
        },
        "interactionDetails": {
          "core": {
            "callCenterAgent": {
              "callID": "Support Contact - 3767767",
              "callTopic": "contract",
              "callFeeling": "negative"
            }
          }
        }
      }
    }
  }
}
```

Vous verrez alors ceci. Vous devez mettre à jour manuellement 2 champs :

- **_id** : définissez-le sur un identifiant aléatoire, par exemple `--aepUserLdap--1234`
- **timestamp** : mettez à jour l’horodatage vers la date et l’heure actuelles
- **phoneNumber** : saisissez le numéro de téléphone du compte créé précédemment sur le site web de démonstration. Vous pouvez le trouver dans le panneau Visionneuse de profils sous **Identités**.

Vous devez également vérifier et peut-être mettre à jour ces champs :

- **datasetId** : vous devez copier l’identifiant du jeu de données pour le système de démonstration du jeu de données - jeu de données d’événement pour le centre d’appels (Global v1.1)

![Kafka](./images/kc20ds.png)

- **imsOrgID** : votre identifiant de l’organisation IMS est `--aepImsOrgId--`

>[!NOTE]
>
>Le champ **_id** doit être unique pour chaque ingestion de données. Si vous générez plusieurs événements, veillez à mettre à jour le champ **_id** chaque fois vers une nouvelle valeur unique.

Vous devriez alors avoir quelque chose comme ceci :

![Kafka](./images/kc21.png)

Ensuite, copiez l’événement d’expérience complet dans le presse-papiers. L’espace blanc de votre charge utile JSON doit être supprimé. Pour ce faire, nous utiliserons un outil en ligne. Pour ce faire, rendez-vous sur [http://jsonviewer.stack.hu/](http://jsonviewer.stack.hu/) .

Collez l’événement d’expérience dans l’éditeur et cliquez sur **Supprimer l’espace blanc**.

![Kafka](./images/kc22a.png)

Ensuite, sélectionnez tout le texte de sortie et copiez-le dans le presse-papiers.

![Kafka](./images/kc23.png)

Revenez à la fenêtre de votre terminal.

![Kafka](./images/kc16.png)

Collez la nouvelle payload sans espaces dans la fenêtre Terminal et cliquez sur **Entrée**.

![Kafka](./images/kc23a.png)

Revenez ensuite à votre site web de démonstration et actualisez la page. Vous devriez maintenant voir un événement d’expérience sur votre profil, sous **Événements d’expérience**, comme celui ci-dessous :

![Kafka](./images/kc24.png)

>[!NOTE]
>
>Si vous souhaitez que les interactions de votre centre d’appels apparaissent dans le panneau Visionneuse de profils, vous devez ajouter le libellé ci-dessous et filtrer votre projet sur [https://dsn.adobe.com](https://dsn.adobe.com), en accédant à l’onglet **Visionneuse de profils** et en ajoutant une nouvelle ligne sous **Événements**, avec ces variables :
>- **Étiquette de type d’événement** : Interactions avec le centre d’appels
>- **Filtre de type d’événement** : callCenterInteractionKafka
>- **Titre** : `--aepTenantId--.interactionDetails.core.callCenterAgent.callID`

![Kafka](./images/kc25.png)

Vous avez terminé cet exercice.

Étape suivante : [Résumé et avantages](./summary.md)

[Revenir au module 2.6](./aep-apache-kafka.md)

[Revenir à tous les modules](../../../overview.md)
