---
title: Utilisation des API Adobe dans Workfront Fusion
description: Découvrez comment utiliser les API Adobe dans Workfront Fusion
role: Developer
level: Beginner
jira: KT-5342
doc-type: Tutorial
exl-id: 23ebf8b4-3f16-474c-afe1-520d88331417
source-git-commit: b083a817700320e8e45645702c2868423c1fae99
workflow-type: tm+mt
source-wordcount: '1749'
ht-degree: 0%

---

# 1.2.2 Utilisation des API Adobe dans Workfront Fusion

Découvrez comment utiliser les API Adobe dans Workfront Fusion.

## 1.2.2.1 utiliser l’API Firefly Text To Image avec Workfront Fusion

1. Pointez sur le deuxième nœud **Définir plusieurs variables** et sélectionnez **+** pour ajouter un autre module.

![WF Fusion](./images/wffusion48.png)

1. Recherchez **http** et sélectionnez **HTTP**.

![WF Fusion](./images/wffusion49.png)

1. Sélectionnez **Effectuer une requête**.

![WF Fusion](./images/wffusion50.png)

1. Sélectionnez les variables suivantes :

- **URL** : `https://firefly-api.adobe.io/v3/images/generate`
- **Méthode** : `POST`

1. Sélectionnez **Ajouter un en-tête**.

![WF Fusion](./images/wffusion51.png)

1. Saisissez les en-têtes suivants :

| Clé | Valeur |
|:-------------:| :---------------:| 
| `x-api-key` | votre variable stockée pour `CONST_client_id` |
| `Authorization` | `Bearer ` + votre variable stockée pour `bearer_token` |
| `Content-Type` | `application/json` |
| `Accept` | `*/*` |

1. Saisissez les détails de la `x-api-key`. Sélectionnez **Ajouter**.

![WF Fusion](./images/wffusion52.png)

1. Sélectionnez **Ajouter un en-tête**.

![WF Fusion](./images/wffusion53.png)

1. Saisissez les détails de la `Authorization`. Sélectionnez **Ajouter**.

![WF Fusion](./images/wffusion54.png)

1. Sélectionnez **Ajouter un en-tête**. Saisissez les détails de la `Content-Type`. Sélectionnez **Ajouter**.

![WF Fusion](./images/wffusion541.png)

1. Sélectionnez **Ajouter un en-tête**. Saisissez les détails de la `Accept`. Sélectionnez **Ajouter**.

![WF Fusion](./images/wffusion542.png)

1. Définissez le **Type de corps** sur **Brut**. Pour **Type de contenu**, sélectionnez **JSON (application/json)**.

![WF Fusion](./images/wffusion55.png)

1. Collez cette payload dans le champ **Demander le contenu**.

```json
{
  "numVariations": 1,
  "size": {
    "width": 2048,
    "height": 2048
  },
  "prompt": "Horses in a field",
  "promptBiasingLocaleCode": "en-US"
}
```

1. Cochez la case **Analyser la réponse**. Sélectionnez **OK**.

![WF Fusion](./images/wffusion56.png)

1. Sélectionnez **Exécuter une fois**.

![WF Fusion](./images/wffusion57.png)

Votre écran devrait ressembler à ceci.

![WF Fusion](./images/wffusion58.png)

1. Sélectionner le **?** l’icône sur le quatrième nœud, HTTP, pour afficher la réponse. Vous devriez voir un fichier image dans la réponse.

![WF Fusion](./images/wffusion59.png)

1. Copiez l’URL de l’image et ouvrez-la dans une fenêtre de navigateur. Votre écran doit ressembler à ceci :

![WF Fusion](./images/wffusion60.png)

1. Cliquez avec le bouton droit sur **HTTP** et renommez en **Firefly T2I**.

![WF Fusion](./images/wffusion62.png)

1. Sélectionnez **Enregistrer** pour enregistrer vos modifications.

![WF Fusion](./images/wffusion61.png)

## 1.2.2.2 utiliser l’API Photoshop avec Workfront Fusion

1. Sélectionnez **clé à molette** entre les nœuds **Définir le jeton du porteur** et **Firefly T2I**. Sélectionnez **Ajouter un routeur**.

![WF Fusion](./images/wffusion63.png)

