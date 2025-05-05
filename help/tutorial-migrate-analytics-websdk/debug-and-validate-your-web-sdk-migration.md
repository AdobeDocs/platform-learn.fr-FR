---
title: Déboguer et valider la migration de Web SDK
description: Découvrez comment déboguer et valider vos données lors de la migration vers Web SDK
solution: Data Collection, Analytics
feature: Web SDK
jira: KT-16763
exl-id: 68f87266-4b87-4953-8de4-6a9a62bac9e6
source-git-commit: 7c0a6c769d56b3e56a5667d5aeff47b55ab6dc33
workflow-type: tm+mt
source-wordcount: '1253'
ht-degree: 0%

---

# Déboguer et valider la migration de Web SDK

Dans cet exercice, vous apprendrez à déboguer et à valider vos données lors de la migration vers le SDK Web. Nous souhaitons encourager deux activités de validation différentes qui peuvent vous aider à vous assurer que tout fonctionne correctement :

1. Le **#1 d’activité de validation** exécute l’Adobe Experience Platform Debugger , qui est une extension de navigateur, et vous permet de vérifier le long du chemin que vos données sont correctement envoyées dans Analytics. Il est recommandé d’effectuer cette activité fréquemment, car vous apportez des modifications à votre propriété de balises et publiez les modifications dans une bibliothèque de développement.
1. L’activité de validation **#2** va dans Adobe Analytics, configure un ou plusieurs projets pour recevoir des données de Web SDK (via votre nouvelle suite de rapports de migration) et vérifie que vos données sont bien intégrées dans les rapports lorsque vous cliquez sur votre site, etc.

## L&#39;Adobe Experience Platform Debugger

