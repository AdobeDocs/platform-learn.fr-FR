---
title: API de modèles personnalisés Firefly
description: Utilisation de l’API de modèles personnalisés Firefly
role: Developer
level: Beginner
jira: KT-5342
doc-type: Tutorial
exl-id: 330f4492-d0df-4298-9edc-4174b0065c9a
source-git-commit: 219945c74c620b9a4b93cb2b7462137118d42d33
workflow-type: tm+mt
source-wordcount: '823'
ht-degree: 1%

---

# API des modèles personnalisés Firefly 1.1.4

## 1.1.4.1 Configurer votre modèle personnalisé

Accédez à [https://firefly.adobe.com/](https://firefly.adobe.com/). Cliquez sur **Modèles personnalisés**.

![Modèles personnalisés Firefly](./images/ffcm1.png){zoomable="yes"}

Il se peut que ce message s’affiche. Si c’est le cas, cliquez sur **Accepter** pour continuer.

![Modèles personnalisés Firefly](./images/ffcm2.png){zoomable="yes"}

Vous devriez alors voir ceci. Cliquez sur **Entraîner un modèle**.

![Modèles personnalisés Firefly](./images/ffcm3.png){zoomable="yes"}

Configurez les champs suivants :

- **Name** : utilisez `--aepUserLdap-- - Citi Signal Router Model`
- **Mode de formation** : sélectionnez **Sujet (aperçu technique)**
- **Concept** : saisissez `router`
- **Enregistrer dans** : ouvrez la liste déroulante et cliquez sur **+ Créer un projet**

![Modèles personnalisés Firefly](./images/ffcm4.png){zoomable="yes"}

Attribuez un nom au nouveau projet : `--aepUserLdap-- - Custom Models`. Cliquez sur **Créer**.

![Modèles personnalisés Firefly](./images/ffcm5.png){zoomable="yes"}

Vous devriez alors voir ceci. Cliquez sur **Créer**.

![Modèles personnalisés Firefly](./images/ffcm6.png){zoomable="yes"}

Vous devez maintenant fournir les images de référence pour le modèle personnalisé à entraîner. Cliquez sur **Sélectionner des images sur votre ordinateur**.

![Modèles personnalisés Firefly](./images/ffcm7.png){zoomable="yes"}

Téléchargez les images de référence [ici](https://tech-insiders.s3.us-west-2.amazonaws.com/CitiSignal_router.zip). Décompressez le fichier de téléchargement, ce qui devrait vous donner ceci.

![Modèles personnalisés Firefly](./images/ffcm8.png){zoomable="yes"}

Accédez au dossier contenant les fichiers image de téléchargement. Sélectionnez-les tous et cliquez sur **Ouvrir**.

![Modèles personnalisés Firefly](./images/ffcm9.png){zoomable="yes"}

Vous verrez alors que vos images sont en cours de chargement.

![Modèles personnalisés Firefly](./images/ffcm10.png){zoomable="yes"}

Au bout de quelques minutes, vos images sont correctement chargées. Il se peut que certaines images comportent une erreur, car la légende de l’image n’a pas été générée ou n’est pas suffisamment longue. Vérifiez chaque image avec une erreur et saisissez une légende qui répond aux exigences et décrit l’image.

![Modèles personnalisés Firefly](./images/ffcm11.png){zoomable="yes"}

Une fois que toutes les images comportent des légendes qui répondent aux exigences, vous devez toujours fournir un exemple d’invite. Saisissez une invite qui utilise le mot &#39;routeur&#39;. Une fois que vous avez fait cela, vous pouvez commencer à entraîner votre modèle. Cliquez sur **Former**.

![Modèles personnalisés Firefly](./images/ffcm12.png){zoomable="yes"}

Tu verras ça. L’entraînement de votre modèle peut prendre entre 20 et 30 minutes, voire plus.

![Modèles personnalisés Firefly](./images/ffcm13.png){zoomable="yes"}

Après 20 à 30 minutes, votre modèle est maintenant entraîné et peut être publié. Cliquez sur **Publier**.

![Modèles personnalisés Firefly](./images/ffcm14.png){zoomable="yes"}

Cliquez de nouveau sur **Publier**.

![Modèles personnalisés Firefly](./images/ffcm15.png){zoomable="yes"}

Fermez la fenêtre contextuelle **Partager un modèle personnalisé**.

![Modèles personnalisés Firefly](./images/ffcm16.png){zoomable="yes"}

## 1.1.4.2 utiliser votre modèle personnalisé dans l’interface utilisateur

Accédez à [https://firefly.adobe.com/cme/train](https://firefly.adobe.com/cme/train). Cliquez sur votre modèle personnalisé pour l’ouvrir.

![Modèles personnalisés Firefly](./images/ffcm19.png){zoomable="yes"}

Cliquez sur **Prévisualiser et tester**.

![Modèles personnalisés Firefly](./images/ffcm17.png){zoomable="yes"}

L’exemple d’invite que vous avez saisi avant d’être exécuté s’affiche.

![Modèles personnalisés Firefly](./images/ffcm18.png){zoomable="yes"}

## 1.1.4.3 Activer votre modèle personnalisé pour l’API de modèles personnalisés des services Firefly

Une fois votre modèle personnalisé entraîné, il peut également être utilisé via l’API. Dans l’exercice 1.1.1, vous avez déjà configuré votre projet Adobe I/O pour l’interaction avec les services Firefly via l’API.

Accédez à [https://firefly.adobe.com/cme/train](https://firefly.adobe.com/cme/train). Cliquez sur votre modèle personnalisé pour l’ouvrir.

![Modèles personnalisés Firefly](./images/ffcm19.png){zoomable="yes"}

Cliquez sur le **de 3 points...**, puis sur **Partager**.

![Modèles personnalisés Firefly](./images/ffcm20.png){zoomable="yes"}

Pour accéder à un modèle personnalisé Firefly, ce dernier doit être partagé avec l’**ID de compte technique** de votre projet Adobe I/O.

Pour récupérer votre **Identifiant de compte technique**, rendez-vous sur [https://developer.adobe.com/console/projects](https://developer.adobe.com/console/projects). Cliquez pour ouvrir votre projet, qui s’appelle `--aepUserLdap-- Firefly`.

![Modèles personnalisés Firefly](./images/ffcm24.png){zoomable="yes"}

Cliquez sur **OAuth de serveur à serveur**.

![Modèles personnalisés Firefly](./images/ffcm25.png){zoomable="yes"}

Cliquez pour copier votre **Identifiant de compte technique**.

![Modèles personnalisés Firefly](./images/ffcm23.png){zoomable="yes"}

Collez votre **ID de compte technique** et cliquez sur **Inviter à modifier**.

![Modèles personnalisés Firefly](./images/ffcm21.png){zoomable="yes"}

Le **ID de compte technique** devrait maintenant pouvoir accéder au modèle personnalisé.

![Modèles personnalisés Firefly](./images/ffcm22.png){zoomable="yes"}

## 1.1.4.4 Interaction avec l’API des modèles personnalisés des services Firefly

Dans l’exercice 1.1.1, Prise en main des services Firefly, vous avez téléchargé le fichier suivant : [postman-ff.zip](./../../../assets/postman/postman-ff.zip) sur votre bureau local, puis vous avez importé cette collection dans Postman.

Ouvrez Postman et accédez au dossier **FF - API de modèles personnalisés**.

![Modèles personnalisés Firefly](./images/ffcm30.png){zoomable="yes"}

Ouvrez la requête **1. FF - getCustomModels** et cliquez sur **Envoyer**.

![Modèles personnalisés Firefly](./images/ffcm31.png){zoomable="yes"}

Vous devriez voir le modèle personnalisé que vous avez créé précédemment, nommé `--aepUserLdap-- - Citi Signal Router Model`, dans le cadre de la réponse. Le champ **assetId** est l’identifiant unique de votre modèle personnalisé, qui sera référencé dans la requête suivante.

![Modèles personnalisés Firefly](./images/ffcm32.png){zoomable="yes"}

Ouvrez la requête **2. Générer des images asynchrones**. Dans cet exemple, vous allez demander la génération de 2 variations en fonction de votre modèle personnalisé. N’hésitez pas à mettre à jour l’invite qui, dans ce cas, est `a white router on a volcano in Africa`.

Cliquez sur **Envoyer**.

![Modèles personnalisés Firefly](./images/ffcm33.png){zoomable="yes"}

La réponse contient un champ **jobId**. La tâche de génération de ces 2 images est en cours d’exécution. Vous pouvez vérifier le statut à l’aide de la requête suivante.

![Modèles personnalisés Firefly](./images/ffcm34.png){zoomable="yes"}

Ouvrez la requête **3. Obtenez le statut CM** puis cliquez sur **Envoyer**. Vous devriez alors voir que le statut est défini sur en cours d’exécution.

![Modèles personnalisés Firefly](./images/ffcm35.png){zoomable="yes"}

Après quelques minutes, cliquez de nouveau sur **Envoyer** pour la requête **3. Obtention du statut CM**. Vous devriez alors constater que le statut est passé à **réussi** et vous devriez voir deux URL d’image dans le cadre de la sortie. Cliquez pour ouvrir les deux fichiers.

![Modèles personnalisés Firefly](./images/ffcm36.png){zoomable="yes"}

Il s’agit de la première image générée dans cet exemple.

![Modèles personnalisés Firefly](./images/ffcm37.png){zoomable="yes"}

Il s’agit de la deuxième image générée dans cet exemple.

![Modèles personnalisés Firefly](./images/ffcm38.png){zoomable="yes"}

Vous avez maintenant terminé cet exercice.

## Étapes suivantes

Accédez à [ Résumé et avantages ](./summary.md){target="_blank"}

Revenez à [ Utilisation des API Photoshop ](./ex3.md){target="_blank"}

Revenez à [ Présentation des services Adobe Firefly ](./firefly-services.md){target="_blank"}
