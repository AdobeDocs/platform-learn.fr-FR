---
title: Foundation - Configuration de la collecte de données Adobe Experience Platform et de l’extension du SDK Web - Présentation de la collecte de données Adobe Experience Platform
description: Foundation - Configuration de la collecte de données Adobe Experience Platform et de l’extension du SDK Web - Présentation de la collecte de données Adobe Experience Platform
kt: 5342
doc-type: tutorial
exl-id: 391c79d6-9c42-465e-bce8-60fa6474979c
source-git-commit: 3a19e88e820c63294eff38bb8f699a9f690afcb9
workflow-type: tm+mt
source-wordcount: '1269'
ht-degree: 10%

---

# 1.1.3 Présentation de la collecte de données Adobe Experience Platform

## Contexte

Examinons maintenant de plus près les blocs de création de la collecte de données Adobe Experience Platform pour comprendre ce qui est installé sur votre site web de démonstration. Un examen plus approfondi de l’extension SDK Web de Adobe Experience Platform vous permettra de configurer un élément de données et une règle et d’apprendre à publier une bibliothèque.

## Extension du SDK Web dʼAdobe Experience Platform

Une extension est un ensemble de codes qui étend l’interface de collecte de données Adobe Experience Platform et la fonctionnalité de bibliothèque. La collecte de données Adobe Experience Platform est la plateforme et les extensions sont des applications qui s’exécutent sur la plateforme. Toutes les extensions utilisées dans le tutoriel sont créées et gérées par Adobe, mais les tiers peuvent créer leurs propres extensions pour limiter la quantité de code personnalisé que les utilisateurs de la collecte de données Adobe Experience Platform doivent gérer.

