---
title: Test de l’implémentation
description: Test de l’implémentation
role: Developer
level: Intermediate
recommendations: noDisplay,noCatalog
jira: KT-10447
hide: true
hidefromtoc: true
exl-id: e2213c23-d395-4c57-8c6c-0319cd0fb0ac
source-git-commit: 90f7621536573f60ac6585404b1ac0e49cb08496
workflow-type: tm+mt
source-wordcount: '575'
ht-degree: 2%

---

# Test de l’implémentation

Maintenant que votre page web est configurée et que votre bibliothèque de balises Adobe Experience Platform est déployée, il est temps de tester l’implémentation.

Ouvrez votre page de produits dans votre navigateur. Pour ce faire, cliquez sur _Fichier_ then _Ouvrir le fichier..._ dans votre navigateur ou vous pouvez héberger votre page sur un serveur web et saisir l’URL appropriée.

Une fois la page chargée, vous devriez voir quelque chose comme ceci :

![Page web](../../assets/implementation-strategy/webpage.png)

Ce n&#39;est pas joli, mais ça fera le boulot.

## Inspect des événements de page vue et de consultation de produit

Ouvrez les outils de développement dans votre navigateur, puis cliquez sur le panneau Réseau. Actualisez votre page.

À ce stade, vous devriez voir quatre requêtes :

1. product.html - Votre page web.
2. launch-############-development.js - Votre bibliothèque Launch.
3. interaction : événement de page vue envoyé au serveur.
4. interaction : événement de consultation de produit envoyé au serveur.

N’hésitez pas à examiner les payloads de chaque requête. Pour la première `interact` vous devriez pouvoir voir la charge utile envoyée avec une `eventType` de `web.webpagedetails.pageViews`.

![Inspection de requête de page vue](../../assets/implementation-strategy/webpage-page-viewed-inspection.png)

Pour la seconde `interact` vous devriez pouvoir voir la charge utile envoyée avec une `eventType` de `commerce.productViews`.

![Inspection de la demande d’affichage de produit](../../assets/implementation-strategy/webpage-product-view-inspection.png)

N’hésitez pas à parcourir le reste des données envoyées, y compris les informations sur les produits.

## Inspect du panier ouvert et ajout aux événements du panier

Cliquez maintenant sur le bouton _Ajouter au panier_ bouton .

Vous devriez voir deux requêtes supplémentaires, la première avec une `eventType` de `commerce.productListOpens` (pour ouvrir un nouveau panier) et la seconde avec un `eventType` de `commerce.productListAdds` (pour ajouter le produit au panier).

## Inspect : événement de clic sur les liens de l’application de téléchargement

En fonction du navigateur, un clic sur un lien qui vous éloigne de la page active peut effacer votre panneau réseau. Puisque vous souhaitez examiner la demande réseau pour l’événement de clic sur les liens qui se produit juste avant de quitter la page, vous devez configurer votre navigateur pour conserver les journaux réseau entre les pages. Pour ce faire, cochez une _Conserver le journal_ dans le panneau réseau (Chrome, Safari, Edge) ou en cliquant sur une icône d’engrenage et en cochant une _Journaux persistants_ dans le menu affiché (Firefox).

Cliquez maintenant sur le bouton _Téléchargement de l’application_ lien.

Vous devriez en voir une de plus. `interact` s’affiche dans le panneau réseau. Si vous examinez la requête, vous devez trouver une `eventType` de `web.webinteraction.linkClicks` ainsi que des détails sur le lien sur lequel l’utilisateur a cliqué.

## Vérifier que les données arrivent dans le jeu de données Adobe Experience Platform

Maintenant que les requêtes sont envoyées, vous souhaitez également vérifier si les données arrivent en toute sécurité dans le jeu de données Adobe Experience Platform que vous avez créé. Commencez par accéder au [!UICONTROL Jeux de données] dans Adobe Experience Platform.

Sélectionnez le jeu de données que vous avez précédemment créé.

Vous devrez peut-être attendre quelques minutes, mais bientôt, des informations sur les données en cours de traitement et insérées dans votre jeu de données s’afficheront. Vous devriez également voir si le traitement a réussi ou échoué. En cas d&#39;échec, vous pourrez voir pourquoi il a échoué. Des échecs se produisent généralement car les données que vous envoyez ne correspondent pas au schéma et vous devrez ajuster vos données ou votre schéma en conséquence.

![Ingestion des jeux de données](../../assets/implementation-strategy/dataset-ingestion.png)

## Utilisation de l’extension Adobe Experience Platform Debugger

Pour plus d’informations sur le comportement de votre mise en oeuvre sur le navigateur et sur les serveurs d’Adobe, consultez l’extension de navigateur d’Adobe Experience Platform Debugger !

[Extension Adobe Experience Platform Debugger pour Chrome](https://chrome.google.com/webstore/detail/adobe-experience-platform/bfnnokhpnncpkdmbokanobigaccjkpob)

[Extension Adobe Experience Platform Debugger pour Firefox](https://addons.mozilla.org/fr/firefox/addon/adobe-experience-platform-dbg/)
