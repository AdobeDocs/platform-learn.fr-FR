---
title: Migration des variables globales
description: Découvrez comment migrer des variables globales de la configuration de l’extension Analytics vers Web SDK
solution: Data Collection, Analytics
feature: Web SDK
jira: KT-17277
exl-id: 0917e951-c7e0-4723-8354-d308890bdaac
source-git-commit: 744b26da58307f0d6f6e8715a534ca814e02371c
workflow-type: tm+mt
source-wordcount: '609'
ht-degree: 3%

---

# Migration des variables globales

Dans cet exercice, vous apprendrez à migrer des variables globales de la configuration de l’extension Analytics vers Web SDK.

## Vue d’ensemble

L’extension Adobe Analytics contient une section de configuration appelée « Variables globales ».

![Libellé Variables Globales](assets/analytics-global-variables-label.jpg)

Les variables globales sont des variables définies sur l’objet de suivi Analytics lorsque cet objet est initialisé sur la page. Toutes les variables que vous définissez ici seront définies lorsque l’objet de suivi est créé sur chaque page.

![Ensemble de variables globales](assets/analytics-set-global-variables.jpg)

Si des variables sont définies ici, nous devons également les migrer vers le SDK Web.

## Où ajouter des variables globales dans le Web SDK

Le **résultat** ici est qu’il n’y a pas de zone équivalente dans la configuration de l’extension Web SDK, ce ne sera donc pas aussi facile que de simplement copier sur les variables comme nous l’avons fait dans l’exercice Règle de chargement de page par défaut.
La réponse courte est plutôt la suivante : **Créez une règle qui s’exécute avant les autres règles sur chaque page et définissez-y les variables.**

Si vous n’avez pas besoin d’étapes définies, faites-le et vous en avez terminé avec cette leçon. Si vous souhaitez obtenir de l’aide, continuez...

### Étapes de migration des variables globales vers Web SDK

1. Ouvrez la configuration de l’extension Adobe Analytics

   ![Configuration de l’extension AA](assets/configure-analytics-extension.jpg)

1. Faites défiler l’écran jusqu’à la section Variables globales (image ci-dessus), ouvrez-la et notez toutes les variables définies. Vous devrez connaître ces variables et valeurs à une étape ultérieure.
1. Annulez l’abandon de l’extension Analytics.
1. Sélectionnez **Règles** dans le volet de navigation de gauche, puis cliquez sur **Ajouter une règle**.
1. Nommez votre nouvelle règle « Variables globales ».
1. Cliquez sur le bouton Ajouter sous Événements.

   ![Règle de variable globale 1](assets/global-variable-rule-1.jpg)

1. Configurez votre événement à déclencher avant vos autres règles. Vous devez connaître le type d’événement et l’ordre que vous avez utilisé dans d’autres règles. Exemples de valeurs :
   1. Définissez **Extension** sur Core
   1. Le **type d’événement** peut être Prêt pour DOM, selon votre implémentation
   1. Développez le **Options avancées**
   1. Définissez la variable **Ordre** sur un nombre inférieur à celui de vos autres règles, de sorte qu’elle s’exécute en premier.

      ![Configurer l’événement de variable global](assets/configure-global-variable-event.jpg)
      >[!NOTE]
      >
      >L’essentiel ici est que cette règle se déclenche avant la règle de chargement de page par défaut, de sorte que toutes les variables définies dans cette règle puissent être envoyées dans Analytics via la règle sendEvent. Cependant, nous suggérons que cette règle s’exécute **en premier** globalement, car les variables définies dans la section Variables globales de l’extension Analytics pourraient être modifiées dans d’autres règles. Nous imitons cette fonctionnalité. Dans l’exemple ci-dessus, nous supposons que « 10 » est un numéro de commande inférieur à toutes vos autres règles. Si ce n’est pas le cas, veuillez modifier ce nombre en un nombre inférieur à vos autres règles.
1. Sélectionnez **Conserver les modifications** pour enregistrer votre travail.
1. Vous n’avez pas besoin d’ajouter de conditions à cette règle. Vous pouvez donc laisser cette section de création de règle seule.
1. Cliquez sur l’icône plus sous la section **Actions**
1. Configurer la nouvelle action
   1. Choisissez l’extension Adobe Experience Platform Web SDK **extension**
   1. Pour **Type d’action**, choisissez Mettre à jour la variable
   1. À droite, choisissez votre variable **Élément de données** (pour ce tutoriel, elle s’appelait « Élément de données de page vue », mais le vôtre peut varier)
   1. Sélectionnez **Analytics** sous l’objet de données
   1. Renseignez les variables que vous avez enregistrées à partir de la section Variables globales de la configuration de l’extension Analytics (dans l’exemple de ce tutoriel, définir eVar10 sur l’élément de données de type page)

   ![websdk-global-variables-action](assets/websdk-global-variables-action.jpg)

1. Conserver les modifications
1. Enregistrer la règle dans votre bibliothèque de travail et la créer

Vos variables globales sont désormais migrées vers Web SDK et se déclenchent à chaque chargement de page.
