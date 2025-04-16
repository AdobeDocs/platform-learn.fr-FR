---
title: Automatisation des processus avec Workfront Fusion
description: Découvrez comment traiter l’automatisation avec Workfront Fusion
role: Developer
level: Beginner
jira: KT-5342
doc-type: Tutorial
exl-id: 1b7b2630-864f-4982-be5d-c46b760739c3
source-git-commit: 603e48e0453911177823fe7ceb340f8ca801c5e1
workflow-type: tm+mt
source-wordcount: '947'
ht-degree: 0%

---

# 1.2.3 Automatisation des processus avec Workfront Fusion

Découvrez comment automatiser les processus avec Workfront Fusion.

## 1.2.3.1 Itération sur plusieurs valeurs

Votre scénario doit se présenter comme suit :

![WF Fusion](./images/wffusion200.png)

Jusqu’à présent, vous avez modifié le texte d’un fichier Photoshop par une valeur statique. Pour mettre à l’échelle et automatiser vos workflows de création de contenu, il est nécessaire d’effectuer une itération sur une liste de valeurs et d’insérer ces valeurs de manière dynamique dans le fichier Photoshop. Dans les étapes suivantes, vous allez ajouter une méthode pour effectuer une itération sur les valeurs de votre scénario existant.

Entre le nœud **Router** et le nœud **Photoshop Change Text**, sélectionnez l’icône **clé à molette** et sélectionnez **Ajouter un module**.

![WF Fusion](./images/wffusion201.png)

Recherchez `flow` et sélectionnez **Contrôle de flux**.

![WF Fusion](./images/wffusion202.png)

Sélectionnez **Itérateur**.

![WF Fusion](./images/wffusion203.png)

Votre écran doit ressembler à ceci :

![WF Fusion](./images/wffusion204.png)

Bien qu’il soit possible de lire des fichiers d’entrée tels que des fichiers CSV, vous devez pour l’instant utiliser une version de base d’un fichier CSV en définissant une chaîne de texte et en divisant ce fichier texte.

Vous pouvez trouver la fonction **split** en sélectionnant l’icône **T**, où vous pouvez voir toutes les fonctions disponibles pour manipuler les valeurs de texte. Sélectionnez la fonction **split**, vous devriez voir ceci.

![WF Fusion](./images/wffusion206.png)

La fonction split exige un tableau de valeurs avant le point-virgule et exige que vous spécifiiez le séparateur après le point-virgule. Pour ce test, vous devez utiliser un tableau simple avec 2 champs, **Acheter maintenant** et **Cliquer ici**, et le séparateur à utiliser est **,**.

Saisissez cette valeur dans le champ **Tableau** en remplaçant la fonction **split** actuellement vide : `{{split("Buy now, Click here "; ",")}}`. Sélectionnez **OK**.

![WF Fusion](./images/wffusion205.png)

Sélectionnez **Photoshop Modifier le texte** pour ajouter des variables au lieu de valeurs statiques pour les champs d’entrée et de sortie.

![WF Fusion](./images/wffusion207.png)

Dans **Demander le contenu**, le texte est-il **Cliquez ici**. Ce texte doit être remplacé par les valeurs provenant de votre tableau .

![WF Fusion](./images/wffusion208.png)

Supprimez le texte **Cliquez ici**, puis remplacez-le en sélectionnant la variable **Valeur** dans le nœud **Itérateur**. Cela permet de s’assurer que le texte du bouton dans votre document Photoshop est mis à jour de manière dynamique.

![WF Fusion](./images/wffusion209.png)

Vous devez également mettre à jour le nom du fichier utilisé pour écrire le fichier dans votre compte de stockage Azure. Si le nom de fichier est statique, chaque nouvelle itération remplace simplement le fichier précédent et perd donc les fichiers personnalisés. Le nom de fichier statique actuel est **citisignal-fibre-changed-text.psd** et vous devez maintenant le mettre à jour.

Placez le curseur derrière le mot `text`.

![WF Fusion](./images/wffusion210.png)

Tout d’abord, ajoutez un trait d’`-`, puis sélectionnez la valeur **Position de l’ordre du lot**. Cela permet de s’assurer que pour la première itération, Workfront Fusion ajoute des `-1` au nom du fichier, pour la deuxième itération `-2` et ainsi de suite. Sélectionnez **OK**.

![WF Fusion](./images/wffusion211.png)

Enregistrez votre scénario, puis sélectionnez **Exécuter une fois**.

![WF Fusion](./images/wffusion212.png)

Une fois le scénario exécuté, revenez à votre Explorateur de stockage Azure et actualisez le dossier . Vous devriez alors voir les 2 fichiers nouvellement créés.

![WF Fusion](./images/wffusion213.png)

Téléchargez et ouvrez chaque fichier. Vous devriez différents textes sur les boutons. Il s’agit du fichier `citisignal-fiber-changed-text-1.psd`.

![WF Fusion](./images/wffusion214.png)

