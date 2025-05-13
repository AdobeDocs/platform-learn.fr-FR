---
title: Frame.io et Workfront Fusion
description: Frame.io et Workfront Fusion
role: Developer
level: Beginner
jira: KT-5342
doc-type: Tutorial
exl-id: 37de6ceb-833e-4e75-9201-88bddd38a817
source-git-commit: da6917ec8c4e863e80eef91280e46b20816a5426
workflow-type: tm+mt
source-wordcount: '2674'
ht-degree: 0%

---

# 1.2.5 Frame.io et Workfront Fusion

Dans l’exercice précédent, vous avez configuré le `--aepUserLdap-- - Firefly + Photoshop` de scénario et configuré un webhook entrant pour déclencher le scénario, ainsi qu’une réponse webhook une fois le scénario terminé avec succès. Vous avez ensuite utilisé Postman pour déclencher ce scénario. Postman est un excellent outil de test, mais dans un scénario d’entreprise réel, les utilisateurs professionnels n’utiliseraient pas Postman pour déclencher un scénario. Au lieu de cela, ils utiliseraient une autre application et s’attendraient à ce que cette autre application active un scénario dans Workfront Fusion. Dans cet exercice, c&#39;est exactement ce que vous allez faire avec Frame.io.

>[!NOTE]
>
>Pour réussir cet exercice, vous devez être un utilisateur administrateur dans votre compte Frame.io. L’exercice ci-dessous a été créé pour Frame.io V3 et sera mis à jour ultérieurement pour Frame.io V4.

## 1.2.5.1 Accès à Frame.io

