---
title: Mise en œuvre de Brand Concierge sur votre site web
description: Mise en œuvre de Brand Concierge sur votre site web
kt: 5342
doc-type: tutorial
source-git-commit: fb1fc5c72723cc4e1ede87f90410feb0cc314eea
workflow-type: tm+mt
source-wordcount: '1347'
ht-degree: 0%

---

# 1.4.2 Implémentation de Brand Concierge sur votre site web

>[!IMPORTANT]
>
>Pour effectuer cet exercice, vous devez avoir accès à un environnement de création AEM Assets CS fonctionnel et à un site web AEM CS/EDS.
>
>Si vous ne disposez pas d’un tel environnement, accédez à [Adobe Experience Manager Cloud Service &amp; Edge Delivery Services](./../../../modules/asset-mgmt/module2.1/aemcs.md){target="_blank"}. Suivez les instructions qui s’affichent à cet endroit et vous aurez accès à un tel environnement.

>[!IMPORTANT]
>
>Si vous avez précédemment configuré un programme AEM CS avec un environnement AEM Assets CS, il se peut que votre sandbox AEM CS ait été mis en veille. Étant donné que la réactivation d’un tel sandbox prend entre 10 et 15 minutes, il serait judicieux de lancer le processus de réactivation maintenant afin de ne pas avoir à l’attendre plus tard.

## 1.4.2.1 Configurer votre site web pour afficher Brand Concierge - AEM Author

Pour que Brand Concierge apparaisse sur votre site web, vous devez créer un nouveau bloc personnalisé qui doit être ajouté à une nouvelle page. Vous devez également vous assurer que votre nouvelle page est ajoutée à la navigation de votre site web.

Vous devez maintenant configurer les éléments suivants dans cet ordre :

- Créez un bloc personnalisé qui sera utilisé pour charger Brand Concierge sur votre site web.
- Créez une page sur votre site web pour Brand Concierge.
- Liez le bloc personnalisé que vous venez de créer sur la page Brand Concierge que vous venez de créer.
- Ajoutez une référence pour accéder à la page Brand Concierge nouvellement créée dans le fichier d’en-tête de navigation de votre site web.

### Créer un bloc personnalisé

Pour créer le bloc personnalisé, accédez au référentiel GitHub lié à votre site web.

![Bloquer](./images/block1.png)

#### component-definition.json

Faites défiler jusqu’à ce que le fichier **component-definition.json** s’affiche et ouvrez-le

![Bloquer](./images/block8.png)

Cliquez sur l’icône **crayon** pour commencer à modifier le fichier.

![Bloquer](./images/block8a.png)

Faites défiler jusqu’à ce que le **Blocs** s’affiche. Placez le curseur sous le crochet de fermeture du composant **Cartes**

![Bloquer](./images/block9.png)

Collez ce code et saisissez une virgule **,** après le bloc de code :

```json
{
  "title": "BrandConcierge",
  "id": "brandconcierge",
  "plugins": {
    "xwalk": {
      "page": {
        "resourceType": "core/franklin/components/block/v1/block",
        "template": {
          "name": "BrandConcierge",
          "model": "brandconcierge"
        }
      }
    }
  }
},
```

Cliquez sur **Valider les modifications...**.

![Bloquer](./images/block10.png)

Cliquez sur **Valider les modifications**.

![Bloquer](./images/block10a.png)

#### component-models.json

Faites défiler l’écran vers le bas jusqu’à afficher le fichier **component-models.json**, puis cliquez sur l’icône **crayon** pour commencer à modifier le fichier.

![Bloquer](./images/block11.png)

Faites défiler vers le bas jusqu’à ce que le dernier élément s’affiche. Placez le curseur en regard du crochet fermant du dernier composant.

![Bloquer](./images/block12.png)

Saisissez une virgule **,**, puis appuyez sur Entrée et, sur la ligne suivante, collez ce code :

```json
{
  "id": "brandconcierge",
  "fields": []
}
```

Cliquez sur **Valider les modifications...**.

![Bloquer](./images/block13.png)

Cliquez sur **Valider les modifications**.

