---
title: Automatisation des processus avec Workfront Fusion
description: Découvrez comment traiter l’automatisation avec Workfront Fusion
role: Developer
level: Beginner
jira: KT-5342
doc-type: Tutorial
exl-id: 1b7b2630-864f-4982-be5d-c46b760739c3
source-git-commit: e419f07dbef519d9cf2f0100878e4cc880ad5f94
workflow-type: tm+mt
source-wordcount: '944'
ht-degree: 0%

---

# Automatisation des processus avec Workfront Fusion

Découvrez comment traiter l’automatisation avec Workfront Fusion.

## Itération sur plusieurs valeurs

Votre scénario doit se présenter comme suit :

![WF Fusion](./images/wffusion200.png)

Jusqu’à présent, vous avez modifié le texte d’un fichier Photoshop par une valeur statique. Pour mettre à l’échelle et automatiser vos workflows de création de contenu, il est nécessaire d’effectuer une itération sur une liste de valeurs et d’insérer ces valeurs de manière dynamique dans le fichier Photoshop. Dans les étapes suivantes, vous allez ajouter une méthode pour effectuer une itération sur les valeurs de votre scénario existant.

1. Entre le nœud **Router** et le nœud **Photoshop Change Text**, sélectionnez l’icône **clé à molette** et sélectionnez **Ajouter un module**.

   ![WF Fusion](./images/wffusion201.png)

1. Recherchez `flow` et sélectionnez **Contrôle de flux**.

   ![WF Fusion](./images/wffusion202.png)

1. Sélectionnez **Itérateur**.

   ![WF Fusion](./images/wffusion203.png)

   Votre écran doit ressembler à ceci :

   ![WF Fusion](./images/wffusion204.png)

   Bien qu’il soit possible de lire des fichiers d’entrée tels que des fichiers CSV, vous devez pour l’instant utiliser une version de base d’un fichier CSV en définissant une chaîne de texte et en divisant ce fichier texte.

1. Vous pouvez trouver la fonction **split** en sélectionnant l’icône **T**, où vous pouvez voir toutes les fonctions disponibles pour manipuler les valeurs de texte. Sélectionnez la fonction **split**, vous devriez voir ceci.

   ![WF Fusion](./images/wffusion206.png)

1. La fonction split exige un tableau de valeurs avant le point-virgule et exige que vous spécifiiez le séparateur après le point-virgule. Pour ce test, vous devez utiliser un tableau simple avec 2 champs, **Acheter maintenant** et **Cliquer ici**, et le séparateur à utiliser est **,**.

1. Saisissez cette valeur dans le champ **Tableau** en remplaçant la fonction **split** actuellement vide : `{{split("Buy now, Click here "; ",")}}`. Sélectionnez **OK**.

   ![WF Fusion](./images/wffusion205.png)



1. Sélectionnez **Photoshop Modifier le texte** pour ajouter des variables au lieu de valeurs statiques pour les champs d’entrée et de sortie.

   ![WF Fusion](./images/wffusion207.png)

   Dans **Demander le contenu**, le texte est-il **Cliquez ici**. Ce texte doit être remplacé par les valeurs provenant de votre tableau .

   ![WF Fusion](./images/wffusion208.png)

1. Supprimez le texte **Cliquez ici**, puis remplacez-le en sélectionnant la variable **Valeur** dans le nœud **Itérateur**. Cela permet de s’assurer que le texte du bouton dans votre document Photoshop est mis à jour de manière dynamique.

   ![WF Fusion](./images/wffusion209.png)

   Vous devez également mettre à jour le nom du fichier utilisé pour écrire le fichier dans votre compte de stockage Azure. Si le nom de fichier est statique, chaque nouvelle itération remplace simplement le fichier précédent et perd donc les fichiers personnalisés. Le nom de fichier statique actuel est **citisignal-fibre-changed-text.psd** et vous devez maintenant le mettre à jour.

1. Placez le curseur derrière le mot `text`.

   ![WF Fusion](./images/wffusion210.png)

1. Tout d’abord, ajoutez un trait d’`-`, puis sélectionnez la valeur **Position de l’ordre du lot**. Cela permet de s’assurer que pour la première itération, Workfront Fusion ajoute des `-1` au nom du fichier, pour la deuxième itération `-2` et ainsi de suite. Sélectionnez **OK**.

   ![WF Fusion](./images/wffusion211.png)

1. Enregistrez votre scénario, puis sélectionnez **Exécuter une fois**.

   ![WF Fusion](./images/wffusion212.png)

   Une fois le scénario exécuté, revenez à votre Explorateur de stockage Azure et actualisez le dossier . Vous devriez alors voir les 2 fichiers nouvellement créés.

   ![WF Fusion](./images/wffusion213.png)

1. Téléchargez et ouvrez chaque fichier. Vous devriez différents textes sur les boutons. Il s’agit du fichier `citisignal-fiber-changed-text-1.psd`.

   ![WF Fusion](./images/wffusion214.png)

   Il s’agit du fichier `citisignal-fiber-changed-text-2.psd`.

   ![WF Fusion](./images/wffusion215.png)

