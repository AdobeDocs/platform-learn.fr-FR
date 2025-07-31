---
title: GenStudio for Performance Marketing - Créer une expérience d’e-mail pour AJO
description: GenStudio for Performance Marketing - Créer une expérience d’e-mail pour AJO
role: Developer
level: Beginner
jira: KT-5342
doc-type: Tutorial
exl-id: 9837c076-e6ca-47a0-96b9-5fa5fdba3fd2
source-git-commit: 10f1f6a1f77c41e3c912b3d03b73da7b6c68670c
workflow-type: tm+mt
source-wordcount: '856'
ht-degree: 6%

---

# 1.3.4 Création d’une expérience d’e-mail pour AJO

>[!IMPORTANT]
>
>Pour effectuer cet exercice, vous devez avoir accès à un environnement Adobe Journey Optimizer configuré pour l’intégration à GenStudio for Performance Marketing, qui est actuellement en version bêta.

>[!IMPORTANT]
>
>Pour exécuter toutes les étapes de cet exercice, vous devez avoir accès à un environnement Adobe Workfront existant et, dans cet environnement, vous devez avoir créé un projet et un workflow d’approbation. Si vous suivez l’exercice [Gestion des workflows avec Adobe Workfront](./../../../modules/workflow-planning/module1.2/workfront.md){target="_blank"} la configuration requise sera disponible.

## 1.3.4.1 Créer et approuver une expérience d’e-mail

Dans le menu de gauche, accédez à **Créer**. Sélectionnez **E-mail**.

![GSPeM](./images/gsemail1.png)

Sélectionnez le modèle **E-mail** que vous avez importé précédemment et qui est nommé `--aepUserLdap---citisignal-email-template`. Cliquez sur **Utiliser**.

![GSPeM](./images/gsemail2.png)

Vous devriez alors voir ceci. Remplacez le nom de votre publicité par `--aepUserLdap-- - Email Online Gamers Fiber Max`.

![GSPeM](./images/gsemail3.png)

Sous **Paramètres**, sélectionnez les options suivantes :

- **Marque** : `--aepUserLdap-- - CitiSignal`
- **Langue** : `English (US)`
- **Persona** : `--aepUserLdap-- - Online Gamers`
- **Produit** : `--aepUserLdap-- - CitiSignal Fiber Max`

Cliquez sur **Sélectionner à partir du contenu**.

![GSPeM](./images/gsemail4.png)

Sélectionnez l’`--aepUserLdap-- - neon rabbit.png` de la ressource. Cliquez sur **Utiliser**.

![GSPeM](./images/gsemail5.png)

Saisissez le `convince online gamers to start playing online multiplayer games using CitiSignal internet` d’invite et cliquez sur **Générer**.

![GSPeM](./images/gsemail6.png)

Vous devriez alors voir un élément similaire, avec 4 variations d’e-mail générées. La vue par défaut affiche la vue **mobile**. Vous pouvez basculer vers la vue Bureau en cliquant sur l’icône **ordinateur**.

![GSPeM](./images/gsemail7.png)

Un score de conformité est automatiquement calculé pour chaque e-mail. Cliquez sur le score pour afficher plus de détails.

![GSPeM](./images/gsemail8.png)

Cliquez sur **Afficher et résoudre les problèmes**.

![GSPeM](./images/gsemail9.png)

Vous pouvez ensuite afficher plus de détails sur les mesures à prendre pour optimiser le score de complicance.

![GSPeM](./images/gsemail10.png)

Cliquez ensuite sur **Demander l’approbation** pour vous connecter à Adobe Workfront.

![GSPeM](./images/gsemail11.png)

Sélectionnez votre projet Adobe Workfront, qui doit être nommé `--aepUserLdap-- - CitiSignal Fiber Launch`. Saisissez votre propre adresse e-mail sous **Inviter des personnes** et assurez-vous que le rôle est défini sur **Approbateur**.

![GSPeM](./images/gsemail12.png)

Vous pouvez également utiliser un workflow d’approbation existant dans Adobe Workfront. Pour ce faire, cliquez sur **Utiliser le modèle** et sélectionnez le modèle `--aepuserLdap-- - Approval Workflow`. Cliquez sur **Envoyer**.

![GSPeM](./images/gsemail13.png)

Cliquez sur **Afficher les commentaires dans Workfront**. Vous serez désormais envoyé à l’interface utilisateur de l’épreuve Adobe Workfront.

![GSPeM](./images/gsemail14.png)

Dans l’interface utilisateur d’Adobe Workfront Proof, cliquez sur **Prendre une décision**.

![GSPeM](./images/gsemail15.png)

Sélectionnez **Approuvé** et cliquez sur **Prendre une décision**.

![GSPeM](./images/gsemail16.png)

Cliquez sur **Publier**.

![GSPeM](./images/gsemail17.png)

Sélectionnez votre `--aepUserLdap-- - CitiSignal Fiber Launch Campaign` Campaign et cliquez sur **Publier**.

![GSPeM](./images/gsemail18.png)

Cliquez sur **Ouvrir dans le contenu**.

![GSPeM](./images/gsemail19.png)

Les 4 expériences d’e-mail sont désormais disponibles sous **Contenu** > **Expériences**.

![GSPeM](./images/gsemail20.png)

## 1.3.4.2 Création d’une campagne dans AJO