![Bloquer](./images/block13a.png)

#### component-filters.json

Faites défiler l’écran vers le bas jusqu’à afficher le fichier **component-filters.json**, puis cliquez sur l’icône **crayon** pour commencer à modifier le fichier.

![Bloquer](./images/block14.png)

Vous devriez alors voir ceci.

![Bloquer](./images/block14a.png)

Sous **section**, saisissez une `,` par virgule et collez l’identifiant de votre composant `"brandconcierge"` après la dernière ligne active.

Cliquez sur **Valider les modifications...**.

![Bloquer](./images/block15.png)

Cliquez sur **Valider les modifications**.

![Bloquer](./images/block15a.png)

#### brandconcierge.css

Lors de la création d’un bloc, il est recommandé de créer un fichier pour le style de votre bloc, qui doit porter le même nom. vous devez maintenant créer ce fichier, que nous laisserons vide pour l’instant.

Accédez au dossier **blocs**. Cliquez ensuite sur **Ajouter un fichier** et sélectionnez **Créer un fichier**.

![Bloquer](./images/css1.png)

Dans la zone de texte, saisissez `brandconcierge/brandconcierge.css`. Le fichier peut rester vide pour l&#39;instant. Cliquez sur **Valider les modifications...**.

![Bloquer](./images/css2.png)

Cliquez sur **Valider les modifications**.

![Bloquer](./images/css3.png)

#### brandconcierge.js

Lors de la création d’un bloc, il est recommandé de créer un fichier pour le code JavaScript correspondant à votre bloc, qui doit porter le même nom.

Cliquez sur **Ajouter un fichier** et sélectionnez **Créer un fichier**.

![Bloquer](./images/js1.png)

Dans la zone de texte, saisissez `brandconcierge.js`. Le fichier peut rester vide pour l&#39;instant. Cliquez sur **Valider les modifications...**.

```javascript
export default function decorate(block) {
  block.setAttribute('id', 'brand-concierge-mount');
}
```

![Bloquer](./images/js2.png)

Cliquez sur **Valider les modifications**.

![Bloquer](./images/js3.png)

### Créer une page et lier un nouveau bloc personnalisé