1. Faites un clic droit sur l’objet **Firefly T2I** et sélectionnez **Cloner**.

![WF Fusion](./images/wffusion64.png)

1. Faites glisser et déposez l’objet cloné à proximité de l’objet **Router** qui se connecte automatiquement au **Router**. Votre écran doit ressembler à ceci :

![WF Fusion](./images/wffusion65.png)

Vous disposez désormais d’une copie identique basée sur la requête HTTP T2I **** Firefly. Certains des paramètres de la requête HTTP T2I **** Firefly sont similaires à ce dont vous avez besoin pour interagir avec l’API **Photoshop**, ce qui vous permet de gagner du temps. Désormais, il vous suffit de modifier les variables qui ne sont pas les mêmes, comme l’URL de requête et la payload.

1. Remplacez **URL** par `https://image.adobe.io/pie/psdService/text`.

![WF Fusion](./images/wffusion66.png)

1. Remplacez **Demander du contenu** par la payload ci-dessous :

```json
{
  "inputs": [
    {
      "storage": "external",
      "href": "{{AZURE_STORAGE_URL}}/{{AZURE_STORAGE_CONTAINER}}/citisignal-fiber.psd{{AZURE_STORAGE_SAS_READ}}"
    }
  ],
  "options": {
    "layers": [
      {
        "name": "2048x2048-button-text",
        "text": {
          "content": "Click here"
        }
      },
      {
        "name": "2048x2048-cta",
        "text": {
          "content": "Buy this stuff"
        }
      }
    ]
  },
  "outputs": [
    {
      "storage": "azure",
      "href": "{{AZURE_STORAGE_URL}}/{{AZURE_STORAGE_CONTAINER}}/citisignal-fiber-changed-text.psd{{AZURE_STORAGE_SAS_WRITE}}",
      "type": "vnd.adobe.photoshop",
      "overwrite": true
    }
  ]
}
```

![WF Fusion](./images/wffusion67.png)

Pour que ce **Demander du contenu** fonctionne correctement, certaines variables sont manquantes :

- `AZURE_STORAGE_URL`
- `AZURE_STORAGE_CONTAINER`
- `AZURE_STORAGE_SAS_READ`
- `AZURE_STORAGE_SAS_WRITE`

1. Revenez à votre premier nœud, sélectionnez **Initialiser les constantes** puis choisissez **Ajouter un élément** pour chacune de ces variables.

![WF Fusion](./images/wffusion69.png)

| Clé | Exemple de valeur |
|:-------------:| :---------------:| 
| `AZURE_STORAGE_URL` | `https://vangeluw.blob.core.windows.net` |
| `AZURE_STORAGE_CONTAINER` | `vangeluw` |
| `AZURE_STORAGE_SAS_READ` | `?sv=2023-01-03&st=2025-01-13T07%3A36%3A35Z&se=2026-01-14T07%3A36%3A00Z&sr=c&sp=rl&sig=4r%2FcSJLlt%2BSt9HdFdN0VzWURxRK6UqhB8TEvbWkmAag%3D` |
| `AZURE_STORAGE_SAS_WRITE` | `?sv=2023-01-03&st=2025-01-13T17%3A21%3A09Z&se=2025-01-14T17%3A21%3A09Z&sr=c&sp=racwl&sig=FD4m0YyyqUj%2B5T8YyTFJDi55RiTDC9xKtLTgW0CShps%3D` |

Vous pouvez retrouver vos variables en revenant à Postman, puis en ouvrant votre **Variables d’environnement**.

![ Stockage Azure ](./../module1.1/images/az105.png)

1. Copiez ces valeurs dans Workfront Fusion et ajoutez un nouvel élément pour chacune de ces 4 variables.

1. Votre écran devrait ressembler à ceci. Sélectionnez **OK**.

![WF Fusion](./images/wffusion68.png)

Ensuite, revenez à la requête HTTP clonée pour mettre à jour le **contenu de la requête**. Notez les variables noires dans la **Demander du contenu**, qui sont les variables que vous avez copiées à partir de Postman. Vous devez passer aux variables que vous venez de définir dans Workfront Fusion. Remplacez chaque variable une par une en supprimant le texte noir et en le remplaçant par la variable correcte.

![WF Fusion](./images/wffusion70.png)

