---
title: Bootcamp - CDP en temps réel - Créer un segment et agir - Envoyer votre segment à Adobe Target
description: Bootcamp - CDP en temps réel - Créer un segment et agir - Envoyer votre segment à Adobe Target
kt: 5342
audience: Data Architect, Orchestration Engineer, Marketer
doc-type: tutorial
activity: develop
exl-id: 6a76c2ab-96b7-4626-a6d3-afd555220b1e
source-git-commit: ead28f5631fc430c41e8c756b23dc69ffe19510e
workflow-type: tm+mt
source-wordcount: '878'
ht-degree: 2%

---

# 1.4 Agir : envoyer votre segment à Adobe Target ;

Accédez à [Adobe Experience Platform](https://experience.adobe.com/platform). Une fois connecté, vous accédez à la page d’accueil de Adobe Experience Platform.

![Ingestion des données](./images/home.png)

Avant de continuer, vous devez sélectionner une **sandbox**. L’environnement de test à sélectionner est nommé ``Bootcamp``. Pour ce faire, cliquez sur le texte **[!UICONTROL Production Prod]** dans la ligne bleue en haut de votre écran. Après avoir sélectionné le [!UICONTROL sandbox], vous verrez le changement d’écran et vous êtes maintenant dans votre [!UICONTROL sandbox].

![Ingestion des données](./images/sb1.png)

## 1.4.1 Activation de votre segment vers votre destination Adobe Target

Adobe Target est disponible en tant que destination à partir de Real-Time CDP. Pour configurer votre intégration Adobe Target, accédez à **Destinations**, à **Catalogue**.

Cliquez sur **Personnalisation** dans le **Catégories** . Vous verrez alors le **Adobe Target** carte de destination. Cliquez sur **Activation des segments**.

![AT](./images/atdest1.png)

Sélectionner la destination ``Bootcamp Target`` et cliquez sur **Suivant**.

![AT](./images/atdest3.png)

Dans la liste des segments disponibles, sélectionnez le segment que vous avez créé dans [1.3 Création d’un segment](./ex3.md), qui est nommé `yourLastName - Interest in Real-Time CDP`. Cliquez ensuite sur **Suivant**.

![AT](./images/atdest8.png)

Sur la page suivante, cliquez sur **Suivant**.

![AT](./images/atdest9.png)

Cliquez sur **Terminer**.

![AT](./images/atdest10.png)

Votre segment est maintenant activé vers Adobe Target.

![AT](./images/atdest11.png)

>[!IMPORTANT]
>
>Lorsque vous venez de créer votre destination Adobe Target dans Real-Time CDP, la mise en service de cette destination peut prendre jusqu’à une heure. Il s’agit d’un temps d’attente ponctuel, en raison de la configuration du serveur principal. Une fois la configuration initiale du temps d’attente d’une heure et du serveur principal terminée, les segments de périphérie nouvellement ajoutés envoyés à la destination Adobe Target seront disponibles pour le ciblage en temps réel.

## 1.4.2 Configuration de votre activité Adobe Target basée sur les formulaires

Maintenant que votre segment Real-Time CDP est configuré pour être envoyé à Adobe Target, vous pouvez configurer votre activité de ciblage d’expérience dans Adobe Target. Dans cet exercice, vous allez configurer une activité basée sur le compositeur d’expérience visuelle.

Accédez à la page d’accueil de Adobe Experience Cloud en accédant à [https://experiencecloud.adobe.com/](https://experiencecloud.adobe.com/). Cliquez sur **Cible** pour l’ouvrir.

![RTCDP](./images/excl.png)

Sur le **Adobe Target** Page d’accueil, vous verrez toutes les activités existantes.
Cliquez sur **+ Créer une activité** pour créer une activité.

![RTCDP](./images/exclatov.png)

Sélectionner **Ciblage d’expérience**.

![RTCDP](./images/exclatcrxt.png)

Sélectionner **Visuel** et définissez la variable **URL d’activité** to `https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises/particpantXX.html`, mais avant cela, remplacez XX par un nombre compris entre 01 et 30.

>[!IMPORTANT]
>
>Chaque participant à l’activation doit utiliser une page web distincte pour éviter les collisions de différentes expériences Adobe Target. Vous pouvez sélectionner une page web et trouver l’URL en vous rendant ici : [https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises.html](https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises.html).
>
>Les pages partagent toutes la même URL de base et se terminent par le nombre de participants.
>
>Par exemple, le participant 1 doit utiliser l’URL `https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises/particpant01.html`, participant 30 doit utiliser l’URL `https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises/particpant30.html`.

Sélectionner l’espace de travail **AT Bootcamp**.

Cliquez sur **Suivant**.

![RTCDP](./images/exclatcrxtdtlform.png)

Vous êtes maintenant dans le compositeur d’expérience visuelle. Il peut s’écouler entre 20 et 30 secondes avant que le site web ne soit complètement chargé.

![RTCDP](./images/atform1.png)

L’audience par défaut est actuellement **Tous les visiteurs**. Cliquez sur le bouton **3 points** en regard de **Tous les visiteurs** et cliquez sur **Modification de l’audience**.

![RTCDP](./images/atform3.png)

La liste des audiences disponibles s’affiche désormais. Le segment Adobe Experience Platform que vous avez créé précédemment et que vous avez envoyé à Adobe Target fait désormais partie de cette liste. Sélectionnez le segment que vous avez précédemment créé dans Adobe Experience Platform. Cliquez sur **Attribution d’une audience**.

![RTCDP](./images/exclatvecchaud.png)

Votre segment Adobe Experience Platform fait désormais partie de cette activité de ciblage d’expérience.

![RTCDP](./images/atform4.png)

Avant de pouvoir modifier l’image principale, vous devez cliquer sur **Tout autoriser** sur la bannière de cookie.

Pour ce faire, accédez à **Parcourir**

![RTCDP](./images/cook1.png)

Cliquez ensuite sur **Tout autoriser**.

![RTCDP](./images/cook2.png)

Ensuite, revenez à **Composer**.

![RTCDP](./images/cook3.png)

Changeons maintenant l&#39;image de héros sur la page d&#39;accueil du site web. Cliquez sur l’image principale par défaut du site web, puis sur **Remplacer le contenu** puis sélectionnez **Image**.

![RTCDP](./images/atform5.png)

Recherche du fichier image **rtcdp.png**. Sélectionnez-le, puis cliquez sur **Enregistrer**.

![RTCDP](./images/atform6.png)

Vous verrez ensuite la nouvelle expérience avec la nouvelle image, pour le public sélectionné.

![RTCDP](./images/atform7.png)

Cliquez sur le titre de votre activité dans le coin supérieur gauche pour la renommer.

![RTCDP](./images/exclatvecname.png)

Pour le nom, veuillez utiliser :

- `yourLastName - RTCDP - XT (VEC)`

Cliquez sur **Suivant**.

![RTCDP](./images/atform8.png)

Cliquez sur **Suivant**.

![RTCDP](./images/atform8a.png)

Sur le **Objectifs et paramètres** - page, accédez à **Mesures d’objectif**.

![RTCDP](./images/atform9.png)

Définissez l’objectif Principal sur **Engagement** - **Temps passé sur le site**. Cliquez sur **Enregistrer et fermer**.

![RTCDP](./images/vec3.png)

Vous êtes maintenant sur le **Présentation de l’activité** page. Vous devez toujours activer votre activité.

![RTCDP](./images/atform10.png)

Cliquez sur le champ **Inactif** et sélectionnez **Activer**.

![RTCDP](./images/atform11.png)

Vous obtiendrez alors une confirmation visuelle que votre activité est maintenant active.

![RTCDP](./images/atform12.png)

Votre activité est maintenant en ligne et peut être testée sur le site web de bootcamp.

Si vous revenez maintenant à votre site web de démonstration et rendez-vous sur la page produit pour **Real-Time CDP**, vous êtes alors immédiatement admissible pour le segment que vous avez créé et l’activité Adobe Target s’affiche en temps réel sur la page d’accueil.

>[!IMPORTANT]
>
>Chaque participant à l’activation doit utiliser une page web distincte pour éviter les collisions de différentes expériences Adobe Target. Vous pouvez sélectionner une page web et trouver l’URL en vous rendant ici : [https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises.html](https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises.html).
>
>Les pages partagent toutes la même URL de base et se terminent par le nombre de participants.
>
>Par exemple, le participant 1 doit utiliser l’URL `https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises/particpant01.html`, participant 30 doit utiliser l’URL `https://bootcamp.aepdemo.net/content/aep-bootcamp-experience/language-masters/en/exercises/particpant30.html`.

![RTCDP](./images/atform12a.png)

Étape suivante : [1.5 Agir : envoyer votre segment à Facebook ;](./ex5.md)

[Retour au flux utilisateur 1](./uc1.md)

[Revenir à tous les modules](../../overview.md)
