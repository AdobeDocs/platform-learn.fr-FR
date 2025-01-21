---
title: Migrer les règles de page supplémentaires
description: Découvrez comment migrer des règles supplémentaires basées sur des pages vers l’extension Web SDK.
solution: Data Collection, Analytics
feature: Web SDK
jira: KT-16764
exl-id: d1345da7-018d-4c0c-ba9b-d4ff7b35df03
source-git-commit: 7c0a6c769d56b3e56a5667d5aeff47b55ab6dc33
workflow-type: tm+mt
source-wordcount: '732'
ht-degree: 0%

---

# Migrer les règles de page supplémentaires

Dans cet exercice, vous apprendrez à migrer des règles supplémentaires basées sur des pages vers l’extension Web SDK. Vous constaterez que cet exercice est similaire à celui que vous avez déjà effectué lors de la migration de votre règle de chargement de page par défaut vers Web SDK. Les méthodes s’appliquent toujours. La plus grande différence est qu’avec ces règles, vous n’ajouterez pas d’action Envoyer l’événement, car dans la plupart des cas, votre règle ne contient pas d’action Envoyer la balise d’une extension Analytics.

## Vue d’ensemble

Revenons un peu en arrière et parlons des implémentations Analytics telles qu’elles sont avec l’extension Adobe Analytics tags (également appelée implémentation « AppMeasurement », puisqu’il s’agit du nom du fichier JavaScript).

Je ne vais pas présumer de la manière exacte dont vous êtes implémenté, mais dans de nombreuses implémentations utilisant des balises Experience Platform, un certain nombre de règles ne se déclenchent que de manière conditionnelle, en fonction de quelque chose sur la page ou dans l’URL. Voici quelques exemples :

* Règle de résultats de recherche, qui ne se déclenche que lorsqu’une recherche interne a été effectuée et que la page de résultats de recherche s’affiche
* Règle de page de destination de Campaign, déclenchée uniquement lorsqu’il existe un code de suivi dans l’URL
* Règle de type de page, déclenchée uniquement pour une page qui est un certain type de page, par exemple la page des détails du produit, la page du panier, etc.
* Toute autre page qui se déclenche de manière conditionnelle

Le point essentiel ici est que tous ces cas d’utilisation ne se déclenchent que **parfois** sur une page. Nous nous attendons **également** à ce que la règle de page par défaut se déclenche. Par conséquent, nous ne voulons pas inclure une balise d’envoi (extension AA) ou un événement d’envoi (extension Web SDK) avec l’une de ces règles, sinon cela entraînerait deux accès pour le même chargement de page.

Par conséquent, ces règles créent l’objet , mais elles n’envoient pas les données. Nous nous assurons simplement que ces règles se déclenchent **avant** la règle de chargement de page par défaut, de sorte qu’après avoir créé l’objet , l’action Envoyer la balise/Envoyer l’événement sur la règle de chargement de page par défaut envoie tout le contenu. Maintenant, il est probable que vous sachiez tout cela, et c’est ainsi que votre site est configuré. Cependant, si vous découvrez votre propre mise en œuvre ou si vous devez la « corriger » pour qu’elle ressemble à cette méthode, cet exercice s’avère particulièrement utile.

## Exemple de migration d’une règle conditionnelle

Voici un exemple de migration d’une règle qui se déclenche de manière conditionnelle. Je vais utiliser l’exemple ci-dessus d’une page de destination de campagne. Comme je l’ai dit plus haut, cela suit le même modèle que celui avec lequel nous avons déjà travaillé dans notre règle de page par défaut, sauf que c’est encore plus facile, car nous définissons uniquement des variables et ne déclenchons aucun accès.

1. Recherchez la règle conditionnelle. Dans cet exemple, nous trouvons la règle de code de suivi de campagne et la sélectionnons.

   ![Sélection de la règle de code de suivi Campaign](assets/campaign-tracking-code-rule-select.jpg)

1. Lorsque la règle s’ouvre, nous pouvons constater qu’il existe une condition sur le déclenchement de cette règle en fonction d’un paramètre de chaîne de requête. Nous n’avons pas besoin de modifier quoi que ce soit à propos de la condition, car nous voulons uniquement mettre à jour/migrer l’action, et non l’événement ou la condition.
1. Cliquez dans l’action **Adobe Analytics - Définir la variable**
1. Notez tout ce qui est défini dans l’action. Dans cet exemple, nous remarquons que la variable **event101** est définie, ainsi que la variable **Campaign**.

   ![event101](assets/event101.jpg)
   ![var de campagne](assets/campaign-variable.jpg)

1. Nous avons seulement cliqué ici pour faire la note, et nous n&#39;avons pas besoin de modifier quoi que ce soit, donc maintenant nous pouvons simplement cliquer sur **annuler**.
1. Créez une action en cliquant sur l’icône **plus** dans la section Actions

   ![nouvelle action](assets/new-action-conditional-rule.jpg)

1. Configurer la nouvelle règle
   1. Sélectionnez **Adobe Experience Platform Web SDK** dans la liste déroulante Extension .
   1. Sélectionnez **Mettre à jour la variable** dans le menu déroulant Type d’action .
   1. Dans le panneau de droite, sélectionnez l’objet **Analytics** dans l’objet de données

      ![Action Mettre à jour la variable](assets/configure-conditional-rule-action.jpg)

1. Définissez maintenant event101 et la variable de campagne sur les mêmes valeurs que celles définies dans l’action existante.

   ![Définir event101](assets/web-sdk-event101.jpg)
   ![Définir la campagne](assets/web-sdk-campaign-var.jpg)

1. Vous pouvez désormais **Conserver les modifications** et **Enregistrer dans la bibliothèque** et votre règle a été migrée vers Web SDK.

>[!IMPORTANT]
>
>Comme pour la règle de chargement de page par défaut, nous avons conservé l’action **Définir la variable** de l’extension Analytics dans la règle afin de pouvoir comparer les données lors de la validation de la migration. N’oubliez pas de revenir plus tard et de supprimer l’action de l’extension Analytics lors du nettoyage final.
