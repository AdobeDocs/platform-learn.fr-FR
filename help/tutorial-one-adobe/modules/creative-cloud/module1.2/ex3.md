---
title: Automatisation des processus avec Workfront Fusion
description: Automatisation des processus avec Workfront Fusion
kt: 5342
doc-type: tutorial
exl-id: 1b7b2630-864f-4982-be5d-c46b760739c3
source-git-commit: f1f70a0e4ea3f59b5b121275e7db633caf953df9
workflow-type: tm+mt
source-wordcount: '989'
ht-degree: 0%

---

# 1.2.3 Automatisation des processus avec Workfront Fusion

Votre scénario ressemble maintenant à ceci.

![WF Fusion](./images/wffusion200.png)

## 1.2.3.1 Itération sur plusieurs valeurs

Jusqu’à présent, vous avez modifié le texte d’un fichier Photoshop par une valeur statique. Pour mettre à l’échelle et automatiser vos workflows de création de contenu, il est nécessaire d’effectuer une itération sur une liste de valeurs et d’insérer ces valeurs de manière dynamique dans le fichier Photoshop. Dans les étapes suivantes, vous allez ajouter une méthode pour effectuer une itération sur les valeurs de votre scénario existant.

Entre le nœud **Router** et le nœud **Photoshop Change Text**, cliquez sur l’icône **clé à molette** et sélectionnez **Ajouter un module**.

![WF Fusion](./images/wffusion201.png)

Recherchez `flow` et sélectionnez **Contrôle de flux**.

![WF Fusion](./images/wffusion202.png)

Sélectionnez **Itérateur**.

![WF Fusion](./images/wffusion203.png)

Tu devrais avoir ça.

![WF Fusion](./images/wffusion204.png)

Bien qu’il soit possible de lire des fichiers d’entrée tels que des fichiers CSV, vous devez pour l’instant utiliser une version de base d’un fichier CSV en définissant une chaîne de texte et en divisant ce fichier texte.

Vous pouvez trouver la fonction **split** en cliquant sur l’icône **T**, où vous pouvez voir toutes les fonctions disponibles pour manipuler les valeurs de texte. Cliquez sur la fonction **split** et vous devriez alors voir ceci.

![WF Fusion](./images/wffusion206.png)

La fonction split exige un tableau de valeurs avant le point-virgule et exige que vous spécifiiez le séparateur après le point-virgule. Pour ce test, vous devez utiliser un tableau simple avec 2 champs, **Acheter maintenant** et **Cliquer ici**, et le séparateur à utiliser est **,**.

Saisissez cette valeur dans le champ **Tableau** en remplaçant la fonction **split** actuellement vide : `{{split("Buy now, Click here "; ",")}}`. Cliquez sur **OK**.

![WF Fusion](./images/wffusion205.png)

Votre itérateur est maintenant configuré et si vous deviez exécuter votre scénario maintenant, il l’exécuterait deux fois. Un problème persiste cependant, car vous utilisez actuellement des valeurs statiques dans votre nœud **Texte de modification de Photoshop**. Cliquez sur **Photoshop Modifier le texte** pour ajouter des variables au lieu de valeurs statiques pour les champs d’entrée et de sortie.

![WF Fusion](./images/wffusion207.png)

Dans le **Demander du contenu**, le texte **Cliquez ici** s’affiche. Ce texte doit être remplacé par les valeurs provenant de votre tableau .

![WF Fusion](./images/wffusion208.png)

Supprimez le texte **Cliquez ici**, puis remplacez-le en sélectionnant la variable **Valeur** dans le nœud **Itérateur**. Cela permet de s’assurer que le texte du bouton dans votre document Photoshop est mis à jour de manière dynamique.

![WF Fusion](./images/wffusion209.png)

Vous devez également mettre à jour le nom du fichier utilisé pour écrire le fichier dans votre compte de stockage Azure. Si le nom de fichier est statique, chaque nouvelle itération remplacera simplement le fichier précédent et, par conséquent, vous perdrez les fichiers personnalisés. Le nom de fichier statique actuel est **citisignal-fibre-changed-text.psd** et vous devez maintenant le mettre à jour. Placez le curseur derrière le mot `text`.

![WF Fusion](./images/wffusion210.png)

Tout d’abord, ajoutez un trait d’`-`, puis sélectionnez la valeur **Position de l’ordre du lot**. Cela permet de s’assurer que pour la première itération, Workfront Fusion ajoute des `-1` au nom du fichier, pour la deuxième itération `-2` et ainsi de suite. Cliquez sur **OK**.

![WF Fusion](./images/wffusion211.png)

Enregistrez votre scénario, puis cliquez sur **Exécuter une fois**.

![WF Fusion](./images/wffusion212.png)

Une fois le scénario exécuté, revenez à votre Explorateur de stockage Azure et actualisez le dossier . Vous devriez alors voir les 2 fichiers nouvellement créés.

![WF Fusion](./images/wffusion213.png)