Accédez à [https://my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com){target="_blank"}. Cliquez sur votre **Programme** pour l’ouvrir.

![&#x200B; AEMCS &#x200B;](./images/aemcs6.png)

Cliquez ensuite sur le **de 3 points...** dans l’onglet **Environnements** et cliquez sur **Afficher les détails**.

![&#x200B; AEMCS &#x200B;](./images/aemcs9.png)

Vous verrez ensuite les détails de votre environnement. Cliquez sur l’URL de votre environnement de **création**.

>[!NOTE]
>
>Il est possible que votre environnement soit mis en veille. Si c’est le cas, vous devrez d’abord réactiver votre environnement. Vous trouverez des instructions pour réactiver dans la vidéo ci-dessous.

>[!VIDEO](https://video.tv.adobe.com/v/3478141?quality=12&learn=on)

![&#x200B; AEMCS &#x200B;](./images/aemcs10.png)

Vous devriez alors voir votre environnement de création AEM. Accédez à **Sites**.

![&#x200B; AEMCS &#x200B;](./images/block21.png)

Accédez à **CitiSignal**. Cliquez sur **Créer** puis sélectionnez **Page**.

![&#x200B; AEMCS &#x200B;](./images/block23.png)

Sélectionnez **Page** et cliquez sur **Suivant**.

![&#x200B; AEMCS &#x200B;](./images/block24.png)

Saisissez les valeurs suivantes :

- Titre : **Brand Concierge**
- Nom : **brandconcierge**
- Titre De La Page : **Brand Concierge**

Cliquez sur **Créer**.

![&#x200B; AEMCS &#x200B;](./images/block25.png)

Sélectionnez **Ouvrir**.

![&#x200B; AEMCS &#x200B;](./images/block22.png)

Vous devriez alors voir ceci.

![&#x200B; AEMCS &#x200B;](./images/block26.png)

Cliquez dans la zone vierge pour sélectionner le composant **section**. Cliquez ensuite sur l’icône plus **+** dans le menu de droite.

![&#x200B; AEMCS &#x200B;](./images/block27.png)

Votre bloc personnalisé doit alors s’afficher dans la liste des blocs disponibles. Cliquez pour le sélectionner.

![&#x200B; AEMCS &#x200B;](./images/block28.png)

Vous devriez alors voir un bloc vide ajouté à cette page. Ce bloc sera chargé dynamiquement à l’aide des bibliothèques JavaScript que vous ajouterez à l’étape suivante.

Cliquez sur **Publier**.

![&#x200B; AEMCS &#x200B;](./images/block29.png)

Cliquez de nouveau sur **Publier**.

![&#x200B; AEMCS &#x200B;](./images/block30.png)

Votre nouvelle page est maintenant publiée et peut être ajoutée à l’en-tête de navigation à l’étape suivante.

### Mettre à jour le fichier d’en-tête de navigation

Dans votre présentation AEM Sites, accédez à **CitiSignal** et cochez la case du fichier **Header/nav**. Cliquez sur **Modifier**.

![&#x200B; AEMCS &#x200B;](./images/nav0.png)

Sélectionnez le champ **Texte** dans l’écran d’aperçu, puis cliquez sur le champ **Texte** sur le côté droit de l’écran pour le modifier.

![&#x200B; AEMCS &#x200B;](./images/nav0a.png)

Créez une nouvelle option de menu dans le menu de navigation avec le `Brand Concierge` texte. Sélectionnez ensuite le texte **Brand Concierge** puis cliquez sur l&#39;icône **lien**.

![&#x200B; AEMCS &#x200B;](./images/nav1.png)

Saisissez ceci pour le champ **Chemin ou URL** `/content/CitiSignal/brandconcierge.html` et saisissez `Brand Concierge` pour le champ **Titre**. Cliquez sur **Enregistrer**.

![&#x200B; AEMCS &#x200B;](./images/nav3.png)

Tu devrais avoir ça. Cliquez sur **Terminé**.

![&#x200B; AEMCS &#x200B;](./images/nav4.png)

Tu devrais avoir ça. Cliquez sur **Publier**.

![&#x200B; AEMCS &#x200B;](./images/nav4a.png)

Cliquez de nouveau sur **Publier**.

![&#x200B; AEMCS &#x200B;](./images/nav5.png)

Votre nouvelle page est maintenant ajoutée au menu.

## 1.4.2.2 Configurer votre site web pour afficher Brand Concierge - GitHub

Après avoir mis à jour le contenu à l’aide de votre environnement de création AEM, vous devez maintenant mettre à jour une partie du code du référentiel GitHub utilisé pour votre site web.

### Bibliothèques JavaScript

Les bibliothèques suivantes sont nécessaires pour implémenter Brand Concierge sur votre site web exécuté sur AEM CS/EDS :

- [styleconfigurations.js](./assets/styleconfigurations.js)
- [alloy.js](./assets/alloy.js)
- [brandconciergemain.js](./assets/brandconciergemain.js)

Téléchargez les 3 fichiers sur votre bureau.

![Brand Concierge](./images/aem0.png)

Accédez au projet GitHub de votre site web AEM CS/EDS. Accédez à **scripts**.

![Brand Concierge](./images/aem1.png)

Cliquez sur **Ajouter un fichier** puis sélectionnez **Télécharger des fichiers**.

![Brand Concierge](./images/aem3.png)

Cliquez sur **Choisir vos fichiers**.

![Brand Concierge](./images/aem3a.png)

Sélectionnez les 3 fichiers **styleConfigurations.js, alloy.js et brandconciergemain.js** sur votre bureau et cliquez sur **Ouvrir**.

![Brand Concierge](./images/aem4.png)

Cliquez sur **Valider les modifications**.

![Brand Concierge](./images/aem5.png)

### Mettre à jour head.html

À l’étape précédente, vous avez chargé 3 nouvelles bibliothèques. Ces bibliothèques doivent maintenant être chargées lors du chargement de votre site web. Pour ce faire, ajoutez des références à ces fichiers dans le fichier **head.html**.

En outre, vous devez également fournir des instructions dans le fichier **head.html** pour vous assurer que les bibliothèques sont chargées dans le bon ordre et de manière correcte.

Pour ce faire, accédez au projet GitHub de votre site Web CS/EDS AEM en cliquant sur **Code**.

![Brand Concierge](./images/aem6.png)

Faites défiler l’écran vers le bas. Ouvrez le fichier **head.html**.

![Brand Concierge](./images/aem7.png)

Cliquez sur l’icône **crayon** pour modifier ce fichier.

![Brand Concierge](./images/aem8.png)

Vous devriez alors voir ceci.

![Brand Concierge](./images/aem9.png)

Faites défiler jusqu’à la ligne 43 et collez les éléments suivants :

Vous devez mettre à jour 2 champs du code ci-dessous :

>[!IMPORTANT]
>
>- **datastreamId** est actuellement défini sur « XXXXX » et doit être remplacé par l’identifiant du flux de données que vous avez créé à l’étape précédente.
>- **orgId** doit être remplacé par l’ID d’organisation IMS de votre instance Adobe Experience Cloud.

```javascript
<script src="/scripts/styleconfigurations.js"></script>

<script>
		!function (n, o) {
      o.forEach(function (o) {
        n[o] || ((n.__alloyNS = n.__alloyNS ||
          []).push(o), n[o] = function () {
            var u = arguments; return new Promise(
              function (i, l) { n[o].q.push([i, l, u]) })
          }, n[o].q = [])
      })
    }
      (window, ["alloy"]);
	</script>


<script src="/scripts/alloy.js"></script>

<script>
	alloy("configure", {
		defaultConsent: "in",
        edgeDomain: "edge.adobedc.net",
        edgeBasePath: "ee",
        datastreamId: "XXXXX", // replace datastreamId
        orgId: "--aepImsOrgId--", // replace ims org Id
        debugEnabled: true,
        idMigrationEnabled: false,
        thirdPartyCookiesEnabled: false,
        prehidingStyle: ".personalization-container { opacity: 0 !important }",
    });

window["alloy"]("sendEvent", {
    conversation: {
        fetchConversationalExperience: true
    }
}).then(result => {
    console.log("Conversation experience fetched", result);
    window["alloy"]("bootstrapConversationalExperience", {
        selector: "#brand-concierge-mount",
        src: "/scripts/brandconciergemain.js",
        stylingConfigurations: window.styleConfiguration,
        stickySession: true // create a sticky session cookie with expiration
    })
});
</script>
```

Cliquez sur **Valider la modification...**.

![Brand Concierge](./images/aem10.png)

Cliquez sur **Valider la modification**.

![Brand Concierge](./images/aem11.png)

Vous avez maintenant mis à jour le code requis pour charger les bibliothèques sur votre site web.

![Brand Concierge](./images/aem12.png)

## 1.4.2.3 Tester votre configuration

Vous pourrez maintenant tester vos modifications sur votre site web en accédant à `main--citisignal-aem-accs--XXX.aem.page` ou `main--citisignal-aem-accs--XXX.aem.live`, après avoir remplacé XXX par votre compte utilisateur GitHub, qui dans cet exemple est `woutervangeluwe`.

Dans cet exemple, l’URL complète devient :
`https://main--citisignal-aem-accs--woutervangeluwe.aem.page` et/ou `https://main--citisignal-aem-accs--woutervangeluwe.aem.live`

Cela peut prendre un certain temps avant que toutes les ressources ne s’affichent correctement, car elles doivent d’abord être publiées.

Vous devriez alors voir ceci. Cliquez sur **Brand Concierge**.

![Brand Concierge](./images/aem13.png)

Vous devriez alors voir ce Brand Concierge où vous pouvez saisir votre invite.

![Brand Concierge](./images/aem14.png)

Revenir à [Brand Concierge](./brandconcierge.md){target="_blank"}

[Revenir à tous les modules](./../../../overview.md){target="_blank"}