1. Effectuez ces 3 modifications dans la section **entrées**. Sélectionnez **OK**.

![WF Fusion](./images/wffusion71.png)

1. Effectuez ces 3 modifications dans la section **sorties**. Sélectionnez **OK**.

![WF Fusion](./images/wffusion72.png)

1. Cliquez avec le bouton droit sur le nœud cloné, puis sélectionnez **Renommer**. Remplacez le nom par **Photoshop Modifier le texte**.

![WF Fusion](./images/wffusion73.png)

Votre écran doit ressembler à ceci :

![WF Fusion](./images/wffusion74.png)

1. Sélectionnez **Exécuter une fois**.

![WF Fusion](./images/wffusion75.png)

1. Sélectionnez l’icône **rechercher** sur le nœud **Modifier le texte de Photoshop** pour afficher la réponse. Vous devriez avoir une réponse qui ressemble à ceci, avec un lien vers un fichier de statut.

![WF Fusion](./images/wffusion76.png)

1. Avant de poursuivre les interactions avec l’API Photoshop, désactivez l’itinéraire vers le nœud T2I **** Firefly pour ne pas envoyer d’appels d’API inutiles à ce point d’entrée de l’API. Sélectionnez l’icône **clé à molette**, puis sélectionnez **Désactiver l’itinéraire**.

![WF Fusion](./images/wffusion77.png)

Votre écran doit ressembler à ceci :

![WF Fusion](./images/wffusion78.png)

1. Ajoutez ensuite un autre nœud **Définir plusieurs variables**.

![WF Fusion](./images/wffusion79.png)

1. Placez-le après le nœud **Texte de modification de Photoshop**.

![WF Fusion](./images/wffusion80.png)

1. Sélectionnez le nœud **Définir plusieurs variables**, puis sélectionnez **Ajouter un élément**. Sélectionnez la valeur de la variable dans la réponse de la requête précédente.

| Nom de la variable | Valeur de variable |
|:-------------:| :---------------:| 
| `psdStatusUrl` | `data > _links > self > href` |

1. Sélectionnez **Ajouter**.

![WF Fusion](./images/wffusion81.png)

1. Sélectionnez **OK**.

![WF Fusion](./images/wffusion82.png)

1. Cliquez avec le bouton droit sur le nœud **Modifier le texte de Photoshop** et sélectionnez **Cloner**.

![WF Fusion](./images/wffusion83.png)

1. Faites glisser la requête HTTP clonée après le nœud **Définir plusieurs variables** que vous venez de créer.

![WF Fusion](./images/wffusion83.png)

1. Cliquez avec le bouton droit sur la requête HTTP clonée, sélectionnez **Renommer** et remplacez le nom par **Statut de vérification de Photoshop**.

![WF Fusion](./images/wffusion84.png)

1. Sélectionnez pour ouvrir la requête HTTP. Modifiez l’URL afin qu’elle référence la variable que vous avez créée à l’étape précédente, puis définissez la **Méthode** sur **GET**.

![WF Fusion](./images/wffusion85.png)

1. Supprimez le **Corps** en sélectionnant l’option vide.

![WF Fusion](./images/wffusion86.png)

1. Sélectionnez **OK**.

![WF Fusion](./images/wffusion87.png)

1. Sélectionnez **Exécuter une fois**.

![WF Fusion](./images/wffusion88.png)

Une réponse contenant le champ **statut**, avec le statut défini sur **en cours** s’affiche. Photoshop a besoin de quelques secondes pour terminer le processus.

![WF Fusion](./images/wffusion89.png)

Maintenant que vous savez que la réponse a besoin d’un peu plus de temps pour être terminée, il peut être judicieux d’ajouter un minuteur devant cette requête HTTP afin qu’elle ne s’exécute pas immédiatement.

1. Sélectionnez le nœud **Outils**, puis sélectionnez **Veille**.

![WF Fusion](./images/wffusion90.png)

1. Placez le nœud **Sleep** entre **Set multiple variables** et **Photoshop Check Status**. Définissez le paramètre **Délai** sur **5 secondes**. Sélectionnez **OK**.

![WF Fusion](./images/wffusion91.png)

