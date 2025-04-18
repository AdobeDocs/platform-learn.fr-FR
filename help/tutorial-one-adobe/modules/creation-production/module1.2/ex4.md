---
title: Automatisation à l’aide de connecteurs
description: Automatisation à l’aide de connecteurs
role: Developer
level: Beginner
jira: KT-5342
doc-type: Tutorial
exl-id: 0b20ba91-28d4-4f4d-8abe-074f802c389e
source-git-commit: 156725fe0f89d97f109de1518f7fa79ffd7cea41
workflow-type: tm+mt
source-wordcount: '2050'
ht-degree: 1%

---

# 1.2.4 Automatisation à l&#39;aide de connecteurs

Vous allez maintenant commencer à utiliser les connecteurs prêts à l’emploi dans Workfront Fusion for Photoshop et vous allez connecter la requête Texte-2-Image de Firefly et les requêtes Photoshop dans un seul scénario.

## 1.2.4.1 Dupliquer et préparer votre scénario

Dans le menu de gauche, accédez à **Scénarios** et sélectionnez votre dossier `--aepUserLdap--`. Vous devriez ensuite voir le scénario que vous avez créé précédemment, qui est nommé `--aepUSerLdap-- - Adobe I/O Authentication`.

![WF Fusion](./images/wffc1.png)

Cliquez sur la flèche pour ouvrir le menu déroulant et sélectionnez **Cloner**.

![WF Fusion](./images/wffc2.png)

Définissez le **Nom** du scénario cloné sur `--aepUserLdap-- - Firefly + Photoshop` et sélectionnez l’équipe **cible** appropriée. Cliquez sur **Ajouter** pour ajouter un nouveau webhook.

![WF Fusion](./images/wffc3.png)

Définissez le **nom du Webhook** sur `--aepUserLdap-- - Firefly + Photoshop Webhook`. Cliquez sur **Enregistrer**.

![WF Fusion](./images/wffc4.png)

Vous devriez alors voir ceci. Cliquez sur **Enregistrer**.

![WF Fusion](./images/wffc5.png)

Vous devriez alors voir ceci. Cliquez sur le module **Webhook**.

![WF Fusion](./images/wffc6.png)

Cliquez sur **Copier l’adresse dans le presse-papiers** puis sur **Redéterminer la structure des données**.

![WF Fusion](./images/wffc7.png)

Ouvrez Postman. Ajoutez une nouvelle requête dans le même dossier que celui que vous utilisiez auparavant.

![WF Fusion](./images/wffc9.png)

Vérifiez que les paramètres suivants sont appliqués :

- Nom de la requête : `POST - Send Request to Workfront Fusion Webhook Firefly + Photoshop`
- Type de demande : `POST`
- URL de requête : collez l’URL que vous avez copiée à partir du webhook de votre scénario Workfront Fusion.

Accédez à **Body** et définissez **Body Type** sur **raw** - **JSON**. Collez la payload suivante dans le **corps**.

```json
{
    "psdTemplate": "citisignal-fiber.psd",
    "xlsFile": "placeholder",
    "prompt":"misty meadows",
    "cta": "Buy this now!",
    "button": "Click here to buy!"
}
```

Cette nouvelle payload garantit que toutes les informations de variable sont fournies depuis l’extérieur du scénario, au lieu d’être codées en dur dans le scénario. Dans un scénario d’entreprise, une organisation a besoin qu’un scénario soit défini de manière réutilisable, ce qui signifie qu’un certain nombre de variables doivent être fournies en tant que variables d’entrée au lieu d’être codées en dur dans le scénario.

Tu devrais avoir ça. Cliquez sur **Envoyer**.

![WF Fusion](./images/wffc10.png)

Le webhook Workfront Fusion n’a pas encore été saisi.

![WF Fusion](./images/wffc11.png)

Une fois que vous avez cliqué sur **Envoyer**, le message doit passer à **Déterminé avec succès**. Cliquez sur **OK**.

![WF Fusion](./images/wffc12.png)

## 1.2.4.2 Mettre à jour le module Firefly T2I

Cliquez avec le bouton droit sur le module **Firefly T2I** et sélectionnez **Supprimer le module**.

![WF Fusion](./images/wffcff1.png)

Cliquez sur l’icône **+**, saisissez le `firefly` de terme de recherche, puis sélectionnez **Adobe Firefly**.

![WF Fusion](./images/wffcff2.png)

Sélectionnez **Générer une image**.

![WF Fusion](./images/wffcff3.png)

