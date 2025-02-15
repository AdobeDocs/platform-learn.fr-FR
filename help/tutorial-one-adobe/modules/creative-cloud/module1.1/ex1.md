---
title: Prise en main des services Firefly
description: Découvrez comment utiliser Postman et Adobe I/O pour interroger les API des services Adobe Firefly
role: Developer
level: Beginner
jira: KT-5342
doc-type: Tutorial
exl-id: 52385c33-f316-4fd9-905f-72d2d346f8f5
source-git-commit: 5ee9c3b7cde5444ecceca4b01cc275d6263d8a59
workflow-type: tm+mt
source-wordcount: '224'
ht-degree: 0%

---

# 1.1.1 Prise en main des services Firefly

Découvrez comment utiliser Postman et Adobe I/O pour interroger les API Adobe Firefly Services.

## Conditions préalables 1.1.1.1

Avant de poursuivre cet exercice, vous devez avoir terminé la configuration de [votre projet Adobe I/O](./../../../modules/getting-started/gettingstarted/ex6.md) et vous devez également avoir configuré une application pour interagir avec les API, telles que [Postman](./../../../modules/getting-started/gettingstarted/ex7.md) ou [PostBuster](./../../../modules/getting-started/gettingstarted/ex8.md).

## 1.1.1.2 Adobe I/O - access_token

Dans la collection **Adobe IO - OAuth**, sélectionnez la requête nommée **POST - Obtenir le jeton d’accès** et sélectionnez **Envoyer**. La réponse doit contenir un nouveau **accestoken**.

![Postman](./images/ioauthresp.png){zoomable="yes"}

## 1.1.1.3 API Firefly Services, Texte 2 Image

Maintenant que vous disposez d’un nouveau jeton d’accès valide, vous êtes prêt à envoyer votre première requête aux API des services Firefly.

Sélectionnez la requête nommée **POST - Firefly - T2I V3** dans la collection **FF - Firefly Services Tech Insiders**.

![Firefly](./images/ff1.png){zoomable="yes"}

Copiez l’URL de l’image à partir de la réponse et ouvrez-la dans votre navigateur web pour afficher l’image.

![Firefly](./images/ff2.png){zoomable="yes"}

Vous devriez voir une belle image représentant `horses in a field`.

![Firefly](./images/ff3.png){zoomable="yes"}

N’hésitez pas à lire la requête API avant de passer à l’exercice suivant.

## Étapes suivantes

Accédez à [Optimiser votre processus Firefly à l’aide de Microsoft Azure et des URL prédéfinies](./ex2.md){target="_blank"}

Revenez à [ Présentation des services Adobe Firefly ](./firefly-services.md){target="_blank"}

Revenir à [Tous les modules](./../../../overview.md){target="_blank"}
