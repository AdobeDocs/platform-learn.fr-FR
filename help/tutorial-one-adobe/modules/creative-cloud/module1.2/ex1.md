---
title: Prise en main de Workfront Fusion
description: Prise en main de Workfront Fusion
kt: 5342
doc-type: tutorial
exl-id: 42e260e0-8af0-4d71-b634-48c1966bd912
source-git-commit: f1f70a0e4ea3f59b5b121275e7db633caf953df9
workflow-type: tm+mt
source-wordcount: '727'
ht-degree: 3%

---

# 1.2.1 Prise en main de Workfront Fusion

Dans cet exercice, vous allez utiliser Workfront Fusion et Adobe I/O pour interroger les API Adobe Firefly Services.

## 1.2.1.1 Créer un nouveau scénario

Accédez à [https://experience.adobe.com/](https://experience.adobe.com/). Cliquez pour ouvrir **Workfront Fusion**.

![WF Fusion](./images/wffusion1.png)

Vous devriez alors voir ceci. Accédez à **Scénarios**.

![WF Fusion](./images/wffusion2.png)

Cliquez sur l’icône **+** pour créer un dossier.

![WF Fusion](./images/wffusion2a.png)

Pour le nom du dossier, utilisez : `--aepUserLdap--`. Cliquez sur **Enregistrer**.

![WF Fusion](./images/wffusion2b.png)

Sélectionnez votre dossier, puis cliquez sur **Créer un nouveau scénario**.

![WF Fusion](./images/wffusion3.png)

Un scénario vide s’affiche alors. Cliquez sur l’icône **outils** et sélectionnez **Définir plusieurs variables**.

![WF Fusion](./images/wffusion4.png)

Vous devez maintenant déplacer l’icône **horloge** sur le nouveau **Définir plusieurs variables** ajouté.

![WF Fusion](./images/wffusion5.png)

Tu verras ça.

![WF Fusion](./images/wffusion6.png)

Cliquez ensuite avec le bouton droit sur le point d’interrogation et sélectionnez **Supprimer le module**.

![WF Fusion](./images/wffusion7.png)

Cliquez ensuite avec le bouton droit de la souris sur l’objet **Définir plusieurs variables** et sélectionnez **Paramètres**.

![WF Fusion](./images/wffusion8.png)

## 1.2.1.2 Configurer l’authentification d’Adobe I/O

Vous devez maintenant configurer les variables nécessaires pour vous authentifier en cas d’Adobe I/O. Dans l’exercice précédent, vous avez créé un projet Adobe I/O. Les variables de ce projet d’Adobe I/O doivent maintenant être définies dans Workfront Fusion.

Les variables suivantes doivent être définies :

| Clé | Valeur |
|:-------------:| :---------------:| 
| `CONST_client_id` | l’identifiant client de votre projet Adobe I/O ; |
| `CONST_client_secret` | votre secret client de projet Adobe I/O |
| `CONST_scope` | votre projet d’Adobe I/O Portée |

Vous pouvez retrouver ces variables en accédant à [https://developer.adobe.com/console/projects](https://developer.adobe.com/console/projects) et en ouvrant votre projet d’Adobe I/O nommé `--aepUserLdap-- Firefly`.

![WF Fusion](./images/wffusion9.png)

Dans votre projet, cliquez sur **Serveur OAuth** pour afficher les valeurs des clés ci-dessus.

![WF Fusion](./images/wffusion10.png)

Avec les clés et valeurs ci-dessus, vous pouvez configurer l’objet **Définir plusieurs variables**. Cliquez sur **Ajouter un élément**.

![WF Fusion](./images/wffusion11.png)

Saisissez le **Nom de la variable** : **CONST_client_id** et sa **Valeur de la variable**, puis cliquez sur **Ajouter**.

![WF Fusion](./images/wffusion12.png)

Cliquez sur **Ajouter un élément**.

![WF Fusion](./images/wffusion13.png)

Saisissez le **Nom de la variable** : **CONST_client_secret** et sa **Valeur de la variable**, puis cliquez sur **Ajouter**.

![WF Fusion](./images/wffusion14.png)

Cliquez sur **Ajouter un élément**.

![WF Fusion](./images/wffusion15.png)

Saisissez le **Nom de la variable** : **CONST_scope** et sa **Valeur de la variable**, puis cliquez sur **Ajouter**.

![WF Fusion](./images/wffusion16.png)

Cliquez sur **OK**.

![WF Fusion](./images/wffusion17.png)

Pointez sur votre objet **Définir plusieurs variables** et cliquez sur la grande icône **+** pour ajouter un autre module.

![WF Fusion](./images/wffusion18.png)

Vous devriez alors voir ceci.

![WF Fusion](./images/wffusion19.png)

Dans la barre de recherche, saisissez **http**. Sélectionnez **HTTP** pour l’ouvrir.

![WF Fusion](./images/wffusion21.png)

puis sélectionnez **Effectuer une requête**.

![WF Fusion](./images/wffusion20.png)

| Clé | Valeur |
|:-------------:| :---------------:| 
| `URL` | `https://ims-na1.adobelogin.com/ims/token/v3` |
| `Method` | `POST` |
| `Body Type` | `x-www-form-urlencoded` |

Cliquez sur **Ajouter un élément**.

![WF Fusion](./images/wffusion22.png)

Ajoutez des éléments pour chacune des valeurs ci-dessous :

| Clé | Valeur |
|:-------------:| :---------------:| 
| `client_id` | votre variable prédéfinie pour `CONST_client_id` |
| `client_secret` | votre variable prédéfinie pour `CONST_client_secret` |
| `scope` | votre variable prédéfinie pour `CONST_scope` |
| `grant_type` | `client_credentials` |

Configuration pour `client_id`.

![WF Fusion](./images/wffusion23.png)

Configuration pour `client_secret`.

![WF Fusion](./images/wffusion25.png)

Configuration pour `scope`.

![WF Fusion](./images/wffusion26.png)

Configuration pour `grant_type`.

![WF Fusion](./images/wffusion28.png)

Présentation de la configuration. Faites défiler vers le bas et cochez la case **Analyser la réponse**. Cliquez sur **OK**.

![WF Fusion](./images/wffusion27.png)

Vous devriez alors voir ceci. Cliquez sur **Exécuter une fois**.

![WF Fusion](./images/wffusion29.png)

Une fois le scénario exécuté, vous devriez voir ceci.

![WF Fusion](./images/wffusion30.png)

Cliquez sur l’icône **point d’interrogation** de l’objet **Définir plusieurs variables** pour voir ce qui s’est passé lorsque cet objet a été exécuté.

![WF Fusion](./images/wffusion31.png)

Cliquez sur l’icône **point d’interrogation** de l’objet **HTTP - Effectuer une requête** pour voir ce qui s’est passé lorsque cet objet a été exécuté. Dans l’**OUTPUT**, le **access_token** est renvoyé par Adobe I/O.

![WF Fusion](./images/wffusion32.png)

Pointez sur l’objet **HTTP - Effectuer une requête** et cliquez sur l’icône **+** pour ajouter un autre module.

![WF Fusion](./images/wffusion33.png)

Dans la barre de recherche, recherchez `tools`. Sélectionnez **Outils**.

![WF Fusion](./images/wffusion34.png)

Sélectionnez **Définir plusieurs variables**.

![WF Fusion](./images/wffusion35.png)

Sélectionnez **Ajouter un élément**.

![WF Fusion](./images/wffusion36.png)

Définissez le **Nom de variable** sur `bearer_token`. Sélectionnez `access_token` comme **valeur de variable** dynamique. Cliquez sur **Ajouter**.

![WF Fusion](./images/wffusion37.png)

Tu devrais avoir ça. Cliquez sur **OK**.

![WF Fusion](./images/wffusion38.png)

Cliquez de nouveau sur **Exécuter**.

![WF Fusion](./images/wffusion39.png)

Une fois le scénario exécuté, cliquez sur l’icône **point d’interrogation** sur le dernier objet **Définir plusieurs variables**. Vous devriez alors voir que le jeton access_token est stocké dans la variable `bearer_token`.

![WF Fusion](./images/wffusion40.png)

Cliquez ensuite avec le bouton droit de la souris sur le premier objet **Définir plusieurs valeurs** et sélectionnez **Renommer**.

![WF Fusion](./images/wffusion41.png)

Définissez le nom sur **Initialiser les constantes**. Cliquez sur **OK**.

![WF Fusion](./images/wffusion42.png)

Renommez le second objet et définissez son nom sur **Authentification en Adobe I/O**. Cliquez sur **OK**.

![WF Fusion](./images/wffusion43.png)

Renommez le troisième objet et définissez le nom en **Définir le jeton du porteur**. Cliquez sur **OK**.

![WF Fusion](./images/wffusion44.png)

Tu devrais avoir ça.

![WF Fusion](./images/wffusion45.png)

Ensuite, remplacez le nom de votre scénario par `--aepUSerLdap-- - Adobe I/O Authentication`.

![WF Fusion](./images/wffusion46.png)

Cliquez sur **Enregistrer**.

![WF Fusion](./images/wffusion47.png)

Étape suivante : [1.2.2 Utilisation d’API Adobes dans Workfront Fusion](./ex2.md)

[Retour au module 1.2](./automation.md)

[Revenir à tous les modules](./../../../overview.md)
