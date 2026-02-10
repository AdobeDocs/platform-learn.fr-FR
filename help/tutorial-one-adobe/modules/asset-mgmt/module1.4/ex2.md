---
title: Utilisation de votre modèle Dynamic Media avec Adobe Journey Optimizer
description: Utilisation de votre modèle Dynamic Media avec Adobe Journey Optimizer
kt: 5342
doc-type: tutorial
exl-id: 0dd499cc-ec3b-42c3-9c08-6512ea5b9377
source-git-commit: 8f746831d4a1481f8ccc14539273c4b16ca5170b
workflow-type: tm+mt
source-wordcount: '637'
ht-degree: 9%

---

# 1.4.2 Utilisation de votre modèle Dynamic Media avec Adobe Journey Optimizer

## 1.4.2.1 Créer votre campagne dans Adobe Journey Optimizer

Connectez-vous à Adobe Journey Optimizer en allant sur [Adobe Experience Cloud](https://experience.adobe.com?lang=fr). Cliquez sur **Journey Optimizer**.

![ACOP &#x200B;](./images/acophome.png)

Vous serez redirigé vers la vue **Accueil** dans Journey Optimizer. Tout d’abord, assurez-vous d’utiliser le bon sandbox. Le sandbox à utiliser est appelé `--aepSandboxName--`. Vous serez alors dans la vue **Accueil** de votre `--aepSandboxName--` sandbox.

![ACOP &#x200B;](./images/acoptriglp.png)

Vous allez maintenant créer une campagne. Contrairement au parcours basé sur un événement de l’exercice précédent, qui repose sur les événements d’expérience entrants, les entrées ou les sorties d’audience pour déclencher un parcours pour un client spécifique, les campagnes ciblent une audience entière une fois avec du contenu unique tel que des newsletters, des promotions ponctuelles ou des informations génériques, ou périodiquement avec du contenu similaire envoyé régulièrement, par exemple des campagnes d’anniversaire et des rappels.

Dans le menu, accédez à **Campagnes** et cliquez sur **Créer une campagne**.

![Journey Optimizer](./images/gsemail21.png)

Sélectionnez **Planifié - Marketing** et cliquez sur **Créer**.

![Journey Optimizer](./images/gsemail22.png)

Dans l’écran de création de la campagne, configurez les éléments suivants :

- **Nom** : `--aepUserLdap-- - CitiSignal Fiber Max DM Email Campaign`.

Cliquez sur **Actions**.

![Journey Optimizer](./images/gsemail23.png)

Cliquez sur **+ Ajouter une action** puis sélectionnez **E-mail**.

![Journey Optimizer](./images/gsemail24.png)

Sélectionnez ensuite une **configuration d’e-mail** existante, puis cliquez sur **Modifier le contenu**.

![Journey Optimizer](./images/gsemail25.png)

Tu verras ça. Pour la **ligne d’objet**, utilisez la commande suivante :

```
{{profile.person.name.firstName}}, say hello to CitiSignal Fiber Max!
```

Cliquez ensuite sur **Modifier le contenu**.

![Journey Optimizer](./images/gsemail26.png)

Sélectionnez **Créer en partant de zéro**.

![Journey Optimizer](./images/gsemail27.png)

Vous devriez alors voir ceci.

![Journey Optimizer](./images/gsemail28.png)

Ajoutez 2x **1:1 colonne** à la zone de travail.

![Journey Optimizer](./images/gsemail29.png)

Accédez à **Fragments**, faites glisser le fragment **en-tête** vers la première colonne 1:1, puis faites glisser le fragment **pied de page** vers la deuxième colonne 1:1.

![Journey Optimizer](./images/gsemail30.png)

Ajoutez une nouvelle colonne 1:1 entre les 2 fragments, puis ajoutez une **Image** dans cette colonne 1:1. Cliquez ensuite sur **Parcourir**.

![Journey Optimizer](./images/gsemail31.png)

Accédez au dossier dans lequel vous avez stocké votre modèle Dynamic Media. Sélectionnez votre modèle Dynamic Media, puis cliquez sur **Sélectionner**.

![Journey Optimizer](./images/gsemail32.png)

Vous devriez alors voir ceci. Toi aussi. notez la section **PARAMETERS** qui permet de modifier les paramètres du modèle dynamic media.

![Journey Optimizer](./images/gsemail33.png)

## 1.4.2.2 Personnaliser le modèle Dynamic Media

Comme nous l’avons vu dans l’exercice précédent, AJO doit maintenant décider dynamiquement quelles valeurs doivent faire partie du modèle Dynamic Media.

Tout comme dans l’étape **Aperçu** de l’exercice précédent, les champs **city_paris**, **city_dubai** et **city_ny** doivent être définis sur 1, ce qui signifie que ces images seront masquées.

Pour le champ **titre**, cliquez sur l’icône de personnalisation.

![Journey Optimizer](./images/gsemail34.png)

Remplacez le texte par défaut par le texte suivant : `Hi {{profile.person.name.firstName}}`. Cliquez sur **Enregistrer**.

![Journey Optimizer](./images/gsemail35.png)

Pour le champ **corps**, cliquez sur l’icône de personnalisation.

![Journey Optimizer](./images/gsemail36.png)

Remplacez le texte par défaut par le texte suivant : `CitiSignal is coming to {{profile.homeAddress.city}}!`. Cliquez sur **Enregistrer**.

![Journey Optimizer](./images/gsemail37.png)

Assurez-vous que le champ **`dynamic_city_hide`** est défini sur 0. Cliquez sur l’icône de personnalisation de l’**`dynamic_city_image`** du champ.

![Journey Optimizer](./images/gsemail38.png)

Remplacez le texte par défaut par le texte suivant : `--aepUserLdap--CitiSignalDM/citisignal-fiber-max-is-coming_citisignal-{{profile._experienceplatform.individualCharacteristics.fiber_rollout.closest_rollout_city}}-1`. Cliquez sur **Enregistrer**.

![Journey Optimizer](./images/gsemail39.png)

Vous devriez alors voir ceci. L’image n’est plus rendue ici, ce qui est attendu car les variables dynamiques ne sont pas disponibles dans le contexte de l’éditeur d’e-mail.

Cliquez sur **Enregistrer**.

![Journey Optimizer](./images/gsemail40.png)

Essayez d’abord votre configuration, cliquez sur **Simuler du contenu** puis sélectionnez **Simuler du contenu**.

![Journey Optimizer](./images/gsemail41.png)

Vous devriez alors voir quelque chose comme ça. Si aucun profil de test n’est disponible, vous pouvez l’ajouter en accédant à **Gérer les profils de test**.

Une fois que vous disposez de profils de test contenant les données nécessaires pour tester ce cas d’utilisation, vous pouvez passer d’un profil à un autre pour voir les modifications se produire de manière dynamique.

Voici un profil lié à la ville de déploiement New York.

![Journey Optimizer](./images/gsemail42.png)

Voici un profil lié à la ville de déploiement Paris.

![Journey Optimizer](./images/gsemail43.png)

Voici un profil lié à la ville du déploiement Dubaï.

Cliquez sur **Fermer**.

![Journey Optimizer](./images/gsemail44.png)

Vous avez maintenant terminé cet exercice. Il n’est pas nécessaire de publier votre campagne par e-mail.

## Étapes suivantes

Revenir à [Adobe Experience Manager Assets et Dynamic Media](./aemassetsdm.md){target="_blank"}

[Revenir à tous les modules](./../../../overview.md){target="_blank"}