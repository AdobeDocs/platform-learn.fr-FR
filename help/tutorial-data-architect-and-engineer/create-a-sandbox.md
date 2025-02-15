---
title: Création d’un sandbox
seo-title: Create a sandbox | Getting Started with Adobe Experience Platform for Data Architects and Data Engineers
breadcrumb-title: Création d’un sandbox
description: Dans cette leçon, vous allez créer un sandbox d’environnement de développement que vous pourrez utiliser pour le reste du tutoriel.
role: Data Architect, Data Engineer
feature: Sandboxes
jira: KT-4348
thumbnail: 4348-create-a-sandbox.jpg
exl-id: a04afada-52a1-4812-8fa2-14be72e68614
source-git-commit: 286c85aa88d44574f00ded67f0de8e0c945a153e
workflow-type: tm+mt
source-wordcount: '398'
ht-degree: 2%

---

# Créer un sandbox

<!--25min-->

Dans cette leçon, vous allez créer un sandbox d’environnement de développement que vous utiliserez pour le reste du tutoriel.

Les sandbox fournissent des environnements isolés où vous pouvez tester les fonctionnalités sans mélanger les ressources et les données avec votre environnement de production. Pour plus d’informations, consultez la [documentation relative aux sandbox](https://experienceleague.adobe.com/docs/experience-platform/sandbox/home.html?lang=fr).

**Architectes de données** et **Ingénieurs de données** devront créer des sandbox en dehors de ce tutoriel.

Avant de commencer les exercices, regardez cette courte vidéo pour en savoir plus sur les sandbox :
>[!VIDEO](https://video.tv.adobe.com/v/29838/?learn=on&enablevpops)

## Autorisations requises

Dans la leçon [Configurer les autorisations](configure-permissions.md), vous allez configurer tous les contrôles d’accès requis pour suivre cette leçon.

<!--
* Permission items **[!UICONTROL Sandbox Administration]** > **[!UICONTROL View Sandboxes]** and **[!UICONTROL Manage Sandboxes]**
* Permission item **[!UICONTROL Sandboxes]** > **[!UICONTROL Prod]**
* User-role access to the `Luma Tutorial Platform` product profile
* Admin-level access to the `Luma Tutorial Platform` product profile
-->

## Création d’un sandbox

Créons un sandbox :

1. Connectez-vous à l’interface de [Adobe Experience Platform](https://experience.adobe.com/platform)
1. Accédez à **[!UICONTROL Sandbox]** dans le volet de navigation de gauche
1. Sélectionnez **[!UICONTROL Créer un sandbox]** en haut à droite
   ![Sélectionnez Créer un sandbox](assets/sandbox-createSandbox.png)

1. Sélectionnez **[!UICONTROL Développement]** comme **[!UICONTROL Type]**
1. Nommez votre sandbox `luma-tutorial` (envisagez d’ajouter votre nom à la fin)
1. Donnez un titre à votre `Luma Tutorial` de tutoriel (pensez à ajouter votre nom à la fin).
1. Sélectionnez le bouton **[!UICONTROL Créer]**
   ![Créer votre sandbox](assets/sandbox-nameSandbox.png)
   >[!NOTE]
   >
   >Bien que vous puissiez utiliser n’importe quelle valeur arbitraire pour le nom et le titre de votre sandbox, il est recommandé de respecter les valeurs suggérées, car nous nous référerons à ces libellés tout au long du tutoriel. Si plusieurs personnes au sein de votre organisation suivent ce tutoriel, pensez à ajouter votre nom à la fin du titre et du nom du sandbox, par exemple luma-tutorial-ignatiusjreilly.

La création des sandbox prend environ 30 secondes, période pendant laquelle un statut « [!UICONTROL Création] » s’affiche. Une fois le sandbox entièrement créé, il s’affiche sous la forme « [!UICONTROL  Actif ] :
![Statut actif](assets/sandbox-active.png)

Attendez que votre sandbox soit « [!UICONTROL  actif ] avant de passer à l’exercice suivant.

## Ajouter le nouveau sandbox au rôle

Une fois que le sandbox est actif, vous devez l’inclure dans votre rôle pour pouvoir l’utiliser. Pour l’ajouter à votre rôle (privilèges Administrateur système ou Administrateur de produit requis) :

1. Accédez à l’écran [!UICONTROL  Autorisations ]
1. Ouvrir le rôle `Luma Tutorial Platform`
1. Vous pouvez _supprimer_ le sandbox `Prod` du rôle
1. Ajouter le sandbox `Luma Tutorial`
1. Sélectionnez **[!UICONTROL Enregistrer]**
1. Sur la ligne [!UICONTROL Sandbox], sélectionnez **[!UICONTROL Modifier]**

   ![Ajout du tutoriel Luma](assets/sandbox-addLumaTutorial.png)

1. Rechargez (ou cliquez sur Maj pour recharger) la page. Vous devriez maintenant être dans le sandbox `Luma Tutorial` ou elle devrait apparaître dans la liste déroulante sandbox
1. Basculez vers le sandbox `Luma Tutorial` si vous ne l’avez pas déjà fait

   ![Confirmer la sandbox](assets/sandbox-confirmDropdown.png)

Très bien, vous avez créé votre sandbox et êtes prêt à [Configurer Developer Console et Postman](set-up-developer-console-and-postman.md) !
