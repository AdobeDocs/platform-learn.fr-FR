---
title: Utilisation des API Adobe dans Workfront Fusion
description: Découvrez comment utiliser les API Adobe dans Workfront Fusion
role: Developer
level: Beginner
jira: KT-5342
doc-type: Tutorial
exl-id: 23ebf8b4-3f16-474c-afe1-520d88331417
source-git-commit: 603e48e0453911177823fe7ceb340f8ca801c5e1
workflow-type: tm+mt
source-wordcount: '1749'
ht-degree: 0%

---

# 1.2.2 Utilisation des API Adobe dans Workfront Fusion

Découvrez comment utiliser les API Adobe dans Workfront Fusion.

## 1.2.2.1 utiliser l’API Firefly Text To Image avec Workfront Fusion

Pointez sur le deuxième nœud **Définir plusieurs variables** et sélectionnez **+** pour ajouter un autre module.

![WF Fusion](./images/wffusion48.png)

Recherchez **http** et sélectionnez **HTTP**.

![WF Fusion](./images/wffusion49.png)

Sélectionnez **Effectuer une requête**.

![WF Fusion](./images/wffusion50.png)

Sélectionnez les variables suivantes :

- **URL** : `https://firefly-api.adobe.io/v3/images/generate`
- **Méthode** : `POST`

Sélectionnez **Ajouter un en-tête**.

![WF Fusion](./images/wffusion51.png)

Saisissez les en-têtes suivants :

| Clé | Valeur |
|:-------------:| :---------------:| 
| `x-api-key` | votre variable stockée pour `CONST_client_id` |
| `Authorization` | `Bearer ` + votre variable stockée pour `bearer_token` |
| `Content-Type` | `application/json` |
| `Accept` | `*/*` |

Saisissez les détails de la `x-api-key`. Sélectionnez **Ajouter**.

![WF Fusion](./images/wffusion52.png)

Sélectionnez **Ajouter un en-tête**.

![WF Fusion](./images/wffusion53.png)

Saisissez les détails de `Authorization`. Sélectionnez **Ajouter**.

![WF Fusion](./images/wffusion54.png)

Sélectionnez **Ajouter un en-tête**. Saisissez les détails de la `Content-Type`. Sélectionnez **Ajouter**.

![WF Fusion](./images/wffusion541.png)

Sélectionnez **Ajouter un en-tête**. Saisissez les détails de la `Accept`. Sélectionnez **Ajouter**.

![WF Fusion](./images/wffusion542.png)

Définissez le type **de** corps sur **Raw**. Pour **Type de** contenu, sélectionnez **JSON (application/json).**

![WF Fusion](./images/wffusion55.png)

Collez cette payload dans le champ **Demander le contenu**.

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

Cochez la case Analyse **de la réponse**. Sélectionnez **OK.**

![WF Fusion](./images/wffusion56.png)

Sélectionnez **Exécuter une fois**.

![WF Fusion](./images/wffusion57.png)

Votre écran devrait ressembler à ceci.

![WF Fusion](./images/wffusion58.png)

Sélectionner le **?** l’icône sur le quatrième nœud, HTTP, pour afficher la réponse. Vous devriez voir un fichier image dans la réponse.

![WF Fusion](./images/wffusion59.png)

Copiez l’URL de l’image et ouvrez-la dans une fenêtre de navigateur. Votre écran doit ressembler à ceci :

![WF Fusion](./images/wffusion60.png)

Cliquez avec le bouton droit sur **HTTP** et renommez en **Firefly T2I**.

![WF Fusion](./images/wffusion62.png)

Sélectionnez **Enregistrer** pour enregistrer vos modifications.

![WF Fusion](./images/wffusion61.png)

## 1.2.2.2 utiliser l’API Photoshop avec Workfront Fusion

Sélectionnez **clé à molette** entre les nœuds **Définir le jeton du porteur** et **Firefly T2I**. Sélectionnez **Ajouter un routeur**.

