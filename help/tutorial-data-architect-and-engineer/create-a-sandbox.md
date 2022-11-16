---
title: Création d’un environnement de test
seo-title: Create a sandbox | Getting Started with Adobe Experience Platform for Data Architects and Data Engineers
breadcrumb-title: Création d’un environnement de test
description: Dans cette leçon, vous allez créer un environnement de test d’environnement de développement que vous pourrez utiliser pour le reste du tutoriel.
role: Data Architect, Data Engineer
feature: Sandboxes
kt: 4348
thumbnail: 4348-create-a-sandbox.jpg
exl-id: a04afada-52a1-4812-8fa2-14be72e68614
source-git-commit: cc7a77c4dd380ae1bc23dc75608e8e2224dfe78c
workflow-type: tm+mt
source-wordcount: '453'
ht-degree: 5%

---

# Création d’un environnement de test

<!--25min-->

Dans cette leçon, vous allez créer un environnement de test d’environnement de développement que vous utiliserez pour le reste du tutoriel.

Les environnements de test fournissent des environnements isolés dans lesquels vous pouvez tester la fonctionnalité sans mélanger les ressources et les données à votre environnement de production. Pour plus d’informations, voir [documentation des environnements de test](https://experienceleague.adobe.com/docs/experience-platform/sandbox/home.html?lang=fr).

**Architectes de données** et **Ingénieurs de données** Vous devrez créer des environnements de test en dehors de ce tutoriel.

Avant de commencer les exercices, regardez cette courte vidéo pour en savoir plus sur les environnements de test :
>[!VIDEO](https://video.tv.adobe.com/v/29838/?quality=12&learn=on)

## Autorisations requises

Dans le [Configuration des autorisations](configure-permissions.md) leçon, vous configurez tous les contrôles d’accès requis pour terminer cette leçon.

<!--
* Permission items **[!UICONTROL Sandbox Administration]** > **[!UICONTROL View Sandboxes]** and **[!UICONTROL Manage Sandboxes]**
* Permission item **[!UICONTROL Sandboxes]** > **[!UICONTROL Prod]**
* User-role access to the `Luma Tutorial Platform` product profile
* Admin-level access to the `Luma Tutorial Platform` product profile
-->

## Création d’un environnement de test

Créons un environnement de test :

1. Connectez-vous au [Adobe Experience Platform](https://experience.adobe.com/platform) interface
1. Accédez à **[!UICONTROL Environnements de test]** dans le volet de navigation de gauche
1. Sélectionner **[!UICONTROL Création d’un environnement de test]** en haut à droite
   ![Sélectionner Créer un environnement de test](assets/sandbox-createSandbox.png)

1. Sélectionner **[!UICONTROL Développement]** comme la propriété **[!UICONTROL Type]**
1. Nommer votre environnement de test `luma-tutorial` (pensez à ajouter votre nom à la fin)
1. Titre de votre tutoriel `Luma Tutorial` (pensez à ajouter votre nom à la fin)
1. Cliquez sur le bouton **[!UICONTROL Créer]**
   ![Création de votre environnement de test](assets/sandbox-nameSandbox.png)
   >[!NOTE]
   >
   >Bien que vous puissiez utiliser n’importe quelle valeur arbitraire pour votre nom et votre titre d’environnement de test, il est recommandé de respecter les valeurs suggérées, car nous nous référerons à ces étiquettes tout au long du tutoriel. Si plusieurs personnes de votre entreprise suivent ce tutoriel, pensez à ajouter votre nom à la fin du titre et du nom de l’environnement de test, par exemple luma-tutorial-ignatiusjreilly.

La création des environnements de test prend environ 30 secondes, au cours de laquelle un &quot;[!UICONTROL Création]&quot; s’affiche. Une fois l’environnement de test entièrement créé, il s’affiche sous la forme &quot;[!UICONTROL Principal]&quot;:
![État principal](assets/sandbox-active.png)

Patientez jusqu’à ce que votre environnement de test soit &quot;[!UICONTROL Principal]&quot; avant de poursuivre l’exercice suivant.

## Ajouter le nouvel environnement de test au profil de produit

Une fois l’environnement de test principal, vous devez l’inclure dans votre profil de produit pour pouvoir l’utiliser. Pour l’ajouter à votre profil de produit :

1. Dans un onglet de navigateur distinct, connectez-vous au [Admin Console](https://adminconsole.adobe.com)
1. Accédez à **[!UICONTROL Produits > Adobe Experience Platform]**
1. Ouvrez le `Luma Tutorial Platform` profile

   ![Sélection du profil de produit](assets/sandbox-selectProfile.png)

1. Accédez au **[!UICONTROL Autorisations]** tab

1. Sur le [!UICONTROL Environnements de test] ligne, sélectionnez **[!UICONTROL Modifier]**

   ![Sélectionnez Modifier](assets/sandbox-selectSandboxes.png)

1. _Supprimer_ la valeur **[!UICONTROL Prod]** environnement de test que vous avez affecté au profil d’origine
1. Sélectionnez la **[!UICONTROL +]** pour ajouter la nouvelle `Luma Tutorial` sandbox dans la colonne de droite
1. Sélectionner **[!UICONTROL Enregistrer]** pour enregistrer les autorisations mises à jour

   ![Déplacement de l’environnement de test vers l’autre colonne](assets/sandbox-addLumaTutorial.png)

1. Revenez à l’onglet du navigateur avec l’Experience Platform
1. Rechargez la page (ou rechargez-la en maintenant la touche Maj enfoncée). Vous devriez à présent : `Luma Tutorial` sandbox ou devrait apparaître dans la liste déroulante sandbox
1. Basculez vers le `Luma Tutorial` sandbox si vous n’y êtes pas déjà

   ![Confirmation du sandbox](assets/sandbox-confirmDropdown.png)

Super, vous avez créé votre environnement de test et êtes prêt à [Configuration de Developer Console et de Postman](set-up-developer-console-and-postman.md)!
