---
title: Utiliser Cursor.ai pour développer votre projet
description: Utiliser Cursor.ai pour développer votre projet
kt: 5342
doc-type: tutorial
source-git-commit: 2bfa7f4bee54df8411c96b001224d2986e9fcaf9
workflow-type: tm+mt
source-wordcount: '419'
ht-degree: 0%

---

# 1.7.2 Utiliser Cursor.ai pour développer votre projet

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

Vous devez ensuite configurer les outils d’extensibilité de Commerce pour Cursor.ai. Saisissez la commande suivante, puis exécutez-la.

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

En installant les outils d’extensibilité de Commerce pour Cursor.ai, vous disposez désormais d’un serveur MCP dans le cadre de votre environnement Cursor.ai. Dans les exercices suivants, vous utiliserez ce serveur MCP pour vous aider à développer et déployer le projet App Builder.

## 1.7.2.2 Configurer le webhook

Pour cet exercice, vous avez besoin d’un webhook qui doit être configuré afin que, lorsqu’une commande est créée, l’événement order puisse être diffusé en continu vers ce webhook. Dans cet exercice, vous allez utiliser un exemple de point d’entrée à l’aide de [https://pipedream.com/requestbin](https://pipedream.com/requestbin).

Accédez à [https://pipedream.com/requestbin](https://pipedream.com/requestbin), créez un compte, puis un espace de travail. Une fois l’espace de travail créé, un élément similaire s’affiche.

Cliquez sur **copier** pour copier l’URL. Vous devrez spécifier cette URL dans l’exercice suivant. Dans cet exemple, l’URL est `https://eodts05snjmjz67.m.pipedream.net`.

![Cursor.ai + Commerce](./images/webhook1.png)

## 1.7.2.3 Cursor.ai

Ouvrez Cursor.ai. Cliquez sur **Ouvrir le projet**.

![Cursor.ai + Commerce](./images/cursorai14.png)

Accédez au dossier que vous avez créé, qui doit être nommé `--aepUserLdap---commerce`. Dans ce dossier, sélectionnez le dossier nommé `commerce-integration-starter-kit`. Cliquez sur **Ouvrir**.

![Cursor.ai + Commerce](./images/cursorai15.png)

Vous devriez alors voir ceci. Avant de poursuivre, assurez-vous que le dossier de niveau supérieur ouvert dans Cursor.ai est `commerce-integration-starter-kit`.

![Cursor.ai + Commerce](./images/cursorai16.png)

`I would like to build an app that subscribes to order created events and sends them to a configurable URL with basic authentication`

## Étapes suivantes

Revenez à [&#x200B; Outils de développement intelligents pour Adobe Commerce &#x200B;](./aiassisteddev.md){target="_blank"}

[Revenir à tous les modules](./../../../overview.md){target="_blank"}