![WF Fusion](./images/wffusion63.png)

Faites un clic droit sur l’objet **Firefly T2I** et sélectionnez **Cloner**.

![WF Fusion](./images/wffusion64.png)

Faites glisser et déposez l’objet cloné à proximité de l’objet **Router** qui se connecte automatiquement au **Router**. Votre écran doit ressembler à ceci :

![WF Fusion](./images/wffusion65.png)

Vous disposez désormais d’une copie identique basée sur la requête HTTP T2I **&#x200B;**&#x200B;Firefly. Certains des paramètres de la requête HTTP T2I **&#x200B;**&#x200B;Firefly sont similaires à ce dont vous avez besoin pour interagir avec l’API **Photoshop**, ce qui vous permet de gagner du temps. Désormais, il vous suffit de modifier les variables qui ne sont pas les mêmes, comme l’URL de requête et la payload.

Remplacez **URL** par `https://image.adobe.io/pie/psdService/text`.

![WF Fusion](./images/wffusion66.png)

Remplacez **Demander du contenu** par la payload ci-dessous :

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

Revenez à votre premier nœud, sélectionnez **Initialiser les constantes** puis choisissez **Ajouter un élément** pour chacune de ces variables.

![WF Fusion](./images/wffusion69.png)

| Clé | Exemple de valeur |
|:-------------:| :---------------:| 
| `AZURE_STORAGE_URL` | `https://vangeluw.blob.core.windows.net` |
| `AZURE_STORAGE_CONTAINER` | `vangeluw` |
| `AZURE_STORAGE_SAS_READ` | `?sv=2023-01-03&st=2025-01-13T07%3A36%3A35Z&se=2026-01-14T07%3A36%3A00Z&sr=c&sp=rl&sig=4r%2FcSJLlt%2BSt9HdFdN0VzWURxRK6UqhB8TEvbWkmAag%3D` |
| `AZURE_STORAGE_SAS_WRITE` | `?sv=2023-01-03&st=2025-01-13T17%3A21%3A09Z&se=2025-01-14T17%3A21%3A09Z&sr=c&sp=racwl&sig=FD4m0YyyqUj%2B5T8YyTFJDi55RiTDC9xKtLTgW0CShps%3D` |

Vous pouvez retrouver vos variables en revenant à Postman, puis en ouvrant votre **Variables d’environnement**.

