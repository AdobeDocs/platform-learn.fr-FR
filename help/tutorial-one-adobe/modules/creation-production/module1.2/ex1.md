---
title: Prise en main de Workfront Fusion
description: Découvrez comment utiliser Workfront Fusion et Adobe I/O pour interroger les API des services Adobe Firefly
role: Developer
level: Beginner
jira: KT-5342
doc-type: Tutorial
exl-id: 42e260e0-8af0-4d71-b634-48c1966bd912
source-git-commit: b083a817700320e8e45645702c2868423c1fae99
workflow-type: tm+mt
source-wordcount: '698'
ht-degree: 1%

---

# 1.2.1 Prise en main de Workfront Fusion

Découvrez comment utiliser Workfront Fusion et Adobe I/O pour interroger les API des services Adobe Firefly.

## 1.2.1.1 Créer un nouveau scénario

1. Accédez à [https://experience.adobe.com/](https://experience.adobe.com/). Ouvrez **Workfront Fusion**.

   ![WF Fusion](./images/wffusion1.png)

1. Accédez à **Scénarios**.

   ![WF Fusion](./images/wffusion2.png)

1. Sélectionnez **Créer un scénario**.

   ![WF Fusion](./images/wffusion2a.png)

1. Nommez le dossier `--aepUserLdap--` et sélectionnez **Enregistrer**.

   ![WF Fusion](./images/wffusion2b.png)

1. Sélectionnez votre dossier, puis sélectionnez **Créer un scénario**.

   ![WF Fusion](./images/wffusion3.png)

1. Un scénario vide s’affiche, sélectionnez **outils** puis **Définir plusieurs variables**.

   ![WF Fusion](./images/wffusion4.png)

1. Déplacez l’icône **horloge** sur le nouveau composant **Définir plusieurs variables**.

   ![WF Fusion](./images/wffusion5.png)

   Votre écran devrait ressembler à ceci.

   ![WF Fusion](./images/wffusion6.png)

1. Cliquez avec le bouton droit sur le point d’interrogation et sélectionnez **Supprimer le module**.

   ![WF Fusion](./images/wffusion7.png)

1. Cliquez ensuite avec le bouton droit de la souris sur **Définir plusieurs variables** et sélectionnez **Paramètres**.

   ![WF Fusion](./images/wffusion8.png)

## 1.2.1.2 Configurer l’authentification Adobe I/O

Vous devez maintenant configurer les variables nécessaires pour l’authentification sur Adobe I/O. Dans l’exercice précédent, vous avez créé un projet Adobe I/O. Les variables de ce projet Adobe I/O doivent maintenant être définies dans Workfront Fusion.

Les variables suivantes doivent être définies :

| Clé | Valeur |
|:-------------:| :---------------:| 
| `CONST_client_id` | votre identifiant client de projet Adobe I/O ; |
| `CONST_client_secret` | votre secret client de projet Adobe I/O |
| `CONST_scope` | la portée de votre projet Adobe I/O ; |

1. Recherchez ces variables en accédant à [https://developer.adobe.com/console/projects](https://developer.adobe.com/console/projects) et en ouvrant votre projet Adobe I/O nommé `--aepUserLdap-- Firefly`.

   ![WF Fusion](./images/wffusion9.png)

1. Dans votre projet, sélectionnez **Serveur OAuth** pour afficher les valeurs des clés ci-dessus.

   ![WF Fusion](./images/wffusion10.png)

1. À l’aide des clés et valeurs ci-dessus, vous pouvez configurer l’objet **Définir plusieurs variables**. Sélectionnez **Ajouter un élément**.

   ![WF Fusion](./images/wffusion11.png)

1. Saisissez le **Nom de la variable** : **CONST_client_id** et sa **Valeur de la variable**, puis sélectionnez **Ajouter**.

   ![WF Fusion](./images/wffusion12.png)

1. Sélectionnez **Ajouter un élément**.

   ![WF Fusion](./images/wffusion13.png)

1. Saisissez **Nom de la variable** : **CONST_client_secret** et sa **Valeur de la variable**, sélectionnez **Ajouter**.

   ![WF Fusion](./images/wffusion14.png)

1. Sélectionnez **Ajouter un élément**.

   ![WF Fusion](./images/wffusion15.png)

1. Saisissez **Nom de la variable** : **CONST_scope** et sa **Valeur de la variable**, sélectionnez **Ajouter**.

   ![WF Fusion](./images/wffusion16.png)

1. Sélectionnez **OK**.

   ![WF Fusion](./images/wffusion17.png)

1. Pointez sur **Définir plusieurs variables** et sélectionnez la grande icône **+** pour ajouter un autre module.

   ![WF Fusion](./images/wffusion18.png)

   Votre écran devrait ressembler à ceci.

   ![WF Fusion](./images/wffusion19.png)

1. Dans la barre de recherche, saisissez **http**. Sélectionnez **HTTP** pour l’ouvrir.

   ![WF Fusion](./images/wffusion21.png)

1. Sélectionnez **Effectuer une requête**.

   ![WF Fusion](./images/wffusion20.png)

   | Clé | Valeur |
   |:-------------:| :---------------:| 
   | `URL` | `https://ims-na1.adobelogin.com/ims/token/v3` |
   | `Method` | `POST` |
   | `Body Type` | `x-www-form-urlencoded` |

1. Sélectionnez **Ajouter un élément**.

   ![WF Fusion](./images/wffusion22.png)

1. Ajoutez des éléments pour chacune des valeurs ci-dessous :

   | Clé | Valeur |
   |:-------------:| :---------------:| 
   | `client_id` | votre variable prédéfinie pour `CONST_client_id` |
   | `client_secret` | votre variable prédéfinie pour `CONST_client_secret` |
   | `scope` | votre variable prédéfinie pour `CONST_scope` |
   | `grant_type` | `client_credentials` |

1. Configuration pour `client_id` :

   ![WF Fusion](./images/wffusion23.png)

1. Configuration pour `client_secret`.

   ![WF Fusion](./images/wffusion25.png)

1. Configuration pour `scope`.

   ![WF Fusion](./images/wffusion26.png)

1. Configuration pour `grant_type`.

   ![WF Fusion](./images/wffusion28.png)

1. Faites défiler vers le bas et cochez la case **Analyse de la réponse**. Sélectionnez **OK**.

   ![WF Fusion](./images/wffusion27.png)

1. Votre écran devrait ressembler à ceci. Sélectionnez **Exécuter une fois**.

   ![WF Fusion](./images/wffusion29.png)

   Une fois le scénario exécuté, l’écran doit se présenter comme suit :

   ![WF Fusion](./images/wffusion30.png)

1. Sélectionnez l’icône **point d’interrogation** sur l’objet **Définir plusieurs variables** pour voir ce qui s’est passé lorsque cet objet s’est exécuté.

   ![WF Fusion](./images/wffusion31.png)

1. Sélectionnez l’icône **point d’interrogation** sur l’objet **HTTP - Effectuer une requête** pour voir ce qui s’est passé lorsque cet objet s’est exécuté. Dans le **OUTPUT**, consultez le **access_token** renvoyé par Adobe I/O.

   ![WF Fusion](./images/wffusion32.png)

1. Pointez sur **HTTP - Effectuez une requête** puis sélectionnez l’icône **+** pour ajouter un autre module.

   ![WF Fusion](./images/wffusion33.png)

1. Dans la barre de recherche, recherchez `tools`. Sélectionnez **Outils**.

   ![WF Fusion](./images/wffusion34.png)

1. Sélectionnez **Définir plusieurs variables**.

   ![WF Fusion](./images/wffusion35.png)

1. Sélectionnez **Ajouter un élément**.

   ![WF Fusion](./images/wffusion36.png)

1. Définissez **Nom de la variable** sur `bearer_token`. Sélectionnez `access_token` comme **valeur de variable** dynamique. Sélectionnez **Ajouter**.

   ![WF Fusion](./images/wffusion37.png)

1. Votre écran devrait ressembler à ceci. Sélectionnez **OK**.

   ![WF Fusion](./images/wffusion38.png)

1. Sélectionnez **Exécuter une fois** à nouveau.

   ![WF Fusion](./images/wffusion39.png)

1. Une fois le scénario exécuté, sélectionnez l’icône **point d’interrogation** sur le dernier objet **Définir plusieurs variables**. Vous devriez voir que le jeton access_token est stocké dans la variable `bearer_token`.

   ![WF Fusion](./images/wffusion40.png)

1. Cliquez ensuite avec le bouton droit de la souris sur le premier objet **Définir plusieurs valeurs** et sélectionnez **Renommer**.

   ![WF Fusion](./images/wffusion41.png)

1. Définissez le nom sur **Initialiser les constantes**. Sélectionnez **OK**.

   ![WF Fusion](./images/wffusion42.png)

1. Renommez le second objet en **Authentifier sur Adobe I/O**. Sélectionnez **OK**.

   ![WF Fusion](./images/wffusion43.png)

1. Renommez le troisième objet en **Définir le jeton du porteur**. Sélectionnez **OK**.

   ![WF Fusion](./images/wffusion44.png)

   Votre écran doit ressembler à ceci :

   ![WF Fusion](./images/wffusion45.png)

1. Ensuite, remplacez le nom de votre scénario par `--aepUSerLdap-- - Adobe I/O Authentication`.

   ![WF Fusion](./images/wffusion46.png)

1. Sélectionnez **Enregistrer**.

   ![WF Fusion](./images/wffusion47.png)

## Étapes suivantes

Accédez à [ Utilisation des API Adobe dans Workfront Fusion ](./ex2.md){target="_blank"}

Revenez à [Automatisation des services Adobe Firefly](./automation.md){target="_blank"}.

Revenir à [Tous les modules](./../../../overview.md){target="_blank"}
