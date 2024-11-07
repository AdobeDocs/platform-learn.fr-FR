---
title: 'Offer decisioning : testez votre décision à l’aide du site web de démonstration.'
description: Test de votre décision à l’aide du site web de démonstration
kt: 5342
doc-type: tutorial
source-git-commit: 2cdc145d7f3933ec593db4e6f67b60961a674405
workflow-type: tm+mt
source-wordcount: '357'
ht-degree: 3%

---

# 3.3.4 Combinaison d’Adobe Target et d’Offer Decisioning

## 3.3.4.1 Collecte du lien partageable de votre projet de démonstration

Pour charger le projet de site web de démonstration dans Adobe Target, vous devez d’abord collecter un lien spécial qui permettra à Adobe Target de charger votre projet de site web de démonstration.

Pour ce faire, accédez à [https://builder.adobedemo.com/projects](https://builder.adobedemo.com/projects). Une fois connecté avec votre Adobe ID, vous verrez ceci. Cliquez sur le projet de votre site web pour l’ouvrir.

![RTCDP](./images/builder1.png)

Vous allez maintenant voir ceci. Cliquez sur **Partager**.

![RTCDP](./images/builder2.png)

Cliquez sur **Générer le lien**, puis copiez le lien dans le presse-papiers.

![RTCDP](./images/builder3.png)

Accédez à [https://bitly.com](https://bitly.com), collez le lien que vous avez copié et cliquez sur **Raccourcir**. Vous obtiendrez désormais un lien raccourci, qui ressemble à ceci : `https://bit.ly/3JxN7aG`. Vous aurez besoin de ce lien dans le prochain exercice.

![RTCDP](./images/builder4.png)

## 3.3.4.2 Collecte

Accédez maintenant à la page d’accueil de Adobe Experience Cloud en vous rendant à l’adresse [https://experiencecloud.adobe.com/](https://experiencecloud.adobe.com/). Cliquez sur **Target**.

![RTCDP](./../../../modules/rtcdp-b2c/module2.3/images/excl.png)

Sur la page d’accueil **Adobe Target**, vous verrez toutes les activités existantes.

![RTCDP](./../../../modules/rtcdp-b2c/module2.3/images/exclatov.png)

Cliquez sur **+ Créer une activité** pour créer une activité.

![RTCDP](./../../../modules/rtcdp-b2c/module2.3/images/exclatcr.png)

Sélectionnez **Ciblage d’expérience**.

![RTCDP](./images/exclatcrxt.png)

Sélectionnez maintenant **Visuel** et collez votre lien raccourci dans le champ **Entrer dans l’URL d’activité**. Cliquez sur **Suivant**.

![RTCDP](./images/exclatcrxt1.png)

Votre projet de site web de démonstration sera alors chargé dans le compositeur d’expérience visuelle.

![RTCDP](./images/vec1.png)

Accédez au mode **Parcourir** pour cliquer sur **Autoriser tout** dans la fenêtre contextuelle de consentement des cookies.

![RTCDP](./images/vec2.png)

Cliquez sur la zone contenant le texte **Catégories en vedette**. Cliquez sur **Insérer avant**, puis sélectionnez **Offer Decision**.

![RTCDP](./images/vec3.png)

Vous verrez alors cette fenêtre contextuelle. Sélectionnez votre environnement de test `--aepSandboxId--`, puis sélectionnez l’emplacement **Web - Image**.

![RTCDP](./images/vec4.png)

Sélectionnez ensuite votre décision `--demoProfileLdap-- - Luma Decision`. Cliquez sur **Enregistrer**.

![RTCDP](./images/vec5.png)

Vous verrez alors ceci. Veillez à ajouter une règle de modèle supplémentaire **URL** **contient** **votre-nom-projet**. Cliquez sur **Enregistrer**.

![RTCDP](./images/vec6.png)

Vous verrez alors ceci. Cliquez sur **Suivant**.

![RTCDP](./images/vec7.png)

Saisissez un nom pour votre offre. Utilisez ce nom : `--demoProfileLdap-- - XT with Offers (VEC)`. Cliquez sur **Suivant**.

![RTCDP](./images/vec8.png)

Vous verrez alors ceci. Définissez la **mesure de l’objectif** comme indiqué. Cliquez sur **Enregistrer et fermer**.

![RTCDP](./images/vec9.png)

Votre offre est maintenant créée et en cours de publication.

![RTCDP](./images/vec10.png)

Une fois votre offre publiée, vous pouvez l’activer.

Étape suivante : [3.3.5 Utilisez votre décision dans un email et un sms](./ex5.md)

[Revenir au module 3.3](./offer-decisioning.md)

[Revenir à tous les modules](./../../../overview.md)
