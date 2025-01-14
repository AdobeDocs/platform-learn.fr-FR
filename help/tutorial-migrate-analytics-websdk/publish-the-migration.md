---
title: Publish de la migration vers l’évaluation et la production
description: Une fois tous les développements terminés pour la migration et validés, effectuez la génération vers l’évaluation, puis publiez en production lorsque vous êtes prêt.
solution: Data Collection, Analytics
feature: Web SDK
jira: KT-16767
source-git-commit: 15f2122c53a3b2f3dc1942502e908403e55519ab
workflow-type: tm+mt
source-wordcount: '568'
ht-degree: 0%

---


# Publish de la migration vers l’évaluation et la production

Une fois tous les développements terminés pour la migration et validés, effectuez la génération vers l’évaluation, puis publiez en production lorsque vous êtes prêt.

## Vue d’ensemble

Il s’agit réellement de la dernière étape principale de votre migration, qui consiste à déplacer la bibliothèque que vous avez utilisée pour développer et tester votre migration vers votre environnement d’évaluation pour y effectuer les tests finaux, puis vers l’environnement de production.

Si vous revenez à la leçon [Créer et configurer un flux de données](create-and-configure-the-analytics-datastream.md), vous verrez à la fin que nous avons indiqué le flux de données d’évaluation pour envoyer les données d’analyse à la même suite de rapports de développement (ou à une nouvelle suite de rapports d’évaluation). Nous vous rappelons également que nous avons indiqué le flux de données de production pour envoyer des données à la suite de rapports de production existante que vous utilisez.
Il s’agit simplement d’informations utiles puisque nous poussons maintenant la bibliothèque migrée le long du chemin de publication vers l’évaluation et la production.

## Intégration aux environnements d’évaluation et de production

Voici les étapes qui pousseront notre bibliothèque vers les environnements d’évaluation et de production :

1. Dans l’interface Balises, sélectionnez Flux de publication dans le volet de navigation de gauche
1. Votre bibliothèque de migration doit apparaître sous Développement (le nom correspond à ce que vous avez choisi au début de ce processus de migration)

   ![Bibliothèque de migration en développement](assets/migration-lib-in-dev.jpg)

1. Si vous êtes certain d’avoir déjà ajouté chaque modification à la bibliothèque, vous pouvez déplacer la bibliothèque vers l’avant sous les trois points et ignorer les étapes suivantes. Si vous n’êtes pas sûr, suivez les cinq étapes suivantes.
1. Cliquez sur le nom de la bibliothèque pour accéder aux détails de la bibliothèque
1. Vérifiez que vous vous trouvez dans la bonne bibliothèque via le nom .
1. Sélectionnez Ajouter toutes les ressources modifiées au bas de la page
1. Cliquez ensuite sur Enregistrer et créer dans le développement pour ajouter toutes les modifications en file d’attente à la bibliothèque

   ![Ajouter toutes les ressources modifiées](assets/add-all-changed-resources.jpg)

1. Vous revenez alors dans l’interface du flux de publication. Si la création se termine correctement, un point vert apparaît en regard de votre bibliothèque.
1. Vous pouvez ensuite déplacer votre bibliothèque vers l’avant dans le processus de publication, en fonction de vos besoins. Vous pouvez le définir pour les approbations, le déplacer directement vers l’évaluation pour le tester et l’approuver, ou même le déplacer pour approbation ou publication directement en production. Là encore, cela dépend des besoins de publication de votre entreprise.

   ![Processus de publication](assets/publishing-process.jpg)

Félicitations ! À ce stade, votre implémentation Analytics se trouve entièrement sur le Web SDK !

Je vais ajouter une remarque importante que nous avons eue au début de ce tutoriel :

>[!IMPORTANT]
>
>Il est important de noter que l’une des principales raisons pour lesquelles vous effectuez cette migration de votre implémentation est de vous préparer à utiliser les applications Adobe Experience Platform, telles que Customer Journey Analytics, Real-Time CDP ou Journey Optimizer (comme indiqué dans #3 ci-dessus). L’utilisation des données de votre site web à cette fin inclura des étapes supplémentaires qui ne sont pas incluses dans ce tutoriel, mais ce tutoriel sera certainement un prérequis pour cette progression ultérieure de votre implémentation. Par conséquent, suivez ce tutoriel, puis vous pourrez suivre les étapes nécessaires pour envoyer également ces mêmes données de site web à l’Experience Platform.

Bonne chance sur votre parcours avec les analyses et autres efforts de contenu et de marketing !
