---
title: Création de votre premier formulaire
description: Création de votre premier formulaire
kt: 5342
doc-type: tutorial
source-git-commit: 8f59b9fdadc9c5aeadb1d4ecccd75090c339b43e
workflow-type: tm+mt
source-wordcount: '608'
ht-degree: 10%

---

# 1.3.1 Créer votre premier formulaire

>[!IMPORTANT]
>
>Pour effectuer cet exercice, vous devez avoir accès à un environnement de création AEM Assets CS fonctionnel dans lequel AEM Assets Dynamic Media est activé.
>
>Si vous ne disposez pas d’un tel environnement, accédez à [Adobe Experience Manager Cloud Service &amp; Edge Delivery Services](./../../../modules/asset-mgmt/module2.1/aemcs.md){target="_blank"}. Suivez les instructions qui s’affichent à cet endroit et vous aurez accès à un tel environnement.

>[!IMPORTANT]
>
>Si vous avez précédemment configuré un programme AEM CS avec un environnement AEM Assets CS, il se peut que votre sandbox AEM CS ait été mis en veille. Étant donné que la réactivation d’un tel sandbox prend entre 10 et 15 minutes, il serait judicieux de lancer le processus de réactivation maintenant afin de ne pas avoir à l’attendre plus tard.

## 1.3.1.1 -

Accédez à [https://my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com){target="_blank"}. L’organisation que vous devez sélectionner est `--aepImsOrgName--`. Ouvrez votre environnement.

![AEM Forms](./images/aemforms1.png)

Accédez à **Forms**.

![AEM Forms](./images/aemforms2.png)

Accédez à **Forms et documents**.

![AEM Forms](./images/aemforms3.png)

Cliquez sur **Créer** puis sélectionnez **Formulaire adaptatif**.

![AEM Forms](./images/aemforms4.png)

Sélectionnez **Edge Delivery Services** puis sélectionnez **Page vierge**. Cliquez sur **Créer**.

![AEM Forms](./images/aemforms5.png)

Vous devriez alors voir ceci. Renseignez les champs suivants :

- **Titre** : `Fiber Max Interest Form`
- **Nom** : doit être renseigné automatiquement en fonction du champ **Titre**.
- **URL Github** : indiquez le chemin d’accès au référentiel Github lié à votre site web

Cliquez sur **Créer**.

![AEM Forms](./images/aemforms6.png)

Après avoir cliqué sur **Créer**, l’**éditeur universel** doit s’ouvrir automatiquement et un message similaire s’affiche. Cliquez sur l’icône pour ouvrir l’**arborescence de contenu**.

![AEM Forms](./images/aemforms7.png)

Dans l’**Arborescence de contenu**, sélectionnez l’objet **Formulaire adaptatif**.

![AEM Forms](./images/aemforms8.png)

Cliquez ensuite sur l’icône **+** pour ajouter un nouvel élément, puis sélectionnez **Entrée de texte**.

![AEM Forms](./images/aemforms9.png)

Dans l’**Arborescence de contenu**, sélectionnez le champ **Entrée de texte**.

![AEM Forms](./images/aemforms10.png)

Accédez à la vue **De base**. Tu devrais voir ça.

Renseignez les champs suivants :

- **Nom** : `first-name`
- **Titre** : `First Name`

Accédez ensuite à **Validation**.

![AEM Forms](./images/aemforms11.png)

Appuyez sur l’interrupteur pour que ce champ soit obligatoire. Renseignez les champs suivants :

- **Message d’erreur** : `Enter your first name`
- **Modèle** : `[A-Za-z][A-Za-z ]+`
- **Message d’erreur de modèle** : `Letters only!`

![AEM Forms](./images/aemforms12.png)

Dans l’**Arborescence de contenu**, sélectionnez le champ **Formulaire adaptatif**. Cliquez sur l’icône **+**, puis sélectionnez **Entrée de texte**.

![AEM Forms](./images/aemforms13.png)

Dans l’**Arborescence de contenu**, sélectionnez le champ nouvellement créé **Entrée de texte**. Accédez à **Propriétés**.

![AEM Forms](./images/aemforms14.png)

Accédez à la vue **De base**. Tu devrais voir ça.

Renseignez les champs suivants :

- **Nom** : `last-name`
- **Titre** : `Last Name`

Accédez ensuite à **Validation**.

![AEM Forms](./images/aemforms15.png)

Appuyez sur l’interrupteur pour que ce champ soit obligatoire. Renseignez les champs suivants :

- **Message d’erreur** : `Enter your last name`
- **Modèle** : `[A-Za-z][A-Za-z ]+`
- **Message d’erreur de modèle** : `Letters only!`

![AEM Forms](./images/aemforms16.png)

Dans l’**Arborescence de contenu**, sélectionnez le champ **Formulaire adaptatif**. Cliquez sur l’icône **+**, puis sélectionnez **Entrée de texte**.

![AEM Forms](./images/aemforms17.png)

Dans l’**Arborescence de contenu**, sélectionnez le champ nouvellement créé **Entrée de texte**. Accédez à **Propriétés**.

![AEM Forms](./images/aemforms18.png)

Accédez à la vue **De base**. Tu devrais voir ça.

Renseignez les champs suivants :

- **Nom** : `email`
- **Titre** : `Email`

Accédez ensuite à **Validation**.

![AEM Forms](./images/aemforms19.png)

Appuyez sur l’interrupteur pour que ce champ soit obligatoire. Renseignez les champs suivants :

- **Message d’erreur** : `Enter your email address`
- **Modèle** : `^[^@]+@[^@]+\.[^@]+$`
- **Message d’erreur de modèle** : `Please verify your email address!`

![AEM Forms](./images/aemforms20.png)

Dans l’**Arborescence de contenu**, sélectionnez le champ **Formulaire adaptatif**. Cliquez sur l’icône **+**, puis sélectionnez **Entrée de texte**.

![AEM Forms](./images/aemforms21.png)

Dans l’**Arborescence de contenu**, sélectionnez le champ nouvellement créé **Entrée de texte**.

![AEM Forms](./images/aemforms22.png)

Accédez à la vue **De base**. Tu devrais voir ça.

Renseignez les champs suivants :

- **Nom** : `city`
- **Titre** : `city`

Accédez ensuite à **Validation**.

![AEM Forms](./images/aemforms23.png)

Appuyez sur l’interrupteur pour que ce champ soit obligatoire. Renseignez les champs suivants :

- **Message d’erreur** : `Enter your city`
- **Modèle** : `[A-Za-z][A-Za-z ]+`
- **Message d’erreur de modèle** : `Letters only!`

![AEM Forms](./images/aemforms24.png)

Cliquez sur **Publier**.

![AEM Forms](./images/aemforms25.png)

Cliquez de nouveau sur **Publier**.

![AEM Forms](./images/aemforms26.png)

Cliquez pour ouvrir le formulaire.

![AEM Forms](./images/aemforms27.png)

Vous pouvez ensuite remplir le formulaire, mais vous ne pouvez pas encore l’envoyer.

![AEM Forms](./images/aemforms28.png)

## Étapes suivantes

Étape Suivante : [-](./ex1.md){target="_blank"}

Revenir à [Adobe Experience Manager Forms avec Edge Delivery Services](./aemforms.md){target="_blank"}

[Revenir à tous les modules](./../../../overview.md){target="_blank"}
