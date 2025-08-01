---
title: AEM CS - Bloc personnalisé de base
description: AEM CS - Bloc personnalisé de base
kt: 5342
doc-type: tutorial
exl-id: 57c08a88-d885-471b-ad78-1dba5992da9d
source-git-commit: d583df79bff499b7605f77146d52e66bc02810b9
workflow-type: tm+mt
source-wordcount: '814'
ht-degree: 2%

---

# 1.1.4 Développement d’un bloc personnalisé de base

## 1.1.4.1 Configurer votre environnement de développement local

Accédez à [https://desktop.github.com/download/](https://desktop.github.com/download/){target="_blank"}, téléchargez et installez **Github Desktop**.

![Bloquer](./images/block1.png){zoomable="yes"}

Une fois Github Desktop installé, accédez au référentiel GitHub que vous avez créé dans l’exercice précédent. Cliquez sur **&lt;> Code** puis sur **Ouvrir avec GitHub Desktop**.

![Bloquer](./images/block2.png){zoomable="yes"}

Votre référentiel GitHub sera alors ouvert dans le bureau GitHub. N’hésitez pas à modifier le **Chemin local**. Cliquez sur **Cloner**.

![Bloquer](./images/block3.png){zoomable="yes"}

Un dossier local va maintenant être créé.

![Bloquer](./images/block4.png){zoomable="yes"}

Ouvrez Visual Studio Code. Accédez à **Fichier** > **Ouvrir le dossier**.

![Bloquer](./images/block5.png){zoomable="yes"}

Sélectionnez le dossier utilisé par votre configuration GitHub pour **citisignal**.

![Bloquer](./images/block6.png){zoomable="yes"}

Ce dossier est maintenant ouvert dans Visual Studio Code. Vous êtes maintenant prêt à créer un nouveau bloc.

![Bloquer](./images/block7.png){zoomable="yes"}

## 1.1.4.2 Créer un bloc personnalisé de base

Adobe vous recommande de développer des blocs selon une approche en trois phases :

- Créez la définition et le modèle du bloc, examinez-les et mettez-les en production.
- Créez du contenu avec le nouveau bloc.
- Mettez en œuvre la décoration et les styles pour le nouveau bloc.

### component-definition.json

Dans Visual Studio Code, ouvrez le fichier **component-definition.json**.

![Bloquer](./images/block8.png){zoomable="yes"}

Faites défiler jusqu’à afficher le composant **Citation**. Placez le curseur en regard du crochet fermant du dernier composant.

![Bloquer](./images/block9.png){zoomable="yes"}

Collez ce code et saisissez une virgule **,** après le bloc de code :

```json
{
  "title": "FiberOffer",
  "id": "fiberoffer",
  "plugins": {
    "xwalk": {
      "page": {
        "resourceType": "core/franklin/components/block/v1/block",
        "template": {
          "name": "FiberOffer",
          "model": "fiberoffer",
          "offerText": "<p>Fiber will soon be available in your region!</p>",
          "offerCallToAction": "Get your offer now!",
          "offerImage": ""
        }
      }
    }
  }
}
```

Enregistrez vos modifications.

![Bloquer](./images/block10.png){zoomable="yes"}

### component-models.json

Dans Visual Studio Code, ouvrez le fichier **component-models.json**.

![Bloquer](./images/block11.png){zoomable="yes"}

Faites défiler vers le bas jusqu’à ce que le dernier élément s’affiche. Placez le curseur en regard du crochet fermant du dernier composant.

![Bloquer](./images/block12.png){zoomable="yes"}

Saisissez une virgule **,**, puis appuyez sur Entrée et, sur la ligne suivante, collez ce code :

```json
{
  "id": "fiberoffer",
  "fields": [
     {
       "component": "richtext",
       "name": "offerText",
       "value": "",
       "label": "Offer Text",
       "valueType": "string"
     },
     {
       "component": "richtext",
       "valueType": "string",
       "name": "offerCallToAction",
       "label": "Offer CTA",
       "value": ""
     },
     {
       "component": "reference",
       "valueType": "string",
       "name": "offerImage",
       "label": "Offer Image",
        "multi": false
     }
   ]
}
```

Enregistrez vos modifications.

![Bloquer](./images/block13.png){zoomable="yes"}

### component-filters.json

Dans Visual Studio Code, ouvrez le fichier **component-filters.json**.

![Bloquer](./images/block14.png){zoomable="yes"}

Sous **section**, saisissez une virgule **,** et l’identifiant de votre composant **fiberoffer** après la dernière ligne active.

Enregistrez vos modifications.

![Bloquer](./images/block15.png){zoomable="yes"}

## 1.1.4.3 Valider vos modifications

Vous avez apporté plusieurs modifications à votre projet qui doivent être validées dans votre référentiel GitHub. Pour ce faire, ouvrez **GitHub Desktop**.

Vous devriez alors voir les 3 fichiers que vous venez de modifier sous **Modifications**. Vérifiez vos modifications.

![Bloquer](./images/block16.png){zoomable="yes"}

Saisissez un nom pour votre requête de tirage, `Fiber Offer custom block`. Cliquez sur **Valider dans la ressource principale**.

![Bloquer](./images/block17.png){zoomable="yes"}

Vous devriez alors voir ceci. Cliquez sur **Push origin**.

![Bloquer](./images/block18.png){zoomable="yes"}

Au bout de quelques secondes, vos modifications ont été transmises à votre référentiel GitHub.

![Bloquer](./images/block19.png){zoomable="yes"}

Dans votre navigateur, accédez à votre compte GitHub et au référentiel que vous avez créé pour CitiSignal. Vous devriez ensuite voir un élément similaire, montrant que vos modifications ont été reçues.

![Bloquer](./images/block20.png){zoomable="yes"}

## 1.1.4.4 Ajouter votre bloc à une page

Maintenant que votre bloc de devis de base est défini et validé dans le projet CitiSignal, vous pouvez ajouter un bloc **fiberoffer** à une page existante.

Accédez à [https://my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com){target="_blank"}. Cliquez sur votre **Programme** pour l’ouvrir.

![ AEMCS ](./images/aemcs6.png){zoomable="yes"}

Cliquez ensuite sur le **de 3 points...** dans l’onglet **Environnements** et cliquez sur **Afficher les détails**.

![ AEMCS ](./images/aemcs9.png){zoomable="yes"}

Vous verrez ensuite les détails de votre environnement. Cliquez sur l’URL de votre environnement de **création**.

>[!NOTE]
>
>Il est possible que votre environnement soit mis en veille. Si c’est le cas, vous devrez d’abord réactiver votre environnement.

![ AEMCS ](./images/aemcs10.png){zoomable="yes"}

Vous devriez alors voir votre environnement de création AEM. Accédez à **Sites**.

![ AEMCS ](./images/block21.png){zoomable="yes"}

Accédez à **CitiSignal** > **us** > **fr**.

![ AEMCS ](./images/block22.png){zoomable="yes"}

Cliquez sur **Créer** puis sélectionnez **Page**.

![ AEMCS ](./images/block23.png){zoomable="yes"}

Sélectionnez **Page** et cliquez sur **Suivant**.

![ AEMCS ](./images/block24.png){zoomable="yes"}

Saisissez les valeurs suivantes :

- Titre : **CitiSignal Fiber**
- Nom : **citisignal-fibre**
- Titre de la page : **CitiSignal Fiber**

Cliquez sur **Créer**.

![ AEMCS ](./images/block25.png){zoomable="yes"}

Vous devriez alors voir ceci.

![ AEMCS ](./images/block26.png){zoomable="yes"}

Cliquez dans la zone vierge pour sélectionner le composant **section**. Cliquez ensuite sur l’icône plus **+** dans le menu de droite.

![ AEMCS ](./images/block27.png){zoomable="yes"}

Votre bloc personnalisé doit alors s’afficher dans la liste des blocs disponibles. Cliquez pour le sélectionner.

![ AEMCS ](./images/block28.png){zoomable="yes"}

Des champs tels que **Texte de l’offre**, **CTA de l’offre** et **Image de l’offre** sont alors ajoutés à l’éditeur. Cliquez sur **+ Ajouter** dans le champ **Image de l’offre** pour sélectionner une image.

![ AEMCS ](./images/block29.png){zoomable="yes"}

Vous devriez alors voir ceci. Cliquez pour ouvrir le dossier **citisignal**.

![ AEMCS ](./images/blockpub1.png){zoomable="yes"}

Sélectionnez l’image **product-enrichment-1.png**. Cliquez sur **Sélectionner**.

![ AEMCS ](./images/blockpub2.png){zoomable="yes"}

Tu devrais avoir ça. Cliquez sur **Publier**.

![ AEMCS ](./images/blockpub3.png){zoomable="yes"}

Cliquez de nouveau sur **Publier**.

![ AEMCS ](./images/blockpub4.png){zoomable="yes"}

Votre nouvelle page a été publiée.

## 1.1.4.5 Ajouter votre nouvelle page au menu de navigation

Dans votre présentation AEM Sites, accédez à **CitiSignal** > **Fragments** et cochez la case correspondant à **En-tête**. Cliquez sur **Modifier**.

![ AEMCS ](./images/nav0.png){zoomable="yes"}

Ajoutez une option de menu au menu de navigation avec le `Fiber` texte. Sélectionnez le texte **Fibre** et cliquez sur l’icône **lien**.

![ AEMCS ](./images/nav1.png){zoomable="yes"}

Saisissez ceci pour le **&#x200B;**&#x200B;URL`/us/en/citisignal-fiber` et cliquez sur l’icône **V** pour confirmer.

![ AEMCS ](./images/nav3.png){zoomable="yes"}

Tu devrais avoir ça. Cliquez sur **Publier**.

![ AEMCS ](./images/nav4.png){zoomable="yes"}

Cliquez de nouveau sur **Publier**.

![ AEMCS ](./images/nav5.png){zoomable="yes"}

Vous pourrez désormais afficher les modifications apportées à votre site web en accédant à `main--citisignal--XXX.aem.page/us/en/` et/ou `main--citisignal--XXX.aem.live/us/en/`, après avoir remplacé XXX par votre compte utilisateur GitHub, ce qui est `woutervangeluwe` dans cet exemple.

Dans cet exemple, l’URL complète devient :
`https://main--citisignal--woutervangeluwe.aem.page/us/en/` et/ou `https://main--citisignal--woutervangeluwe.aem.live/us/en/`

Vous devriez alors voir ceci. Cliquez sur **Fibre**.

![ AEMCS ](./images/nav6.png){zoomable="yes"}

Voici votre bloc personnalisé de base, mais désormais rendu sur le site web.

![ AEMCS ](./images/nav7.png){zoomable="yes"}

Étape Suivante : Bloc Personnalisé Avancé [1.1.5](./ex5.md){target="_blank"}

Revenir à [Adobe Experience Manager Cloud Service et Edge Delivery Services](./aemcs.md){target="_blank"}

[Revenir à tous les modules](./../../../overview.md){target="_blank"}
