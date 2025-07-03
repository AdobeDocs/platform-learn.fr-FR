---
title: Prise en main des notifications push
description: Prise en main des notifications push
kt: 5342
audience: Data Engineer, Data Architect, Orchestration Engineer, Marketer
doc-type: tutorial
source-git-commit: 203590e3289d2e5342085bf8b6b4e3cd11859539
workflow-type: tm+mt
source-wordcount: '1264'
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

![ACOP ](./../../../../modules/delivery-activation/ajo-b2c/ajob2c-1/images/acophome.png)

Vous serez redirigé vers la vue **Accueil** dans Journey Optimizer. Tout d’abord, assurez-vous d’utiliser le bon sandbox. Le sandbox à utiliser est appelé `--aepSandboxName--`. Vous serez alors dans la vue **Accueil** de votre `--aepSandboxName--` sandbox.

![ACOP ](./../../../../modules/delivery-activation/ajo-b2c/ajob2c-1/images/acoptriglp.png)

## Jeu de données de notification push 3.4.4.1

Adobe Journey Optimizer utilise des jeux de données pour stocker des éléments tels que les jetons push des appareils mobiles ou les interactions avec les messages push (comme : message envoyé, message ouvert, etc.) dans un jeu de données dans Adobe Journey Optimizer.

Vous pouvez trouver ces jeux de données en accédant à **[!UICONTROL Jeux de données]** dans le menu sur le côté gauche de l’écran. Pour afficher les jeux de données système, cliquez sur l’icône de filtre.

Activez l’option **Afficher les jeux de données système** et recherchez **AJO**. Les jeux de données utilisés pour les notifications push s’affichent ensuite.

![Ingestion des données](./images/menudsjo1.png)

## Flux de données 3.4.4.2 pour Mobile

