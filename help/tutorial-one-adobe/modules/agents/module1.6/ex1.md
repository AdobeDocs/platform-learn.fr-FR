---
title: Prise en main des agents AEM
description: Prise en main des agents AEM
kt: 5342
doc-type: tutorial
exl-id: cb1bf6f0-f329-4e38-ba64-36ffdc3b8bd4
source-git-commit: d2b746d50ec559e0b29a7adb27c3521b0e00d386
workflow-type: tm+mt
source-wordcount: '1682'
ht-degree: 1%

---

# 1.6.1 Prise en main des agents AEM

>[!IMPORTANT]
>
>Pour réaliser cet exercice, vous devez avoir accès à un environnement AEM Sites et Assets CS avec services de développement intégré (EDS) fonctionnel, et les différents agents AEM doivent être activés pour l’organisation IMS que vous utilisez.
>
>Si vous ne disposez pas encore d’un tel environnement, passez à l’exercice [Adobe Experience Manager Cloud Service &amp; Edge Delivery Services](./../../../modules/asset-mgmt/module2.1/aemcs.md){target="_blank"}. Suivez les instructions qui s’affichent à cet endroit et vous aurez accès à un tel environnement.

>[!IMPORTANT]
>
>Si vous avez précédemment configuré un programme AEM CS avec un environnement AEM Sites et Assets CS, il se peut que votre sandbox AEM CS ait été mis en veille. Étant donné que la réactivation d’un tel sandbox prend entre 10 et 15 minutes, il serait judicieux de lancer le processus de réactivation maintenant afin de ne pas avoir à l’attendre plus tard.

## 1.6.1.1 Discovery Agent

L’agent de découverte Adobe Experience Manager (AEM) est un outil optimisé par l’IA d’AEM as a Cloud Service qui permet aux utilisateurs et utilisatrices de rechercher, de récupérer et d’utiliser du contenu (y compris Assets, des fragments de contenu et la Forms adaptative) à l’aide d’invites en langage naturel. Il n’est plus nécessaire d’effectuer un filtrage manuel, complexe ou basé sur les clics, car il permet de comprendre l’intention et de rechercher dans le référentiel.

Pour utiliser l’**agent de découverte**, vous allez d’abord créer des balises dans Adobe Experience Manager, puis baliser certaines ressources à l’aide de ces balises. Une fois cette opération terminée, vous pourrez utiliser l’assistant d’IA pour découvrir des ressources de manière simple et conviviale pour l’entreprise.

