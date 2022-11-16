---
title: Ingestion et analyse de données Google Analytics dans Adobe Experience Platform avec le connecteur source BigQuery - Connectez GCP et BigQuery à Adobe Experience Platform
description: Ingestion et analyse de données Google Analytics dans Adobe Experience Platform avec le connecteur source BigQuery - Connectez GCP et BigQuery à Adobe Experience Platform
kt: 5342
audience: Data Engineer, Data Architect, Data Analyst
doc-type: tutorial
activity: develop
exl-id: b2b29cb7-dd5c-48f2-b881-3e10d9f1a0df
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '1758'
ht-degree: 2%

---

# 12.3 Connexion de GCP et BigQuery à Adobe Experience Platform

## Objectifs

- Exploration des API et services dans Google Cloud Platform
- Familiarisez-vous avec OAuth Playground pour le test des API Google
- Créer votre première connexion BigQuery dans Adobe Experience Platform

## Contexte

Adobe Experience Platform fournit un connecteur dans **Sources** qui vous aidera à importer des jeux de données BigQuery dans Adobe Experience Platform. Ce connecteur de données est basé sur l’API Google BigQuery. Par conséquent, il est important de préparer correctement votre Google Cloud Platform et votre environnement BigQuery pour recevoir les appels d’API de Adobe Experience Platform.

Pour configurer le connecteur source BigQuery dans Adobe Experience Platform, vous aurez besoin des 4 valeurs suivantes :

- project
- clientId
- clientSecret
- refreshToken

Jusqu&#39;à présent, vous n&#39;avez que le premier, le **Identifiant de projet**. Ceci **Identifiant de projet** est un ID aléatoire généré par Google lorsque vous avez créé votre projet BigQuery au cours de l’exercice 12.1.

Copiez l’ID de projet dans un fichier texte séparé.

| Informations d’identification | Dénomination | Exemple |
| ----------------- |-------------| -------------|
| Identifiant du projet | random | composé-tâche-306413 |

Vous pouvez vérifier votre ID de projet à tout moment en cliquant sur **Nom du projet** dans la barre de menu supérieure :

![demo](./images/ex1/projectMenu.png)

L’ID de projet s’affiche sur le côté droit :

![demo](./images/ex1/projetcselection.png)

Dans cet exercice, vous apprendrez à obtenir les 3 autres champs obligatoires :

- clientId
- clientSecret
- refreshToken

## 12.3.1 API et services cloud Google

Pour commencer, revenez à la page d’accueil de Google Cloud Platform. Pour ce faire, cliquez simplement sur le logo dans le coin supérieur gauche de votre écran.

![demo](./images/ex2/5.png)

Une fois que vous êtes sur la page d’accueil, accédez au menu de gauche, puis cliquez sur **API et services**, puis cliquez sur **Tableau de bord**.

![demo](./images/ex2/4.png)

Vous verrez maintenant le **API et services** page d’accueil.

![demo](./images/ex2/6.png)

Sur cette page, vous pouvez voir l’utilisation de vos différentes connexions API Google. Pour configurer une connexion API afin que Adobe Experience Platform puisse lire à partir de BigQuery, vous devez suivre les étapes suivantes :

- Tout d’abord, vous devez créer un écran de consentement OAuth pour activer les authentifications futures. Pour des raisons de sécurité de Google, un être humain doit également effectuer la première authentification, avant qu’un accès programmatique ne soit autorisé.
- Deuxièmement, vous avez besoin des informations d’identification API (clientId et clientSecret) qui seront utilisées pour l’authentification API et l’accès à votre connecteur BigQuery.

## Écran de consentement OAuth 12.3.2

Commençons par créer l’écran de consentement OAuth. Dans le menu de gauche de la **API et services** homepage, cliquez sur **Écran de consentement OAuth**.

![demo](./images/ex2/6-1a.png)

Vous verrez alors :

![demo](./images/ex2/6-1.png)

Sélectionnez le Type d’utilisateur : **Externe**. Cliquez ensuite sur **CREATE**.

![demo](./images/ex2/6-2.png)

Vous serez alors sur le **Configuration de l’écran de consentement OAuth** fenêtre.

La seule chose à faire ici est de saisir le nom de l&#39;écran de consentement dans la **Nom de l’application** et sélectionnez le champ **Adresse électronique du service clientèle**. Pour le Nom de l’application, utilisez cette convention d’affectation des noms :

