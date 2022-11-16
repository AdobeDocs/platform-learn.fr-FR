---
title: Adobe Journey Optimizer - API météorologique externe, action SMS, etc. - Définir des actions personnalisées
description: Adobe Journey Optimizer - API météorologique externe, action SMS, etc. - Définir des actions personnalisées
kt: 5342
audience: Data Engineer, Data Architect, Orchestration Engineer, Marketer
doc-type: tutorial
activity: develop
exl-id: 7ee5aee9-3740-4eee-9f53-a44fdb564a00
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '514'
ht-degree: 3%

---

# 8.3 Définition d’une action personnalisée

Dans cet exercice, vous allez créer deux actions personnalisées en combinant l’utilisation de Adobe Journey Optimizer.

Connectez-vous à Adobe Journey Optimizer en accédant à [Adobe Experience Cloud](https://experience.adobe.com). Cliquez sur **Journey Optimizer**.

![ACOP](../module7/images/acophome.png)

Vous serez redirigé vers le **Accueil**  dans Journey Optimizer. Tout d’abord, assurez-vous d’utiliser l’environnement de test approprié. L’environnement de test à utiliser est appelé `--aepSandboxId--`. Pour passer d’un environnement de test à un autre, cliquez sur **Production (VA7)** et sélectionnez l’environnement de test dans la liste. Dans cet exemple, l’environnement de test est nommé **Activation AEP FY22**. Vous serez alors dans le **Accueil** affichage de votre environnement de test `--aepSandboxId--`.

![ACOP](../module7/images/acoptriglp.png)

Dans le menu de gauche, faites défiler l’écran vers le bas et cliquez sur **Configurations**. Cliquez ensuite sur le **Gérer** sous **Actions**.

![Démonstration](./images/menuactions.png)

Vous verrez alors le **Actions** liste.

![Démonstration](./images/acthome.png)

Vous définissez une action qui envoie du texte à un canal de Slack.

## 8.3.1 Action : Envoyer du texte au canal Slack

Vous allez maintenant utiliser un canal de Slack existant et envoyer des messages à ce canal de Slack. Slack dispose d’une API conviviale et nous allons utiliser Adobe Journey Optimizer pour déclencher son API.

![Démonstration](./images/slack.png)

Cliquez sur **Créer une action** pour commencer à ajouter une nouvelle action.

![Démonstration](./images/adda.png)

Une fenêtre contextuelle Action vide s’affiche.

![Démonstration](./images/emptyact.png)

Comme nom de l’action, utilisez `--demoProfileLdap--TextSlack`. Dans cet exemple, le nom de l’action est `vangeluwTextSlack`.

Définissez la description sur : `Send Text to Slack`.

![Démonstration](./images/slackname.png)

Pour le **Configuration d’URL**, utilisez ceci :

- URL: `https://2mnbfjyrre.execute-api.us-west-2.amazonaws.com/prod`
- Méthode : **POST**

>[!NOTE]
>
>L’URL ci-dessus fait référence à une fonction AWS Lambda qui transmettra ensuite votre requête au canal du Slack comme mentionné ci-dessus. Cela permet de protéger l’accès à un canal de Slack détenu par l’Adobe. Si vous disposez de votre propre canal de Slack, vous devez créer une application de Slack via [https://api.slack.com/](https://api.slack.com/), vous devez ensuite créer un webhook entrant dans cette application de Slack, puis remplacer l’URL ci-dessus par l’URL de webhook entrant.

Il n’est pas nécessaire de modifier les champs d’en-tête.

![Démonstration](./images/slackurl.png)

**Authentification** doit être défini sur **Aucune authentification**.

![Démonstration](./images/slackauth.png)

Pour le **Paramètres d’action**, vous devez définir les champs à envoyer au Slack. En toute logique, nous voulons que Adobe Journey Optimizer et Adobe Experience Platform soient le cerveau de la personnalisation, de sorte que le texte à envoyer au Slack doit être défini par Adobe Journey Optimizer, puis envoyé au Slack pour exécution.

Pour le **Paramètres d’action**, cliquez sur le bouton **Modifier la charge utile** icône .

![Démonstration](./images/slackmsgp.png)

Vous verrez alors une fenêtre contextuelle vide.

![Démonstration](./images/slackmsgpopup.png)

Copiez le texte ci-dessous et collez-le dans la fenêtre contextuelle vide.

```json
{
 "text": {
  "toBeMapped": true,
  "dataType": "string",
  "label": "textToSlack"
 }
}
```

FYI : en spécifiant les champs ci-dessous, ces champs deviennent accessibles à partir de votre Parcours client et vous pourrez les remplir dynamiquement à partir du Parcours :

**&quot;toBeMapped&quot;: true,**

**&quot;dataType&quot;: &quot;string&quot;,**

**&quot;label&quot;: &quot;textToSlack&quot;**

Vous verrez alors :

![Démonstration](./images/slackmsgpopup1.png)

Cliquez sur **Enregistrer**.

![Démonstration](./images/twiliomsgpopup2.png)

Faites défiler la page vers le haut et cliquez sur **Enregistrer** une fois de plus pour enregistrer votre action personnalisée.

![Démonstration](./images/slackmsgpopup3.png)

Votre action personnalisée fait désormais partie de la **Actions** liste.

![Démonstration](./images/slackdone.png)

Vous avez défini des événements, des sources de données externes et des actions. Maintenant, consolidons tout ça en un parcours.

Étape suivante : [8.4 Création de votre parcours et de vos messages](./ex4.md)

[Revenir au module 8](journey-orchestration-external-weather-api-sms.md)

[Revenir à tous les modules](../../overview.md)