Connectez-vous à Adobe Journey Optimizer en allant sur [Adobe Experience Cloud](https://experience.adobe.com?lang=fr). Cliquez sur **Journey Optimizer**.

![ACOP ](./../../../modules/delivery-activation/ajo-b2c/ajob2c-1/images/acophome.png)

Vous serez redirigé vers la vue **Accueil** dans Journey Optimizer. Tout d’abord, assurez-vous d’utiliser le bon sandbox. Le sandbox à utiliser est appelé `--aepSandboxName--`. Vous serez alors dans la vue **Accueil** de votre `--aepSandboxName--` sandbox.

![ACOP ](./../../../modules/delivery-activation/ajo-b2c/ajob2c-1/images/acoptriglp.png)

Vous allez maintenant créer une campagne. Contrairement au parcours basé sur un événement de l’exercice précédent, qui repose sur les événements d’expérience entrants, les entrées ou les sorties d’audience pour déclencher un parcours pour un client spécifique, les campagnes ciblent une audience entière une fois avec du contenu unique tel que des newsletters, des promotions ponctuelles ou des informations génériques, ou périodiquement avec du contenu similaire envoyé régulièrement, par exemple des campagnes d’anniversaire et des rappels.

Dans le menu, accédez à **Campagnes** et cliquez sur **Créer une campagne**.

![Journey Optimizer](./images/gsemail21.png)

Sélectionnez **Planifié - Marketing** et cliquez sur **Créer**.

![Journey Optimizer](./images/gsemail22.png)

Dans l’écran de création de la campagne, configurez les éléments suivants :

- **Nom** : `--aepUserLdap--  - Online Gamers CitiSignal Fiber Max`.
- **Description** : Campagne Fibre pour les joueurs en ligne

Cliquez sur **Actions**.

![Journey Optimizer](./images/gsemail23.png)

Cliquez sur **+ Ajouter une action** puis sélectionnez **E-mail**.

![Journey Optimizer](./images/gsemail24.png)

Sélectionnez ensuite une **configuration d’e-mail** existante, puis cliquez sur **Modifier le contenu**.

![Journey Optimizer](./images/gsemail25.png)

Tu verras ça. Pour la **ligne d’objet**, utilisez la commande suivante :

```
{{profile.person.name.firstName}}, say goodbye to delays!
```

Cliquez ensuite sur **Modifier le contenu**.

![Journey Optimizer](./images/gsemail26.png)

Cliquez sur **Importer HTML**.

![Journey Optimizer](./images/gsemail27.png)

Cliquez ensuite sur le bouton pour **Adobe GenStudio for Performance Marketing**.

![Journey Optimizer](./images/gsemail28.png)

Vous devriez alors voir une fenêtre contextuelle qui affiche toutes les expériences d’e-mail publiées dans GenStudio for Performance Marketing. Sélectionnez l’une des expériences d’e-mail disponibles et cliquez sur **Utiliser**.

![Journey Optimizer](./images/gsemail29.png)

Sélectionnez votre propre référentiel AEM Assets CS, qui doit être nommé `--aepUserLdap-- - CitiSignal dev`, puis cliquez sur **Importer**.

![Journey Optimizer](./images/gsemail30.png)

Vous devriez alors voir ceci. Sélectionnez le bouton d’image manquant et cliquez sur **Sélectionner une ressource**.

![Journey Optimizer](./images/gsemail31.png)

Accédez au dossier qui ressemble à celui-ci, en commençant par **GenStudio.zip.....** et sélectionnez le `--aepUserLdap-- - neon rabbit.png` d’image. Cliquez sur **Sélectionner**

![Journey Optimizer](./images/gsemail32.png)

Vous devriez alors voir ceci.

![Journey Optimizer](./images/gsemail33.png)

Faites défiler l’écran jusqu’au pied de page, sélectionnez le mot **Se désabonner** et cliquez sur l’icône **lien**.

![Journey Optimizer](./images/gsemail38.png)

Définissez le **Type** sur **Désinscription/opt-out externe** et définissez l’URL sur `https://techinsiders.org/unsubscribe.html` (le lien de désinscription ne peut pas contenir d’URL vide).

Cliquez sur **Enregistrer** puis sur la **flèche** dans le coin supérieur gauche de l’écran pour revenir à la configuration de la campagne.

![Journey Optimizer](./images/gsemail39.png)

Accédez à **Audience**.

![Journey Optimizer](./images/gsemail34.png)

Cliquez sur **Sélectionner une audience**.

![Journey Optimizer](./images/gsemail35.png)

Sélectionnez l&#39;audience de la liste d&#39;abonnement pour les joueurs en ligne, qui doit être nommé `--aepUserLdap--_SL_Interest_Online_Gaming`. Cliquez sur **Enregistrer**.

![Journey Optimizer](./images/gsemail36.png)

Cliquez sur **Vérifier pour activer**.

![Journey Optimizer](./images/gsemail37.png)

Si votre configuration de campagne ne comporte aucun problème, vous pourrez cliquer sur **Activer**.

![Journey Optimizer](./images/gsemail40.png)

Votre campagne sera alors activée, ce qui prend quelques minutes.

![Journey Optimizer](./images/gsemail41.png)

Au bout de quelques minutes, la campagne est active et l’e-mail est envoyé à la liste d’abonnements que vous avez sélectionnée.

![Journey Optimizer](./images/gsemail42.png)

Vous avez maintenant terminé cet exercice.

## Étapes suivantes

Accédez à [ Résumé et avantages ](./summary.md){target="_blank"}

Revenir à [GenStudio for Performance Marketing](./genstudio.md){target="_blank"}

Revenir à [Tous les modules](./../../../overview.md){target="_blank"}
