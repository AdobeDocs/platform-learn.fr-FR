---
title: Prise en main des services Firefly
description: Découvrez comment utiliser Postman et Adobe I/O pour interroger les API des services Adobe Firefly
role: Developer
level: Beginner
jira: KT-5342
doc-type: Tutorial
exl-id: 52385c33-f316-4fd9-905f-72d2d346f8f5
source-git-commit: 6ef4ce94dbbcd65ab30bcfad24f4ddd746c26b82
workflow-type: tm+mt
source-wordcount: '741'
ht-degree: 0%

---

# 1.1.1 Prise en main des services Firefly

Découvrez comment utiliser Postman et Adobe I/O pour interroger les API Adobe Firefly Services.

## Conditions préalables 1.1.1.1

Avant de poursuivre cet exercice, vous devez avoir terminé la configuration de [votre projet Adobe I/O](./../../../modules/getting-started/gettingstarted/ex6.md) et vous devez également avoir configuré une application pour interagir avec les API, telles que [Postman](./../../../modules/getting-started/gettingstarted/ex7.md) ou [PostBuster](./../../../modules/getting-started/gettingstarted/ex8.md).

## 1.1.1.1 firefly.adobe.com

Accédez à [https://firefly.adobe.com](https://firefly.adobe.com). Cliquez sur l’icône **profil** et vérifiez que vous êtes connecté au **Compte** approprié, qui doit être `--aepImsOrgName--`. Si nécessaire, cliquez sur **Changer de profil** pour passer à ce compte.

![Postman](./images/ffui1.png){zoomable="yes"}

Saisissez le `Horses in a field` d’invite et cliquez sur **Générer**.

![Postman](./images/ffui2.png){zoomable="yes"}

Vous devriez alors voir quelque chose de similaire à ceci.

![Postman](./images/ffui3.png){zoomable="yes"}

Ouvrez ensuite l’**outil de développement** dans votre navigateur.

![Postman](./images/ffui4.png){zoomable="yes"}

Vous devriez alors voir ceci. Accédez à l’onglet **Réseau**.

![Postman](./images/ffui5.png){zoomable="yes"}

Saisissez le terme de recherche **générer**, puis cliquez de nouveau sur **générer**. Vous devriez alors voir une requête nommée **generate-async**. Sélectionnez-la, puis accédez à **Payload** où vous verrez les détails de la requête.

![Postman](./images/ffui6.png){zoomable="yes"}

La requête que vous voyez ici est la requête qui est envoyée au serveur principal des services Firefly côté serveur. Il contient plusieurs paramètres importants :

- **prompt** : il s’agit de votre invite, demandant le type d’image que Firefly doit générer

- **seed** : dans cette requête, les adresses de contrôle ont été générées de manière aléatoire. Chaque fois que Firefly génère une image, il lance par défaut le processus en sélectionnant un nombre aléatoire appelé graine. Ce nombre aléatoire contribue à rendre chaque image unique, ce qui est idéal lorsque vous souhaitez générer une grande variété d’images. Cependant, il peut arriver que vous souhaitiez générer des images similaires entre elles sur plusieurs requêtes. Par exemple, lorsque Firefly génère une image que vous souhaitez modifier à l’aide d’autres options de Firefly (telles que les paramètres prédéfinis de style, les images de référence, etc.), utilisez l’adresse de contrôle de cette image dans les futures requêtes HTTP pour limiter le caractère aléatoire des images futures et affiner l’image que vous souhaitez.

![Postman](./images/ffui7.png){zoomable="yes"}

Jetez à nouveau un coup d’œil à l’interface utilisateur d’. Remplacez **Format** par **Paysage (4:3)**.

![Postman](./images/ffui8.png){zoomable="yes"}

Faites défiler jusqu’à **Effets**, accédez à **Thèmes** et sélectionnez un effet tel que **Bande dessinée**.

![Postman](./images/ffui9.png){zoomable="yes"}

Ouvrez à nouveau l’**outil de développement** dans votre navigateur. Cliquez ensuite sur **Générer** et examinez la requête réseau envoyée.

![Postman](./images/ffui10.png){zoomable="yes"}

Lorsque vous examinez les détails de la requête réseau, les éléments suivants s’affichent :

- **prompt** n&#39;a pas changé par rapport à la requête précédente
- **seed** n’a pas changé par rapport à la requête précédente.
- La **taille** a été modifiée en fonction de la modification du **format**.
- **styles** a été ajouté et contient une référence à l&#39;effet **comic_book** que vous avez sélectionné

![Postman](./images/ffui11.png){zoomable="yes"}

Pour l&#39;exercice suivant, vous devrez utiliser l&#39;un des nombres **seed**. Notez un nombre de départ de votre choix.

Dans l’exercice suivant, vous allez faire des choses similaires avec les services Firefly, mais en utilisant l’API plutôt que l’interface utilisateur. Dans cet exemple, le numéro de contrôle est **45781**.

## 1.1.1.3 Adobe I/O - access_token

Dans la collection **Adobe IO - OAuth**, sélectionnez la requête nommée **POST - Obtenir le jeton d’accès** et sélectionnez **Envoyer**. La réponse doit contenir un nouveau **accestoken**.

![Postman](./images/ioauthresp.png){zoomable="yes"}

## 1.1.1.4 API Firefly Services, Texte 2 Image

Maintenant que vous disposez d’un nouveau jeton d’accès valide, vous êtes prêt à envoyer votre première requête aux API des services Firefly.

Sélectionnez la requête nommée **POST - Firefly - T2I V3** dans la collection **FF - Firefly Services Tech Insiders**.

![Firefly](./images/ff1.png){zoomable="yes"}

Copiez l’URL de l’image à partir de la réponse et ouvrez-la dans votre navigateur web pour afficher l’image.

![Firefly](./images/ff2.png){zoomable="yes"}

Vous devriez voir une belle image représentant `horses in a field`.

![Firefly](./images/ff3.png){zoomable="yes"}

Dans le **Corps** de votre requête **POST - Firefly - T2I V3**, ajoutez ce qui suit sous le champ `"promptBiasingLocaleCode": "en-US"` et remplacez la variable `XXX` par l’un des numéros de contrôle qui ont été utilisés de manière aléatoire par l’interface utilisateur de Firefly Services. Dans cet exemple, le nombre **seed** est `45781`.

```json
,
  "seeds": [
    XXX
  ]
```

Cliquez sur **Envoyer**. Vous recevrez ensuite une réponse avec une nouvelle image générée par les services Firefly. Ouvrez l’image pour l’afficher.

![Firefly](./images/ff4.png){zoomable="yes"}

Vous devriez alors voir une nouvelle image avec de légères différences, en fonction de l’**origine** utilisée.

![Firefly](./images/ff5.png){zoomable="yes"}

Ensuite, dans le **Corps** de votre requête **POST - Firefly - T2I V3**, collez l’objet **styles** ci-dessous sous l’objet **seed**. Le style de l’image générée devient alors **comic_book**.

```json
,
  "contentClass": "art",
  "styles": {
    "presets": [
      "comic_book"
    ],
    "strength": 50
  }
```

## Étapes suivantes

Accédez à [Optimiser votre processus Firefly à l’aide de Microsoft Azure et des URL prédéfinies](./ex2.md){target="_blank"}

Revenez à [ Présentation des services Adobe Firefly ](./firefly-services.md){target="_blank"}

Revenir à [Tous les modules](./../../../overview.md){target="_blank"}
