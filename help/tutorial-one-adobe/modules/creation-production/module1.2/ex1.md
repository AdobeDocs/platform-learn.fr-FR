---
title: Prise en main de Workfront Fusion
description: Découvrez comment utiliser Workfront Fusion et Adobe I/O pour interroger les API Adobe Firefly Services
role: Developer
level: Beginner
jira: KT-5342
doc-type: Tutorial
exl-id: 42e260e0-8af0-4d71-b634-48c1966bd912
source-git-commit: 4b38b40c47b5c373f74a85261adce46f291303a8
workflow-type: tm+mt
source-wordcount: '705'
ht-degree: 1%

---

# 1.2.1 Prise en main de Workfront Fusion

Découvrez comment utiliser Workfront Fusion et Adobe I/O pour interroger les API Adobe Firefly Services.

## 1.2.1.1 Créer un nouveau scénario

Accédez à [https://experience.adobe.com/](https://experience.adobe.com/){target="_blank"}. Ouvrez **Workfront Fusion**.

![WF Fusion](./images/wffusion1.png)

Accédez à **Scénarios**.

![WF Fusion](./images/wffusion2.png)

Cliquez sur l’icône **+** créer un dossier pour votre travail.

![WF Fusion](./images/wffusion2a.png)

Nommez le dossier `--aepUserLdap--` et sélectionnez **Enregistrer**.

![WF Fusion](./images/wffusion2b.png)

Sélectionnez votre dossier, puis sélectionnez **Créer un scénario**.

![WF Fusion](./images/wffusion3.png)

Un scénario vide s’affiche, sélectionnez **outils** puis **Définir plusieurs variables**.

![WF Fusion](./images/wffusion4.png)

Déplacez l’icône **horloge** sur le nouveau composant **Définir plusieurs variables**.

![WF Fusion](./images/wffusion5.png)

Votre écran devrait ressembler à ceci.

![WF Fusion](./images/wffusion6.png)

Cliquez avec le bouton droit sur le point d’interrogation et sélectionnez **Supprimer le module**.

![WF Fusion](./images/wffusion7.png)

Cliquez ensuite avec le bouton droit de la souris sur **Définir plusieurs variables** et sélectionnez **Paramètres**.

![WF Fusion](./images/wffusion8.png)

## 1.2.1.2 Configurer l’authentification Adobe I/O

Vous devez maintenant configurer les variables nécessaires pour l’authentification sur Adobe I/O. Dans l’exercice précédent, vous avez créé un projet Adobe I/O. Les variables de ce projet Adobe I/O doivent maintenant être définies dans Workfront Fusion.

Les variables suivantes doivent être définies :

| Clé | Valeur |
|:-------------:| :---------------:| 
| `CONST_client_id` | votre identifiant client de projet Adobe I/O ; |
| `CONST_client_secret` | votre secret client de projet Adobe I/O |
| `CONST_scope` | la portée de votre projet Adobe I/O ; |

Recherchez ces variables en accédant à [https://developer.adobe.com/console/projects](https://developer.adobe.com/console/projects){target="_blank"} et en ouvrant votre projet Adobe I/O nommé `--aepUserLdap-- One Adobe tutorial`.

![WF Fusion](./images/wffusion9.png)

Dans votre projet, sélectionnez **Serveur OAuth** pour afficher les valeurs des clés ci-dessus.

![WF Fusion](./images/wffusion10.png)

À l’aide des clés et valeurs ci-dessus, vous pouvez configurer l’objet **Définir plusieurs variables**. Sélectionnez **Ajouter un élément**.

![WF Fusion](./images/wffusion11.png)

Saisissez le **Nom de la variable** : **CONST_client_id** et sa **Valeur de la variable**, puis sélectionnez **Ajouter**.

![WF Fusion](./images/wffusion12.png)

Sélectionnez **Ajouter un élément**.

![WF Fusion](./images/wffusion13.png)

Saisissez **Nom de la variable** : **CONST_client_secret** et sa **Valeur de la variable**, sélectionnez **Ajouter**.

![WF Fusion](./images/wffusion14.png)

Sélectionnez **Ajouter un élément**.

![WF Fusion](./images/wffusion15.png)

Saisissez **Nom de la variable** : **CONST_scope** et sa **Valeur de la variable**, sélectionnez **Ajouter**.

![WF Fusion](./images/wffusion16.png)

Sélectionnez **OK**.

![WF Fusion](./images/wffusion17.png)

Pointez sur **Définir plusieurs variables** et sélectionnez la grande icône **+** pour ajouter un autre module.

![WF Fusion](./images/wffusion18.png)

Votre écran devrait ressembler à ceci.

![WF Fusion](./images/wffusion19.png)

Dans la barre de recherche, saisissez **http**. Sélectionnez **HTTP** pour l’ouvrir.

![WF Fusion](./images/wffusion21.png)

Sélectionnez **Effectuer une requête**.

![WF Fusion](./images/wffusion20.png)

| Clé | Valeur |
|:-------------:| :---------------:| 
| `URL` | `https://ims-na1.adobelogin.com/ims/token/v3` |
| `Method` | `POST` |
| `Body Type` | `x-www-form-urlencoded` |

Sélectionnez **Ajouter un élément**.

![WF Fusion](./images/wffusion22.png)

Ajoutez des éléments pour chacune des valeurs ci-dessous :

| Clé | Valeur |
|:-------------:| :---------------:| 
| `client_id` | votre variable prédéfinie pour `CONST_client_id` |
| `client_secret` | votre variable prédéfinie pour `CONST_client_secret` |
| `scope` | votre variable prédéfinie pour `CONST_scope` |
| `grant_type` | `client_credentials` |

Configuration pour `client_id` :

![WF Fusion](./images/wffusion23.png)

Configuration pour `client_secret`.

![WF Fusion](./images/wffusion25.png)

Configuration pour `scope`.

![WF Fusion](./images/wffusion26.png)

Configuration pour `grant_type`.

![WF Fusion](./images/wffusion28.png)

Faites défiler vers le bas et cochez la case **Analyse de la réponse**. Sélectionnez **OK**.

![WF Fusion](./images/wffusion27.png)

Votre écran devrait ressembler à ceci. Sélectionnez **Exécuter une fois**.

![WF Fusion](./images/wffusion29.png)

Une fois le scénario exécuté, l’écran doit se présenter comme suit :

![WF Fusion](./images/wffusion30.png)

Sélectionnez l’icône **point d’interrogation** sur l’objet **Définir plusieurs variables** pour voir ce qui s’est passé lorsque cet objet s’est exécuté.

![WF Fusion](./images/wffusion31.png)

Sélectionnez l’icône **point d’interrogation** sur l’objet **HTTP - Effectuer une requête** pour voir ce qui s’est passé lorsque cet objet s’est exécuté. Dans le **OUTPUT**, consultez le **access_token** renvoyé par Adobe I/O.

![WF Fusion](./images/wffusion32.png)

Pointez sur **HTTP - Effectuez une requête** puis sélectionnez l’icône **+** pour ajouter un autre module.

![WF Fusion](./images/wffusion33.png)

Dans la barre de recherche, recherchez `tools`. Sélectionnez **Outils**.

![WF Fusion](./images/wffusion34.png)

Sélectionnez **Définir plusieurs variables**.

![WF Fusion](./images/wffusion35.png)

Sélectionnez **Ajouter un élément**.

![WF Fusion](./images/wffusion36.png)

Définissez **Nom de la variable** sur `bearer_token`. Sélectionnez `access_token` comme **valeur de variable** dynamique. Sélectionnez **Ajouter**.

![WF Fusion](./images/wffusion37.png)

Votre écran devrait ressembler à ceci. Sélectionnez **OK**.

![WF Fusion](./images/wffusion38.png)

Sélectionnez **Exécuter une fois** à nouveau.

![WF Fusion](./images/wffusion39.png)

Une fois le scénario exécuté, sélectionnez l’icône **point d’interrogation** sur le dernier objet **Définir plusieurs variables**. Vous devriez voir que le jeton access_token est stocké dans la variable `bearer_token`.

![WF Fusion](./images/wffusion40.png)

Cliquez ensuite avec le bouton droit de la souris sur le premier objet **Définir plusieurs valeurs** et sélectionnez **Renommer**.

![WF Fusion](./images/wffusion41.png)

Définissez le nom sur **Initialiser les constantes**. Sélectionnez **OK**.

![WF Fusion](./images/wffusion42.png)

Renommez le second objet en **Authentifier sur Adobe I/O**. Sélectionnez **OK**.

![WF Fusion](./images/wffusion43.png)

Renommez le troisième objet en **Définir le jeton du porteur**. Sélectionnez **OK**.

![WF Fusion](./images/wffusion44.png)

Votre écran doit ressembler à ceci :

![WF Fusion](./images/wffusion45.png)

Ensuite, remplacez le nom de votre scénario par `--aepUserLdap-- - Adobe I/O Authentication`.

![WF Fusion](./images/wffusion46.png)

Sélectionnez **Enregistrer**.

![WF Fusion](./images/wffusion47.png)

## Étapes suivantes

Accédez à [&#x200B; Utilisation des API Adobe dans Workfront Fusion &#x200B;](./ex2.md){target="_blank"}

Revenez à l’automatisation des workflows Creative [avec Workfront Fusion](./automation.md){target="_blank"}

Revenir à [Tous les modules](./../../../overview.md){target="_blank"}
