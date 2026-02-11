---
title: Utiliser le curseur pour développer votre projet
description: Utiliser le curseur pour développer votre projet
kt: 5342
doc-type: tutorial
exl-id: c73498b6-5e08-41b5-81a9-c0a76a6e2792
source-git-commit: 25901342e8d9c46b0edce3b2092b9f1d66ba5849
workflow-type: tm+mt
source-wordcount: '1565'
ht-degree: 0%

---

# 1.7.2 Utiliser le curseur pour développer votre projet

## 1.7.2.1 Configurer votre répertoire et vos outils

Sur votre bureau, créez un répertoire nommé `--aepUserLdap---commerce`

![Commerce et Agentic](./images/cursorai1.png)

Cliquez avec le bouton droit sur votre dossier et sélectionnez **Nouveau terminal dans le dossier**.

![Commerce et Agentic](./images/cursorai2.png)

Vous devriez alors voir ceci.

![Commerce et Agentic](./images/cursorai3.png)

Vous devez maintenant cloner un référentiel Github existant, que vous pouvez afficher [https://github.com/adobe/commerce-integration-starter-kit](https://github.com/adobe/commerce-integration-starter-kit).

Ce référentiel est le kit de démarrage de l’intégration d’Adobe qui utilise Adobe Developer App Builder pour améliorer la fiabilité de la connexion en temps réel et réduire le délai de mise sur le marché des intégrations entre Adobe Commerce et d’autres systèmes back-office, tels que les ERP, les CRM et les PIM.

![Commerce et Agentic](./images/cursorai4.png)

Il existe plusieurs façons de cloner ce référentiel. Dans cet exemple, Terminal est utilisé.

Saisissez la commande suivante dans la fenêtre de votre terminal et exécutez-la.

`git clone https://github.com/adobe/commerce-integration-starter-kit`

![Commerce et Agentic](./images/cursorai5.png)

Au bout de quelques secondes, vous devriez voir ce résultat.

![Commerce et Agentic](./images/cursorai6.png)

Ensuite, vous devez accéder au dossier qui vient d’être créé. Saisissez la commande suivante, puis exécutez-la.

`cd commerce-integration-starter-kit`

![Commerce et Agentic](./images/cursorai7.png)

Vous devriez alors voir ceci.

![Commerce et Agentic](./images/cursorai8.png)

Vous devez ensuite configurer les outils d’extensibilité de Commerce pour Cursor. Saisissez la commande suivante, puis exécutez-la.

`aio commerce extensibility tools-setup`

![Commerce et Agentic](./images/cursorai9.png)

Sélectionnez **Répertoire actuel**.

![Commerce et Agentic](./images/cursorai10.png)

Sélectionnez **Curseur**.

![Commerce et Agentic](./images/cursorai11.png)

Sélectionnez **npm**.

![Commerce et Agentic](./images/cursorai12.png)

Au bout de quelques minutes, vous devriez voir ceci.

![Commerce et Agentic](./images/cursorai13.png)

En installant les outils d’extensibilité de Commerce pour Cursor, un serveur MCP est désormais disponible dans le cadre de votre environnement Cursor. Dans les exercices suivants, vous utiliserez ce serveur MCP pour vous aider à développer et déployer le projet App Builder.

## 1.7.2.2 Configurer le webhook

Pour cet exercice, vous avez besoin d’un webhook qui doit être configuré afin que, lorsqu’une commande est créée, l’événement order puisse être diffusé en continu vers ce webhook. Dans cet exercice, vous allez utiliser un exemple de point d’entrée à l’aide de [https://pipedream.com/requestbin](https://pipedream.com/requestbin).

Accédez à [https://pipedream.com/requestbin](https://pipedream.com/requestbin), créez un compte, puis un espace de travail. Une fois l’espace de travail créé, un élément similaire s’affiche.

Cliquez sur **copier** pour copier l’URL. Vous devrez spécifier cette URL dans l’exercice suivant. Dans cet exemple, l’URL est `https://eodts05snjmjz67.m.pipedream.net`.

![Curseur + Commerce](./images/webhook1.png)

## 1.7.2.3 Créer une application avec un curseur

Ouvrez le curseur. Cliquez sur **Ouvrir le projet**.

![Curseur + Commerce](./images/cursorai14.png)

Accédez au dossier que vous avez créé, qui doit être nommé `--aepUserLdap---commerce`. Dans ce dossier, sélectionnez le dossier nommé `commerce-integration-starter-kit`. Cliquez sur **Ouvrir**.

![Curseur + Commerce](./images/cursorai15.png)

Vous devriez alors voir ceci. Avant de poursuivre, assurez-vous que le dossier de niveau supérieur ouvert dans le curseur est `commerce-integration-starter-kit`.

![Curseur + Commerce](./images/cursorai16.png)

Utilisez le raccourci clavier `Cmd + Shift + J` pour ouvrir les paramètres du curseur. Vous devriez alors voir ceci. Accédez à **Outils et MCP**.

![Curseur + Commerce](./images/cursorai17.png)

Activez le serveur MCP **extensibilité de commerce**. Une fois cette opération terminée, cliquez sur le **X** pour fermer la fenêtre.

![Curseur + Commerce](./images/cursorai18.png)

Copiez l&#39;invite suivante et collez-la dans Cursor. Cliquez ensuite sur le bouton **envoyer**.

`I would like to build an app that subscribes to order created events and sends them to a configurable URL with basic authentication`

![Curseur + Commerce](./images/cursorai19.png)

Le curseur va commencer à raisonner et à exécuter. Le curseur vous demandera une confirmation à quelques reprises. Dans ce cas, cliquez sur **Exécuter**. Cela peut se produire 5 à 10 fois, selon le raisonnement et vos paramètres.

![Curseur + Commerce](./images/cursorai20.png)

Au bout de quelques minutes, vous devriez voir quelque chose comme ça.

![Curseur + Commerce](./images/cursorai21.png)

L’étape suivante, indiquée par Cursor, consiste à créer un fichier portant le nom `.env` et à y fournir les variables requises.

## 1.7.2.4 Créer votre fichier .env

Sélectionnez le fichier **env.dist**. Saisissez la `Cmd + C` de commande, puis saisissez la `Cmd + V` de commande.

![Curseur + Commerce](./images/cursorai22.png)

Renommez le fichier nouvellement créé en `.env`.

![Curseur + Commerce](./images/cursorai23.png)

Ensuite, vous devez fournir les valeurs de toutes les variables dans le fichier **.env**.

![Curseur + Commerce](./images/cursorai24.png)

C&#39;est ici que vous trouverez toutes les informations requises.

### Points d’entrée Commerce

Vous pouvez trouver ces variables sur [https://experience.adobe.com](https://experience.adobe.com?lang=fr). Cliquez sur **Commerce**.

![Curseur + Commerce](./images/cursorai25.png)

Vous devriez alors voir ceci. Cliquez sur l’icône **informations** en regard de votre environnement ACCS, qui doit être nommé `--aepUserLdap-- - ACCS`. Copiez les valeurs du point d’entrée REST et du point d’entrée GraphQL.

Dans cet exemple, il s’agit des valeurs à copier. Collez-les en regard des variables ci-dessous dans le fichier **.env** aux lignes 6 et 7.


- **COMMERCE_BASE_URL** = https://na1-sandbox.api.commerce.adobe.com/Lkp3U7tvTBNAmpFvwnZJ4B/
- **COMMERCE_GRAPHQL_ENDPOINT** = https://na1-sandbox.api.commerce.adobe.com/Lkp3U7tvTBNAmpFvwnZJ4B/graphql

![Curseur + Commerce](./images/cursorai26.png)

Vous devriez ensuite l’avoir dans le fichier **.env**.

![Curseur + Commerce](./images/cursorai26a.png)

### Variables de projet Adobe I/O

Vous pouvez trouver ces variables sur [https://developer.adobe.com/console](https://developer.adobe.com/console). Accédez à **Projets** et cliquez pour ouvrir le projet Adobe I/O que vous avez créé dans l’exercice précédent et qui doit être nommé `--aepUserLdap-- Commerce Events`.

![Curseur + Commerce](./images/cursorai27.png)

Accédez à **Production**.

![Curseur + Commerce](./images/cursorai28.png)

Accédez à **OAuth de serveur à serveur**. Vous devriez alors voir ceci.

![Curseur + Commerce](./images/cursorai29.png)

Copiez les valeurs des champs **ID client**, **Secret client**, **ID de compte technique**, **E-mail de compte technique** et **ID d’organisation** et collez-les en regard des variables ci-dessous dans le fichier **.env** sur les lignes 13 à 17.

- **OAUTH_CLIENT_ID**= **ID client**
- **OAUTH_CLIENT_SECRET**= **Secret client**
- **OAUTH_TECHNICAL_ACCOUNT_ID**= **Identifiant de compte technique**
- **OAUTH_TECHNICAL_ACCOUNT_EMAIL**= **E-mail du compte technique**
- **OAUTH_ORG_ID**= **ID d’organisation**

Vous devriez ensuite l’avoir dans le fichier **.env**.

![Curseur + Commerce](./images/cursorai29a.png)

### COMMERCE_ADOBE_IO_EVENTS_MERCHANT_ID

Pour le champ **COMMERCE_ADOBE_IO_EVENTS_MERCHANT_ID=**, saisissez la valeur `--aepUserLdap--_commerce_events` ligne 34 dans le fichier **.env**.

Vous devriez ensuite l’avoir dans le fichier **.env**.

![Curseur + Commerce](./images/cursorai30.png)

### Configurations de Workspace

Pour récupérer ces variables, revenez à votre projet Adobe I/O et cliquez sur **Présentation de Workspace**.

Après avoir accédé à la présentation de **Workspace**, jetez un coup d’œil à l’URL, qui doit ressembler à ceci : **https://developer.adobe.com/console/projects/133309/4566206088345586770/workspaces/4566206088345619105/details**.

Le premier nombre de cet exemple, 133309, est la valeur à utiliser pour le champ **IO_CONSUMER_ID**.
Le deuxième nombre de cet exemple, 4566206088345586770, est la valeur à utiliser pour le champ **IO_PROJECT_ID**.
Le troisième nombre de cet exemple, 4566206088345619105, est la valeur à utiliser pour le champ **IO_WORKSPACE_ID**.

![Curseur + Commerce](./images/cursorai31.png)

- **IO_CONSUMER_ID**= 133309
- **IO_PROJECT_ID**= 4566206088345586770
- **IO_WORKSPACE_ID**= 4566206088345619105

Copiez ces valeurs et collez-les en regard des variables ci-dessous dans le fichier **.env** sur les lignes 42 à 44.

![Curseur + Commerce](./images/cursorai32.png)

### EVENT_PREFIX

Pour le champ **EVENT_PREFIX =**, saisissez la valeur `--aepUserLdap--_` ligne 47 dans le fichier **.env**.

Vous devriez ensuite l’avoir dans le fichier **.env**.

![Curseur + Commerce](./images/cursorai33.png)

### Webhook

Pour le champ **ORDER_WEBHOOK_URL**, collez l’URL du webhook que vous avez créé précédemment dans cet exercice, qui doit se présenter comme suit : `https://eodts05snjmjz67.m.pipedream.net`.

Vous devriez ensuite l’avoir dans le fichier **.env**.

![Curseur + Commerce](./images/cursorai34.png)

### Informations d’identification App Builder

Vous devez mettre à jour les variables suivantes dans le fichier **.env** sur les lignes 54 à 55 :

- **AIO_RUNTIME_NAMESPACE**=
- **AIO_RUNTIME_AUTH**=

Vous pouvez récupérer les valeurs de ces variables en revenant à votre projet Adobe I/O. Accédez à la présentation de **Workspace** puis cliquez sur **Tout télécharger**.

![Curseur + Commerce](./images/cursorai35.png)

Un fichier comme celui-ci sera ensuite téléchargé. Ouvrez ce fichier à l’aide d’un éditeur de texte.

![Curseur + Commerce](./images/cursorai36.png)

Faites défiler vers la droite jusqu’à afficher **runtime**. Vous devriez alors voir le champ **name**, qui contient la valeur de **AIO_RUNTIME_NAMESPACE**.

![Curseur + Commerce](./images/cursorai37.png)

Faites défiler l’écran vers la droite jusqu’à afficher **auth**, qui contient la valeur de **AIO_RUNTIME_AUTH**.

![Curseur + Commerce](./images/cursorai38.png)

Collez les deux valeurs dans le fichier **.env** sur les lignes 54 à 55, vous devriez alors disposer de ceci.

![Curseur + Commerce](./images/cursorai39.png)

Votre fichier **.env** est maintenant complètement configuré.

## 1.7.2.5 workspace.json

À l’étape précédente, vous avez téléchargé un fichier comme celui-ci à partir de votre projet Adobe I/O.

![Curseur + Commerce](./images/cursorai36.png)

Renommez ce fichier et utilisez le nom `workspace.json`.

![Curseur + Commerce](./images/cursorai40.png)

Copiez le fichier dans le répertoire **scripts**>**intégration**>**config**.

![Curseur + Commerce](./images/cursorai41.png)

## 1.7.2.6 la connexion à Adobe I/O

Revenez à la fenêtre de terminal que vous avez utilisée auparavant. Saisissez la `aio login` de commande.

![Curseur + Commerce](./images/cursorai44.png)

Vous devriez alors voir ceci après vous être connecté via votre navigateur.

![Curseur + Commerce](./images/cursorai45.png)

## 1.7.2.7 Prêt pour le déploiement

Copiez l&#39;invite suivante et collez-la dans Cursor. Cliquez ensuite sur le bouton **envoyer**.

`Please deploy this code to Adobe I/O`

![Curseur + Commerce](./images/cursorai42.png)

Cliquez sur **Exécuter** pour autoriser l&#39;action. Le curseur peut vous demander plusieurs fois de confirmer une action.

![Curseur + Commerce](./images/cursorai43.png)

Le déploiement se terminera alors au bout de quelques minutes.

![Curseur + Commerce](./images/cursorai46.png)

Copiez l&#39;invite suivante et collez-la dans Cursor. Cliquez ensuite sur le bouton **envoyer**.

`run the onboarding to commerce`

![Curseur + Commerce](./images/cursorai50.png)

Au bout de quelques minutes, vous devriez voir ceci.

![Curseur + Commerce](./images/cursorai51.png)

Copiez l&#39;invite suivante et collez-la dans Cursor. Cliquez ensuite sur le bouton **envoyer**.

`subscribe to commerce events`

![Curseur + Commerce](./images/cursorai47.png)

Au bout de quelques minutes, vous devriez voir ceci.

![Curseur + Commerce](./images/cursorai49.png)

## 1.7.2.8 Vérifier la configuration dans Adobe Commerce as a Cloud Service

Accédez à [https://experience.adobe.com](https://experience.adobe.com?lang=fr). Cliquez sur **Commerce**.

![Curseur + Commerce](./images/cursorai60.png)

Cliquez sur votre environnement Adobe Commerce as a Cloud Service pour l’ouvrir, puis connectez-vous.

![Curseur + Commerce](./images/cursorai61.png)

Accédez à **Système** puis à **Abonnements aux événements**.

![Curseur + Commerce](./images/cursorai62.png)

Vous devriez alors voir cette liste d’abonnements aux événements.

![Curseur + Commerce](./images/cursorai63.png)

Accédez à **Magasins** puis à **Configuration**.

![Curseur + Commerce](./images/cursorai64.png)

Accédez à **Services Adobe** et sélectionnez **Adobe I/O Events**. Vous devriez alors constater que le champ **Configuration d’Adobe I/O Workspace** comporte une valeur de quelques astérisques et que le champ **Identifiant du commerçant** doit également comporter une valeur telle que `--aepUserLdap--_commerce_events`.

![Curseur + Commerce](./images/cursorai65.png)

Une fois cette configuration en place, vous pouvez la tester.

## 1.7.2.9 Tester votre scénario

Ouvrez votre site web.

![Curseur + Commerce](./images/cursorai101.png)

Accédez à **Montres** et cliquez sur n&#39;importe quel produit.

![Curseur + Commerce](./images/cursorai102.png)

Configurez le produit et cliquez sur **Ajouter au panier**.

![Curseur + Commerce](./images/cursorai103.png)

Cliquez sur l’icône **Panier** et sélectionnez **Extraire**.

![Curseur + Commerce](./images/cursorai104.png)

Renseignez vos informations et cliquez sur **Passer une commande**.

![Curseur + Commerce](./images/cursorai105.png)

Vous devriez alors voir une confirmation de commande.

![Curseur + Commerce](./images/cursorai106.png)

Basculez vers votre application webhook. Vous devriez maintenant voir un événement entrant pour la commande qui vient d’être confirmée.

![Curseur + Commerce](./images/cursorai107.png)

## 1.7.2.10 du débogage d’Adobe I/O

Revenez à votre projet Adobe I/O. Accédez à la présentation de **Workspace**. Vous devriez voir quelque chose de similaire à ceci. Faites défiler l’écran vers le bas.

![Curseur + Commerce](./images/cursorai108.png)

Cliquez pour ouvrir **Commerce Order Sync**.

![Curseur + Commerce](./images/cursorai109.png)

Accédez à **Déboguer le suivi**. Vous y trouverez les derniers événements entrants, ainsi que leur payload. Cela permet de comprendre les événements qui ont été traités et s’ils l’ont été avec succès.

![Curseur + Commerce](./images/cursorai110.png)

## Étapes suivantes

Revenez à [&#x200B; Outils de développement intelligents pour Adobe Commerce &#x200B;](./aiassisteddev.md){target="_blank"}

[Revenir à tous les modules](./../../../overview.md){target="_blank"}
