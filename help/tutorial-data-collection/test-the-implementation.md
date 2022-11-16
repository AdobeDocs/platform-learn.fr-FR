---
title: Test de l’implémentation
description: Test de l’implémentation
exl-id: 66eb1d4e-32eb-45fc-8da4-8d3c04dc3c7a
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '599'
ht-degree: 2%

---

# Test de l’implémentation

Maintenant que votre page web est configurée et que votre bibliothèque de balises Adobe Experience Platform est déployée, il est temps de tester l’implémentation.

1. Ouvrez votre page de produits dans votre navigateur. Pour ce faire, cliquez sur _Fichier_ then _Ouvrir le fichier..._ dans votre navigateur ou vous pouvez héberger votre page sur un serveur web et saisir l’URL appropriée.

Une fois la page chargée, vous devriez voir quelque chose comme ceci :
![Page web](assets/webpage.png)

Ce n&#39;est pas joli, mais ça fait le boulot.

## Inspect des événements de page vue et de consultation de produit

1. Ouvrez les outils de développement dans votre navigateur, puis cliquez sur le panneau Réseau. Actualisez votre page.
À ce stade, vous devriez voir quatre requêtes :
* product.html - Votre page web.
* launch-############-development.js - Votre bibliothèque Launch.
* interaction : événement de page vue envoyé au serveur.
* interaction : événement de consultation de produit envoyé au serveur.
Inspect de la payload de chaque requête :
1. Pour la première `interact` vous devriez pouvoir voir la charge utile envoyée avec une `eventType` de `web.webpagedetails.pageViews`.
   ![Inspection de requête de page vue](assets/webpage-page-viewed-inspection.png)
1. Pour la seconde `interact` vous devriez pouvoir voir la charge utile envoyée avec une `eventType` de `commerce.productViews`.
   ![Inspection de la demande d’affichage de produit](assets/webpage-product-view-inspection.png)
1. Passez en revue le reste des données envoyées, y compris les informations sur le produit.

## Inspect du panier ouvert et ajout aux événements du panier

1. Cliquez maintenant sur le **_Ajouter au panier_**.

Vous devriez voir deux requêtes supplémentaires, la première avec une `eventType` de `commerce.productListOpens` (pour ouvrir un nouveau panier) et la seconde avec un `eventType` de `commerce.productListAdds` (pour ajouter le produit au panier).

## Inspect : événement de clic sur les liens de l’application de téléchargement

En fonction du navigateur, un clic sur un lien qui vous éloigne de la page active peut effacer votre panneau réseau. Puisque vous souhaitez examiner la demande réseau pour l’événement de clic sur les liens qui se produit juste avant de quitter la page, vous devez configurer votre navigateur pour conserver les journaux réseau sur toutes les pages.

1. Conserver les journaux réseau en cochant la variable **_Conserver le journal_** dans le panneau réseau (Chrome, Safari, Edge) ou en cliquant sur une icône d’engrenage et en cochant une **_Journaux persistants_** dans le menu affiché (Firefox).
1. Cliquez sur le bouton **_Téléchargement de l’application_** lien. Vous devriez en voir une de plus. `interact` s’affiche dans le panneau réseau.
1. Recherchez la requête avec une `eventType` de `web.webinteraction.linkClicks`, puis passez en revue les détails du lien sur lequel l’utilisateur a cliqué.

## Vérifier que les données arrivent dans le jeu de données Adobe Experience Platform

Maintenant que les requêtes sont envoyées, vérifiez si les données arrivent en toute sécurité dans le jeu de données Adobe Experience Platform que vous avez créé.

1. Accédez au **[!UICONTROL Jeux de données]** dans Adobe Experience Platform.
1. Sélectionnez la [dataset](configure-the-server/create-a-dataset.md) que vous avez créé pour ce tutoriel.
Vous devrez peut-être attendre quelques minutes, mais bientôt, des informations sur les données en cours de traitement et insérées dans votre jeu de données s’afficheront. Vous devriez également voir si le traitement a réussi ou échoué. En cas d’échec, vous voyez pourquoi il a échoué. Des échecs se produisent généralement car les données que vous envoyez ne correspondent pas au schéma et vous devez ajuster vos données ou votre schéma en conséquence.
   ![Ingestion des jeux de données](assets/dataset-ingestion.png)

## Utilisation de l’extension Adobe Experience Platform Debugger

Pour plus d’informations sur le comportement de votre mise en oeuvre sur le navigateur et sur les serveurs d’Adobe, consultez l’extension de navigateur Adobe Experience Platform Debugger .

[Extension Adobe Experience Platform Debugger pour Chrome](https://chrome.google.com/webstore/detail/adobe-experience-platform/bfnnokhpnncpkdmbokanobigaccjkpob)

[Extension Adobe Experience Platform Debugger pour Firefox](https://addons.mozilla.org/fr/firefox/addon/adobe-experience-platform-dbg/)

[Suivant : ](summary.md)

>[!NOTE]
>
>Merci d’avoir consacré votre temps à l’apprentissage de la collecte de données. Si vous avez des questions, souhaitez partager des commentaires généraux ou avez des suggestions sur le contenu futur, partagez-les à ce sujet. [Article de discussion de la communauté Experience League](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-launch/tutorial-discussion-use-adobe-experience-platform-data/m-p/543877)