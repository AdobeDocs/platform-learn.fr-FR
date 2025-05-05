---
title: Migration d’Adobe Analytics vers Web SDK à l’aide de balises
description: Découvrez les étapes à suivre lors de la migration vers Web SDK, ainsi que les décisions qui devront être prises en cours de route.
solution: Data Collection, Analytics
feature: Web SDK
jira: KT-16755
exl-id: e578b669-42b4-46ae-b6e6-6688e5c5c772
source-git-commit: d6471c8e383e22fed4ad5870952d0d0470f593db
workflow-type: tm+mt
source-wordcount: '1157'
ht-degree: 0%

---

# Migration d’Adobe Analytics vers Web SDK à l’aide de balises

Découvrez les étapes de migration d’une implémentation d’Adobe Analytics à l’aide de l’extension Analytics dans Balises Experience Platform (anciennement Launch) vers Web SDK, à l’aide de l’extension Web SDK également dans Balises. Lorsque l’extension Adobe Analytics est utilisée dans les balises, le code « AppMeasurement.js » est utilisé en arrière-plan. Par conséquent, vous pouvez considérer ce tutoriel comme une migration d’AppMeasurement vers Web SDK, mais il se trouve entièrement dans Balises et ne couvre PAS le déplacement vers ou depuis une implémentation de JavaScript (à l’exception du code JavaScript utilisé dans l’interface utilisateur des balises). Pour la migration des implémentations de JavaScript, consultez la [documentation](https://experienceleague.adobe.com/fr/docs/analytics/implementation/aep-edge/web-sdk/appmeasurement-to-web-sdk).

>[!NOTE]
>
>Des tutoriels de migration similaires sont disponibles pour :
>
> * [Adobe Target](../tutorial-migrate-target-websdk/introduction.md)
> * [Adobe Audience Manager](https://experienceleague.adobe.com/fr/docs/audience-manager/user-guide/migrate-to-web-sdk/appmeasurement-to-web-sdk)

>[!CAUTION]
>
> Étant donné que Platform Web SDK prend en charge plusieurs applications d’Adobe, toutes les bibliothèques d’Adobe d’une page donnée doivent être migrées en même temps. Par exemple, une implémentation mixte de Web SDK for Target et d’AppMeasurement for Analytics sur une seule page _n’est pas prise en charge_. Cependant, une implémentation mixte sur différentes pages est prise en charge ; par exemple, Web SDK sur la page A et at.js avec l’AppMeasurement sur la page B.

## Résultats de ce tutoriel

Avant de passer aux étapes de migration de votre implémentation Analytics, il est important de comprendre exactement ce que vous allez faire, à savoir modifier/mettre à jour l’_implémentation_ pour Analytics. À la fin de ce tutoriel, lorsque vous allez dans vos rapports et que tout est identique, vous pouvez vous demander : « Maintenant, pourquoi ai-je fait tout cela ? » Il existe d’autres documents pour décrire les avantages de l’utilisation de Web SDK pour votre implémentation d’Analytics, à quelques exceptions près :

1. Prise en charge de l’identifiant d’appareil interne
1. Meilleures performances
1. Relecture de votre implémentation à mesure que vous passez à l’utilisation des applications Adobe Experience Platform (activation de nouveaux cas d’utilisation)

Contactez votre représentant ou représentante Adobe Analytics pour en savoir plus sur la manière dont Web SDK peut vous aider. À mesure que nous avançons dans ce tutoriel, nous nous concentrerons sur _comment_ effectuer la migration.

>[!IMPORTANT]
>
>Il est important de noter que l’une des principales raisons pour lesquelles vous effectuez cette migration de votre implémentation est de vous préparer à utiliser les applications Adobe Experience Platform, telles que Customer Journey Analytics, Real-Time CDP ou Journey Optimizer (comme indiqué dans #3 ci-dessus). L’utilisation des données de votre site web à cette fin inclura des étapes supplémentaires qui ne sont pas incluses dans ce tutoriel, mais ce tutoriel sera certainement un prérequis pour cette progression ultérieure de votre implémentation. Par conséquent, suivez ce tutoriel, puis vous pourrez suivre les étapes nécessaires pour envoyer également ces mêmes données de site web à l’Experience Platform.

## Méthode de migration

Il existe probablement de nombreuses façons d’effectuer ce processus de migration, mais nous devons en aborder deux ici :

**Méthode 1 :** mettez à jour votre propriété Tags existante vers Web SDK, en créant de nouveaux éléments de données et en modifiant les règles qui existent déjà dans votre propriété.

**Méthode 2 :** vous pouvez également créer une nouvelle propriété (en copiant la propriété existante ou en en créant une toute nouvelle), puis configurer cette nouvelle propriété avec Web SDK au lieu de l’extension Adobe Analytics.

**Pour ce tutoriel sur la migration, nous allons utiliser la méthode 1.** Ainsi, les codes incorporés associés à la propriété sont déjà incorporés dans vos sites de développement, d’évaluation et de production, de sorte qu’il n’est pas nécessaire de modifier les codes incorporés. Si vous décidez d’utiliser la méthode 2, n’oubliez pas d’obtenir les nouveaux codes incorporés pour chaque environnement à partir de la section **Environnements** de la nouvelle propriété et de les placer dans la section HEAD de votre site.

>[!NOTE]
>
>Même si nous allons simplement modifier notre propriété existante dans les balises pendant cette migration, il est toujours préférable d’être prudent. Par conséquent, il est vivement recommandé de faire une copie de votre propriété actuelle avant de démarrer la migration. De cette façon, vous pourriez toujours aller dans la copie et regarder comment les choses étaient avant de les modifier, en extraire le code, etc.
>C&#39;est juste bon d&#39;être prudent, juste au cas où. Allez-y et faites la copie de votre propriété. Je vais attendre ici jusqu&#39;à ce que vous reveniez.

## Étapes de migration de votre implémentation Analytics vers Web SDK

Au fur et à mesure que vous passez en revue les étapes, quelques mises en garde sont importantes à comprendre :

1. Tout d’abord, il se peut que vous ayez besoin de toutes ces étapes. Par exemple, il existe une leçon concernant la migration du code personnalisé. Si vous disposez d’une implémentation de balises qui n’utilise pas de code personnalisé (y compris l’utilisation de plug-ins), vous n’aurez pas besoin de cette leçon. Nous avons essayé d’inclure les leçons dont tout le monde aurait besoin, alors lisez au moins les leçons pour voir si vous devez apporter des ajustements à votre site au cours de votre migration.
1. En outre, il n’est tout simplement pas possible de créer un tutoriel de migration qui couvrira 100 % des cas d’utilisation que tout le monde utilise. Comme indiqué au point précédent, nous avons essayé d’inclure les leçons dont la plupart des personnes auront besoin, et qui couvriront la plupart des principaux cas d’utilisation. Cependant, il y aura sans aucun doute des cas d’utilisation qui ne sont pas abordés dans ce tutoriel. Dans ce cas, vérifiez si les leçons incluses vous donnent une bonne idée de la manière dont vous devez migrer pour votre cas d’utilisation. Vous pouvez également demander la collecte de données à vos pairs de la communauté des Experience League [&#128279;](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/ct-p/adobe-launch-community?profile.language=fr).

Le processus de migration implique les étapes clés suivantes :

1. Créez une suite de rapports de validation de migration.
1. Créez et configurez un flux de données.
1. Ajouter et configurer l’extension Web SDK dans les balises (anciennement Adobe Launch)
1. Créez un nouvel élément de données pour envoyer des données via le Web SDK.
1. Migrez votre règle de chargement de page par défaut pour utiliser l’élément de données et les actions Web SDK.
1. Migrez le code personnalisé dans les règles ou pour les plug-ins.
1. Publish vos modifications d’implémentation.
1. Découvrez comment déboguer et valider vos modifications, ainsi que valider votre règle de chargement de page par défaut et les variables qui lui sont associées. Cette validation doit ensuite se poursuivre tout au long de la migration au fur et à mesure que vous apportez des modifications.
1. Migrez des règles de chargement de page supplémentaires.
1. Migrer les règles de lien personnalisées.
1. Après la validation complète, supprimez les références à l’extension Analytics et supprimez l’extension elle-même.
1. Après avoir apporté toutes les modifications, poussez la bibliothèque vers l’évaluation, puis vers la production.
1. Une fois tout terminé, effectuez un nouveau test. Cette action est nécessaire car vous avez apporté des modifications en supprimant les références à l’ancien code Analytics et vous souhaitez vous assurer que tout fonctionne toujours correctement.

>[!NOTE]
>
>Nous nous engageons à vous aider à réussir la migration d’Analytics vers Web SDK. Si vous rencontrez des obstacles avec votre migration ou si vous pensez qu&#39;il manque des informations essentielles dans ce guide, veuillez nous le faire savoir en postant dans [cette discussion communautaire](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/tutorial-discussion-migrate-adobe-analytics-to-web-sdk-using/m-p/732308?profile.language=fr#M604){target="_blank"}.

