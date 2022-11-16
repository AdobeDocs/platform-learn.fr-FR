---
title: 'offer decisioning : testez votre décision à l’aide du site web de démonstration.'
description: Test de votre décision à l’aide du site web de démonstration
kt: 5342
audience: Data Engineer, Data Architect, Orchestration Engineer, Marketer
doc-type: tutorial
activity: develop
exl-id: cdb2ba7d-bfc3-43ce-b9a1-1f0866322589
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '358'
ht-degree: 4%

---

# 9.4 Combinaison d’Adobe Target et d’Offer Decisioning

## 9.4.1 Collecte du lien partageable de votre projet de démonstration

Pour charger le projet de site web de démonstration dans Adobe Target, vous devez d’abord collecter un lien spécial qui permettra à Adobe Target de charger votre projet de site web de démonstration.

Pour ce faire, accédez à [https://builder.adobedemo.com/projects](https://builder.adobedemo.com/projects). Une fois connecté avec votre Adobe ID, vous verrez ceci. Cliquez sur le projet de votre site web pour l’ouvrir.

![RTCDP](./images/builder1.png)

Vous allez maintenant voir ceci. Cliquez sur **Partager**.

![RTCDP](./images/builder2.png)

Cliquez sur **Générer un lien** puis copiez le lien dans le presse-papiers.

![RTCDP](./images/builder3.png)

Accédez à [https://bitly.com](https://bitly.com), collez le lien que vous avez copié et cliquez sur **Raccourcir**. Vous obtenez maintenant un lien raccourci, qui ressemble à ceci : `https://bit.ly/3JxN7aG`. Vous aurez besoin de ce lien dans le prochain exercice.

![RTCDP](./images/builder4.png)

## 9.4.2 Collecte

Accédez maintenant à la page d’accueil de Adobe Experience Cloud en accédant à [https://experiencecloud.adobe.com/](https://experiencecloud.adobe.com/). Cliquez sur **Cible**.

![RTCDP](../module6/images/excl.png)

Sur le **Adobe Target** Page d’accueil, vous verrez toutes les activités existantes.

![RTCDP](../module6/images/exclatov.png)

Cliquez sur **+ Créer une activité** pour créer une activité.

![RTCDP](../module6/images/exclatcr.png)

Sélectionner **Ciblage d’expérience**.

![RTCDP](./images/exclatcrxt.png)

Maintenant, sélectionnez **Visuel** et collez le lien raccourci dans le champ **Entrée dans l’URL d’activité**. Cliquez sur **Suivant**.

![RTCDP](./images/exclatcrxt1.png)

Votre projet de site web de démonstration sera alors chargé dans le compositeur d’expérience visuelle.

![RTCDP](./images/vec1.png)

Accédez à **Parcourir** mode pour cliquer **Autoriser tout** dans la fenêtre contextuelle de consentement du cookie.

![RTCDP](./images/vec2.png)

Cliquez sur la zone contenant le texte. **Catégories proposées**. Cliquez sur **Insérer avant** puis sélectionnez **Offer Decision**.

![RTCDP](./images/vec3.png)

Vous verrez alors cette fenêtre contextuelle. Sélectionner votre environnement de test `--aepSandboxId--` puis sélectionnez l’emplacement. **Web - Image**.

![RTCDP](./images/vec4.png)

Ensuite, sélectionnez votre décision. `--demoProfileLdap-- - Luma Decision`. Cliquez sur **Enregistrer**.

![RTCDP](./images/vec5.png)

Vous verrez alors ceci. Veillez à ajouter une règle de modèle supplémentaire. **URL** **contains** **your-project-name**. Clics **Enregistrer**.

![RTCDP](./images/vec6.png)

Vous verrez alors ceci. Cliquez sur **Suivant**.

![RTCDP](./images/vec7.png)

Saisissez le nom de votre offre. Utilisez ce nom : `--demoProfileLdap-- - XT with Offers (VEC)`. Cliquez sur **Suivant**.

![RTCDP](./images/vec8.png)

Vous verrez alors ceci. Définissez vos **Mesure de l’objectif** comme indiqué. Cliquez sur **Enregistrer et fermer**.

![RTCDP](./images/vec9.png)

Votre offre est maintenant créée et en cours de publication.

![RTCDP](./images/vec10.png)

Une fois votre offre publiée, vous pouvez l’activer.

Étape suivante : [9.5 Utiliser votre décision dans un email et un SMS](./ex5.md)

[Revenir au module 9](./offer-decisioning.md)

[Revenir à tous les modules](./../../overview.md)
