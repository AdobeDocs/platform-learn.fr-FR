---
title: Création de règles de balise pour le SDK Web Platform
description: Découvrez comment envoyer un événement à l’Edge Network Platform avec votre objet XDM à l’aide d’une règle de balise. Cette leçon fait partie du tutoriel Implémentation d’Adobe Experience Cloud avec le SDK web.
feature: Tags
jira: KT-15403
exl-id: e06bad06-3ee3-475f-9b10-f0825a48a312
source-git-commit: a8431137e0551d1135763138da3ca262cb4bc4ee
workflow-type: tm+mt
source-wordcount: '1983'
ht-degree: 2%

---

# Création de règles de balise

Découvrez comment envoyer des événements à l’Edge Network Adobe Experience Platform avec votre objet XDM à l’aide de règles de balise. Une règle de balise est une combinaison d’événements, de conditions et d’actions qui indique à la propriété de balise de faire quelque chose. Avec le SDK Web Platform, les règles sont utilisées pour envoyer des événements à l’Edge Network Platform avec les données appropriées.

## Objectifs d&#39;apprentissage

À la fin de cette leçon, vous pouvez :

* Utilisation d’une convention d’affectation de nom pour la gestion des règles dans les balises
* Envoi d’un événement avec des champs XDM à l’aide des actions Mettre à jour la variable et Envoyer un événement
* Empiler plusieurs jeux de champs XDM dans plusieurs règles
* Mappage d’éléments de données de tableau individuels ou entiers à l’objet XDM
* Publish d’une règle de balise à une bibliothèque de développement


## Conditions préalables