Accédez à [Adobe Experience Platform Data Collection](https://experience.adobe.com/launch/) et sélectionnez **Balises**.

Il s’agit de la page Propriétés de la collecte de données Adobe Experience Platform que vous avez déjà vue.

![Page Propriétés](./images/launch1.png)

Dans **Prise en main**, Demo System a créé deux propriétés clientes pour vous : une pour le site web et une pour l’application mobile. Recherchez-les en recherchant `--aepUserLdap--` dans la zone **[!UICONTROL Rechercher]**.
Cliquez pour ouvrir la propriété **Web**.

![Zone de recherche](./images/property6.png)



La page Présentation de la propriété s’affiche alors. Cliquez sur **[!UICONTROL Extensions]** dans le rail de gauche, puis sur **SDK Web Adobe Experience Platform** et cliquez sur **[!UICONTROL Configurer]**.

![Page d’aperçu de la propriété](./images/property7.png)

Bienvenue dans le SDK Web de Adobe Experience Platform ! Ici, vous pouvez configurer l’extension avec le Datastream que vous avez créé dans [Prise en main](./../../../modules/gettingstarted/gettingstarted/ex2.md) ainsi qu’avec une configuration plus avancée.

Le domaine Edge par défaut est toujours **edge.adobedc.net**. Si vous avez mis en oeuvre une configuration CNAME dans votre environnement Adobe Experience Cloud ou Adobe Experience Platform, vous devrez mettre à jour le **[!UICONTROL domaine Edge]**.

Si le domaine Edge de votre instance est différent de celui par défaut, mettez à jour le domaine Edge ici. Si vous n’êtes pas sûr, utilisez le domaine par défaut. Un domaine Edge permet de configurer un serveur de suivi propriétaire, qui utilise ensuite une configuration CNAME dans le serveur principal pour s’assurer que les données sont collectées dans Adobe.

![Extensions home](./images/property9edgedomain.png)

Sous **[!UICONTROL Datastreams]**, vous avez déjà sélectionné votre flux de données dans la section **Prise en main** . Vous avez sélectionné ce flux de données : `--aepUserLdap-- - Demo System Datastream`, dans la liste de la zone **[!UICONTROL Datastream]**, pour chacun des environnements.

Cliquez sur **[!UICONTROL Enregistrer]** pour revenir à la vue Extensions.

![Extensions home](./images/property9edge.png)

## Éléments de données

Les éléments de données sont les blocs de construction de votre dictionnaire de données (ou mappage de données). Utilisez des éléments de données pour recueillir, organiser et diffuser des données dans les technologies marketing et publicitaires.

Un seul élément de données est une variable dont la valeur peut être mappée à des chaînes de requête, des URL, des valeurs de cookie, des variables JavaScript, etc. Vous pouvez référencer cette valeur par son nom de variable dans toute la collecte de données Adobe Experience Platform. Cette collection d’éléments de données devient le dictionnaire des données définies que vous pouvez utiliser pour créer vos règles (événements, conditions et actions). Ce dictionnaire de données est partagé dans toute la collecte de données Adobe Experience Platform afin d’être utilisé avec toute extension ajoutée à votre propriété.

Vous allez maintenant modifier un élément de données existant dans un format compatible avec le SDK Web.

Cliquez sur Éléments de données dans le rail de gauche pour accéder à la page Éléments de données .

![Page d’accueil des éléments de données](./images/dataelement1.png)

>[!NOTE]
>
>Vous ne modifiez qu’un élément de données dans cet exercice, mais vous pouvez voir le bouton **[!UICONTROL Ajouter un élément de données]** sur cette page, qui serait utilisé pour ajouter une nouvelle variable au dictionnaire de données. Il peut ensuite être utilisé dans toute la collecte de données Adobe Experience Platform. N’hésitez pas à consulter certains autres éléments de données existants, principalement l’utilisation du stockage local comme source de données.

Dans la barre de recherche, saisissez **XDM - Product View** et cliquez sur l’élément de données qu’il renvoie.

![Rechercher ruleArticlePages](./images/dataelement2.png)

Cet écran affiche l’objet XDM que vous allez modifier. Le modèle de données d’expérience (XDM) est un concept qui sera exploré beaucoup plus loin dans ce tutoriel technique, mais pour l’instant, il suffit de le comprendre comme le format requis par le SDK Web de Adobe Experience Platform. Vous ajouterez un peu plus d’informations aux données collectées sur les pages Article du site web de démonstration.

Cliquez sur le bouton plus en regard de **web** au bas de l’arborescence.

Cliquez sur le bouton plus en regard de **webPageDetails**.

Cliquez sur **siteSection**. Vous voyez maintenant que **siteSection** n’est encore lié à aucun élément de données. Changeons cela.

![Accédez à la section du site](./images/dataelement3.png)

Faites défiler vers le haut et saisissez le texte `%Product Category%`. Cliquez sur **[!UICONTROL Enregistrer]**.

![Enregistrer](./images/dataelement4.png)

À ce stade, l’extension SDK Web Adobe Experience Platform est installée et vous avez mis à jour un élément de données pour collecter des données par rapport à une structure XDM. Ensuite, vérifions les règles qui enverront les données au bon moment.

## Règles

La collecte de données Adobe Experience Platform est un système basé sur des règles. Il recherche les interactions utilisateur et les données associées. Lorsque les critères définis dans votre règle sont satisfaits, la règle déclenche l’extension, le script ou le code côté client que vous avez identifié.

Créez des règles pour intégrer les données et les fonctionnalités du marketing, ainsi qu’une technologie d’annonces qui rassemble les produits disparates en une seule solution.

Ventilons la règle qui envoie des données sur les pages de l’article.

Cliquez sur **[!UICONTROL Rules]** dans le rail de gauche.

**[!UICONTROL Recherchez]** pour `Product View`.

Cliquez sur la règle renvoyée.

![ Média - Recherche de règles sur les pages d’article ](./images/rule1.png)

Regardons les éléments individuels qui constituent cette règle.

Pour toutes les règles : si un **[!UICONTROL événement]** spécifié se produit, les **[!UICONTROL conditions]** sont évaluées, puis les **[!UICONTROL actions]** spécifiées ont lieu si nécessaire.

![Media - Règle Pages d’article](./images/rule2.png)

Cliquez sur l’événement **Core - Custom Event**. Il s’agit de la vue qui charge.

Cliquez sur la liste déroulante **Type d’événement** .

Cette section répertorie certaines des interactions standard que vous pouvez utiliser pour signaler à la collecte de données Adobe Experience Platform d’exécuter les actions, si les conditions sont vraies.

![Événements](./images/rule3.png)

Cliquez sur **[!UICONTROL Annuler]** pour revenir à la règle.

Cliquez sur l’action **Envoyer l’événement d’expérience &quot;Consultation produit&quot;**.

![Action Envoyer un événement](./images/rule5a.png)

Vous pouvez y voir les données envoyées à la périphérie par le SDK Web de Adobe Experience Platform. Plus précisément, il utilise l’ **alloy** **[!UICONTROL Instance]** du SDK Web. L’événement **[!UICONTROL Type]** est défini sur **Consultations du produit Commerce (panier)** et les données XDM que vous envoyez sont l’élément de données **XDM - Consultation du produit** que vous avez modifié précédemment.

![Action Envoyer un événement](./images/rule5.png)

Maintenant que vous avez examiné la règle, vous pouvez publier toutes vos modifications dans la collecte de données Adobe Experience Platform.

## Publish dans une bibliothèque

Enfin, pour valider la règle et l’élément de données que vous venez de mettre à jour, vous devez publier une bibliothèque contenant les éléments modifiés dans notre propriété. Vous devez suivre quelques étapes rapides dans la section **[!UICONTROL Publication]** de la collecte de données Adobe Experience Platform.

Cliquez sur **[!UICONTROL Flux de publication]** dans le volet de navigation de gauche.

Cliquez sur la bibliothèque existante, appelée **Main**.

![Accès à la bibliothèque](./images/publish1.png)

Cliquez sur le bouton **Ajouter toutes les ressources modifiées** . Ensuite,
Cliquez sur le bouton **Enregistrer et créer pour le développement** .

![Accès à la bibliothèque](./images/publish1a.png)

La création de la bibliothèque peut prendre quelques minutes. Une fois l’opération terminée, un point vert s’affiche à gauche du nom de la bibliothèque.

![Bibliothèque de contenu](./images/publish2.png)

Comme vous pouvez le constater sur l’écran Flux de publication , le processus de publication dans la collecte de données Adobe Experience Platform ne répond pas aux exigences de ce tutoriel. Nous allons juste utiliser une seule bibliothèque dans notre environnement de développement.

Étape suivante : [1.1.4 Collecte de données Web côté client](./ex4.md)

[Revenir au module 1.1](./data-ingestion-launch-web-sdk.md)

[Revenir à tous les modules](./../../../overview.md)