![&#x200B; Stockage Azure &#x200B;](./../module1.1/images/az105.png)

Copiez ces valeurs dans Workfront Fusion et ajoutez un nouvel élément pour chacune de ces 4 variables.

Votre écran devrait ressembler à ceci. Sélectionnez **OK**.

![WF Fusion](./images/wffusion68.png)

Ensuite, revenez à la requête HTTP clonée pour mettre à jour le **contenu de la requête**. Notez les variables noires dans la **Demander du contenu**, qui sont les variables que vous avez copiées à partir de Postman. Vous devez passer aux variables que vous venez de définir dans Workfront Fusion. Remplacez chaque variable une par une en supprimant le texte noir et en le remplaçant par la variable correcte.

![WF Fusion](./images/wffusion70.png)

Effectuez ces 3 modifications dans la section **entrées**. Sélectionnez **OK**.

![WF Fusion](./images/wffusion71.png)

Apportez ces 3 modifications dans la **section des sorties** . Sélectionnez **OK**.

![WF Fusion](./images/wffusion72.png)

Cliquez avec le bouton droit sur le nœud cloné et choisissez **Renommer**. Remplacez le nom par **Photoshop Modifier le texte**.

![WF Fusion](./images/wffusion73.png)

Votre écran doit ressembler à ceci :

![WF Fusion](./images/wffusion74.png)

Sélectionnez **Exécuter une fois**.

![WF Fusion](./images/wffusion75.png)

Sélectionnez l’icône **de recherche** dans le nœud Photoshop Modifier le  **texte** pour afficher la réponse. Vous devriez avoir une réponse qui ressemble à ceci, avec un lien vers un fichier d’état.

![WF Fusion](./images/wffusion76.png)

Avant de poursuivre les interactions d’API Photoshop, désactivez l’itinéraire vers le **nœud Firefly T2I** pour ne pas envoyer d’appels d’API inutiles à ce point de terminaison d’API. Sélectionnez l’icône **clé à molette**, puis sélectionnez **Désactiver l’itinéraire**.

![WF Fusion](./images/wffusion77.png)

Votre écran doit ressembler à celui-ci :

![WF Fusion](./images/wffusion78.png)

Ajoutez ensuite un autre nœud **Définir plusieurs variables**.

![WF Fusion](./images/wffusion79.png)

Placez-le après le nœud **Texte de modification de Photoshop**.

![WF Fusion](./images/wffusion80.png)

Sélectionnez le nœud **Définir plusieurs variables**, puis sélectionnez **Ajouter un élément**. Sélectionnez la valeur de la variable dans la réponse de la requête précédente.

| Nom de la variable | Valeur de variable |
|:-------------:| :---------------:| 
| `psdStatusUrl` | `data > _links > self > href` |

Sélectionnez **Ajouter**.

![WF Fusion](./images/wffusion81.png)

Sélectionnez **OK**.

![WF Fusion](./images/wffusion82.png)

Cliquez avec le bouton droit sur le nœud **Modifier le texte de Photoshop** et sélectionnez **Cloner**.

![WF Fusion](./images/wffusion83.png)

Faites glisser la requête HTTP clonée après le nœud **Définir plusieurs variables** que vous venez de créer.

![WF Fusion](./images/wffusion83.png)

Cliquez avec le bouton droit sur la requête HTTP clonée, sélectionnez **Renommer** et remplacez le nom par **Statut de vérification de Photoshop**.

![WF Fusion](./images/wffusion84.png)

Sélectionnez pour ouvrir la requête HTTP. Modifiez l’URL afin qu’elle référence la variable que vous avez créée à l’étape précédente, puis définissez la **Méthode** sur **GET**.

![WF Fusion](./images/wffusion85.png)

Supprimez le **Corps** en sélectionnant l’option vide.

![WF Fusion](./images/wffusion86.png)

Sélectionnez **OK**.

![WF Fusion](./images/wffusion87.png)

Sélectionnez **Exécuter une fois**.

![WF Fusion](./images/wffusion88.png)

Une réponse contenant le champ **statut**, avec le statut défini sur **en cours** s’affiche. Photoshop a besoin de quelques secondes pour terminer le processus.

![WF Fusion](./images/wffusion89.png)

Maintenant que vous savez que la réponse a besoin d’un peu plus de temps pour être terminée, il peut être judicieux d’ajouter un minuteur devant cette requête HTTP afin qu’elle ne s’exécute pas immédiatement.

Sélectionnez le nœud **Outils**, puis sélectionnez **Veille**.

![WF Fusion](./images/wffusion90.png)

Placez le nœud **Sleep** entre **Set multiple variables** et **Photoshop Check Status**. Définissez le paramètre **Délai** sur **5 secondes**. Sélectionnez **OK**.

![WF Fusion](./images/wffusion91.png)

Votre écran devrait ressembler à ceci. Le problème avec la configuration ci-dessous est que 5 secondes d’attente peuvent être suffisantes, mais peut-être pas suffisantes. En réalité, il serait préférable d’avoir une solution plus intelligente comme une boucle do...while qui vérifie l’état toutes les 5 secondes jusqu’à ce que l’état soit égal à **réussi**. Vous pouvez donc mettre en œuvre une telle tactique dans les étapes suivantes.

![WF Fusion](./images/wffusion92.png)

Sélectionnez l’icône **clé à molette** entre **Définir plusieurs variables** et **Mettre en veille**. Sélectionnez **Ajouter un module**.

![WF Fusion](./images/wffusion93.png)

Recherchez `flow` puis sélectionnez **Contrôle de flux**.

![WF Fusion](./images/wffusion94.png)

Sélectionnez **Répéteur**.

![WF Fusion](./images/wffusion95.png)

Définissez **les répétitions** sur **20**. Sélectionnez **OK**.

![WF Fusion](./images/wffusion96.png)

Ensuite, sélectionnez **+** sur le Photoshop vérifier l’état **&#x200B;**&#x200B;pour ajouter un autre module.

![WF Fusion](./images/wffusion97.png)

Recherchez **flow** et sélectionnez **Flow Control**.

![WF Fusion](./images/wffusion98.png)

Sélectionnez **Agrégateur de tableaux**.

![WF Fusion](./images/wffusion99.png)

Définissez **Module Source** sur **Répéteur**. Sélectionnez **OK**.

![WF Fusion](./images/wffusion100.png)

Votre écran doit ressembler à ceci :

![WF Fusion](./images/wffusion101.png)

Sélectionnez l’icône **clé à molette** puis **Ajouter un module**.

![WF Fusion](./images/wffusion102.png)

Recherchez **outils** et sélectionnez **Outils**.

![WF Fusion](./images/wffusion103.png)

Sélectionnez **Obtenir plusieurs variables**.

![WF Fusion](./images/wffusion104.png)

Sélectionnez **+ Ajouter un élément** puis définissez le **Nom de variable** sur `done`.

![WF Fusion](./images/wffusion105.png)

Sélectionnez **OK**.

![WF Fusion](./images/wffusion106.png)

Sélectionnez le nœud **Définir plusieurs variables** que vous avez configuré précédemment. Pour initialiser la variable **done**, vous devez la définir sur `false` ici. Sélectionnez **+ Ajouter un élément**.

![WF Fusion](./images/wffusion107.png)

Utilisez `done` pour le **Nom de la variable**

Pour définir le statut, une valeur booléenne est nécessaire. Pour trouver la valeur booléenne, sélectionnez **engrenage** puis sélectionnez `false`. Sélectionnez **Ajouter**.

![WF Fusion](./images/wffusion108.png)

Sélectionnez **OK**.

![WF Fusion](./images/wffusion109.png)

Sélectionnez ensuite l’icône **clé à molette** après le nœud **Obtenir plusieurs variables** que vous avez configuré.

![WF Fusion](./images/wffusion110.png)

Sélectionnez **Configurer un filtre**. Vous devez maintenant vérifier la valeur de la variable **done**. Si cette valeur est définie sur **false**, la partie suivante de la boucle doit être exécutée. Si la valeur est définie sur **true**, cela signifie que le processus s’est déjà terminé avec succès, de sorte qu’il n’est pas nécessaire de poursuivre avec la partie suivante de la boucle.

![WF Fusion](./images/wffusion111.png)

Pour l’étiquette, utilisez **Avons-nous terminé ?**. Définissez la **Condition** à l’aide de la variable déjà existante **done**, l’opérateur doit être défini sur **Égal à** et la valeur doit être la variable booléenne `false`. Sélectionnez **OK**.

![WF Fusion](./images/wffusion112.png)

Ensuite, faites de l’espace entre les nœuds **Statut de vérification de Photoshop** et **Agrégateur de tableau**. Sélectionnez ensuite l’icône **clé à molette** et sélectionnez **Ajouter un routeur**. Vous effectuez cette opération, car après avoir vérifié le statut du fichier Photoshop, il doit y avoir 2 chemins d’accès. Si le statut est `succeeded`, la variable de **done** doit être définie sur `true`. Si le statut n’est pas égal à `succeeded`, la boucle doit continuer. Le routeur va permettre de vérifier et de régler cela.

![WF Fusion](./images/wffusion113.png)

Après avoir ajouté le routeur, sélectionnez l’icône **clé à molette** et sélectionnez **Configurer un filtre**.

![WF Fusion](./images/wffusion114.png)

Pour l’étiquette, utilisez **Nous avons terminé**. Définissez la **Condition** à l’aide de la réponse du nœud **Statut de la vérification Photoshop** en choisissant le champ de réponse **data.output[].status**. L’opérateur doit être défini sur **Égal à** et la valeur doit être `succeeded`. Sélectionnez **OK**.

![WF Fusion](./images/wffusion115.png)

Sélectionnez ensuite le nœud vide avec le point d’interrogation et recherchez **outils**. Sélectionnez ensuite **Outils**.

![WF Fusion](./images/wffusion116.png)

Sélectionnez **Définir plusieurs variables**.

![WF Fusion](./images/wffusion117.png)

Lorsque cette branche du routeur est utilisée, cela signifie que le statut de la création du fichier Photoshop est terminé avec succès. Cela signifie que la boucle do...while n’a plus besoin de continuer à vérifier le statut dans Photoshop. Vous devez donc définir la variable `done` sur `true`.

Pour le **Nom de variable**, utilisez `done`.

Pour la **Valeur de variable**, vous devez utiliser la valeur booléenne `true`. Sélectionnez l’icône **engrenage** puis sélectionnez `true`. Sélectionnez **Ajouter**.

![WF Fusion](./images/wffusion118.png)

Sélectionnez **OK**.

![WF Fusion](./images/wffusion119.png)

Cliquez ensuite avec le bouton droit sur le nœud **Définir plusieurs variables** que vous venez de créer et sélectionnez **Cloner**.

![WF Fusion](./images/wffusion120.png)

Faites glisser le nœud cloné afin qu’il se connecte à l’**agrégateur de tableau**. Cliquez ensuite avec le bouton droit sur le nœud et sélectionnez **Renommer**, puis remplacez le nom par `Placeholder End`.

![WF Fusion](./images/wffusion122.png)

Supprimez la variable existante et sélectionnez **+ Ajouter un élément**. Pour l’**Nom de variable**, utilisez `placeholder`. Pour l’**Valeur de variable**, utilisez `end`. Sélectionnez **Ajouter** puis sélectionnez **OK**.

![WF Fusion](./images/wffusion123.png)

Sélectionnez **Enregistrer** pour enregistrer votre scénario. Sélectionnez ensuite   **Exécuter une fois**.

![WF Fusion](./images/wffusion124.png)

Votre scénario est ensuite exécuté et doit se terminer correctement. Notez que la boucle do...while que vous avez configurée fonctionne correctement. Dans l’exécution ci-dessous, vous pouvez constater que le **Répéteur** s’est exécuté 20 fois en fonction de la bulle sur le nœud **Outils > Obtenir plusieurs variables**. Après ce nœud, vous avez configuré un filtre qui vérifiait le statut et les nœuds suivants ont été exécutés uniquement si le statut n’était pas égal à **réussi**. Dans cette exécution, la partie suivant le filtre ne s’est exécutée qu’une seule fois, car le statut était déjà **réussi** lors de la première exécution.

![WF Fusion](./images/wffusion125.png)

Vous pouvez vérifier le statut de la création de votre nouveau fichier Photoshop en cliquant sur la bulle dans la requête HTTP **Vérification du statut de Photoshop** et en accédant au champ **statut**.

![WF Fusion](./images/wffusion126.png)

Vous avez maintenant configuré la version de base d’un scénario répétable qui automatise un certain nombre d’étapes. Dans l’exercice suivant, vous allez en reparler en ajoutant de la complexité.

## Étapes suivantes

Accédez à [&#x200B; Automatisation des processus avec Workfront Fusion &#x200B;](./ex3.md){target="_blank"}

Revenez à l’automatisation des workflows Creative [avec Workfront Fusion](./automation.md){target="_blank"}

Revenir à [Tous les modules](./../../../overview.md){target="_blank"}