Vous connaissez les balises de collecte de données et le [site de démonstration Luma](https://luma.enablementadobe.com/content/luma/us/en.html) et avez terminé les leçons précédentes du tutoriel :

* [Configurer un schéma XDM](configure-schemas.md)
* [Configuration d’un espace de noms d’identité](configure-identities.md)
* [Configurer un trains de données](configure-datastream.md)
* [Installer l’extension SDK Web](install-web-sdk.md)
* [Création d’éléments de données](create-data-elements.md)
* [Création d’identités](create-identities.md)

## Conventions de dénomination

Pour gérer les règles dans les balises, il est recommandé de respecter une convention d’affectation de nom standard. Ce tutoriel utilise une convention de dénomination en cinq parties :

* [**location**] - [**event**] - [**purpose**] - [**order**]

où ;

1. **location** correspond à la ou aux pages du site sur lequel la règle se déclenche.
1. **event** est le déclencheur de la règle
1. **purpose** est l’action principale effectuée par la règle.
1. **order** est l’ordre dans lequel la règle doit se déclencher par rapport aux autres règles.
<!-- minor update -->

## Création de règles de balise

Dans les balises, les règles sont utilisées pour exécuter des actions (appels de déclenchement) sous diverses conditions. L’extension de balises SDK Web Platform comprend deux actions utilisées dans cette leçon :

* **[!UICONTROL La variable de mise à jour]** mappe des éléments de données aux propriétés dans un objet XDM
* **[!UICONTROL Envoyer l’événement]** envoie l’objet XDM à l’Edge Network Experience Platform

Dans le reste de cette leçon, nous :

1. Créez une règle avec l’action **[!UICONTROL Mettre à jour la variable]** pour définir une &quot;configuration globale&quot; des champs XDM.

1. Créez des règles supplémentaires avec l’action **[!UICONTROL Mettre à jour la variable]** qui remplacent notre &quot;configuration globale&quot; et contribuez à des champs XDM supplémentaires sous certaines conditions (par exemple, en ajoutant des détails sur les produits sur les pages de produits).

1. Créez une autre règle avec l’action **[!UICONTROL Envoyer l’événement]**, qui enverra l’objet XDM complet à l’Edge Network Adobe Experience Platform.

Toutes ces règles seront séquencées correctement à l’aide de l’option &quot;[!UICONTROL order]&quot;.

Cette vidéo donne un aperçu du processus :

>[!VIDEO](https://video.tv.adobe.com/v/3427710/?learn=on)

### Champs de configuration globaux

Pour créer une règle de balise pour les champs XDM globaux :

1. Ouvrez la propriété de balise que vous utilisez pour ce tutoriel.

1. Accédez à **[!UICONTROL Rules]** dans le volet de navigation de gauche.

1. Sélectionnez le bouton **[!UICONTROL Créer une règle]**

   ![Créer une règle](assets/rules-create.png)

1. Donnez à la règle le nom `all pages - library loaded - set global variables - 1`.

1. Dans la section **[!UICONTROL Events]** , sélectionnez **[!UICONTROL Add]**

   ![Nommez la règle et ajoutez un événement](assets/rule-name-new.png)

1. Utilisez l’ **[!UICONTROL extension Core]** et sélectionnez **[!UICONTROL Library Loaded (Page Top)]** comme **[!UICONTROL Event Type]** (Type d’événement)

1. Sélectionnez la liste déroulante **[!UICONTROL Avancé]** et saisissez `1` comme **[!UICONTROL Commande]**

   >[!NOTE]
   >
   > Plus le numéro de commande est bas, plus tôt il s’exécute. Par conséquent, nous donnons à notre &quot;configuration globale&quot; un numéro de commande faible.

1. Sélectionnez **[!UICONTROL Conserver les modifications]** pour revenir à l’écran de règle principal.
   ![Sélectionner le déclencheur chargé de bibliothèque](assets/create-tag-rule-trigger-loaded.png)

1. Dans la section **[!UICONTROL Actions]** , sélectionnez **[!UICONTROL Ajouter]**

1. En tant que **[!UICONTROL extension]**, sélectionnez **[!UICONTROL Adobe Experience Platform Web SDK]**

1. En tant que **[!UICONTROL Type d’action]**, sélectionnez **[!UICONTROL Mettre à jour la variable]**

1. En tant qu&#39; **[!UICONTROL élément de données]**, sélectionnez l&#39; `xdm.variable.content` que vous avez créé dans la leçon [Créer des éléments de données](create-data-elements.md).

   ![Mettre à jour le schéma de variable](assets/create-rule-update-variable.png)

Maintenant, mappez vos [!UICONTROL éléments de données] avec le [!UICONTROL schéma] utilisé par votre objet XDM. Vous pouvez mapper des propriétés individuelles ou des objets entiers. Dans cet exemple, vous mappez les propriétés individuelles :

1. Recherchez le champ eventType et sélectionnez-le

1. Saisissez la valeur `web.webpagedetails.pageViews`

   >[!TIP]
   >
   > Pour comprendre les valeurs à renseigner dans le champ `eventType`, vous devez accéder à la page de schéma et sélectionner le champ `eventType` pour afficher les valeurs suggérées sur le rail de droite. Vous pouvez également saisir une nouvelle valeur, si nécessaire.
   > ![eventType valeurs suggérées sur la page des schémas](assets/create-tag-rule-eventType.png)

1. Recherchez ensuite l’objet `identityMap` dans le schéma et sélectionnez-le.

1. Associer à l’élément de données `identityMap.loginID`

   ![ Mettre à jour la carte d’identité des variables ](assets/create-rule-variable-identityMap.png)


   >[!TIP]
   >
   > Les champs XDM ne seront pas inclus dans la requête réseau si l’élément de données est nul. Par conséquent, lorsque l’utilisateur n’est pas authentifié et que l’élément de données `identityMap.loginID` est nul, l’objet `identityMap` ne sera pas envoyé. C&#39;est pourquoi nous pouvons le définir dans notre &quot;configuration globale&quot;.

1. Faites défiler l’écran vers le bas jusqu’à ce que vous atteigniez l’objet **`web`**

1. Sélectionner pour l’ouvrir

1. Mappez les éléments de données suivants aux variables XDM `web` correspondantes

   * **`web.webPageDetials.name`** à `%page.pageInfo.pageName%`
   * **`web.webPageDetials.server`** à `%page.pageInfo.server%`
   * **`web.webPageDetials.siteSection`** à `%page.pageInfo.hierarchie1%`

1. Définissez `web.webPageDetials.pageViews.value` sur `1`.

   ![Mettre à jour le contenu de la variable](assets/create-rule-xdm-variable-content.png)

   >[!TIP]
   >
   > Bien qu’Adobe Analytics n’ait pas besoin de `eventType` défini sur `web.webpagedetails.pageViews` ni de `web.webPageDetails.pageViews.value` pour traiter une balise en tant que page vue, il est utile d’avoir une méthode standard pour indiquer une page vue pour d’autres applications en aval.


1. Sélectionnez **[!UICONTROL Conserver les modifications]**, puis **[!UICONTROL Enregistrer]** la règle dans l’écran suivant pour terminer la création de la règle.


### Champs de page de produit

Maintenant, commencez à utiliser **[!UICONTROL Mettre à jour la variable]** dans des règles séquencées supplémentaires pour enrichir l’objet XDM avant de l’envoyer à [!UICONTROL Platform Edge Network].

>[!TIP]
>
>L’ordre des règles détermine la règle qui s’exécute en premier lorsqu’un événement est déclenché. Si deux règles possèdent le même type d’événement, celle dont le nombre est le plus faible s’exécute en premier.
> 

Commencez par effectuer le suivi des consultations de produit sur la page des détails du produit de Luma :

1. Sélectionnez **[!UICONTROL Ajouter une règle]**
1. Nommez-le [!UICONTROL `ecommerce - library loaded - set product details variables - 20`]
1. Sélectionnez le ![+ symbole](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) sous Événement pour ajouter un nouveau déclencheur.
1. Sous **[!UICONTROL Extension]**, sélectionnez **[!UICONTROL Core]**
1. Sous **[!UICONTROL Event Type]**, sélectionnez **[!UICONTROL Library Loaded (Page Top)]** (Bibliothèque chargée (Haut de page))
1. Sélectionnez pour ouvrir **[!UICONTROL Options avancées]**, saisissez `20`. Cette valeur de commande garantit que la règle s’exécute _après_ l’ `all pages - library loaded - set global variables - 1` qui définit la configuration globale.
1. Sélectionnez **[!UICONTROL Keep changes]**

   ![Règles XDM Analytics](assets/set-up-analytics-pdp.png)

1. Sous **[!UICONTROL Conditions]**, sélectionnez **[!UICONTROL Ajouter]**
1. Laissez **[!UICONTROL Type logique]** sur **[!UICONTROL Normal]**
1. Laissez **[!UICONTROL Extension]** sur **[!UICONTROL Core]**
1. Sélectionnez **[!UICONTROL Type de condition]** comme **[!UICONTROL Chemin sans chaîne de requête]**
1. Sur la droite, activez le bouton bascule **[!UICONTROL Regex]**
1. Sous **[!UICONTROL path equals]** set `/products/`. Pour le site de démonstration Luma, la règle se déclenche uniquement sur les pages de produits.
1. Sélectionnez **[!UICONTROL Conserver les modifications]**

   ![Règles XDM Analytics](assets/set-up-analytics-product-condition.png)

1. Sous **[!UICONTROL Actions]**, sélectionnez **[!UICONTROL Ajouter]**
1. Sélectionnez l’extension **[!UICONTROL Adobe Experience Platform Web SDK]**
1. Sélectionnez **[!UICONTROL Action Type]** comme **[!UICONTROL Mise à jour de variable]**
1. Sélectionnez `xdm.variable.content` comme **[!UICONTROL élément de données]**
1. Faites défiler jusqu’à l’objet `commerce`
1. Ouvrez l’objet **[!UICONTROL productViews]** et définissez **[!UICONTROL value]** sur `1`

   ![ Configuration de la consultation de produit ](assets/set-up-analytics-prodView.png)

   >[!TIP]
   >
   >La définition de commerce.productViews.value=1 dans XDM correspond automatiquement à l’événement `prodView` dans Analytics.

1. Faites défiler l’écran jusqu’à `eventType` et définissez-le sur `commerce.productViews`

   >[!NOTE]
   >
   >Comme cette règle a un ordre plus élevé, elle remplacera le `eventType` défini dans la règle &quot;configuration globale&quot;. `eventType` ne peut contenir qu’une seule valeur et nous vous recommandons de la définir avec l’événement le plus précieux.

1. Faites défiler l’écran jusqu’à et sélectionnez le tableau `productListItems`
1. Sélectionnez **[!UICONTROL Fournir des éléments individuels]**
1. Sélectionnez **[!UICONTROL Ajouter un élément]**

   ![Définition de l’événement d’affichage de produit](assets/set-up-analytics-xdm-individual.png)

   >[!CAUTION]
   >
   >**`productListItems`** est un type de données `array` qui s’attend donc à ce que les données entrent en tant que collection d’éléments. En raison de la structure de couche de données du site de démonstration Luma et parce qu’il est possible d’afficher un seul produit à la fois sur le site Luma, vous ajoutez des éléments individuellement. Lors de l’implémentation sur votre propre site web, en fonction de la structure de votre couche de données, vous pouvez fournir un tableau entier.

1. Sélectionnez pour ouvrir **[!UICONTROL Item 1]**
1. Mapper **`productListItems.item1.SKU`** à `%product.productInfo.sku%`

   ![Variable d’objet XDM SKU du produit](assets/set-up-analytics-sku.png)

1. Sélectionnez **[!UICONTROL Conserver les modifications]**

1. Sélectionnez **[!UICONTROL Enregistrer]** pour enregistrer la règle.


### Champs du panier

Vous pouvez mapper un tableau entier à un objet XDM, à condition que le tableau corresponde au format du schéma XDM. L’élément de données de code personnalisé `cart.productInfo` que vous avez créé précédemment effectue des boucles à travers l’objet de couche de données `digitalData.cart.cartEntries` sur Luma et le convertit au format requis de l’objet `productListItems` du schéma XDM.

Pour illustrer cela, reportez-vous à la comparaison ci-dessous de la couche de données du site Luma (à gauche) avec l’élément de données traduit (à droite) :

![Format de tableau d’objet XDM](assets/data-element-xdm-array.png)

Comparez l’élément de données à la structure `productListItems` (indice, il doit correspondre).

>[!IMPORTANT]
>
>Notez comment les variables numériques sont traduites, avec des valeurs de chaîne dans la couche de données telles que `price` et `qty` reformatées en nombres dans l’élément de données. Ces exigences de format sont importantes pour l’intégrité des données dans Platform et sont déterminées à l’étape [configurer les schémas](configure-schemas.md) . Dans cet exemple, **[!UICONTROL quantity]** utilise le type de données **[!UICONTROL Integer]** .
> ![Type de données de schéma XDM](assets/set-up-analytics-quantity-integer.png)

Mappons maintenant notre tableau à l’objet XDM :


1. Créez une nouvelle règle nommée `ecommerce - library loaded - set shopping cart variables - 20`
1. Sélectionnez le ![+ symbole](https://spectrum.adobe.com/static/icons/workflow_18/Smock_AddCircle_18_N.svg) sous Événement pour ajouter un nouveau déclencheur.
1. Sous **[!UICONTROL Extension]**, sélectionnez **[!UICONTROL Core]**
1. Sous **[!UICONTROL Event Type]**, sélectionnez **[!UICONTROL Library Loaded (Page Top)]** (Bibliothèque chargée (Haut de page))
1. Sélectionnez pour ouvrir **[!UICONTROL Options avancées]**, saisissez `20`
1. Sélectionnez **[!UICONTROL Conserver les modifications]**

   ![Règles XDM Analytics](assets/set-up-analytics-cart-sequence.png)

1. Sous **[!UICONTROL Conditions]**, sélectionnez **[!UICONTROL Ajouter]**
1. Laissez **[!UICONTROL Type logique]** sur **[!UICONTROL Normal]**
1. Laissez **[!UICONTROL Extensions]** comme **[!UICONTROL Core]**
1. Sélectionnez **[!UICONTROL Type de condition]** comme **[!UICONTROL Chemin sans chaîne de requête]**
1. À droite, **n’activez pas** le bouton bascule **[!UICONTROL Regex]**
1. Sous **[!UICONTROL path equals]** set `/content/luma/us/en/user/cart.html`. Pour le site de démonstration Luma, la règle se déclenche uniquement sur la page de panier.
1. Sélectionnez **[!UICONTROL Conserver les modifications]**

   ![Règles XDM Analytics](assets/set-up-analytics-cart-condition.png)

1. Sous **[!UICONTROL Actions]**, sélectionnez **[!UICONTROL Ajouter]**
1. Sélectionnez l’extension **[!UICONTROL Adobe Experience Platform Web SDK]**
1. Sélectionnez **[!UICONTROL Action Type]** comme **[!UICONTROL Mise à jour de variable]**
1. Sélectionnez `xdm.variable.content` comme **[!UICONTROL élément de données]**
1. Faites défiler l’écran jusqu’à l’objet `commerce` et sélectionnez-le pour l’ouvrir.
1. Ouvrez l’objet **[!UICONTROL productListViews]** et définissez **[!UICONTROL value]** sur `1`.

   ![ Configuration de la consultation de produit ](assets/set-up-analytics-cart-view.png)

   >[!TIP]
   >
   >La définition de commerce.productListViews.value=1 dans XDM correspond automatiquement à l’événement `scView` dans Analytics.

1. Sélectionnez `eventType` et définissez sur `commerce.productListViews`

1. Faites défiler l’écran jusqu’au tableau **[!UICONTROL productListItems]** et sélectionnez-le

1. Sélectionnez **[!UICONTROL Fournir un tableau entier]**

1. Associer à l’élément de données **`cart.productInfo`**

1. Sélectionnez **[!UICONTROL Conserver les modifications]**

1. Sélectionnez **[!UICONTROL Enregistrer]** pour enregistrer la règle.

Créez deux autres règles pour le passage en caisse et l’achat suivant le même modèle avec les différences suivantes :

**Nom de la règle** : `ecommerce  - library loaded - set checkout variables - 20`

1. **[!UICONTROL Condition]** : /content/luma/us/en/user/checkout.html
1. Définissez `eventType` sur `commerce.checkouts`.
1. Définissez `commerce.checkout.value` sur `1`.

   >[!TIP]
   >
   >Cela équivaut à définir l’événement `scCheckout` dans Analytics.


**Nom de la règle** : `ecommerce - library loaded - set purchase variables -  20`

1. **[!UICONTROL Condition]** : /content/luma/us/en/user/checkout/order/thank-you.html
1. Définissez `eventType` sur `commerce.purchases`.
1. Définissez `commerce.purchases.value` sur `1`.

   >[!TIP]
   >
   >Cela équivaut à définir l’événement `purchase` dans Analytics.

1. Définissez `commerce.order.purchaseID` sur l’élément de données `cart.orderId`
1. Définissez `commerce.order.currencyCode` sur la valeur codée en dur `USD`

   ![Définition de purchaseID pour Analytics](assets/set-up-analytics-purchase.png)

   >[!TIP]
   >
   >Cela équivaut à définir des variables `s.purchaseID` et `s.currencyCode` dans Analytics.

1. Faites défiler l’écran jusqu’au tableau **[!UICONTROL productListItems]** et sélectionnez-le
1. Sélectionnez **[!UICONTROL Fournir un tableau entier]**
1. Associer à l’élément de données **`cart.productInfo.purchase`**
1. Sélectionnez **[!UICONTROL Conserver les modifications]**
1. Sélectionnez **[!UICONTROL Save]**

Lorsque vous avez terminé, les règles suivantes doivent être créées.

![Règles XDM Analytics](assets/set-up-analytics-rules.png)


### Envoyer la règle d’événement

Maintenant que vous avez défini les variables, vous pouvez créer la règle pour envoyer l’objet XDM complet à l’Edge Network Platform avec l’action **[!UICONTROL Envoyer l’événement]**.

1. À droite, sélectionnez **[!UICONTROL Ajouter une règle]** pour créer une autre règle.

1. Donnez à la règle le nom `all pages - library loaded - send event - 50`.

1. Dans la section **[!UICONTROL Events]** , sélectionnez **[!UICONTROL Add]**

1. Utilisez **[!UICONTROL Core Extension]** et sélectionnez `Library Loaded (Page Top)` comme **[!UICONTROL Event Type]**

1. Sélectionnez la liste déroulante **[!UICONTROL Avancé]** et saisissez `50` dans **[!UICONTROL Ordre]**. Cette règle se déclenche après toutes les autres règles que vous avez configurées (dont `1` ou `20` comme [!UICONTROL Commande]).

1. Sélectionnez **[!UICONTROL Conserver les modifications]** pour revenir à l’écran de règle principal.
   ![Sélectionner le déclencheur chargé de bibliothèque](assets/create-tag-rule-trigger-loaded-send.png)

1. Dans la section **[!UICONTROL Actions]** , sélectionnez **[!UICONTROL Ajouter]**

1. En tant que **[!UICONTROL extension]**, sélectionnez **[!UICONTROL Adobe Experience Platform Web SDK]**

1. En tant que **[!UICONTROL Type d’action]**, sélectionnez **[!UICONTROL Send event]**

1. En tant que **[!UICONTROL XDM]**, sélectionnez l’élément de données `xdm.variable.content` créé dans la leçon précédente.

1. Sélectionnez **[!UICONTROL Conserver les modifications]** pour revenir à l’écran de règle principal.

   ![Ajouter l’action Envoyer l’événement](assets/create-rule-send-event-action.png)
1. Sélectionnez **[!UICONTROL Enregistrer]** pour enregistrer la règle.

   ![Enregistrer la règle](assets/create-rule-save-rule.png)

## Publish des règles dans une bibliothèque

Ensuite, publiez la règle dans votre environnement de développement afin que vous puissiez vérifier qu’elle fonctionne.

Pour créer une bibliothèque :

1. Accédez à **[!UICONTROL Flux de publication]** dans le volet de navigation de gauche.

1. Sélectionnez **[!UICONTROL Ajouter une bibliothèque]**

   ![Sélectionner Ajouter une bibliothèque](assets/rule-publish-library.png)
1. Pour le **[!UICONTROL Nom]**, saisissez `Luma Web SDK Tutorial`
1. Pour l’ **[!UICONTROL environnement]**, sélectionnez `Development`
1. Sélectionnez **[!UICONTROL Ajouter toutes les ressources modifiées]**

   >[!NOTE]
   >
   >    Vous devriez voir tous les composants de balise créés dans les leçons précédentes. L’extension Core contient le JavaScript de base requis par toutes les propriétés de balise web.

1. Sélectionnez **[!UICONTROL Enregistrer et créer pour le développement]**

   ![Créer et créer la bibliothèque](assets/create-tag-rule-library-changes.png)

La création de la bibliothèque peut prendre quelques minutes. Une fois l’opération terminée, un point vert s’affiche à gauche du nom de la bibliothèque :

![Build complete](assets/create-rule-development-success.png)

Comme vous pouvez le constater sur l’écran [!UICONTROL Flux de publication], le processus de publication ne s’étend pas au-delà de la portée de ce tutoriel. Ce tutoriel utilise une seule bibliothèque dans votre environnement de développement.

Vous êtes maintenant prêt à valider les données de la requête à l’aide de l’Adobe Experience Platform Debugger .

[Suivant ](validate-with-debugger.md)

>[!NOTE]
>
>Merci d’avoir consacré du temps à l’apprentissage du SDK Web Adobe Experience Platform. Si vous avez des questions, souhaitez partager des commentaires généraux ou avez des suggestions sur le contenu à venir, partagez-les sur cet [post de discussion de la communauté Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996)
