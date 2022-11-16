---
title: Foundation - Real-time Customer Profile - Visualisez votre propre profil client en temps réel - interface utilisateur
description: Foundation - Real-time Customer Profile - Visualisez votre propre profil client en temps réel - interface utilisateur
kt: 5342
audience: Data Engineer, Data Architect, Marketer
doc-type: tutorial
activity: develop
exl-id: ed13e37f-48eb-4668-b828-6c58340a7cc1
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '557'
ht-degree: 2%

---

# 3.2 Visualisation de votre propre profil client en temps réel - interface utilisateur

Au cours de cet exercice, vous vous connecterez à Adobe Experience Platform et afficherez votre propre profil client en temps réel dans l’interface utilisateur.

## Histoire

Dans Real-time Customer Profile, toutes les données de profil s’affichent avec les données d’événement, ainsi que les appartenances à des segments existants. Les données affichées peuvent provenir de n’importe où, des applications d’Adobe et des solutions externes. Il s’agit de la vue la plus puissante de Adobe Experience Platform, le véritable système d’enregistrement d’expérience.

## 3.2.1 Utilisation de la vue Profil client dans Adobe Experience Platform

Accédez à [Adobe Experience Platform](https://experience.adobe.com/platform). Une fois connecté, vous accédez à la page d’accueil de Adobe Experience Platform.

![Ingestion des données](../module2/images/home.png)

Avant de continuer, vous devez sélectionner une **sandbox**. L’environnement de test à sélectionner est nommé ``--aepSandboxId--``. Pour ce faire, cliquez sur le texte **[!UICONTROL Production Prod]** dans la ligne bleue en haut de votre écran. Après avoir sélectionné le [!UICONTROL sandbox], vous verrez le changement d’écran et vous êtes maintenant dans votre [!UICONTROL sandbox].

![Ingestion des données](../module2/images/sb1.png)

Dans le menu de gauche, accédez à **Profils** et à **Parcourir**.

![Profil client](./images/homemenu.png)

Dans le panneau Visionneuse de profils de votre site web, vous pouvez trouver plusieurs identités. Chaque identité est liée à un espace de noms.

![Profil client](./images/identities.png)

Dans le panneau Visionneuse de profils, vous pouvez voir ces combinaisons d’identifiants et d’espaces de noms :

| Identité | Espace de noms |
|:-------------:| :---------------:|
| Experience Cloud ID (ECID) | 12507560687324495704459439363261812234 |
| Email ID | woutervangeluwe+06022022-01@gmail.com |
| Identifiant du numéro de mobile | +32473622044+06022022-01 |

Avec Adobe Experience Platform, tous les identifiants sont également importants. Auparavant, l’ECID était l’identifiant le plus important dans le contexte de l’Adobe et tous les autres identifiants étaient liés à l’ECID dans une relation hiérarchique. Avec Adobe Experience Platform, ce n’est plus le cas, et chaque ID peut être considéré comme un identifiant Principal.

En règle générale, l’identifiant Principal dépend du contexte. Si vous demandez à votre centre d’appels, **Quel est l’identifiant le plus important ?** ils répondront probablement, **le numéro de téléphone !** Mais si vous demandez à votre équipe CRM, elle répond : **L&#39;adresse email !**  Adobe Experience Platform comprend cette complexité et la gère à votre place. Chaque application, qu’elle soit Adobe ou non, parlera avec Adobe Experience Platform en se référant à l’identifiant qu’elle considère Principal. Et ça marche tout simplement.

Pour le champ **Espace de noms d’identité**, sélectionnez **Email** et pour le champ **Valeur d’identité** saisissez l’adresse électronique que vous avez utilisée pour vous enregistrer dans l’exercice précédent. Cliquez sur **Affichage**. Votre profil s’affiche alors dans la liste. Cliquez sur le bouton **Identifiant de profil** pour ouvrir votre profil.

![Profil client](./images/popupecid.png)

Vous voyez maintenant un aperçu de quelques éléments importants **Attributs de profil** de votre profil client.

![Profil client](./images/profile.png)

Si vous souhaitez voir tous les attributs de profil disponibles pour votre profil, accédez à **Attributs**.

![Profil client](./images/profilattr.png)

Accédez à **Événements**, où vous pouvez voir les entrées pour chaque événement d’expérience lié à votre profil.

![Profil client](./images/profileee.png)

Enfin, accédez à l’option de menu **abonnement au segment**. Vous verrez désormais tous les segments à inclure dans ce profil.

![Profil client](./images/profileseg.png)

Maintenant que vous avez appris à afficher le profil en temps réel d’un client en utilisant l’interface utilisateur de Adobe Experience Platform, faisons de même avec les API en utilisant Postman et l’Adobe I/O pour effectuer des requêtes contre les API de Adobe Experience Platform.

Étape suivante : [3.3 Visualiser votre propre profil client en temps réel - API](./ex3.md)

[Revenir au module 3](./real-time-customer-profile.md)

[Revenir à tous les modules](../../overview.md)