Votre écran devrait ressembler à ceci. Le problème avec la configuration ci-dessous est que 5 secondes d’attente peuvent être suffisantes, mais peut-être pas suffisantes. En réalité, il serait préférable d’avoir une solution plus intelligente comme une boucle do...while qui vérifie l’état toutes les 5 secondes jusqu’à ce que l’état soit égal à **réussi**. Vous pouvez donc mettre en œuvre une telle tactique dans les étapes suivantes.

![WF Fusion](./images/wffusion92.png)

1. Sélectionnez l’icône **clé à molette** entre **Définir plusieurs variables** et **Mettre en veille**. Sélectionnez **Ajouter un module**.

![WF Fusion](./images/wffusion93.png)

1. Recherchez `flow` puis sélectionnez **Contrôle de flux**.

![WF Fusion](./images/wffusion94.png)

1. Sélectionnez **Répéteur**.

![WF Fusion](./images/wffusion95.png)

1. Définissez **Répétitions** sur **20**. Sélectionnez **OK**.

![WF Fusion](./images/wffusion96.png)

1. Sélectionnez ensuite **+** dans le **Statut de la vérification de Photoshop** pour ajouter un autre module.

![WF Fusion](./images/wffusion97.png)

1. Recherchez **flow** et sélectionnez **Flow Control**.

![WF Fusion](./images/wffusion98.png)

1. Sélectionnez **Agrégateur de tableaux**.

![WF Fusion](./images/wffusion99.png)

1. Définissez **Module Source** sur **Répéteur**. Sélectionnez **OK**.

![WF Fusion](./images/wffusion100.png)

Votre écran doit ressembler à ceci :

![WF Fusion](./images/wffusion101.png)

1. Sélectionnez l’icône **clé à molette** puis **Ajouter un module**.

![WF Fusion](./images/wffusion102.png)

1. Recherchez **outils** et sélectionnez **Outils**.

![WF Fusion](./images/wffusion103.png)

1. Sélectionnez **Obtenir plusieurs variables**.

![WF Fusion](./images/wffusion104.png)

1. Sélectionnez **+ Ajouter un élément** puis définissez le **Nom de variable** sur `done`.

![WF Fusion](./images/wffusion105.png)

1. Sélectionnez **OK**.

![WF Fusion](./images/wffusion106.png)

1. Sélectionnez le nœud **Définir plusieurs variables** que vous avez configuré précédemment. Pour initialiser la variable **done**, vous devez la définir sur `false` ici. Sélectionnez **+ Ajouter un élément**.

![WF Fusion](./images/wffusion107.png)

1. Utilisez `done` pour le **Nom de la variable**

1. Pour définir le statut, une valeur booléenne est nécessaire. Pour trouver la valeur booléenne, sélectionnez **engrenage** puis sélectionnez `false`. Sélectionnez **Ajouter**.

![WF Fusion](./images/wffusion108.png)

1. Sélectionnez **OK**.

![WF Fusion](./images/wffusion109.png)

1. Sélectionnez ensuite l’icône **clé à molette** après le nœud **Obtenir plusieurs variables** que vous avez configuré.

![WF Fusion](./images/wffusion110.png)

1. Sélectionnez **Configurer un filtre**. Vous devez maintenant vérifier la valeur de la variable **done**. Si cette valeur est définie sur **false**, la partie suivante de la boucle doit être exécutée. Si la valeur est définie sur **true**, cela signifie que le processus s’est déjà terminé avec succès, de sorte qu’il n’est pas nécessaire de poursuivre avec la partie suivante de la boucle.

![WF Fusion](./images/wffusion111.png)

1. Pour l’étiquette, utilisez **Avons-nous terminé ?**. Définissez la **Condition** à l’aide de la variable déjà existante **done**, l’opérateur doit être défini sur **Égal à** et la valeur doit être la variable booléenne `false`. Sélectionnez **OK**.

![WF Fusion](./images/wffusion112.png)

1. Ensuite, faites de l’espace entre les nœuds **Statut de vérification de Photoshop** et **Agrégateur de tableau**. Sélectionnez ensuite l’icône **clé à molette** et sélectionnez **Ajouter un routeur**. Vous effectuez cette opération, car après avoir vérifié le statut du fichier Photoshop, il doit y avoir 2 chemins d’accès. Si le statut est `succeeded`, la variable de **done** doit être définie sur `true`. Si le statut n’est pas égal à `succeeded`, la boucle doit continuer. Le routeur va permettre de vérifier et de régler cela.