Accédez à [https://experience.adobe.com/#/data-collection/](https://experience.adobe.com/#/data-collection/).

Dans le menu de gauche, accédez à **[!UICONTROL Flux de données]** et recherchez le flux de données que vous avez créé dans [Prise en main](./../../../../modules/getting-started/gettingstarted/ex2.md), qui est nommé `--aepUserLdap-- - Demo System Datastream (Mobile)`. Cliquez pour l’ouvrir.

![Cliquez sur icône Flux de données dans le volet de navigation de gauche](./images/edgeconfig1a.png)

Cliquez sur **Modifier** sur le service **Adobe Experience Platform**.

![Cliquez sur icône Flux de données dans le volet de navigation de gauche](./images/edgeconfig1.png)

Vous verrez ensuite les paramètres de train de données qui ont été définis et dans quels jeux de données les événements et les attributs de profil seront stockés.

Vous devez également activer les options suivantes si elles ne sont pas encore activées :

- **Offer Decisioning**
- **Destinations de personnalisation**
- **Adobe Journey Optimizer**

Cliquez sur **Enregistrer**.

![Nommez le flux de données et enregistrez](./images/edgeconfig2.png)

## 3.4.4.3 votre propriété de collecte de données pour Mobile

Accédez à [https://experience.adobe.com/#/data-collection/](https://experience.adobe.com/#/data-collection/). Dans le cadre de la [Prise en main](./../../../../modules/getting-started/gettingstarted/ex1.md), 2 propriétés de collecte de données ont été créées.
Vous utilisez déjà ces propriétés du client de collecte de données dans le cadre de modules précédents.

Cliquez pour ouvrir la propriété Collecte de données pour les appareils mobiles.

![DSN ](./images/launchprop.png)

Dans votre propriété Collecte de données, accédez à **Extensions**. Vous verrez ensuite les différentes extensions nécessaires pour l’application mobile. Cliquez pour ouvrir l’extension **Adobe Experience Platform Edge Network**.

![Collecte de données dʼAdobe Experience Platform](./images/launchprop1.png)

Vous verrez alors que votre flux de données pour mobile est lié ici. Cliquez ensuite sur **Annuler** pour revenir à la présentation de vos extensions.

![Collecte de données dʼAdobe Experience Platform](./images/launchprop2.png)

Tu reviendras ensuite ici. L’extension s’affiche pour **AEP Assurance**. AEP Assurance vous permet de contrôler, de tester, de simuler et de valider la manière dont vous collectez les données ou dont les expériences sont diffusées dans votre application mobile. Vous pouvez en savoir plus sur AEP Assurance et le projet Griffon ici [https://aep-sdks.gitbook.io/docs/beta/project-griffon](https://aep-sdks.gitbook.io/docs/beta/project-griffon).

![Collecte de données dʼAdobe Experience Platform](./images/launchprop8.png)

Cliquez ensuite sur **Configurer** pour ouvrir l’extension **Adobe Journey Optimizer**.

![Collecte de données dʼAdobe Experience Platform](./images/launchprop9.png)

Vous verrez ensuite que c’est là que le jeu de données pour le suivi des événements push est lié.

![Collecte de données dʼAdobe Experience Platform](./images/launchprop10.png)

Il n’est pas nécessaire d’apporter des modifications à votre propriété de collecte de données.

## 3.4.4.4 Vérifier la configuration de votre Surface d’application

Accédez à [https://experience.adobe.com/#/data-collection/](https://experience.adobe.com/#/data-collection/). Dans le menu de gauche, accédez à **Surfaces de l’application** et ouvrez la Surface de l’application pour **DX Demo App APNS**.

![Collecte de données dʼAdobe Experience Platform](./images/appsf.png)

Vous verrez ensuite la surface d’application configurée pour iOS et Android.

![Collecte de données dʼAdobe Experience Platform](./images/appsf1.png)

## 3.4.4.5 Testez la configuration des notifications push à l’aide d’AEP Assurance.

Une fois l&#39;application installée, vous la trouverez sur l&#39;écran d&#39;accueil de votre appareil. Cliquez sur l’icône pour ouvrir l’application.

![DSN ](./../../../../modules/getting-started/gettingstarted/images/mobileappn1.png)

Lorsque vous utilisez l’application pour la première fois, il vous sera demandé de vous connecter à l’aide de votre Adobe ID. Terminez le processus de connexion.

![DSN ](./../../../modules/../getting-started/gettingstarted/images/mobileappn2.png)

Après vous être connecté, une notification s’affichera pour vous demander l’autorisation d’envoyer des notifications. Nous enverrons des notifications dans le cadre du tutoriel. Cliquez donc sur **Autoriser**.

![DSN ](./../../../modules/../getting-started/gettingstarted/images/mobileappn3.png)

Vous verrez alors la page d’accueil de l’application. Accédez à **Paramètres**.

![DSN ](./../../../modules/../getting-started/gettingstarted/images/mobileappn4.png)

Dans les paramètres, vous verrez qu’un **Projet public** est actuellement chargé dans l’application. Cliquez sur **Projet personnalisé**.

![DSN ](./../../../modules/../getting-started/gettingstarted/images/mobileappn5.png)

Vous pouvez désormais charger un projet personnalisé. Cliquez sur le code QR pour charger facilement votre projet.

![DSN ](./../../../modules/../getting-started/gettingstarted/images/mobileappn6.png)

Après avoir parcouru la section **Prise en main**, vous avez obtenu le résultat suivant. Cliquez pour ouvrir le **Projet de vente au détail mobile** qui a été créé pour vous.

![DSN ](./../../../modules/../getting-started/gettingstarted/images/dsn5b.png)

Si vous avez fermé accidentellement la fenêtre de votre navigateur ou pour des sessions de démonstration ou d’activation ultérieures, vous pouvez également accéder à votre projet de site web en accédant à [https://dsn.adobe.com/projects](https://dsn.adobe.com/projects). Après vous être connecté avec votre Adobe ID, voici ce que vous verrez. Cliquez sur votre projet d’application mobile pour l’ouvrir.

![DSN ](./../../../modules/../getting-started/gettingstarted/images/web8a.png)

Cliquez ensuite sur **Exécuter**.

![DSN ](./images/web8b.png)

Vous verrez ensuite cette fenêtre contextuelle, qui contient un code QR. Scannez ce code QR à partir de l’application mobile.

![DSN ](./../../../modules/../getting-started/gettingstarted/images/web8c.png)

Votre ID de projet s’affichera alors dans l’application, après quoi vous pourrez cliquer sur **Enregistrer**.

![DSN ](./../../../modules/../getting-started/gettingstarted/images/mobileappn7.png)

Maintenant, revenez à **Accueil** dans l’application. Votre application est maintenant prête à être utilisée.

![DSN ](./../../../modules/../getting-started/gettingstarted/images/mobileappn8.png)

Vous devez maintenant scanner un code QR pour connecter votre appareil mobile à votre session AEP Assurance.

Pour démarrer une session AEP Assurance, accédez à [https://experience.adobe.com/#/data-collection/](https://experience.adobe.com/#/data-collection/). Cliquez sur **Assurance** dans le menu de gauche. Cliquez ensuite sur **Créer une session**.

![Collecte de données dʼAdobe Experience Platform](./images/griffon3.png)

Cliquez sur **Démarrer**.

![Collecte de données dʼAdobe Experience Platform](./images/griffon5.png)

Renseignez les valeurs :

- Nom de la session : utilisez `--aepUserLdap-- - push debugging` et remplacez ldap par votre ldap.
- URL de base : utiliser `dxdemo://default`

Cliquez sur **Suivant**.

![Collecte de données dʼAdobe Experience Platform](./images/griffon4.png)

Un code QR s’affiche alors à l’écran, que vous devez numériser avec votre appareil iOS.

![Collecte de données dʼAdobe Experience Platform](./images/griffon6.png)

Sur votre appareil mobile, ouvrez l’application de caméra et numérisez le code QR affiché par AEP Assurance.

![Collecte de données dʼAdobe Experience Platform](./images/ipadPushTest8a.png)

Vous verrez alors un écran contextuel, vous demandant de saisir le code PIN. Copiez le code PIN de l’écran AEP Assurance, puis cliquez sur **Connexion**.

![Collecte de données dʼAdobe Experience Platform](./images/ipadPushTest9.png)

Tu verras ça.

![Collecte de données dʼAdobe Experience Platform](./images/ipadPushTest11.png)

Dans Assurance, vous verrez désormais qu’un appareil est connecté à la session Assurance. Cliquez sur **Terminé**.

![Collecte de données dʼAdobe Experience Platform](./images/griffon7.png)

Accédez à **Push Debug**.

>[!NOTE]
>
>Si vous ne trouvez pas **Débogage push** dans le menu de gauche, cliquez sur **Configurer** dans le coin inférieur gauche de l’écran et ajoutez **Débogage push** au menu.

Vous verrez quelque chose comme ça.

![Collecte de données dʼAdobe Experience Platform](./images/griffon10.png)

Quelques explications :

- La première colonne, **Client**, affiche les identifiants disponibles sur votre appareil iOS. Un ECID et un jeton push s’affichent.
- La 2e colonne affiche les **informations d’identification et configuration App Store**, qui ont été configurées dans le cadre de l’exercice **3.4.5.4Créer une configuration d’application dans Launch**
- La deuxième colonne affiche des informations **Profil**, avec des informations supplémentaires sur la plateforme sur laquelle réside le jeton push (APNS ou APNSSandbox). Si vous cliquez sur le bouton **Inspecter le profil**, vous accédez à Adobe Experience Platform et le profil client en temps réel complet s’affiche.

Pour tester votre configuration push, cliquez sur le bouton **Envoyer la configuration push de test**. Cliquez sur **Envoyer une notification push de test**

![Collecte de données dʼAdobe Experience Platform](./images/griffon11.png)

Vous devez vous assurer que l’application **DX Demo** n’est pas ouverte au moment où vous cliquez sur le bouton **Envoyer une notification push**. Si l’application est ouverte, la notification push peut être reçue en arrière-plan et n’est pas visible.

Une notification push comme celle-ci s’affiche alors sur votre appareil mobile.

![Collecte de données dʼAdobe Experience Platform](./images/ipadPush2.png)

Si vous avez reçu la notification push, cela signifie que votre configuration est correcte et qu’elle fonctionne correctement. Vous pouvez désormais créer un parcours réel qui se traduira par l’envoi d’un message push depuis Journey Optimizer.

## Étapes suivantes

Accédez à [3.3.2 Configuration d’un parcours avec des messages push](./ex2.md){target="_blank"}

Revenez à [Adobe Journey Optimizer : messages push et in-app](ajopushinapp.md){target="_blank"}

Revenir à [Tous les modules](./../../../../overview.md){target="_blank"}
