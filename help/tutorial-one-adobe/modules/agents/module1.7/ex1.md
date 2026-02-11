---
title: Configuration de votre environnement de développement
description: Configuration de votre environnement de développement
kt: 5342
doc-type: tutorial
exl-id: c9bfb327-362f-4475-89da-8e9788940d56
source-git-commit: ce3ee3dde103383a6f7897cba36d548058879ea7
workflow-type: tm+mt
source-wordcount: '640'
ht-degree: 5%

---

# 1.7.1 Configuration de votre environnement de développement

## 1.7.1.1 Créer votre projet Adobe I/O

Accédez à [https://developer.adobe.com/console/home](https://developer.adobe.com/console/home){target="_blank"}.

Veillez à sélectionner l’instance appropriée dans le coin supérieur droit de l’écran. Votre instance est `--aepImsOrgName--`.

>[!NOTE]
>
> La capture d’écran ci-dessous montre une organisation spécifique sélectionnée. Lorsque vous parcourez ce tutoriel, il est très probable que votre organisation porte un nom différent. Lorsque vous vous êtes inscrit à ce tutoriel, les détails de l’environnement à utiliser vous ont été fournis. Veuillez suivre ces instructions.

Sélectionnez ensuite **Créer un projet à partir d’un modèle**.

![Extensibilité GSPeM](./images/commerceagent1.png)

Sélectionnez **App Builder**.

![Extensibilité GSPeM](./images/commerceagent2.png)

Saisissez le nom `--aepUserLdap-- vangeluw Commerce Events`. Cliquez sur **Enregistrer**.

![Extensibilité GSPeM](./images/commerceagent4.png)

Vous devriez alors voir quelque chose comme ça.

![Extensibilité GSPeM](./images/commerceagent5.png)

Cliquez sur **+ Ajouter un service** puis sélectionnez **API**.

![Extensibilité GSPeM](./images/commerceagent6.png)

Recherchez et sélectionnez l’API **Événements I/O**. Cliquez sur **Suivant**.

![Extensibilité GSPeM](./images/commerceagent7.png)

Remplacez le nom des informations d’identification par `vangeluw Commerce Events - Production`. Cliquez sur **Enregistrer l’API configurée**.

![Extensibilité GSPeM](./images/commerceagent8.png)

Vous devriez alors voir ceci. Cliquez sur **+ Ajouter un service** puis sélectionnez **API**.

![Extensibilité GSPeM](./images/commerceagent9.png)

Recherchez et sélectionnez l’API **I/O Management API**. Cliquez sur **Suivant**.

![Extensibilité GSPeM](./images/commerceagent10.png)

Cliquez sur **Enregistrer l’API configurée**.

![Extensibilité GSPeM](./images/commerceagent11.png)

Vous devriez alors voir ceci. Cliquez sur **+ Ajouter un service** puis sélectionnez **API**.

![Extensibilité GSPeM](./images/commerceagent12.png)

Recherchez et sélectionnez l’API **Adobe Commerce as a Cloud Service**. Cliquez sur **Suivant**.

![Extensibilité GSPeM](./images/commerceagent13.png)

Sélectionnez **Authentification de serveur à serveur**. Cliquez sur **Suivant**.

![Extensibilité GSPeM](./images/commerceagent14.png)

Cliquez sur **Suivant**.

![Extensibilité GSPeM](./images/commerceagent15.png)

Sélectionnez **Par défaut - Cloud Manager**. Cliquez sur **Enregistrer l’API configurée**.

![Extensibilité GSPeM](./images/commerceagent16.png)

Vous devriez alors voir ceci. Cliquez sur **+ Ajouter un service** puis sélectionnez **API**.

![Extensibilité GSPeM](./images/commerceagent17.png)

Recherchez et sélectionnez l’API **Adobe I/O Events pour Adobe Commerce**. Cliquez sur **Suivant**.

![Extensibilité GSPeM](./images/commerceagent18.png)

Cliquez sur **Enregistrer l’API configurée**.

![Extensibilité GSPeM](./images/commerceagent19.png)

Votre projet est maintenant configuré et peut être utilisé.

![Extensibilité GSPeM](./images/commerceagent20.png)

## 1.7.1.2 Configurer votre environnement de développement

Pour créer, envoyer et déployer votre application extensible, les applications et packages suivants doivent être installés dans votre environnement de développement local sur votre ordinateur :

- Node.js (version 20.x ou ultérieure)
- npm (package avec Node.js)
- Interface de ligne de commande (CLI) Adobe Developer

Si ces applications ou packages ne sont pas encore installés sur votre ordinateur, procédez comme suit.

### Node.js et npm

Accédez à [https://nodejs.org/en/download](https://nodejs.org/en/download). Vous devriez alors le voir, avec un certain nombre de commandes de terminal qui doivent être exécutées pour que Node.js et npm soient installés. Les commandes présentées ici s&#39;appliquent à MacBook.

![Extensibilité GSPeM](./images/commerceagent21.png)

Tout d’abord, ouvrez une nouvelle fenêtre de terminal. Collez et exécutez la commande mentionnée à la ligne 2 de la capture d’écran :

`curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.40.3/install.sh | bash`

Exécutez ensuite la commande à la ligne 5 de la capture d’écran :

`\. "$HOME/.nvm/nvm.sh"`

Après avoir exécuté les deux commandes avec succès, exécutez cette commande :

`node -v`

Vous devriez voir un numéro de version renvoyé.

![Extensibilité GSPeM](./images/commerceagent22.png)

Exécutez ensuite la commande suivante :

`npm -v`

Si NPM n’est pas encore installé, vous pouvez l’installer à l’aide de la commande suivante : `npm install -g npm@11.9.0`.

Vous devriez voir un numéro de version renvoyé.

![Extensibilité GSPeM](./images/commerceagent23.png)

Si les 2 dernières commandes ont renvoyé un numéro de version, votre configuration de ces 2 fonctionnalités est réussie.

### Interface de ligne de commande (CLI) Adobe Developer

Pour installer l’interface de ligne de commande (CLI) d’Adobe Developer, exécutez la commande suivante dans une fenêtre de terminal :

`npm install -g @adobe/aio-cli`

L’exécution de cette commande peut prendre quelques minutes, le résultat final devrait être similaire à ceci :

![Extensibilité GSPeM](./images/commerceagent24.png)

L’interface de ligne de commande (CLI) d’Adobe Developer est désormais installée avec succès.

### Extension SDK de l’interface de ligne de commande (CLI) Adobe Developer pour Commerce

Pour installer l’extension Adobe I/O SDK pour Commerce, exécutez la commande suivante dans une fenêtre de terminal :

`npm install @adobe/aio-commerce-sdk`

![Extensibilité GSPeM](./images/commerceagent25.png)

### Plug-ins Adobe Commerce pour l’interface de ligne de commande Adobe I/O

Pour installer les modules externes Adobe Commerce pour l’interface de ligne de commande Adobe I/O, exécutez la commande suivante dans une fenêtre de terminal :

`aio plugins:install https://github.com/adobe-commerce/aio-cli-plugin-commerce @adobe/aio-cli-plugin-app-dev @adobe/aio-cli-plugin-runtime`

![Extensibilité GSPeM](./images/commerceagent26.png)

Vous avez maintenant configuré les éléments de base pour pouvoir exécuter un projet App Builder, en combinaison avec Adobe Commerce, Adobe I/O Events et Adobe I/O Runtime.

## Étapes suivantes

Accédez à [Utiliser Cursor.ai pour développer votre projet](./ex2.md){target="_blank"}

Revenez à [Outils de développement intelligents pour Adobe Commerce](./aiassisteddev.md){target="_blank"}

[Revenir à tous les modules](./../../../overview.md){target="_blank"}
