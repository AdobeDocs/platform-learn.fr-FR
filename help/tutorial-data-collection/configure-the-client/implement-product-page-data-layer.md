---
title: Mise en oeuvre d’une couche de données sur une page de produit
description: Mise en oeuvre d’une couche de données sur une page de produit
exl-id: 0debf34a-48d4-4029-b790-7fd78865c334
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '632'
ht-degree: 0%

---

# Mise en oeuvre d’une couche de données sur une page de produit

Pour ce tutoriel, vous implémentez la couche de données client Adobe pour un site web d’e-commerce classique. Si vous ne l’avez pas déjà fait, veuillez lire [Utilisation de la couche de données client Adobe](how-to-use-the-adobe-client-data-layer.md) Commencez par comprendre la couche de données client d’Adobe.

Supposons que l’utilisateur consulte vos produits et clique sur un rouleau de mousse pour en savoir plus. L’utilisateur accède à la page des détails du produit en forme de rouleau de mousse.

## Création d’une page de détails de produit simple

1. Copiez et collez le code suivant dans un nouveau fichier de HTML et enregistrez-le sur votre ordinateur.

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

Dans le `<head>` y a une balise `<script>` balise . C’est là que vous placez votre code JavaScript. Bien qu’il ne soit pas nécessaire de placer la variable `<script>` dans la balise `<head>` , il est recommandé. Cela permet de garantir que les données sont disponibles dès que possible pour la couche de données afin de prendre en charge divers cas d’utilisation.

## Ajout de la couche de données d’Adobe

1. Dans le `<script>` , ajoutez ce code qui crée la balise `adobeDataLayer` puis envoie les informations d’événement et de données appropriées dans le tableau. Les données sont conformes au schéma XDM. [que vous avez créé](../configure-the-server/create-a-schema.md).

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

Dans cet exemple, vous avez effectué deux transmissions vers la couche de données, chacune contenant une `event` clé. Inclusion d’une `event` la clé communique non seulement l’événement qui s’est produit sur la page, mais elle simplifie également la création de règles appropriées dans les balises par le marketeur.

La première transmission à la couche de données avertit les utilisateurs (règles de balise) que l’utilisateur a consulté la page. Il ajoute également le nom de la page et la section du site à la couche de données.

La seconde transmission à la couche de données avertit les utilisateurs (règles de balises) que l’utilisateur a consulté un produit. Il ajoute également des informations sur les produits à la couche de données.

## Ajout de code pour le suivi de l’ajout de panier

Pour ce tutoriel, vous pouvez suivre le moment où l’utilisateur clique sur le [!UICONTROL Ajouter au panier] bouton .

1. Copiez et collez ce code après le code de couche de données. La fonction est appelée lorsque l’utilisateur clique sur la fonction [!UICONTROL Ajouter au panier] bouton .

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

Cette fonction vérifie initialement si un panier existe déjà pour un utilisateur.  Si le panier n’existe pas, vous pouvez envoyer une `cartOpened` à la couche de données. Plus tard, vous lancez une `productAddedToCart` dans la couche de données. Les informations sur les produits existent déjà dans la couche de données. Vous n’avez donc pas besoin de les ajouter à nouveau.

## Bouton Ajouter un attribut à ajouter au panier

1. Ajoutez un `onclick` à l’attribut [!UICONTROL Ajouter au panier] qui appelle votre nouveau `onAddToCartClick` fonction .

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

## Ajout de code pour le suivi des téléchargements d’applications

Une dernière chose à suivre est lorsque l’utilisateur clique sur la variable _[!UICONTROL Téléchargement de l’application]_ lien.

1. Pour ce faire, copiez et collez ce code sous le code d’ajout de panier. Cette fonction est appelée lorsque l’utilisateur clique sur la fonction _[!UICONTROL Téléchargement de l’application]_ lien.

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

## Ajout d’un attribut pour télécharger le lien de l’application

1. Ajoutez un `onclick` à l’attribut [!UICONTROL Téléchargement de l’application] lien qui appelle votre nouveau `onDownloadAppClick` fonction .

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

[Suivant : ](create-a-tags-property-and-install-extensions.md)

>[!NOTE]
>
>Merci d’avoir consacré votre temps à l’apprentissage de la collecte de données. Si vous avez des questions, souhaitez partager des commentaires généraux ou avez des suggestions sur le contenu futur, partagez-les à ce sujet. [Article de discussion de la communauté Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-use-adobe-experience-platform-data/m-p/543877)