Accédez à [https://app.frame.io/projects](https://app.frame.io/projects){target="_blank"}.

Cliquez sur l’icône **+** créer votre propre projet dans Frame.io.

![E/S de trame](./images/frame1.png)

Saisissez le nom `--aepUserLdap--` et cliquez sur **Créer un projet**.

![E/S de trame](./images/frame2.png)

Votre projet s’affiche alors dans le menu de gauche.
Dans l’un des exercices précédents, vous avez téléchargé [citisignal-fibre.psd](./../../../assets/ff/citisignal-fiber.psd){target="_blank"} sur votre bureau. Sélectionnez ce fichier, puis faites-le glisser et déposez-le dans le dossier du projet qui vient d’être créé.

![E/S de trame](./images/frame3.png)

## 1.2.5.2 Workfront Fusion et Frame.io

Dans l’exercice précédent, vous avez créé l’`--aepUserLdap-- - Firefly + Photoshop` de scénario, qui a commencé par un webhook personnalisé et s’est terminé par une réponse webhook. L’utilisation des webhooks a ensuite été testée à l’aide de Postman, mais il est évident que le but d’un tel scénario est d’être appelé par une application externe. Comme indiqué précédemment, Frame.io sera cet exercice, mais entre Frame.io et le `--aepUserLdap-- - Firefly + Photoshop`, un autre scénario Workfront Fusion est nécessaire. vous allez à présent configurer ce scénario.

Accédez à [https://experience.adobe.com/](https://experience.adobe.com/){target="_blank"}. Ouvrez **Workfront Fusion**.

![WF Fusion](./images/wffusion1.png)

Dans le menu de gauche, accédez à **Scénarios** et sélectionnez votre dossier `--aepUserLdap--`. Cliquez sur **Créer un nouveau scénario**.

![E/S de trame](./images/frame4.png)

Utilisez le nom `--aepUserLdap-- - Frame IO Custom Action`.

![E/S de trame](./images/frame5.png)

Cliquez sur l’**objet de point d’interrogation** sur la zone de travail. Saisissez le `webhook` de texte dans la zone de recherche, puis cliquez sur **Webhooks**.

![E/S de trame](./images/frame6.png)

Cliquez sur **Webhook personnalisé**.

![E/S de trame](./images/frame7.png)

Cliquez sur **Ajouter** pour créer une URL webhook.

![E/S de trame](./images/frame8.png)

Pour le **nom du Webhook**, utilisez `--aepUserLdap-- - Frame IO Custom Action Webhook`. Cliquez sur **Enregistrer**.

![E/S de trame](./images/frame9.png)

Vous devriez alors voir ceci. Laissez cet écran ouvert et intact car vous en aurez besoin lors d&#39;une prochaine étape. Vous devrez copier l’URL du webhook à l’étape suivante, en cliquant sur **Copier l’adresse dans le presse-papiers**.

![E/S de trame](./images/frame10.png)

Accédez à [https://developer.frame.io/](https://developer.frame.io/){target="_blank"}. Cliquez sur **OUTILS DE DÉVELOPPEMENT** puis choisissez **Actions personnalisées**.

![E/S de trame](./images/frame11.png)

Cliquez sur **Créer une action personnalisée**.

![E/S de trame](./images/frame12.png)

Saisissez les valeurs suivantes :

- **NAME** : utilisez `--aepUserLdap-- - Frame IO Custom Action Fusion`
- **DESCRIPTION** : utilisez `--aepUserLdap-- - Frame IO Custom Action Fusion`
- **EVENT** : utilisez `fusion.tutorial`.
- **URL** : saisissez l’URL du webhook que vous venez de créer dans Workfront Fusion
- **ÉQUIPE** : sélectionnez l’équipe Frame.io appropriée, dans ce cas, **Un tutoriel Adobe**.

Cliquez sur **Envoyer**.

![E/S de trame](./images/frame15.png)

Vous devriez alors voir ceci.

![E/S de trame](./images/frame14.png)

Revenez à [https://app.frame.io/projects](https://app.frame.io/projects){target="_blank"}. Actualisez la page.

![E/S de trame](./images/frame16.png)

Après avoir actualisé la page, cliquez sur le **de 3 points...** sur la ressource **citisignal-fibre.psd**. L’action personnalisée que vous avez créée précédemment devrait alors apparaître dans le menu qui s’affiche. Cliquez sur le `--aepUserLdap-- - Frame IO Custom Action Fusion` d’action personnalisée.

![E/S de trame](./images/frame17.png)

Vous devriez alors voir un **Succès !Fenêtre contextuelle**. Cette fenêtre contextuelle est le résultat de la communication entre Frame.io et Workfront Fusion.

![E/S de trame](./images/frame18.png)

Redéfinissez l’écran sur Workfront Fusion. Vous devriez maintenant voir **Déterminé avec succès** apparaître dans l’objet Webhook personnalisé. Cliquez sur **OK**.

![E/S de trame](./images/frame19.png)

Cliquez sur **Exécuter une fois** pour activer le mode test, puis testez à nouveau la communication avec Frame.io.

![E/S de trame](./images/frame20.png)

Revenez à Frame.io et cliquez de nouveau sur le `--aepUserLdap-- - Frame IO Custom Action Fusion` d’action personnalisée.

![E/S de trame](./images/frame21.png)

Rebasculez l’écran sur Workfront Fusion. Vous devriez maintenant voir une coche verte et une bulle indiquant **1**. Cliquez sur la bulle pour afficher les détails.

![E/S de trame](./images/frame22.png)

La vue détaillée de la bulle vous montre les données reçues de Frame.io. Vous devriez voir différents ID. Par exemple, le champ **resource.id** affiche l’ID unique dans Frame.io de la ressource **citisignal-fibre.psd**.

![E/S de trame](./images/frame23.png)

Maintenant que la communication a été établie entre Frame.io et Workfront Fusion, vous pouvez continuer votre configuration.

## 1.2.5.3 Fournir une réponse de formulaire personnalisé à Frame.io

Lorsque l’action personnalisée est appelée dans Frame.io, Frame.io s’attend à recevoir une réponse de Workfront Fusion. Si vous repensez au scénario que vous avez créé dans l’exercice précédent, un certain nombre de variables sont nécessaires pour mettre à jour le fichier PSD Photoshop standard. Ces variables sont définies dans la payload que vous avez utilisée :

```json
{
    "psdTemplate": "citisignal-fiber.psd",
    "xlsFile": "placeholder",
    "prompt":"misty meadows",
    "cta": "Buy this now!",
    "button": "Click here to buy!"
}
```

Pour que le `--aepUserLdap-- - Firefly + Photoshop` de scénario s’exécute correctement, des champs tels que **prompt**, **cta**, **button** et **psdTemplate** sont donc nécessaires.

Les 3 premiers champs **invite**, **cta**, **button** nécessitent une entrée utilisateur qui doit être collectée dans Frame.io lorsque l’utilisateur appelle l’action personnalisée. Ainsi, la première chose à faire dans Workfront Fusion est de vérifier si ces variables sont disponibles ou non et, dans le cas contraire, Workfront Fusion doit répondre à Frame.io pour demander la saisie de ces variables. Pour ce faire, utilisez un formulaire dans Frame.io.

Revenez à Workfront Fusion et ouvrez votre `--aepUserLdap-- - Frame IO Custom Action` de scénario. Pointez sur l’objet **Custom webhook** et cliquez sur l’icône **+** pour ajouter un autre module.

![E/S de trame](./images/frame24.png)

Recherchez `Flow Control` et cliquez sur **Contrôle de flux**.

![E/S de trame](./images/frame25.png)

Cliquez pour sélectionner **Router**.

![E/S de trame](./images/frame26.png)

Vous devriez alors voir ceci.

![E/S de trame](./images/frame27.png)

Cliquez sur le **?** objet , puis cliquez pour sélectionner **Webhooks**.

![E/S de trame](./images/frame28.png)

Sélectionnez **Réponse du Webhook**.

![E/S de trame](./images/frame29.png)

Vous devriez alors voir ceci.

![E/S de trame](./images/frame30.png)

Copiez le code JSON ci-dessous et collez-le dans le champ **Corps**.


```json
{
  "title": "What do you want Firefly to generate?",
  "description": "Enter your Firefly prompt.",
  "fields": [
    {
      "type": "text",
      "label": "Prompt",
      "name": "Prompt",
      "value": ""
    },
    {
      "type": "text",
      "label": "CTA Text",
      "name": "CTA Text",
      "value": ""
    },
    {
      "type": "text",
      "label": "Button Text",
      "name": "Button Text",
      "value": ""
    }
  ]
}
```

Cliquez sur l’icône pour nettoyer et embellir le code JSON. Cliquez ensuite sur **OK**.

![E/S de trame](./images/frame31.png)

Cliquez sur **Enregistrer** pour enregistrer vos modifications.

![E/S de trame](./images/frame32.png)

Vous devez ensuite configurer un filtre pour vous assurer que ce chemin d’accès au scénario s’exécute uniquement lorsqu’aucune invite n’est disponible. Cliquez sur l’icône **clé à molette**, puis sélectionnez **Configurer un filtre**.

![E/S de trame](./images/frame33.png)

Configurez les champs suivants :

- **Libellé** : utilisez `Prompt isn't available`.
- **Condition** : utilisez `{{1.data.Prompt}}`.
- **Opérateurs de base** : sélectionnez **N’existe pas**.

>[!NOTE]
>
>Les variables dans Workfront Fusion peuvent être spécifiées manuellement à l’aide de la syntaxe suivante : `{{1.data.Prompt}}`. Le nombre dans la variable fait référence au module dans le scénario. Dans cet exemple, vous pouvez constater que le premier module du scénario est appelé **Webhooks** et qu’il possède un numéro de séquence de **1**. Cela signifie que la variable `{{1.data.Prompt}}` accédera au champ **data.Prompt** à partir du module portant le numéro de séquence 1. Les numéros de séquence peuvent parfois être différents. Faites donc attention lorsque vous copiez/collez de telles variables et vérifiez toujours que le numéro de séquence utilisé est correct.

Cliquez sur **OK**.

![E/S de trame](./images/frame34.png)

Vous devriez alors voir ceci. Cliquez d’abord sur l’icône **Enregistrer**, puis sur **Exécuter une fois** pour tester votre scénario.

![E/S de trame](./images/frame35.png)

Vous devriez alors voir ceci.

![E/S de trame](./images/frame36.png)

Revenez à Frame.io et cliquez de nouveau sur le `--aepUserLdap-- - Frame IO Custom Action Fusion` d’action personnalisée sur la ressource **citisignal-fibre.psd**.

![E/S de trame](./images/frame37.png)

Vous devriez maintenant voir une invite dans Frame.io. Ne remplissez pas encore les champs et ne soumettez pas encore le formulaire. Cette invite s’affiche en fonction de la réponse de Workfront Fusion que vous venez de configurer.

![E/S de trame](./images/frame38.png)

Revenez à Workfront Fusion et cliquez sur la bulle dans le module **Réponse Webhook**. Sous **ENTRÉE**, vous verrez le corps contenant la payload JSON pour le formulaire. Cliquez de nouveau sur **Exécuter**.

![E/S de trame](./images/frame40.png)

Vous devriez alors revoir ceci.

![E/S de trame](./images/frame41.png)

Revenez à Frame.io et remplissez les champs comme indiqué. Cliquez sur **Envoyer**.

![E/S de trame](./images/frame39.png)

Vous devriez alors voir un **Succès !Fenêtre contextuelle**.

![E/S de trame](./images/frame42.png)

Revenez à Workfront Fusion et cliquez sur la bulle dans le module **Custom webhook**. Dans l’opération 1, sous **OUTPUT**, vous pouvez désormais voir un nouvel objet **data** qui contient des champs tels que **Button Text**, **CTA Text** et **Prompt**. Avec ces variables d’entrée utilisateur disponibles dans votre scénario, vous disposez de suffisamment de éléments pour continuer votre configuration.

![E/S de trame](./images/frame43.png)

## 1.2.5.4 Récupérer l&#39;emplacement du fichier à partir de Frame.io

Comme nous l’avons vu précédemment, des champs tels que **prompt**, **cta**, **button** et **psdTemplate** sont nécessaires au fonctionnement de ce scénario. Les 3 premiers champs sont déjà disponibles, mais le **psdTemplate** à utiliser est toujours manquant. Le **psdTemplate** référencera désormais un emplacement Frame.io car le fichier **citisignal-fibre.psd** est hébergé dans Frame.io. Pour récupérer l’emplacement de ce fichier, vous devez configurer et utiliser la connexion Frame.io dans Workfront Fusion.

Revenez à Workfront Fusion et ouvrez votre `--aepUserLdap-- - Frame IO Custom Action` de scénario. Survoler la **?** le module , cliquez sur l’icône **+** pour ajouter un autre module et recherchez des `frame`. Cliquez sur **Frame.io**.

![E/S de trame](./images/frame44.png)

Cliquez sur **Frame.io (hérité)**.

![E/S de trame](./images/frame45.png)

Cliquez sur **Obtenir une ressource**.

![E/S de trame](./images/frame46.png)

Pour utiliser la connexion Frame.io, vous devez d’abord la configurer. Cliquez sur **Ajouter** pour ce faire.

![E/S de trame](./images/frame47.png)

Ouvrez la liste déroulante **Type de connexion**.

![E/S de trame](./images/frame48.png)

Sélectionnez **Clé API Frame.io** et saisissez le nom `--aepUserLdap-- - Frame.io Token`.

![E/S de trame](./images/frame49.png)

Pour obtenir un jeton API, rendez-vous sur [https://developer.frame.io/](https://developer.frame.io/){target="_blank"}. Cliquez sur **OUTILS DE DÉVELOPPEMENT** puis choisissez **Jetons**.

![E/S de trame](./images/frame50.png)

Cliquez sur **Créer un jeton**.

![E/S de trame](./images/frame51.png)

Utilisez l’`--aepUserLdap-- - Frame.io Token` **Description** et cliquez sur **Sélectionner toutes les portées**.

![E/S de trame](./images/frame52.png)

Faites défiler vers le bas et cliquez sur **Envoyer**.

![E/S de trame](./images/frame53.png)

Votre jeton est maintenant créé. Cliquez sur **Copier** pour le copier dans le presse-papiers.

![E/S de trame](./images/frame54.png)

Revenez à votre scénario dans Workfront Fusion. Collez le jeton dans le champ **Votre clé API Frame.io**. Cliquez sur **OK**. Votre connexion sera maintenant testée par Workfront Fusion.

![E/S de trame](./images/frame55.png)

Si la connexion a été testée avec succès, elle s’affiche automatiquement sous **Connexion**. Vous disposez désormais d’une connexion réussie et vous devez terminer la configuration pour obtenir tous les détails de la ressource à partir de Frame.io, y compris l’emplacement du fichier. Pour ce faire, vous devez fournir l’**ID de ressource**.

![E/S de trame](./images/frame56.png)

Le **ID de ressource** est partagé par Frame.io avec Workfront Fusion dans le cadre de la communication initiale **Webhook personnalisé** et se trouve sous le champ **resource.id**. Sélectionnez **resource.id** et cliquez sur **OK**.

![E/S de trame](./images/frame57.png)

Vous devriez maintenant voir ceci. Enregistrez vos modifications, puis cliquez sur **Exécuter une fois** pour tester votre scénario.

![E/S de trame](./images/frame58.png)

Revenez à Frame.io et cliquez de nouveau sur le `--aepUserLdap-- - Frame IO Custom Action Fusion` d’action personnalisée sur la ressource **citisignal-fibre.psd**.

![E/S de trame](./images/frame37.png)

Vous devriez maintenant voir une invite dans Frame.io. Ne remplissez pas encore les champs et ne soumettez pas encore le formulaire. Cette invite s’affiche en fonction de la réponse de Workfront Fusion que vous venez de configurer.

![E/S de trame](./images/frame38.png)

Revenez à Workfront Fusion. Cliquez de nouveau sur **Exécuter**.

![E/S de trame](./images/frame59.png)

Revenez à Frame.io et remplissez les champs comme indiqué. Cliquez sur **Envoyer**.

![E/S de trame](./images/frame39.png)

Revenez à Workfront Fusion et cliquez sur la bulle dans le module **Frame.io - Obtenir une ressource**.

![E/S de trame](./images/frame60.png)

Vous pouvez désormais voir de nombreuses métadonnées sur la ressource spécifique **citisignal-fibre.psd**.

![E/S de trame](./images/frame61.png)

L’information spécifique nécessaire à ce cas d’utilisation est l’URL de l’emplacement du fichier **citisignal-fibre.psd**, que vous pouvez trouver en faisant défiler l’écran jusqu’au champ **Original**.

![E/S de trame](./images/frame62.png)

Vous disposez désormais de tous les champs (**invite**, **cta**, **button** et **psdTemplate**) nécessaires au fonctionnement de ce scénario.

## 1.2.5.5 Appeler le scénario Workfront

Dans l’exercice précédent, vous avez configuré le `--aepUserLdap-- - Firefly + Photoshop` de scénario. Vous devez maintenant apporter une modification mineure à ce scénario.

Ouvrez l’`--aepUserLdap-- - Firefly + Photoshop` du scénario dans un autre onglet et cliquez sur le premier module **Adobe Photoshop - Apply PSD edits**. Vous devriez maintenant voir que le fichier d’entrée est configuré pour utiliser un emplacement dynamique dans Microsoft Azure. Étant donné que pour ce cas d’utilisation, le fichier d’entrée n’est plus stocké dans Microsoft Azure, mais à la place à l’aide du stockage Frame.io, vous devez modifier ces paramètres.

![E/S de trame](./images/frame63.png)

Remplacez **Stockage** par **Externe** et **Emplacement du fichier** pour n’utiliser que la variable **psdTemplate** provenant du module **Custom webhook** entrant. Cliquez sur **OK** puis sur **Enregistrer** pour enregistrer vos modifications.

![E/S de trame](./images/frame64.png)

Cliquez sur le module **Webhook personnalisé**, puis sur **Copier l’adresse dans le presse-papiers**. Vous devez copier l’URL, car vous devrez l’utiliser dans l’autre scénario.

![E/S de trame](./images/frame65.png)

Revenez à votre `--aepUserLdap-- - Frame IO Custom Action` de scénario. Pointez sur le module **Frame.io - Obtenir une ressource** et cliquez sur l’icône **+**.

![E/S de trame](./images/frame66.png)

Saisissez `http`, puis cliquez sur **HTTP**.

![E/S de trame](./images/frame67.png)

Sélectionnez **Effectuer une requête**.

![E/S de trame](./images/frame68.png)

Collez l’URL du webhook personnalisé dans le champ **URL**. Définissez la **Méthode** sur POST**.

![E/S de trame](./images/frame69.png)

Définissez **Type de corps** sur **Brut** et **Type de contenu** sur **JSON (application/json)**.
Collez la payload JSON ci-dessous dans le champ **Demander le contenu** et cochez la case correspondant à **Analyser la réponse**.

```json
{
    "psdTemplate": "citisignal-fiber.psd",
    "xlsFile": "placeholder",
    "prompt":"misty meadows",
    "cta": "Buy this now!",
    "button": "Click here to buy!"
}
```

Une payload statique est désormais configurée, mais elle doit devenir dynamique à l’aide des variables collectées précédemment.

![E/S de trame](./images/frame70.png)

Pour le champ **psdTemplate**, remplacez la variable statique **citisignal-fibre.psd** par la variable **Original**.

![E/S de trame](./images/frame71.png)

Pour les champs **invite**, **cta** et **button**, remplacez les variables statiques par les variables dynamiques qui ont été insérées dans le scénario par la requête webhook entrante de Frame.io, à savoir les champs **data.Prompt**, **data.CTA Text** et **data.Button Text**.

Cliquez sur **OK**.

![E/S de trame](./images/frame72.png)

Cliquez sur **Enregistrer** pour enregistrer vos modifications.

![E/S de trame](./images/frame73.png)

## 1.2.5.6 Enregistrer une nouvelle ressource dans Frame.io

Une fois que l’autre scénario Workfront Fusion a été invoqué, un nouveau modèle Photoshop PSD est disponible. Ce fichier PSD doit être à nouveau stocké dans Frame.io, qui est la dernière étape de ce scénario.

Pointez sur le module **HTTP - Effectuer une requête** et cliquez sur l’icône **+**.

![E/S de trame](./images/frame74.png)

Sélectionnez **Frame.io (hérité)**.

![E/S de trame](./images/frame75.png)

Sélectionnez **Créer une ressource**.

![E/S de trame](./images/frame76.png)

Votre connexion Frame.io sera automatiquement sélectionnée.

![E/S de trame](./images/frame77.png)

Sélectionnez les options suivantes :

- **Identifiant de l’équipe** : sélectionnez l’identifiant de l’équipe approprié, dans ce cas `One Adobe Tutorial`.
- **Identifiant du projet** : utilisez `--aepUserLdap--`.
- **ID de dossier** : utilisez `root`.
- **Type** : utilisez `File`.

![E/S de trame](./images/frame78.png)

Pour le champ **Nom**, vous pouvez utiliser une variable telle que **horodatage** (ou la transformer en quelque chose de plus logique pour vous). La variable prédéfinie **horodatage** se trouve sous l’onglet **Date et heure**.

![E/S de trame](./images/frame79.png)

Pour le champ **URL Source**, utilisez le code JSON ci-dessous.

```json
{{6.data.newPsdTemplate}}
```

>[!NOTE]
>
>Les variables dans Workfront Fusion peuvent être spécifiées manuellement à l’aide de la syntaxe suivante : `{{6.data.newPsdTemplate}}`. Le nombre dans la variable fait référence au module dans le scénario. Dans cet exemple, vous pouvez constater que le sixième module du scénario s’appelle **HTTP - Effectuer une requête** et possède un numéro de séquence de **6**. Cela signifie que la variable `{{6.data.newPsdTemplate}}` accédera au champ **data.newPsdTemplate** à partir du module portant le numéro de séquence 6. Les numéros de séquence peuvent parfois être différents. Faites donc attention lorsque vous copiez/collez de telles variables et vérifiez toujours que le numéro de séquence utilisé est correct.

Cliquez sur **OK**.

![E/S de trame](./images/frame80.png)

Cliquez sur **Enregistrer** pour enregistrer vos modifications.

![E/S de trame](./images/frame81.png)

Enfin, vous devez configurer un filtre pour vous assurer que ce chemin du scénario s’exécute uniquement lorsqu’une invite est disponible. Cliquez sur l’icône **clé à molette**, puis sélectionnez **Configurer un filtre**.

![E/S de trame](./images/frame82.png)

Configurez les champs suivants :

- **Libellé** : utilisez `Prompt is available`.
- **Condition** : utilisez `{{1.data.Prompt}}`.
- **Opérateurs de base** : sélectionnez **existe**.

>[!NOTE]
>
>Les variables dans Workfront Fusion peuvent être spécifiées manuellement à l’aide de la syntaxe suivante : `{{1.data.Prompt}}`. Le nombre dans la variable fait référence au module dans le scénario. Dans cet exemple, vous pouvez constater que le premier module du scénario est appelé **Webhooks** et qu’il possède un numéro de séquence de **1**. Cela signifie que la variable `{{1.data.Prompt}}` accédera au champ **data.Prompt** à partir du module portant le numéro de séquence 1. Les numéros de séquence peuvent parfois être différents. Faites donc attention lorsque vous copiez/collez de telles variables et vérifiez toujours que le numéro de séquence utilisé est correct.

Cliquez sur **OK**.

![E/S de trame](./images/frame83.png)

Cliquez sur **Enregistrer** pour enregistrer vos modifications.

![E/S de trame](./images/frame84.png)

## 1.2.5.7 Tester votre cas d’utilisation de bout en bout

Cliquez sur **Exécuter une fois** dans votre `--aepUserLdap-- - Frame IO Custom Action` de scénario.

![E/S de trame](./images/frame85.png)

Revenez à Frame.io et cliquez de nouveau sur le `--aepUserLdap-- - Frame IO Custom Action Fusion` d’action personnalisée sur la ressource **citisignal-fibre.psd**.

![E/S de trame](./images/frame37.png)

Vous devriez maintenant voir une invite dans Frame.io. Ne remplissez pas encore les champs et ne soumettez pas encore le formulaire. Cette invite s’affiche en fonction de la réponse de Workfront Fusion que vous venez de configurer.

![E/S de trame](./images/frame38.png)

Revenez à Workfront Fusion. Cliquez sur **Exécuter une fois** dans votre `--aepUserLdap-- - Frame IO Custom Action` de scénario.

![E/S de trame](./images/frame86.png)

Dans Workfront Fusion, ouvrez l’`--aepUserLdap-- - Firefly + Photoshop` du scénario et cliquez également sur **Exécuter une fois** dans ce scénario.

![E/S de trame](./images/frame87.png)

Revenez à Frame.io et remplissez les champs comme indiqué. Cliquez sur **Envoyer**.

![E/S de trame](./images/frame39.png)

Après 1 à 2 minutes, une nouvelle ressource devrait apparaître automatiquement dans Frame.io. Double-cliquez sur la nouvelle ressource pour l’ouvrir.

![E/S de trame](./images/frame88.png)

Vous pouvez maintenant voir clairement que toutes les variables d’entrée utilisateur ont été automatiquement appliquées.

![E/S de trame](./images/frame89.png)

Vous avez maintenant terminé cet exercice avec succès.

## Étapes suivantes

Accédez à [1.2.6 Frame.io vers Fusion vers AEM Assets](./ex6.md){target="_blank"}

Revenez à l’automatisation des workflows Creative [avec Workfront Fusion](./automation.md){target="_blank"}

Revenir à [Tous les modules](./../../../overview.md){target="_blank"}