Accédez à [https://my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com){target="_blank"}. L’organisation que vous devez sélectionner est `--aepImsOrgName--`.

### Création et utilisation de balises avec Assets

Cliquez pour ouvrir votre programme Cloud Manager, qui doit être appelé `--aepUserLdap-- - CitiSignal AEM+ACCS`.

![Agents AEM](./images/aemagents1.png)

Cliquez sur l’URL de votre environnement pour l’ouvrir.

![Agents AEM](./images/aemagents2.png)

Cliquez sur l’icône **marteau**.

![Agents AEM](./images/aemagents3.png)

Sous **Général**, cliquez sur **Balisage**.

![Agents AEM](./images/aemagents4.png)

Vous devriez alors voir ceci. Cliquez sur **Créer** puis sélectionnez **Créer un espace de noms**.

![Agents AEM](./images/aemagents5.png)

Dans le champ **Titre**, saisissez : `CitiSignal`. Cliquez sur **Créer**.

![Agents AEM](./images/aemagents6.png)

Accédez à l’espace de noms **CitiSignal** en cliquant dessus. Cliquez sur **Créer** puis sélectionnez **Créer une balise**.

![Agents AEM](./images/aemagents7.png)

Dans le champ **Titre**, saisissez : `Campaign`. Cliquez sur **Envoyer**.

![Agents AEM](./images/aemagents8.png)

Sélectionnez la balise **Campaign** en cliquant dessus. Cliquez sur **Créer** puis sélectionnez **Créer une balise**.

![Agents AEM](./images/aemagents9.png)

Dans le champ **Titre**, saisissez : `Winter 2026`. Cliquez sur **Envoyer**.

![Agents AEM](./images/aemagents10.png)

Sélectionnez la balise **Campaign** en cliquant dessus. Cliquez sur **Créer** puis sélectionnez **Créer une balise**.

![Agents AEM](./images/aemagents11.png)

Dans le champ **Titre**, saisissez : `Spring 2026`. Cliquez sur **Envoyer**.

![Agents AEM](./images/aemagents12.png)

Vous devriez maintenant avoir ceci.

![Agents AEM](./images/aemagents13.png)

Cliquez sur **Adobe Experience Manager** puis sur **Assets**.

![Agents AEM](./images/aemagents14.png)

Cliquez sur **Fichiers**.

![Agents AEM](./images/aemagents15.png)

Double-cliquez sur le dossier **CitiSignal** pour l’ouvrir.

![Agents AEM](./images/aemagents16.png)

Cliquez sur **Créer** puis sélectionnez **Fichiers**.

![Agents AEM](./images/aemagents17.png)

Téléchargez le fichier [citisignal-images-campaign.zip](./assets/citisignal-images-campaign.zip) et décompressez-le sur votre bureau.

![Agents AEM](./images/aemagents17a.png)

Sélectionnez. les 3 fichiers que vous venez de télécharger et cliquez sur **ouvrir**.

![Agents AEM](./images/aemagents18.png)

Cliquez sur **Télécharger**.

![Agents AEM](./images/aemagents19.png)

Vous devriez alors voir ceci.

![Agents AEM](./images/aemagents20.png)

Sélectionnez la première image, puis cliquez sur **Propriétés**.

![Agents AEM](./images/aemagents21.png)

Cliquez sur l’icône **dossier** sous Balises.

![Agents AEM](./images/aemagents22.png)

Sélectionnez la balise **Printemps 2026** puis cliquez sur **Sélectionner**. Répétez ce processus pour ces images :

- citisignal_lion.png
- citisignal_leopard.png
- citisignal_gorilla.png
- citisignal_rabbit.png

![Agents AEM](./images/aemagents23.png)

Une fois la balise sélectionnée pour toutes les images, accédez à **Experience Manager Assets**.

![Agents AEM](./images/aemagents24.png)

Sélectionnez le référentiel que vous utilisez.

![Agents AEM](./images/aemagents25.png)

Accédez à **Assets** puis ouvrez le dossier **CitiSignal**.

![Agents AEM](./images/aemagents26.png)

Ouvrez la première image.

![Agents AEM](./images/aemagents27.png)

Sélectionnez **Approuvé** puis cliquez sur **Enregistrer**.

![Agents AEM](./images/aemagents28.png)

Sous **Balises**, vous pouvez voir la balise que vous avez sélectionnée précédemment.

![Agents AEM](./images/aemagents29.png)

Répétez ce processus afin que les 4 images soient approuvées.

![Agents AEM](./images/aemagents30.png)

Ensuite, accédez à **Mon espace de travail** et cliquez pour ouvrir **Assistant IA**.

![Agents AEM](./images/aemagents31.png)

Saisissez l’invite suivante et cliquez sur **Envoyer**.

```javascript
find all assets tagged with 'Spring 2026'
```

![Agents AEM](./images/aemagents32.png)

Si vous avez accès à plusieurs environnements AEM Assets CS, voici ce que vous verrez. Cliquez sur la réponse proposée pour l’environnement que vous souhaitez utiliser, puis cliquez sur **Envoyer**.

![Agents AEM](./images/aemagents34.png)

Vous devriez alors voir une réponse similaire. Cliquez sur l’icône pour développer l’assistant d’IA en plein écran.

![Agents AEM](./images/aemagents35.png)

Passez en revue les réponses.

![Agents AEM](./images/aemagents36.png)

Dans la fenêtre de l’assistant d’IA, vous pouvez cliquer sur pour afficher l’une de ces ressources.

![Agents AEM](./images/aemagents37.png)

Vous serez ensuite dirigé directement vers AEM Assets CS, vers cette image spécifique.

![Agents AEM](./images/aemagents38.png)

Vous pouvez ensuite également consulter toutes les autres métadonnées disponibles.

![Agents AEM](./images/aemagents39.png)

## Agent de production 1.6.1.2 Experience

### Mise à jour de contenu - Assets

La compétence Mise à jour de contenu permet de mettre à jour facilement le contenu existant, notamment les fragments de contenu, les pages, les formulaires et les ressources. L’agent peut effectuer des actions telles que la mise à jour, la suppression, le remplacement ou l’ajout d’éléments de contenu pour que les expériences restent exactes et à jour. Les entrées peuvent être des descriptions en langage naturel et, lorsqu’elles sont utilisées avec des PDF et des captures d’écran Jira, elles peuvent également fournir des entrées.

Revenez à l’écran de l’assistant d’IA.

![Agents AEM](./images/aemagents40.png)

Saisissez l’invite suivante et cliquez sur **Envoyer**.

`Generate multiple social media formats (Instagram 1080x1920, Facebook 1200x630, Twitter 1200x675) for the third image`

![Agents AEM](./images/aemagents40a.png)

Après quelques minutes, vous devriez voir une réponse similaire.

![Agents AEM](./images/aemagents41.png)

Examinez les images qui ont été générées.

![Agents AEM](./images/aemagents42.png)

### Mise à jour de contenu - Pages

Revenez à votre environnement de création Adobe Experience Manager, puis accédez à **Sites**.

![Agents AEM](./images/aemagents43.png)

Accédez à **CitiSignal**. Cliquez sur **Créer** puis sélectionnez **Page**.

![Agents AEM](./images/aemagents44.png)

Sélectionnez **Page** et cliquez sur **Suivant**.

![Agents AEM](./images/aemagents45.png)

Saisissez les valeurs suivantes :

- Titre : **Fibre max**
- Nom : **fibre-max**
- Titre de la page : **Fibre max**

Cliquez sur **Créer**.

![Agents AEM](./images/aemagents46.png)

Sélectionnez **Ouvrir**.

![Agents AEM](./images/aemagents47.png)

Vous devriez alors voir ceci.

![Agents AEM](./images/aemagents48.png)

Cliquez dans la zone vierge pour sélectionner le composant **section**. Cliquez ensuite sur l’icône plus **+** dans le menu de droite et sélectionnez **Héros**.

![Agents AEM](./images/aemagents49.png)

Vous devriez alors voir ceci. Cliquez sur **+ Ajouter** pour ajouter une image.

![Agents AEM](./images/aemagents50.png)

Sélectionnez votre référentiel de ressources. Ouvrez ensuite le dossier **CitiSignal**.

![Agents AEM](./images/aemagents51.png)

Choisissez l&#39;image du lion que vous avez téléchargé précédemment. Cliquez sur **Sélectionner**.

![Agents AEM](./images/aemagents52.png)

Vous devriez alors voir ceci. Cliquez sur la zone **texte** pour modifier le texte.

![Agents AEM](./images/aemagents53.png)

Collez ce texte dans la zone :

```
This winter, be as fast as a lion.
```

Sélectionnez **Titre 1** puis cliquez sur **Terminé**.

![Agents AEM](./images/aemagents54.png)

Vous devriez alors voir ceci. Accédez à **Arborescence de contenu** et sélectionnez la zone **Section**.

![Agents AEM](./images/aemagents55.png)

Cliquez sur l’icône **+**, puis sélectionnez **Cartes**.

![Agents AEM](./images/aemagents56.png)

Vous devriez alors voir ceci. Assurez-vous que dans l’arborescence **Contenu**, **Cartes** est sélectionné.

Cliquez ensuite 4 fois sur le bouton **+**.

![Agents AEM](./images/aemagents57.png)

Vous devriez maintenant voir ceci, où il y a 4 objets **Card** dans l&#39;objet **Cards**.

![Agents AEM](./images/aemagents58.png)

Sélectionnez la première **Carte**. Cliquez sur la zone **texte** pour modifier le texte.

![Agents AEM](./images/aemagents59.png)

Collez le texte suivant. Vérifiez que la première ligne de texte utilise **Titre 1**. Cliquez sur **Terminé**.

```
99.9% network reliability

Game, video chat and stream on multiple devices with ultra low lag.
```

![Agents AEM](./images/aemagents60.png)

Sélectionnez la deuxième **Carte**. Cliquez sur la zone **texte** pour modifier le texte.

![Agents AEM](./images/aemagents61.png)

Collez le texte suivant. Vérifiez que la première ligne de texte utilise **Titre 1**. Cliquez sur **Terminé**.

```
3-year

price lock guarantee

For new and existing Fiber Max customers on all internet plans.

No hidden fees.
```

![Agents AEM](./images/aemagents62.png)

Sélectionnez la troisième **Carte**. Cliquez sur la zone **texte** pour modifier le texte.

![Agents AEM](./images/aemagents63.png)

Collez le texte suivant. Vérifiez que la première ligne de texte utilise **Titre 1**. Cliquez sur **Terminé**.

```
More ways to save

Save over 45% on the best entertainment with CitiSignal
```

![Agents AEM](./images/aemagents64.png)

Sélectionnez la quatrième **Carte**. Cliquez sur la zone **texte** pour modifier le texte.

![Agents AEM](./images/aemagents65.png)

Collez le texte suivant. Vérifiez que la première ligne de texte utilise **Titre 1**. Cliquez sur **Terminé**.

```
Get Fiber Max now!

Fill out the form here to get started.
```

![Agents AEM](./images/aemagents66.png)

Vous devriez maintenant avoir ceci. Cliquez sur **Publier**.

![Agents AEM](./images/aemagents67.png)

Cliquez de nouveau sur **Publier**.

![Agents AEM](./images/aemagents68.png)

Cliquez sur **Ouvrir la page**.

![Agents AEM](./images/aemagents69.png)

Copiez l’URL de la page comme vous en aurez besoin ensuite.

L’URL doit être similaire à ceci : `https://author-pXXXXXX-eXXXXXXX.adobeaemcloud.com/content/CitiSignal/fiber-max.html`.

![Agents AEM](./images/aemagents70.png)

Accédez à [https://experience.adobe.com/#/experiencemanager/](https://experience.adobe.com/#/experiencemanager/). Cliquez pour ouvrir **Assistant IA**.

![Agents AEM](./images/aemagents71.png)

Collez l’invite suivante et cliquez sur **envoyer**. Remplacez XXX dans cette invite par l’URL que vous avez copiée à l’étape précédente.

```
On the page XXX, please make the following changes:

- change the word 'winter' to 'spring'
- change the word 'lion' to 'leopard'
- change the image in the hero block to use the image 'citisignal_leopard.png'
- change the text '99.9% network reliability' to '99.999% network reliability'
```

![Agents AEM](./images/aemagents72.png)

Après 1-2 minutes, vous devriez voir ceci. Saisissez le `generate` d’invite et cliquez sur **Envoyer**.

![Agents AEM](./images/aemagents74.png)

Quelques minutes plus tard, une confirmation comme celle-ci devrait s’afficher indiquant que les modifications ont été effectuées. Cliquez sur **Prévisualiser la page mise à jour**.

![Agents AEM](./images/aemagents75.png)

Vous obtenez maintenant une confirmation visuelle des modifications qui ont été apportées. Cette page d’aperçu est fournie uniquement à titre d’information. Vous ne pouvez pas agir à partir de cette page.

![Agents AEM](./images/aemagents76.png)

Pour agir, cliquez sur **Modifier dans AEM**.

![Agents AEM](./images/aemagents75a.png)

Dans l’éditeur universel, vous voyez désormais toutes les modifications en détail, avec la possibilité de tout modifier. Une fois la page vérifiée, cliquez sur **Publier**.

![Agents AEM](./images/aemagents77.png)

Cliquez de nouveau sur **Publier**. La modification que vous avez apportée n’a pas encore été publiée dans votre environnement de production. Au lieu de cela, il a été publié sous **Lancements** dans AEM.

Les lancements vous permettent de développer efficacement du contenu en vue d’une publication ultérieure. Un lancement est créé pour vous permettre d’apporter des modifications en vue d’une publication ultérieure, tout en conservant vos pages actives. Cela signifie que vous modifiez deux versions simultanément : les pages qui sont actuellement publiées et une version de ces pages, qui sera publiée à un moment donné dans le futur. Une fois ce délai écoulé, vous pouvez remplacer les pages d’origine et publier la nouvelle version.

![Agents AEM](./images/aemagents78.png)

Pour **Promouvoir** vos modifications en attente pour une version ultérieure, revenez à AEM. Cliquez sur **Adobe Experience Manager** en haut de la page, cliquez sur l’icône **marteau**, puis sélectionnez **Lancements**.

![Agents AEM](./images/aemagents79.png)

Un **Launch** en attente devrait maintenant s’afficher. Cochez la case en regard de l’**Launch** en attente.

![Agents AEM](./images/aemagents80.png)

Cliquez sur **Promouvoir**.

![Agents AEM](./images/aemagents81.png)

Sélectionnez **Promouvoir le lancement complet** et cliquez sur **Suivant**.

![Agents AEM](./images/aemagents82.png)

Cliquez sur **Promouvoir**.

![Agents AEM](./images/aemagents83.png)

Vous devriez maintenant voir ceci. Vos modifications sont en cours de production.

![Agents AEM](./images/aemagents84.png)

Actualisez votre page. Toutes vos modifications devraient maintenant s’afficher sur la page publiée.

![Agents AEM](./images/aemagents85.png)

Au lieu de suivre le processus de promotion manuel, vous pouvez également saisir le `accept` d’invite dans l’assistant AI.

![Agents AEM](./images/aemagents86.png)

Vous devriez ensuite obtenir une confirmation que les modifications sont publiées.

![Agents AEM](./images/aemagents87.png)

### Mise à jour de contenu - Création de formulaire

Dans le module [Adobe Experience Manager Forms avec Edge Delivery Services](./../../asset-mgmt/module1.3/aemforms.md){target="_blank"} vous trouverez les étapes de création d&#39;un formulaire de manière manuelle.

La compétence Création de formulaire permet désormais aux utilisateurs et utilisatrices de créer des formulaires adaptatifs par le biais d’invites de langage naturel sans dépendre du développement ou des équipes informatiques. Cette fonctionnalité accélère le développement des formulaires tout en maintenant la cohérence de la marque et en permettant aux utilisateurs professionnels de créer des formulaires sans avoir une connaissance technique approfondie des produits.

Accédez à [https://experience.adobe.com/#/ai-assistant/chat](https://experience.adobe.com/#/ai-assistant/chat).

![Agents AEM](./images/aemagentsforms1.png)

Saisissez l’invite suivante et cliquez sur **envoyer**.

```
Create a new adaptive form using Edge Delivery Services and the existing CitiSignal site, with the following details:
- Form name: "citisignal-fiber-max-interest-2"
- Form fields: 4 text input fields are needed, for "first-name", "last-name", "email" and "city"
- When the form is submitted, send the submission to a spreadsheet, with this URL: https://docs.google.com/spreadsheets/d/1WwKrcM8mZ2d_W3sMheUAw3nFhP_OFk05TsqxhHkudfQ/edit?usp=sharing.
```

## Étapes suivantes

Accédez à [1.6.2 Serveurs et curseur AEM MCP](./ex2.md){target="_blank"}

Revenir à [AEM et agents](./aemagents.md){target="_blank"}

[Revenir à tous les modules](./../../../overview.md){target="_blank"}
