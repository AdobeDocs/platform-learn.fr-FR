---
title: Création de votre premier formulaire
description: Création de votre premier formulaire
kt: 5342
doc-type: tutorial
source-git-commit: 9aad8cb1fdfa739d1660bc25376b874fa8ed8c89
workflow-type: tm+mt
source-wordcount: '1109'
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

## Exigences en matière d’environnement 1.3.1.1 pour l’utilisation d’AEM Forms avec Edge Delivery Services

Avant de configurer votre premier formulaire, plusieurs exigences doivent être remplies avant de pouvoir suivre les étapes ci-dessous.

### Configuration du programme

Dans la section **Solutions et modules complémentaires** de votre programme Cloud Manager, **Forms** doit être activé.

![AEM Forms](./images/program.png)

### blocs

Dans votre référentiel Github, les blocs suivants doivent être disponibles :

- **formulaire**
- **embed-adaptive-form**

![AEM Forms](./images/block.png)

### scripts

Les scripts suivants doivent être disponibles dans votre référentiel Github :

- **form-editor-support.css**
- **form-editor-support.js**

![AEM Forms](./images/scripts1.png)

En outre, dans le fichier **editor-support.js**, les modifications suivantes doivent être apportées pour activer la modification des formulaires dans l’éditeur universel.

- remplacez la déclaration de fonction **function attachmentEventListners(main)** par **async function attachmentEventListners(main)**
- ajouter les lignes 152 et 153 :

```
const module = await import('./form-editor-support.js');
module.attachEventListners(main);
```

![AEM Forms](./images/scripts2.png)

En outre, dans le fichier **editor-support.js**, modifiez les lignes 90 à 92 comme suit :

```
if (block.dataset.aueModel === 'form') {
        return true;
      } else if (newBlock) {
```

![AEM Forms](./images/scripts3.png)

### paths.json

Vérifiez la configuration de votre référentiel Github, en particulier dans le fichier **paths.json**. Ces lignes doivent être présentes dans le fichier :

- Sous les mappages : **« /content/forms/af/:/forms/ »**
- Sous inclut : **« /content/forms/af/ »**

```json
{
  "mappings": [
    "/content/CitiSignal/:/",
    "/content/CitiSignal/configuration:/.helix/config.json",
    "/content/CitiSignal/headers:/.helix/headers.json",
    "/content/CitiSignal/metadata:/metadata.json",
    "/content/CitiSignal.resource/enrichment/enrichment.json:/enrichment/enrichment.json",
    "/content/forms/af/:/forms/"
  ],
  "includes": [
    "/content/CitiSignal/",
    "/content/forms/af/"
  ]
}
```

![AEM Forms](./images/paths.png)

Une fois ces exigences en place, vous pouvez créer votre premier formulaire.

## 1.3.1.1 Créer un formulaire

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

Après avoir publié votre formulaire, il est désormais également disponible sur votre domaine Edge Delivery Services, qui ressemble à ceci :

`https://main--techinsidersXX-citisignal-aem-accs--woutervangeluwe.aem.page/forms/fiber-max-interest-form`

![AEM Forms](./images/aemforms29.png)

## 1.3.1.2 Envoyer le formulaire

Pour envoyer votre formulaire, 2 éléments sont requis :

- un bouton **Envoyer**
- une action **Envoyer**

En outre, dans cet exercice, vous devez utiliser une feuille de calcul Google pour enregistrer les envois de ce formulaire.

### feuille de calcul Google

Accédez à [https://drive.google.com](https://drive.google.com) puis créez une nouvelle feuille de calcul vierge.

![AEM Forms](./images/sheet1.png)

Nommez votre fichier `citisignal-fiber-max-interest`.

À la ligne 1, dans les cellules A-B-C-D, entrez les noms de champ suivants :

- prénom
- nom
- E-mail
- ville

Cliquez ensuite sur **Partager**.

![AEM Forms](./images/sheet2.png)

Partagez le fichier avec **forms@adobe.com** avec des droits d’accès de niveau **Éditeur**.

Cliquez ensuite sur **Copier le lien**.

Cliquez sur **Envoyer**.

![AEM Forms](./images/sheet3.png)

Vous devrez utiliser le lien copié à l’étape suivante.

### Bouton Envoyer

Pour configurer le bouton **Envoyer**, accédez à **Arborescence de contenu**, sélectionnez **Formulaire adaptatif**, cliquez sur l’icône **+**, puis sélectionnez **Envoyer**.

![AEM Forms](./images/aemforms30.png)

Vous devriez alors voir ceci.

![AEM Forms](./images/aemforms31.png)

### Action Envoyer

Les actions Envoyer font partie d’une extension de l’éditeur universel.

>[!NOTE]
>
>Si l’icône **Modifier les propriétés du formulaire** ne s’affiche pas, cela signifie que cette extension n’est pas encore activée pour votre environnement. Pour activer cette extension, accédez à [https://experience.adobe.com/#/aem/extension-manager](https://experience.adobe.com/#/aem/extension-manager) puis activez l’extension **Modifier les propriétés du formulaire**.
>
>![AEM Forms](./images/extmgr.png)

Cliquez sur l’icône **Modifier les propriétés du formulaire**.

![AEM Forms](./images/aemforms32.png)

Sélectionnez **Envoyer à la feuille de calcul**. Collez l’URL de la feuille de Google que vous avez créée précédemment.

Cliquez sur **Enregistrer et fermer**.

![AEM Forms](./images/aemforms33.png)

>[!NOTE]
>
>Si vous recevez une erreur 401 - Non autorisé, il se peut qu’elle s’affiche. parce que votre environnement n’a pas été activé pour fonctionner avec Google Sheets. Contactez votre représentant Adobe pour que votre environnement soit activé.

Cliquez sur **Publier**.

![AEM Forms](./images/aemforms34.png)

Cliquez de nouveau sur **Publier**.

![AEM Forms](./images/aemforms35.png)

Vous pouvez ensuite actualiser votre site, remplir les formulaires et cliquer sur **Envoyer**.

![AEM Forms](./images/aemforms36.png)

Votre envoi doit alors être réussi.

![AEM Forms](./images/aemforms37.png)

Si vous jetez ensuite un coup d’œil à votre feuille de Google, vous y verrez également l’envoi réussi.

![AEM Forms](./images/aemforms38.png)

Cet exercice est maintenant terminé.

## Étapes suivantes

Revenir à [Adobe Experience Manager Forms avec Edge Delivery Services](./aemforms.md){target="_blank"}

[Revenir à tous les modules](./../../../overview.md){target="_blank"}
