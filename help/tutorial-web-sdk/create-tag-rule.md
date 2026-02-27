---
title: Création de règles de balises pour Platform Web SDK
description: Découvrez comment envoyer un événement à Platform Edge Network avec votre objet XDM à l’aide d’une règle de balise. Cette leçon fait partie du tutoriel Implémentation d’Adobe Experience Cloud avec le SDK web.
feature: Tags
jira: KT-15403
exl-id: e06bad06-3ee3-475f-9b10-f0825a48a312
source-git-commit: 9b5e7192094e2d3b8eb41cbb4a0f28411e990e8f
workflow-type: tm+mt
source-wordcount: '1803'
ht-degree: 2%

---

# Création de règles de balises

Découvrez comment envoyer des événements à Adobe Experience Platform Edge Network avec votre objet XDM à l’aide de règles de balises. Une règle de balise est une combinaison d’événements, de conditions et d’actions qui indique à la propriété de balise d’effectuer une opération. Avec Platform Web SDK, les règles sont utilisées pour envoyer des événements à Platform Edge Network avec les données appropriées.



## Objectifs d’apprentissage

À la fin de cette leçon, vous êtes capable de :

* Utiliser une convention de nommage pour la gestion des règles dans les balises
* Envoyer un événement avec des champs XDM à l’aide des actions Mettre à jour la variable et Envoyer l’événement
* Empilement de plusieurs ensembles de champs XDM sur plusieurs règles
* Mappez des éléments de données de tableau individuels ou entiers à l’objet XDM.
* Publication d’une règle de balise dans une bibliothèque de développement


## Conditions préalables

