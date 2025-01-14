---
title: Créer les modifications d’implémentation dans la bibliothèque de développement
description: Découvrez comment apporter des modifications à la bibliothèque de développement dans votre propriété de balises afin de pouvoir tester les résultats sur votre site web de développement.
solution: Data Collection, Analytics
feature: Web SDK
jira: KT-16762
source-git-commit: 7ae56d997884cf1558e72c0ad553df1c5d43c081
workflow-type: tm+mt
source-wordcount: '482'
ht-degree: 0%

---


# Créer les modifications d’implémentation dans la bibliothèque de développement

Découvrez comment apporter des modifications à la bibliothèque de développement dans votre propriété de balises afin de pouvoir tester les résultats sur votre site web de développement.

Au fur et à mesure que vous avancerez dans ce tutoriel, ou vraiment à chaque fois que vous apporterez des modifications à votre implémentation, vous devrez créer/publier ces modifications afin de les voir sur vos sites de développement, d’évaluation ou de production. Je suis sûr que vous l&#39;avez déjà fait, puisqu&#39;il s&#39;agit d&#39;un document de migration et non d&#39;un document de mise en œuvre pour la première fois. En réalité, vous souhaiterez le faire assez souvent, car vous exécutez chaque fonction et souhaitez la tester et vous assurer qu’elle fonctionne correctement, en envoyant les données appropriées à Analytics.

Par conséquent, il y aura quelques rappels dans ce tutoriel pour créer ou publier vos modifications. Si nécessaire, placez un signet sur cette page et n’hésitez pas à l’intégrer à votre bibliothèque de développement. Vous pouvez le faire à tout moment.

Alors, construisons ce que nous avons fait jusqu&#39;à présent. D’ailleurs, nous pouvons parfois échanger « créer » et « publier » dans ce tutoriel. Le plus important est de savoir si vous « créez » une bibliothèque de développement ou d’évaluation, ou si vous « publiez » des ressources dans la bibliothèque et l’environnement de production, quel que soit le mot que nous utilisons.

## Création des modifications de migration apportées au développement dans les balises Experience Platform

1. Dans votre propriété dans les balises Experience Platform, sélectionnez **Flux de publication** dans le volet de navigation de gauche, puis ajoutez une nouvelle bibliothèque.

   ![Flux de publication](assets/publishing-flow-new-library.jpg)

1. Nommez la bibliothèque comme vous le souhaitez, par exemple **Migration initiale de Web SDK**.
1. Sélectionnez l’environnement **Développement**.
1. Sélectionnez **Ajouter toutes les ressources modifiées** pour ajouter tous les éléments sur lesquels vous avez travaillé.

   ![Nouvelle bibliothèque ](assets/new-library-websdk-migration.jpg)

1. Enregistrer et créer dans le développement

   ![Enregistrer et créer en développement](assets/save-and-build-to-dev.jpg)

1. Une fois la génération terminée, vous pourrez voir si elle a réussi. Placez le pointeur de la souris sur le point vert à gauche de la nouvelle bibliothèque de votre flux de publication. En fait, si le point vert est présent, il se termine correctement et vous le dira.

   ![ Publication réussie ](assets/successful-publish.jpg)

### Sélectionner une bibliothèque de travail

Voici un bon raccourci pour parcourir les modifications apportées aux balises. Au lieu de parcourir l’ensemble du flux de publication chaque fois que vous apportez une modification, vous pouvez choisir une bibliothèque de travail, et enregistrer et créer en un clic sur un bouton. Fais-le. Tu me remercieras plus tard.

1. À peu près n’importe où dans l’interface utilisateur des balises, cliquez sur Sélectionner une bibliothèque de travail en haut à droite de l’interface utilisateur, puis choisissez celle de votre choix. Pour ce tutoriel, choisissez Migration initiale de Web SDK .

   ![Sélectionner la bibliothèque de travail](assets/select-working-library.jpg)

