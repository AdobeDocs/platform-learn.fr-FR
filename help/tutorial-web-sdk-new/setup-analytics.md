---
title: Configuration d’Adobe Analytics à l’aide du SDK Web Experience Platform
description: Découvrez comment configurer Adobe Analytics à l’aide du SDK Web Experience Platform. Cette leçon fait partie du tutoriel Mise en oeuvre de Adobe Experience Cloud avec le SDK Web .
solution: Data Collection, Analytics
exl-id: e08d222c-a15f-4462-b033-99937d741d5e
source-git-commit: 5e778dde1698110fade7163ed2585f059c27274c
workflow-type: tm+mt
source-wordcount: '2803'
ht-degree: 1%

---

# Configuration d’Adobe Analytics avec le SDK Web de Platform

Découvrez comment configurer Adobe Analytics à l’aide de [SDK Web Experience Platform](https://experienceleague.adobe.com/docs/platform-learn/data-collection/web-sdk/overview.html?lang=fr), créez des règles de balise pour envoyer des données à Adobe Analytics et vérifiez qu’Analytics capture les données comme prévu.

[Adobe Analytics](https://experienceleague.adobe.com/docs/analytics.html?lang=fr) est une application de pointe qui vous permet de comprendre vos clients en tant que personnes et d’orienter votre activité grâce aux renseignements sur vos clients.

![Diagramme SDK Web vers Adobe Analytics](assets/dc-websdk-aa.png)

## Objectifs d&#39;apprentissage

À la fin de cette leçon, vous saurez comment :

* Configuration d’un flux de données pour activer Adobe Analytics
* Identifier les champs XDM standard qui seront automatiquement mappés aux variables Analytics
* Définissez des variables Analytics personnalisées à l’aide du groupe de champs Modèle Adobe Analytics ExperienceEvent ou des règles de traitement.
* Envoi de données vers une autre suite de rapports en remplaçant le flux de données
* Validation des variables Adobe Analytics à l’aide de Debugger et d’Assurance

## Conditions préalables

Pour terminer cette leçon, vous devez d’abord :

* Familiarisez-vous avec Adobe Analytics et accédez-y.

* posséder au moins un identifiant de suite de rapports de test/développement. Si vous ne disposez pas d’une suite de rapports de test/développement que vous pouvez utiliser pour ce tutoriel, [créez-en une](https://experienceleague.adobe.com/docs/analytics/admin/manage-report-suites/new-report-suite/t-create-a-report-suite.html?lang=fr).

* Suivez les leçons des sections Configuration initiale et Configuration des balises de ce tutoriel.

## Configuration du flux de données

Le SDK Web Platform envoie les données de votre site Web à l’Edge Network Platform. Votre flux de données indique ensuite à l’Edge Network Platform à quelles suites de rapports Adobe Analytics vos données doivent être transférées.

1. Accédez à [Collecte de données](https://experience.adobe.com/#/data-collection){target="blank"} interface
1. Dans le volet de navigation de gauche, sélectionnez **[!UICONTROL Datastreams]**
1. Sélectionnez la `Luma Web SDK: Development Environment` datastream

   ![Sélectionnez la flux de données du SDK Web Luma.](assets/datastream-luma-web-sdk-development.png)

1. Sélectionnez **[!UICONTROL Ajouter un service]**.
   ![Ajout d’un service au flux de données](assets/datastream-analytics-addService.png)
1. Sélectionner **[!UICONTROL Adobe Analytics]** comme la propriété **[!UICONTROL Service]**
1. Saisissez le  **[!UICONTROL Identifiant de suite de rapports]** de votre suite de rapports de développement
1. Sélectionnez **[!UICONTROL Enregistrer]**.

   ![Analyse de l’enregistrement des flux de données](assets/datastream-add-analytics.png)

   >[!TIP]
   >
   >Pour ajouter d’autres suites de rapports, sélectionnez **[!UICONTROL Ajouter une suite de rapports]** équivaut au balisage multisuite.

>[!WARNING]
>
>Dans ce tutoriel, vous configurez uniquement la suite de rapports Adobe Analytics pour votre environnement de développement. Lorsque vous créez des flux de données pour votre propre site web, vous créez des flux de données et des suites de rapports supplémentaires pour vos environnements d’évaluation et de production.

## Schémas XDM et variables Analytics

Félicitations ! Vous avez déjà configuré un schéma compatible avec Adobe Analytics dans la variable [Configuration d’un schéma](configure-schemas.md) leçon !

Mais vous vous demandez peut-être, comment définir toutes mes props, eVars et événements ?

Plusieurs méthodes peuvent être utilisées simultanément :

1. Définissez des champs XDM standard et certains mappent automatiquement aux variables Analytics.
1. Mappez des champs XDM supplémentaires aux variables Analytics dans les règles de traitement Analytics.
1. Associez-les aux variables Analytics directement dans le schéma XDM.

<!-- Implementing Platform Web SDK should be as product-agnostic as possible. For Adobe Analytics, mapping eVars, props, and events doesn't occur during schema creation, nor during the tag rules configuration as it has been done traditionally. Instead, every XDM key-value pair becomes a Context Data Variable that maps to an Analytics variable in one of two ways: 

1. Automatically mapped variables using reserved XDM fields
1. Manually mapped variables using Analytics Processing Rules

To understand what XDM variables are auto-mapped to Adobe Analytics, please see [Variables automatically mapped in Analytics](https://experienceleague.adobe.com/docs/experience-platform/edge/data-collection/adobe-analytics/automatically-mapped-vars.html?lang=en). Any variable that is not auto-mapped must be manually mapped. 

 1. **Product-agnostic XDM**: maintain a semantic key-value pair XDM schema and use [Adobe Analytics Processing Rules](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/c-processing-rules/processing-rules.html) to map the XDM fields to eVars, props, and so on. By a semantic XDM schema, we mean that the field names themselves have meaning. For example, the field name `web.webPageDetails.pageName` has more meaning than say `prop1` or `evar3`.


 1. **Analytics-specific XDM**: Use a purpose-built Adobe Analytics field group in the XDM schema called `Adobe Analytics ExperienceEvent Template`
 
The approach Adobe has seen customers prefer is the **Analytics-specific XDM**, because it skips the mapping step in the Adobe Analytics Processing Rules interface. The steps in this lesson use the **Analytics-specific XDM** approach.
-->

### Champs mappés automatiquement

De nombreux champs XDM sont automatiquement mappés aux variables Analytics.

Le schéma créé dans la variable [Configuration d’un schéma](configure-schemas.md) La leçon contient quelques variables mappées automatiquement aux variables Analytics, comme indiqué dans ce tableau :

| XDM vers les variables mappées automatiquement dans Analytics | Variable Adobe Analytics |
|-------|---------|
| `identitymap.ecid.[0].id` | mid |
| `web.webPageDetails.name` | s.pageName |
| `web.webPageDetails.server` | s.server |
| `web.webPageDetails.siteSection` | s.channel |
| `commerce.productViews.value` | prodView |
| `commerce.productListViews.value` | scView |
| `commerce.checkouts.value` | scCheckout |
| `commerce.purchases.value` | Achat |
| `commerce.order.currencyCode` | s.currencyCode |
| `commerce.order.purchaseID` | s.purchaseID |
| `productListItems[].SKU` | s.products=;product name;;; (primary - voir la remarque ci-dessous) |
| `productListItems[].name` | s.products=;product name;;; (fallback - voir la remarque ci-dessous) |
| `productListItems[].quantity` | s.products=;;quantité du produit;; |
| `productListItems[].priceTotal` | s.product=;;;prix du produit; |

Les sections individuelles de la chaîne de produit Analytics sont définies par le biais de différentes variables XDM sous la variable `productListItems` .
>Depuis le 18 août 2022, `productListItems[].SKU` est prioritaire pour le mappage au nom du produit dans la variable s.products .
>La valeur définie sur `productListItems[].name` est mappé sur le nom du produit uniquement si `productListItems[].SKU` n’existe pas. Dans le cas contraire, il n’est pas mappé et est disponible dans les données contextuelles.
>Ne définissez pas de chaîne vide ni de valeur nulle sur  `productListItems[].SKU`. Cela a pour effet indésirable de mapper le nom du produit dans la variable s.products .

Pour obtenir la liste des mappages la plus récente, reportez-vous à la section [Mappage des variables Analytics dans Adobe Experience Edge](https://experienceleague.adobe.com/docs/experience-platform/edge/data-collection/adobe-analytics/automatically-mapped-vars.html?lang=fr).


### Mise en correspondance avec les variables Analytics avec les règles de traitement

Tous les champs du schéma XDM deviennent disponibles pour Adobe Analytics en tant que variables de données contextuelles avec le préfixe suivant. `a.x.`. Par exemple : `a.x.web.webinteraction.region`

Dans cet exercice, vous mappez une variable XDM à une prop. Suivez les mêmes étapes que pour tout mappage personnalisé que vous devez effectuer pour n’importe quel mappage `eVar`, `prop`, `event`ou accessible via les règles de traitement.

1. Accès à l’interface d’Analytics
1. Accédez à [!UICONTROL Administration] > [!UICONTROL Outils d’administration] > [!UICONTROL Suites de rapports]
1. Sélectionnez la suite de rapports de développement/test que vous utilisez pour le tutoriel > [!UICONTROL Modifier les paramètres] > [!UICONTROL Général] > [!UICONTROL Règles de traitement]

   ![Achat Analytics](assets/analytics-process-rules.png)

1. Création d’une règle pour **[!UICONTROL Remplacer la valeur de]** `[!UICONTROL Product SKU (prop1)]` to `a.x.productlistitems.0.sku`. N’oubliez pas d’ajouter une note expliquant pourquoi vous créez la règle et nommez son titre. Sélectionnez **[!UICONTROL Enregistrer]**.

   ![Achat Analytics](assets/analytics-set-processing-rule.png)

   >[!IMPORTANT]
   >
   >La première fois que vous mappez à une règle de traitement, l’interface utilisateur ne vous affiche pas les variables de données contextuelles de l’objet XDM. Pour corriger les éléments qui sélectionnent une valeur, cliquez sur Enregistrer pour revenir à la modification. Toutes les variables XDM doivent maintenant apparaître.

### Mise en correspondance avec les variables Analytics à l’aide du groupe de champs Adobe Analytics

Une alternative aux règles de traitement consiste à mapper les variables Analytics dans le schéma XDM à l’aide de la variable `Adobe Analytics ExperienceEvent Template` groupe de champs. Cette approche a gagné en popularité car de nombreux utilisateurs la trouvent plus simple que de configurer des règles de traitement. Toutefois, en augmentant la taille de la payload XDM, elle peut augmenter la taille du profil dans d’autres applications comme Real-Time CDP.

Pour ajouter la variable `Adobe Analytics ExperienceEvent Template` groupe de champs à votre schéma :

1. Ouvrez le [Collecte de données](https://experience.adobe.com/#/data-collection){target="blank"} interface
1. Sélectionner **[!UICONTROL Schémas]** à partir du volet de navigation de gauche
1. Assurez-vous que vous êtes dans l’environnement de test que vous utilisez à partir du tutoriel
1. Ouvrez votre `Luma Web Event Data` schema
1. Dans le **[!UICONTROL Groupes de champs]** , sélectionnez **[!UICONTROL Ajouter]**
1. Recherchez le `Adobe Analytics ExperienceEvent Template` groupe de champs et l’ajouter à votre schéma


Définissez maintenant un eVar de marchandisage dans la chaîne de produit. Avec la variable `Adobe Analytics ExperienceEvent Template` groupe de champs, vous pouvez mapper des variables à des eVars de marchandisage ou des événements dans la chaîne de produit. On parle également de paramètre **Marchandisage Syntaxe du produit**.

1. Revenez à la propriété de balise.

1. Ouvrir la règle `ecommerce - library loaded - set product details variables - 20`

1. Ouvrez le **[!UICONTROL Définir la variable]** action

1. Sélectionner pour ouvrir `_experience > analytics > customDimensions > eVars > eVar1`

1. Définissez la variable **[!UICONTROL Valeur]** to `%product.productInfo.title%`

1. Sélectionner **[!UICONTROL Conserver les modifications]**

   ![Variable d’objet XDM SKU du produit](assets/set-up-analytics-product-merchandising.png)

1. Sélectionner **[!UICONTROL Enregistrer]** pour enregistrer la règle

Comme vous venez de le voir, pratiquement toutes les variables Analytics peuvent être définies dans la variable `Adobe Analytics ExperienceEvent Template` groupe de champs.

>[!NOTE]
>
> Remarquez que la variable `_experience` objet sous `productListItems` > `Item 1`. Définition de toute variable sous cette option [!UICONTROL objet] définit les eVars ou événements de syntaxe de produit.


## Envoi de données vers une autre suite de rapports

Vous pouvez modifier les données de suite de rapports Adobe Analytics envoyées aux visiteurs sur certaines pages. Cela nécessite une configuration dans le flux de données et une règle.

### Configuration du flux de données pour un remplacement de suite de rapports

Pour configurer un paramètre de remplacement de suite de rapports Adobe Analytics dans le flux de données :

1. Ouvrez votre flux de données.
1. Modifiez la variable **[!UICONTROL Adobe Analytics]** en ouvrant la ![more](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) puis en sélectionnant **[!UICONTROL Modifier]**

   ![Remplacer le flux de données](assets/datastream-edit-analytics.png)

1. Sélectionnez la variable **[!UICONTROL Options avancées]** pour ouvrir **[!UICONTROL Remplacements de suites de rapports]**

1. Sélectionnez les suites de rapports à remplacer. Dans ce cas, `Web SDK Course Dev` et `Web SDK Course Stg`

1. Sélectionnez **[!UICONTROL Enregistrer]**.

   ![Remplacer le flux de données](assets/analytics-datastreams-edit-adobe-analytics-configurations-report-suites.png)


### Configuration d’une règle pour un remplacement de suite de rapports

Créons une règle pour envoyer un appel de page vue supplémentaire à une autre suite de rapports. Utilisez la fonction de remplacement de la banque de données pour modifier la suite de rapports d’une page à l’aide de la variable **[!UICONTROL Envoyer un événement]** Action.

1. Créez une règle, nommez-la. `homepage - library loaded - AA report suite override - 51`

1. Sélectionnez le signe plus sous **[!UICONTROL Événement]** pour ajouter un nouveau déclencheur

1. Sous **[!UICONTROL Extension]**, sélectionnez **[!UICONTROL Core]**

1. Sous **[!UICONTROL Type d’événement]**, sélectionnez **[!UICONTROL bibliothèque chargée]**

1. Sélectionner pour ouvrir **[!UICONTROL Options avancées]**, saisissez `51`. Cela garantit que la règle s’exécute après la `all pages - library loaded - send event - 50` qui définit le XDM de ligne de base avec le **[!UICONTROL Mettre à jour la variable]** type d’action.

   ![Remplacement de suites de rapports Analytics](assets/set-up-analytics-rs-override.png)

1. Sous **[!UICONTROL Conditions]**, sélectionnez sur **[!UICONTROL Ajouter]**

1. Laisser **[!UICONTROL Type de logique]** as **[!UICONTROL Normal]**

1. Laisser **[!UICONTROL Extensions]** as **[!UICONTROL Core]**

1. Sélectionner **[!UICONTROL Type de condition]** as **[!UICONTROL Chemin sans chaîne de requête]**

1. À droite, laissez le champ **[!UICONTROL Regex]** bouton désactivé

1. Sous **[!UICONTROL path est égal à]** set `/content/luma/us/en.html`. Pour le site de démonstration Luma, la règle ne se déclenche que sur la page d’accueil.

1. Sélectionner **[!UICONTROL Conserver les modifications]**

   ![Condition de remplacement de la suite de rapports Analytics](assets/set-up-analytics-override-condition.png)

1. Sous **[!UICONTROL Actions]** select **[!UICONTROL Ajouter]**

1. Comme la variable **[!UICONTROL Extension]**, sélectionnez **[!UICONTROL SDK Web Adobe Experience Platform]**

1. Comme la variable **[!UICONTROL Type d’action]**, sélectionnez **[!UICONTROL Envoyer un événement]**

1. Comme la variable **[!UICONTROL Type]**, sélectionnez `web.webpagedetails.pageViews`

1. Comme la variable **[!UICONTROL Données XDM]**, sélectionnez la variable `xdm.variable.content` que vous avez créé dans la variable [Création d’éléments de données](create-data-elements.md) leçon

   ![Remplacement de la banque de données Analytics](assets/set-up-analytics-datastream-override-1.png)

1. Faites défiler l’écran vers le bas jusqu’à **[!UICONTROL Remplacements des configurations de flux de données]** section

1. Laissez le champ **[!UICONTROL Développement]** onglet sélectionné.

   >[!TIP]
   >
   >    Cet onglet détermine dans quel environnement de balises le remplacement se produit. Pour cet exemple, vous spécifiez uniquement l’environnement de développement, mais lorsque vous déployez ceci en production, pensez à le faire également dans la variable **[!UICONTROL Production]** environnement.


1. Sélectionnez la variable **[!UICONTROL Datastream]**, dans ce cas `Luma Web SDK: Development Environment`

1. Sous **[!UICONTROL Suites de rapports]**, sélectionnez le site de rapports pour lequel vous souhaitez remplacer le rapport. Dans ce cas, `tmd-websdk-course-stg`.

1. Sélectionner **[!UICONTROL Conserver les modifications]**

1. Et **[!UICONTROL Enregistrer]** votre règle

   ![Remplacement de la banque de données Analytics](assets/analytics-tags-report-suite-override.png)


## Créer votre environnement de développement

Ajoutez vos nouveaux éléments de données et vos nouvelles règles à vos `Luma Web SDK Tutorial` bibliothèque de balises et recréez votre environnement de développement.

Félicitations ! L’étape suivante consiste à valider votre mise en oeuvre Adobe Analytics par le biais du SDK Web Experience Platform.

## Validation d’Adobe Analytics avec Debugger

Découvrez comment vérifier qu’Adobe Analytics capture l’ECID, les pages vues, la chaîne de produit et les événements de commerce électronique avec la fonction Edge Trace du débogueur Experience Platform.

Dans le [Debugger](validate-with-debugger.md) leçon, vous avez appris à inspecter la requête XDM côté client avec Platform Debugger et la console de développement du navigateur, ce qui est similaire à la façon dont vous déboguez une `AppMeasurement.js` Mise en oeuvre d’Analytics. Vous avez également appris à valider les requêtes côté serveur de Platform Edge Network envoyées aux applications Adobe et à afficher une payload entièrement traitée à l’aide d’Assurance.

Pour valider qu’Analytics capture correctement les données par le biais du SDK Web Experience Platform, vous devez suivre deux étapes pour :

1. Validation du traitement des données par l’objet XDM sur l’Edge Network Platform à l’aide de la fonction Edge Trace du débogueur Experience Platform
1. Validation du traitement complet des données par Analytics à l’aide de Adobe Experience Platform Assurance

### Validation des identifiants Experience Cloud

1. Accédez au [Site de démonstration Luma](https://luma.enablementadobe.com/content/luma/us/en.html){target="_blank"}
1. Sélectionnez le bouton de connexion en haut à droite et utilisez les informations d’identification à l’adresse : test@adobe.com p: test pour vous authentifier
1. Ouvrez le débogueur Experience Platform et [basculez la propriété de balise sur le site sur votre propre propriété de développement.](validate-with-debugger.md#use-the-experience-platform-debugger-to-map-to-your-tags-property)


1. Pour activer Edge Trace, accédez à Experience Platform Debugger, dans le volet de navigation de gauche, sélectionnez **[!UICONTROL Journaux]**, puis sélectionnez la variable **[!UICONTROL Edge]** et sélectionnez **[!UICONTROL Connexion]**

   ![Connexion à Edge Trace](assets/analytics-debugger-edgeTrace.png)

1. Il sera vide pour l’instant.

   ![Trace Edge connectée](assets/analytics-debugger-edge-connected.png)

1. Actualisez la page Luma et vérifiez à nouveau le débogueur Experience Platform, car les données doivent passer. La ligne commençant par **[!UICONTROL Mappage automatique Analytics]** est la balise Adobe Analytics
1. Sélectionnez cette option pour ouvrir les deux `[!UICONTROL mappedQueryParams]` Liste déroulante et deuxième liste déroulante pour afficher les variables Analytics

   ![Balise Analytics Edge Trace](assets/analytics-debugger-edge-analytics.png)

   >[!TIP]
   >
   >La deuxième liste déroulante correspond à l’identifiant de suite de rapports Analytics auquel vous envoyez des données. Elle doit correspondre à votre propre suite de rapports, et non à celle de la capture d’écran.

1. Faire défiler vers le bas pour trouver `[!UICONTROL c.a.x.identitymap.ecid.[0].id]`. Il s’agit d’une variable de données contextuelles qui capture ECID.
1. Continuez à faire défiler l’écran vers le bas jusqu’à ce que vous voyiez Analytics `[!UICONTROL mid]` Variable . Les deux identifiants correspondent à l’identifiant Experience Cloud de votre appareil.
1. Sur le site Luma,

   ![Analytics ECID](assets/analytics-debugger-ecid.png)

   >[!NOTE]
   >
   >Puisque vous êtes connecté, prenez quelques instants pour valider l’ID authentifié. `112ca06ed53d3db37e4cea49cc45b71e` pour l’utilisateur **`test@adobe.com`** est également capturé dans la variable `[!UICONTROL c.a.x.identitymap.lumacrmid.[0].id]`

### Validation du remplacement de la suite de rapports

Au-dessus, vous avez configuré un remplacement de la chaîne de données pour la variable [Page d’accueil Luma](https://luma.enablementadobe.com/content/luma/us/en.html).  Validation de cette configuration

1. Recherchez une ligne avec **[!UICONTROL Configuration du flux de données après application du remplacement]**. Vous y trouverez la suite de rapports principale et les suites de rapports supplémentaires qui ont été configurées pour les remplacements de suite de rapports.

   ![Validation de la liste de remplacement d’une suite de rapports Analytics](assets/aep-debugger-datastream-override.png)

1. Faites défiler l’écran jusqu’à la ligne commençant par **[!UICONTROL Mappage automatique Analytics]**  et vérifiez que la variable `[!UICONTROL reportSuiteIds]` affiche la suite de rapports que vous avez spécifiée dans vos configurations de remplacement.

   ![Validation de l’appel de remplacement d’une suite de rapports Analytics](assets/aep-debugger-analytics-report-suite-override.png)

### Validation des pages vues du contenu

Accédez à une page de produit telle que [Page produit Didi Sport Watch](https://luma.enablementadobe.com/content/luma/us/en/products/gear/watches/didi-sport-watch.html#24-WG02).  Vérifiez que les pages vues du contenu sont capturées par Analytics.

1. Recherchez `[!UICONTROL c.a.x.web.webpagedetails.pageviews.value]=1`.
1. Faites défiler l’écran vers le bas pour afficher la `[!UICONTROL gn]` Variable . Il s’agit de la syntaxe dynamique Analytics de la variable `[!UICONTROL s.pageName]` Variable . Il capture le nom de la page à partir de la couche de données.

   ![Chaîne de produit Analytics](assets/analytics-debugger-edge-page-view.png)

### Validation de la chaîne de produit et des événements de commerce électronique

Comme vous vous trouvez déjà sur une page de produit, cet exercice continue d’utiliser la même trace Edge pour valider que les données de produit sont capturées par Analytics. Les événements de chaîne de produit et de commerce électronique sont automatiquement associés à des variables XDM dans Analytics. Tant que vous avez mappé sur le `productListItem` Variable XDM pendant [configuration d’un schéma XDM pour Adobe Analytics](setup-analytics.md#configure-an-xdm-schema-for-adobe-analytics), l’Edge Network Platform s’occupe de mapper les données aux variables d’analyse appropriées.

**Commencez par valider que la variable `Product String` est défini**

1. Recherchez `[!UICONTROL c.a.x.productlistitems.][0].[!UICONTROL sku]`. La variable capture la valeur de l’élément de données que vous avez mappée à la variable `productListItems.item1.sku` plus tôt dans cette leçon
1. Recherchez également `[!UICONTROL c.a.x.productlistitems.][0].[!UICONTROL _experience.analytics.customdimensions.evars.evar1]`. La variable capture la valeur de l’élément de données auquel vous avez mappé `productListItems.item1._experience.analytics.customdimensions.evars.evar1`
1. Faites défiler l’écran vers le bas pour afficher la `[!UICONTROL pl]` Variable . Il s’agit de la syntaxe dynamique de la variable de chaîne de produit Analytics.
1. Notez que le nom du produit de la couche de données est mappé à la fois à la `[!UICONTROL c.a.x.productlistitems.][0].[!UICONTROL sku]` et la variable `[!UICONTROL product]` du paramètre de la chaîne products.  En outre, le titre du produit de la couche de données est mappé à evar1 de marchandisage dans la chaîne de produits.

   ![Chaîne de produit Analytics](assets/analytics-debugger-prodstring.png)

   Le suivi Edge traite `commerce` événements légèrement différents `productList` dimensions. Une variable de données contextuelles n’est pas mappée de la même manière que le nom du produit est mappé sur `[!UICONTROL c.a.x.productlistitem.[0].name]` ci-dessus. À la place, le suivi Edge affiche le mappage automatique de l’événement final dans Analytics. `event` Variable . Platform Edge Network le mappe en conséquence tant que vous mappez à la XDM appropriée. `commerce` Variable while [configuration du schéma pour Adobe Analytics](setup-analytics.md#configure-an-xdm-schema-for-adobe-analytics); dans ce cas, la variable `commerce.productViews.value=1`.

1. De retour dans la fenêtre du débogueur Experience Platform, faites défiler l’écran jusqu’au `[!UICONTROL events]` est définie sur `[!UICONTROL prodView]`

1. Remarque `[!UICONTROL c.a.x.eventType]` est défini sur `commerce.productViews` car vous vous trouvez sur une page de produits.

   >[!TIP]
   >
   > La variable `ecommerce - pdp library loaded - AA (order 20)` la règle remplace la valeur de `eventType` défini par la variable `all pages global content variables - library loaded - AA (order 1)` car elle est définie pour se déclencher ultérieurement dans la séquence.


   ![Consultation produit Analytics](assets/analytics-debugger-prodView.png)

**Validez le reste des événements de commerce électronique et les chaînes de produits définis pour Analytics.**

1. Ajouter [Didi Sport Watch](https://luma.enablementadobe.com/content/luma/us/en/products/gear/watches/didi-sport-watch.html#24-WG02) au panier
1. Accédez au [Page Panier](https://luma.enablementadobe.com/content/luma/us/en/user/cart.html), vérifiez Edge Trace pour

   * `eventType` défini sur `commerce.productListViews`
   * `[!UICONTROL events: "scView"]`, et
   * la chaîne de produit est définie

   ![Vue du panier Analytics](assets/analytics-debugger-cartView.png)

1. Passez à l’extraction, cochez Edge Trace pour

   * `eventType` défini sur `commerce.checkouts`
   * `[!UICONTROL events: "scCheckout"]`, et
   * la chaîne de produit est définie

   ![Passage en caisse Analytics](assets/analytics-debugger-checkout.png)

1. Remplissez uniquement les **Prénom** et **Nom** champs du formulaire d’expédition et sélectionnez **Continuer**. Sur la page suivante, sélectionnez **Passer commande**
1. Sur la page de confirmation, vérifiez Edge Trace pour

   * `eventType` défini sur `commerce.purchases`
   * Événement d’achat en cours de définition `[!UICONTROL events: "purchase"]`
   * Variable de code de devise en cours de définition `[!UICONTROL cc: "USD"]`
   * Identifiant d’achat défini dans `[!UICONTROL pi]`
   * Chaîne de produit `[!UICONTROL pl]` définition du nom, de la quantité et du prix du produit

   ![Achat Analytics](assets/analytics-debugger-purchase.png)



## Validation d’Adobe Analytics à l’aide d’Assurance

Adobe Experience Platform Assurance vous aide à inspecter, à tester, à simuler et à valider la manière dont vous collectez des données ou diffusez des expériences avec votre site web et votre application mobile.

Au cours de l’exercice précédent, vous avez vérifié qu’Adobe Analytics capturait l’ECID, les pages vues, la chaîne de produit et les événements de commerce électronique avec la fonction Edge Trace du débogueur Experience Platform.  Ensuite, vous validez ces mêmes événements à l’aide de Adobe Experience Platform Assurance, une autre interface permettant d’accéder aux mêmes données dans Edge Trace.

Comme vous l’avez appris dans la [Assurance](validate-with-assurance.md) leçon : il existe plusieurs façons d’initier une session d’assurance. Puisque vous avez déjà ouvert un Adobe Experience Platform Debugger avec une session Edge Trace lancée à partir du dernier exercice, nous vous recommandons d’accéder à Assurance par l’intermédiaire du débogueur :
![Assurance via la collecte de données Adobe Experience Platform](assets/assurance-open-aep-debugger.png)

Dans le **[!UICONTROL &quot;Tutoriel du SDK Web 3&quot;]** Entrée de la session d’assurance **[!UICONTROL &quot;hitdebugger&quot;]** dans la barre de recherche des événements pour filtrer les résultats sur les données Adobe Analytics Post-traitées.
![Assurance Adobe des données après traitement Analytics](assets/assurance-hitdebugger.png)

### Validation des identifiants Experience Cloud

Pour vérifier qu’Adobe Analytics capture l’ECID, sélectionnez une balise et ouvrez la charge utile.  Le fournisseur de cette balise doit être : **[!UICONTROL com.adobe.analytics.hitdebugger]**
![Validation Adobe Analytics avec Assurance](assets/assurance-hitdebugger-payload.png)

Faites défiler l’écran jusqu’à **[!UICONTROL mcvisId]** pour vérifier que l’ECID est correctement capturé.
![Validation des identifiants Experience Cloud avec Assurance](assets/assurance-hitdebugger-mcvisId.png)

### Validation des pages vues du contenu

À l’aide de la même balise, vérifiez que les pages vues du contenu sont mappées à la variable Adobe Analytics correcte.
Faites défiler jusqu’à **[!UICONTROL pageName]** pour valider que la variable `Page Name` est correctement capturé
![Validation du nom de page avec Assurance](assets/assurance-hitdebugger-content-pagename.png)

### Validation de la chaîne de produit et des événements de commerce électronique

En suivant les mêmes cas d’utilisation de validation utilisés lors de la validation avec le débogueur Experience Platform ci-dessus, continuez à utiliser la même balise pour valider la variable `Ecommerce Events` et la variable `Product String`.

1. Recherchez la payload où l’événement **[!UICONTROL events]** contain `prodView`
   ![Validation de la chaîne de produit avec Assurance](assets/assurance-hitdebugger-prodView-event.png)
1. Faites défiler jusqu’à **[!UICONTROL product-string]** pour valider la variable `Product String`.
   * Notez que `Product SKU` et `Merchandizing eVar1`.
1. Faites défiler l’écran vers le bas et validez `prop1`, que vous avez configuré à l’aide des règles de traitement de la section précédente, contient la variable `Product SKU`\
   ![Chaîne de produit avec validation des variables de marchandisage avec assurance](assets/assurance-hitdebugger-prodView-productString-merchVar.png)

Continuez à valider votre mise en oeuvre en consultant les événements de panier, de passage en caisse et d’achat.

1. Recherchez la payload où l’événement **[!UICONTROL events]** contain `scView` et validez la chaîne de produit.
   ![Validation de la chaîne de produit avec Assurance](assets/assurance-hitdebugger-scView-event.png)
1. Recherchez la payload où l’événement **[!UICONTROL events]** contain `scCheckout` et validez la chaîne de produit.
   ![Validation de la chaîne de produit avec Assurance](assets/assurance-hitdebugger-scView-event.png)
1. Recherchez la payload où l’événement **[!UICONTROL events]** contain `purchase`
   ![Validation de la chaîne de produit avec Assurance](assets/assurance-hitdebugger-purchase-event.png)
1. Lors de la validation de la variable `purchase` , notez que la variable `Product String` doit contenir la variable `Product SKU`, `Product Quantity` , et `Product Total Price`.
1. En outre, pour la variable `purchase` validez la variable `purchase-id` et/ou `purchaseId` sont définis


Félicitations ! Tu l&#39;as fait ! C’est la fin de la leçon et vous êtes maintenant prêt à mettre en oeuvre Adobe Analytics avec le SDK Web Platform pour votre propre site web.

[Suivant : ](setup-audience-manager.md)

>[!NOTE]
>
>Merci d’avoir consacré du temps à l’apprentissage du SDK Web Adobe Experience Platform. Si vous avez des questions, souhaitez partager des commentaires généraux ou avez des suggestions sur le contenu futur, partagez-les à ce sujet. [Article de discussion de la communauté Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996)
