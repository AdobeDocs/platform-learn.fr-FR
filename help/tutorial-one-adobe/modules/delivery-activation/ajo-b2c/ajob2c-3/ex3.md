---
title: Offer Decisioning - Tester votre décision
description: Offer Decisioning - Tester votre décision
kt: 5342
doc-type: tutorial
exl-id: c40b9b8c-9717-403c-bf02-6b8f42a59c05
source-git-commit: 2e856759e1a9b5509ad0632e28b269bcfc4ae861
workflow-type: tm+mt
source-wordcount: '414'
ht-degree: 1%

---

# 3.3.3 Configurer une campagne avec des messages in-app

Connectez-vous à Adobe Journey Optimizer en allant sur [Adobe Experience Cloud](https://experience.adobe.com?lang=fr). Cliquez sur **Journey Optimizer**.

![ACOP ](./../../../../modules/delivery-activation/ajo-b2c/ajob2c-1/images/acophome.png)

Vous serez redirigé vers la vue **Accueil** dans Journey Optimizer. Tout d’abord, assurez-vous d’utiliser le bon sandbox. Le sandbox à utiliser est appelé `--aepSandboxName--`. Vous serez alors dans la vue **Accueil** de votre `--aepSandboxName--` sandbox.

![ACOP ](./../../../../modules/delivery-activation/ajo-b2c/ajob2c-1/images/acoptriglp.png)

## Configuration 3.3.3.1 canal de messages in-app

Dans le menu de gauche, accédez à **Canaux** puis sélectionnez **Configurations de canal**. Cliquez sur **Créer une configuration de canal**.

![ InApp ](./images/inapp1.png)

Saisissez le nom : `--aepUserLdap--_In-app_Messages`, sélectionnez le canal **Messagerie in-app** puis activez les plateformes **Web**, **iOS** et **Android**.

![ InApp ](./images/inapp2.png)

Faites défiler l’écran vers le bas, vous devriez voir ceci.

![ InApp ](./images/inapp3.png)

Assurez-vous que l’option **Une seule page** est activée.

Pour **Web**, saisissez l&#39;URL du site Web qui a été créé précédemment dans le cadre du module **Prise en main**, qui se présente comme suit : `https://dsn.adobe.com/web/--aepUserLdap---XXXX`. N’oubliez pas de remplacer le **XXXX** par le code unique de votre site web.

Pour **iOS** et **Android**, saisissez `com.adobe.dsn.dxdemo`.

![ InApp ](./images/inapp4.png)

Faites défiler vers le haut et cliquez sur **Envoyer**.

![ InApp ](./images/inapp5.png)

Votre configuration de canal est maintenant prête à être utilisée.

![ InApp ](./images/inapp6.png)

## 3.3.3.2 Configurer une campagne planifiée pour les messages in-app

Dans le menu de gauche, accédez à **Campagnes** puis cliquez sur **Créer une campagne**.

![ InApp ](./images/inapp7.png)

Sélectionnez **Planifié - Marketing** puis cliquez sur **Créer**.

![ InApp ](./images/inapp8.png)

Saisissez le nom `--aepUserLdap-- - CitiSignal Fiber Max`, puis cliquez sur **Actions**.

![ InApp ](./images/inapp9.png)

Cliquez sur **+ Ajouter une action** puis sélectionnez **Message in-app**.

![ InApp ](./images/inapp10.png)

Sélectionnez la configuration de canal de message in-app que vous avez créée à l’étape précédente, et qui est nommée : `--aepUserLdap--_In-app_Messages`. Cliquez sur **Modifier le contenu**.

![ InApp ](./images/inapp11.png)

Vous devriez alors voir ceci. Cliquez sur **Modal**.

![ InApp ](./images/inapp12.png)

Cliquez sur **Modifier la disposition**.

![ InApp ](./images/inapp13.png)

Cliquez sur l’icône **URL Media** pour sélectionner une ressource dans AEM Assets.

![ InApp ](./images/inapp14.png)

Accédez au dossier **citisignal-images** et sélectionnez le fichier image **neon-rabbit.jpg**. Cliquez sur **Sélectionner**.

![ InApp ](./images/inapp15.png)

Pour le texte **En-tête**, utilisez : `CitiSignal Fiber Max`.
Pour le texte **Body**, utilisez : `Conquer lag with Fiber Max`.

![ InApp ](./images/inapp16.png)

Définissez le **texte de #1 du bouton** sur : `Go to Plans`.
Définissez la **cible** sur `com.adobe.dsn.dxdemo://plans`.

Cliquez sur **Vérifier pour activer**.

![ InApp ](./images/inapp17.png)

Cliquez sur **Activer**.

![ InApp ](./images/inapp18.png)

Le statut de votre campagne est maintenant défini sur **Activation**. La diffusion de la campagne peut prendre quelques minutes.

![ InApp ](./images/inapp19.png)

Une fois que le statut est passé à **Actif**, vous pouvez tester votre campagne.

![ InApp ](./images/inapp20.png)

## 3.3.3.3 Tester votre campagne de messagerie in-app sur mobile

Sur votre appareil mobile, ouvrez l’application . Le nouveau message in-app doit alors apparaître après le lancement de l’application. Cliquez sur le bouton **Accéder aux plans**.

![ InApp ](./images/inapp21.png)

Vous serez ensuite redirigé vers la page **Plans**.

![ InApp ](./images/inapp22.png)

## Étapes suivantes

Accédez à [ Résumé et avantages ](./summary.md){target="_blank"}

Revenez à [Adobe Journey Optimizer : messages push et in-app](ajopushinapp.md){target="_blank"}

Revenir à [Tous les modules](./../../../../overview.md){target="_blank"}