Téléchargez et ouvrez chaque fichier. Vous devriez alors voir les différents textes sur les boutons. Il s’agit du fichier `citisignal-fiber-changed-text-1.psd`.

![WF Fusion](./images/wffusion214.png)

Il s’agit du fichier `citisignal-fiber-changed-text-2.psd`.

![WF Fusion](./images/wffusion215.png)

## 1.2.3.2 Activer votre scénario à l’aide d’un webhook

Jusqu’à présent, vous avez exécuté votre scénario manuellement pour le tester. Mettons maintenant à jour votre scénario avec un webhook, afin qu’il puisse être activé à partir d’un environnement externe.

Cliquez sur l’icône **+**, recherchez **webhook** puis sélectionnez **Webhooks**.

![WF Fusion](./images/wffusion216.png)

Sélectionnez **Webhook personnalisé**.

Faites glisser et connectez le nœud **Custom webhook** afin qu’il se connecte au premier nœud de la zone de travail, appelé **Initialize Constants**.

![WF Fusion](./images/wffusion217.png)

Cliquez sur le nœud **Webhook personnalisé**. Cliquez ensuite sur **Ajouter**.

![WF Fusion](./images/wffusion218.png)

Définissez le **nom du Webhook** sur `--aepUserLdap-- - Tutorial 1.2`.

![WF Fusion](./images/wffusion219.png)

Cochez la case **Obtenir les en-têtes de requête**. Cliquez sur **Enregistrer**.

![WF Fusion](./images/wffusion220.png)

Votre URL webhook est maintenant disponible. Copiez l’URL.

![WF Fusion](./images/wffusion221.png)

Ouvrez Postman et ajoutez un nouveau dossier dans la collection **FF - Firefly Services Tech Insiders**.

![WF Fusion](./images/wffusion222.png)

Nommez votre dossier `--aepUserLdap-- - Workfront Fusion`.

![WF Fusion](./images/wffusion223.png)

Dans le dossier que vous venez de créer, cliquez sur le **de 3 points...** et sélectionnez **Ajouter une requête**.

![WF Fusion](./images/wffusion224.png)

Définissez le **Type de méthode** sur **POST** puis collez l’URL de votre webhook dans la barre d’adresse.

![WF Fusion](./images/wffusion225.png)

Vous devez envoyer un corps personnalisé, de sorte que les éléments de variable puissent être fournis d’une source externe à votre scénario Workfront Fusion. Accédez à **Corps** et sélectionnez **brut**.

![WF Fusion](./images/wffusion226.png)

Collez le texte ci-dessous dans le corps de votre requête. Cliquez sur **Envoyer**.

```json
{
    "psdTemplate": "placeholder",
    "xlsFile": "placeholder"
}
```

![WF Fusion](./images/wffusion229.png)

Revenez à Workfront Fusion. Un message s’affiche maintenant sur votre webhook personnalisé : **Déterminé avec succès**.

![WF Fusion](./images/wffusion227.png)

Cliquez sur **Enregistrer** puis sur **Exécuter une fois**. Votre scénario est désormais actif, mais ne s’exécutera pas tant que vous n’aurez pas cliqué de nouveau sur **Envoyer** dans Postman.

![WF Fusion](./images/wffusion230.png)

Accédez à Postman, puis cliquez de nouveau sur **Envoyer**.

![WF Fusion](./images/wffusion228.png)

Votre scénario s’exécutera à nouveau et créera les 2 fichiers comme avant.

![WF Fusion](./images/wffusion232.png)

Remplacez le nom de votre requête Postman par `POST - Send Request to Workfront Fusion Webhook`.

![WF Fusion](./images/wffusion233.png)

Vous devez maintenant commencer à utiliser la variable **psdTemplate**. Au lieu de coder en dur l’emplacement du fichier d’entrée dans le nœud **Texte de modification de Photoshop**, vous allez maintenant utiliser la variable entrante de la requête Postman.

Ouvrez le nœud **Texte de modification de Photoshop** et accédez à **Demander du contenu**. Sélectionnez le nom de fichier codé en dur **citisignal-fibre.psd** sous **entrées** et supprimez-le.

![WF Fusion](./images/wffusion234.png)

Sélectionnez la variable **psdTemplate**. Cliquez sur **OK** puis enregistrez votre scénario.

![WF Fusion](./images/wffusion235.png)

Cliquez sur **ACTIVÉ** pour activer votre scénario. Votre scénario s’exécute désormais sans arrêt.

![WF Fusion](./images/wffusion236.png)

Revenez à Postman. Saisissez le `citisignal-fiber.psd` de nom de fichier comme valeur de la variable **psdTemplate**, puis cliquez de nouveau sur **Envoyer** pour exécuter à nouveau votre scénario.

![WF Fusion](./images/wffusion237.png)

En spécifiant le modèle de PSD en tant que variable fournie par un système externe, vous avez désormais créé un scénario réutilisable.

Vous avez maintenant terminé cet exercice.

Étape suivante : [Résumé et avantages](./summary.md)

[Retour au module 1.2](./automation.md)

[Revenir à tous les modules](./../../../overview.md)
