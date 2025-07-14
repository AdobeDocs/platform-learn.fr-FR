---
title: Pages de destination dans Adobe Journey Optimizer
description: Pages de destination dans Adobe Journey Optimizer
kt: 5342
doc-type: tutorial
exl-id: bf499aad-91d0-4fb5-a38c-db8fcd56480b
source-git-commit: 83e8418b1a9e5e0e37f97473d2c7539ccd3fd803
workflow-type: tm+mt
source-wordcount: '1240'
ht-degree: 10%

---

# 3.6.2 Pages de destination

Connectez-vous à Adobe Journey Optimizer en allant sur [Adobe Experience Cloud](https://experience.adobe.com?lang=fr). Cliquez sur **Journey Optimizer**.

![ACOP ](./../../../../modules/delivery-activation/ajo-b2c/ajob2c-1/images/acophome.png)

Vous serez redirigé vers la vue **Accueil** dans Journey Optimizer. Tout d’abord, assurez-vous d’utiliser le bon sandbox. Le sandbox à utiliser est appelé `--aepSandboxName--`. Vous serez alors dans la vue **Accueil** de votre `--aepSandboxName--` sandbox.

![ACOP ](./../../../../modules/delivery-activation/ajo-b2c/ajob2c-1/images/acoptriglp.png)

## Listes d’abonnements 3.6.2.1

Les landing pages de Adobe Journey Optimizer fonctionnent conjointement avec les **listes d’abonnements**. Pour configurer des pages de destination, vous devez d’abord configurer des **listes d’abonnements**.

CitiSignal souhaite interroger ses clients sur leur intérêt pour les domaines suivants :

- Smart Home
- Travailler à partir de la maison
- Jeux en ligne

Une fois qu’un client a indiqué son intérêt pour l’un de ces domaines, il doit être ajouté à une liste spécifique afin de pouvoir être ciblé avec un contenu spécifique par la suite dans le cadre des campagnes à venir.

Vous allez maintenant créer 3 listes d’abonnements.

Dans le menu de gauche, accédez à **Listes d’abonnements**. Cliquez sur **Créer une liste d’abonnements**.

![Landing pages](./images/lp1.png)

Pour **Titre**, utilisez : `--aepUserLdap--_SL_Interest_in_Smart_Home`.
Pour **Description**, utilisez : `Interest in Smart Home`.

Cliquez sur **Envoyer**.

![Landing pages](./images/lp2.png)

Cliquez sur **Créer une liste d’abonnements** pour créer une autre liste.

![Landing pages](./images/lp3.png)

Pour **Titre**, utilisez : `--aepUserLdap--_SL_Interest_WFH`.
Pour **Description**, utilisez : `Interest in Work From Home`.

Cliquez sur **Envoyer**.

![Landing pages](./images/lp4.png)

Cliquez sur **Créer une liste d’abonnements** pour créer une autre liste.

![Landing pages](./images/lp5.png)

Pour **Titre**, utilisez : `--aepUserLdap--_SL_Interest_Online_Gaming`.
Pour **Description**, utilisez : `Interest in Online Gaming`.

Cliquez sur **Envoyer**.

![Landing pages](./images/lp6.png)

Vous avez maintenant créé les 3 listes dont vous avez besoin.

![Landing pages](./images/lp7.png)

## Préréglage De La Page De Destination 3.6.2.2

Pour utiliser les pages de destination dans Adobe Journey Optimizer, un préréglage doit être créé.

Dans le menu de gauche, accédez à **Administration** > **Canaux** puis sélectionnez **Préréglages de page de destination**.

Cliquez sur **Créer un préréglage de page de destination**.

![Landing pages](./images/lp8.png)

Pour le champ **Nom**, utilisez : `--aepUserLdap-- - CitiSignal LP` et sélectionnez le sous-domaine disponible dans votre instance.

>[!NOTE]
>
>Si vous ne voyez pas de sous-domaine dans votre instance, contactez votre administrateur AJO pour en ajouter un.

Cliquez sur **Envoyer**.

![Landing pages](./images/lp9.png)

Votre préréglage de page de destination a maintenant été créé.

![Landing pages](./images/lp10.png)

## Page de destination 3.6.2.3

Vous pouvez maintenant créer votre page de destination. Dans le menu de gauche, accédez à **Gestion de contenu** > **Pages de destination**.

Cliquez sur **Créer une page de destination**.

![Landing pages](./images/lp11.png)

Pour le champ **Titre**, utilisez : `vangeluw - CitiSignal Interests`. Sélectionnez ensuite le **préréglage de la page de destination** que vous avez configuré à l’étape précédente.

Cliquez sur **Créer**.

![Landing pages](./images/lp12.png)

Vous devriez alors voir ceci.

![Landing pages](./images/lp13.png)

Remplacez le champ **Nom de la page** par `--aepUserLdap-- - CitiSignal Interests`.

Saisissez ce nom personnalisé sous **Paramètres d’accès** : `--aepUserLdap---citisignal-interests`.

Cliquez sur **Ouvrir Designer**.

![Landing pages](./images/lp14.png)

Sélectionnez **Créer en partant de zéro**.

![Landing pages](./images/lp15.png)

Vous devriez alors voir ceci.

![Landing pages](./images/lp16.png)

Ajoutez un composant de structure **colonne 1:1** à la zone de travail.

![Landing pages](./images/lp17.png)

Ajoutez un composant de contenu **Formulaire** à la zone de travail.

![Landing pages](./images/lp18.png)

Remplacez le champ **Libellé** de **Case à cocher 1** par `Keep me updated about CitiSignal's offering for Smart Home`.

Assurez-vous que la case à cocher **Opt-in si cochée** est activée et que **Liste d’abonnements** est sélectionnée.

Cliquez ensuite sur **Sélectionner une liste d’abonnements**.

![Landing pages](./images/lp19.png)

Sélectionnez ensuite le `--aepUserLdap--_SL_Interest_in_Smart_Home` de liste et cliquez sur **Sélectionner**.

![Landing pages](./images/lp20.png)

Cliquez sur **+ Ajouter un champ** puis sélectionnez **Case à cocher**.

![Landing pages](./images/lp21.png)

Vous devriez alors voir ceci.

![Landing pages](./images/lp22.png)

Remplacez le champ **Libellé** de **Case à cocher 2** par `Keep me updated about CitiSignal's offering for Work From Home`.

Assurez-vous que la case à cocher **Opt-in si cochée** est activée et que **Liste d’abonnements** est sélectionnée.

Cliquez ensuite sur **Sélectionner une liste d’abonnements**.

![Landing pages](./images/lp23.png)

Sélectionnez ensuite le `--aepUserLdap--_SL_Interest_WFH` de liste et cliquez sur **Sélectionner**.

![Landing pages](./images/lp24.png)

Cliquez sur **+ Ajouter un champ** puis sélectionnez **Case à cocher**.

![Landing pages](./images/lp25.png)

Vous devriez alors voir ceci.

![Landing pages](./images/lp26.png)

Remplacez le champ **Libellé** de **Case à cocher 3** par `Keep me updated about CitiSignal's offering for Online Gaming`.

Assurez-vous que la case à cocher **Opt-in si cochée** est activée et que **Liste d’abonnements** est sélectionnée.

Cliquez ensuite sur **Sélectionner une liste d’abonnements**.

![Landing pages](./images/lp27.png)

Sélectionnez ensuite le `--aepUserLdap--_SL_Interest_Online_Gaming` de liste et cliquez sur **Sélectionner**.

![Landing pages](./images/lp28.png)

Vous devriez alors voir ceci.

![Landing pages](./images/lp29.png)

Accédez au champ de formulaire **CALL TO ACTION**.

Mettez à jour les champs suivants :

- **Texte** - Libellé du bouton : `Save`.
- **Action de confirmation** : sélectionnez **Texte de confirmation**.
- **Texte de confirmation** : utilisez : `Thanks for updating your preferences!`.
- **Action d’erreur** : sélectionnez **Texte d’erreur**.
- **Texte d’erreur** : utilisez : `There was an error updating your preferences.`

Cliquez sur **Enregistrer** puis sur la flèche dans le coin supérieur gauche pour revenir à l’écran précédent.

![Landing pages](./images/lp30.png)

Cliquez sur **Publier**.

![Landing pages](./images/lp31.png)

Cliquez de nouveau sur **Publier**.

![Landing pages](./images/lp32.png)

Votre page de destination est maintenant publiée et peut être utilisée dans un e-mail.

![Landing pages](./images/lp33.png)

## 3.6.2.4 inclure la page de destination dans l’e-mail

Dans l’exercice 3.1, vous avez créé un parcours appelé `--aepUserLdap-- - Registration Journey`.

![ACOP ](./../../../../modules/delivery-activation/ajo-b2c/ajob2c-1/images/published.png)

Vous devez maintenant mettre à jour l’e-mail dans ce parcours pour inclure le lien vers la page de destination.

Dans le menu de gauche, accédez à **Parcours** puis cliquez pour ouvrir le `--aepUserLdap-- - Registration Journey` de parcours.

![Landing pages](./images/lp34.png)

Cliquez sur **Plus...**, puis sélectionnez **Créer une version**.

![Landing pages](./images/lp35.png)

Cliquez sur **Créer une version**.

![Landing pages](./images/lp36.png)

Cliquez pour sélectionner l’action **E-mail**, puis sélectionnez **Modifier le contenu**.

![Landing pages](./images/lp37.png)

Cliquez sur **Modifier le corps de l’e-mail**.

![Landing pages](./images/lp38.png)

Vous devriez alors voir quelque chose comme ça. Ajoutez un nouveau composant de structure **colonne 1:1** à la zone de travail.

![Landing pages](./images/lp39.png)

Ajoutez un nouveau composant de contenu **Texte** dans le composant de structure nouvellement créé.

![Landing pages](./images/lp40.png)

Collez le texte suivant dans le composant de contenu **Texte**.

`Would you like to hear from us about Smart Home news? Do you work from home and would you like to hear our tips? Or are you an avid online gamer and do you want to receive our game reviews? Click here to update your preferences and interests!`

Appliquez un style à votre texte pour qu’il ressemble à ceci, puis sélectionnez le mot `here`. Cliquez sur l’icône **lien**.

Définissez le **Type** du lien sur **Page de destination** et définissez le champ **Cible** sur **Vide**.

Cliquez sur l’icône **modifier** pour sélectionner la page de destination à lier.

![Landing pages](./images/lp41.png)

Sélectionnez l’`--aepUserLdap-- - CitiSignal Interests` de la page de destination. Cliquez sur **Sélectionner**.

![Landing pages](./images/lp42.png)

Vous devriez alors voir ceci. Cliquez sur **Enregistrer**.

![Landing pages](./images/lp43.png)

Cliquez sur la flèche située dans le coin supérieur gauche pour revenir à l’écran précédent.

![Landing pages](./images/lp44.png)

Cliquez sur la flèche dans le coin supérieur gauche pour revenir à l’écran précédent.

![Landing pages](./images/lp45.png)

Cliquez sur **Enregistrer**.

![Landing pages](./images/lp46.png)

Cliquez sur **Publier**.

![Landing pages](./images/lp47.png)

Cliquez de nouveau sur **Publier**.

![Landing pages](./images/lp48.png)

Vos modifications ont maintenant été publiées et vous pouvez tester votre parcours.

![Landing pages](./images/lp49.png)

## 3.6.2.5 Tester le parcours et la page de destination

Accédez à [https://dsn.adobe.com](https://dsn.adobe.com). Après vous être connecté avec votre Adobe ID, voici ce que vous verrez. Cliquez sur le **de 3 points...** sur le projet de votre site web, puis cliquez sur **Exécuter** pour l’ouvrir.

![DSN ](./../../datacollection/dc1.1/images/web8.png)

Vous verrez ensuite votre site web de démonstration s’ouvrir. Sélectionnez l’URL et copiez-la dans le presse-papiers.

![DSN ](../../../getting-started/gettingstarted/images/web3.png)

Ouvrez une nouvelle fenêtre de navigateur en mode privé.

![DSN ](../../../getting-started/gettingstarted/images/web4.png)

Collez l’URL de votre site web de démonstration, que vous avez copiée à l’étape précédente. Il vous sera ensuite demandé de vous connecter à l’aide de votre Adobe ID.

![DSN ](../../../getting-started/gettingstarted/images/web5.png)

Sélectionnez votre type de compte et terminez le processus de connexion.

![DSN ](../../../getting-started/gettingstarted/images/web6.png)

Votre site web est alors chargé dans une fenêtre de navigateur en mode privé. Pour chaque exercice, vous devrez utiliser une nouvelle fenêtre de navigateur en mode privé pour charger l’URL de votre site web de démonstration. Accédez à **Se connecter**

![DSN ](../../../getting-started/gettingstarted/images/web7.png)

Cliquez sur **CRÉER UN COMPTE**. Renseignez vos informations et cliquez sur **S’inscrire**.

![Démonstration](./../../../../modules/delivery-activation/datacollection/dc1.2/images/pv9.png)

Vous serez maintenant redirigé vers la page d’accueil. Ouvrez le panneau Visionneuse de profils et accédez au profil client en temps réel. Dans le panneau Visionneuse de profil, toutes vos données personnelles doivent s’afficher, comme vos nouveaux identifiants d’e-mail et de téléphone ajoutés.

![Démonstration](./../../../../modules/delivery-activation/datacollection/dc1.2/images/pv10.png)

1 minute après la création de votre compte, vous recevrez un e-mail de création de compte de Adobe Journey Optimizer.

Cliquez sur le lien contenu dans l’e-mail pour mettre à jour vos préférences.

![Configuration de Launch](./images/email.png)

Vous devriez alors voir le formulaire que vous avez créé. Cochez certaines cases et cliquez sur **Enregistrer**.

![Configuration de Launch](./images/email1.png)

Un message de confirmation s’affiche alors.

![Configuration de Launch](./images/email2.png)

## 3.6.2.6 rapports de liste d’abonnements

Pour afficher les rapports disponibles sur les listes d’abonnements, accédez à **Listes d’abonnements** dans le menu de gauche, puis cliquez pour ouvrir l’une des listes d’abonnements que vous avez configurées précédemment.

![Landing pages](./images/lp50.png)

Cliquez sur **Rapport**.

![Landing pages](./images/lp51.png)

Vous devriez alors voir l’aperçu de la liste, avec le nombre de personnes qui se sont inscrites ou désinscrites.

![Landing pages](./images/lp52.png)

## Étapes suivantes

Accédez à [3.6.3 AJO et GenStudio for Performance Marketing](./ex3.md)

Revenez à [Adobe Journey Optimizer : Gestion de contenu](./ajocontent.md){target="_blank"}

Revenir à [Tous les modules](./../../../../overview.md){target="_blank"}