| Dénomination | Exemple |
| ----------------- |-------------| 
| `--demoProfileLdap-- - AEP BigQuery Connector` | vangeluw - AEP BigQuery Connector |

![demo](./images/ex2/6-3.png)

Faites ensuite défiler l’écran vers le bas jusqu’à ce que vous voyiez **Coordonnées du développeur** et indiquez une adresse électronique.

![demo](./images/ex2/6-3a.png)

Cliquez sur **ENREGISTRER ET CONTINUER**.

![demo](./images/ex2/6-4.png)

Vous verrez alors ceci. Cliquez sur **ENREGISTRER ET CONTINUER**.

![demo](./images/ex2/o1.png)

Vous verrez alors ceci. Cliquez sur **ENREGISTRER ET CONTINUER**.

![demo](./images/ex2/o2.png)

Vous verrez alors ceci. Cliquez sur **RETOUR AU TABLEAU DE BORD**.

![demo](./images/ex2/o3.png)

Vous verrez alors ceci. Cliquez sur **PUBLIER L’APPLICATION**.

![demo](./images/ex2/o4.png)

Cliquez sur **CONFIRMER**.

![demo](./images/ex2/o5.png)

Vous verrez alors ceci.

![demo](./images/ex2/o6.png)

À l’étape suivante, vous allez terminer la configuration de l’API et obtenir vos informations d’identification d’API.

## 12.3.3 Informations d’identification de l’API Google : Secret client et ID client

Dans le menu de gauche, cliquez sur **Informations d’identification**. Vous verrez alors :

![demo](./images/ex2/7.png)

Cliquez sur le bouton **+ CRÉER DES INFORMATIONS D’IDENTIFICATION** bouton .

![demo](./images/ex2/9.png)

Vous verrez 3 options. Cliquez sur le bouton **ID client OAuth**:

![demo](./images/ex2/11.png)

Dans l’écran suivant, sélectionnez **application web**.

![demo](./images/ex2/12.png)

Plusieurs nouveaux champs s’affichent. Vous devez maintenant saisir la variable **Nom** de l’ID client OAuth et saisissez également la variable **URI de redirection autorisés**.

Suivez cette convention d’affectation des noms :

| Champ | Valeur | Exemple |
| ----------------- |-------------| -------------| 
| Nom | ldap - AEP BigQuery Connector | vangeluw - Platform BigQuery Connector |
| URI de redirection autorisés | https://developers.google.com/oauthplayground | https://developers.google.com/oauthplayground |

Le **URI de redirection autorisés** est un champ très important, car vous en aurez besoin plus tard pour obtenir le RefreshToken, vous devez terminer la configuration de BigQuery Source Connector dans Adobe Experience Platform.

![demo](./images/ex2/12-1.png)

Avant de continuer, vous devez pousser physiquement le **Entrée** après avoir saisi l’URL pour stocker la valeur dans la variable **URI de redirection autorisés** champ . Si vous ne cliquez pas sur l’icône **Entrée** , vous rencontrez des problèmes ultérieurement, dans la variable **OAuth 2.0 Playground**.

Cliquez ensuite sur **Créer**:

![demo](./images/ex2/19.png)

Votre ID client et votre secret client s’affichent désormais.

![demo](./images/ex2/20.png)

Copiez ces deux champs et collez-les dans un fichier texte sur votre bureau. Vous pouvez toujours accéder à ces informations d’identification ultérieurement, mais il est plus facile de les enregistrer dans un fichier texte en regard de votre ID de projet BigQuery.

Pour récupérer votre configuration du connecteur source BigQuery dans Adobe Experience Platform, vous disposez déjà des valeurs suivantes :

| Informations d’identification de BigQuery Connector | Valeur |
| ----------------- |-------------| 
| Identifiant du projet | votre propre ID de projet (ex.: composer-task-306413) |
| clientid | yourclientid |
| cilentsecret | yourclientsecret |


Vous manquez toujours le **refreshToken**. Pour des raisons de sécurité, l’attribut refreshToken est obligatoire. Dans le monde des API, les jetons expirent généralement toutes les 24 heures. Ainsi, la variable **refreshToken** est nécessaire pour actualiser le jeton de sécurité toutes les 24 heures, de sorte que la configuration de votre connecteur source puisse continuer à se connecter à Google Cloud Platform et à BigQuery.

## 12.3.4 API BigQuery et refreshToken

