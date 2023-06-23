---
title: Mise en oeuvre d’une couche de données sur une page de produit
description: Mise en oeuvre d’une couche de données sur une page de produit
role: Developer
level: Intermediate
recommendations: noDisplay,noCatalog
jira: KT-10447
hide: true
hidefromtoc: true
exl-id: a72011a5-ea9c-45df-a0f3-5eb40bc99d3f
source-git-commit: 90f7621536573f60ac6585404b1ac0e49cb08496
workflow-type: tm+mt
source-wordcount: '573'
ht-degree: 0%

---

# Mise en oeuvre d’une couche de données sur une page de produit

Pour ce tutoriel, vous allez mettre en oeuvre la couche de données client Adobe pour un site web de commerce électronique standard. Si vous ne l’avez pas déjà fait, veuillez lire [Utilisation de la couche de données client Adobe](how-to-use-the-adobe-client-data-layer.md) Commencez par comprendre le fonctionnement de la couche de données client Adobe.

Supposons que l’utilisateur consulte vos produits et clique sur un rouleau de mousse pour en savoir plus. L’utilisateur accède à la page des détails du produit en forme de rouleau de mousse.

Voici le HTML de votre page des détails du produit :

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <title>Product Page</title>
    <script>
      // Code will go here.
    </script>
  </head>
  <body>
    <h1>Foam Roller</h1>
    <p>This foam roller is composed of durable material that holds its shape and delivers deep tissue therapy. Purchase now for only $18.95!</p>
    <button type="button">Add to cart</button>
    <a href="https://example.com/download">Download the app</a>
  </body>
</html>
```

Comme vous l’avez peut-être remarqué, à l’intérieur du `<head>` y a une balise `<script>` balise . C’est là que vous allez placer votre code JavaScript. Il n’est pas nécessaire de placer la variable `<script>` balise dans `<head>`, mais envoyer les données à la couche de données dès que possible permet au marketeur de les envoyer rapidement vers Adobe Experience Platform avant que l’utilisateur ne quitte la page.

Dans le `<script>` , vous commencerez par créer la balise `adobeDataLayer` puis en poussant les informations d’événement et de données appropriées dans le tableau. Les données sont conformes au schéma XDM. [que vous avez créé](../configure-the-server/create-a-schema.md).

```js
window.adobeDataLayer = window.adobeDataLayer || [];
window.adobeDataLayer.push({
  "event": "pageViewed",
  "web": {
    "webPageDetails": {
      "name": "Foam Roller",
      "siteSection": "Equipment"
    },
  }
});
window.adobeDataLayer.push({
  "event": "productViewed",
  "productListItems": [
    {
      "SKU": "eqfr08",
      "currencyCode": "USD",
      "name": "Foam Roller",
      "priceTotal": 18.95
    }
  ]
});
```

Dans cet exemple, vous avez effectué deux transmissions vers la couche de données, chacune contenant une `event` clé. Inclusion d’une `event` la clé communique non seulement l’événement qui s’est produit sur la page, mais elle simplifie également la création de règles appropriées par le marketeur dans les balises Adobe Experience Platform.

La première notification push vers la couche de données avertit les utilisateurs (règles de balises) que l’utilisateur a consulté la page. Il ajoute également le nom de la page et la section du site à la couche de données.

La seconde transmission à la couche de données avertit les utilisateurs (règles de balises) que l’utilisateur a consulté un produit. Il ajoute également des informations sur les produits à la couche de données.

## Ajouter au panier

Vous souhaitez probablement également effectuer le suivi du moment où l’utilisateur clique sur le [!UICONTROL Ajouter au panier] bouton .

Pour ce faire, créez une fonction qui est appelée lorsque l’utilisateur clique sur la fonction [!UICONTROL Ajouter au panier] bouton .

```js
window.onAddToCartClick = function() {
  // In a real implementation, you would change this condition to 
  // only pass if a cart doesn't already exist. You would typically 
  // do this by checking a cookie or variable value.
  if (true) {
    window.adobeDataLayer.push({
      "event": "cartOpened",
    });
  }
  window.adobeDataLayer.push({
    "event": "productAddedToCart"
  });
};
```

Lorsque cette fonction est appelée, elle vérifie d’abord si un panier existe déjà pour un utilisateur. En règle générale, cela se fait en vérifiant si un cookie ou une variable spécifique existe. Si le panier n’existe pas, vous enverrez une `cartOpened` dans la couche de données. Par la suite, vous enverrez une `productAddedToCart` dans la couche de données. Les informations sur les produits existent déjà dans la couche de données. Vous n’avez donc pas besoin de les ajouter à nouveau.

Ajoutez un `onclick` à l’attribut [!UICONTROL Ajouter au panier] qui appelle votre nouveau `onAddToCartClick` fonction .

Le résultat de votre page de HTML doit se présenter comme suit :

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <title>Product Page</title>
    <script>
      window.adobeDataLayer = window.adobeDataLayer || [];
      window.adobeDataLayer.push({
        "event": "pageViewed",
        "web": {
          "webPageDetails": {
            "name": "Foam Roller",
            "siteSection": "Equipment"
          },
        },
        "productListItems": [
          {
            "SKU": "eqfr08",
            "currencyCode": "USD",
            "name": "Foam Roller",
            "priceTotal": 18.95
          }
        ]
      });
      window.adobeDataLayer.push({
        "event": "productViewed"
      });
      window.onAddToCartClick = function() {
        // In a real implementation, you would change this condition to 
        // only pass if a cart doesn't already exist. You would typically 
        // do this by checking a cookie or variable value.
        if (true) {
          window.adobeDataLayer.push({
            "event": "cartOpened",
          });
        }
        window.adobeDataLayer.push({
          "event": "productAddedToCart"
        });
      };
    </script>
  </head>
  <body>
    <h1>Foam Roller</h1>
    <p>This foam roller is composed of durable material that holds its shape and delivers deep tissue therapy. Purchase now for only $18.95!</p>
    <button type="button" onclick="onAddToCartClick()">Add to cart</button>
    <a href="https://example.com/download">Download the app</a>
  </body>
</html>
```

