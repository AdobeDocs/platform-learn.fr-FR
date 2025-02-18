---
title: Foundation - Profil client en temps réel - Visualiser votre propre profil client en temps réel - Interface utilisateur
description: Foundation - Profil client en temps réel - Visualiser votre propre profil client en temps réel - Interface utilisateur
kt: 5342
doc-type: tutorial
exl-id: 66cb9b20-46e0-4b4a-af38-aa152bba342a
source-git-commit: 3d61d91111d8693ab031fbd7b26706c02818108c
workflow-type: tm+mt
source-wordcount: '570'
ht-degree: 1%

---

# 2.1.2 Visualiser votre propre profil client en temps réel - Interface utilisateur

Dans cet exercice, vous allez vous connecter à Adobe Experience Platform et afficher votre propre profil client en temps réel dans l’interface utilisateur.

## Contexte

Dans le profil client en temps réel, toutes les données de profil s’affichent avec les données d’événement, ainsi que les appartenances à des segments existants. Les données affichées peuvent provenir de n’importe où, des applications Adobe et des solutions externes. Il s’agit de la vue la plus puissante de Adobe Experience Platform, le véritable système d’expérience d’enregistrement.

## Utilisation de la vue Profil client dans Adobe Experience Platform

Accédez à [Adobe Experience Platform](https://experience.adobe.com/platform). Une fois connecté, vous accédez à la page d’accueil de Adobe Experience Platform.

![Ingestion des données](../../datacollection/dc1.2/images/home.png)

Avant de continuer, vous devez sélectionner un **sandbox**. Le sandbox à sélectionner est nommé ``--aepSandboxName--``. Après avoir sélectionné la [!UICONTROL sandbox] appropriée, la modification d’écran s’affiche et vous êtes maintenant dans votre [!UICONTROL sandbox] dédié.

![Ingestion des données](../../datacollection/dc1.2/images/sb1.png)

Dans le menu de gauche, accédez à **Profils** et à **Parcourir**.

![Profil client](./images/homemenu.png)

Dans le panneau Visionneuse de profils de votre site Web, vous pouvez trouver plusieurs identités. Chaque identité est liée à un espace de noms.

![Profil client](./images/identities.png)

Dans le panneau Visionneuse de profils, vous pouvez voir les combinaisons d’identifiants et d’espaces de noms suivantes :

| Identité | Espace de noms |
|:-------------:| :---------------:|
| Experience Cloud ID (ECID) | 79943948563923140522865572770524243489 |
| Experience Cloud ID (ECID) | 70559351147248820114888181867542007989 |
| ID d’e-mail | woutervangeluwe+18112024-01@gmail.com |
| ID du numéro de mobile | +32473622044+18112024-01 |

Avec Adobe Experience Platform, tous les identifiants sont également importants. Auparavant, l’ECID était l’identifiant le plus important dans le contexte Adobe et tous les autres identifiants étaient liés à l’ECID dans une relation hiérarchique. Avec Adobe Experience Platform, ce n’est plus le cas, et chaque identifiant peut être considéré comme un identifiant principal.

En règle générale, l’identifiant principal dépend du contexte. Si vous demandez à votre centre d&#39;appels, **Quel est l&#39;ID le plus important ?** ils répondront probablement, **le numéro de téléphone !** Mais si vous demandez à votre équipe CRM, ils vous répondront, **l&#39;adresse e-mail !** Adobe Experience Platform comprend cette complexité et la gère pour vous. Chaque application, qu’il s’agisse d’une application Adobe ou d’une application autre qu’Adobe, communique avec Adobe Experience Platform en se référant à l’identifiant qu’elle considère comme principal. Et ça marche tout simplement.

Pour le champ **Espace de noms d’identité**, sélectionnez **E-mail** et pour le champ **Valeur d’identité** saisissez l’adresse e-mail que vous avez utilisée pour vous enregistrer dans l’exercice précédent. Cliquez sur **Afficher**. Votre profil apparaît alors dans la liste. Cliquez sur le **Identifiant de profil** pour ouvrir votre profil.

![Profil client](./images/popupecid.png)

Vous voyez maintenant un aperçu de quelques **attributs de profil** importants de votre profil client. Pour afficher tous les attributs de profil disponibles pour votre profil, cliquez sur **Attributs**.

![Profil client](./images/profile.png)

Une liste complète de tous les attributs s’affiche alors.

![Profil client](./images/profilattr.png)

Accédez à **Événements**, où vous pouvez voir les entrées de chaque événement d’expérience lié à votre profil.

![Profil client](./images/profileee.png)

Enfin, accédez à l’option de menu **Appartenance à une audience**. Vous trouverez ici toutes les audiences admissibles de ce client. La liste peut actuellement être vide, mais cela changera dans les modules suivants.

![Profil client](./images/profileseg.png)

Maintenant que vous avez appris à afficher le profil en temps réel de n’importe quel client à l’aide de l’interface utilisateur de Adobe Experience Platform, faisons de même via les API en utilisant Postman et Adobe I/O pour effectuer des requêtes sur les API de Adobe Experience Platform.

## Étapes suivantes

Accédez à [2.1.3 Visualiser votre propre profil client en temps réel - API](./ex3.md){target="_blank"}

Revenez au [profil client en temps réel](./real-time-customer-profile.md){target="_blank"}

Revenir à [Tous les modules](./../../../../overview.md){target="_blank"}
