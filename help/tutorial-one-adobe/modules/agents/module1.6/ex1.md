---
title: Content Production Agent
description: Content Production Agent
kt: 5342
doc-type: tutorial
exl-id: cb1bf6f0-f329-4e38-ba64-36ffdc3b8bd4
source-git-commit: 7ea3bdc9557ea9e88ddd9693f9ffbfbc634857f8
workflow-type: tm+mt
source-wordcount: '859'
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

### Mise à jour du contenu

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

### Création de formulaire

La compétence Création de formulaire permet aux utilisateurs de créer des formulaires adaptatifs à l’aide d’invites de langage naturel sans dépendre du développement ou des équipes informatiques. Cette fonctionnalité accélère le développement des formulaires tout en maintenant la cohérence de la marque et en permettant aux utilisateurs professionnels de créer des formulaires sans avoir une connaissance technique approfondie des produits.


## Étapes suivantes

Revenir à [AEM et agents](./aemagents.md){target="_blank"}

[Revenir à tous les modules](./../../../overview.md){target="_blank"}