Faites glisser et déposez le module **Adobe Firefly** afin qu&#39;il se connecte au module **Router**.

![WF Fusion](./images/wffcff4.png)

Cliquez sur le module **Adobe Firefly** pour l&#39;ouvrir, puis sur **Ajouter** pour créer une nouvelle connexion.

![WF Fusion](./images/wffcff5.png)

Renseignez les champs suivants :

- **Nom de la connexion** : utilisez `--aepUserLdap-- - Firefly connection`.
- **Environnement** : utilisez **Production**.
- **Type** : utilisez **Compte personnel**.
- **ID client** : copiez le **ID client** de votre projet Adobe I/O nommé `--aepUserLdap-- - One Adobe tutorial`.
- **Secret client** : copiez le **Secret client** de votre projet Adobe I/O nommé `--aepUserLdap-- - One Adobe tutorial`.

Vous trouverez les **ID client** et **Secret client** de votre projet Adobe I/O [ici](https://developer.adobe.com/console/projects.).

![WF Fusion](./images/wffc20.png)

Une fois tous les champs remplis, cliquez sur **Continuer**. Votre connexion sera alors automatiquement validée.

![WF Fusion](./images/wffcff6.png)

Sélectionnez ensuite la variable **invite** fournie au scénario par le **Webhook personnalisé** entrant. Cliquez sur **OK**.

![WF Fusion](./images/wffcff7.png)

Avant de continuer, vous devez désactiver l&#39;ancien itinéraire dans le scénario car pour cet exercice, vous n&#39;utiliserez que le nouvel itinéraire que vous êtes en train de configurer. Pour ce faire, cliquez sur l’icône **clé à molette** entre le module **Router** et le module **Iterator**, puis sélectionnez **Désactiver l’itinéraire**.

![WF Fusion](./images/wffcff7a.png)

Cliquez sur **Enregistrer** pour enregistrer vos modifications, puis sur **Exécuter une fois** pour tester votre configuration.

![WF Fusion](./images/wffcff8.png)

Accédez à Postman, vérifiez l’invite dans votre demande, puis cliquez sur **Envoyer**.

![WF Fusion](./images/wffcff8a.png)

Une fois que vous avez cliqué sur Envoyer, revenez à Workfront Fusion et cliquez sur l’icône de bulle dans le module **Adobe Firefly** pour vérifier les détails.

![WF Fusion](./images/wffcff9.png)

Accédez à **OUTPUT** dans **Details** > **url** pour rechercher l’URL de l’image générée par **Adobe Firefly**.

![WF Fusion](./images/wffcff10.png)

Vous devriez maintenant voir une image qui représente l’invite que vous avez envoyée à partir de la demande de Postman, dans ce cas **misty meadows**.

![WF Fusion](./images/wffcff11.png)

## 1.2.4.2 Modifier l’arrière-plan du fichier PSD

Vous allez maintenant mettre à jour votre scénario pour le rendre plus intelligent en utilisant davantage de connecteurs prêts à l’emploi. Vous connecterez également la sortie de Firefly à Photoshop, de sorte que l’image d’arrière-plan du fichier PSD change dynamiquement à l’aide de la sortie de l’action Générer une image de Firefly.

Vous devriez alors voir ceci. Ensuite, passez la souris sur le module **Adobe Firefly** et cliquez sur l’icône **+**.

![WF Fusion](./images/wffc15.png)

Dans le menu de recherche, saisissez `Photoshop`, puis cliquez sur l’action **Adobe Photoshop**.

![WF Fusion](./images/wffc16.png)

Sélectionnez **Appliquer les modifications PSD**.

![WF Fusion](./images/wffc17.png)

Vous devriez alors voir ceci. Cliquez sur **Ajouter** pour ajouter une nouvelle connexion à Adobe Photoshop.

![WF Fusion](./images/wffc18.png)

Configurez votre connexion comme suit :

- Type de connexion : sélectionnez **Adobe Photoshop (serveur à serveur)**
- Nom de la connexion : saisissez `--aepUserLdap-- - Adobe IO`
- Identifiant client : collez votre identifiant client
- Secret client : collez votre secret client

Cliquez sur **Continuer**.

![WF Fusion](./images/wffc19.png)

Pour rechercher votre **ID client** et **Secret client**, accédez à [https://developer.adobe.com/console/home](https://developer.adobe.com/console/home){target="_blank"} puis ouvrez votre projet Adobe I/O, nommé `--aepUserLdap-- One Adobe tutorial`. Accédez à **OAuth de serveur à serveur** pour trouver votre ID client et votre secret client. Copiez ces valeurs et collez-les dans la configuration de la connexion dans Workfront Fusion.

![WF Fusion](./images/wffc20.png)

Après avoir cliqué sur **Continuer**, une fenêtre contextuelle s’affiche brièvement pendant la vérification de vos informations d’identification. Une fois cette opération terminée, vous devriez voir ceci.

![WF Fusion](./images/wffc21.png)

Vous devez maintenant saisir l’emplacement du fichier PSD que vous souhaitez que Fusion utilise. Pour **Stockage**, sélectionnez **Azure** et pour **Emplacement du fichier**, saisissez `{{1.AZURE_STORAGE_URL}}/{{1.AZURE_STORAGE_CONTAINER}}/{{1.AZURE_STORAGE_SAS_READ}}`. Placez le curseur en regard de la deuxième `/`. Ensuite, examinez les variables disponibles et faites défiler l’écran vers le bas pour trouver la variable **psdTemplate**. Cliquez sur la variable **psdTemplate** pour la sélectionner.

![WF Fusion](./images/wffc22.png)

Vous devriez alors voir ceci.

![WF Fusion](./images/wffc23.png)

Faites défiler l’écran jusqu’à afficher **Calques**. Cliquez sur **Ajouter un élément**.

![WF Fusion](./images/wffc24.png)

Vous devriez alors voir ceci. Vous devez maintenant saisir le nom du calque dans votre modèle Photoshop PSD utilisé pour l’arrière-plan du fichier.

![WF Fusion](./images/wffc25.png)

Dans le fichier **citisignal-fibre.psd**, vous trouverez le calque utilisé pour l&#39;arrière-plan. Dans cet exemple, ce calque est nommé **2048x2048-background**.

![WF Fusion](./images/wffc26.png)

Collez le nom **2048x2048-background** dans la boîte de dialogue Workfront Fusion.

![WF Fusion](./images/wffc27.png)

Faites défiler vers le bas jusqu’à afficher **Entrée**. Vous devez maintenant définir ce qui doit être inséré dans le calque d’arrière-plan. Dans ce cas, vous devez sélectionner la sortie du module **Adobe Firefly**, qui contient l&#39;image générée dynamiquement.

Pour **Storage**, sélectionnez **External**. Pour **Emplacement du fichier**, copiez et collez la variable `{{XX.details[].url}}` à partir de la sortie du module **Adobe Firefly**. Remplacez **XX** dans la variable par le numéro de séquence du module **Adobe Firefly**, qui est dans cet exemple **22**.

![WF Fusion](./images/wffc28.png)

Faites ensuite défiler l’écran vers le bas jusqu’à afficher **Modifier**. Définissez **Modifier** sur **Oui** et **Type** sur **Calque**. Cliquez sur **Ajouter**.

![WF Fusion](./images/wffc29.png)

Vous devriez alors voir ceci. Vous devez ensuite définir la sortie de l’action. Cliquez sur **Ajouter un élément** sous **sorties**.

![WF Fusion](./images/wffc30.png)

Sélectionnez **Azure** pour **Stockage**, collez ce `{{1.AZURE_STORAGE_URL}}/{{1.AZURE_STORAGE_CONTAINER}}/citisignal-fiber-replacedbg.psd{{1.AZURE_STORAGE_SAS_WRITE}}` sous **Emplacement du fichier** et sélectionnez **vnd.adobe.photoshop** sous **Type**. Cliquez pour activer **Afficher les paramètres avancés**.

![WF Fusion](./images/wffc31.png)

Sous **Paramètres avancés**, sélectionnez **Oui** pour remplacer les fichiers portant le même nom.
Cliquez sur **Ajouter**.

![WF Fusion](./images/wffc32.png)

Tu devrais avoir ça. Cliquez sur **OK**.

![WF Fusion](./images/wffc33.png)

Cliquez sur **Enregistrer** pour enregistrer vos modifications, puis sur **Exécuter une fois** pour tester votre configuration.

![WF Fusion](./images/wffc33a.png)

Accédez à Postman, vérifiez l’invite dans votre demande, puis cliquez sur **Envoyer**.

![WF Fusion](./images/wffcff8a.png)

Vous devriez alors voir ceci. Cliquez sur la bulle dans le module **Adobe Photoshop - Apply PSD edits**.

![WF Fusion](./images/wffc33b.png)

Vous pouvez maintenant constater qu’un nouveau fichier PSD a été généré et stocké dans votre compte de stockage Azure Microsoft.

![WF Fusion](./images/wffc33c.png)

## 1.2.4.3 Modifier les calques de texte du fichier PSD

### Texte De L’Appel À L’Action

Ensuite, passez la souris sur le module **Adobe Photoshop - Apply PSD edits** et cliquez sur l’icône **+**.

![WF Fusion](./images/wffc34.png)

Sélectionnez **Adobe Photoshop**.

![WF Fusion](./images/wffc35.png)

Sélectionnez **Modifier les calques de texte**.

![WF Fusion](./images/wffc36.png)

Vous devriez alors voir ceci. Tout d’abord, sélectionnez votre connexion Adobe Photoshop déjà configurée, qui doit être nommée `--aepUserLdap-- Adobe IO`.

Vous devez maintenant définir l’emplacement du fichier **Input**, qui est la sortie de l’étape précédente. Sous **Calques**, vous devez saisir le **Nom** du calque de texte à modifier.

![WF Fusion](./images/wffc37.png)

Pour le **Fichier d’entrée**, sélectionnez **Azure** pour le **Stockage de fichier d’entrée** et veillez à sélectionner la sortie de la requête précédente, **Adobe Photoshop - Appliquer les modifications de PSD**, que vous pouvez prendre à partir d’ici : `data[]._links.renditions[].href`

![WF Fusion](./images/wffc37a.png)

Ouvrez le fichier **citisignal-fibre.psd**. Dans le fichier , vous remarquerez que le calque contenant l’appel à l’action est nommé **2048x2048-cta**.

![WF Fusion](./images/wffc38.png)

Saisissez le nom **2048x2048-cta** sous **Nom** dans la boîte de dialogue.

![WF Fusion](./images/wffc39.png)

Faites défiler vers le bas jusqu’à afficher **Texte** > **Contenu**. Sélectionnez la variable **cta** dans la payload du Webhook.

![WF Fusion](./images/wffc40.png)

Faites défiler jusqu’à afficher **Output**. Pour **Stockage**, sélectionnez **Azure**. Pour **Emplacement du fichier**, saisissez l’emplacement ci-dessous. Notez l’ajout de la variable `{{timestamp}}` au nom de fichier. Celle-ci est utilisée pour s’assurer que chaque fichier généré a un nom unique. Définissez également la variable **Type** sur **vnd.adobe.photoshop**. Cliquez sur **OK**.

`{{1.AZURE_STORAGE_URL}}/{{1.AZURE_STORAGE_CONTAINER}}/citisignal-fiber-changed-text-{{timestamp}}.psd{{1.AZURE_STORAGE_SAS_WRITE}}`

![WF Fusion](./images/wffc41.png)

### Texte du bouton

Cliquez avec le bouton droit sur le module que vous venez de créer et sélectionnez **Cloner**. Un second module similaire sera créé.

![WF Fusion](./images/wffc42.png)

Connectez le module cloné au module **Adobe Photoshop - Modifier les calques de texte** précédent.

![WF Fusion](./images/wffc42a.png)

Vous devriez alors voir ceci. Tout d’abord, sélectionnez votre connexion Adobe Photoshop déjà configurée, qui doit être nommée `--aepUserLdap-- Adobe IO`.

Vous devez maintenant définir l’emplacement du fichier **Input**, qui est la sortie de l’étape précédente. Sous **Calques**, vous devez saisir le **Nom** du calque de texte à modifier.

![WF Fusion](./images/wffc43.png)

Pour le **fichier d’entrée**, sélectionnez **Azure** pour le **stockage de fichier d’entrée** et veillez à sélectionner la sortie de la requête précédente, **Adobe Photoshop - Modifier les calques de texte**, que vous pouvez prendre à partir d’ici : `data[]._links.renditions[].href`

Ouvrez le fichier **citisignal-fibre.psd**. Dans le fichier , vous remarquerez que le calque contenant l’appel à l’action est nommé **2048x2048-button-text**.

![WF Fusion](./images/wffc44.png)

Saisissez le nom **2048x2048-button-text** sous **Name** dans la boîte de dialogue.

![WF Fusion](./images/wffc43.png)

Faites défiler vers le bas jusqu’à afficher **Texte** > **Contenu**. Sélectionnez la variable **button** dans la payload Webhook.

![WF Fusion](./images/wffc45.png)

Faites défiler jusqu’à afficher **Output**. Pour **Stockage**, sélectionnez **Azure**. Pour **Emplacement du fichier**, saisissez l’emplacement ci-dessous. Notez l’ajout de la variable `{{timestamp}}` au nom de fichier. Celle-ci est utilisée pour s’assurer que chaque fichier généré a un nom unique. Définissez également la variable **Type** sur **vnd.adobe.photoshop**. Cliquez sur **OK**.

`{{1.AZURE_STORAGE_URL}}/{{1.AZURE_STORAGE_CONTAINER}}/citisignal-fiber-changed-text-{{timestamp}}.psd{{1.AZURE_STORAGE_SAS_WRITE}}`

![WF Fusion](./images/wffc46.png)

Cliquez sur **Enregistrer** pour enregistrer vos modifications.

![WF Fusion](./images/wffc47.png)

## 1.2.4.4 la réponse du Webhook

Après avoir appliqué ces modifications à votre fichier Photoshop, vous devez configurer une **réponse Webhook** qui sera renvoyée à l’application qui a activé ce scénario.

Pointez sur le module **Adobe Photoshop - Modifier les calques de texte** puis cliquez sur l’icône **+**.

![WF Fusion](./images/wffc48.png)

Recherchez `webhooks` et sélectionnez **Webhook**.

![WF Fusion](./images/wffc49.png)

Sélectionnez **Réponse du Webhook**.

![WF Fusion](./images/wffc50.png)

Vous devriez alors voir ceci. Collez la payload ci-dessous dans **Body**.

```json
{
    "newPsdTemplate": ""
}
```

![WF Fusion](./images/wffc51.png)

Copiez et collez la variable `{{XX.data[]._links.renditions[].href}}` et remplacez **XX** par le numéro de séquence du dernier module **Adobe Photoshop - Modifier les calques de texte**, qui est dans ce cas **25**. Cochez la case **Afficher les paramètres avancés** puis cliquez sur **Ajouter un élément**.

![WF Fusion](./images/wffc52.png)

Dans le champ **Clé**, saisissez `Content-Type`. Dans le champ **Valeur**, saisissez `application/json`. Cliquez sur **Ajouter**.

![WF Fusion](./images/wffc52a.png)

Tu devrais avoir ça. Cliquez sur **OK**.

![WF Fusion](./images/wffc53.png)

Cliquez sur **Alignement automatique**.

![WF Fusion](./images/wffc54.png)

Vous devriez alors voir ceci. Cliquez sur **Enregistrer** pour enregistrer vos modifications, puis sur **Exécuter une fois** pour tester votre scénario.

![WF Fusion](./images/wffc55.png)

Revenez à Postman et cliquez sur **Envoyer**. L’invite utilisée ici est **prairies brumeuses**.

![WF Fusion](./images/wffc56.png)

Le scénario sera alors activé et, au bout d’un certain temps, une réponse contenant l’URL du fichier PSD nouvellement créé s’affichera dans Postman.

![WF Fusion](./images/wffc58.png)

Pour rappel : une fois le scénario exécuté dans Workfront Fusion, vous serez en mesure d’afficher des informations sur chaque module en cliquant sur la bulle au-dessus de chaque module.

![WF Fusion](./images/wffc59.png)

À l’aide de l’explorateur de stockage Azure, vous pouvez ensuite rechercher et ouvrir le fichier PSD nouvellement créé en double-cliquant dessus dans l’explorateur de stockage Azure.

![WF Fusion](./images/wffc60.png)

Votre fichier doit alors ressembler à ceci, avec l’arrière-plan qui est remplacé par un arrière-plan avec des **prairies brumeuses**.

![WF Fusion](./images/wffc61.png)

Si vous exécutez à nouveau votre scénario, puis envoyez une nouvelle requête depuis Postman à l’aide d’une autre invite, vous verrez à quel point votre scénario est devenu facile et réutilisable. Dans cet exemple, la nouvelle invite utilisée est **Sunny Desert**.

![WF Fusion](./images/wffc62.png)

Quelques minutes plus tard, un nouveau fichier PSD a été généré avec un nouvel arrière-plan.

![WF Fusion](./images/wffc63.png)

## Étapes suivantes

Accédez à [1.2.5 Frame.io et Workfront Fusion](./ex5.md){target="_blank"}

Revenez à l’automatisation des workflows Creative [avec Workfront Fusion](./automation.md){target="_blank"}

Revenir à [Tous les modules](./../../../overview.md){target="_blank"}