Vous connaissez les balises de la collecte de données et le site de démonstration [Luma](https://newluma.enablementadobe.com) et avez terminé les leçons précédentes du tutoriel :

* [Configuration d’un schéma XDM](configure-schemas.md)
* [Configuration d’un espace de noms d’identité](configure-identities.md)
* [Configurer un trains de données](configure-datastream.md)
* [Installer l’extension SDK Web](install-web-sdk.md)
* [Création d’éléments de données](create-data-elements.md)
* [Création d’identités](create-identities.md)

## Conventions de dénomination

Pour gérer les règles dans les balises, il est recommandé de suivre une convention de dénomination standard. Ce tutoriel utilise une convention de nommage en cinq parties :

* [**location**] - [**event**] - [**purpose**] - [**order**]

où ;

1. **emplacement** est la ou les pages du site sur lesquelles la règle se déclenche
1. **event** est le déclencheur de la règle
1. **objectif** est la principale action effectuée par la règle
1. **ordre** est l’ordre dans lequel la règle doit se déclencher par rapport aux autres règles
<!-- minor update -->

## Ajout de l’extension Adobe Client Data Layer (ACDL)

Le site web Luma utilise une couche de données pilotée par les événements appelée couche de données client Adobe (ACDL). Chaque fois qu’un événement se produit, il est placé dans le tableau `adobeDataLayer`. Nous utiliserons ces événements pour créer nos règles, bien que de nombreuses options soient prêtes à l’emploi.

1. Accédez à **[!UICONTROL Extensions]**
1. Filtrer sur **[!UICONTROL la couche de données client Adobe]**
1. Sélectionnez **[!UICONTROL Installer]**

   ![Ajout de l’extension Adobe Client Data Layer](assets/rules-acdl-extension.png)

1. Conserver les paramètres par défaut
1. Sélectionnez **[!UICONTROL Enregistrer]**

## Création de règles de balises

Dans les balises, les règles sont utilisées pour exécuter des actions (appels de déclenchement) sous diverses conditions. L’extension de balises de Platform Web SDK comprend deux actions utilisées dans les règles :

* **[!UICONTROL Mettre à jour la variable]** mappe les éléments de données à vos variables XDM ou de données
* **[!UICONTROL Envoyer l’événement]** envoie les données à Experience Platform Edge Network

Dans la suite de cette leçon, nous avons :

1. Utilisez l’action **[!UICONTROL Mettre à jour la variable]** pour définir une « configuration globale » des champs XDM.

1. Utilisez l’action **[!UICONTROL Mettre à jour la variable]** qui remplace notre « configuration globale » et qui fournit des champs XDM supplémentaires sous certaines conditions (par exemple, l’ajout de détails de produit sur les pages de produit).

1. Utilisez l’action **[!UICONTROL Envoyer l’événement]** pour envoyer toutes les données souhaitées à Adobe Experience Platform Edge Network.

Toutes ces règles seront correctement séquencées à l’aide de l’option « [!UICONTROL order] ».

Cette vidéo donne un aperçu du processus :

>[!VIDEO](https://video.tv.adobe.com/v/3427710/?learn=on&enablevpops)

### Champs de configuration globale

Pour créer une règle de balise pour les champs XDM globaux :

1. Ouvrez la propriété de balise que vous utilisez pour ce tutoriel

1. Accédez à **[!UICONTROL Règles]** dans le volet de navigation de gauche

1. Sélectionnez le bouton **[!UICONTROL Créer une règle]**

   ![Créer une règle](assets/rules-create.png)

1. Donnez à la règle le nom `all pages - adobeDataLayer push - set global variables - 1`.

1. Dans la section **[!UICONTROL Événements]**, sélectionnez **[!UICONTROL Ajouter]**

   ![Nommez la règle et ajoutez un événement](assets/rule-name-new.png)

1. Utilisez l’extension **[!UICONTROL Adobe Client Data Layer]** et sélectionnez **[!UICONTROL Données transmises]** comme **[!UICONTROL Type d’événement]**

1. Sélectionnez la liste déroulante **[!UICONTROL Avancé]** et saisissez `1` comme **[!UICONTROL Commande]**.

   >[!NOTE]
   >
   > Plus le numéro de commande est bas, plus tôt il s’exécute. Par conséquent, nous donnons à notre « configuration globale » un numéro d’ordre faible.

1. Écouter **[!UICONTROL Tous les événements]**
1. Sélectionnez **[!UICONTROL Conserver les modifications]** pour revenir à l’écran principal des règles
   ![Sélectionner le déclencheur de bibliothèque chargé](assets/create-tag-rule-trigger-loaded.png)

1. Dans la section **[!UICONTROL Actions]**, sélectionnez **[!UICONTROL Ajouter]**

1. Sélectionnez **[!UICONTROL Adobe Experience Platform Web SDK en tant qu’extension]**&#x200B;**&#x200B;**

1. Sélectionnez **[!UICONTROL Type d’action]**, puis **[!UICONTROL Mettre à jour la variable]**

1. En tant que **[!UICONTROL Élément de données]**, sélectionnez le `xdm.variable.content` que vous avez créé dans la leçon [Créer des éléments de données](create-data-elements.md)

   ![Mettre à jour le schéma de variables](assets/create-rule-update-variable.png)

1. Maintenant, spécifiez les champs XDM en les mappant aux valeurs appropriées :

   | Champ XDM | Mapper à |
   |---|---|
   | `eventType` | `Web Webpagedetails Page Views` (commencez à saisir pour voir les valeurs suggérées) |
   | `identityMap` | élément de données `Identity Map` |
   | `web.webPageDetails.name` | élément de données `Page Name` |
   | `web.webPageDetails.pageViews.value` | `1` |


   >[!TIP]
   >
   > Les champs XDM ne sont pas inclus dans la requête réseau si l’élément de données est null. Par conséquent, lorsque l’utilisateur n’est pas authentifié et que l’élément de données `Identity Map` est nul, l’objet `identityMap` n’est pas envoyé. C’est pourquoi nous pouvons le définir dans notre « configuration globale ».

   >[!TIP]
   >
   > Bien que ni `eventType` défini sur `web.webpagedetails.pageViews` ni `web.webPageDetails.pageViews.value` ne soient nécessaires pour qu’Adobe Analytics traite une balise en tant que page vue, il est utile de disposer d’une méthode standard pour indiquer une page vue pour d’autres applications en aval.

1. Lorsque vous aurez terminé, votre `XDM Variable` ressemblera à ceci. Notez comment les champs remplis et partiellement remplis sont indiqués par les cercles bleus :
   ![&#x200B; Variable XDM &#x200B;](assets/rule-xdm-variable.png)
1. Sélectionnez **[!UICONTROL Conserver les modifications]** puis **[!UICONTROL Enregistrer]** la règle dans l’écran suivant pour la terminer



### Champs de la page Produit

Commencez à présent à utiliser **[!UICONTROL Mettre à jour la variable]** dans des règles séquencées supplémentaires pour enrichir l’objet XDM avant de l’envoyer à [!UICONTROL Platform Edge Network].

>[!TIP]
>
>L’ordre des règles détermine la règle qui s’exécute en premier lorsqu’un événement est déclenché. Si deux règles ont le même type d’événement, celle qui a le plus petit nombre s’exécute en premier.
> 

Commencez par effectuer le suivi des consultations de produit sur la page des détails du produit de Luma :

1. Sélectionnez **[!UICONTROL Ajouter une règle]**
1. Nommez-le [!UICONTROL `product detail pages - adobeDataLayer push - set product details variables - 20`]
1. Sélectionnez le symbole ![+ sous Événement &#x200B;](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) ajouter un nouveau déclencheur
1. Sous **[!UICONTROL Extension]**, sélectionnez **[!UICONTROL Couche de données client Adobe]**
1. Sous **[!UICONTROL Type d’événement]**, sélectionnez **[!UICONTROL Données transmises]**
1. Sélectionnez pour ouvrir **[!UICONTROL Options avancées]**, puis saisissez `20`. Cette valeur d’ordre garantit que la règle s’exécute _après_ la règle des variables globales.
1. Écoute d’un événement **[!UICONTROL spécifique]**
1. Saisissez `productView` comme **[!UICONTROL Événement/Clé pour lequel s’enregistrer]**
1. Sélectionnez **[!UICONTROL Conserver les modifications]**

   ![Règles XDM Analytics](assets/rule-pdp-event.png)


1. Sous **[!UICONTROL Actions]** sélectionnez **[!UICONTROL Ajouter]**
1. Sélectionner l’extension **[!UICONTROL Adobe Experience Platform Web SDK]**
1. Sélectionnez **[!UICONTROL Type d’action]** comme **[!UICONTROL Variable de mise à jour]**
1. Sélectionnez `XDM Variable` comme **[!UICONTROL Élément de données]**
1. Mappez ces champs XDM aux valeurs appropriées :

   | Champ XDM | Mapper à |
   |---|---|
   | `eventType` | `Commerce Product Views` (commencez à saisir pour voir les valeurs suggérées) |
   | `commerce.productViews.value` | `1` |
   | `productListItems.name` | `Ecommerce Product Name` (Sélectionnez **[!UICONTROL Fournir des éléments individuels]** et **[!UICONTROL Ajouter un élément]** en premier ) |
   | `productListItems.sku` | `Ecommerce Product Id` |

1. Sélectionnez **[!UICONTROL Conserver les modifications]**

1. Sélectionnez **[!UICONTROL Enregistrer]** pour enregistrer la règle

   >[!NOTE]
   >
   >Comme cette règle présente un ordre supérieur, elle remplacera le jeu de `eventType` défini dans la règle « Configuration globale ». `eventType` ne peut contenir qu’une seule valeur et nous vous recommandons de la définir avec l’événement le plus important.

   >[!TIP]
   >
   >La définition de commerce.productViews.value=1 dans XDM mappe automatiquement à l’événement `prodView` dans Analytics


### Champs Panier

Vous pouvez mapper un tableau entier à un objet XDM, à condition que le tableau corresponde au format du schéma XDM. L’élément de données de code personnalisé `Ecommerce Cart Products` vous avez créé précédemment effectue une boucle sur l’objet de couche de données `adobeDataLayer.ecommerce.cart.items` sur le site web de Luma et le traduit au format requis de l’objet `productListItems` du schéma XDM.

Pour illustrer cette situation, reportez-vous à la comparaison ci-dessous de la couche de données de site Luma (à gauche) avec l’élément de données traduit (à droite) :

![Format de tableau d’objets XDM](assets/data-element-xdm-array.png)

Comparez l’élément de données à la structure `productListItems` (conseil, il doit correspondre).

>[!IMPORTANT]
>
>Notez la manière dont les variables numériques sont traduites, avec des valeurs de chaîne dans la couche de données telles que `price` et `qty` reformatées en nombres dans l’élément de données. Ces exigences de format sont importantes pour l’intégrité des données dans Platform et sont déterminées lors de l’étape [configurer les schémas](configure-schemas.md). Dans l’exemple, **[!UICONTROL quantity]** utilise le type de données **[!UICONTROL Integer]**.
> ![Type de données de schéma XDM](assets/set-up-analytics-quantity-integer.png)

Maintenant, mappons notre tableau à l’objet XDM :


1. Créez une règle nommée `cart page - adobeDataLayer push - set cart variables - 20`
1. Sélectionnez le symbole ![+ sous Événement &#x200B;](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) ajouter un nouveau déclencheur
1. Sous **[!UICONTROL Extension]**, sélectionnez **[!UICONTROL Couche de données client Adobe]**
1. Sous **[!UICONTROL Type d’événement]**, sélectionnez **[!UICONTROL Données transmises]**
1. Sélectionnez pour ouvrir **[!UICONTROL Options avancées]**, puis saisissez `20`. Cette valeur d’ordre garantit que la règle s’exécute _après_ la règle des variables globales.
1. Écoute d’un événement **[!UICONTROL spécifique]**
1. Saisissez `cartView` comme **[!UICONTROL Événement/Clé pour lequel s’enregistrer]**
1. Sélectionnez **[!UICONTROL Conserver les modifications]**


   ![Règle Événement pour le panier](assets/rule-cart-event.png)

1. Sous **[!UICONTROL Actions]** sélectionnez **[!UICONTROL Ajouter]**
1. Sélectionner l’extension **[!UICONTROL Adobe Experience Platform Web SDK]**
1. Sélectionnez **[!UICONTROL Type d’action]** comme **[!UICONTROL Variable de mise à jour]**
1. Sélectionnez `XDM Variable` comme **[!UICONTROL Élément de données]**
1. Mappez ces champs XDM aux valeurs appropriées :

   | Champ XDM | Mapper à |
   |---|---|
   | `eventType` | `Commerce Product List (Cart) Views` (commencez à saisir pour voir les valeurs suggérées) |
   | `commerce.productListViews.value` | `1` |
   | `productListItems.name` | `Ecommerce Product Name` (Sélectionnez **[!UICONTROL Fournir des éléments individuels]** et **[!UICONTROL Ajouter un élément]** en premier ) |
   | `productListItems.sku` | `Ecommerce Product Id` |



   >[!TIP]
   >
   >La définition de commerce.productListViews.value=1 dans XDM mappe automatiquement à l’événement `scView` dans Analytics

1. Sélectionnez `eventType` et définissez sur `commerce.productListViews`

1. Faites défiler jusqu’à et sélectionnez le tableau **[!UICONTROL productListItems]**

1. Sélectionnez **[!UICONTROL Fournir un tableau entier]**

1. Mapper à **`cart.productInfo`** élément de données

1. Sélectionnez **[!UICONTROL Conserver les modifications]**

1. Sélectionnez **[!UICONTROL Enregistrer]** pour enregistrer la règle

Créez deux autres règles pour le passage en caisse et l’achat selon le même modèle avec les différences ci-dessous :

**Nom de la règle** : `ecommerce  - library loaded - set checkout variables - 20`

1. **[!UICONTROL Condition]** : /content/luma/us/en/user/checkout.html
1. Définissez `eventType` sur `commerce.checkouts`.
1. Définissez `commerce.checkout.value` sur `1`.

   >[!TIP]
   >
   >Cela revient à définir `scCheckout` événement dans Analytics


**Nom de la règle** : `ecommerce - library loaded - set purchase variables -  20`

1. **[!UICONTROL Condition]** : /content/luma/us/en/user/checkout/order/thank-you.html
1. Définissez `eventType` sur `commerce.purchases`.
1. Définissez `commerce.purchases.value` sur `1`.

   >[!TIP]
   >
   >Cela revient à définir `purchase` événement dans Analytics

1. `commerce.order.purchaseID` à l’élément de données `cart.orderId`
1. Définissez `commerce.order.currencyCode` sur la valeur codée en dur `USD`

   ![Définition de purchaseID pour Analytics](assets/set-up-analytics-purchase.png)

   >[!TIP]
   >
   >Cela revient à définir des variables `s.purchaseID` et `s.currencyCode` dans Analytics

1. Faites défiler jusqu’à et sélectionnez le tableau **[!UICONTROL productListItems]**
1. Sélectionnez **[!UICONTROL Fournir un tableau entier]**
1. Mapper à **`cart.productInfo.purchase`** élément de données
1. Sélectionnez **[!UICONTROL Conserver les modifications]**
1. Sélectionnez **[!UICONTROL Enregistrer]**

Lorsque vous avez terminé, vous devriez voir les règles suivantes créées.

![Règles XDM Analytics](assets/set-up-analytics-rules.png)


### Règle d’événement d’envoi

Maintenant que vous avez défini les variables, vous pouvez créer la règle pour envoyer l’objet XDM complet à Platform Edge Network avec l’action **[!UICONTROL Envoyer l’événement]**.

1. Sur la droite, sélectionnez **[!UICONTROL Ajouter une règle]** pour créer une autre règle

1. Donnez à la règle le nom `all pages - library loaded - send event - 50`.

1. Dans la section **[!UICONTROL Événements]**, sélectionnez **[!UICONTROL Ajouter]**

1. Utilisez l’extension **[!UICONTROL Core]** et sélectionnez `Library Loaded (Page Top)` comme **[!UICONTROL type d’événement]**.

1. Sélectionnez la liste déroulante **[!UICONTROL Avancé]** et saisissez `50` dans **[!UICONTROL Ordre]**. Cela permet de s’assurer que cette règle se déclenche après toutes les autres règles que vous avez configurées (dont le `1`Ordre`20` était [!UICONTROL &#x200B; ou &#x200B;]).

1. Sélectionnez **[!UICONTROL Conserver les modifications]** pour revenir à l’écran principal des règles
   ![Sélectionner le déclencheur de bibliothèque chargé](assets/create-tag-rule-trigger-loaded-send.png)

1. Dans la section **[!UICONTROL Actions]**, sélectionnez **[!UICONTROL Ajouter]**

1. Sélectionnez **[!UICONTROL Adobe Experience Platform Web SDK en tant qu’extension]**&#x200B;**&#x200B;**

1. Sélectionnez **[!UICONTROL Type d’action]**, **[!UICONTROL Envoyer l’événement]**

1. En tant que **[!UICONTROL XDM]**, sélectionnez l’élément de données `xdm.variable.content` créé dans la leçon précédente

1. Sélectionnez **[!UICONTROL Conserver les modifications]** pour revenir à l’écran principal des règles

   ![Ajouter l’action Envoyer l’événement](assets/create-rule-send-event-action.png)
1. Sélectionnez **[!UICONTROL Enregistrer]** pour enregistrer la règle

   ![Enregistrer la règle](assets/create-rule-save-rule.png)

## Publication des règles dans une bibliothèque

Publiez ensuite la règle dans votre environnement de développement afin de vérifier qu’elle fonctionne.

Pour créer une bibliothèque, procédez comme suit :

1. Accédez à **[!UICONTROL Flux de publication]** dans le volet de navigation de gauche

1. Sélectionnez **[!UICONTROL Ajouter une bibliothèque]**

   ![Sélectionnez Ajouter une bibliothèque](assets/rule-publish-library.png)
1. Pour le **[!UICONTROL Nom]**, saisissez `Luma Web SDK Tutorial`
1. Pour le **[!UICONTROL Environnement]**, sélectionnez `Development`
1. Sélectionnez **[!UICONTROL Ajouter toutes les ressources modifiées]**

   >[!NOTE]
   >
   >    Vous devriez voir tous les composants de balise créés dans les leçons précédentes. L’extension Core contient le JavaScript de base requis par toutes les propriétés de balise web.

1. Sélectionnez **[!UICONTROL Enregistrer et créer pour le développement]**

   ![Création et génération de la bibliothèque](assets/create-tag-rule-library-changes.png)

La création de la bibliothèque peut prendre quelques minutes et, lorsqu’elle est terminée, un point vert s’affiche à gauche du nom de la bibliothèque :

![Création terminée](assets/create-rule-development-success.png)

Comme vous pouvez le voir dans l’écran [!UICONTROL Flux de publication], le processus de publication ne se limite pas au contenu de ce tutoriel. Ce tutoriel utilise uniquement une bibliothèque dans votre environnement de développement.

Vous êtes maintenant prêt à valider les données de la requête à l’aide d’Adobe Experience Platform Debugger.

>[!NOTE]
>
>Merci d’avoir investi votre temps dans votre apprentissage de Adobe Experience Platform Web SDK. Si vous avez des questions, souhaitez partager des commentaires généraux ou avez des suggestions sur le contenu futur, veuillez les partager dans ce [article de discussion de la communauté Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996)
