---
title: Prise en main des notifications push
description: Prise en main des notifications push
kt: 5342
audience: Data Engineer, Data Architect, Orchestration Engineer, Marketer
doc-type: tutorial
exl-id: b46e0205-b0a1-4a14-95f6-9afe21cd2b5e
source-git-commit: fb14ba45333bdd5834ff0c6c2dc48dda35cfe85f
workflow-type: tm+mt
source-wordcount: '1235'
ht-degree: 9%

---

# 3.3.1 Prise en main des notifications push

Pour utiliser les notifications push avec Adobe Journey Optimizer, il existe un certain nombre de paramètres à vérifier et à connaître.

Voici tous les paramètres à vérifier :

- Jeux de données et schémas dans Adobe Experience Platform
- Flux de données pour mobile
- Propriété de collecte de données pour mobile
- Surface d’application pour les certificats push
- Tester votre configuration push à l&#39;aide d&#39;AEP Assurance

Examinons-les une par une.

Connectez-vous à Adobe Journey Optimizer en allant sur [Adobe Experience Cloud](https://experience.adobe.com?lang=fr). Cliquez sur **Journey Optimizer**.

![ACOP &#x200B;](./../../../../modules/delivery-activation/ajo-b2c/ajob2c-1/images/acophome.png)

Vous serez redirigé vers la vue **Accueil** dans Journey Optimizer. Tout d’abord, assurez-vous d’utiliser le bon sandbox. Le sandbox à utiliser est appelé `--aepSandboxName--`. Vous serez alors dans la vue **Accueil** de votre `--aepSandboxName--` sandbox.

![ACOP &#x200B;](./../../../../modules/delivery-activation/ajo-b2c/ajob2c-1/images/acoptriglp.png)

## Jeu de données de notification push 3.3.1.1

Adobe Journey Optimizer utilise des jeux de données pour stocker des éléments tels que les jetons push des appareils mobiles ou les interactions avec les messages push (comme : message envoyé, message ouvert, etc.) dans un jeu de données dans Adobe Journey Optimizer.

Vous pouvez trouver ces jeux de données en accédant à **Jeux de données** dans le menu sur le côté gauche de l’écran. Pour afficher les jeux de données système, cliquez sur l’icône **Activer les filtres**.

Activez l’option pour **Système** et recherchez **AJO**. Les jeux de données utilisés pour les notifications push s’affichent ensuite.

![Ingestion des données](./images/menudsjo1.png)

## Flux de données 3.3.1.2 pour Mobile

Accédez à [https://experience.adobe.com/#/data-collection/](https://experience.adobe.com/#/data-collection/).

Dans le menu de gauche, accédez à **Flux de données** et recherchez le flux de données que vous avez créé dans [Prise en main](./../../../../modules/getting-started/gettingstarted/ex2.md), qui est nommé `--aepUserLdap-- - One Adobe Datastream (Mobile)`. Cliquez pour l’ouvrir.

![Flux de données](./images/edgeconfig1a.png)

Cliquez sur **Modifier** sur le service **Adobe Experience Platform**.

![Flux de données](./images/edgeconfig1.png)

Vous verrez ensuite les paramètres de train de données qui ont été définis et dans quels jeux de données les événements et les attributs de profil seront stockés.

Vous devez également activer les options suivantes si elles ne sont pas encore activées :

- **Offer Decisioning**
- **Destinations de personnalisation**
- **Adobe Journey Optimizer**

Cliquez sur **Enregistrer**.

![Nommez le flux de données et enregistrez](./images/edgeconfig2.png)

## 3.3.1.3 votre propriété de collecte de données pour Mobile

Accédez à [https://experience.adobe.com/#/data-collection/](https://experience.adobe.com/#/data-collection/), à **Balises**. Dans le cadre du module [Prise en main](./../../../../modules/getting-started/gettingstarted/ex1.md), les propriétés des balises de collecte de données ont été créées.

Vous utilisez déjà ces propriétés de balises de collecte de données dans le cadre de modules précédents.

Cliquez pour ouvrir la propriété Collecte de données pour les appareils mobiles.

![DSN &#x200B;](./images/launchprop.png)

Dans votre propriété Collecte de données, accédez à **Extensions**. Vous verrez ensuite les différentes extensions nécessaires pour l’application mobile. Cliquez pour sélectionner l’extension **Adobe Experience Platform Edge Network** puis sélectionnez **Configurer**.

![Collecte de données dʼAdobe Experience Platform](./images/launchprop1.png)

Vous verrez alors que votre flux de données pour mobile est lié ici. Cliquez ensuite sur **Annuler** pour revenir à la présentation des extensions.

![Collecte de données dʼAdobe Experience Platform](./images/launchprop2.png)

Tu reviendras ensuite ici. L’extension s’affiche pour **AEP Assurance**. AEP Assurance vous permet de contrôler, de tester, de simuler et de valider la manière dont vous collectez les données ou dont les expériences sont diffusées dans votre application mobile. Vous pouvez en savoir plus sur AEP Assurance ici : [https://experienceleague.adobe.com/fr/docs/experience-platform/assurance/home](https://experienceleague.adobe.com/fr/docs/experience-platform/assurance/home).

![Collecte de données dʼAdobe Experience Platform](./images/launchprop8.png)

Cliquez ensuite sur **Configurer** pour ouvrir l’extension **Adobe Journey Optimizer**. Cette extension active les notifications push et les mesures pour Adobe Journey Optimizer.

![Collecte de données dʼAdobe Experience Platform](./images/launchprop9.png)

Vous verrez ensuite que c’est là que le jeu de données pour le suivi des événements push est lié. Il n’est pas nécessaire d’apporter des modifications à votre propriété de collecte de données. Cliquez sur **Annuler** pour revenir à l’écran précédent.

![Collecte de données dʼAdobe Experience Platform](./images/launchprop10.png)

## 3.3.1.4 Vérifier la configuration de votre Surface d’application

Accédez à [https://experience.adobe.com/#/data-collection/](https://experience.adobe.com/#/data-collection/). Dans le menu de gauche, accédez à **Surfaces de l’application** et ouvrez la Surface de l’application pour **DX Demo App APNS**.

![Collecte de données dʼAdobe Experience Platform](./images/appsf.png)

Vous verrez ensuite la surface d’application configurée pour iOS et Android.

![Collecte de données dʼAdobe Experience Platform](./images/appsf1.png)

## 3.3.1.5 Testez la configuration des notifications push à l’aide d’AEP Assurance.

Vous avez déjà installé l’application mobile **DX Demo** dans le cadre du module **Prise en main**. Une fois l&#39;application installée, vous la trouverez sur l&#39;écran d&#39;accueil de votre appareil. Cliquez sur l’icône pour ouvrir l’application.

![DSN &#x200B;](./../../../../modules/getting-started/gettingstarted/images/mobileappn1.png)

Après vous être connecté, une notification s’affichera pour vous demander l’autorisation d’envoyer des notifications. Nous enverrons des notifications dans le cadre du tutoriel. Cliquez donc sur **Autoriser**.

![DSN &#x200B;](./../../../modules/../getting-started/gettingstarted/images/mobileappn2.png)

Vous verrez alors la page d’accueil de l’application. Accédez à **Paramètres**.

![DSN &#x200B;](./../../../modules/../getting-started/gettingstarted/images/mobileappn3.png)

Dans les paramètres, vous verrez qu’un **Projet public** est actuellement chargé dans l’application. Cliquez sur **Projet personnalisé**.

![DSN &#x200B;](./../../../modules/../getting-started/gettingstarted/images/mobileappn4.png)

Vous pouvez désormais charger un projet personnalisé. Cliquez sur le code QR pour charger facilement votre projet.

![DSN &#x200B;](./../../../modules/../getting-started/gettingstarted/images/mobileappn5.png)

Après avoir parcouru la section **Prise en main**, vous avez obtenu le résultat suivant. Cliquez pour ouvrir le **Projet de vente au détail mobile** qui a été créé pour vous.

![DSN &#x200B;](./../../../modules/../getting-started/gettingstarted/images/dsn5b.png)

Si vous avez fermé accidentellement la fenêtre de votre navigateur ou pour des sessions de démonstration ou d’activation ultérieures, vous pouvez également accéder à votre projet de site web en accédant à [https://dsn.adobe.com/projects](https://dsn.adobe.com/projects). Après vous être connecté avec votre Adobe ID, voici ce que vous verrez. Cliquez sur votre projet d’application mobile pour l’ouvrir.

![DSN &#x200B;](./../../../modules/../getting-started/gettingstarted/images/web8a.png)

Cliquez ensuite sur **Exécuter**.

![DSN &#x200B;](./images/web8b.png)

Vous verrez ensuite cette fenêtre contextuelle, qui contient un code QR. Scannez ce code QR à partir de l’application mobile.

![DSN &#x200B;](./../../../modules/../getting-started/gettingstarted/images/web8c.png)

Votre ID de projet s’affiche alors dans l’application, après quoi vous pouvez cliquer sur **Basculer**.

![DSN &#x200B;](./../../../modules/../getting-started/gettingstarted/images/mobileappn7.png)

Votre application est maintenant prête à être utilisée.

![DSN &#x200B;](./../../../modules/../getting-started/gettingstarted/images/mobileappn8.png)

Vous devez maintenant scanner un code QR pour connecter votre appareil mobile à votre session Assurance.

Pour démarrer une session AEP Assurance, accédez à [https://experience.adobe.com/#/data-collection/](https://experience.adobe.com/#/data-collection/). Cliquez sur **Assurance** dans le menu de gauche. Cliquez ensuite sur **Créer une session**.

![Collecte de données dʼAdobe Experience Platform](./images/griffon3.png)

Sélectionnez **Connexion de lien profond** puis cliquez sur **Démarrer**.

![Collecte de données dʼAdobe Experience Platform](./images/griffon5.png)

Renseignez les valeurs :

- Nom de la session : `--aepUserLdap-- - Push Debugging`
- URL de base : `dxdemo://default`

Cliquez sur **Suivant**.

![Collecte de données dʼAdobe Experience Platform](./images/griffon4.png)

Un code QR s’affiche alors à l’écran, que vous devez numériser avec votre appareil iOS.

![Collecte de données dʼAdobe Experience Platform](./images/griffon6.png)

Sur votre appareil mobile, ouvrez l’application de caméra et numérisez le code QR affiché par Assurance.

![Collecte de données dʼAdobe Experience Platform](./images/ipadPushTest8a.png)

Vous verrez alors un écran contextuel, vous demandant de saisir le code PIN. Copiez le code PIN de l’écran AEP Assurance, puis cliquez sur **Connexion**.

![Collecte de données dʼAdobe Experience Platform](./images/ipadPushTest9.png)

Tu verras ça.

![Collecte de données dʼAdobe Experience Platform](./images/ipadPushTest11.png)

Dans Assurance, vous verrez désormais qu’un appareil client est connecté à la session Assurance. Cliquez ensuite sur **Configurer**.

![Collecte de données dʼAdobe Experience Platform](./images/griffon7.png)

Faites défiler jusqu’à **Push Debug**. Cliquez sur l’icône **+**, puis sur **Enregistrer**.

![Collecte de données dʼAdobe Experience Platform](./images/griffon7a.png)

Accédez à **Push Debug**. Tu devrais voir ça.

![Collecte de données dʼAdobe Experience Platform](./images/griffon10.png)

Quelques explications :

- La première colonne, **Client**, affiche les identifiants disponibles sur votre appareil iOS. Un ECID et un jeton push s’affichent.
- La 2e colonne affiche les **informations d’identification et configuration App Store**
- La deuxième colonne affiche des informations **Profil**, avec des informations supplémentaires sur la plateforme sur laquelle réside le jeton push (APNS ou APNSSandbox). Si vous cliquez sur le bouton **Inspecter le profil**, vous accédez à Adobe Experience Platform et le profil client en temps réel complet s’affiche.

Pour tester votre configuration push, cliquez sur le bouton **Envoyer la configuration push de test**. Cliquez sur **Envoyer une notification push de test**

![Collecte de données dʼAdobe Experience Platform](./images/griffon11.png)

Vous devez vous assurer que l’application **DX Demo** n’est pas ouverte au moment où vous cliquez sur le bouton **Envoyer une notification push**. Si l&#39;application est ouverte, la notification push peut être reçue en arrière-plan et ne pas être visible.

Une notification push comme celle-ci s’affiche alors sur votre appareil mobile.

![Collecte de données dʼAdobe Experience Platform](./images/ipadPush2.png)

Si vous avez reçu la notification push, cela signifie que votre configuration est correcte et qu’elle fonctionne correctement. Vous pouvez désormais créer un parcours réel qui se traduira par l’envoi d’un message push depuis Journey Optimizer.

## Étapes suivantes

Accédez à [3.3.2 Configuration d’un parcours avec des messages push](./ex2.md){target="_blank"}

Revenez à [Adobe Journey Optimizer : messages push et in-app](ajopushinapp.md){target="_blank"}

Revenir à [Tous les modules](./../../../../overview.md){target="_blank"}
