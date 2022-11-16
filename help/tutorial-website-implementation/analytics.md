---
title: Ajout d’Adobe Analytics
description: Découvrez comment mettre en oeuvre Adobe Analytics à l’aide de l’extension de balise Adobe Analytics, envoyer la balise de page vue, ajouter des variables, suivre les événements et ajouter des modules externes. Cette leçon fait partie du tutoriel Mise en oeuvre de l’Experience Cloud sur les sites web .
solution: Data Collection, Analytics
exl-id: dababaf2-ff8f-4178-8eaf-04a707b4ab05
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '3891'
ht-degree: 83%

---

# Ajout d’Adobe Analytics

Dans cette leçon, vous allez implémenter l’[extension Adobe Analytics](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/analytics/overview.html?lang=fr) et créer des règles pour envoyer des données à Adobe Analytics.

[Adobe Analytics](https://experienceleague.adobe.com/docs/analytics.html?lang=fr) est une solution de pointe qui vous permet de comprendre vos clients en tant que personnes et d’orienter votre activité grâce aux renseignements sur vos clients.

>[!NOTE]
>
>Adobe Experience Platform Launch est intégré à Adobe Experience Platform comme une suite de technologies destinées à la collecte de données. Plusieurs modifications terminologiques ont été apportées à l’interface que vous devez connaître lors de l’utilisation de ce contenu :
>
> * Le platform launch (côté client) est désormais **[[!DNL tags]](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html?lang=fr)**
> * Le platform launch côté serveur est désormais **[[!DNL event forwarding]](https://experienceleague.adobe.com/docs/experience-platform/tags/event-forwarding/overview.html)**
> * Les configurations Edge sont désormais **[[!DNL datastreams]](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/datastreams.html?lang=fr)**


## Objectifs d’apprentissage

À la fin de cette leçon, vous saurez comment :

1. ajouter l’extension Adobe Analytics ;
1. définir des variables globales à l’aide de l’extension ;
1. ajouter la balise de page vue ;
1. ajouter des variables supplémentaires à l’aide de règles ;
1. ajouter le suivi des clics et d’autres balises basées sur un événement ;
1. ajouter des plug-ins Analytics.

Il existe de nombreux éléments qui peuvent être implémentés pour Analytics dans les balises . Cette leçon n’est pas exhaustive, mais elle devrait vous donner une vue d’ensemble adéquate des techniques principales dont vous avez besoin pour l’implémenter sur votre propre site.

## Conditions préalables

Vous devez avoir terminé les leçons de la rubrique [Configuration des balises](create-a-property.md) et [Ajout d’Identity Service](id-service.md).

En outre, vous aurez besoin d’au moins un identifiant de suite de rapports et de votre serveur de suivi. Si vous ne disposez pas de suite de rapports de test ou de développement que vous pouvez utiliser pour ce tutoriel, créez-en une. Si vous n’êtes pas sûr de la marche à suivre, consultez [la documentation](https://experienceleague.adobe.com/docs/analytics/admin/manage-report-suites/new-report-suite/new-report-suite.html?lang=fr). Vous pouvez récupérer votre serveur de suivi à partir de votre mise en œuvre actuelle, ou auprès de votre consultant ou de votre représentant de l’Assistance clientèle Adobe.

## Ajout de l’extension Analytics

L’extension Analytics se compose de deux parties principales :

1. La configuration de l’extension, qui gère les paramètres principaux de la bibliothèque AppMeasurement.js et qui peut définir des variables globales.
1. Les actions de règle, qui effectuent les opérations suivantes :
   1. Définir des variables
   1. Effacer des variables
   1. Envoyer la balise Analytics

**Ajout de l’extension Analytics**

1. Accédez à **[!UICONTROL Extensions > Catalogue]**.
1. Recherchez l’extension Adobe Analytics.
1. Cliquez sur **[!UICONTROL Installer]**.

   ![Installer l’extension Analytics](images/analytics-catalog-install.png)

1. Sous [!UICONTROL Gestion des bibliothèques > Suites de rapports], saisissez les identifiants de suite de rapports à utiliser avec chaque environnement de balises. Si vos utilisateurs ont accès à Adobe Analytics, notez que lorsque vous commencez à saisir du texte dans la zone, une liste préremplie de toutes vos suites de rapports s’affiche. (Dans ce tutoriel, il est possible d’utiliser une même suite de rapports pour tous les environnements, mais dans la vie réelle, vous souhaiterez utiliser des suites de rapports distinctes, comme illustré ci-dessous)

   ![Entrer les identifiants des suites de rapports](images/analytics-config-reportSuite.png)

   >[!TIP]
   >
   > Nous vous recommandons d’utiliser l’option [!UICONTROL Gérer la bibliothèque pour moi] comme paramètre de [!UICONTROL Gestion des bibliothèques], car il facilite grandement mise à jour de la bibliothèque `AppMeasurement.js`.

1. Sous [!UICONTROL Général > Serveur de suivi], entrez votre serveur de suivi, par exemple `tmd.sc.omtrdc.net`. Entrez votre serveur de suivi SSL si votre site prend en charge `https://`

   ![Entrer les serveurs de suivi](images/analytics-config-trackingServer.png)

1. Dans le [!UICONTROL Section Variables globales], sous [!UICONTROL Paramètres supplémentaires], définissez la variable [!UICONTROL Nom de la page] en utilisant votre `Page Name` élément de données. Cliquez sur l’icône ![icône d’élément de données](images/icon-dataElement.png) pour ouvrir le modal et choisir l’élément de données `Page Name` de la page.

1. Cliquez sur **[!UICONTROL Enregistrer dans la bibliothèque]**.

   ![Définir la variable de nom de page et enregistrer](images/analytics-extension-pageName.png)

>[!NOTE]
>
>Les variables globales peuvent être définies dans la configuration de l’extension ou dans les actions de règle. Gardez à l’esprit que lorsque vous définissez des variables dans la configuration de l’extension, la couche de données doit être définie. *before* code incorporé de balise.

## Envoi de la balise de page vue

Vous allez maintenant créer une règle pour déclencher la balise Analytics, qui enverra la variable [!UICONTROL Nom de page] définie dans la configuration de l’extension.

Vous avez déjà créé une règle &quot;Toutes les pages - Bibliothèque chargée&quot; dans la [Ajout d’un élément de données, d’une règle et d’une bibliothèque](add-data-elements-rules.md) leçon de ce tutoriel, qui est déclenché sur chaque page au chargement de la bibliothèque de balises. You *can* utilisez également cette règle pour Analytics. Toutefois, cette configuration nécessite que tous les attributs de couche de données utilisés dans la balise Analytics soient définis avant les codes incorporés de balise. Pour plus de flexibilité en matière de collecte de données, vous allez créer une règle « Toutes les pages » déclenchée sur Prêt pour DOM afin de déclencher la balise Analytics.

**Envoi de la balise de page vue**

1. Accédez au **[!UICONTROL Règles]** dans le volet de navigation de gauche, puis cliquez sur **[!UICONTROL Ajouter une règle]**

   ![Ajouter une règle](images/analytics-addRule.png)

1. Attribuez un nom à la règle `All Pages - DOM Ready`.
1. Cliquez sur **[!UICONTROL Événements > Ajouter]** pour ouvrir l’écran `Event Configuration`.

   ![Attribuer un nom à la règle et ajouter un événement](images/analytics-domReady-nameAddAnalyticsEvent.png)

1. Sélectionnez **[!UICONTROL Type d’événement > Prêt pour DOM]**. Notez que la commande de la règle est « 50 ».
1. Cliquez sur **[!UICONTROL Conserver les modifications]**
   ![Configurer l’événement](images/analytics-configureEventDomReady.png)

1. Sous Actions, cliquez sur l’icône ![Plus](images/icon-plus.png) pour ajouter une nouvelle action.

   ![Cliquer sur l’icône Plus pour ajouter une nouvelle action](images/analytics-ruleAddAction.png)

1. Sélectionnez **[!UICONTROL Extension > Adobe Analytics]**.

1. Sélectionnez **[!UICONTROL Type d’action > Envoyer la balise]**.

1. Laissez Suivi défini sur `s.t()`. Si vous souhaitiez effectuer un appel `s.tl()` dans une règle d’événement de clics, vous pouvez également utiliser l’action Envoyer la balise.

1. Cliquez sur le bouton **[!UICONTROL Conserver les modifications]**.

   ![Cliquer sur l’icône Plus pour ajouter une nouvelle action](images/analytics-sendBeacon.png)

1. Cliquez sur **[!UICONTROL Enregistrer dans la bibliothèque et créer]**.

   ![Enregistrer dans la bibliothèque et créer](images/analytics-saveToLibraryAndBuild.png)

### Validation de la balise de page vue

Maintenant que vous avez créé une règle pour envoyer une balise Analytics, vous devriez être en mesure de voir la requête dans l’Experience Cloud Debugger.

1. Ouvrez le [site Luma](https://luma.enablementadobe.com/content/luma/us/en.html) dans votre navigateur Chrome.
1. Cliquez sur l’icône ![Ouvrir l’Experience Cloud Debugger](images/analytics-debuggerIcon.png) pour ouvrir l’**[!UICONTROL Adobe Experience Cloud Debugger]**.
1. Assurez-vous que le débogueur mappe la propriété de balise à *your* Environnement de développement, comme décrit dans la section [leçon précédente](switch-environments.md)

   ![Votre environnement de développement de balises affiché dans Debugger](images/switchEnvironments-debuggerOnWeRetail.png)

1. Cliquez pour ouvrir l’onglet Analytics.
1. Développez le nom de votre suite de rapports pour afficher toutes les requêtes qui lui sont envoyées.
1. Vérifiez que la requête a été déclenchée avec la variable et la valeur Nom de page.

   ![Valider l’accès à la page](images/analytics-validatePageHit.png)

>[!NOTE]
>
>Si Nom de page ne s’affiche pas, revenez à la procédure décrite sur cette page pour vous assurer que vous n’avez rien manqué.

## Ajout de variables à l’aide de règles

Lorsque vous avez configuré l’extension Analytics, vous avez renseigné la variable `pageName`dans la configuration de l’extension. Il s’agit d’un emplacement idéal pour renseigner d’autres variables globales, telles que les eVars et les props, à condition que la valeur soit disponible sur la page avant le chargement du code incorporé de balise.

Les règles qui utilisent l’action `Set Variables` offrent un emplacement plus souple pour définir des variables ainsi que des événements. Les règles vous permettent de définir des variables et des événements Analytics différents sous certaines conditions. Par exemple, vous pouvez définir le `prodView` uniquement sur les pages Détails du produit et l’événement `purchase` uniquement sur les pages de confirmation de commande. Cette section vous explique comment définir des variables à l’aide de règles.

### Exemple d’utilisation

Les pages Détails du produit (PDP) sont des points importants pour la collecte de données sur des sites de vente au détail. En règle générale, vous souhaitez qu’Analytics enregistre l’affichage d’un produit et le produit consulté. Cela s’avère utile pour déterminer quels produits sont prisés par vos clients. Sur un site multimédia, les pages d’articles ou de vidéos peuvent utiliser des techniques de suivi similaires à celles que vous utiliserez dans cette section.  Lorsque vous chargez une page Détails du produit, vous pouvez définir cette valeur dans une `eVar` « Type de page », de même que certains événements et l’ID du produit. Cela nous permettra de voir les éléments suivants dans notre analyse :

1. Le nombre de chargements des pages Détails du produit
1. Les produits spécifiques consultés et le nombre de consultations
1. L’impact d’autres facteurs (campagnes, recherche, etc.) sur le nombre de chargements de PDP par des personnes

### Création d’un élément de données pour le type de page

Tout d’abord, vous devez identifier les pages qui sont les pages Détails du produit. Vous procéderez ainsi avec un élément de données.

**Création de l’élément de données pour le type de page**

1. Cliquez sur **[!UICONTROL Éléments de données]** dans le volet de navigation de gauche
1. Cliquez sur **[!UICONTROL Ajouter un élément de données]**.

   ![Ajouter un nouvel élément de données](images/analytics-addDataElement.png)

1. Nommez l’élément de données `Page Type`.
1. Sélectionnez **[!UICONTROL Type d’élément de données > Variable JavaScript]**.
1. Utilisation `digitalData.page.category.type` comme la propriété **[!UICONTROL Nom de variable JavaScript]**
1. Vérifiez les **[!UICONTROL Texte clair]** et **[!UICONTROL Forcer la minuscule]** options
1. Cliquez sur **[!UICONTROL Enregistrer dans la bibliothèque]**.

   ![Ajouter un nouvel élément de données pour le type de page](images/analytics-PageTypeDataElement.png)

### Création d’un élément de données pour l’ID du produit

Ensuite, vous collecterez l’ID du produit de la page Détails du produit actuelle avec un élément de données.

**Création de l’élément de données pour l’ID du produit**

1. Cliquez sur **[!UICONTROL Éléments de données]** dans le volet de navigation de gauche
1. Cliquez sur **[!UICONTROL Ajouter un élément de données]**.

   ![Ajouter un nouvel élément de données](images/analytics-addDataElement.png)

1. Nommez l’élément de données `Product Id`.
1. Sélectionnez **[!UICONTROL Type d’élément de données > Variable JavaScript]**.
1. Utilisation `digitalData.product.0.productInfo.sku` comme la propriété **[!UICONTROL Nom de variable JavaScript]**
1. Vérifiez les **[!UICONTROL Texte clair]** et **[!UICONTROL Forcer la minuscule]** options
1. Cliquez sur **[!UICONTROL Enregistrer dans la bibliothèque]**.

   ![Ajouter un nouvel élément de données pour le type de page](images/analytics-ProductIdDataElement.png)

### Ajout de l’extension Adobe Analytics Product String Extension

Si vous connaissez déjà les implémentations Adobe Analytics, alors il est probable que la [variable de produits](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/products.html?lang=fr) vous soit également familière. La variable de produits a une syntaxe très spécifique et est utilisée de manières légèrement différentes selon le contexte. Pour faciliter le renseignement de la variable products dans les balises, trois extensions supplémentaires ont déjà été créées sur le marketplace de l’extension de balise . Dans cette section, vous allez ajouter une extension créée par Adobe Consulting à utiliser sur la page Détails du produit.

**Ajout de `Adobe Analytics Product String` l’extension**

1. Accédez à la page [!UICONTROL Extensions > Catalogue].
1. Recherchez l’extension `Adobe Analytics Product String` créée par Adobe Consulting Services et cliquez sur **[!UICONTROL Installer]**.
   ![Ajouter l’extension Adobe Analytics Product String créée par Adobe Consulting](images/analytics-addProductStringExtension.png)
1. Prenez quelques instants pour lire les instructions.
1. Cliquez sur **[!UICONTROL Enregistrer dans la bibliothèque]**.

   ![Enregistrer l’extension et la créer dans votre bibliothèque.](images/analytics-addProductStringExtensionSave.png)

### Création de la règle pour les pages Détails du produit

Maintenant, vous allez utiliser vos nouveaux éléments de données et votre nouvelle extension pour créer la règle de votre page Détails du produit. Pour cette fonctionnalité, vous allez créer une autre règle de chargement de page, déclenchée par Prêt pour DOM. Cependant, vous allez utiliser une condition afin qu’elle ne se déclenche que sur les pages Détails du produit, ainsi que le paramètre de commande afin qu’il se déclenche _avant_ la règle qui envoie la balise.

**Création de la règle de page Détails du produit**

1. Accédez au **[!UICONTROL Règles]** dans le volet de navigation de gauche, puis cliquez sur **[!UICONTROL Ajouter une règle]**

   ![Ajouter une règle](images/analytics-addRule2.png)

1. Attribuez un nom à la règle `Product Details - DOM Ready - 40`.
1. Cliquez sur **[!UICONTROL Événements > Ajouter]** pour ouvrir l’écran `Event Configuration`.

   ![Attribuer un nom à la règle et ajouter un événement](images/analytics-domReadyAddEvent.png)

1. Sélectionnez **[!UICONTROL Type d’événement > Prêt pour DOM]**.
1. Définissez **[!UICONTROL Commande]** sur 40, de telle sorte que la règle s’exécute *avant* la règle contenant l’action Analytics > Envoyer la balise.
1. Cliquez sur **[!UICONTROL Conserver les modifications]**

   ![Configurer l’événement](images/analytics-configDOMReadyEvent.png)

1. Sous **[!UICONTROL Conditions]**, cliquez sur l’icône ![Plus](images/icon-plus.png) pour ouvrir l’écran `Condition Configuration`.
   ![Cliquer sur l’icône Plus pour ajouter une nouvelle condition](images/analytics-PDPRuleAddCondition.png)

   1. Sélectionnez **[!UICONTROL Type de condition > Comparaison des valeurs]**.
   1. Utilisez le sélecteur d’élément de données et sélectionnez `Page Type` dans le premier champ.
   1. Sélectionnez **[!UICONTROL Contient]** dans la liste déroulante des opérateurs de comparaison.
   1. Dans le type de champ suivant `product-page` (la partie unique de la valeur de type de page extraite de la couche de données sur les PDP).
   1. Cliquez sur **[!UICONTROL Conserver les modifications]**

      ![Définir la condition](images/analytics-PDP-condition.png)

1. Sous Actions, cliquez sur l’icône ![Plus](images/icon-plus.png) pour ajouter une nouvelle action.

   ![Cliquer sur l’icône Plus pour ajouter une nouvelle action](images/analytics-PDPAddAction.png)

1. Sélectionnez **[!UICONTROL Extension > Adobe Analytics Product String]**.
1. Sélectionnez **[!UICONTROL Type d’action > Définir les s.products]**.

1. Dans la section **[!UICONTROL Événement d’e-commerce Analytics]**, sélectionnez **[!UICONTROL prodView]**.

1. Dans la section **[!UICONTROL Variables de couche de données pour les données de produit]**, utilisez le sélecteur d’élément de données pour sélectionner l’élément de données `Product Id`.

1. Cliquez sur **[!UICONTROL Conserver les modifications]**

   ![Ajouter la variable Chaîne de produit à l’aide de l’extension Adobe Analytics Product String extension](images/analytics-PDPaddProductString.png)


1. Sous Actions, cliquez sur l’icône ![Plus](images/icon-plus.png) pour ajouter une nouvelle action.

   ![Ajouter une autre action pour la Chaîne de produit](images/analytics-PDPaddAnotherAction.png)

1. Sélectionnez **[!UICONTROL Extension > Adobe Analytics]**.
1. Sélectionnez **[!UICONTROL Type d’action > Définir des variables]**.
1. Sélectionnez **[!UICONTROL eVar1 > Définir comme]** et saisissez `product detail page`.
1. Définissez **[!UICONTROL event1]**, en laissant les valeurs facultatives vides.
1. Sous Événements, cliquez sur le bouton **[!UICONTROL Ajouter]**.
1. Définissez l’événement **[!UICONTROL prodView]**, en laissant les valeurs facultatives vides.
1. Cliquez sur **[!UICONTROL Conserver les modifications]**

   ![Définir les variables Analytics dans la règle PDP](images/analytics-PDPsetVariables.png)

1. Cliquez sur **[!UICONTROL Enregistrer dans la bibliothèque et créer]**.

   ![Enregistrer la règle](images/analytics-PDP-saveRule.png)

### Validation des données de la page Détails du produit

Vous venez de créer une règle qui définit les variables avant l’envoi de la balise. Vous devriez maintenant être en mesure d’afficher les nouvelles données sortantes dans l’accès du Experience Cloud Debugger.

**Validation des données de la page Détails du produit**

1. Ouvrez le [site Luma](https://luma.enablementadobe.com/content/luma/us/en.html) dans votre navigateur Chrome.
1. Accédez à une page de détails du produit.
1. Cliquez sur l’icône ![Ouvrir l’Experience Cloud Debugger](images/analytics-debuggerIcon.png) pour ouvrir l’**[!UICONTROL Adobe Experience Cloud Debugger]**.
1. Cliquez sur l’onglet Analytics.
1. Développez votre suite de rapports.
1. Notez les variables de détails du produit qui se trouvent désormais dans le débogueur, à savoir que `eVar1` a été défini sur « page Détails du produit », que la variable `Events` a été définie sur « event1 » et « prodView », que la variable Produits a été définie avec l’ID du produit que vous affichez et que votre Nom de page est toujours défini par l’extension Analytics.

   ![Valider l’accès à la page](images/analytics-validatePDPvars.png)

## Envoi d’une balise Lien de suivi

Lors du chargement d’une page, vous déclenchez généralement une balise de chargement de page déclenchée par la fonction `s.t()`. Cela incrémente automatiquement une mesure `page view` pour la page répertoriée dans la variable `pageName`.

Cependant, il arrive parfois que vous ne souhaitiez pas incrémenter les pages vues sur votre site, étant donné que l’action qui se produit est « plus limitée » (voire différente), par rapport à une page vue. Dans ce cas, vous utiliserez la fonction `s.tl()`, communément appelée « Lien de suivi ». Bien qu’elle soit qualifiée de requête de lien de suivi, il n’est pas nécessaire de la déclencher via un clic sur les liens. Il peut être déclenché par *any* des événements disponibles dans le créateur de règles de balises, y compris votre propre code JavaScript personnalisé.

Dans ce tutoriel, vous déclencherez un appel `s.tl()` à l’aide de l’un des événements JavaScript les plus cool, un événement `Enters Viewport`.

### Le cas d’utilisation

Pour ce cas d’utilisation, vous souhaitez savoir si les visiteurs font suffisamment défiler la page d’accueil Luma pour voir la variable *Produits présentés* de notre page. Nous avons un certain désaccord interne au sein de notre entreprise sur le fait de savoir si les visiteurs voient ou non cette section, vous souhaitez donc utiliser Analytics pour en avoir le cœur net.

### Création de la règle dans les balises

1. Accédez au **[!UICONTROL Règles]** dans le volet de navigation de gauche, puis cliquez sur **[!UICONTROL Ajouter une règle]**

   ![Ajouter une règle](images/analytics-addRule3.png)
1. Attribuez un nom à la règle `Homepage - Featured Products enters Viewport`.
1. Cliquez sur **[!UICONTROL Événements > Ajouter]** pour ouvrir l’écran `Event Configuration`.

   ![Ajouter une règle de produits phares](images/analytics-newArrivalsRuleAdd2.png)

1. Sélectionnez **[!UICONTROL Type d’événement > Entre dans la fenêtre d’affichage]**. Cela ouvre un champ dans lequel vous devez entrer le sélecteur CSS qui identifie l’élément de votre page qui devra déclencher la règle lorsque l’élément entrera dans la fenêtre d’affichage du navigateur.
1. Revenez à la page d’accueil de Luma et faites défiler l’écran jusqu’à la section Produits présentés .
1. Cliquez avec le bouton droit de la souris sur l’espace entre le titre &quot;FEATURED PRODUCTS&quot; et les éléments de cette section, puis sélectionnez `Inspect` dans le menu contextuel. Ça vous rapprochera de ce que vous souhaitez.
1. Tout autour, peut-être juste sous la section sélectionnée, cherchez un élément div avec `class="we-productgrid aem-GridColumn aem-GridColumn--default--12"`. Localisez cet élément.
1. Cliquez avec le bouton droit sur cet élément et sélectionnez **[!UICONTROL Copier > Copier le sélecteur]**.

   ![Entre dans la fenêtre d’affichage](images/analytics-copyElementSelector.png)

1. Revenez aux balises et collez cette valeur du presse-papiers dans le champ intitulé `Elements matching the CSS selector`.
   1. Notez que c’est à vous de décider comment identifier les sélecteurs CSS. Cette méthode est un peu sensible, car certaines modifications sur la page peuvent rompre ce sélecteur. Tenez-en compte lorsque vous utilisez des sélecteurs CSS dans des balises.
1. Cliquez sur **[!UICONTROL Conserver les modifications]**

   ![Entre dans la fenêtre d’affichage](images/analytics-configEntersViewportEvent.png)

1. Sous Conditions, cliquez sur l’icône ![Plus](images/icon-plus.png) pour ajouter une nouvelle condition.
1. Sélectionnez **[!UICONTROL Type de condition > Comparaison des valeurs]**.
1. Utilisez le sélecteur d’élément de données et sélectionnez `Page Name` dans le premier champ.
1. Sélectionnez **[!UICONTROL Égal à]** dans la liste déroulante des opérateurs de comparaison.
1. Dans le type de champ suivant `content:luma:us:en` (Il s’agit du nom de page de la page d’accueil tel qu’il est extrait de la couche de données. Nous voulons seulement que cette règle s’exécute sur la page d’accueil.)
1. Cliquez sur **[!UICONTROL Conserver les modifications]**

   ![Configurer la condition de la page d’accueil](images/analytics-configHomepageCondition.png)

1. Sous Actions, cliquez sur l’icône ![Plus](images/icon-plus.png) pour ajouter une nouvelle action.
1. Sélectionnez **[!UICONTROL Extension > Adobe Analytics]**.
1. Sélectionnez **[!UICONTROL Type d’action > Définir des variables]**.
1. Définissez `eVar3` sur `Home Page - Featured Products`.
1. Définissez `prop3` sur `Home Page - Featured Products`.
1. Définissez la variable `Events` sur `event3`.
1. Cliquez sur **[!UICONTROL Conserver les modifications]**

   ![Entre dans la fenêtre d’affichage](images/analytics-configViewportAction.png)

1. Sous Actions, cliquez sur l’icône ![Plus](images/icon-plus.png) pour ajouter une nouvelle action.

1. Sélectionnez **[!UICONTROL Extension > Adobe Analytics]**.
1. Sélectionnez **[!UICONTROL Type d’action > Envoyer la balise]**.
1. Choisissez la **[!UICONTROL `s.tl()`]** option de suivi
1. Dans le champ **[!UICONTROL Nom du lien]**, saisissez `Scrolled down to Featured Products`. Cette valeur figurera dans le rapport Liens personnalisés dans Analytics.
1. Cliquez sur **[!UICONTROL Conserver les modifications]**

   ![Configurer la balise de produits phares](images/analytics-configEntersViewportBeacon.png)

1. Cliquez sur **[!UICONTROL Enregistrer dans la bibliothèque et créer]**.

   ![Enregistrer la règle et créer](images/analytics-saveCustomLinkRule.png)

### Validation de la balise Lien de suivi

Vous allez maintenant vous assurer que cet accès se déclenche lorsque vous faites défiler l’écran jusqu’à la section Produits présentés de la page d’accueil de notre site. Lorsque vous chargez la page d’accueil pour la première fois, la requête ne doit pas être faite, mais lorsque vous faites défiler la page vers le bas et que la section s’affiche, l’accès doit se déclencher avec les nouvelles valeurs.

1. Ouvrez le [site Luma](https://luma.enablementadobe.com/content/luma/us/en.html) dans votre navigateur Chrome et assurez-vous que vous êtes en haut de la page d’accueil.
1. Cliquez sur l’**[!UICONTROL icône]**![ Ouvrir l’Experience Cloud Debugger](images/analytics-debuggerIcon.png) pour ouvrir l’[!UICONTROL Adobe Experience Cloud Debugger].
1. Cliquez sur l’onglet Analytics.
1. Développez l’accès à votre suite de rapports.
1. Notez l’accès normal à la page vue pour la page d’accueil avec le nom de la page, etc. (mais rien dans eVar3 ou prop3).

   ![Debugger avec une page vue](images/analytics-debuggerPageView.png)

1. Laissez le débogueur ouvert, faites défiler votre site vers le bas jusqu’à ce que vous puissiez voir la section Produits présentés .
1. Affichez de nouveau le débogueur. Un nouvel accès Analytics devrait s’être affiché. Cet accès doit avoir les paramètres associés à l’accès s.tl() que vous configurez, à savoir :
   1. `LinkType = "link_o"` (cela signifie que l’accès est un accès à un lien personnalisé, et non un accès à la page vue).
   1. `LinkName = "Scrolled down to Featured Products"`
   1. `prop3 = "Home Page - Featured Products"`
   1. `eVar3 = "Home Page - Featured Products"`
   1. `Events = "event3"`

      ![Debugger avec une page vue](images/analytics-debuggerEntersViewport.png)

## Ajout d’un plug-in

Un plug-in est un élément de code JavaScript que vous pouvez ajouter à votre mise en œuvre pour exécuter une fonction spécifique qui n’est pas intégrée au produit. Les plug-ins peuvent être conçus par vous, par d’autres clients ou partenaires Adobe ou par Adobe Consulting.

Trois étapes sont possibles pour implémenter des plug-ins :

1. Inclure la fonction doPlugins, à l’endroit où le plug-in sera référencé
1. Ajouter le code de fonction principal correspondant au plug-in
1. Inclure le code qui appelle la fonction et qui définit des variables, etc.

### Accès global à l’objet Analytics

Si vous allez ajouter la fonction doPlugins (ci-dessous) et utiliser des plug-ins, vous devez cocher une case pour rendre l’objet Analytics « s » disponible globalement dans l’implémentation d’Analytics.

1. Accédez à **[!UICONTROL Extensions > Installées]**.

1. Dans l’extension Adobe Analytics, cliquez sur **[!UICONTROL Configurer]**.

   ![Configuration d’Analytics](images/analytics-configureExtension.png)

1. Sous **[!UICONTROL Gestion des bibliothèques]**, sélectionnez la case `Make tracker globally accessible`. Comme vous pouvez le constater dans la bulle d’aide, le suivi sera maintenant inclus globalement dans la portée sous window.s, ce qui sera important lorsque vous y ferez référence dans le code JavaScript de votre client.
   ![Rendre le suivi accessible globalement](images/analytics-makeTrackerGlobal.png)

### Inclusion de la fonction doPlugins

Pour ajouter des plug-ins, vous devez ajouter une fonction intitulée doPlugins. Cette fonction n’est pas ajoutée par défaut, mais une fois ajoutée, elle est gérée par la bibliothèque AppMeasurement et appelée en dernier lorsqu’un accès est envoyé dans Adobe Analytics. Par conséquent, vous pouvez utiliser cette fonction pour exécuter certains codes JavaScript afin de définir des variables plus facilement définies de cette manière.

1. Pendant que vous êtes toujours dans l’extension Analytics, faites défiler l’écran vers le bas et développez la section intitulée `Configure Tracker Using Custom Code.`
1. Cliquez sur **[!UICONTROL Ouvrir l’éditeur]**.
1. Collez le code suivant dans l’éditeur de code :

   ```javascript
   /* Plugin Config */
   s.usePlugins=true
   s.doPlugins=function(s) {
   /* Add calls to plugins here */
   }
   ```

1. Laissez cette fenêtre ouverte pour l’étape suivante

### Ajout d’un code de fonction pour le plug-in

Vous allez en fait appeler deux plug-ins dans ce code, mais l’un d’eux est intégré dans la bibliothèque AppMeasurement. Pour celui-ci, vous n’avez donc pas besoin d’ajouter la fonction à appeler. Toutefois, pour le second, vous devez ajouter le code de fonction. Cette fonction s’intitule getValOnce().

### Le plug-in getValOnce()

Ce plug-in a pour objectif d’éviter que les valeurs ne soient incorrectement dupliquées dans le code lorsqu’un visiteur actualise une page ou utilise le bouton Précédent du navigateur pour revenir à une page sur laquelle une valeur a été définie. Dans cette leçon, vous l’utiliserez pour empêcher la duplication de l’événement `clickthrough`.

Le code de ce plug-in est disponible dans la [documentation d’Analytics](https://experienceleague.adobe.com/docs/analytics/implementation/vars/plugins/getvalonce.html), mais il est inclus ici pour faciliter le copier-coller.

1. Copiez le code suivant.

   ```javascript
   /* Adobe Consulting Plugin: getValOnce v2.01 */
   s.getValOnce=function(vtc,cn,et,ep){if(vtc&&(cn=cn||"s_gvo",et=et||0,ep="m"===ep?6E4:864E5,vtc!==this.c_r(cn))){var e=new Date;e.setTime(e.getTime()+et*ep);this.c_w(cn,vtc,0===et?0:e);return vtc}return""};
   ```

1. Collez-le dans la fenêtre de code de l’extension Analytics (si vous ne l’avez pas encore ouvert, rouvrez-le comme indiqué à l’étape précédente), **complètement sous** la fonction doPlugins (et non à l’intérieur).

   ![Ajouter un code de plug-in](images/analytics-doPluginsAndGeValOnceCode2.png)

Vous pouvez désormais appeler ce plug-in au sein de doPlugins.

### Appel de plug-ins au sein de doPlugins

Maintenant que le code est là et qu’il peut être référencé, vous pouvez adresser des appels aux plug-ins au sein de la fonction doPlugins.

Tout d’abord, appelez un plug-in qui a été intégré à la bibliothèque AppMeasurement, appelé « Utilitaire ». On y fait référence en tant que `s.Util.getQueryParam`, puisqu’il fait partie de l’objet s, qu’il est un utilitaire intégré et qu’il va prendre des valeurs (basées sur un paramètre) de la chaîne de requête dans l’URL.

1. Copiez le code suivant :

   ```javascript
   s.campaign = s.Util.getQueryParam("cid");
   ```

1. Collez-le dans la fonction doPlugins. Cela lancera une recherche de paramètre appelé `cid` dans l’URL de la page actuelle et le placera dans la variable s.campaign.
1. Appelez la fonction getValOnce en copiant le code suivant et en le collant directement sous l’appel à getQueryParam :

   ```javascript
   s.campaign=s.getValOnce(s.campaign,'s_cmp',30);
   ```

   Ce code s’assure que la même valeur n’est pas envoyée plus d’une fois de suite pendant 30 jours (consultez la documentation pour savoir comment personnaliser ce code selon vos besoins).

   ![Appeler des plug-ins dans doPlugins](images/analytics-doPluginsWithPlugins2.png)

1. Enregistrez la fenêtre de code
1. Cliquez sur **[!UICONTROL Enregistrer dans la bibliothèque et créer]**.

   ![Appeler des plug-ins dans doPlugins](images/analytics-saveExtensionAndBuild2.png)

### Validation des plug-ins

Vous pouvez désormais vous assurer que les plug-ins fonctionnent.

**Validation des plug-ins**

1. Ouvrez le [site Luma](https://luma.enablementadobe.com/content/luma/us/en.html) dans votre navigateur Chrome.
1. Cliquez sur l’icône ![Ouvrir l’Experience Cloud Debugger](images/analytics-debuggerIcon.png) pour ouvrir l’**[!UICONTROL Adobe Experience Cloud Debugger]**.
1. Cliquez sur l’onglet Analytics.
1. Développez votre suite de rapports.
1. Notez que l’accès à Analytics n’a pas de variable Campaign.
1. Laissez le débogueur ouvert, puis revenez au site Luma et ajoutez `?cid=1234` à l’URL. Appuyez ensuite sur Entrée pour actualiser la page en incluant cette chaîne de requête.

   ![Ajouter une chaîne de requête](images/analytics-cidAdded.png)

1. Vérifiez le débogueur et confirmez l’existence d’une seconde requête Analytics avec une variable Campaign définie sur `1234`.

   ![getQueryParam, étape 1](images/analytics-getQueryParam1.png)

1. Revenez en arrière et actualisez à nouveau la page Luma, avec la chaîne de requête toujours dans l’URL.
1. Vérifiez l’accès suivant dans le débogueur. La variable Campagne **ne doit pas** être présente, car le module getValOnce s’est assuré qu’elle n’est pas dupliquée et qu’elle ne ressemble pas à une autre personne issue du code de suivi de campagne.

   ![getQueryParam, étape 1](images/analytics-getQueryParam2.png)

1. BONUS : vous pouvez le tester autant de fois que vous le souhaitez en modifiant la valeur du paramètre `cid` dans la chaîne de requête. La variable Campaign ne doit être présente qu’à condition qu’il existe une **première** exécution de la page avec la valeur. Si vous ne voyez pas la valeur Campaign dans le débogueur, modifiez simplement la valeur du `cid` dans la chaîne de requête de l’URL et appuyez sur Entrée pour la voir à nouveau dans le débogueur.

   >[!NOTE]
   >
   >Il existe en fait plusieurs manières différentes de récupérer un paramètre en dehors de la chaîne de requête de l’URL, y compris dans la configuration de l’extension Analytics. Toutefois, dans ces autres options qui ne se rapportent pas aux plug-ins, elles ne permettent pas d’arrêter la duplication inutile, comme vous l’avez fait ici avec le plug-in getValOnce. Il s’agit de la méthode préférée de l’auteur, mais vous devez déterminer la méthode qui vous convient le mieux, ainsi qu’à vos besoins.

Beau travail ! Vous avez terminé la leçon sur Analytics. Bien sûr, vous pouvez faire bien d’autres choses pour améliorer notre mise en oeuvre d’Analytics, mais nous espérons que cela vous a donné certaines des compétences de base pour répondre au reste de vos besoins.

[Suite : « Ajout d’Adobe Audience Manager » >](audience-manager.md)