Il existe de nombreuses façons d’obtenir un jeton d’actualisation pour accéder aux API Google Cloud Platform. L’une de ces options est l’utilisation de Postman, par exemple.
Cependant, Google a créé quelque chose de plus facile à tester et à lire avec ses API, un outil appelé **OAuth 2.0 Playground**.

Pour accéder à **OAuth 2.0 Playground**, accédez à [https://developers.google.com/oauthplayground](https://developers.google.com/oauthplayground).

Vous verrez alors le **OAuth 2.0 Playground** page d’accueil.

![demo](./images/ex2/22.png)

Cliquez sur le bouton **engrenage** dans le coin supérieur droit de l’écran :

![demo](./images/ex2/22-1.png)

Assurez-vous que vos paramètres sont identiques à ce que vous pouvez voir dans l’image ci-dessus.

Vérifiez deux fois que les paramètres sont sûrs à 100 %.

Une fois que vous avez terminé, cochez la case **Utilisation de vos propres informations d’identification OAuth**

![demo](./images/ex2/22-2.png)

Deux champs doivent s’afficher et vous avez la valeur pour eux.

![demo](./images/ex2/23.png)

Renseignez les champs suivants du tableau :

| Paramètres de l’API de terrain de lecture | Vos informations d’identification d’API Google |
| ----------------- |-------------| 
| ID client OAuth | votre propre identifiant client (dans le fichier texte de votre bureau) ; |
| Secret client OAuth | votre propre secret client (dans le fichier texte de votre bureau) |

![demo](./images/ex2/23-a.png)

Copiez le **ID client** et **Secret du client** dans le fichier texte que vous avez créé sur votre bureau.

![demo](./images/ex2/20.png)

Une fois que vous avez rempli vos informations d’identification, veuillez cliquer sur **Fermer**

![demo](./images/ex2/23-1.png)

Dans le menu de gauche, vous pouvez voir toutes les API Google disponibles. Rechercher **API BigQuery v2**.

![demo](./images/ex2/27.png)

Sélectionnez ensuite la portée comme indiqué dans l’image ci-dessous :

![demo](./images/ex2/26.png)

Une fois que vous les avez sélectionnés, un bouton bleu s’affiche, qui indique : **Autorisation des API**. Cliquez dessus.

![demo](./images/ex2/28.png)

Sélectionnez le compte Google que vous avez utilisé pour configurer GCP et BigQuery.

Un avertissement peut s&#39;afficher : **Cette application n’est pas vérifiée**. Cela se produit car votre Platform BigQuery Connector n’a pas encore été officiellement validé. Google ne sait donc pas s’il s’agit d’une application authentique ou non. Vous devez ignorer cette notification.

Cliquez sur **Avancé**.

![demo](./images/ex2/32.png)

Cliquez ensuite sur **Accédez à ldap - AEP BigQuery Connector (non sécurisé).**.

![demo](./images/ex2/33.png)

Vous serez redirigé vers notre écran de consentement OAuth que vous avez créé.

![demo](./images/ex2/29.png)

Si vous utilisez l’authentification à deux facteurs (2FA), saisissez le code de vérification qui vous a été envoyé.

![demo](./images/ex2/30.png)

Google vous montre maintenant huit **Autorisation** s’affiche. Cliquez sur **Autoriser** pour les huit demandes d’autorisation. (Il s’agit d’une procédure qui doit être suivie et confirmée une fois par un être humain réel, avant que l’API autorise les demandes programmatiques).

Encore une fois, **huit fenêtres contextuelles différentes** ne s’affiche pas. Vous devez cliquer sur **Autoriser** pour tous.

![demo](./images/ex2/29.png)

Après les huit demandes d’autorisation, cet aperçu s’affiche. Cliquez sur **Autoriser** pour terminer le processus.

![demo](./images/ex2/35.png)

Après la dernière **Autoriser** Cliquez en appuyant sur la touche, vous serez renvoyé à la plate-forme OAuth 2.0 et vous verrez ceci :

![demo](./images/ex2/36.png)

Cliquez sur **Échanger le code d’autorisation des jetons**.

![demo](./images/ex2/36-1.png)

Après quelques secondes, la variable **Étape 2 - Échange du code d’autorisation pour les jetons** se ferme automatiquement. vous verrez **Étape 3 - Configuration de la requête vers l’API**.

Vous devez retourner à **Étape 2 Échange du code d’autorisation pour les jetons**, puis cliquez sur **Étape 2 Échange du code d’autorisation pour les jetons** pour visualiser à nouveau le **Jeton d’actualisation**.

![demo](./images/ex2/37.png)

Vous verrez maintenant le **Jeton d’actualisation**.

![demo](./images/ex2/38.png)

Copiez le **Jeton d’actualisation** et collez-le dans le fichier texte sur votre bureau avec les autres informations d’identification du connecteur source BigQuery :

| Informations d’identification du connecteur source BigQuery | Valeur |
| ----------------- |-------------| 
| Identifiant du projet | votre propre ID de projet aléatoire (par exemple,: apt-summer-273608) |
| clientid | yourclientid |
| cilentsecret | yourclientsecret |
| refreshtoken | yourrefreshtoken |

Ensuite, configurez votre connecteur source dans Adobe Experience Platform.

## Exercice 12.3.5 - Connecter Platform à votre propre table BigQuery

Connectez-vous à Adobe Experience Platform en accédant à cette URL : [https://experience.adobe.com/platform](https://experience.adobe.com/platform).

Une fois connecté, vous accédez à la page d’accueil de Adobe Experience Platform.

![Ingestion des données](../module2/images/home.png)

Avant de continuer, vous devez sélectionner une **sandbox**. L’environnement de test à sélectionner est nommé ``--aepSandboxId--``. Pour ce faire, cliquez sur le texte **[!UICONTROL Production Prod]** dans la ligne bleue en haut de votre écran. Après avoir sélectionné l’environnement de test approprié, l’écran change et vous êtes désormais dans votre environnement de test dédié.

![Ingestion des données](../module2/images/sb1.png)

Dans le menu de gauche, accédez à Sources. Vous verrez alors le **Sources** page d’accueil. Dans le **Sources** , cliquez sur **Bases de données**. Cliquez sur le bouton **Google BigQuery** carte. Cliquez ensuite sur **Configuration** ou **+ Configurer**.

![demo](./images/1.png)

Vous devez maintenant créer une connexion.

Cliquez sur **Nouveau compte**. Vous devez maintenant renseigner tous les champs ci-dessous, en fonction de la configuration que vous avez effectuée dans GCP et BigQuery.

![demo](./images/3.png)

Commençons par nommer la connexion :

Utilisez cette convention d’affectation des noms :

| Informations d’identification de BigQuery Connector | Valeur | Exemple |
| ----------------- |-------------| -------------| 
| Nom de compte | `--demoProfileLdap-- - BigQuery Connection` | vangeluw - Connexion à BigQuery |
| Description | `--demoProfileLdap-- - BigQuery Connection` | vangeluw - Connexion à BigQuery |

Ce qui devrait vous donner quelque chose comme ceci :

![demo](./images/ex2/39-a.png)

Renseignez ensuite l’API GCP et BigQuery **Authentification du compte**-details que vous avez stocké dans un fichier texte sur votre bureau :

| Informations d’identification de BigQuery Connector | Valeur |
| ----------------- |-------------| 
| Identifiant du projet | votre propre ID de projet aléatoire (par exemple,: apt-summer-273608) |
| clientId | ... |
| clientSecret | ... |
| refreshToken | ... |

Votre **Authentification du compte**-details doit maintenant ressembler à ceci :

![demo](./images/ex2/39-xx.png)

Après avoir renseigné tous ces champs, cliquez sur **Connexion à la source**.

![demo](./images/ex2/39-2.png)

Si votre **Authentification du compte** les détails ont été correctement renseignés. vous devriez maintenant voir une confirmation visuelle du bon fonctionnement de la connexion, en voyant la variable **Connecté** confirmation.

![demo](./images/ex2/projectid.png)

Maintenant que votre connexion est créée, veuillez cliquer sur **Suivant**:

![demo](./images/42.png)

Le jeu de données BigQuery que vous avez créé lors de l’exercice 12.2 s’affiche désormais.

![demo](./images/datasets.png)

Bien joué ! Dans l’exercice suivant, vous allez charger des données de cette table et les mapper à un schéma et à un jeu de données dans Adobe Experience Platform.

Étape suivante : [12.4 Chargement de données de BigQuery dans Adobe Experience Platform](./ex4.md)

[Revenir au module 12](./customer-journey-analytics-bigquery-gcp.md)

[Revenir à tous les modules](./../../overview.md)
