---
title: Foundation - Real-time Customer Profile - Visualisez votre propre profil client en temps réel - interface utilisateur
description: Foundation - Real-time Customer Profile - Visualisez votre propre profil client en temps réel - interface utilisateur
kt: 5342
doc-type: tutorial
source-git-commit: 2cdc145d7f3933ec593db4e6f67b60961a674405
workflow-type: tm+mt
source-wordcount: '564'
ht-degree: 1%

---

# 2.1.2 Visualisation de votre propre profil client en temps réel - interface utilisateur

Au cours de cet exercice, vous vous connecterez à Adobe Experience Platform et afficherez votre propre profil client en temps réel dans l’interface utilisateur.

## Histoire

Dans Real-time Customer Profile, toutes les données de profil s’affichent avec les données d’événement, ainsi que les appartenances à des segments existants. Les données affichées peuvent provenir de n’importe où, des applications d’Adobe et des solutions externes. Il s’agit de la vue la plus puissante de Adobe Experience Platform, le véritable système d’enregistrement d’expérience.

## 2.1.2.1 Utilisation de la vue Profil client dans Adobe Experience Platform

Accédez à [Adobe Experience Platform](https://experience.adobe.com/platform). Une fois connecté, vous accédez à la page d’accueil de Adobe Experience Platform.

![Ingestion des données](../../datacollection/module1.2/images/home.png)

Avant de continuer, vous devez sélectionner un **sandbox**. L’environnement de test à sélectionner est nommé ``--aepSandboxId--``. Pour ce faire, cliquez sur le texte **[!UICONTROL Production Prod]** dans la ligne bleue en haut de votre écran. Après avoir sélectionné l’[!UICONTROL sandbox] approprié, vous verrez le changement d’écran et vous êtes désormais dans votre [!UICONTROL sandbox] dédié.

![Ingestion des données](../../datacollection/module1.2/images/sb1.png)

Dans le menu de gauche, accédez à **Profils** et à **Parcourir**.

![Profil client](./images/homemenu.png)

Dans le panneau Visionneuse de profils de votre site web, vous pouvez trouver plusieurs identités. Chaque identité est liée à un espace de noms.

![Profil client](./images/identities.png)

Dans le panneau Visionneuse de profils, vous pouvez voir ces combinaisons d’identifiants et d’espaces de noms :

| Identité | Espace de noms |
|:-------------:| :---------------:|
| Identifiant Experience Cloud (ECID) | 12507560687324495704459439363261812234 |
| Email ID | woutervangeluwe+06022022-01@gmail.com |
| Identifiant du numéro de mobile | +32473622044+06022022-01 |

Avec Adobe Experience Platform, tous les identifiants sont également importants. Auparavant, l’ECID était l’identifiant le plus important dans le contexte de l’Adobe et tous les autres identifiants étaient liés à l’ECID dans une relation hiérarchique. Avec Adobe Experience Platform, ce n’est plus le cas, et chaque ID peut être considéré comme un identifiant principal.

En règle générale, l’identifiant principal dépend du contexte. Si vous demandez à votre centre d&#39;appels, **Quel est l&#39;identifiant le plus important ?** ils répondront probablement, **le numéro de téléphone !** Mais si vous demandez à votre équipe de gestion de la relation client, ils répondront, **L&#39;adresse email !** Adobe Experience Platform comprend cette complexité et la gère à votre place. Chaque application, qu’elle soit Adobe ou non, parlera avec Adobe Experience Platform en se référant à l’identifiant qu’elle considère comme principal. Et ça marche tout simplement.

Pour le champ **Identity namespace**, sélectionnez **Email** et pour le champ **Identity Value**, saisissez l’adresse électronique que vous avez utilisée pour l’enregistrement dans l’exercice précédent. Cliquez sur **Afficher**. Votre profil s’affiche alors dans la liste. Cliquez sur l’ **ID de profil** pour ouvrir votre profil.

![Profil client](./images/popupecid.png)

Vous voyez maintenant un aperçu de quelques **attributs de profil** importants de votre profil client.

![Profil client](./images/profile.png)

Si vous souhaitez voir tous les attributs de profil disponibles pour votre profil, accédez à **Attributs**.

![Profil client](./images/profilattr.png)

Accédez à **Événements**, où vous pouvez voir les entrées pour chaque événement d’expérience lié à votre profil.

![Profil client](./images/profileee.png)

Enfin, accédez à l’option de menu **Appartenance au segment**. Vous verrez désormais tous les segments à inclure dans ce profil.

![Profil client](./images/profileseg.png)

Maintenant que vous avez appris à afficher le profil en temps réel d’un client en utilisant l’interface utilisateur de Adobe Experience Platform, faisons de même avec les API en utilisant Postman et l’Adobe I/O pour effectuer des requêtes contre les API de Adobe Experience Platform.

Étape suivante : [2.1.3 Visualiser votre propre profil client en temps réel - API](./ex3.md)

[Revenir au module 2.1](./real-time-customer-profile.md)

[Revenir à tous les modules](../../../overview.md)
