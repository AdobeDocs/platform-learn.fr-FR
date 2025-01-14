---
title: Suppression des éléments d’extension Adobe Analytics
description: Une fois le débogage et la validation terminés, supprimez toutes les références aux éléments d’extension Adobe Analytics et supprimez l’extension elle-même.
solution: Data Collection, Analytics
feature: Web SDK
jira: KT-16766
source-git-commit: 7ae56d997884cf1558e72c0ad553df1c5d43c081
workflow-type: tm+mt
source-wordcount: '563'
ht-degree: 0%

---


# Suppression des éléments d’extension Adobe Analytics

Une fois le débogage et la validation terminés, supprimez toutes les références aux éléments d’extension Adobe Analytics et supprimez l’extension elle-même.

## Vue d’ensemble

Une fois que vous êtes satisfait(e) que tout le contenu de votre propriété a été migré vers Web SDK et que vous avez terminé le débogage et la validation (dans votre environnement de développement), vous êtes prêt(e) à supprimer les références à l’extension Adobe Analytics. C’est à vous de décider à quelle vitesse vous supprimez ces éléments et combien de fois vous les testez pendant que vous le faites. Si vous souhaitez être plus prudent, supprimez les références lentement et testez-les entre chaque suppression. Si vous êtes certain que tout fonctionne correctement et que la migration est correcte, vous pouvez « arracher le pansement » et supprimer tous les éléments. Nous recommanderions tout de même des tests à la fin de l&#39;exercice, bien sûr.

## Supprimer les anciennes actions des règles

Encore une fois, nous allons supposer que vous avez déjà tout testé et que cela fonctionne correctement. À ce stade, vous pouvez accéder à vos règles une par une et supprimer les actions appartenant à l’extension Adobe Analytics.

1. Ouvrez l’une de vos règles, par exemple votre règle de chargement de page par défaut.
1. Après avoir effectué la migration de cette règle, vous disposez probablement de 4 actions (ou plus).

   ![Les 4 actions](assets/all-four-actions.jpg)

1. Vous pouvez constater que les deux premiers comportent l’identifiant « Adobe Analytics ». Il s’agit des actions que nous voulons supprimer.
1. Placez le pointeur de la souris sur la première, comme l’action « Adobe Analytics - Définir les variables », et un X s’affiche pour permettre la suppression. Cliquez sur le X et l’action disparaît. Supprimez toutes les actions Adobe Analytics de la règle, dans ce cas l’action Définir la variable et l’action Envoyer la balise .
1. Il ne restera alors que les actions de Web SDK

   ![Actions de Web SDK uniquement](assets/websdk-actions-only.jpg)

1. Enregistrer dans la bibliothèque
1. Créez la bibliothèque et testez votre site pour vous assurer qu’il n’y a aucune nouvelle erreur et que tout fonctionne correctement
1. Répétez cette action pour les autres règles, en créant dans votre bibliothèque de développement et en effectuant des tests entre chaque suppression (ou aussi souvent que vous le souhaitez). Vous pouvez simplement effectuer un test dans le débogueur ou vérifier les rapports dans la suite de rapports de migration, là encore en fonction de votre niveau de confort.

## Supprimer les extensions

Maintenant que vous avez supprimé les références à votre extension Adobe Analytics, vous pouvez supprimer (ou désactiver) l’extension, ainsi que toutes les autres extensions qui l’utilisent ou qui en dépendent. Personnellement, j&#39;aime une approche prudente, et donc « désactiver » est mon choix au lieu de désinstaller, du moins au début.

1. Sélectionnez **Extensions** dans le rail de gauche de l’interface utilisateur.
1. Assurez-vous que l’onglet **Installé** est sélectionné.
1. Sélectionnez l’extension Adobe Analytics.
1. Sur le rail de droite, choisissez de désactiver l’extension (ou cliquez sur les trois points et désinstallez si vous préférez).

   ![Désactiver l’extension Analytics](assets/disable-analytics-extension.jpg)

1. Faites de même pour l’extension du service d’ID d’Experience Cloud, car vous n’en aurez plus besoin. L’extension Web SDK gère l’identifiant. Vous n’avez donc pas besoin de l’extension supplémentaire.
1. Faites de même pour toutes les autres extensions associées à l’extension Adobe Analytics, mais uniquement après avoir effectué les modifications de migration nécessaires.
1. Créez les modifications dans votre environnement de développement.

