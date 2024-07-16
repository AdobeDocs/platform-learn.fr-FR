---
title: Configuration d’Adobe Analytics à l’aide du SDK Web Experience Platform
description: Découvrez comment configurer Adobe Analytics à l’aide du SDK Web Experience Platform. Cette leçon fait partie du tutoriel Implémentation d’Adobe Experience Cloud avec le SDK web.
solution: Data Collection, Analytics
jira: KT-15408
exl-id: de86b936-0a47-4ade-8ca7-834c6ed0f041
source-git-commit: a8431137e0551d1135763138da3ca262cb4bc4ee
workflow-type: tm+mt
source-wordcount: '2865'
ht-degree: 1%

---

# Configuration d’Adobe Analytics avec le SDK Web de Adobe Experience Platform

Découvrez comment configurer Adobe Analytics à l’aide du [SDK Web Adobe Experience Platform](https://experienceleague.adobe.com/en/docs/platform-learn/data-collection/web-sdk/overview), créer des règles de balises pour envoyer des données à Adobe Analytics et vérifier qu’Analytics capture les données comme prévu.

[Adobe Analytics](https://experienceleague.adobe.com/fr/docs/analytics) est une application de pointe qui vous permet de comprendre vos clients en tant que personnes et d’orienter votre activité grâce aux renseignements sur vos clients.

![Diagramme SDK Web vers Adobe Analytics](assets/dc-websdk-aa.png)

## Objectifs d&#39;apprentissage

À la fin de cette leçon, vous saurez comment :

* Configuration d’un flux de données pour activer Adobe Analytics
* Identifier les champs XDM standard automatiquement mappés aux variables Analytics
* Définition des variables Analytics dans l’objet de données
* Envoi de données vers une autre suite de rapports en remplaçant le flux de données
* Validation des variables Adobe Analytics à l’aide de Debugger et d’Assurance

## Conditions préalables

Pour terminer cette leçon, vous devez d’abord :

* Familiarisez-vous avec Adobe Analytics et accédez-y.

* posséder au moins un identifiant de suite de rapports de test/développement. Si vous ne disposez pas d’une suite de rapports de test/développement que vous pouvez utiliser pour ce tutoriel, [créez-en une](https://experienceleague.adobe.com/en/docs/analytics/admin/admin-tools/manage-report-suites/c-new-report-suite/t-create-a-report-suite).

* Suivez les leçons des sections Configuration initiale et Configuration des balises de ce tutoriel.

## Configuration du flux de données

Le SDK Web Platform envoie les données de votre site Web à l’Edge Network Platform. Votre flux de données indique ensuite à Platform Edge Network à quelles suites de rapports Adobe Analytics vos données doivent être envoyées.

1. Accédez à l’interface [Collecte de données](https://experience.adobe.com/#/data-collection){target="blank"}
1. Dans le volet de navigation de gauche, sélectionnez **[!UICONTROL Datastreams]**
1. Sélectionnez le flux de données `Luma Web SDK: Development Environment` créé précédemment.

   ![Sélectionnez la banque de données du SDK Web Luma](assets/datastream-luma-web-sdk-development.png)

1. Sélectionnez **[!UICONTROL Ajouter un service]**
   ![Ajouter un service à la banque de données](assets/datastream-analytics-addService.png)
1. Sélectionnez **[!UICONTROL Adobe Analytics]** comme **[!UICONTROL Service]**
1. Saisissez l’**[!UICONTROL identifiant de suite de rapports]** de votre suite de rapports de développement.
1. Sélectionnez **[!UICONTROL Save]**

   ![Analyse de l’enregistrement de la banque de données](assets/datastream-add-analytics.png)

   >[!TIP]
   >
   >L’ajout d’autres suites de rapports en sélectionnant **[!UICONTROL Ajouter une suite de rapports]** équivaut à un balisage multisuite.

>[!WARNING]
>
>Dans ce tutoriel, vous configurez uniquement la suite de rapports Adobe Analytics pour votre environnement de développement. Lorsque vous créez des flux de données pour votre propre site web, vous devez créer des flux de données et des suites de rapports supplémentaires pour vos environnements d’évaluation et de production.

## Définition des variables Analytics

Il existe plusieurs façons de définir des variables Analytics dans une implémentation du SDK Web :

1. Mappage automatique des champs XDM aux variables Analytics (automatique).
1. Définissez des champs dans l’objet `data` (recommandé).
1. Faire correspondre les champs XDM aux variables Analytics dans les règles de traitement Analytics (ce qui n’est plus recommandé).
1. Associer les variables Analytics directement dans le schéma XDM (ce qui n’est plus recommandé).

Depuis mai 2024, vous n’avez plus besoin de créer un schéma XDM pour mettre en oeuvre Adobe Analytics avec le SDK Web Platform. L’objet `data` (et l’élément de données `data.variable` que vous avez créé dans la leçon [Créer des éléments de données](create-data-elements.md)) peut être utilisé pour définir toutes les variables Analytics personnalisées. La définition de ces variables dans l’objet de données sera familière aux clients Analytics existants, sera plus efficace que l’utilisation de l’interface des règles de traitement et empêchera les données inutiles de prendre de l’espace dans les profils client en temps réel (important si vous disposez de Real-Time Customer Data Platform ou de Journey Optimizer).

### Champs mappés automatiquement

De nombreux champs XDM sont automatiquement mappés aux variables Analytics. Pour obtenir la liste des mappages la plus récente, reportez-vous à la section [Mappage des variables Analytics dans Adobe Experience Edge](https://experienceleague.adobe.com/en/docs/experience-platform/edge/data-collection/adobe-analytics/automatically-mapped-vars).

Cela se produit si _même si vous n’avez pas défini de schéma personnalisé_. Le SDK Web Experience Platform collecte automatiquement certaines données et les envoie à Platform Edge Network en tant que champs XDM. Par exemple, le SDK Web lit l’URL de la page active et l’envoie en tant que champ XDM `web.webPageDetails.URL`. Ce champ est transféré à Adobe Analytics et renseigne automatiquement les rapports URL de page dans Adobe Analytics.

Si vous implémentez le SDK Web pour Adobe Analytics avec un schéma XDM, comme vous l’avez fait dans ce tutoriel, certains des champs XDM que vous avez mis en oeuvre automatiquement sont mappés aux variables Analytics, comme indiqué dans ce tableau :

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

Les sections individuelles de la chaîne de produit Analytics sont définies par le biais de différentes variables XDM sous l’objet `productListItems`.

>[!NOTE]
>
>À compter du 18 août 2022, `productListItems[].SKU` aura la priorité pour le mappage au nom du produit dans la variable s.products .
>La valeur définie sur `productListItems[].name` est mappée au nom du produit uniquement si `productListItems[].SKU` n’existe pas. Dans le cas contraire, il n’est pas mappé et est disponible dans les données contextuelles.
>Ne définissez pas de chaîne vide ou de valeur nulle sur `productListItems[].SKU`. Cela a pour effet indésirable de mapper le nom du produit dans la variable s.products .


### Définition de variables dans l’objet de données

Mais qu&#39;en est-il des eVars, des props et des événements ? La définition de variables dans l’objet `data` est la méthode recommandée pour définir ces variables Analytics avec le SDK Web. La définition de variables dans l’objet de données peut également remplacer l’une des variables mappées automatiquement.

Tout d’abord, qu’est-ce que l’objet `data` ? Dans tout événement de SDK Web, vous pouvez envoyer deux objets avec des données personnalisées, l’objet `xdm` et l’objet `data`. Tous deux sont envoyés à Platform Edge Network, mais seul l’objet `xdm` est envoyé au jeu de données Experience Platform. Les propriétés de l’objet `data` peuvent être mappées sur les champs Edge vers `xdm` à l’aide de la fonction Préparation de données pour la collecte de données , mais ne sont pas envoyées à l’Experience Platform. Cela en fait un moyen idéal d’envoyer des données à des applications telles qu’Analytics, qui ne sont pas créées de manière native sur Experience Platform.

Voici les deux objets d’un appel SDK Web générique :

![ objets data et xdm](assets/analytics-data-object-intro.png)

Adobe Analytics est configuré pour rechercher les propriétés de l’objet `data.__adobe.analytics` et les utiliser pour les variables Analytics.

Maintenant voyons comment ça marche. Définissons `eVar1` et `prop1` avec notre nom de page et voyons comment la valeur mappée XDM peut être écrasée.

1. Ouvrez la règle de balise `all pages - library loaded - set global variables - 1`.
1. Ajouter une nouvelle **[!UICONTROL Action]**
1. Sélectionnez l’extension **[!UICONTROL Adobe Experience Platform Web SDK]**
1. Sélectionnez **[!UICONTROL Action Type]** comme **[!UICONTROL Mise à jour de variable]**
1. Sélectionnez `data.variable` comme **[!UICONTROL élément de données]**
1. Sélectionnez l’objet **[!UICONTROL analytics]**
1. Définissez `eVar1` comme élément de données `page.pageInfo.pageName`
1. Définissez `prop1` pour copier la valeur de `eVar1`
1. Pour tester le remplacement des valeurs mappées XDM, dans la section **[!UICONTROL Additional property]** , définissez le nom de page comme valeur statique `test`.
1. Enregistrer la règle


Maintenant, nous devons inclure l’objet de données dans notre règle d’événement d’envoi.

1. Ouvrez la règle de balise `all pages - library loaded - send event - 50`.
1. Ouvrez l’action **[!UICONTROL Send Event]**
1. Sélectionnez `data.variable` comme **[!UICONTROL Data]**
1. Sélectionnez **[!UICONTROL Conserver les modifications]**
1. Sélectionnez **[!UICONTROL Save]**



<!--


### Map to Analytics variables with processing rules

All fields in the XDM schema become available to Adobe Analytics as Context Data Variables with the following prefix `a.x.`. For example, `a.x.web.webinteraction.region`

In this exercise, you map one XDM variable to a prop. Follow these same steps for any custom mapping that you must do for any `eVar`, `prop`, `event`, or variable accessible via Processing Rules.

1. Go to the Analytics interface
1. Go to [!UICONTROL Admin] > [!UICONTROL Admin Tools] > [!UICONTROL Report Suites ]
1. Select the dev/test report suite that you are using for the tutorial > [!UICONTROL Edit Settings] > [!UICONTROL General] > [!UICONTROL Processing Rules]

    ![Analytics Purchase](assets/analytics-process-rules.png)   

1. Create a rule to **[!UICONTROL Overwrite value of]** `[!UICONTROL Product SKU (prop1)]` to `a.x.productlistitems.0.sku`. Remember to add a note about why you are creating the rule and name your rule title. Select **[!UICONTROL Save]**

    ![Analytics Purchase](assets/analytics-set-processing-rule.png)   

    >[!IMPORTANT]
    >
    >The first time you map to a processing rule, the UI does not show you the context data variables from the XDM object. To fix that select any value, Save, and come back to edit. All XDM variables should now appear.

### Map to Analytics variables using the Adobe Analytics field group

An alternative to processing rules is to map to Analytics variables in the XDM schema using the `Adobe Analytics ExperienceEvent Template` field group. This approach has gained popularity because many users find it simpler than configuring processing rules, however, by increasing the size of the XDM payload it could in turn increase the profile size in other applications like Real-Time CDP.

To add the `Adobe Analytics ExperienceEvent Template` field group to your schema:

1. Open the [Data Collection](https://experience.adobe.com/#/data-collection){target="blank"} interface
1. Select **[!UICONTROL Schemas]** from the left navigation
1. Make sure you are in the sandbox you are using from the tutorial
1. Open your `Luma Web Event Data` schema
1. In the **[!UICONTROL Field Groups]** section, select **[!UICONTROL Add]**
1. Find the `Adobe Analytics ExperienceEvent Template` field group and add it to your schema


Now, set a merchandising eVar in the product string. With the `Adobe Analytics ExperienceEvent Template` field group, you are able to map variables to merchandising eVars or events within the product string. This is also known as setting **Product Syntax Merchandising**. 

1. Go back to your tag property

1. Open the rule `ecommerce - library loaded - set product details variables - 20`

1. Open the **[!UICONTROL Set Variable]** action

1. Select to open `_experience > analytics > customDimensions > eVars > eVar1`

1. Set the **[!UICONTROL Value]** to `%product.productInfo.title%`

1. Select **[!UICONTROL Keep Changes]**

    ![Product SKU XDM object Variable](assets/set-up-analytics-product-merchandising.png)

1. Select **[!UICONTROL Save]** to save the rule

As you just saw, basically all of the Analytics variables can be set in the `Adobe Analytics ExperienceEvent Template` field group.

>[!NOTE]
>
> Notice the `_experience` object under `productListItems` > `Item 1`. Setting any variable under this [!UICONTROL object] sets Product Syntax eVars or Events.

-->

## Envoi de données vers une autre suite de rapports

Vous pouvez modifier les données de suite de rapports Adobe Analytics envoyées aux visiteurs sur certaines pages. Cela nécessite une configuration dans le flux de données et une règle.

### Configuration du flux de données pour un remplacement de suite de rapports

Pour configurer le paramètre de remplacement de la suite de rapports Adobe Analytics dans le flux de données :

1. Ouvrez votre flux de données.
1. Modifiez la configuration **[!UICONTROL Adobe Analytics]** en ouvrant le menu ![more](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) , puis en sélectionnant **[!UICONTROL Modifier]**

   ![Remplacer l’ensemble de données](assets/datastream-edit-analytics.png)

1. Sélectionnez **[!UICONTROL Options avancées]** pour ouvrir les **[!UICONTROL remplacements de suites de rapports]**

1. Sélectionnez les suites de rapports à remplacer. Dans ce cas, `Web SDK Course Dev` et `Web SDK Course Stg`

1. Sélectionnez **[!UICONTROL Save]**

   ![Remplacer l’ensemble de données](assets/analytics-datastreams-edit-adobe-analytics-configurations-report-suites.png)


### Configuration d’une règle pour un remplacement de suite de rapports

Créons une règle pour envoyer un appel de page vue supplémentaire à une autre suite de rapports. Utilisez la fonction de remplacement de la banque de données pour modifier la suite de rapports d’une page à l’aide de l’action **[!UICONTROL Envoyer l’événement]**.

1. Créez une nouvelle règle, nommez-la `homepage - library loaded - AA report suite override - 51`

1. Sélectionnez le signe plus sous **[!UICONTROL Event]** pour ajouter un nouveau déclencheur.

1. Sous **[!UICONTROL Extension]**, sélectionnez **[!UICONTROL Core]**

1. Sous **[!UICONTROL Event Type]**, sélectionnez **[!UICONTROL Library Loaded (Page Top)]** (Bibliothèque chargée (Haut de page))

1. Sélectionnez pour ouvrir **[!UICONTROL Options avancées]**, saisissez `51`. Cela garantit que la règle s’exécute après le `all pages - library loaded - send event - 50` qui définit le XDM de base avec le type d’action **[!UICONTROL Mettre à jour la variable]**.
1. Sélectionnez **[!UICONTROL Conserver les modifications]**

   ![Remplacement de suite de rapports Analytics](assets/set-up-analytics-rs-override.png)

1. Sous **[!UICONTROL Conditions]**, sélectionnez **[!UICONTROL Ajouter]**

1. Laissez **[!UICONTROL Type logique]** sur **[!UICONTROL Normal]**

1. Laissez **[!UICONTROL Extensions]** comme **[!UICONTROL Core]**

1. Sélectionnez **[!UICONTROL Type de condition]** comme **[!UICONTROL Chemin sans chaîne de requête]**

1. À droite, laissez le bouton bascule **[!UICONTROL Regex]** désactivé

1. Sous **[!UICONTROL path equals]** set `/content/luma/us/en.html`. Pour le site de démonstration Luma, la règle ne se déclenche que sur la page d’accueil.

1. Sélectionnez **[!UICONTROL Conserver les modifications]**

   ![Condition de remplacement de la suite de rapports Analytics](assets/set-up-analytics-override-condition.png)

1. Sous **[!UICONTROL Actions]**, sélectionnez **[!UICONTROL Ajouter]**

1. En tant que **[!UICONTROL extension]**, sélectionnez **[!UICONTROL Adobe Experience Platform Web SDK]**

1. En tant que **[!UICONTROL Type d’action]**, sélectionnez **[!UICONTROL Envoyer l’événement]**

1. En tant que **[!UICONTROL données XDM]**, sélectionnez l’élément de données `xdm.variable.content` que vous avez créé dans la leçon [Créer des éléments de données](create-data-elements.md).

1. En tant que **[!UICONTROL Data]**, sélectionnez l’élément de données `data.variable` que vous avez créé dans la leçon [Créer des éléments de données](create-data-elements.md).

   ![Remplacement de la banque de données Analytics](assets/set-up-analytics-datastream-override-1.png)

1. Faites défiler l’écran jusqu’à la section **[!UICONTROL Remplacements des configurations de Datastream]** .

1. Laissez l’onglet **[!UICONTROL Développement]** sélectionné.

   >[!TIP]
   >
   >    Cet onglet détermine dans quel environnement de balises le remplacement se produit. Pour cet exercice, vous spécifiez uniquement l’environnement de développement, mais lorsque vous déployez ceci en production, pensez à le faire également dans l’environnement **[!UICONTROL Production]**.

1. Sélectionnez le **[!UICONTROL sandbox]** que vous utilisez pour le tutoriel.
1. Sélectionnez le **[!UICONTROL Datastream]**, ici `Luma Web SDK: Development Environment`

1. Sous **[!UICONTROL Suites de rapports]**, sélectionnez le site de rapports pour lequel vous souhaitez effectuer le remplacement. Dans ce cas, `tmd-websdk-course-stg`.

1. Sélectionnez **[!UICONTROL Conserver les modifications]**

1. Et **[!UICONTROL Enregistrer]** votre règle

   ![Remplacement de la banque de données Analytics](assets/analytics-tags-report-suite-override.png)


## Créer votre environnement de développement

Ajoutez vos règles mises à jour à votre bibliothèque de balises `Luma Web SDK Tutorial` et recréez votre environnement de développement.

Félicitations ! L’étape suivante consiste à valider votre mise en oeuvre Adobe Analytics par le biais du SDK Web Experience Platform.

## Validation d’Adobe Analytics avec Debugger

Découvrez comment vérifier qu’Adobe Analytics capture l’ECID, les pages vues, la chaîne de produit et les événements de commerce électronique avec la fonction Edge Trace du débogueur Experience Platform.

Dans la leçon [Debugger](validate-with-debugger.md), vous avez appris à inspecter la requête XDM côté client avec Platform Debugger et la console de développement du navigateur, ce qui est similaire à la façon dont vous déboguez une implémentation `AppMeasurement.js` d’Analytics. Vous avez également appris à valider les requêtes côté serveur de Platform Edge Network envoyées aux applications Adobe et à afficher une payload entièrement traitée à l’aide d’Assurance.

Pour valider qu’Analytics capture correctement les données par le biais du SDK Web Experience Platform, vous devez suivre deux étapes pour :

1. Validation du traitement des données par l’objet XDM sur l’Edge Network Platform à l’aide de la fonction Edge Trace du débogueur Experience Platform
1. Validation du traitement complet des données par Analytics à l’aide de Adobe Experience Platform Assurance

### Validation des identifiants Experience Cloud

1. Accédez au [site de démonstration Luma](https://luma.enablementadobe.com/content/luma/us/en.html){target="_blank"}
1. Sélectionnez le bouton de connexion en haut à droite et utilisez les informations d’identification à l’adresse : test@adobe.com p: test pour vous authentifier
1. Ouvrez le débogueur Experience Platform et [basculez la propriété de balise sur le site vers votre propre propriété de développement](validate-with-debugger.md#use-the-experience-platform-debugger-to-map-to-your-tags-property)


1. Pour activer Edge Trace, accédez à Experience Platform Debugger, dans le volet de navigation de gauche, sélectionnez **[!UICONTROL Journaux]**, puis sélectionnez l’onglet **[!UICONTROL Edge]** et sélectionnez **[!UICONTROL Se connecter]**

   ![Connecter Edge Trace](assets/analytics-debugger-edgeTrace.png)

1. Il sera vide pour l’instant.

   ![Edge Trace connectée](assets/analytics-debugger-edge-connected.png)

1. Actualisez la page Luma et vérifiez à nouveau le débogueur Experience Platform, car les données doivent passer. La ligne commençant par **[!UICONTROL Mappage automatique Analytics]** est la balise Adobe Analytics
1. Sélectionnez cette option pour ouvrir la liste déroulante `[!UICONTROL mappedQueryParams]` et la deuxième liste déroulante afin d’afficher les variables Analytics.

   ![Balise Analytics Edge Trace](assets/analytics-debugger-edge-analytics.png)

   >[!TIP]
   >
   >La deuxième liste déroulante correspond à l’identifiant de suite de rapports Analytics auquel vous envoyez des données. Elle doit correspondre à votre propre suite de rapports, et non à celle de la capture d’écran.

1. Faites défiler l’écran vers le bas pour trouver `[!UICONTROL c.a.x.identitymap.ecid.[0].id]`. Il s’agit d’une variable de données contextuelles qui capture ECID.
1. Continuez à faire défiler l’écran vers le bas jusqu’à ce que la variable Analytics `[!UICONTROL mid]` s’affiche. Les deux identifiants correspondent à l’identifiant Experience Cloud de votre appareil.
1. Sur le site Luma,

   ![ECID Analytics](assets/analytics-debugger-ecid.png)

   >[!NOTE]
   >
   >Puisque vous êtes connecté, prenez quelques instants pour valider l’ID authentifié `112ca06ed53d3db37e4cea49cc45b71e` pour que l’utilisateur **`test@adobe.com`** soit également capturé dans le `[!UICONTROL c.a.x.identitymap.lumacrmid.[0].id]`

### Validation du remplacement de la suite de rapports

Ci-dessus, vous avez configuré un remplacement de la banque de données pour la [page d’accueil Luma](https://luma.enablementadobe.com/content/luma/us/en.html).  Validation de cette configuration

1. Recherchez une ligne avec la **[!UICONTROL configuration Datastream après l’application du remplacement]**. Vous y trouverez la suite de rapports principale et les suites de rapports supplémentaires qui ont été configurées pour les remplacements de suite de rapports.

   ![Validation de la liste de remplacement de la suite de rapports Analytics](assets/aep-debugger-datastream-override.png)

1. Faites défiler l’écran jusqu’à la ligne commençant par **[!UICONTROL Mappage automatique Analytics]** et vérifiez que `[!UICONTROL reportSuiteIds]` affiche la suite de rapports que vous avez spécifiée dans vos configurations de remplacement.

   ![Validation de l’appel de remplacement d’une suite de rapports Analytics](assets/aep-debugger-analytics-report-suite-override.png)

### Validation des pages vues du contenu

Accédez à une page de produits telle que la [page produit Didi Sport Watch](https://luma.enablementadobe.com/content/luma/us/en/products/gear/watches/didi-sport-watch.html#24-WG02).  Vérifiez que les pages vues du contenu sont capturées par Analytics.

1. Recherchez `[!UICONTROL c.a.x.web.webpagedetails.pageviews.value]=1`.
1. Faites défiler l’écran vers le bas pour afficher la variable `[!UICONTROL gn]`. Il s’agit de la syntaxe dynamique Analytics de la variable `[!UICONTROL s.pageName]`. Il capture le nom de la page à partir de la couche de données.

   ![Chaîne de produit Analytics](assets/analytics-debugger-edge-page-view.png)

### Validation de la chaîne de produit et des événements de commerce électronique

Comme vous vous trouvez déjà sur une page de produit, cet exercice continue d’utiliser la même trace Edge pour valider que les données de produit sont capturées par Analytics. Les événements de chaîne de produit et de commerce électronique sont automatiquement associés à des variables XDM dans Analytics. Tant que vous avez mappé sur la variable XDM `productListItem` appropriée lors de la [configuration d’un schéma XDM pour Adobe Analytics](setup-analytics.md#configure-an-xdm-schema-for-adobe-analytics), l’Edge Network Platform s’occupe de mapper les données sur les variables d’analyse appropriées.

**Commencez par valider que le `Product String` est défini**

1. Recherchez `[!UICONTROL c.a.x.productlistitems.][0].[!UICONTROL sku]`. La variable capture la valeur de l’élément de données que vous avez mappée à `productListItems.item1.sku` plus tôt dans cette leçon.
1. Recherchez également `[!UICONTROL c.a.x.productlistitems.][0].[!UICONTROL _experience.analytics.customdimensions.evars.evar1]`. La variable capture la valeur de l’élément de données que vous avez mappée à `productListItems.item1._experience.analytics.customdimensions.evars.evar1`.
1. Faites défiler l’écran vers le bas pour afficher la variable `[!UICONTROL pl]`. Il s’agit de la syntaxe dynamique de la variable de chaîne de produit Analytics.
1. Notez que le nom du produit de la couche de données est mappé à la fois au paramètre `[!UICONTROL c.a.x.productlistitems.][0].[!UICONTROL sku]` et `[!UICONTROL product]` de la chaîne products.  En outre, le titre du produit de la couche de données est mappé à evar1 de marchandisage dans la chaîne de produits.

   ![Chaîne de produit Analytics](assets/analytics-debugger-prodstring.png)

   Edge Trace traite les événements `commerce` légèrement différemment des dimensions `productList`. Vous ne voyez pas de variable de données contextuelles mappée de la même manière que le nom du produit mappé à `[!UICONTROL c.a.x.productlistitem.[0].name]` ci-dessus. À la place, Edge Trace affiche le mappage automatique de l’événement final dans la variable Analytics `event`. Platform Edge Network le mappe en conséquence tant que vous mappez à la variable XDM `commerce` appropriée lors de la [configuration du schéma pour Adobe Analytics](setup-analytics.md#configure-an-xdm-schema-for-adobe-analytics) ; dans ce cas, `commerce.productViews.value=1`.

1. De retour dans la fenêtre du débogueur Experience Platform, faites défiler l’écran jusqu’à la variable `[!UICONTROL events]`, elle est définie sur `[!UICONTROL prodView]`.

1. Notez également que `[!UICONTROL c.a.x.eventType]` est défini sur `commerce.productViews` puisque vous vous trouvez sur une page de produits.

   >[!TIP]
   >
   > La règle `ecommerce - pdp library loaded - AA (order 20)` remplace la valeur de `eventType` définie par la règle `all pages global content variables - library loaded - AA (order 1)`, car elle est définie pour se déclencher ultérieurement dans la séquence.


   ![Consultation produit Analytics](assets/analytics-debugger-prodView.png)

**Validez le reste des événements de commerce électronique et les chaînes de produit sont définies pour Analytics**

1. Ajoutez [Didi Sport Watch](https://luma.enablementadobe.com/content/luma/us/en/products/gear/watches/didi-sport-watch.html#24-WG02) au panier
1. Accédez à la [page de panier](https://luma.enablementadobe.com/content/luma/us/en/user/cart.html), cochez Edge Trace pour

   * `eventType` défini sur `commerce.productListViews`
   * `[!UICONTROL events: "scView"]` et
   * la chaîne de produit est définie

   ![Consultation du panier Analytics](assets/analytics-debugger-cartView.png)

1. Passez à l’extraction, cochez Edge Trace pour

   * `eventType` défini sur `commerce.checkouts`
   * `[!UICONTROL events: "scCheckout"]` et
   * la chaîne de produit est définie

   ![Passage en caisse Analytics](assets/analytics-debugger-checkout.png)

1. Renseignez les champs **Prénom** et **Nom** du formulaire d’expédition et sélectionnez **Continuer**. Sur la page suivante, sélectionnez **Passer commande**
1. Sur la page de confirmation, vérifiez Edge Trace pour

   * `eventType` défini sur `commerce.purchases`
   * Événement d’achat en cours de définition `[!UICONTROL events: "purchase"]`
   * Variable de code de devise en cours de définition `[!UICONTROL cc: "USD"]`
   * ID d’achat en cours de définition dans `[!UICONTROL pi]`
   * Chaîne de produit `[!UICONTROL pl]` définissant le nom, la quantité et le prix du produit

   ![Achat Analytics](assets/analytics-debugger-purchase.png)



## Validation d’Adobe Analytics à l’aide d’Assurance

Adobe Experience Platform Assurance vous aide à inspecter, à tester, à simuler et à valider la manière dont vous collectez des données ou diffusez des expériences avec votre site web et votre application mobile.

Au cours de l’exercice précédent, vous avez vérifié qu’Adobe Analytics capturait l’ECID, les pages vues, la chaîne de produit et les événements de commerce électronique avec la fonction Edge Trace du débogueur Experience Platform.  Ensuite, vous validez ces mêmes événements à l’aide de Adobe Experience Platform Assurance, une autre interface pour accéder aux mêmes données dans Edge Trace.

Comme vous l’avez appris dans la leçon [Assurance](validate-with-assurance.md), il existe plusieurs façons d’initier une session d’assurance. Puisque vous avez déjà ouvert un Adobe Experience Platform Debugger avec une session Edge Trace lancée à partir du dernier exercice, nous vous recommandons d’accéder à Assurance par l’intermédiaire du débogueur :
![Assurance via la collecte de données Adobe Experience Platform](assets/assurance-open-aep-debugger.png)

Dans le **[!UICONTROL &quot;Tutoriel Web SDK 3&quot;]** Session d’assurance, entrez **[!UICONTROL &quot;hitdebugger&quot;]** dans la barre de recherche des événements pour filtrer les résultats sur les données traitées Adobe Analytics Post.
![ Assurance Adobe des données traitées d’Analytics ](assets/assurance-hitdebugger.png)

### Validation des identifiants Experience Cloud

Pour vérifier qu’Adobe Analytics capture l’ECID, sélectionnez une balise et ouvrez la charge utile.  Le fournisseur de cette balise doit être **[!UICONTROL com.adobe.analytics.hitdebugger]**
![Validation Adobe Analytics avec Assurance](assets/assurance-hitdebugger-payload.png)

Faites ensuite défiler l’écran jusqu’à **[!UICONTROL mcvisId]** pour vérifier que l’ECID est correctement capturé.
![Validation des identifiants Experience Cloud avec Assurance](assets/assurance-hitdebugger-mcvisId.png)

### Validation des pages vues du contenu

À l’aide de la même balise, vérifiez que les pages vues du contenu sont mappées à la variable Adobe Analytics correcte.
Faites défiler l’écran jusqu’à **[!UICONTROL pageName]** pour vérifier que le `Page Name` est correctement capturé.
![Validation du nom de page avec Assurance](assets/assurance-hitdebugger-content-pagename.png)

### Validation de la chaîne de produit et des événements de commerce électronique

En suivant les mêmes cas d’utilisation de validation utilisés lors de la validation avec le débogueur Experience Platform ci-dessus, continuez à utiliser la même balise pour valider les `Ecommerce Events` et `Product String`.

1. Recherchez la payload où les **[!UICONTROL events]** contiennent `prodView`
   ![Validation de chaîne de produit avec assurance](assets/assurance-hitdebugger-prodView-event.png)
1. Faites défiler l’écran jusqu’à **[!UICONTROL product-string]** pour valider le `Product String`.
   * Notez les `Product SKU` et `Merchandizing eVar1`.
1. Faites défiler la page vers le bas et validez que `prop1`, que vous avez configuré à l’aide des règles de traitement de la section précédente, contient le `Product SKU`\
   ![Chaîne de produit avec validation des variables de marchandisage avec assurance](assets/assurance-hitdebugger-prodView-productString-merchVar.png)

Continuez à valider votre mise en oeuvre en consultant les événements de panier, de passage en caisse et d’achat.

1. Recherchez la charge utile où les **[!UICONTROL événements]** contiennent `scView` et validez la chaîne de produit.
   ![Validation de chaîne de produit avec assurance](assets/assurance-hitdebugger-scView-event.png)
1. Recherchez la charge utile où les **[!UICONTROL événements]** contiennent `scCheckout` et validez la chaîne de produit.
   ![Validation de chaîne de produit avec assurance](assets/assurance-hitdebugger-scView-event.png)
1. Recherchez la payload où les **[!UICONTROL events]** contiennent `purchase`
   ![Validation de chaîne de produit avec assurance](assets/assurance-hitdebugger-purchase-event.png)
1. Lors de la validation de l’événement `purchase`, notez que `Product String` doit contenir les éléments `Product SKU`, `Product Quantity` et `Product Total Price`.
1. En outre, pour le `purchase`, validez que les `purchase-id` et/ou `purchaseId` sont définis.


Félicitations ! Tu l&#39;as fait ! C’est la fin de la leçon et vous êtes maintenant prêt à mettre en oeuvre Adobe Analytics avec le SDK Web Platform pour votre propre site web.

[Suivant : ](setup-audience-manager.md)

>[!NOTE]
>
>Merci d’avoir consacré du temps à l’apprentissage du SDK Web Adobe Experience Platform. Si vous avez des questions, souhaitez partager des commentaires généraux ou avez des suggestions sur le contenu à venir, partagez-les sur cet [post de discussion de la communauté Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-implement-adobe-experience-cloud-with-web/td-p/444996)