## Téléchargement de l’application

Une dernière chose à faire est de suivre le moment où l’utilisateur clique sur la variable _[!UICONTROL Téléchargement de l’application]_ lien.

Pour ce faire, créez une fonction qui est appelée lorsque l’utilisateur clique sur la fonction _[!UICONTROL Téléchargement de l’application]_ lien.

```js
window.onDownloadAppClick = function(event) {
  window.adobeDataLayer.push({
    "event": "downloadAppClicked",
    "eventInfo": {
      "web": {
        "webInteraction": {
          "URL": "https://example.com/download",
          "name": "App Download",
          "type": "download"
        }
      }
    }
  });
};
```

Dans ce cas, les informations sur le lien sont enveloppées dans une balise `eventInfo` clé. Comme décrit dans [Utilisation de la couche de données client Adobe](how-to-use-the-adobe-client-data-layer.md), cela indique à la couche de données de communiquer ces données avec l’événement, mais à _not_ conservez les données dans la couche de données. Pour un clic sur un lien, il n’est pas utile d’ajouter des informations sur le lien sur lequel l’utilisateur a cliqué à la couche de données, car elles ne concernent pas l’ensemble de la page et ne s’appliquent pas aux autres événements qui peuvent se produire.

Ajoutez un `onclick` à l’attribut [!UICONTROL Téléchargement de l’application] lien qui appelle votre nouveau `onDownloadAppClick` fonction .

Le résultat de votre page de HTML doit se présenter comme suit :

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <title>Product Page</title>
    <script>
      window.adobeDataLayer = window.adobeDataLayer || [];
      window.adobeDataLayer.push({
        "event": "pageViewed",
        "web": {
          "webPageDetails": {
            "name": "Foam Roller",
            "siteSection": "Equipment"
          },
        },
        "productListItems": [
          {
            "SKU": "eqfr08",
            "currencyCode": "USD",
            "name": "Foam Roller",
            "priceTotal": 18.95
          }
        ]
      });
      window.adobeDataLayer.push({
        "event": "productViewed"
      });
      window.onAddToCartClick = function() {
        // In a real implementation, you would change this condition to 
        // only pass if a cart doesn't already exist. You would typically 
        // do this by checking a cookie or variable value.
        if (true) {
          window.adobeDataLayer.push({
            "event": "cartOpened",
          });
        }
        window.adobeDataLayer.push({
          "event": "productAddedToCart"
        });
      };
      window.onDownloadAppClick = function() {
        window.adobeDataLayer.push({
          "event": "downloadAppClicked",
          "eventInfo": {
            "web": {
              "webInteraction": {
                "URL": "https://example.com/download",
                "name": "App Download",
                "type": "download"
              }
            }
          }
        });
      };
    </script>
  </head>
  <body>
    <h1>Foam Roller</h1>
    <p>This foam roller is composed of durable material that holds its shape and delivers deep tissue therapy. Purchase now for only $18.95!</p>
    <button type="button" onclick="onAddToCartClick()">Add to cart</button>
    <a href="https://example.com/download" onclick="onDownloadAppClick()">Download the app</a>
  </body>
</html>
```
