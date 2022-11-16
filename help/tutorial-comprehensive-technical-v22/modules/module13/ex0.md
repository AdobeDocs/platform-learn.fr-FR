---
title: Activation des segments vers Microsoft Azure Event Hub - Configuration de votre environnement Microsoft Azure
description: Activation des segments vers Microsoft Azure Event Hub - Configuration de votre environnement Microsoft Azure
kt: 5342
audience: Data Engineer, Data Architect, Data Analyst
doc-type: tutorial
activity: develop
exl-id: 79711c1a-674c-4233-9c6c-af3bad6d0e0c
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '478'
ht-degree: 2%

---

# 13.0 Configuration de votre environnement

## 13.0.1 Création d’un abonnement Azure

>[!NOTE]
>
>Si vous disposez déjà d’un abonnement Azure, vous pouvez ignorer cette étape. Poursuivez l’exercice 13.0.2 dans ce cas.

Accédez à [https://portal.azure.com](https://portal.azure.com) et connectez-vous avec votre compte Azure. Si vous n’en avez pas, utilisez votre adresse électronique personnelle pour créer votre compte Azure.

![02-azure-portal-email.png](./images/02-azure-portal-email.png)

Une fois la connexion établie, l’écran suivant s’affiche :

![03-azure-logged-in.png](./images/03-azure-logged-in.png)

Cliquez sur le menu à gauche et sélectionnez **Toutes les ressources**, l’écran d’abonnement Azure s’affiche si vous n’êtes pas encore abonné. Dans ce cas, sélectionnez **Commencer avec une version d’évaluation gratuite d’Azure**.

![04-azure-start-subscribe.png](./images/04-azure-start-subscribe.png)

Remplissez le formulaire d&#39;abonnement Azure, fournissez votre téléphone mobile et votre carte de crédit pour l&#39;activation (vous aurez un tarif réduit pendant 30 jours et vous ne serez pas facturé, sauf si vous effectuez une mise à niveau) :

![05-azure-subscription-form.png](./images/05-azure-subscription-form.png)

Lorsque le processus d’abonnement est terminé, vous pouvez procéder comme suit :

![06-azure-subscription-ok.png](./images/06-azure-subscription-ok.png)


## 13.0.2 Installation de Visual Code Studio

Vous utiliserez Microsoft Visual Code Studio pour gérer votre projet Azure. Vous pouvez le télécharger via [ce lien](https://code.visualstudio.com/download). Suivez les instructions d’installation de votre système d’exploitation spécifique sur ce même site web.

## 13.0.3 Installation des extensions Visual Code

Installation des fonctions Azure pour Visual Studio Code à partir de [https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-azurefunctions](https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-azurefunctions). Cliquez sur le bouton d’installation :

![07-azure-code-extension-install.png](./images/07-azure-code-extension-install.png)

Installez le compte Azure et la connexion à Visual Studio Code à partir de [https://marketplace.visualstudio.com/items?itemName=ms-vscode.azure-account](https://marketplace.visualstudio.com/items?itemName=ms-vscode.azure-account). Cliquez sur le bouton d’installation :

![08-azure-account-extension-install.png](./images/08-azure-account-extension-install.png)

## 13.0.4 Installation de node.js

>[!NOTE]
>
>Si node.js est déjà installé, vous pouvez ignorer cette étape. Poursuivez l’exercice 13.0.5 dans ce cas.

### macOS

Assurez-vous que la variable [Homebrew](https://brew.sh/) installé en premier. Suivez les instructions [here](https://brew.sh/).

![Nœud](./images/brew.png)

Une fois que vous avez installé Homebrew, exécutez la commande suivante :

```javascript
brew install node
```

### Windows

Téléchargez la [Windows Installer](https://nodejs.org/en/#home-downloadhead) directement à partir de [nodejs.org](https://nodejs.org/en/) site web.

## 13.0.5 Vérification de la version de node.js

Pour ce module, la version 12 de node.js doit être installée. Toute autre version de node.js peut entraîner des problèmes avec l’exercice 13.5.

Avant de poursuivre, vérifiez maintenant votre version de node.js.

Exécutez cette commande pour vérifier la version de node.js :

```javascript
node -v
```

Si votre version est inférieure ou supérieure à 12, vous devez effectuer une mise à niveau ou une mise à niveau.

### Mise à niveau/rétrogradation de la version de node.js sur macOS

Assurez-vous que vous disposez du module **n** installé.

Pour installer le package **n**, exécutez la commande suivante :

```javascript
sudo npm install -g n
```

Si votre version est inférieure ou supérieure à la version 12, exécutez cette commande pour mettre à niveau ou rétrograder :

```javascript
sudo n 12.6.0
```

### Mise à niveau/rétrogradation de la version de node.js sous Windows

Désinstallez node.js de Windows > Panneau de Contrôle > Ajouter ou supprimer des programmes.

Installation de la version requise à partir du [nodejs.org](https://nodejs.org/en/) site web.

## 13.0.6 Installer le package NPM : requête

Vous devez installer le package **requête** dans le cadre de la configuration de node.js.

Pour installer le package **requête**, exécutez la commande suivante :

```javascript
npm install request
```


Étape suivante : [13.1 Configuration de votre environnement Microsoft Azure EventHub](./ex1.md)

[Revenir au module 13](./segment-activation-microsoft-azure-eventhub.md)

[Revenir à tous les modules](./../../overview.md)