![WF Fusion](./images/wffusion113.png)

1. Après avoir ajouté le routeur, sélectionnez l’icône **clé à molette** et sélectionnez **Configurer un filtre**.

![WF Fusion](./images/wffusion114.png)

1. Pour l’étiquette, utilisez **Nous avons terminé**. Définissez la **Condition** à l’aide de la réponse du nœud **Statut de la vérification Photoshop** en choisissant le champ de réponse **data.output[].status**. L’opérateur doit être défini sur **Égal à** et la valeur doit être `succeeded`. Sélectionnez **OK**.

![WF Fusion](./images/wffusion115.png)

1. Sélectionnez ensuite le nœud vide avec le point d’interrogation et recherchez **outils**. Sélectionnez ensuite **Outils**.

![WF Fusion](./images/wffusion116.png)

1. Sélectionnez **Définir plusieurs variables**.

![WF Fusion](./images/wffusion117.png)

1. Lorsque cette branche du routeur est utilisée, cela signifie que le statut de la création du fichier Photoshop est terminé avec succès. Cela signifie que la boucle do...while n’a plus besoin de continuer à vérifier le statut dans Photoshop. Vous devez donc définir la variable `done` sur `true`.

1. Pour le **Nom de variable**, utilisez `done`.

1. Pour la **Valeur de variable**, vous devez utiliser la valeur booléenne `true`. Sélectionnez l’icône **engrenage** puis sélectionnez `true`. Sélectionnez **Ajouter**.

![WF Fusion](./images/wffusion118.png)

1. Sélectionnez **OK**.

![WF Fusion](./images/wffusion119.png)

1. Cliquez ensuite avec le bouton droit sur le nœud **Définir plusieurs variables** que vous venez de créer et sélectionnez **Cloner**.

![WF Fusion](./images/wffusion120.png)

1. Faites glisser le nœud cloné afin qu’il se connecte à l’**agrégateur de tableau**. Cliquez ensuite avec le bouton droit sur le nœud et sélectionnez **Renommer**, puis remplacez le nom par `Placeholder End`.

![WF Fusion](./images/wffusion122.png)

1. Supprimez la variable existante et sélectionnez **+ Ajouter un élément**. Pour l’**Nom de variable**, utilisez `placeholder`. Pour l’**Valeur de variable**, utilisez `end`. Sélectionnez **Ajouter** puis sélectionnez **OK**.

![WF Fusion](./images/wffusion123.png)

1. Sélectionnez **Enregistrer** pour enregistrer votre scénario. Sélectionnez ensuite   **Exécuter une fois**.

![WF Fusion](./images/wffusion124.png)

Votre scénario est ensuite exécuté et doit se terminer correctement. Notez que la boucle do...while que vous avez configurée fonctionne correctement. Dans l’exécution ci-dessous, vous pouvez constater que le **Répéteur** s’est exécuté 20 fois en fonction de la bulle sur le nœud **Outils > Obtenir plusieurs variables**. Après ce nœud, vous avez configuré un filtre qui vérifiait le statut et les nœuds suivants ont été exécutés uniquement si le statut n’était pas égal à **réussi**. Dans cette exécution, la partie suivant le filtre ne s’est exécutée qu’une seule fois, car le statut était déjà **réussi** lors de la première exécution.

![WF Fusion](./images/wffusion125.png)

1. Vous pouvez vérifier le statut de la création de votre nouveau fichier Photoshop en cliquant sur la bulle dans la requête HTTP **Vérification du statut de Photoshop** et en accédant au champ **statut**.

![WF Fusion](./images/wffusion126.png)

Vous avez maintenant configuré la version de base d’un scénario répétable qui automatise un certain nombre d’étapes. Dans l’exercice suivant, vous allez en reparler en ajoutant de la complexité.

## Étapes suivantes

Accédez à [ Automatisation des processus avec Workfront Fusion ](./ex3.md){target="_blank"}

Revenez à [Automatisation des services Adobe Firefly](./automation.md){target="_blank"}.

Revenir à [Tous les modules](./../../../overview.md){target="_blank"}