Il s’agit du fichier `citisignal-fiber-changed-text-2.psd`.

![WF Fusion](./images/wffusion215.png)

## 1.2.3.2 Activer le scénario à l’aide d’un webhook

Jusqu’à présent, vous avez exécuté votre scénario manuellement pour le tester. Mettons maintenant à jour votre scénario avec un webhook, afin qu’il puisse être activé à partir d’un environnement externe.

Sélectionnez **+**, recherchez **webhook** puis sélectionnez **Webhooks**.

![WF Fusion](./images/wffusion216.png)

Sélectionnez **Webhook personnalisé**.

Faites glisser et connectez le nœud **Custom webhook** afin qu’il se connecte au premier nœud de la zone de travail, appelé **Initialize Constants**.

![WF Fusion](./images/wffusion217.png)

Sélectionnez le nœud **Webhook personnalisé**. Sélectionnez ensuite **Ajouter**.

![WF Fusion](./images/wffusion218.png)

Définissez **nom du Webhook** sur `--aepUserLdap-- - Tutorial 1.2`.

![WF Fusion](./images/wffusion219.png)

Cochez la case **Obtenir les en-têtes de requête**. Sélectionnez **Enregistrer**.

![WF Fusion](./images/wffusion220.png)

Votre URL webhook est maintenant disponible. Copiez l’URL.

![WF Fusion](./images/wffusion221.png)

Ouvrez Postman et ajoutez un nouveau dossier dans la collection **FF - Firefly Services Tech Insiders**.

![WF Fusion](./images/wffusion222.png)

Nommez votre dossier `--aepUserLdap-- - Workfront Fusion`.

![WF Fusion](./images/wffusion223.png)

Dans le dossier que vous venez de créer, sélectionnez la **de 3 points...** et sélectionnez **Ajouter une requête**.

![WF Fusion](./images/wffusion224.png)

Définissez le **Type de méthode** sur **POST** et collez l’URL de votre webhook dans la barre d’adresse.

![WF Fusion](./images/wffusion225.png)

Vous devez envoyer un corps personnalisé, de sorte que les éléments de variable puissent être fournis d’une source externe à votre scénario Workfront Fusion.

Accédez à **Corps** et sélectionnez **brut**.

![WF Fusion](./images/wffusion226.png)

Collez le texte ci-dessous dans le corps de votre requête. Sélectionnez **Envoyer**.

```json
{
	"psdTemplate": "placeholder",
	"xlsFile": "placeholder"
}
```

![WF Fusion](./images/wffusion229.png)

De retour dans Workfront Fusion, un message s’affiche sur votre webhook personnalisé et indique : **Déterminé avec succès**.

![WF Fusion](./images/wffusion227.png)

Sélectionnez **Enregistrer** puis sélectionnez **Exécuter une fois**. Votre scénario est maintenant actif, mais ne s’exécutera pas tant que vous n’aurez pas sélectionné **Envoyer** à nouveau dans Postman.

![WF Fusion](./images/wffusion230.png)

Dans Postman, sélectionnez à nouveau **Envoyer**.

![WF Fusion](./images/wffusion228.png)

Votre scénario s’exécute à nouveau et crée les 2 fichiers comme avant.

![WF Fusion](./images/wffusion232.png)

Remplacez le nom de votre requête Postman par `POST - Send Request to Workfront Fusion Webhook`.

![WF Fusion](./images/wffusion233.png)

Vous devez maintenant commencer à utiliser la variable **psdTemplate**. Au lieu de coder en dur l’emplacement du fichier d’entrée dans le nœud **Texte de modification de Photoshop**, vous utiliserez la variable entrante de la requête Postman.

Ouvrez le nœud **Texte de modification de Photoshop** et accédez à **Demander du contenu**. Sélectionnez le nom de fichier codé en dur **citisignal-fibre.psd** sous **entrées** et supprimez-le.

![WF Fusion](./images/wffusion234.png)

Sélectionnez la variable **psdTemplate**. Sélectionnez **OK** puis enregistrez votre scénario.

![WF Fusion](./images/wffusion235.png)

Sélectionnez **ACTIVÉ** pour activer votre scénario. Votre scénario s’exécute maintenant sans arrêt.

![WF Fusion](./images/wffusion236.png)

De retour dans Postman, saisissez le `citisignal-fiber.psd` de nom de fichier comme valeur de la variable **psdTemplate** et sélectionnez **Envoyer** pour exécuter à nouveau votre scénario.

![WF Fusion](./images/wffusion237.png)

En spécifiant le modèle PSD en tant que variable fournie par un système externe, vous avez désormais créé un scénario réutilisable.

Vous avez maintenant terminé cet exercice.

## Étapes suivantes

Accédez à Automatisation [1.2.4 à l’aide de connecteurs](./ex4.md){target="_blank"}

Revenez à l’automatisation des workflows Creative [avec Workfront Fusion](./automation.md){target="_blank"}

Revenir à [Tous les modules](./../../../overview.md){target="_blank"}