## Activez votre scénario à l’aide d’un webhook

Jusqu’à présent, vous avez exécuté votre scénario manuellement pour le tester. Mettons maintenant à jour votre scénario avec un webhook, afin qu’il puisse être activé à partir d’un environnement externe.

1. Sélectionnez **+**, recherchez **webhook** puis sélectionnez **Webhooks**.

   ![WF Fusion](./images/wffusion216.png)

1. Sélectionnez **Webhook personnalisé**.

1. Faites glisser et connectez le nœud **Custom webhook** afin qu’il se connecte au premier nœud de la zone de travail, appelé **Initialize Constants**.

   ![WF Fusion](./images/wffusion217.png)

1. Sélectionnez le nœud **Webhook personnalisé**. Sélectionnez ensuite **Ajouter**.

   ![WF Fusion](./images/wffusion218.png)

1. Définissez **nom du Webhook** sur `--aepUserLdap-- - Tutorial 1.2`.

   ![WF Fusion](./images/wffusion219.png)

1. Cochez la case **Obtenir les en-têtes de requête**. Sélectionnez **Enregistrer**.

   ![WF Fusion](./images/wffusion220.png)

1. Votre URL webhook est maintenant disponible. Copiez l’URL.

   ![WF Fusion](./images/wffusion221.png)

1. Ouvrez Postman et ajoutez un nouveau dossier dans la collection **FF - Firefly Services Tech Insiders**.

   ![WF Fusion](./images/wffusion222.png)

1. Nommez votre dossier `--aepUserLdap-- - Workfront Fusion`.

   ![WF Fusion](./images/wffusion223.png)

1. Dans le dossier que vous venez de créer, sélectionnez la **de 3 points...** et sélectionnez **Ajouter une requête**.

   ![WF Fusion](./images/wffusion224.png)

1. Définissez le **Type de méthode** sur **POST** puis collez l’URL de votre webhook dans la barre d’adresse.

   ![WF Fusion](./images/wffusion225.png)

   Vous devez envoyer un corps personnalisé, de sorte que les éléments de variable puissent être fournis d’une source externe à votre scénario Workfront Fusion.

1. Accédez à **Corps** et sélectionnez **brut**.

   ![WF Fusion](./images/wffusion226.png)

1. Collez le texte ci-dessous dans le corps de votre requête. Sélectionnez **Envoyer**.

   ```json
   {
       "psdTemplate": "placeholder",
       "xlsFile": "placeholder"
   }
   ```

   ![WF Fusion](./images/wffusion229.png)

1. De retour dans Workfront Fusion, un message s’affiche sur votre webhook personnalisé et indique : **Déterminé avec succès**.

   ![WF Fusion](./images/wffusion227.png)

1. Sélectionnez **Enregistrer** puis sélectionnez **Exécuter une fois**. Votre scénario est maintenant actif, mais ne s’exécutera pas tant que vous n’aurez pas sélectionné **Envoyer** à nouveau dans Postman.

   ![WF Fusion](./images/wffusion230.png)

1. Dans Postman, sélectionnez à nouveau **Envoyer**.

   ![WF Fusion](./images/wffusion228.png)

   Votre scénario s’exécute à nouveau et crée les 2 fichiers comme avant.

   ![WF Fusion](./images/wffusion232.png)

1. Remplacez le nom de votre requête Postman par `POST - Send Request to Workfront Fusion Webhook`.

   ![WF Fusion](./images/wffusion233.png)

   Vous devez maintenant commencer à utiliser la variable **psdTemplate**. Au lieu de coder en dur l’emplacement du fichier d’entrée dans le nœud **Texte de modification de Photoshop**, vous utiliserez la variable entrante de la requête Postman.

1. Ouvrez le nœud **Texte de modification de Photoshop** et accédez à **Demander du contenu**. Sélectionnez le nom de fichier codé en dur **citisignal-fibre.psd** sous **entrées** et supprimez-le.

   ![WF Fusion](./images/wffusion234.png)

1. Sélectionnez la variable **psdTemplate**. Sélectionnez **OK** puis enregistrez votre scénario.

   ![WF Fusion](./images/wffusion235.png)

1. Sélectionnez **ACTIVÉ** pour activer votre scénario. Votre scénario s’exécute maintenant sans arrêt.

   ![WF Fusion](./images/wffusion236.png)

1. De retour dans Postman, saisissez le `citisignal-fiber.psd` de nom de fichier comme valeur de la variable **psdTemplate** et sélectionnez **Envoyer** pour exécuter à nouveau votre scénario.

   ![WF Fusion](./images/wffusion237.png)

   En spécifiant le modèle de PSD en tant que variable fournie par un système externe, vous avez désormais créé un scénario réutilisable.

   Vous avez maintenant terminé cet exercice.

## Étapes suivantes

Accédez à [Résumé et avantages de l’automatisation des services Firefly](./summary.md){target="_blank"}

Revenez à [Automatisation des services d’Adobe Firefly ](./automation.md){target="_blank"}

Revenir à [Tous les modules](./../../../overview.md){target="_blank"}