Ce débogueur est une extension de navigateur disponible sur le magasin Chrome. Il existe un [ tutoriel vidéo](https://experienceleague.adobe.com/fr/docs/platform-learn/data-collection/debugger/overview) qui explique comment télécharger et utiliser le débogueur, et il est recommandé de le parcourir d’abord pour en connaître l’utilisation de base.

Une fois le débogueur opérationnel, vous pouvez l’utiliser pour vous assurer que les données circulent correctement depuis votre site et via l’Edge Network. Ce tutoriel sera utilisé de manière assez basique, mais veuillez utiliser le débogueur à sa pleine capacité pour vérifier vos données.

**Hypothèse (toujours dangereuse, mais j’espère qu’elle conviendra dans ce cas) :** étant donné que nous effectuons la migration de la propriété des balises vers le SDK web dans cet exemple, nous n’avons pas besoin de placer un nouveau code incorporé sur le site. Il y en aura déjà eu. Cependant, si vous décidez d’adopter davantage une approche « lift and shift » (effet élévateur et déplacement) sur une propriété de balises entièrement nouvelle, vous disposerez de nouveaux codes incorporés à placer sur vos environnements de développement, d’évaluation et de production. Dans le cas de ce tutoriel, tant que l’extension Web SDK est installée et configurée avec des règles qui envoient des données, les données s’affichent dans le débogueur.

### Affichage des données de Web SDK dans le débogueur

Maintenant que vous avez migré votre règle de page par défaut (ou si vous avez migré des règles) et que vous l’avez publiée dans une bibliothèque dans l’environnement de développement, vous devriez être en mesure d’exécuter votre site et de voir les données qui circulent dans le débogueur.

Étapes d’affichage des données :

1. Ouvrez l’environnement de développement de votre site dans le navigateur
1. Ouvrez le débogueur en cliquant sur l’extension de navigateur dans la barre d’état des extensions située en haut de la fenêtre du navigateur

   ![Extension Debugger](assets/debugger-extension.jpg)

   >[!TIP]
   >
   >Dans le coin inférieur droit du débogueur se trouve une icône et un libellé « Verrouiller ». À gauche de celui-ci, vous pouvez voir la page que vous déboguez. Sur votre site, cliquez sur l’icône de verrouillage, qui verrouille le débogueur sur la fenêtre de votre site. Dans le cas contraire, si vous cliquez dans un autre onglet/une autre fenêtre de navigateur, le débogueur répond à ce site. Lors du débogage de votre site, il est simplement plus facile de s’assurer que le débogueur vous donne toujours des informations sur votre site.

1. Vérifiez que vous vous trouvez sur la page **Résumé** du débogueur (icône « Accueil » en haut à gauche). **Actualisez votre site** dans sa fenêtre de navigateur. Si le débogueur récupère le code incorporé sur votre site et que vous n’avez pas supprimé le code Analytics (conformément à ce tutoriel), des indications s’affichent indiquant qu’il existait du code pour Adobe Experience Platform Web SDK et Adobe Analytics, ainsi que pour les balises Adobe Experience Platform. Les autres seront grisés.

   ![Résumé du débogueur](assets/debugger-summary.jpg)

1. Pour afficher les données ajoutées via le SDK Web, cliquez sur le lien **SDK Web Experience Platform** dans le rail de gauche
1. Cliquez sur **Effacer les événements** simplement pour supprimer les accès qui se sont produits
1. Actualisez à nouveau votre site et revenez au débogueur
1. Cliquez ensuite sur le champ de données en regard de **événements** dans le tableau

   ![Champ Events dans le débogueur](assets/events-field-in-debugger.jpg)

1. Dans le champ Valeur , développez jusqu’à 0, data, __adobe et analytics
1. Vous devriez voir les variables que vous définissez dans la ou les règles qui se déclenchent sur cette page, y compris la règle de chargement de page par défaut et les règles spéciales.

   ![Objet de données dans le débogueur](assets/data-object-in-debugger.jpg)

1. Effectuez ces étapes chaque fois que vous avez modifié quelque chose dans votre propriété de balises et que vous avez publié les modifications apportées au développement, afin de voir l’effet des modifications que vous avez apportées à votre implémentation Analytics.

## Validation des données dans Analysis Workspace

L’essentiel de cette recommandation est de prendre vos données d’analyse actuelles provenant de votre implémentation de balises à l’aide de l’extension Adobe Analytics et de les comparer aux mêmes rapports qui seront désormais remplis par le SDK Web.
Il y a peut-être plusieurs façons d&#39;établir ces comparaisons, mais je vais vous donner deux exemples de la façon de le faire.

### Option 1 : comparer les données à l’aide de deux panneaux dans un seul projet

1. Création d’un projet dans Analysis Workspace et ajout de deux panneaux
1. Définissez la suite de rapports du panneau 1 sur votre suite de rapports de production Adobe Analytics actuelle
1. Définissez la suite de rapports du panneau 2 sur votre nouvelle suite de rapports de développement Web SDK
1. Placez le même rapport dans les deux panneaux, en utilisant une période qui inclut des jours complets uniquement où les données ont été envoyées aux deux suites de rapports
1. Comparer les données

Voici à quoi cela pourrait ressembler (étant entendu qu’il n’existe aucune donnée dans ces suites de rapports de démonstration vides) :

![Comparer les numéros de suites de rapports](assets/compare-report-suite-numbers-panels.jpg)

Comme vous pouvez le voir, le rapport est le même dans les deux panneaux, et le calendrier est le même également. La différence réside dans la suite de rapports, comme indiqué dans les étapes ci-dessus.
**Avantage de cette option :** vous pouvez procéder un par un avec des rapports/dimensions et tester exactement ce que vous souhaitez tester, au fur et à mesure des modifications apportées à l’implémentation.

### Option 2 : comparaison des données à l’aide de deux projets

1. Ouvrir un projet existant qui utilise vos données d’extension Adobe Analytics actuelles
1. Effectuez un « Enregistrer sous » pour faire une copie de ce projet, en le nommant par exemple « Projet de validation de la migration de Web SDK ».
1. Modifiez la suite de rapports du projet copié afin qu’elle pointe vers votre suite de rapports de développement Web SDK
1. Ouvrez chaque projet dans une fenêtre différente et dimensionnez-les de sorte que vous puissiez les voir les uns à côté des autres sur votre écran
1. Comparer les données

Cela ressemblera beaucoup à l’image ci-dessus, sauf que chaque panneau se trouve dans son propre projet et dans une fenêtre différente.
**Avantage de cette option :** dans ce cas, il n’est pas nécessaire d’ajouter et de configurer à nouveau tous vos rapports, mais vous pouvez voir à quoi ressembleront vos rapports actuels à l’aide de la nouvelle extension de SDK Web avec une configuration minimale.

Il est possible que vous souhaitiez faire les deux, ce qui est également une autre excellente option.

>[!IMPORTANT]
>
>Maintenant que vous avez terminé de valider votre règle de chargement de page par défaut, vous pouvez passer au tutoriel. Cependant, nous vous implorons de tester/valider souvent, probablement au moins chaque fois que vous modifiez une règle ou apportez d’autres modifications importantes. N’oubliez pas que si vous constatez un problème au fur et à mesure, vous serez plus heureux si vous n’avez qu’à vérifier UNE seule chose au lieu de tester plusieurs modifications que vous avez apportées depuis la dernière validation.

Bonne validation !
