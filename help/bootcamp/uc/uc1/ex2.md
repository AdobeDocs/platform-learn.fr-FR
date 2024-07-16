---
title: Bootcamp - Real-time Customer Profile - Visualisez votre propre profil client en temps réel - interface utilisateur
description: Bootcamp - Real-time Customer Profile - Visualisez votre propre profil client en temps réel - interface utilisateur
jira: KT-5342
audience: Data Engineer, Data Architect, Marketer
doc-type: tutorial
activity: develop
feature: Profiles
exl-id: 4c810767-00ab-4cae-baa9-97b0cb9bf2df
source-git-commit: 5876de5015e4c8c337c235c24cc28b0a32e274dd
workflow-type: tm+mt
source-wordcount: '491'
ht-degree: 0%

---

# 1.2 Visualisation de votre propre profil client en temps réel - interface utilisateur

Au cours de cet exercice, vous vous connecterez à Adobe Experience Platform et afficherez votre propre profil client en temps réel dans l’interface utilisateur.

## Histoire

Dans Real-time Customer Profile, toutes les données de profil s’affichent avec les données d’événement, ainsi que les appartenances à l’audience existantes. Les données affichées peuvent provenir de n’importe où, des applications d’Adobe et des solutions externes. Il s’agit de la vue la plus puissante de Adobe Experience Platform, le véritable système d’enregistrement d’expérience.

## 1.2.1 Utilisation de la vue Profil client dans Adobe Experience Platform

Accédez à [Adobe Experience Platform](https://experience.adobe.com/platform). Une fois connecté, vous accédez à la page d’accueil de Adobe Experience Platform.

![Ingestion des données](./images/home.png)

Avant de continuer, vous devez sélectionner un **sandbox**. L’environnement de test à sélectionner est nommé ``Bootcamp``. Pour ce faire, cliquez sur le texte **[!UICONTROL Production Prod]** dans la ligne bleue en haut de votre écran. Après avoir sélectionné l’[!UICONTROL sandbox] approprié, vous verrez le changement d’écran et vous êtes désormais dans votre [!UICONTROL sandbox] dédié.



Dans le menu de gauche, accédez à **Profils** et à **Parcourir**.

![Profil client](./images/homemenu.png)

Dans le panneau Visionneuse de profils de votre site web, vous trouverez la présentation des identités. Chaque identité est liée à un espace de noms.

![Profil client](./images/identities.png)




Avec Adobe Experience Platform, tous les identifiants sont également importants. Auparavant, l’ECID était l’identifiant le plus important dans le contexte de l’Adobe et tous les autres identifiants étaient liés à l’ECID dans une relation hiérarchique. Avec Adobe Experience Platform, ce n’est plus le cas, et chaque ID peut être considéré comme un identifiant principal.

En règle générale, l’identifiant principal dépend du contexte. Si vous demandez à votre centre d&#39;appels, **Quel est l&#39;identifiant le plus important ?** ils répondront probablement, **le numéro de téléphone !** Mais si vous demandez à votre équipe de gestion de la relation client, ils répondront, **L&#39;adresse email !** Adobe Experience Platform comprend cette complexité et la gère à votre place. Chaque application, qu’elle soit Adobe ou non, parlera avec Adobe Experience Platform en se référant à l’identifiant qu’elle considère comme principal. Et ça marche tout simplement.

Pour le champ **Identity namespace**, sélectionnez **ECID** et, pour le champ **Identity Value**, saisissez l’ECID que vous pouvez trouver dans le panneau Visionneuse de profils du site web de bootcamp. Cliquez sur **Afficher**. Votre profil s’affiche alors dans la liste. Cliquez sur l’ **ID de profil** pour ouvrir votre profil.

![Profil client](./images/popupecid.png)

Vous voyez maintenant un aperçu de quelques **attributs de profil** importants de votre profil client.

![Profil client](./images/profile.png)

Accédez à **Événements**, où vous pouvez voir les entrées pour chaque événement d’expérience lié à votre profil.

![Profil client](./images/profileee.png)

Enfin, accédez à l’option de menu **Appartenance à une audience**. Vous verrez désormais toutes les audiences qui remplissent les critères de ce profil.

![Profil client](./images/profileseg.png)

Créons maintenant une nouvelle audience qui vous permettra de personnaliser l’expérience client pour un client anonyme ou un client connu.

Étape suivante : [1.3 Création d’une audience - IU](./ex3.md)

[Retour au flux utilisateur 1](./uc1.md)

[Revenir à tous les modules](../../overview.md)
